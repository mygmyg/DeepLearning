#基于深度学习的图像超分辨率

超分辨率技术通过合成图像中的子像素信息，提高图像分辨率。超分辨率问题，实际上是一个病态问题，因为在图像分辨率降低的过程中，丢失的高频细节很难恢复。常见的合成方法包括：

	图像中相邻像素间插值
	影像中相邻帧间插值
	频域滤波，降低噪声
### 概率生成模型

概率生成模型的目的，就是找出给定观测数据内部的统计规律，并且能够基于所得到的概率分布模型，产生全新的，与观测数据类似的数据。与庞大的真实数据相比，概率生成模型的参数个数要远远小于数据的数量。因此，在训练过程中，生成模型会被强迫去发现数据背后更为简单的统计规律，从而能够生成这些数据。常见的有`生成对抗网络（GAN）`，`变分自动编码模型（VAE）`，`自回归模型（Auto-regressive）`,现在比较流行的自回归模型，包括最近刚刚提出的像素CNN或者像素RNN，它们可以用于图像或者视频的生成。。


![](http://static.leiphone.com/uploads/new/article/740_740/201701/586f6f0ac715f.png?imageMogr2/format/jpg/quality/90)

### GAN 
GAN为无监督学习，提供了一个非常有潜力的解决方案。GAN (Generative Adversarial Networks)的优点：

	避免了马尔科夫链式的学习机制；
	各种类型的损失函数都可以整合到GAN模型中；
	概率密度不可计算时，GAN仍可以使用,这是因为GAN引入了内部对抗的训练机制，可以逼近一些不容易计算的目标函数；
	生成模型G的参数更新不是来自于数据样本本身（不是对数据的似然性进行优化），而是来自于判别模型D的一个反传梯度。
	理论上，任何一个可微分的函数，都可以用来参数化GAN的生成模型和判别模型。
	
缺点：

	GAN的可解释性非常差，一个数据分布Pg(G)，没有显示的表达式。
	实际应用中GAN比较难训练。

##### GAN 原理
![](http://static.leiphone.com/uploads/new/article/740_740/201701/586f723cc049b.png?imageMogr2/format/jpg/quality/90)

当一个判别模型的能力已经非常强的时候，如果生成模型所生成的数据，还是能够使它产生混淆，无法正确判断的话，那我们就认为这个生成模型实际上已经学到了真实数据的分布。

![](http://static.leiphone.com/uploads/new/article/740_740/201701/586f72bce7f27.png?imageMogr2/format/jpg/quality/90)

## 图像超分辨率

超分辨率问题，实际上是一个病态问题，因为在图像分辨率降低的过程中，丢失的高频细节很难恢复。但是GAN在某种程度上可以学习到高分辨率图像的分布，从而能够生成质量比较好的高分辨率图像。因为传统上做一个图像超分辨率，都要去对一些高频细节进行建模，而这里生成模型训练目的就简化为迷惑判别模型。
Ian Goodfellow 等人的 2014 年论文中，生成器输出的样本：
![](http://static.leiphone.com/uploads/new/article/740_740/201612/58623acede3a7.png?imageMogr2/format/jpg/quality/90)

可以看出，生成器在生成数字和人脸图像方面做得不错。但是，使用 CIFAR-10 数据库生成的风景、动物图片十分模糊。



## SRGAN

[SRGAN](https://github.com/buriburisuri/SRGAN)

	The existing CNN based super-resolution skill mainly use MSE loss and this makes super-resolved images look blurry. If we replace MSE loss with gradients from GAN, we may prevent the blurry artifacts of the super-resolved images and this is the key idea of this paper. 

![](http://static.leiphone.com/uploads/new/article/740_740/201701/586f74284d83b.png?imageMogr2/format/jpg/quality/90)

![](http://read.html5.qq.com/image?src=forum&q=5&r=0&imgflag=7&imageUrl=http://mmbiz.qpic.cn/mmbiz_png/ymzg67DoLHK9dTf073yF09siaxv4znGsrILDib2dK4BuwMMYicEYeTwgKRWOpxhQeIqwkQhLoqB8Mh6YNq7WfMMbQ/0?wx_fmt=png)

与以往基于深度学习模型做图像超分辨率的结果相比的话（比如SRResNet等），我们可以看到GAN的结果图能够提供更丰富的细节。这也就是GAN做图像生成时的一个显著优点，即能够提供更锐利的数据细节。[GAN](http://www.leiphone.com/news/201701/Kq6FvnjgbKK8Lh8N.html)

### LAPGANs

深度图像生成模型：在对抗网络应用拉普拉斯金字塔。用一系列的卷积神经网络（CNN）连续生成清晰度不断提高的图像，能最终得到高分辨率图像。该模型被称为 LAPGANs。在学习序列中，LAPGAN 不断地进行 downsample 和 upsample 操作，然后在每一个 Pyramid level 中，只将残差传递给判别模型（D）进行判断。这样的 sequential + 残差结合的方式，能有效减少 GAN 需要学习的内容和难度，从而达到了 “辅助” GAN 学习的目的。
![](http://static.leiphone.com/uploads/new/article/740_740/201609/57c7a4283c69a.png?imageMogr2/format/jpg/quality/90)

与此前 GAN 架构的区别是：传统的 GAN 只有一个 生成器 CNN，负责生成整幅图像；而在拉普拉斯金字塔结构中，金字塔的每一层（某特定分辨率），都有一个关联的 CNN。每一个 CNN 都会生成比上一层 CNN 更加清晰的图像输出，然后把该输出作为下一层的输入。这样连续对图片进行升采样，每一步图像的清晰度都有提升。[生成对抗网络](http://www.leiphone.com/news/201612/Cdcb1X9tm1zsGSWD.html)