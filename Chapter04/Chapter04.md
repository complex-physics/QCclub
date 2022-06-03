量子信息遇到人工智能

# 概览

**时间：**2022年01月16日

**摘要：** 本次演讲三大部分。第1部分用概率模型理解量子测量，发现只能对单量子比特可以刻画，无法刻画多量子比特。第2部分用测量结果来重构黑盒中的量子态，指出重构密度矩阵是指数困难的，但是可以用Classical Shadow Tomography(CST)重构预测系统性质。扈鸿业的研究指出，CST重构和纠缠模式有关；并且提出用局域哈密顿量的演化可以替代量子线路演化动力学。第3部分展示用机器学习来帮助重构和相分类等问题。

**主讲人:** 扈鸿业，加州大学圣地亚哥分校博士候选人，16年在北京大学吴飙老师指导下获得学士学位。

**主要研究领域:** 量子信息，人工智能，量子多体物理。

**个人主页:** http://www.hongyehu.com/

**记录人：**黄清扬；庄嘉培



[TOC]



# 用概率模型理解量子测量

> 假如我们不知道量子力学理论，我们可以怎么理解实验对量子系统的测量结果呢？

用概率模型是一个很自然的想法。这部分会介绍怎么用概率模型理解量子测量结果

1. 单量子比特
2. 双量子比特

## 单量子比特

对于单量子比特的量子态
$$
|\uparrow\rangle+| \downarrow \rangle
$$

#### 测量

1. 算符 $\sigma_{z}$ 得到的测量结果：$\uparrow,\downarrow,\downarrow,\uparrow,\downarrow,\uparrow,\downarrow\dots$
2. 算符 $\sigma_{x}$ 得到的测量结果：$\rightarrow,\rightarrow,\rightarrow,\rightarrow\dots$

#### 建模

建立隐变量模型

假设隐变量 $\vec{\lambda}$ 有两位值

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220603200337905.png" style="zoom:67%;" />

隐变量的分布 $p_{|\psi\rangle}(\vec{\lambda})$ 取决于黑盒中我们要测量的量子态
$$
\begin{array}{ll}
p\left(+1 \mid 10, \sigma_{x}\right)=1 & p\left(+1 \mid 00, \sigma_{z}\right)=1 \\
p\left(+1 \mid 00, \sigma_{x}\right)=1 & p\left(-1 \mid 10, \sigma_{z}\right)=1
\end{array}
$$
公式含义

- $p\left(+1 \mid 10, \sigma_{x}\right)=1$：如果隐变量 $\vec{\lambda}=10$，通过$\sigma_{x}$测量，模型百分百给出$+1$的结果 

通过这个隐变量模型，完全可以描述上诉量子测量实验的结果‘

> 量子力学看起来没有很神奇
>
> 但是这只是单量子比特，所以我们需要探索双量子比特

## 双量子比特

纠缠的两个量子比特形成了EPR态，如果我们把这一对粒子分别发给Rick 和 Morty

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220123214433791.png" style="zoom:50%;" />

1. 如果计算Rick 和 Morty之间的互信息(mutual information)是2 bits，但是在经典系统中，他们的互信息不会超过1 bit

> 局域隐变量理论(local hidden variable theory) 可否描述2量子比特？

#### 测量

对于双量子比特的量子态——GHZ态
$$
|\uparrow\uparrow\rangle+|\downarrow \downarrow\rangle
$$

Rick 和 Morty可以测量三个方向

- $\vec{n}_{1} \cdot \vec{\sigma}$
- $ \vec{n}_{2} \cdot \vec{\sigma}$ 
- $\vec{n}_{3} \cdot \vec{\sigma}$

#### 局域隐变量理论

假设我们有一个局域隐变量(local hidden variable)模型可以描述实验，那么需要三个经典比特信息来描述隐变量
$$
\begin{array}{ccc}
\text { Rick } & \text { Morty } & p \\
 000 & 000 & p_{1} \\
001 & 001 & p_{2} \\
010 & 010 & p_{3} \\
011 & 011 & p_{4} \\
100 & 100 & p_{5} \\
101 & 101 & p_{6} \\
110 & 110 & p_{7} \\
111 & 111 & p_{8} \\
\end{array}
$$
其中

- 表格中三位数字，第一位表示对第一个方向$\vec{n}_{1} \cdot \vec{\sigma}$的测量
  - 如果是0，表示测量到+1
  - 如果是1，表示测量到-1
- 另外两位类似，对于另外两个方向的测量

如果是经典模型，会有以下关系
$$
\begin{array}{l}
p\left(\vec{n}_{1} \cdot \vec{\sigma}_{A}=\vec{n}_{2} \cdot \vec{\sigma}_{B}\right)=p_{1}+p_{2}+p_{7}+p_{8} \\
p\left(\vec{n}_{2} \cdot \vec{\sigma}_{A}=\vec{n}_{3} \cdot \vec{\sigma}_{B}\right)=p_{1}+p_{4}+p_{5}+p_{8} \\
p\left(\vec{n}_{3} \cdot \vec{\sigma}_{A}=\vec{n}_{1} \cdot \vec{\sigma}_{B}\right)=p_{1}+p_{3}+p_{6}+p_{8}
\end{array}
$$
这些公式的含义

1. $p\left(\vec{n}_{1} \cdot \vec{\sigma}_{A}=\vec{n}_{2} \cdot \vec{\sigma}_{B}\right)$ 表示Rick测量$\vec{n}_{1} \cdot \vec{\sigma}$ 得到的结果和 Morty测量$\vec{n}_{1} \cdot \vec{\sigma}$ 得到的结果是一样的概率

那么有个推论
$$
\begin{aligned}
&p\left(\vec{n}_{1} \cdot \vec{\sigma}_{A}=\vec{n}_{2} \cdot \vec{\sigma}_{B}\right)+p\left(\vec{n}_{2} \cdot \vec{\sigma}_{A}=\vec{n}_{3} \cdot \vec{\sigma}_{B}\right)+p\left(\vec{n}_{3} \cdot \vec{\sigma}_{A}=\vec{n}_{1} \cdot \vec{\sigma}_{B}\right) 
\\=&1+2 p_{1}+2 p_{8} \geq 1
\end{aligned}
$$
如果真的存在这样的经典理论，给出的预测是
$$
\frac{1+\vec{n}_{1} \cdot \vec{n}_{2}}{2}+\frac{1+\vec{n}_{2} \cdot \vec{n}_{3}}{2}+\frac{1+\vec{n}_{3} \cdot \vec{n}_{1}}{2} \geq 1
$$

#### 量子理论

但是如果测量方向选择如下

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220123233836429.png" style="zoom:50%;" />

量子理论和实验会告诉你
$$
\begin{aligned}
&\frac{1+\vec{n}_{1} \cdot \vec{n}_{2}}{2}+\frac{1+\vec{n}_{2} \cdot \vec{n}_{3}}{2}+\frac{1+\vec{n}_{3} \cdot \vec{n}_{1}}{2} =\frac{3}{4} \\
&\qquad \qquad \qquad \qquad \qquad \Downarrow\\
&\qquad \qquad \qquad \qquad \quad \frac{3}{4}\geq 1
\end{aligned}
$$
感兴趣的同学可以用在线量子计算机做这个实验，参考 [Local Reality and the CHSH Inequality](https://qiskit.org/textbook/ch-demos/chsh.html)

## 评论

> 1. 当你有两个量子比特，并且你可以随机测量这三个方向的时候，那么你经典的概率模型，是不足以描述量子的实验现象。
>    - 所以局域隐变量(local hidden variable)不足以重现量子力学的结果
> 2. 隐变量模型其实就是非监督学习里面的生成模型(generative models)
>    - 前面讲概率模式是局域的，存在可能性经典生成模型可以复现量子力学的结果
> 3. 偏哲学的讨论，这个问题就是当年爱因斯坦和波尔的一个大论战，Locality 和Reality，如果对具体内容感兴趣参考
>    - Roger Penrose 的书《[The Road to Reality](https://en.wikipedia.org/wiki/The_Road_to_Reality)》
>    - 中文译本《[通向实在之路](https://book.douban.com/subject/25823056/)》罗杰•彭罗斯

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/220px-The_Road_to_Reality.jpg" style="zoom: 67%;" />

# 量子态层析成像

在现实中，我们没办法直接观测到量子态，我们观测到的都是测量得到的经典数据。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124000237397.png" style="zoom:80%;" />

所以我们可以把量子系统看成一个**黑盒**，那么就有两大任务

1. 怎么去通过比较好的设计实验？去测量黑盒信息。
2. 怎么样去利用这些测量到的经典的信息？去预测这个量子黑盒的一些性质。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124001312794.png" style="zoom:50%;" />

## 密度矩阵

如果要写下对量子体系的完整描述，需要用密度矩阵(Density matrix)
$$
D \times D=\left(\begin{array}{llll}
* & * & * & * \\
* & * & * & * \\
* & * & * & * \\
* & * & * & *
\end{array}\right)
$$
密度矩阵的性质

- Hermitian
- Identity trace
- Positive definite

对角化的值是经典概率，所以要是正数，加起来等于1。这些性质保证了本征值符合这些条件。

例子 2 qubits GHZ 态的密度矩阵
$$
\begin{array}{l}
\rho_{ GHZ }=\left|\psi_{ GHZ }\right\rangle\left\langle\psi_{ GHZ }\right|=\left(\begin{array}{cccc}
0.5 & 0 & 0 & 0.5 \\
0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 \\
0.5 & 0 & 0 & 0.5
\end{array}\right)
\end{array}
$$
密度矩阵可以用泡利矩阵$\sigma$展开
$$
|\psi\rangle\langle\psi|=\frac{1}{2^{n / 2}} \sum_{\alpha} \gamma_{\alpha} \sigma^{\alpha}
$$
其中

- $\gamma_{\alpha}$ 是展开系数
- $\gamma_{\alpha}$ 可以写成  $\gamma_{\alpha}=\frac{1}{2^{n / 2}} \operatorname{Tr}\left[|\psi\rangle\langle\psi| \sigma^{\alpha}\right]$
- $\sigma^{\alpha}$ 表示一个泡利串，比如 $\sigma^{0321}=I Z Y X$



## 量子态层析成像

通过实验得到密度矩阵的过程，称为量子态层析成像技术(Quantum state tomography) 简称。

但是这种过程的代价是非常巨大的，因为

1. 每次测量都是对量子态的破坏，所以做多少测量就需要做出多少份的量子态
2. [arXiv:1508.01797](https://arxiv.org/abs/1508.01797) 这篇论文证明了，QST得到密度矩阵的过程需要的量子态数量是指数增长的



#### fidelity

目标密度矩阵是 $\rho=\frac{1}{2^{n / 2}} \sum_{\alpha} \gamma_{\alpha} \sigma^{\alpha}$，但是你制备出来的是 $\rho^{\prime}=\frac{1}{2^{n / 2}} \sum_{\alpha} \gamma_{\alpha}^{\prime} \sigma^{\alpha}$. fidelity就是描述两个量之间的相似程度
$$
F=\langle\psi|\rho| \psi\rangle=\sum_{\alpha} \gamma_{\alpha} \gamma_{\alpha}^{\prime}=\underset{\alpha \sim \gamma_{\alpha}^{2}}{ E } \frac{\gamma_{\alpha}^{\prime}}{\gamma_{\alpha}}
$$
理论上也是需要指数增长次数的实验去估计这个值

- 例如，测量8个粒子的系统，需要大约$\sim 656,000$ 次的测量



## 明确目标

在大部分情况下，我们是要预测量子态的一些性质，而不需要密度矩阵这么完整的信息。例如

1. 量子化学中找基态
2. 拓扑物态中物相分类

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124004846693.png" style="zoom:80%;" />

# Classical Shadow Tomography

2020年，Hsin-Yuan Huang,和John Preskill提出Classical Shadow Tomography [arXiv:2002.08953](https://arxiv.org/abs/2002.08953)

- 第一部分是量子测量
- 第二步是在经典电脑中处理
- 可以预测一些Quantum Fidelity等一些性质，而且需要的测量次数不会指数暴涨

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124005417746.png" style="zoom:80%;" />

#### 第一部分：测量

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124010140411.png" style="zoom:50%;" />

流程

1. 制备一个量子态 $\rho$
2. 随机选择一个幺正演化 $\rho \rightarrow \rho^{\prime}=U \rho U^{\dagger}$
3. 测量 $\rho^{\prime} \rightarrow|b\rangle\langle b|$
4. 电脑计算 $|b\rangle\left\langle b\left|\rightarrow \hat{\sigma}_{U, b}=U^{\dagger}\right| b\right\rangle\langle b| U$

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124010413065.png" style="zoom:50%;" />

得到的 $\hat{\sigma}_{U, b}=U^{\dagger}|b\rangle\langle b| U$ 就是Classical Shadows

其中

- 幺正演化的选择是随机的 $P(U)$
- 测量的过程也是随机的 

$$
\begin{array}{l}
\operatorname{Tr}\left(|b\rangle\langle b| \rho^{\prime}\right)=\operatorname{Tr}\left(|b\rangle\langle b| U \rho U^{\dagger}\right) \\
=\operatorname{Tr}\left(U^{\dagger}|b\rangle\langle b| U \rho\right)=\operatorname{Tr}\left(\hat{\sigma}_{U, b} \rho\right)
\end{array}
$$

- 所以最后得到 $\hat{\sigma}_{U, b}$ 的概率是两个概率的乘积

$$
P\left(\hat{\sigma}_{U, b} \mid \rho\right)=P(U) \operatorname{Tr}\left(\hat{\sigma}_{U, b} \rho\right)
$$

- 多次实验之后得到数据集

$$
\left\{\hat{\sigma}_{U, b} \mid P\left(\hat{\sigma}_{U, b} \mid \rho\right)=P(U) \operatorname{Tr}\left(\hat{\sigma}_{U, b} \rho\right)\right\}
$$



#### 第二部分：重构

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124010902523.png" style="zoom:50%;" />

从这些Classical Shadows的数据集中，怎么重构出密度矩阵？——取平均
$$
\sigma=\underset{\hat{\sigma} \in E _{\sigma \mid \rho}}{ E } \hat{\sigma}=\sum_{U, \hat{\sigma}} \hat{\sigma} P(U) \operatorname{Tr}(\hat{\sigma} \rho) 
$$
平均值 $\sigma$ 和密度矩阵 $\rho$ 之间是一个线性映射 $M$，称为measurement channel
$$
\sigma=M [\rho]
$$
如果选取幺正演化$U$ 是足够随机的，那么上式是可逆的
$$
\rho={ M ^{-1}[\sigma]}=\underset{\hat{\sigma} \in E _{\sigma \mid \rho}}{ E } M ^{-1}[\hat{\sigma}]
$$
其中

- $M ^{-1}$ 叫reconstruction map
- $M ^{-1}$ 是预测量子性质的基础

## reconstruction map

用$M ^{-1}$ 预测量子性质

1. 重构密度矩阵 $\rho=\underset{\hat{\sigma} \in E _{\sigma \mid \rho}}{ E } M ^{-1}[\hat{\sigma}]$
2. 线性性质 $\hat{o}=\operatorname{Tr}\left(O M ^{-1}[\hat{a}]\right)$
3. 非线性性质

$$
\begin{aligned}
e^{-S_{\rho}(A)} &=\operatorname{Tr}_{A}\left(\operatorname{Tr}_{\bar{A}} \rho\right)^{2} \\
&=\underset{\hat{\sigma}, \hat{\sigma}^{\prime} \in E _{\sigma \mid \rho}}{ E } \operatorname{Tr}_{A}\left(\operatorname{Tr}_{\bar{A}} M ^{-1}[\hat{\sigma}] \operatorname{Tr}_{\bar{A}} M ^{-1}\left[\hat{\sigma}^{\prime}\right]\right) 
\end{aligned}
$$

> 但是构建 $M ^{-1}$ 也不是容易的事情

## 例子

以前知道可构建 $M ^{-1}$ 的Unitary channel只有两个

1. Global Haar Unitary
2. Local Haar Unitary

#### Global Haar

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124012754451.png" style="zoom:50%;" />
$$
\begin{aligned}
M [\rho]=\frac{1}{D+1}(\rho+ 1 )\\
M ^{-1}[\sigma]=(D+1) \sigma- 1
\end{aligned}
$$
优缺点

1. 优点：适合低秩观察量，比如Fidelity
2. 缺点：构建这个矩阵需要很深的量子线路，实验上不易实现

#### Local Haar Unitary

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124013056048.png" style="zoom:50%;" />


$$
\begin{aligned}
M [\rho]=\bigotimes_{i} \frac{1}{d+1}\left(\rho_{i}+ 1 _{i}\right)\\
M ^{-1}[\sigma]=\bigotimes_{i}\left((d+1) \sigma_{i}- 1 _{i}\right)
\end{aligned}
$$
优缺点

1. 优点：适合局域的性质
2. 缺点：非局域性质不好预测



上面两个是极端

- Local Haar Unitary没有信息交互
- Global Haar Unitary所有的信息都混在一起

那么我们可不可以构建中间的合适演化矩阵？有的，如下

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124013545405.png" style="zoom:50%;" />

### 纠缠

上面三个例子，线路产生的纠缠分别是

1. Global Haar产生的纠缠是volume law纠缠
2. Local Haar产生的纠缠是没有纠缠
3. shallow circuit产生的纠缠是介于上面两者之间的

> 意识到，纠缠的模式可能决定了  $M ^{-1}$ 的特性

这个是扈鸿业做的工作，他们证明了这个猜想。接下来介绍这个工作

# Locally Scrambled Shadow Tomography

重构过程
$$
\rho= M ^{-1}[\sigma]=d^{N} \sum_{A \in 2^{\Omega} N} r_{A} \sigma_{A}
$$
其中

- $r_{A}$ 取决于纠缠性质

## 流程

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124015703800.png" style="zoom:50%;" />

1-计算演化矩阵的纠缠模式(entanglement patterns)
$$
W^{(2)}[\sigma]=\underset{U}{ E }\left(e^{-S_{\{\}}^{(2)}}, e^{-S_{\{1\}}^{(2)}}, e^{-S_{\{2\}}^{(2)}}, e^{-S_{\{1,2\}}^{(2)}}, \cdots, e^{-S_{A}^{(2)}}, \cdot\right)
$$
2-知道了纠缠模式之后，可以解约束线性方程
$$
\sum_{A, C} r_{A} F_{A, B, C} W_{C}^{(2)}[\sigma]=\delta_{B,(11 \cdots 1)}
$$
3-重构
$$
\rho= M ^{-1}[\sigma]=d^{N} \sum_{A \in 2^{\Omega} N} r_{A} \sigma_{A}
$$
这个工作的意义

1. 发现：演化矩阵的纠缠模式(entanglement patterns)，决定了重构$M ^{-1}$ 
2. 连接了量子动力学(演化矩阵$U$)和量子信息(量子态层析成像)



## 数值例子

简要回顾刚刚做了什么

1. 原本的量子态 $\rho$ 经过演化 $\rho \rightarrow \rho^{\prime}=U \rho U^{\dagger}$ 后测量
2. 测量数据，根据扈鸿业他们工作提出的纠缠模式方法，计算出重构的量子态 $\rho_{\text {construct }}$

接下来是计算，重构的量子态 $\rho_{\text {construct }}$和原本的量子态 $\rho$ 的Fidelity  
$$
F \left(\rho, \rho_{\text {construct }}\right)
$$

#### 结果-1

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124020228411.png" style="zoom:50%;" />

Fidelity接近1，说明重构的效果很好。

#### 结果-2

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124020353599.png" style="zoom:50%;" />

1. 如果没有加演化，直接测量 $\rho$，重构需要的测量次数是指数增长的（蓝线）
2. 如果加了3层shallow circuit的演化线路，测量次数增长很小（红线）
3. 如果加的shallow circuit层数趋于无穷，不管系统的量子比特数有多少，做测量实验的次数不用增长（绿线）

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124013545405.png" style="zoom:50%;" />

# Approximate Tomography with Local Hamiltonian Dynamics

演化线路的物理实验上很难实现

![image-20220124021458413](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124021458413.png)

但是这种幺正演化的动力学过程，我们是否可以用一个哈密顿量来产生随机动力学，替代线路的动力学过程？
$$
U=e^{-i H T}
$$

1. 这个哈密顿量是局域的
2. 这个哈密顿量的演化是混沌的，因此可以历遍所有态空间

## 自旋哈密顿量

选择了无序的自旋哈密顿量
$$
H_{t}=\sum_{\langle i, j\rangle} J_{i j} X_{i} X_{j}+h \sum_{i}\left(\cos \theta_{t} X_{i}+\sin \theta_{t} Y_{i}\right)
$$
其中

- X方向上的耦合 $J_{i j} \sim \operatorname{Uni}\left[J-\frac{J}{2}, J+\frac{J}{2}\right]$ 是随机的

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124033700096.png" style="zoom: 50%;" />

- 磁场方向在不同时刻也是随机选择的

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124022203321.png" style="zoom:50%;" />

最后得到的演化矩阵
$$
U=\prod_{t=1}^{T} e^{-i H_{t}}
$$
这种过程是比较容易在量子模拟器上实现

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124022349262.png" style="zoom:50%;" />

## Local Frame Potential

为了刻画这个演化 $U=\prod_{t=1}^{T} e^{-i H_{t}}$ 是否满足前面说的重构，提出Local Frame Potential的概念

- Local Frame Potential如果越接近0，越满足条件

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124040246396.png" style="zoom:50%;" />

- 可以看出随着时间，Local Frame Potential下降很快。所以只要超过一个不长的时间，就可以拿去做Classical Shadow Tomography

## 模拟结果

![](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124023201550.png)

只要一个quench无序哈密顿量就足够多信息，去重构黑盒中的量子态

比如去计算黑盒中量子态的保真度(Fidelity)

![](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124023329786.png)

- 可以看出经过一个短时间的演化，保真度(Fidelity)就能接近1
- 之前的研究大家认为需要全局的信息搅动(scrambling)，但是全局的搅动需要等更长的时间
- 扈鸿业的研究提出局域的信息搅动(local scrambling)就足够

## 第二部分的小结

从量子态层析成像开始

1. Classical Shadow Tomography
2. Locally Scrambled Shadow Tomography
3. Approximate Tomography with Local Hamiltonian Dynamics

这些构成本次演讲的第二部门，目标是重构黑盒中的量子态

1. 先介绍了前人的工作Classical Shadow Tomography
2. 然后介绍扈鸿业自己的演讲，用纠缠模式来帮助重构
3. 用局域哈密顿量动力学来替代演化线路

# 机器学习

第二部分讲的重构，我们是否可以用机器学习来帮忙呢？

## 问题描述

一族哈密顿量$H(x)$，每个哈密顿量基态的量子态，它的classical shadows对应图中黑点

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124025120595.png" style="zoom:50%;" />

如果现在给你一个新的哈密顿量，这个哈密顿量基态的classical shadows红色的点表示，这个红色的点在哪里？也就是说classical shadows是什么样的？

> classical shadows例子
>
> 1-对每个点的量子比特测量，得到
> $$
> \left|s_{i}^{(t)}\right\rangle \in\{|0\rangle,|1\rangle,|+\rangle,|-\rangle,|+i\rangle,|-i\rangle\}
> $$
> 2-构建泡利算子
> $$
> \sigma_{i}^{(t)}=3\left|s_{i}^{(t)}\right\rangle\left\langle s_{i}^{(t)}\right|- I
> $$
> 3-把算子直积得到classical shadows
> $$
> \sigma_{T}(\rho)=\frac{1}{T} \sum_{t=1}^{T} \sigma_{1}^{(t)} \otimes \cdots \otimes \sigma_{n}^{(t)}
> $$



## 核模型

$$
\hat{\sigma}(x)=\frac{1}{N} \sum_{l=1}^{N} k\left(x, x_{l}\right) \sigma_{T}\left(\rho\left(x_{l}\right)\right)
$$

用核模型证明，如果有黑色这些点，机器可以预测出红色点

1-选择一个核Dirichlet kernel
$$
k\left(x, x_{l}\right)=\sum_{k,\|k\|_{2} \leq \Lambda} \cos \left(\pi k\left(x-x_{l}\right)\right)
$$
H-Y Huang, R. Kueng, G. Torlai, V. Albert, J. Preskill (2021) 这篇文章给出，如果红色的点和黑色的点是在一个相内，之间没有相变。那么机器学习可以很准确预测红色点。

- 证明过程详见Preskill的论文 [arXiv:2106.12627](https://arxiv.org/abs/2106.12627) 

## 物相分类

用机器学习预测相分类

#### 对称性破缺相变

对于朗道提出的对称性破缺相变分类

- 存在一些和对称性有关的局域观测量$O$，使得
  1. $\operatorname{tr}(O \rho) \geq 1, \forall \rho \in$ 属于相 $A $ 
  2. $ \operatorname{tr}(O \rho)<\hat{ i }, \forall \rho \in$ 属于相 $B$
- 机器是可以学到的，在特征空间，学到一个超平面(hyperplane) 来区分两个相

#### 拓扑相

对于拓扑相，有个很有趣的理论

- 线性的性质不能区分拓扑量子态

> **Theorem:** Consider two distinct topological phases $A$ and $B$. No observable $O$ exists such that
> $$
> \operatorname{tr}(O \rho)>0, \forall \rho \in \text { phase } A, \operatorname{tr}(O \rho) \leq 0, \forall \rho \in \text { phase } B
> $$

对这个理论有兴趣的可以参考

1. Preskill的论文 [arXiv:2106.12627](https://arxiv.org/abs/2106.12627) 
2. 文小刚老师的书 《Quantum Information Meets Quantum Matter》[arXiv:1508.02595](https://arxiv.org/abs/1508.02595)

## 数值结果

还是Preskill的论文 [arXiv:2106.12627](https://arxiv.org/abs/2106.12627) 里面的结果

Rydberg原子模型

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124032526270.png" style="zoom:50%;" />

其中参数Detuning $(\Delta / \Omega)$和interaction range决定了3个物相

1. Disordered
2. Z2-ordered
3. Z3-ordered

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124032657428.png" style="zoom:50%;" />

经过训练，预测基态的表征

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124033001452.png" style="zoom:67%;" />

另外一个结果是对于2D anti-ferromagnetic random Heisenberg model
$$
H=\sum_{\langle i j\rangle} J_{i j}\left(X_{i} X_{j}+Y_{i} Y_{j}+Z_{i} Z_{j}\right)
$$
预测基态，和DMRG结果对比

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220124033207873.png" style="zoom:50%;" />

# 结论

1. 很多量子模拟器在发展
2. 但是重构完整的密度矩阵(quantum state tomography)是不可能的
3. 本演讲中的Classical shadows加上机器学习去理解黑盒中的量子态







# 附录：相关资源

第1部分

1. 在线量子计算机做不等式实验 [Local Reality and the CHSH Inequality](https://qiskit.org/textbook/ch-demos/chsh.html)
2. 量子测量的一些偏哲学的讨论，Roger Penrose 的书《[The Road to Reality](https://en.wikipedia.org/wiki/The_Road_to_Reality)》中文译本《[通向实在之路](https://book.douban.com/subject/25823056/)》罗杰•彭罗斯

第2部分

1. [arXiv:1508.01797](https://arxiv.org/abs/1508.01797) 这篇论文证明了，QST得到密度矩阵的过程需要的量子态数量是指数增长的
2. [arXiv:2002.08953](https://arxiv.org/abs/2002.08953) John Preskill提出Classical Shadow Tomography 
3. [arxiv2107.04817](https://arxiv.org/pdf/2107.04817.pdf) Classical Shadow Tomography with Locally Scrambled Quantum Dynamics 扈鸿业和尤亦庄关于演化动力学下Classical Shadow Tomography
4. [arxiv.2102.10132](https://arxiv.org/pdf/2102.10132.pdf) Hamiltonian-Driven Shadow Tomography of Quantum States

第3部分

1. Preskill的论文 [arXiv:2106.12627](https://arxiv.org/abs/2106.12627) Provably efficient machine learning for quantum many-body problems
2. 文小刚老师的书 《Quantum Information Meets Quantum Matter》[arXiv:1508.02595](https://arxiv.org/abs/1508.02595)

公众号文章：

- [解密神奇的量子黑盒](https://mp.weixin.qq.com/s/e1uiTp0NwvzT8i_lE1sxaQ) 扈鸿业