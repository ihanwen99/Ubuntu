# PyTorch

瀚文的Ubuntu学习之路

用这个README文件记录我的Ubuntu配置过程，方便之后重新配置使用

## 190515配置PyTorch

需要预先配置好 Conda（详见Ubuntu文件夹）

### PyTorch 的安装

在官网上面直接安装就好（可以自己选择配置）

<https://pytorch.org/get-started/locally/>

其中CUDA的版本可以在NVIDIA控制面板中帮助子菜单-选择系统信息-组件查看

### CUDA从入门到精通

https://blog.csdn.net/qq_30263737/article/details/81235580

## 190518 Windows下面使用Anaconda配置多Python环境

只需要在cmd环境下面`activate LearnPyTorch`就可以进入我们新创建的LearnPyTorch环境啦

## 190518 继续学习PyTorch

##### Windows下运行Pytorch tutorial代码报错：BrokenPipeError: [Errno 32] Broken pipe

源代码地址： [Training a classifier (CIFAR10)](https://pytorch.org/tutorials/beginner/blitz/cifar10_tutorial.html)

该问题的产生是由于windows下多线程的问题，和DataLoader类有关，具体细节点这里[Fix memory leak when using multiple workers on Windows](https://github.com/pytorch/pytorch/pull/5585)。

**解决方案：**

修改调用torch.utils.data.DataLoader()函数时的 num_workers 参数。该参数官方API解释如下： 

- **num_workers** ([*int*](https://docs.python.org/3/library/functions.html#int)*, optional*) – how many subprocesses to use for data loading. 0 
  means that the data will be loaded in the main process. (default: 0)

  该参数是指在进行数据集加载时，启用的线程数目。可以通过修改num_works参数为 **0** ，只启用一个主进程加载数据集，避免在windows使用多线程即可。

### 190519 继续学习PyTorch

国内的清华源和中科大源截止到目前（190519）已经挂掉了

### [热身：numpy](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id14)

Numpy提供了一个n维数组对象，以及许多用于操作这些数组的函数。Numpy是科学计算的通用框架; 它对计算图，深度学习或渐变都一无所知。但是，通过使用numpy操作手动实现网络的前向和后向传递，我们可以轻松地使用numpy将两层网络适配到随机数据。<<https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id14>>

### [PyTorch：Tensors](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id15)

Numpy是一个很棒的框架，但它不能利用GPU来加速其数值计算。对于现代深度神经网络，GPU通常提供[50倍或更高的](https://github.com/jcjohnson/cnn-benchmarks)加速，因此不幸的是，numpy对于现代深度学习来说还不够。

与numpy不同，PyTorch Tensors可以利用GPU加速其数值计算。要在GPU上运行PyTorch Tensor，只需将其转换为新的数据类型即可。

在这里，我们使用PyTorch Tensors将双层网络与随机数据相匹配。就像上面的numpy示例一样，我们需要手动实现网络中的前向和后向传递<>

1.numpy.dot()` 返回的是两个数组的点积(dot product)

2.**线性整流函数**（Rectified Linear Unit, **ReLU**），又称**修正线性单元，**是一种人工神经网络中常用的激活函数（activation function），通常指代以斜坡函数及其变种为代表的非线性函数。

![img](https://gss2.bdstatic.com/-fo3dSag_xI4khGkpoWK1HF6hhy/baike/w%3D268%3Bg%3D0/sign=4d2369e667600c33f079d9ce22773632/d788d43f8794a4c25b5e4dd902f41bd5ac6e39c6.jpg)



​	通常意义下，线性整流函数指代数学中的斜坡函数，即![img](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D119/sign=547aa813232eb938e86d7ef3ec6385fe/9d82d158ccbf6c818097871ab03eb13532fa409b.jpg)在神经网络中，线性整流作为神经元的激活函数，定义了该神经元在线性变换 ![img](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D56/sign=e7a581f2e524b899da3c793e6f068e17/adaf2edda3cc7cd9428d9f2b3501213fb90e91a4.jpg) 之后的非线性输出结果。换言之，对于进入神经元的来自上一层神经网络的输入向量![img](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D9/sign=63d5bbefd82a283447a63a3a5baeba/6d81800a19d8bc3eb2b9ad388e8ba61ea9d3458a.jpg) ，使用线性整流激活函数的神经元会输出![img](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/s%3D117/sign=09b749e86c59252da7171905039a032c/2fdda3cc7cd98d10d1a7a7c32d3fb80e7aec90d5.jpg)至下一层神经元或作为整个神经网络的输出（取决现神经元在网络结构中所处位置）。

## [Autograd](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id16)

#### [PyTorch：Tensors和autograd](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id17)

在上面的例子中，我们不得不手动实现神经网络的前向和后向传递。手动实现反向传递对于小型双层网络来说并不是什么大问题，但对于大型复杂网络来说很快就会变得非常繁琐。

值得庆幸的是，我们可以使用自动微分来自动计算神经网络中的后向传递。**PyTorch**中的 **autograd**包提供了这个功能。使用autograd时，网络的正向传递将定义 **计算图形** ; 图中的节点将是张量，边将是从输入张量产生输出张量的函数。通过此图反向传播，您可以轻松计算渐变。

#### [PyTorch：定义新的autograd函数](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id18)

在引擎盖下，每个原始autograd运算符实际上是两个在Tensors上运行的函数。的**正向**函数从输入张量计算输出张量。该**向后**功能接收输出张量的梯度相对于一些标量值，并计算输入张量的梯度相对于该相同标量值。

在PyTorch中，我们可以通过定义`torch.autograd.Function`和实现`forward` 和`backward`函数的子类来轻松定义我们自己的autograd运算符。然后，我们可以通过构造一个实例并将其称为函数来使用我们的新autograd运算符，并传递包含输入数据的Tensors。

在这个例子中，我们定义了自己的自定义autograd函数来执行ReLU非线性，并使用它来实现我们的双层网络。

#### [TensorFlow：静态图](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id19)

PyTorch autograd看起来很像TensorFlow：在两个框架中我们定义了一个计算图，并使用自动微分来计算梯度。两者之间最大的区别是TensorFlow的计算图是**静态的**，PyTorch使用 **动态**计算图。

在TensorFlow中，我们定义计算图一次，然后一遍又一遍地执行相同的图，可能将不同的输入数据提供给图。在PyTorch中，每个前向传递定义了一个新的计算图。

静态图很好，因为你可以预先优化图形; 例如，框架可能决定融合某些图形操作以提高效率，或者提出一种策略，用于在多个GPU或许多机器上分布图形。如果您反复使用相同的图表，那么这个可能代价高昂的前期优化可以摊销，因为相同的图表会反复重新运行。

静态和动态图表不同的一个方面是控制流程。对于某些模型，我们可能希望对每个数据点执行不同的计算; 例如，对于每个数据点，可以针对不同数量的时间步长展开循环网络; 这种展开可以作为循环实现。使用静态图形，循环结构需要是图形的一部分; 因此，TensorFlow提供了诸如`tf.scan`将循环嵌入到图中的运算符。使用动态图形情况更简单：因为我们为每个示例动态构建图形，我们可以使用常规命令流程控制来执行每个输入不同的计算。

## [nn模块](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id20)

### [PyTorch：nn](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id21)

计算图和autograd是定义复杂运算符和自动获取导数的非常强大的范例; 然而，对于大型神经网络，原始autograd可能有点太低级别。

在构建神经网络时，我们经常考虑将计算安排到**层中**，其中一些**层**具有**可学习的参数** ，这些**参数**将在学习期间进行优化。

在TensorFlow，像包 [Keras](https://github.com/fchollet/keras)， [TensorFlowSlim](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/contrib/slim)，和[TFLearn](http://tflearn.org/)通过原始的计算图表，是构建神经网络的有用提供更高层次的抽象。

在PyTorch中，该`nn`包用于同样的目的。该`nn` 包定义了一组**模块**，大致相当于神经网络层。模块接收输入张量并计算输出张量，但也可以保持内部状态，例如包含可学习参数的张量。该`nn`软件包还定义了一组在训练神经网络时常用的有用损失函数。

### [PyTorch: optim](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id22)

到目前为止，我们通过手动改变持有可学习参数的Tensors （使用`torch.no_grad()` 或`.data`避免在autograd中跟踪历史记录）来更新模型的权重。对于像随机梯度下降这样的简单优化算法来说，这不是一个巨大的负担，但在实践中，我们经常使用更复杂的优化器如AdaGrad，RMSProp，Adam等来训练神经网络。

PyTorch中的optim包提取了优化算法的概念，并提供了常用优化算法的实现。

### [PyTorch：自定义nn模块](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id23)

有时您需要指定比现有模块序列更复杂的模型; 对于这些情况，您可以通过子类化`nn.Module`和定义`forward`接收输入Tensors并使用其他模块或Tensors上的其他autograd操作生成输出Tensors 来定义您自己的模块。

### [PyTorch：控制流+重量共享](https://pytorch.org/tutorials/beginner/pytorch_with_examples.html#id24)

作为动态图和权重共享的一个例子，我们实现了一个非常奇怪的模型：一个完全连接的ReLU网络，在每个正向传递上选择1到4之间的随机数并使用那么多隐藏层，重复使用相同的权重多次计算最里面的隐藏层。

对于这个模型，我们可以使用普通的Python流控制来实现循环，并且我们可以通过在定义正向传递时多次重复使用相同的模块来实现最内层之间的权重共享。

`torch.mm(a, b)`是矩阵a和b**矩阵相乘**

`torch.clamp(input, min, max, out=None)` → Tensor
将输入input张量每个元素的夹紧到区间 [min,max][min,max]，并返回结果到一个新张量。
