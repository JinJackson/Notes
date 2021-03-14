# Compare-Aggregate

题目：A COMPARE-AGGREGATE MODEL FOR MATCHING TEXT SEQUENCES

## 摘要：

1. 提出来一种较为通用的compare-aggregate框架，该框架先进行词级别的匹配，然后使用CNN进行聚合。
2. 主要用两种不同的比较函数去匹配两个向量。发现一些基于元素运算的简单比较函数（simple comparison functions）比一些标准的网络或者神经张量网络能更好的工作。
3. 使用四种不同的数据集进行评价模型的性能。

***

## Introduction

**传统的深度学习模型：**

> 首先对句子进行embedding,得到embedding vector,然后通过RNN或者CNN将其encoder。
>
> 然后，为了匹配两个序列，最直接的方法就是将每个句子的encoder看作向量来比较。
>
> **缺点：**用单一的vector去encode整个句子并不十分有效，因此又出现了**attention机制、记忆网络**等

**“compare-aggregate”框架：**

> 最早由Google在《A Decomposable Attention Model for Natural Language Inference》论文中提出来。
>
> 这类方法主要是先对小单元的vector进行比较，然后再将比较的结果进行聚合，做最后的判断。
>
> **eg.**
>
> **match-LSTM：**在进行文本蕴含的时候，首先将假设中的每个单词与前提的注意加权进行比较，然后将比较的结果通过LSTM进行聚合
>
> **交互模型：**从两个句子里找出一对单词，然后进行单元比较。最后使用相似层和多层CNN将这些单词交互的结果组合在一起
>
> **可分解attention模型：**每个句子中的单词都和其他句子进行attention加权计算，产生一系列的比较向量，然后进行聚合加MLP进行最后的分类

以上的研究都展示了“**compare-aggregate**”框架的有效性，但是存在两点限制：提出来的每个模型都只会用于一种或两种任务； 这些研究并没有重视比较两个小文本单元的比较功能。即本质上是要去关注两个序列在语义上的相似度，进行序列的小元素的比较只为了选择出更加合适的比较函数。

## 本文贡献：

- 提出了统一的“compare-aggregate”框架，能有效应用于句子匹配任务上

- 用四种不同的数据集，分别是代表不同的任务，在其上进行了六种不同的比较函数的测试，最终发现基于元素的减法和乘法，结果最好

## 模型结构

![image-20201011154747656](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\模型结构.png)

### 主要分为四层：
#### Step1.Preprocessing:

> 首先对Q和A进行预处理，获得两个新的矩阵$\bar{Q}:$和 $\bar{A}$，其目的是为每个序列中的每个单词获得一个新的embedding vector，使每个词都能获得句子的上下文信息。
> 比如$\bar{Q}$里面的$\bar{q_i}$是$\bar{Q}$的第$i^{th}$列向量，是通过对 $\bar{Q}$中的第$i^{th}$个字及其在Q中的上下文进行编码。具体公式如下：
>
> <img src="D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\Q和A的preprocess.png" alt="在这里插入图片描述" style="zoom: 67%;" />
>
> 其中：$\bigotimes$表示把$b^i$重复，类似于广播
>
> 原文表示为：这是将Q和A经过一个modified的LSTM/GRU，通过这种方式，使得$ \bar{Q}$和$ \bar{A}$记得句子里的有用信息。

```python
function compAggWikiqa:new_proj_module()
    local input = nn.Identity()()
    local i = nn.Sigmoid()(nn.Linear(self.emb_dim, self.mem_dim)(input))  
    local u = nn.Tanh()(nn.Linear(self.emb_dim, self.mem_dim)(input))
    local output = nn.CMulTable(){i, u}
    local module = nn.gModule({input}, {output})
    if self.proj_module_master then
        share_params(module, self.proj_module_master)
    end
    return module
end
```

#### Step2.Attention:

就是传统的attention机制

![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\注意力机制.png)

用问题对答案做attention，可以得到权重矩阵G，即$ \bar{A} $和$\bar{Q}$的注意力权重

然后将$\bar{Q}$作为V，即$\bar{Q}$的每个列向量$\bar{q_j}$和G的列向量相乘，得到对应的表示$h_j$

```python
function compAggWikiqa:new_att_module()
    local linput, rinput = nn.Identity()(), nn.Identity()()
    --padding
    local lPad = nn.Padding(1,1)(linput)
    --local M_l = nn.Linear(self.mem_dim, self.mem_dim)(lPad)
    local M_r = nn.MM(false, true){lPad, rinput}
    local alpha = nn.SoftMax()( nn.Transpose({1,2})(M_r) )
    local Yl =  nn.MM(){alpha, lPad}
    local att_module = nn.gModule({linput, rinput}, {Yl})
    if self.att_module_master then
        share_params(att_module, self.att_module_master)
    end
    return att_module
end
```

#### Step3.Comparison:

将答案信息$\bar{a_j}$与$h_j$进行比较得到新的向量表示$t_j$，作者比较了多种comparison方式。其实就是找出来一个最好的函数，即论文里所谓的comparison layer。

+ Neuralnet:将两个向量进行拼接，过层神经网络。

  ![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\NeuralNet.png)

+ Neuraltensornet: 用张量网络连接两个向量，过relu.

  ![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\NeuralTensorNet.png)
  
+ EUCLID+COS:

  作者发现在很多论文里，使用的最好的就是欧氏距离和cosine相似度，因此又将两者的结果拼接起来：

  ![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\EuclidCos.png)

  【注】：但是作者觉得，这样结合还是会导致这两个原始的vector里面会丢失很多有用的信息，因此考虑到了利用这两个vector里面的元素直接进行计算，于是就提出了下面的两个比较函数：

+ SUB&MULT:

  ![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\sub&multi.png)

  【注】：然后作者还发现sub的计算方法和欧氏距离很相近，mul又比较接近于cosine.因此，又对这两个比较方式的结果进行拼接，过一层神经网络：
  
+ SUBMULT+NN:

  ![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\SubMult+NN.png)

#### Step4:Aggregation

最后得到了一系列的$t_j$，用CNN聚合即可：

![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\CNN聚合.png)

最后利用向量**r**，根据不同的任务对模型进行训练和预测。文本蕴含做三分类，答案选择任务，则是从多个候选答案中选择正确答案。

# 3. Experiments

word embedding: GloVe 在GloVe里面没有的直接初始化为0
 hidden layer = 150
 optimize： adamax$\beta _1$  =0.9 , $\beta _2$ = 0.999
 batch_size: 30
 lr = 0.002

下面就在这四种数据集上进行了相关实验：

![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\exp1.png)

![在这里插入图片描述](D:\Dev\typoraspace\notes\NLP\Text_Matching\2017Compare-Aggregate\imgs\exp2.png)