
@[TOC](目录)

 * * *
已经说明[线性区分性的定义](https://blog.csdn.net/qq_33208851/article/details/91490875)，以下将对线性不可区分做介绍
## 1.线性不可区分的解决方案（linear inseparable）：
数据集在空间中对应的向量不可被一个超平面区分开 
两个步骤来解决：
1，利用一个非线性的映射把原数据集中的向量点转化到一个更高维度的空间中 
2，在这个高维度的空间中找一线性的超平面来根据线性可分的情况处理
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612145259498.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
所以对线性不可划分得情况，关键是找出一种由低维向高维得映射方法，例如下图中：由映射关系y=x^2将点从一维映射到二维空间中，可以找到某直线y=b（b为常数），将分类线性划分
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612141224410.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
如何利用非线性映射把原始数据转化到高维中？
例如：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612150309708.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
## 2. 如何选择低向高维的转化方法？
### 2.1 核方法
在线性SVM中转化为最优问题时求解公式计算都是以内积的形式出现的，把训练集向量点转化到高维的非线性映射函数，因为内积算法复杂度非常大，所以我们利用核函数来取代计算非线性映射函数的内积，两者计算的内积等同，但核函数大大降低了计算复杂度。
### 2.2 常见核函数
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612153051477.png#pic_center)
### 2.3 核函数举例
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612153519800.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
## 3. SVM扩展解决多分类问题
以上我们讨论的均是二分类的问题，那么能否解决多分类的问题？
解决思路：假设有5个分类，
第一个分类器将类别为a和其他的类别区分开来：{{a},{b,c,d,e}}
第二个分类器在{b,c,d,e}中将类别为b和其他的类别区分开来：{{a},{b},{c,d,e}}
...
最后得到：{{a},{b},{c},{d},{e}}

