
@[TOC](目录)

 * * *

## 1.什么是神经网络?
神经网络（Neural Network)以人脑中的神经网络为启发而产生的，最著名对的算法是backpropagation（BP）算法。可用来解决分类问题，也可用来解决回归问题（详情见[前言](https://blog.csdn.net/qq_33208851/article/details/91354105)）
## 2.多层向前神经网络（Multiplier Feed-Forward Neural Network）
多层向前神经网络中使用了**BP算法**：

 - 通过迭代性来处理训练集中的实例
 - 计算经过神经网络后预测值和真实值之间的误差
 - 反向最小化误差更新两个神经节点之间的误差
 - 终止条件：权重的更新低于某个阈值、预测的错误率低于某个阈值、达到预设的循环次数

多层向前神经网络的组成，每一层由单元组成（图中小圈圈）
**输入层**：由训练集的实例特征向量传入
**隐藏层**：层数为一至任意多个，输入和输出只有一层
**输出层**：输出结果
注：

 - 经过权重节点传入下一层，一层的输出是下一层的输入
 - 作为多层向前神经网络，理论上，如果有足够多的隐藏层和足够大的训练集，可以模拟出任何方程
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190612164025466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
 - 上图中有两层（输入层不算），两个神经节点之间连线有权值

## 3. 设计神经网络
**基本思想**：自己预设一定范围内的权值，偏差值西塔等数值，通过训练集实例数据的输入，计算出各个神经节点的输出值（包括隐藏层和输出层）。然后反向进行计算：首先计算出输出层的Errj（错误偏差率），接着是隐藏层的Errj（两者计算公式不同）、△Wij（神经节点之间的权重的更新值）以及偏向更新值△θ。这样就得到了经过反向过程之后的权值、输出、偏向等，输入测试实例就可以预测出结果。
**算法**
输入：D：数据集，L：学习率（learning rate），一个多层向前神经网络（自己定义权值、偏向的向前神经网络）
输出：一个训练好的神经网络（a trained neural network）
初始化权重（weights）和偏向（bias）:随机在-1到1之间，或者-0.5到0.5之间，每个单元有一个偏向
步骤：
 1. 将某一训练实例的特征值作为inputs(n个特征值则input layer有n个单元节点)单元节点的输入
 2. 在隐藏层和输出层计算每个节点的输出![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613120400245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
 **I**j:j节点的“输入”，**O**i：由i，j节点连接成的线的前驱节点的输出（i如果是输入层的节点那么oi就是该节点的输入值），西塔j为j节点的偏向（每个节点有一个初始的bias）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613122600303.png#pic_center)
经过非线性转换f得到outputs：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613122827591.png#pic_center)
 3. 反向计算：
 3.1 计算输出层的Errj（j节点的错误值）,Oj是j节点的输出值，Tj是j节点的真实值
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613123849269.png#pic_center)
 3.2 计算隐藏层的Errj，Oj是j节点的输出值，Errk是节点j和节点k连接线上的后继（k为后）节点的错误值
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613123921226.png#pic_center)
3.3 权重更新：原始权重加上更新差值，权重差值=学习率l·j节点的错误值Errj·i节点的输出Oi（学习率L应该是给定的0-1之间的一个数）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613124537590.png#pic_center)
3.4 最后是偏向更新：新偏向值=原始偏向值+偏向更新差值，偏向更新差值=学习率l·j节点的错误值
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613125112688.png#pic_center)
至此一个训练样本训练结束
 4. 将训练样本中其他样本重复上述步骤



 - 使用神经网络训练之前，必须确定神经网络的层数，以及每层单元的个数
 - 特征向量在被传入输入层时通常被先标准化到0和1之间(为了加速学习过程)
 - 没有明确的规则来设计最好有多少个隐藏层。根据实验测试和误差，以及准确来实验并改进
 - **交叉验证(Cross-Validation)**：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613103400973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
假设有一组样本数据，将其划分为三份（K），两份用来进行训练一份用来测试：
红测试，蓝灰训练：将训练好的模型用红来做评估，得到一个准确度（Accuracy_red)
蓝测试，红灰训练：将训练好的模型用蓝来做评估，得到一个准确度（Accuracy_blue)
灰测试，红蓝训练：将训练好的模型用灰来做评估，得到一个准确度（Accuracy_gray)
`Accuracy=（Accuracy_red+Accuracy_blue+Accuracy_gray)/3`
也叫K-fold cross validation
## 4. 实例

**正向**计算：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613115758962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
注：initial input里面的数据
**反向**计算：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613115904382.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjA4ODUx,size_16,color_FFFFFF,t_70#pic_center)
## 5. 小结

