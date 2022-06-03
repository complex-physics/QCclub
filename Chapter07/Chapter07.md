光量子信息处理

## 概览

**时间：**2022年02月20日

**摘要：**  第一部分是一些量子信息学的概念简介。第二部分介绍常见线性光学元件及其功能用元件实现单量子比特和幺正操作和测量。第三部分讲量子态实验产生与测量，具体是纠缠光源和单光子的产生与测量。第四部分把前面讲到的线性光学元件，光源，探测器组合成的实验举了三个例子。第五部分介绍集成光量子技术，以即该技术和其他技术的对比。

**主讲人:** 孟雨，中国科学技术大学-量子信息重点实验室

**主要研究领域:**  实验量子光学，实验量子信息

**联系方式:** mengyu23@mail.ustc.edu.cn

**记录人：**庄嘉培



[TOC]

1. 量子信息学简介
2. 线性光学元件
3. 量子态实验产生与测量
4. 实验举例
   - Sagnac环产生纠缠源
   - CNOT gate
   - 多光子纠缠态
5. 集成光量子技术

# 1 量子信息学简介

> 本章是一些很基本的量子信息的概念，一般同学可以直接跳到第二章节关于`线性光学元件` 的介绍

## 量子比特

1. 经典的信息处理中, 基本单元是经典比特(bit) 只能取 0 或 1
2. 量子计算中的基本单元-**量子比特(qubit)** 利用了量子力学的叠加特性
   - 量子比特(qubit) 可以是0和1的叠加态, 用态矢表示为 $|0\rangle$ 和| $|1\rangle$, 
   - 态矢 $|0\rangle$ 和| $|1\rangle$ 形成一组正交基, 称为computational basis
   - 用间量的表示方式

$$
|0\rangle=\left[\begin{array}{l}
1 \\
0
\end{array}\right] \quad|1\rangle=\left[\begin{array}{l}
0 \\
1
\end{array}\right]
$$

3. Qubit可以用一个球空间的矢量来描述, 称为在洛赫球 (Bloch sphere)
   - 球面上的急表示纯态, 可以用球坐标表示为

$$
|q\rangle=\cos \left(\frac{\theta}{2}\right)|0\rangle+e^{i \phi} \sin \left(\frac{\theta}{2}\right)|1\rangle
$$

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326231228056.png" style="zoom: 33%;" />

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326231350892.png" style="zoom:50%;" />

## 量子逻辑门

### Pauli矩阵

- 单个qubit的矩阵空间可以由3个Pauli矩阵和单位矩阵构成

$$
\begin{aligned}
\sigma_{1}=\sigma_{x}=&\left[\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right] \\
\sigma_{2}=\sigma_{y}=&\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right] \\
\sigma_{3}=\sigma_{z}=&\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]
\\
\sigma_{0}=I=&\left[\begin{array}{ll}
1 & 0 \\
0 & 1
\end{array}\right]
\end{aligned}
$$

- 于是一个量子比特的密度矩阵可以表示为

$$
\hat{\rho}(\vec{P})=\frac{1}{2}(\hat{I}+\vec{P} \cdot \vec{\sigma})=\frac{1}{2}\left(\hat{I}+P_{x} \hat{\sigma}_{1}+P_{y} \hat{\sigma}_{2}+P_{z} \hat{\sigma}_{3}\right)
$$

- 三个Pauli算符对应 qubit 在Bloch球上饶三个轴转动的操作

$$
\begin{aligned}
\begin{array}{l}
\hat{R}_{x}(\theta) \equiv e^{-i \theta \hat{X} / 2}=\cos \frac{\theta}{2} \hat{I}-i \sin \frac{\theta}{2} \hat{X}=\left(\begin{array}{cc}
\cos \frac{\theta}{2} & -i \sin \frac{\theta}{2} \\
-i \sin \frac{\theta}{2} & \cos \frac{\theta}{2}
\end{array}\right) \\
\hat{R}_{y}(\theta) \equiv e^{-i \theta \hat{Y} / 2}=\cos \frac{\theta}{2} \hat{I}-i \sin \frac{\theta}{2} \hat{Y}=\left(\begin{array}{cc}
\cos \frac{\theta}{2} & -\sin \frac{\theta}{2} \\
\sin \frac{\theta}{2} & \cos \frac{\theta}{2}
\end{array}\right) \\
\hat{R}_{z}(\theta) \equiv e^{-i \theta \hat{Z} / 2}=\cos \frac{\theta}{2} \hat{I}-i \sin \frac{\theta}{2} \hat{Z}=\left(\begin{array}{cc}
e^{-i \theta / 2} & 0 \\
0 & e^{i \theta / 2}
\end{array}\right)
\end{array}
\end{aligned}
$$

- 任意一个单比特量子操作都可以分解为

$$
\hat{U}=e^{i \delta} \hat{R}_{z}(\alpha) \hat{R}_{y}(\theta) \hat{R}_{z}(\beta)
$$

### Hadamard 门

- Hadamard 门的矩阵表示

$$
H=\frac{1}{\sqrt{2}}\left[\begin{array}{rr}
1 & 1 \\
1 & -1
\end{array}\right]
$$

- Hadamard 门对量子态的作用效果

$$
\begin{aligned}
\begin{array}{ll}
H|0\rangle=|+\rangle & H|1\rangle=|-\rangle \\
H|+\rangle=|0\rangle & H|-\rangle=|1\rangle
\end{array}
\end{aligned}
$$

### 双比特逻辑门

例子：控制非门 (CNOT)

控制非门 (CNOT) 的矩阵表示
$$
\begin{aligned}
\text { CNOT }=\left(\begin{array}{llll}
1 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0
\end{array}\right)
\end{aligned}
$$
控制非门 (CNOT) 构建纠缠态

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326232436356.png" style="zoom:50%;" />

## 量子测量

1. Pauli-Z的本征态为 $|0\rangle$ 和 $|1\rangle$ 
   - 也就是矩阵 $\left[\begin{array}{cc}1 & 0 \\ 0 & -1\end{array}\right]$ 拥有本征向量 $|0\rangle=\left[\begin{array}{l}1 \\ 0\end{array}\right]$ 和 $|1\rangle=\left[\begin{array}{l}0 \\ 1\end{array}\right]$
2. 对于任意一个叠加态 $|\psi\rangle=\alpha|0\rangle+\beta| 1\rangle$, 测量会破坏其叠加特性, 概率性的得到| $\mid 0\rangle$ 或者 $|1\rangle$ 。





# 2 线性光学元件

1. 利用物理系统（光子）的特性进行编码的常见方式
2. 常见线性光学元件及其功能
3. 用元件实现单qubit \& 幺正操作和测量
4. 不同编码方式之间的转换

## 光子系统中的qubit编码

> 利用物理系统（光子）的特性进行编码的常见方式

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326233501199.png" style="zoom:50%;" />

1. 偏振自由度编码qubit：
   - H表示水平偏振态 $|0\rangle_{L}=|H\rangle$
   - V表示坚直偏振态 $|1\rangle_{L}=|V\rangle$
2. 路径自由度编码：
   - 第一个路径 $|0\rangle_{L}=|p a t h a\rangle$
   - 第二个路径 $|1\rangle_{L}=|\operatorname{path} b\rangle$
   - 更多的路径......
     1. 路径编码可以编码不止一个qubit，可以拓展到高维编码
     2. 但是路径编码对相位是很敏感的，容易使得光路不稳定
     3. 所以使用较多的是用偏振来编码
3. 其他编码方式:
   - 光子的到达时间(time-bin)
   - 轨道角动量自由度
   - 频率自由度

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/Snipaste_2022-03-26_23-35-41.png" style="zoom:50%;" />

## 线性光学元件

### 波片

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327104203810.png" style="zoom: 33%;" />

- **波片**是操控偏振的光学器件
- 组成：双折射晶体
- 功能：
  - O光和E光在相位上出现时间上的分离
- 常见的波片
  1. 半波片 Half wave plate (HWP) ：O光和E光之间加入$\frac{ \lambda }{2}$ 的相位
  2. 四分之一波片  quart wave plate (QWP)：O光和E光之间加入$\frac{ \lambda }{4}$ 的相位

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327104323420.png" style="zoom:50%;" />

### 其他常见器件

1. 分束器 beam splitter (BS)
   - 功能：将入射光按照不同强度比例，向两个端口出射
   - 特点：偏振不敏感，一般是5-5分

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327104537619.png" style="zoom:50%;" />

2. 偏振分束器 polarization beam splitter (PBS)
   - 功能
     1. 水平偏振的光透射
     2. 竖直偏振的光反射

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327104954253.png" style="zoom:50%;" />

3. 光束偏移器 beam displacer (BD)
   - 利用晶体的双折射效应
   - 不同偏振的光会在横向空间上分开

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327105208516.png" style="zoom:50%;" />



##  单qubit \& 幺正操作和测量

> 通过完备基底类似概念的门组合，构建任意单qubit门，在实验中有利于简化原件的种类

1. 任意的单qubit门的**幺正演化操作**, 可以通过2个QWP(四分之一波片)和 HWP(半波片)的组合, 可以实现

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326235009828.png" style="zoom:50%;" />

2. 任意单qubit**测量**, 可以通过1个QWP+1个HWP+1个PBS的 组合实现

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220326235028456.png" style="zoom:50%;" />

其中SPAD是指单光子雪崩二极管，起到光电转换的功能。

## 单qubit 模式自由度转换

路径编码和模式编码之间可以等价转换 

1. 基于PBS：偏振编码$\rightarrow$路径编码$\rightarrow$偏振编码

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327110348688.png" style="zoom:50%;" />

2. 基于BD
   - 偏振编码$\rightarrow$路径编码
   - 演讲者亲自的实验

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327110822519.png" style="zoom:50%;" />



# 3 量子态实验产生与测量

## 纠缠光源

**参量下转换过程**产生纠缠光子对：

1. 当一束频率为 $\omega_{p}$ 的激光
2. 经过一个高功率的激光器泵浦时
   - 一块二阶极化率 $\chi^{(2)}$ 不为 0 的非线性光学晶体 
3. 晶体的非线性作用有概率使得泵浦光子同时产生
   - 一个频率为 $\omega_{s}$ 信号光子
   - 和一个频率为 $\omega_{i}$ i闲频光子

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327001406659.png" style="zoom:50%;" />

光子对满足动量守恒和能量守恒

- 所以光子的自旋，偏振等物理相互关联
- 所以这对光子是纠缠光子对

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327001459060.png" style="zoom:50%;" />

### 相位匹配

相位匹配情况的不同可将参量下转换分为 I型 和 II型

- I型相位匹配: 
  - 信号光和闲频光取相同的偏振且与泵浦光垂直, 
  - 产生的参量光的空间分布是以泵浦光为轴成锥形分布;
- II型相位匹配: 
  - 产生的两个光子偏振互相垂直, 
  - 空间分布为两个顶点重含的圆锥

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327002019270.png" style="zoom:50%;" />



## 光子的符合测量

多通道符合计数 Multichannel Coincidence counting

- 动机：非线性晶体产生纠缠光子对是概率性的，一般非纠缠的光子是大大多于纠缠光子，所以需要找出纠缠光子对的信号，否则纠缠光子对的信号就淹没在普通光子中
- 机制：
  1. 如图的黑框是个时间窗口
  2. 在同个时间窗口里到达的光子被判定为纠缠光子，才进行计数
  3. 实际实验中，一秒钟单光子计数普通光子大约百万次，纠缠光子计数到的小两个数量级

## 单光子源

产生单光子的常见两种方式

1. 准单光子源：衰减激光强调, 概率性的, 多光子事件存在的概率不为 0 。
2. "预报式" (heralding) 单光子源: 对一系列纠缠光子对中的信号光子进行破坏式测量, 即可宣布式地得到一系列 的闲频单光子。
   - 理论上对信号光子测量成功的概率即为闲频光子的预报效率

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220327114016826.png" style="zoom:50%;" />



## 光子收集探测

光子需要转换为电信号才能被计算机处理，光子收集系统包含

1. 光纤耦合系统——耦合架、耦合头 (光纤准直器、透镜) 
2. 单光子计数器——常用雪崩放电二极管 Single-photon avalanche diode (SPAD)
3. 多通道符合计数模块

# 4 实验举例

> 前面讲到的线性光学元件，光源，探测器组合成的

## Sagnac环产生纠缠源

II型周期性极化磷酸氧钛钾(periodically poled KTiOPO4, PPKTP) 晶体通过Sagnac环结构产生偏振纠缠源

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526152646439.png" style="zoom:67%;" />![](C:\Users\JPZhuang\AppData\Roaming\Typora\typora-user-images\image-20220526152713203.png)



## CNOT gate



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526152646439.png" style="zoom:67%;" />



## 多光子纠缠态



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526152713203.png" style="zoom:67%;" />





# 5 集成光量子技术 

集成光量子技术就是把激光器、调制器、探测器等有源器件用光波导分数器、偏振器、滤偏振滤波器等无源器件连接起来，并且集成在同一个衬底上的光学系统。

- 它具有多功能化、高度集成化、小型化等特点。

与光学平台比较:

- 小型化利于集成, 稳定更抗品;
- 与电子芯㤃加工的CMOSI艺兼容,
- 硅具有良好的导光性能, 在通讯波段透明;

与半导体芯㲏比较:

- 光波导, 光束的走向更容易控制;
- 利于光子的量子特性吅以提升计算模拟速度;
- 波分复用技术使光子传输带宽大大增加;



光波导 (optical waveguide) 是引导光波在其传播的介 质装置, 又称介质关波导。

- 集成光波导，包括平面 (薄膜) 介质光波导和条形介质光波导
- 圆柱形光波导一一光纤

光子芯片通常采用路径编码的方式



## 片上编码基础

下面来介绍一下一些以路径编码为主的无源器件

1. 定向耦合器 Directional couple DC-H_-ladamard gate



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526153624098.png" style="zoom:67%;" />



定向耦合器它是对波长敏感的，所以仅只有在有限带宽的时候才适用。为了解决这一问题，又研究了多模干涉耦含器

2. 多模干涉耦含器 Multimode Interferometer MMI — 基于自成象原理 (self-imaging)

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526153705739.png" style="zoom:67%;" />



相位调节器 Phase shifter

- 马赫曾德干涉仪 Mach Zehnder interferometer $M Z I$ 
  - 2个方向耦合器或多模干涉耦合器
  - 1个相位调节 
- SU2么正变换
  - 1个MZI
  - 2个相位调节器

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526153501907.png" style="zoom:80%;" />

## 片上纠缠源

基于自发四波混频原理

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/Snipaste_2022-05-26_15-37-47.png" style="zoom:67%;" />

北京大学的王建威老师组做的一个片上高维纠缠态的一个产生原理图



## 片上的CNOT门

2008 年 O $^{\prime}$ brien组首次实现CNOT门，证明了片上线路的可行性。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526154037903.png" style="zoom:80%;" />

## Metalens阵列多光子源

基于超构透镜阵列的高维多光子量子源

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526154127829.png" style="zoom:80%;" />

国内做相关方面研究的组

- 天津大学一一李小英
- 北京大学一一王剑威
- 浙江大学一一戴道锌
- 上海交通大学一一金贤敏
- 中国科学技术大学一一任希锋、冯兰天、李传锋（存储）



# 附录：

## 参考文献

1. 集成光量子技术方面的综述 Wang, J. et al. Integrated photonic quantum technologies. Nature Photon. 14, 273 (2020).
2. 一些博士论文，可以发邮件给孟雨求论文  mengyu23@mail.ustc.edu.cn

## 问答

