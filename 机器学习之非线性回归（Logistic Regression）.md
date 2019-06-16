
@[TOC](目录)

 * * *

## 1. 线性回归存在的问题
（为什么举这个例子？逻辑回归为什么Y是0，1分类。。。哎，咱也不知道，咱也不敢问）假设肿瘤的良（0）恶（1）性与肿瘤尺寸大小（tumor size）有如下关系：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061420524429.png#pic_center)
某一尺寸大小的肿瘤均划分成了良性、恶性，其划分Malignant可能等于0.5。但是当加入一个尺寸很大的样本时：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614205544520.png#pic_center)
为了拟合所有数据，回归线将发生变化，如果Malignant仍然等于0.5，那么将会出现一部分先前划分为恶性肿瘤的样本被划分成良性（因为尺寸大小小于Malignant=0.5对应的tumor size），所以我们就只能将Malignant的值进行调整
## 2. Logistic Regression基本模型
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614212056242.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
**逻辑回归公式**：
引入Sigmoid函数使曲线平滑化：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614212558403.png#pic_center)
其中，g为决策值，z=θx+b，x为特征值，e为自然对数
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614213657247.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
该函数是一条S形的曲线，并且曲线在中心点附近的增长速度较快，在两段的增长速度较慢。w值越大，曲线中心的增长速度越快。从图上可知，Y的值域为(0,1)，那么就可以将决策函数值大于等于0.5的具有对应x属性的对象归为正样本，决策函数值小于0.5的具有对应x属性的对象归为负样本。这样就可以对样本 数据进行二分类。
**预测函数**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214159899.png#pic_center)
可用**概率表示**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614215038660.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
这是条件概率，在给定X，θ的条件下，y=1发生的概率

**损失函数**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614221225107.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614221253979.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614221550586.png#pic_center)
该直线使得红点与预测值（红点x在直线上的值）的差值的平方之和最小，即找到合适的θ0，θ1使得上式之和最小

## 3. 逻辑回归推导
逻辑回归是一种简单，常见的二分类模型，通过输入未知类别对象的属性特征序列得到对象所处的类别。由于Y(x)是一个概率分布函数，因此对于二分类而言，离中心点的距离越远，其属于某一类的可能性就越大。
对于常见二分类，逻辑回归通过一个区间分布进行划分，即如果Y值大于等于0.5,则属于正样本，如果Y值小于0.5，则属于负样本，这样就可以得到逻辑回归模型，判别函数如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614220701190.png#pic_center)
在模型参数w与b没有确定的情况下，模型是无法工作的，因此接下来就是在实际应用期间最重要的是模型参数w和b的估计。
其代价函数为（这里的Y(x)为h(x)=θ0+θ1X）：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614220846720.png#pic_center)
给定y值为1时，代价函数曲线横坐标为决策函数Y(x)的值越接近1，则代价越小,反之越大。当决策函数Y(x)的值为1时，代价为0。类似的，当给定y值为0时有同样的性质。
如果将所有m个样本的代价累加并平均，就可以得到最终的代价函数：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614220919556.png#pic_center)
由于y的取值为0或1，结合上面两个公式可以得到：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061422094199.png#pic_center)
这样就得到了样本的总的代价函数，代价越小表明所得到模型更符合真实模型。当损失函数最小的时候，就得到了所求参数。
**梯度下降解法**：
关于损失函数的求解，可以通过梯度下降法求解，先设置一个学习率。从1到n，更新：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614221007790.png#pic_center)
其中更新法则为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614221027734.png#pic_center)
重复更新步骤，直到代价函数的值收敛为止。对于学习率的设定，如果过小，则可能会迭代过多的次数而导致整个过程变得很慢；如果过大，则可能导致错过最佳收敛点。所以，在计算过程中要选择合适的学习率。
## 4. 应用实例
以下为研究一个学生优秀还是差等的问题，已知训练数据的学生基本特征信息如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614222526125.png#pic_center)
需要分类学生数据：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614222615862.png#pic_center)
步骤一：
整理数据，转化为数学模型
将分数归一化，除以10，将评级优表示为1，评级差表示为0，则转化为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614222737737.png#pic_center)
步骤二：
假设Y(x)为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614222858589.png#pic_center)
求出此时的损失函数，同时初始值设置为（0.5,0.5,0.5,0.5),学习率为0.3，并且设置损失函数为0.1时，迭代停止截止。
步骤三：
第一次迭代的值为（-0.096，0.50008，-0.32，0.350858），不断迭代，直到损失函数小于0.1.
步骤四：
最终就能求出Y(x）的表达式，从而能够分类上面的数据：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061422302571.png#pic_center)
参考连接：[https://baijiahao.baidu.com/s?id=1628902000717534995&wfr=spider&for=pc](https://baijiahao.baidu.com/s?id=1628902000717534995&wfr=spider&for=pc)
## 5. python实现代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061422341383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614223514918.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
