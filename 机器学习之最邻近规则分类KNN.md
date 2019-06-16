
@[TOC](目录)

 * * *

## 1.什么是KNN(k-nearest neighbor)?
K最近邻(K-Nearest Neighbor,KNN)算法，是著名的模式识别统计学方法，在机器学习分类算法中占有相当大的地位。它是一个理论上比较成熟的方法。既是最简单的机器学习算法之一，也是基于实例的学习方法中最基本的，又是最好的文本分类算法之一。
## 2. 基本思想
如果一个实例在特征空间中的K个最相似（即特征空间中最近邻）的实例中的大多数属于某一个类别，则该实例也属于这个类别。所选择的邻居都是已经正确分类的实例。
该算法假定所有的实例对应于N维欧式空间Ân中的点。通过计算一个点与其他所有点之间的距离，取出与该点最近的K个点，然后统计这K个点里面所属分类比例最大的，则这个点属于该分类。
一张图助你理解：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610121649106.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
该算法涉及3个主要因素：实例集、距离或相似的衡量、k的大小。
一个实例的最近邻是根据标准欧氏距离定义的。更精确地讲，把任意的实例x表示为下面的特征向量：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610112521360.png#pic_center)
## 3.算法详述
为了判断未知实例的类别，以所有 已知类别的实例作为参照
选择参数K
计算 未知实例与已知实例的距离
选择K个最近的已知实例
根据少数服从多数的投票法则(majority-voting),让未知实例归类为K个最近临近样本中最多数的类别
## 4. 例子
以下由打斗次数和接吻次数的数据集以及对应的电影类型，预知在某一打斗次数和接吻次数条件下应该归为哪一类 ：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610121814541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
把训练集虚拟成向量（点集）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610122400660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
计算G点与所有点的距离：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610122529229.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061012255619.png#pic_center)
若给定的K值为3，则选择最小的3个距离 的点：a,b,c
在a,b,c中投票选取最大概率出现的类型：Romance
所以G的归类应该是Romance
## 5. K值选取对归类的影响
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190610123316140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
根据K值的不同讨论绿色点的归类：

 - K=1：最近的1个是蓝色，且距离的结果集中只有一个（1：0），归类为蓝色
 - K=4：最近的4个为内实圈中的4个，投票结果是红色（3：1），归类为红色
 - k=9：最近的9个为外虚圈内的9个，投票结果为红色（6：3），归类为红色

选取不同的K值对归类结果存在影响，可以通过增大K值减少噪音（最好选取奇数）

## 6. 小结
**优点**：简单，易于理解，容易实现，通过对K的选择可具备丢噪音 数据的健壮性
**缺点**：需要大量的空间来存储所有已知的 实例；算法复杂度高（需要比较所有已知的实例和要分类的实例）；当样本分布不平衡时，比如其中一类样本过大占主导的时候，新的实例可能被归为这个主导样本，因为这类样本实例的数量过大，但是这个新的未知实例并未接近目标样本：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061012482680.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
上图Y本属于红类，单由于 蓝色的样本数量过大，结果将Y归为蓝色（主导地位）
**改进**：考虑距离，增加权重，即距离小的权重比较大
