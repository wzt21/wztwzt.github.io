**Dropout: A Simple Way to Prevent Neural Networks from  Overfitting**

net would become robust against dropout by manking many copies of each hidden unit,but this is a poor solution for exactly the same reason as **replica codes are a a poor way to deal with a noisy channel.**

dropout 模型
标准神经网络的前向操作：

<img width="363" height="98" alt="Image" src="https://github.com/user-attachments/assets/9ea8e2c1-f063-4c3b-afa0-cb6890bde106" />

f激活函数
带有dropout的前向操作：

<img width="352" height="192" alt="Image" src="https://github.com/user-attachments/assets/85c735c8-665b-4a23-9eca-67d6b3304bae" />

<!-- Failed to upload "image.png" -->

最大范数正则化

<img width="966" height="226" alt="Image" src="https://github.com/user-attachments/assets/fa2d1658-39a4-4f4a-8ad8-70df59f4c3d2" />

无监督预训练
预训练获得的权重应除以p

贝叶斯神经网络？

对特征的影响
We hypothesize that for each hidden unit, dropout prevents co-adaptation by making the presence of other hidden units unreliable. Therefore, a hidden unit cannot rely on other specific units to correct its mistakes. It must perform well in a wide variety of different contexts provided by the other hidden units.

在不使用随机性的情况下获得 dropout 的一些好处的一种方法是边缘化噪声，以获得一个在期望上与 dropout 过程作用相同的正则化器。

**训练dropout神经网络**
网络大小
如果 n 大小的层对于任何给定任务的标准神经网络是最优的，那么一个好的 dropout 网络应该至少有 n/p 个单元。

学习率和动量
dropout 网络通常应该使用比标准神经网络最优学习率高 10-100 倍的学习率。另一种减少噪声影响的方法是使用高动量。虽然 0.9 的动量值在标准网络中很常见，但在 dropout 中，我们发现 0.95 到 0.99 左右的值效果要好得多。使用高学习率和/或动量显著加快了学习速度。

最大范数正则化
这将每个隐藏单元的传入权重向量的范数约束为上限 c。c 的典型值范围从 3 到 4。

dropout率
隐藏单元的 p 典型值在 0.5 到 0.8 的范围内。对于输入层，选择取决于输入的类型。对于实值输入（图像块或语音帧），典型值是 0.8。对于隐藏层，p 的选择与隐藏单元数量 n 的选择是耦合的。较小的 p 需要大的 n，这会减慢训练速度并导致欠拟合。较大的 p 可能不足以产生防止过拟合的 dropout。
