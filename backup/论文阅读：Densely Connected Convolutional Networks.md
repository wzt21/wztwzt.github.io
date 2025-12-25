**DenseNet有几个引人注目的优势：它们缓解了消失梯度问题，加强了特征传播，鼓励了特征重用，并大大减少了参数数量。**

<img width="603" height="513" alt="Image" src="https://github.com/user-attachments/assets/81cb529a-70a1-421c-8006-c1e36774d986" />

当输入或梯度的信息通过许多层时，当它到达网络的末端（或开始）时，它可能消失并“洗掉”。尽管这些不同的方法在网络拓扑和训练过程中有所不同，但它们都具有一个关键特征：**它们创建了从早期层到后期层的短路径。**

至关重要的是，与resnet相反，我们从不在将特征传递到层之前通过求和来组合特征；相反，我们通过连接功能来组合功能。这在 
 层网络中引入了(L(L+1)/2)连接，而不是传统架构中的L。由于其密集连接性模式，我们将我们的方法称为密集卷积网络（DenseNet）。

DenseNet的一大优势是其改善了整个网络的信息流和梯度，这使得它们易于训练。密集连接具有正则化效果，这减少了训练集大小较小的任务的过度拟合。
随机深度通过在训练期间随机丢弃层来改进深度残差网络的训练。这表明并非所有层都是需要的，并强调了深度（剩余）网络中存在大量冗余。

<img width="1234" height="257" alt="Image" src="https://github.com/user-attachments/assets/f166ce80-4a5a-47fc-bbde-42e88733da4a" />

DenseNets没有从极深或极宽的架构中汲取代表性的力量，而是通过功能重用利用网络的潜力，产生易于训练和高度参数化的精简模型。

考虑通过卷积网络的单个图像x0。网络由L层组成，每个层实现非线性变换 Hl(·)，其中l索引层。Hl(·)可以是诸如[批量归一化]BN、ReLU[6]、合并[19]或卷积Conv等操作的复合函数。我们将第lth层的输出表示为xl 。

ResNets的一个优点是梯度可以直接通过连接自身的函数从后面的层流到前面的层。然而，恒等式函数和Hl的输出通过求和组合，这可能会阻碍网络中的信息流。

为了进一步改善层之间的信息流，我们提出了一种不同的连接模式:我们引入从任何层到所有后续层的直接连接。图1图解了生成的DenseNet的布局。因此，第 l 层接收所有前一层的特征映射，x0,x1,x2,...xl-1 作为输入:
<img width="349" height="54" alt="Image" src="https://github.com/user-attachments/assets/466797a9-4d36-4420-82d5-7da54cbb7d62" />

我们将  Hl(·)定义为三个连续操作的复合函数:批量归一化(BN)[14]、校正线性单位(ReLU)[6]和3 × 3卷积(Conv)。

If each function H` produces k feature maps, it follows that the lth layer has k0 +k ×(`l−1) input feature-maps, where k0 is the number of channels in the input layer. An important difference between DenseNet and existing network architectures is that DenseNet can have very narrow layers, e.g., k = 12. We refer to the hyper-parameter k as the growth rate of the network.

The global state, once written, can be accessed from everywhere within the network and, unlike in traditional network architectures, there is no need to replicate it from layer to layer.

a 1×1 convolution can be introduced as bottleneck layer before each 3×3 convolution to reduce the number of input feature-maps, and thus to improve computational efficiency.

所有的网络都使用随机梯度下降(SGD)进行训练。在CIFAR和SVHN上，我们分别使用批大小为64进行300和40个周期的训练。初始学习率设置为0.1，分别在训练总数的50%和75%时除以10。在ImageNet上，我们训练模型90个epoch，批处理大小为256。最初的学习率设置为0.1，在第30和60个迭代降低10倍。注意，DenseNet的简单实现可能包含内存效率低下。为了减少gpu上的内存消耗，请参考我们关于DenseNets[26]内存高效实现的技术报告。

这表明DenseNets可以利用更大、更深入的模型所增加的表征能力。这也表明它们不存在过拟合或残差网络[11]的优化困难。

DenseNets比其他体系结构（特别是ResNet）更有效地利用参数。具有瓶颈结构和过渡层降维的DenseNetBC参数效率特别高。

enseNets的性能与最先进的ResNets不相上下，同时需要更少的参数和计算就能达到类似的性能。

对于密集卷积网络提高精度的一种解释可能是，通过较短的连接，单个层从损失函数获得额外的监督。

在遵循简单的连通性规则的同时，DenseNets自然地集成了身份映射、深度监督和多样化深度的属性。根据我们的实验，它们允许在整个网络中重用特征，因此可以学习更紧凑的，更准确的模型。由于其紧凑的内部表示和减少的特征冗余，DenseNets可能是构建在卷积特征上的各种计算机视觉任务的良好特征提取器，例如[4,5]。我们计划在未来的工作中利用DenseNets研究这种特征转移。

