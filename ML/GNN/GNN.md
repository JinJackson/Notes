# GNN 图神经网络



## 1.图神经网络

图神经网络是针对一些图结构数据设计的网络



## 2.模型结构：

![image-20201110145011623](D:\Dev\typoraspace\notes\ML\GNN\imgs\模型结构.png)

上图中的**节点**表示**对象或概念**，**边**表示它们之间的**关系**。 每个概念自然都有其特点及相关概念，所以基于每个节点的邻居节点的信息引入 **$x_n$表示**，我们在本文中称之为**n的全局表示**,因为他是综合了相邻节点的信息。

定义$ f_w$状态局部转移函数，$g_w$是局部输出函数描述输出的产生。有如下表示

![image-20201110145410773](D:\Dev\typoraspace\notes\ML\GNN\imgs\fun1.png)

其中：$l_n$表示节点n的特征表示 	$l_{co[n]}$表示相邻边的特征向量	  $ x_{ne[n]}$表示节点n相邻节点的全局表示	表示节点n相邻节点的特征向量	$ x_n$和 $o_n$考虑信息的传递是由相邻节点通过相邻边传过来的

![image-20201110150242591](D:\Dev\typoraspace\notes\ML\GNN\imgs\定理1.png)

![image-20201110151548853](D:\Dev\typoraspace\notes\ML\GNN\imgs\3.png)

![image-20201110151621738](D:\Dev\typoraspace\notes\ML\GNN\imgs\4.png)

![image-20201110151653864](D:\Dev\typoraspace\notes\ML\GNN\imgs\学习1.png)

![image-20201110151729613](D:\Dev\typoraspace\notes\ML\GNN\imgs\学习2.png)

![image-20201110151801885](D:\Dev\typoraspace\notes\ML\GNN\imgs\学习3.png)

![image-20201110151819477](D:\Dev\typoraspace\notes\ML\GNN\imgs\学习4.png)