# TANDA

题目：**T**AND**A: Transfer and Adapt Pre-Trained Transformer Models for Answer Sentence Selection**

地址：https://arxiv.org/pdf/1911.04118.pdf



## 任务定义：

- **AS2任务：**

给定问题 q 和答案句子库 S={s1,...,sn}，AS2 任务目的是找到能够正确回答 q 的句子 s_k，r(q,S)=s_k，其中 k=argmax p(q,s_i)，使用神经网络模型计算 p(q,s_i)。

## **动机**

这篇文章聚焦的是问答系统（Q&A）中的一个问题：回答句子选择（Answer  Sentence Selection，AS2），给定一个问题和一组候选答案句子，选择出正确回答问题的句子（例如，由搜索引擎检索）。AS2  是目前虚拟客服中普遍采用的技术，例如 Google Home、Alexa、Siri 等，即采用搜索引擎+AS2 的模式。

## **贡献**

（1）本文提出了一种用于自然语言任务的预训练变换模型精调的有效技术-TANDA(  Transfer AND  Adapt)。首先通过使用一个大而高质量的数据集对模型进行精调，将一个预先训练的模型转换为一个用于一般任务的模型。然后，执行第二个精调步骤，以使传输的模型适应目标域

（2）构建了一个应用于 AS2 的数据库 ASNQ（Answer Sentence Natural Questions）。

## 模型结构

![image-20201105165346567](D:\Dev\typoraspace\notes\NLP\Text_Matching\2019TANDA\imgs\model.png)

**基于Transformer进行AS2任务**

<img src="D:\Dev\typoraspace\notes\NLP\Text_Matching\2019TANDA\imgs\transformer-based.png" alt="image-20201105165538290" style="zoom: 80%;" />

输入包括两条文本，由三个标记 [CLS]、[SEP] 和 [EOS]  分隔。将根据令牌、段及其位置编码的嵌入向量作为输入，输入到transformer模型中。输出为向量 x，x  描述单词、句子分段之间的依赖关系，应该是[CLS]的输出结果。将 x 输入到全连接层中，输出层用于最终的任务。



## TANDA

在经典的任务中，一般只针对目标任务和域进行一次模型精调。对于AS2，训练数据是由问题和答案组成的包含正负标签（答案是否正确回答了问题）的句子对。当训练样本数据较少时，完成 AS2  任务的模型稳定性较差，此时在新任务中推广需要大量样本来精调大量Transformer参数。本文提出，将精调过程分为两个步骤：转移到任务，然后适应目标域。

首先，使用 AS2 的大型通用数据集完成标准的精调处理。这个步骤应该将语言模型迁移到具体的 AS2 任务。由于目标域的特殊性（AS2），所得到的模型在目标域的数据上无法达到最佳性能，此时采用第二个精调步骤使分类器适应目标域。



## ASNQ

本文构建了一个专门适用于 AS2 任务的通用数据库 ASNQ。ASNQ 基于经典 NQ 语料库建设，NQ 是用于机器阅读（Machine Reading，MR）任务的语料库，其中每个问题与一个 Wiki 页面关联。



## 实验

不同模型在WikiQA数据集上的性能如下图所示：

<img src="D:\Dev\typoraspace\notes\NLP\Text_Matching\2019TANDA\imgs\result1.png" alt="img" style="zoom:67%;" />

不同模型在trec - qa数据集上的性能如下图所示：

<img src="D:\Dev\typoraspace\notes\NLP\Text_Matching\2019TANDA\imgs\result2.png" alt="img" style="zoom:67%;" />

## 总结

本文的工作将经典的精调（fine-tuning）过程拆成了两次，其中一次针对通用数据集，另一次针对目标数据集，此外，还专门构建了适用于AS2任务的通用数据集ASNQ。本文在两个著名的实验基准库：WikiQA和TREC-QA上进行实验，分别达到了 92% 和 94.3% 的 MAP 分数，超过了近期获得的 83.4% 和 87.5% 的最高分数。本文还讨论了 TANDA  在受不同类型噪声影响的 Alexa 特定数据集中的实验，确认了 TANDA 在工业环境中的有效性。