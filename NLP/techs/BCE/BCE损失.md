# BCELoss和BCEWithLogitsLoss

## 1.BCELoss



如果3张图片分3类，会输出一个3*3的矩阵。

<img src="D:\Dev\typoraspace\notes\NLP\imgs\BCE\inputs" alt="在这里插入图片描述" style="zoom: 50%;" />

先用Sigmoid给这些值都搞到0~1之间：

<img src="D:\Dev\typoraspace\notes\NLP\imgs\BCE\sigmoid" alt="img" style="zoom:50%;" />

假设Target是：

<img src="D:\Dev\typoraspace\notes\NLP\imgs\BCE\target.png" alt="在这里插入图片描述" style="zoom: 50%;" />

![image-20201002153521731](D:\Dev\typoraspace\notes\NLP\imgs\BCE\计算过程.png)

<img src="D:\Dev\typoraspace\notes\NLP\imgs\BCE\验证" alt="在这里插入图片描述" style="zoom:50%;" />

## BCEWithLogitsLoss

BCEWithLogitsLoss就是把Sigmoid-BCELoss合成一步。我们直接用刚刚的input验证一下是不是0.7193：

<img src="D:\Dev\typoraspace\notes\NLP\imgs\BCE\BCEwithLogits" alt="在这里插入图片描述" style="zoom:50%;" />