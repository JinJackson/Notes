# 对抗训练FGM

全称：Fast Gradient Method

来源：《Explaining and Harnessing Adversarial Examples》

地址：https://arxiv.org/abs/1412.6572

作者 : GAN之父goodfellow



## 贡献：

在这篇论文中，Goodfellow等人对现有的工作进行了一个全面的总结，更重要的是，这篇论文：

1. 解释了神经网络对干扰表现脆弱的原因是**神经网络的线性**（而早期的解释是对抗样本的原因是非线性和过拟合） 
2. 论文中设计了一种快速生成adversarial examples的方法（**Fast Gradient Sign Method**），这个方法被之后的工作所广泛采用



## 思想：

由于Input feature的精度是有限的，当添加的干扰 ![[公式]](https://www.zhihu.com/equation?tex=%5Ceta) 对于Input真正的信息来说微不足道的时候，样本 ![[公式]](https://www.zhihu.com/equation?tex=x) 和对抗样本 ![[公式]](https://www.zhihu.com/equation?tex=%5Ctilde%7Bx%7D) （ ![[公式]](https://www.zhihu.com/equation?tex=%5Ctilde%7Bx%7D%3Dx%2B%5Ceta) ）不应当被分类器错分。即借用对抗样本，增强模型鲁棒性。所以我们希望样本 ![[公式]](https://www.zhihu.com/equation?tex=x) 和对抗样本 ![[公式]](https://www.zhihu.com/equation?tex=%5Ctilde%7Bx%7D)在扰动$\parallel \eta \parallel_{\infin} < \epsilon$，其中$\epsilon$是一个足够小的数，甚至可以被丢弃。

![image-20201019112223865](D:\Dev\typoraspace\notes\NLP\techs\对抗训练\panda_eg.png)



## 生成对抗样本的方法

+ ### Fast Gradient Sign Method

  假设有一个模型，它的参数是 ![[公式]](https://www.zhihu.com/equation?tex=%5Ctheta) ，输入是 ![[公式]](https://www.zhihu.com/equation?tex=x%2Cy) 目标， ![[公式]](https://www.zhihu.com/equation?tex=J%28%5Ctheta%2Cx%2Cy%29) 是神经网络的损失函数。在目前的 ![[公式]](https://www.zhihu.com/equation?tex=%5Ctheta) 值，局部上可以将函数近似为线性，使用FGSM（Fast Gradient Sign Method），我们得到一个最优的扰动。以下这张图片展示了如何利用FGSM对熊猫图片施加干扰让其被识别为长臂猿：

  扰动$\eta$的计算方法

  ![image-20201019112450010](C:\Users\jackson.DESKTOP-QEOIPSL\AppData\Roaming\Typora\typora-user-images\image-20201019112450010.png)

  即，对抗样本$\hat{x} = x + \eta$

  解释：

  > 常规的分类模型训练在更新参数时都是将参数减去计算得到的梯度，这样就能使得损失值越来越小，从而模型预测对的概率越来越大。既然无目标攻击是希望模型将输入图像错分类成正确类别以外的其他任何一个类别都算攻击成功，那么只需要损失值越来越大就可以达到这个目标，也就是模型预测的概率中对应于真实标签的概率越小越好，这和原来的参数更新目的正好相反。因此我只需要在输入图像中加上计算得到的梯度方向，这样修改后的图像经过分类网络时的损失值就比修改前的图像经过分类网络时的损失值要大，换句话说，模型预测对的概率变小了。这就是FGSM算法的内容，一方面是基于输入图像计算梯度，另一方面更新输入图像时是加上梯度，而不是减去梯度，这和常见的分类模型更新参数正好背道而驰。  前面我们提到之所以采用梯度方向而不是采用梯度值是为了控制扰动的L∞距离，这只是其中的一部分。在Figure1中，梯度方向前一般会有一个权重参数e，这个权重参数可以用来控制攻击噪声的幅值，参数值越大，攻击强度也越大，肉眼也更容易观察到攻击噪声（因为输入图像归一化成0到1，所以图中e值只有0.07，换算成0到255的话差不多18个像素值），因此最终的攻击噪声就如下所示。因为FGSM算法的攻击噪声幅值评价指标是L∞，因此权重参数e和梯度方向就可以控制每个像素的最大变化值。

+ ### Fast Gradient Method

  

