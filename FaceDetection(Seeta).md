
# SeetaFace Detection

该模块基于我们提出的一种结合经典级联结构和多层神经网络的人脸检测方法实现，其所采用的漏斗型级联结构（Funnel-Structured Cascade，FuSt）专门针对多姿态人脸检测而设计，其中引入了由粗到精的设计理念，兼顾了速度和精度的平衡。

如图1所示，FuSt级联结构在顶部由多个针对不同姿态的快速LAB级联分类器构成，紧接着是若干个基于SURF特征的多层感知机（MLP）级联结构，最后由一个统一的MLP级联结构（同样基于SURF特征）来处理所有姿态的候选窗口，整体上呈现出上宽下窄的漏斗形状。从上往下，各个层次上的分类器及其所采用的特征逐步变得复杂，从而可以保留人脸窗口并排除越来越难与人脸区分的非人脸候选窗口。

![](http://static.leiphone.com/uploads/new/article/740_740/201612/584a474fa9371.png?imageMogr2/format/jpg/quality/90)

与SeetaFace Detection开源代码配套开放的是一个准正面人脸检测模型（使用了约20万人脸图像训练而来），可以实现准正面人脸的准确检测（旋转角度约45度以内，但对于姿态偏转较大的人脸也具备一定的检测能力）。

![](http://static.leiphone.com/uploads/new/article/740_740/201612/584a480a2c010.png?imageMogr2/format/jpg/quality/90)

![](http://static.leiphone.com/uploads/new/article/740_740/201612/584a47ca16431.png?imageMogr2/format/jpg/quality/90)

FDDB 上的ROC曲线
