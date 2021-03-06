+++
title = "TensorFlow介绍"
date = "2019-02-05T18:29:26+08:00"
toc = true
tags = ["TensorFlow"]
categories = ["深度学习", "TensorFlow"]
description = ""
+++


# 1.关于TensorFlow

TensorFlow是一个采用数据流图（data flow graphs），用于数值计算的开源软件库。节点（Nodes）在图中表示数学操作，图中的（edges）则表示在节点间相互联系的多维数据数组，即张量（tensor）。它灵活的架构让你可以在多种平台上展开计算，例如台式计算机中的一个或多个CPU（或GPU），服务器，移动设备等等。TensorFlow 最初由Google大脑小组（隶属于Google机器智能研究机构）的研究员和工程师们开发出来，用于机器学习和深度神经网络方面的研究，但这个系统的通用性使其也可广泛用于其他计算领域。

<!--more-->



### 1.1什么是数据流图（Data Flow Graph）

  数据流图用“结点”（nodes）和“线”(edges)的有向图来描述数学计算。“节点” 一般用来表示施加的数学操作，但也可以表示数据输入（feed in）的起点/输出（push out）的终点，或者是读取/写入持久变量（persistent variable）的终点。“线”表示“节点”之间的输入/输出关系。这些数据“线”可以输运“size可动态调整”的多维数据数组，即“张量”（tensor）。张量从图中流过的直观图像是这个工具取名为“Tensorflow”的原因。一旦输入端的所有张量准备好，节点将被分配到各种计算设备完成异步并行地执行运算。

![](数据流图.gif)

### 1.2TensorFLow 六大特性

1.高度的灵活性—-提供很多的工具让你来构建图,也可以在tf基础上写上层库,对tf操作进行组合,还可以动手丰富底层操作,自己添加tf内容
2.真正的可移植性—-tf在CPU和GPU上运行，可以运行在台式机、服务器、手机移动设备,Android,ios都可以,平台之间转移可以不用改
3.将科研和产品联系在一起—-tf可以免去很大的代码重写工作,帮助科研工作者提高科研产出率
4.自动求微分—-用户只需要定义预测模型的结构，将这个结构和目标函数结合在一起，并添加数据,tf将自动为你计算相关的微分导数
5.多语言支持—-官方文档中写明,目前有python/c++使用界面,还鼓励开发者开发其他语言
6.性能最优化—-给予了线程、队列、异步操作等以最佳支持,tf让你可以将你手边硬件的计算潜能全部发挥出来。你可以自由地将tf图中的计算元素分配到不同设备上,tf可以帮你管理好这些不同副本

