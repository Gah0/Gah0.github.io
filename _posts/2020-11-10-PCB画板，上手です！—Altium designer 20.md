---
title: PCB画板，上手です！
author: Gah0
date: 2020-11-10 14:10:00 +0800
categories: [Tutorial]
tags: [PCB,Electorics,Tutorial]
---

# PCB画板快速上手—Altium designer 20 操作教程

```mermaid
graph LR
   1.功能分析 --> 2.仿真电路设计 --> 3.电路原理图设计 --> 4.PCB设计与生产 --> 5.元件焊接 --> 6.产品调试  --> 7.产品改进

```

1.确定产品功能，比如我要做流水灯，需要LED灯，NE555等IC芯片组成，并查看该IC资料分析用处，想法构建产品。

这次我利用了NE555芯片做了一个脉冲发生器之类的东西，在NE555的芯片引脚会受到电压影响而产生波形信号。
通过电容不断反复充放电，会有了一个电压升降的过程，因此波形信号会按照充放电的频率不断变化。

2.利用mutilsum等EDA对单个IC进行分析，仿真可以验证某个元件是否能实现功能。

于是我利用了Mutilsim进行了仿真与计算，发现电阻120Ω-500.12KΩ是可以50HZ-238HZ左右的频率，占空比在50%。

3.电路原理图设计，根据上文的仿真实现完整的电路图。

4.PCB设计与生产，将合适的元件进行规范的电路设计，并通过打印机器生成作品（PCB画板/打板）

5.元件焊接，得到电路板后，进行焊接。

6.调试该完整的电路功能是否符合预想。

7.对产品进行改进。



本文主要介绍PCB画板过程，记录自己的画板/打板经历。



### AD操作（一）

**新建项目 (Project)**

> 一个完整的项目必然包含原理图，PCB，把他们归为一个项目

**新建原理图 (Schematic)**

**新建原理图元件库 (Schematic Library)**

**新建PCB图 (PCB)**

**新建PCB元件库 (PCB Library)**

![1](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/1.png)

**创建完成后**

> 记得保存，记得保存，记得保存。
>
> 对每个新建窗户都要按一下CTRL+S快捷键

![2](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/2.png)

#### 1.旋转元件

**提示**：旋转元件：鼠标按住元件，同时按**键盘X**或**键盘Y**。



### AD操作：画PCB封装（二）

不过对于我这次的打板，我需要用自己的LED灯泡，在观察AD20中的pcb封装(footprint)基本和我想要的不一样，多余的封装线条（打板时会上油墨），不同距离的**孔径，孔距**，因此我需要自己画某个元器件的PCB封装，再导入到元件库中使用。

#### 1.栅格设置

在绘画PCB封装前，图纸背后限定的最小的单位长度，1格=0.127mil。

我们可以改变栅格的长度，菜单栏 -> 视图 -> 栅格 -> 设置全局捕捉栅格 -> 100mil 改为 1mil

**注意**：画所有PCB封装前，首先建议修改PCB封装库图纸的单位量，把`mil`改成`mm`。

> 以下图为淘宝的**微动开关**规格。

![淘宝的微动开关](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/淘宝的微动开关.png)

> 以下为**微动开关**的PCB封装，在Top Overlay层绘画，以下为四个过孔与四根直线，打板后，直线部分与数字会变成白色线条和注释，以下的过孔应该使用焊盘，此外，这是我第一次画封装，没想到直径1.5cm焊盘直径会这么小。

![PCB封装重新画](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/PCB封装.jpg)

这次的电路设计，电路所需的主要的PCB封装是LED焊盘，微动开关，排母过孔，滑动变阻器过孔，8PIN（NE555）, 16 PIN（CD4017）, 18PIN （LM3914）DIP底座

![PCB封装基底座](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/PCB封装基底座.png)

**小提示：**dip封装的芯片，去淘宝搜索dip芯片底座的数据，在AD中利用快速向导 (Footprint Wizard) 去生成PCB封装（长宽固定，双排引脚对齐），这样的封装就不需要自己画了，简单省事。

一般来说，AD自带的元件基本都有PCB封装，但是封装的属性是固定的，我不知道如何修改他。上网搜索了一会，只有电容与电阻的类型是符合我的电路设计要求，因此我没有自己画电阻与电容。



#### 2.圆点设置

菜单栏  -> 编辑  ->  设置参考 -> 位置  （**快捷键-E-F-L**）  然后可以自己放置圆点的位置。

![PCB元件与层](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/PCB元件与层.png)

AD软件下方有很多的方块，这些都是PCB的层，一般都在**Top Overlay**层画封装，上图是错误的，因为他不是PCB板的最顶层。



#### 3.电路层设置

**鼠标右键 >> Layer Stack Manager** 可以更改PCB的层次与结构

打PCB板的时候，因为是资金不足，因此我只需要两层，TOP LAYER与BOTTOM LAYER。

![PCB层](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/PCB层.png)

> 以下为存放LED灯的过孔，孔径2.54mm，孔距1mm，基本上所有焊接洞洞板都是这个数据。
>
> 过孔是错误的，实际上要使用焊盘，请注意。

![更改单位](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/更改单位.png)



#### 4.长度测量

我们知道开辅助打游戏会比较爽，画图也一样，我们用直线来做辅助

先以原点画一条直线作为坐标轴，这样就容易观察直线的长度，也易于放**孔径对齐等**。

若要检查工作区中两个点之间的距离，请使用测量距离 （**快捷方式**Ctrl+M**） 。



### AD操作：画原理图元件（三）

画好PCB封装后，就是画元件图了。

绘画原理元件库时，图纸背后限定的最小的单位长度，1格=0.127mil。

我们可以改变栅格的长度，**菜单栏 -> 视图 -> 栅格 -> 设置捕捉栅格 ->100mil 改为 1mil**

> 以下为自己画的**微动开关**原理图元件，两根导线，两个小圆圈，两个多边形组成的元件

![导入PCB封装](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/导入PCB封装.png)

如果元件已经放入原理图，而又忘记导入封装，又或者PCB封装需要修改，可以在图中左处 SCH Library 中选中的元件，**更新原理图（Update Schematic）** 即可。



### AD操作：画电路图（四）

直到我排好原理图后，就可以开始排放电路图。

> 以下为排放好的电路原理图

![生成PCB](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/生成PCB.png)

电路原理图完成之后，我们就可以开始生成PCB了。

### AD操作：画PCB（五）



#### 1.器件排放

电路这么多器件，要用多大面积呢？

我们这时可以全选器件，然后 **菜单栏  -> 工具  ->  器件摆放 -> 在矩形区域排列**

这时重新一画，器件就按规则排列了，然后你就知道整个PCB大概需要多少面积。

下一步就可以裁剪PCB。



#### 2.快速裁剪PCB

首先对PCB设置好规格，在电路层中选择粉红色的**机械层**（Mechanical 1）

然后按 绘画 机械层 **线条**，把PCB板子裁剪成合适的长宽。（键盘快捷-P-L）

> 板子的大小取决于你的钱包。

按住Shift键，选中所有机械层线条

然后  **菜单栏  -> 设计  ->  板子形状 -> 在矩形区域排列**（键盘快捷-D-S-D）



#### 3.设置原点

**菜单栏  -> 编辑  ->  原点 -> 设置**   然后可以自己放置圆点的位置。



#### 4.隐藏元件

突出元件导通的过孔或者焊盘，**方便布线**。

快捷键Shift + S



#### 5.器件摆放

一般来说，PCB的元器件摆放一般按照功能区域划分。



##### 1.器件等距摆放

一般全选器件后，使用排列功能，让元件整齐排放，像棍子一样，如图LED灯整齐排放。

![QQ截图20201016113551](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/QQ截图20201016113551.png)

##### 2.在原理图选中PCB器件器件

在AD软件的窗户中，鼠标右键 -> 垂直分割，得到两个窗户。

然后 菜单栏  -> 工具 -> 交叉选择模式 （**快捷键 shift + ctrl + x**）

选中原理图的元件，PCB中的元件就会高亮。

往别的地方画个框，自动移动选中的元件在一起。

![交叉工具联合](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/交叉工具联合.png)

PCB的布局尽量按照信号优先，美观其次，毕竟我加入过外貌协会。



#### 6.设置PCB电路板电线的类

眼花缭乱的飞线看的不明不白，里面信号线与电源线痴痴缠绵。你需要分类！

菜单栏  -> 设计  -> 类 ，新建一个类规则，把所有的VCC，GND全部放进去，这样子就可以在PCB面板中设置显示高亮信号线

然后到面板（panel）调出PCB，修改信号与电源线颜色（Nat Color）



#### 7.干掉规则

> 元件有绿色错误。
>

那是软件规则设置错误了。

![设计规则检查器](https://raw.githubusercontent.com/Gah0/Gah0.github.io/master/_posts/20201110/设计规则检查器.png)

菜单栏  -> 工具  ->  设置规则检查 -> 右键去除所有错误，保留电气属性的报错。

然后连续按下键盘T ， M复位错误标志。



#### 8.敷铜

敷铜的话可以有效隔绝电路之间的信号线路与其他线路干扰

画好铜皮之后。

对铜皮右键 -> 键盘Y ->  重铺选中的铺铜 (R)

铺完之后记得更改网络。



### AD操作：打印文件（六）

#### 1.PDF

菜单栏->文件->智能PDF

PCB层的光绘文件一般保留Overlay, Mechanical, solder.



#### 2.bom表

 菜单栏->报告->bill of Materials

可以自由选择一些不必要的信息输出



#### 3.光绘文件

菜单栏->文件->制造输出->Gerber File

在“层”页面，绘制层->选择使用的。



#### 4.转孔文件

菜单栏->文件->制造输出->NC Drill Files



#### 5.SMT贴片

菜单栏->文件->装配输出->Generates pick and place files



#### 6.IPC网表

给厂家检测的

菜单栏->文件->制造输出->Test Point Report



这一次还是一个比较简单的项目，因此我积累到了很多的细节问题，希望下次打板能顺利进行。


