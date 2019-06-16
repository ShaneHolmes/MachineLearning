
@[TOC](目录)


K-means聚类算法属于非监督学习(unsupervised learning)，即训练集无类别标记，详情见[前言](https://blog.csdn.net/qq_33208851/article/details/91354105)
***
## 1. 算法思想
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615112929241.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
样本数据没有分类，例如体现为上图中的点。根据点的分布，可以将这些点划分为不同的簇cluster。划分好的cluster满足聚类中的对象相似度较高，而不同的聚类中的对象的相似度较小。这些数据划分为K个聚类，其中K是由我们自己指定的值。所以我们要一开始就指定K值，以空间中K个随机的点为中心进行聚类，对其他的点分别计算到达这K个点的距离，并将那些点归为距离最小的那一类。然后利用均值等方法更新每一个类（K个）的中心值。通过迭代的方法，逐步更新各个聚类中心，直至得到最好的聚类结果
## 2. 算法描述
 （1）. 适当选择K个类的初始中心（随机？）
 （2）. 对任意一个样本，求出其到各个中心的距离，将样本归到距离最短的中心所在的类
 （3）. 利用均值等方法更新该类的中心值
 （4）. 对于所有的K个聚类中心，如果利用（2）（3）的迭代更新后结果保持不变，那么迭代结束，否则继续迭代
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615115446876.png#pic_center)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615115638705.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
## 3. 应用实例
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615120756468.png#pic_center)
对以上样本分成K=2的两类（初始选的center：c1,c2分别是（1，1），（2，1），下图中的五角星）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615120831164.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615121946996.png#pic_center)
上图中，D矩阵中
d11=0：  （1，1）点到（1，1）点的距离
d12=1：  （2，1）点到（1，1）点的距离
d13=3.61:（4，3）点到（1，1）点的距离
d14=5： （5，4）点到（1，1）点的距离
d21=1：  （1，1）点到（2，1）点的距离
d22=0：  （2，1）点到（2，1）点的距离
d23=0.283:（4，3）点到（2，1）点的距离
d24=4.24： （5，4）点到（2，1）点的距离
竖着比较：
d11<d21,点（1，1）属于类1；
d12>d22,d13>d23,d14>d24，点（2，1），（4，3），（5，4）均属于类2
分类情况如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122003430.png#pic_center)
重新计算中心点c1,c2：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122239971.png#pic_center)
新的中心点如下图（五角星）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122306103.png#pic_center)
再计算各个点距离中心点c1,c2的距离（矩阵D）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122539372.png#pic_center)
根据距离远近重新分类：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122602851.png#pic_center)
计算新的中心点c1,c2：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122636987.png#pic_center)
新的中心点如下图（五角星）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122658813.png#pic_center)
再计算各个点距离中心点c1,c2的距离（矩阵D）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122727597.png#pic_center)
根据距离远近重新分类结果（没有改变）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122753702.png#pic_center)
停止
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190615122957829.png#pic_center)
## 4. 小结
优点：速度快，简单
缺点：最终结果跟初始选择点有关，容易陷入局部最优，需要K值
