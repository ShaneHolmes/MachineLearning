
@[TOC](目录)

 * * *

## 1.什么是SVM?
SVM(Support Verctor Machine)支持向量机，最常拿来就是做分类。也就是说，如果我有一堆已经分好类的东西（可是分类的依据是未知的），那当收到新的东西时，SVM可以预测新的数据要分到哪一堆去。支持向量机通过求得一个划分超平面来划分两类不同的数据样本，把正例放在一边，反例放在一边。它是一类按监督学习（supervised learning）（训练集有类别标记的为监督学习，[分类详情](https://blog.csdn.net/qq_33208851/article/details/91354105)）方式对数据进行二元分类（binary classification）的广义线性分类器（generalized linear classifier），其决策边界是对学习样本求解的最大边距超平面（maximum-margin hyperplane）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612100812711.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
以上黑线可加强为一根棍子，使得棍子的直径最大，这样即使存在局部扰动，依旧可以达到一定的划分效果


## 2. 基本思想
支持向量机要做的就是寻找一个划分超平面使得离它最近的两个异类样本到该平面的距离之和最大，反映到上图就是找到一条直线进行划分，并且这根线可以变粗，可以长到最粗的那根线就可以作为划分超平面了
线性描述如下：
如果所有样本都正确分类，就有对于正类样本 Wx+b>0，异类样本 Wx+b<0  其中W ={w1,w2,w3......}所对应的额列向量
通过对W 和 b 进行适当地放缩就可以使得对于正类样本 Wx+b>=1,异类样本Wx+b<=-1；如果有训练样本使得上式的等号成立的话它就是我们要寻找的支持向量。支持向量之间的距离就是就是我们要寻找的最大的间隔，就是2/||W||，||W||=w1^2+W2^2+W3^2+...。所以我们就是要在划分正确地基础上使得划分间隔最大，这就是支持向量机的模型
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061212365622.png#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061212371039.png#pic_center)
总共可以有无数可能的超平面
如何选取使边际（margin）最大的超平面（Max Margin Hyperplane，MMH）？
如上图所示，超平面一侧最近点的距离等于到另一侧最近点的距离，两侧的超平面平行
## 3. 线性区分性
**线性可区分（linear separable）**：在上图中能够找到超平面，完全将两类区分，此类为线性可区分
**线性不可区分（linear inseparable）**：不能找到超平面，完全将两类区分，此类为线性可区分。如下图：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612125511666.png#pic_center)
注：划分超平面后，有红点在蓝色部分，有蓝点在红色部分
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612125629967.png#pic_center)
注：此种划分为非线性划分

## 4. 数学定义及公式
超平面可定义为：

```
W*X+b=0
```
其中，**W**：weight vector 
**W**={w1,w2,...,wn},n是特征值的个数，1·n维
**X**：训练实例，n·1维
b：bias偏差
将b假设为额外的weight，超平面方程写为：

```
w1x1+w2x2+w0=0
```
所有超平面右上方的点满足：

```
w1x1+w2x2+w0>0
```
所有超平面左下方的点满足：

```
w1x1+w2x2+w0<0
```
调整weight，使得超平面定义边际的两边：

```
H1：w1x1+w2x2+w0>=1,for yi=+1,
H2：w1x1+w2x2+w0<=-1,for yi=-1
```
综合以上两式，得到：

```
yi(w1x1+w2x2+w0)>=1
```
所有坐落在边际的两边的超平面上的被称作“支持向量”（support vectors）
分界的超平面和H1或H2上任意一点的距离为：1/||w||
注：||w||是向量的范数，为sqrt(w1^2 + w2^2+...+ wn^2)
所以最大边际距离为2/||w||
## 5. 实例
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612135038340.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
**w**=（a,2a),(通过计算(2,3)-(1,1)得来)
使用(1,1)点，W·X+b=0，得a+2a+w0=-1
使用(2,3)点，W·X+b=0，得2a+6a+w0=1
求出a,w0
## 6. 小结
优点：1.训练好的模型的算法复杂度是由支持向量的个数决定的，而不是由数据的务度决定的。所以 SVM不太容易产生overfitting
2.SVM训练出来的模型完全依赖于支持向量(Support Vectors).即使训练集里面所有非支持 向量的点都被去除，重复训练过程，结果仍然会得到完全一样的模型。
3. SVM如果训练得出的支持向屋个数比较小，SVM训练出的模型比较容易被泛化。

