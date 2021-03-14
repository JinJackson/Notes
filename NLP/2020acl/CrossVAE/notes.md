# Crossing Variational Autoencoders for Answer Retrieval

**Conference:** 2020 ACL

**arxiv**:

**idea:**VAE



### Model Arcitecture

![image-20210314111755060](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111755060.png)

+ 图(a)为传统的孪生网络结构，也称为‘Dual Encoder’结构，即双Encoder结构，使用两个**独立**的编码器对问题和答案进行分别编码

+ 图(b)为双VAE结构，即‘Dual-VAEs’结构，通过两个**独立**的VAE分别得到隐状态$Z_q$和$Z_a$，对两个隐状态进行概率估计$p(Y|Z_q,Z_a)$
+ 图(c)为本文提出的交叉VAE模型，试图通过Q的隐状态$Z_q$重构成答案A，通过A的隐状态$Z_a$重构问题Q，让$Z_q$与$Z_a$中保留对齐语义，通过这种方式来进行概率估计$p(Y|Z_q,Z_a)$

### How to train?
+ ##### 第一部分：VAE重构损失

  式(1)表示用答案a进入Encoder($E_a$)得到隐状态$Z_a$，并用$Z_a$生成问题q

  式(2)表示用问题q进入Encoder($E_q$)得到隐状态$Z_q$，并用$Z_q$生成答案a
  ![image-20210314111823104](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111823104.png)

  记两个解码器分别为$D_q$和$D_a$，得到两个VAE的重构损失为：
  ![image-20210314111904259](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111904259.png)

  

+ ##### 第二部分：KL散度作为正则化

  变分自编码器采用KL散度正则化器来对齐后验概率$PE(z_q|q)$和概率$PE(z_a|a)$:
  ![image-20210314111917862](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111917862.png)

  其中，PE代表后验概率，$\theta_E$和$\theta_D$是需要优化的参数

+ ##### 第三部分：匹配结果损失

  匹配结果损失即交叉熵：
  ![image-20210314111929738](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111929738.png)

+ ##### 损失结果：
  ![image-20210314111938636](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210314111938636.png)
  
  其中，$\alpha,\beta,\gamma$为超参数
