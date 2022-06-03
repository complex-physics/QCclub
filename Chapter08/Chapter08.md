量子模拟 Quantum' Simulation



**时间：**2022年02月13日

**摘要：**  本演讲先是介绍了量子模拟 Quantum' Simulation的基本概念，包括产生的动机。然后介绍实验上用什么物理系统来实现量子模拟，比如冷原子，超导量子比特，离子阱等等。最后介绍量子模拟的一些应用，比如在热化动力学，模拟拓扑物态，高温超导等等物理。

**主讲人:**  Hengyun (Harry) Zhou 本科MIT，博士哈佛

**主要研究领域:**  

**个人主页:** 

**记录人：** 庄嘉培



[TOC]



# 概览

## The Promise of Quantum Science \& Technology

最近这些年量子技术的发展，和百年前的量子革命不同的地方

1925年，薛定谔方程z

$$
H(t)|\psi(t)\rangle=i \hbar \frac{d}{d t}|\psi(t)\rangle
$$


> 现在有什么新的发展？

1. 量子计算(Quantum Computing)
   - Shor's algorithm 1994
   - First implementatians $\sim 2000 s$
2. 量子模拟(Quantum Simulation)
   - Feynman 1982
   - First implementations $\sim 2000 s$
3. 量子传感(Quantum Metrology)
   - First proposals $1980 s$ 
   - First implementations $\sim 2000 s$
4. 量子通讯(Quantum Communication) 
   - Bennett \& Brassard, 1984 
   - First networks $\sim 2010$ s

这些发展的一个内在逻辑

> 能够有效地去**控制**一些量子系统(Controllable quantum systems)，**探测**一个量子系统



### Feynman's Vision

具体到量子模拟方向，1982年费曼(Richard Feynman)提出最基本的想法

> "Nature isn't classical, dammit, and if you want to make a simulation of nature, you'd better make it quantum mechanical, and by golly it's a wonderful problem, because it doesn't look so easy." 
>
> —— Richard Feynman
>
> Simulating Physics with Computers http://www.cs.berkeley.edu/~christos/classics/Feynman.pdf", International Journal of Theoretical Physics, volume 21, 1982, p. 467-488, at p. 486

大自然本身并不是一个经典的系统，如果我们想去模拟大自然，那我们也许就应该用这个一些量子系统来进行模拟。

为什么说用经典计算模拟会有困难？理由之一

- 如果有1个量子比特: $a_{0}|0\rangle+a_{1}|1\rangle$
  - 需要两个两个数字描述
- 如果有2个量子比特: $a_{00}|00\rangle+a_{01}|01\rangle+a_{10}|10\rangle+a_{11}|11\rangle$
  - 需要4个两个数字描述
- 如果有N个量子比特
  - 需要 $2^{N}$ 个两个数字描述 
  - 指数级



> "Let the computer itself be built of quantum mechanical elements which obey quantum mechanical laws" 
>
> —— Richard Feynman



## 量子模拟(Quantum Simulation)

量子模拟(Quantum Simulation)的基本思路：

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430004850076.png" style="zoom:50%;" />

1. 量子系统的演化过程 $|\phi(0)\rangle \stackrel{U}{\longrightarrow}|\phi( t )\rangle$
2. 但是因为不好计算最后的结果是什么，我们可以制备另外一个平台，有另外一套演化。另外一个最终的测量。
3. 这些东西在某种程度上一一对应的关系，跟我们原来的系统是一个某种程度上的近似。

### 实验系统

模拟使用的真实实验系统，常见的有

1. 冷原子 Cold atoms
2. 离子阱 Trapped ions
3. 超导量子比特 SC qubits
4. 光子 Photonics
5. 量子点 Quantum dots
6. 金刚石色心 Color centers

> 这些系统需要满足什么条件呢？

- 初态准备 State preparation
- 实现幺正演化 Implement interesting unitary U
- 测量 Measurement

这些过程其实除了量子模拟，同时也是量子计算需要的过程。所以我们可以对比一下两者的关系

1. 量子模拟可以看作是量子计算的简化版。
   - 量子计算在容错等方面比量子模拟要求高很多。
   - 同时这个也意味着量子模拟可能是我们近期就能够做很多的工作



# 用什么系统去模拟

## 冷原子 Cold atoms

量子模拟做得最多的，可能是冷原子系统。

举例说明

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430010956252.png" style="zoom:50%;" />

量子气显微镜

- 不同的光晶格来限制这些原子
- 有一个高分辨率的显微镜，能够单个观测在系统里每一个晶格里有没有原子
  - 甚至一些实验可以探测，在某一个单独地方原子的原子态。

Quantum gas microscopes. *Gross and Bloch, Science 357, 995-1001 (2017)*

Quantum gas microscopes enable the high-resolution fluorescence detection of atoms in single sites of a two-dimensional layer of optical lattices. The lattice spacing is small (typically $0.5 \mu m$ ), such that the atoms can move through the lattice by tunneling with amplitude $t$. Additionally, they interact with each other with strength $U$ when multiple atoms meet at the same lattice site. Quantum gas microscopy can provide access to single snapshots of the locally resolved atomic density in strongly correlated many-body systems.

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430011555914.png" style="zoom:50%;" />

五六年前的比较新的一个技术

1. 作用：制备均匀初态
2. 通过光学的手段把原子束缚在光镊之中
3. 通过Spatial light modulator (SLM)，相当于是一个能够施加相位的阵列，通过光的干涉能够实现各种各样不同的的光斑。
4. 通过acousto-optical deflector (AOD) 快速重新排布原子

Deterministic atom array preparation. 

Left: Schematic of the optical setup to generate arbitrary two-dimensional trap arrays via the spatial light modulator (SLM). The position of the moving tweezer, which sorts the initially randomly loaded atoms into the target array, is computercontrolled (control system) using an acousto-optical deflector (2d-AOD). The charge-coupled device (CCD) camera allows for nondestructive position monitoring of the atoms. 

Right: Example of one realization of deterministic array loading. The initially randomly loaded sample (top) is sorted in about $100 ms$ to a uniformly filled two-dimensional array (bottom). The detected atomic fluorescence is encoded from dark to light in the color scale; each spatially distinct area of high fluorescence signal corresponds to a single atom. [Adapted, with permission, from (153)]



## 离子阱 Trapped ions

- 前面冷原子领域中，用光束缚的情况，它们实际上一般是中性原子。
- 在离子阱 Trapped ions 领域，把这个中性原子打掉一个电子，得到带一个正电荷的离子，这个离子我们就可以用电场去束缚它。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430113635106.png" style="zoom:50%;" />

通过一些激光，我们能够把离子之中的自旋自由度，和系统声子的一些自由度相耦合起来，就可以实现不同离子之间的量子门，哈密顿量演化的操作。

## 超导量子比特 SC qubits

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430115204826.png" style="zoom:50%;" />

-  可以通过一些 flux 来调相互作用。可以模拟一些比如说错扑量的系统。
-  超导量子比特的一个优势：不同比特之间的联系是通过微波波段的波导相联系。有比较高的自由去得到一些比较奇奇怪怪的连接状态图。

## 金刚石色心 Color centers

演讲者自己的研究方向

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430120102205.png" style="zoom:50%;" />

## 各方向的对比

TABLE I. Strengths and weaknesses of some of the proposed and demonstrated quantum simulators.

| Quantum simulator               | Strength                                       | Weakness                       |
| ------------------------------- | ---------------------------------------------- | ------------------------------ |
| Neutral atoms                   | Scaling                                        | Individual control and readout |
| Trapped ions                    | Individual control and readout                 | Scaling                        |
| Cavity arrays                   | Individual control and readout                 | Scaling                        |
| Electronic spins (quantum dots) | Individual control and readout; tunability     | Scaling                        |
| Superconducting circuits        | Individual control and readout; tunability     | Scaling(some recent progress)  |
| Photons (linear optics)         | Flexibility                                    | Scaling                        |
| Nuclear spins (NMR)             | Well-established; readily available technology | Scaling; no individual control |

上面的表格是10年前的综述。经过这10年发展，发生了一些改变

- Neutral atoms已经可以做到Individual control and readout
- Trapped ions的拓展从五六个达到三十多个

# 模拟什么

这个问题可以细分成两个问题

1. 模拟什么模型？
2. 想探究什么样的物理？

#### 模拟什么模型

- 凝聚态物理中的
  - Hubbard models 这个模型被认为是解释高温超导的重要模型
  - Spin models 自旋模型有很有趣的物理和复杂的计算
- 高能物理
  - 晶格规范理论 Lattice gauge theories

#### 探究什么样的物理

- 高温超导 High-Tc superconductivity
- 热化动力学 Thermalization dynamics
- 拓扑 Topology

## 例子1 热化动力学：局域化

问题：对于一个封闭的量子系统，如果一开始状态是纯态，那么演化到最后还是纯态。但是热平衡的话，系统的态是混态。所以一个封闭的量子系统里，热平衡这个概念到底是如何出现？

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430141814448.png" style="zoom:50%;" />

一些有趣的问题

1. 系统如何趋向于平衡？
2. 为什么趋向于平衡？
3. 什么系统不会趋向于热平衡？

这些问题是量子模拟的用武之地

### 局域化

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430142130279.png" style="zoom:50%;" />

单个粒子的局域化叫 Anderson localization
$$
H=t \sum_{\langle i j\rangle}\left(c_{i}^{\dagger} c_{j}+c_{j}^{\dagger} c_{i}\right)+\sum_{i} U_{i} c_{i}^{\dagger} c_{i}
$$
如果原子在这种光势阱里边，它很自然的就构造了这样的一个模型。

Many-body localization
$$
\begin{aligned}
\hat{H}=&-J \sum_{i, \sigma}\left(\hat{c}_{i, \sigma}^{\dagger} \hat{c}_{i+1, \sigma}+\text { h.c. }\right) \\
&+\Delta \sum_{i, \sigma} \cos (2 \pi \beta i+\phi) \hat{c}_{i, \sigma}^{\dagger} \hat{c}_{i, \sigma}+U \sum_{i} \hat{n}_{i, \uparrow} \hat{n}_{i, \downarrow}
\end{aligned}
$$

## 例子2 - 黑洞

黑洞Black holes被认为是最快能趋于热平衡的系统。  "fast scramblers"

- 我们可以设计出像这样快速热平衡的量子系统吗？
- 我们可以用这个系统去研究热化的动力学吗？

#### 离子阱模拟

- 离子阱方面的实验，构造一个幺正演化 $U$。
- 再构造一个共轭的幺正演化 $U^{*}$。
- 整个过程等效是 teleportation

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430203124616.png" style="zoom:50%;" />

这部分和第一次课程尤亦庄老师讲的一样，Alice的信息丢进黑洞，通过收集霍金辐射Hawking
radiation，$U^{*}$ 过程有可能把Alice的信息复原出来

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430203151779.png" style="zoom:50%;" />

## 例子3 高温超导

高温超导的相图 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430215110869.png" style="zoom:50%;" />

虽然结构很复杂，但是可以等效成二维ferimi Hubbard model

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430215226271.png" style="zoom:50%;" />

实验上：用量子器显微镜探索ferimi Hubbard model

- 测量自旋之间的关联函数
- 各向异性超导
- 观测空穴的动力学，这是传统凝聚态系统没办法观测到的

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220430215436420.png" style="zoom:50%;" />



## 例子4 拓扑

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220514225446678.png" style="zoom:50%;" />

1. 左边两个图是量子霍尔效应的实验示意图和结果示意图。
2. 右边的图是toric code模型，一个含有拓扑序的模型。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526143545588.png" style="zoom:50%;" />

用超导量子比特模拟拓扑物态系统





### 拓扑序

2021年的两个在拓扑序方面的研究

1. 哈佛组用里德堡原子模拟了 toric code形式的量子自旋液体  [DOI: 10.1126/science.abi8794](https://www.science.org/doi/10.1126/science.abi8794)
2. 谷歌的研究组用超导模拟了 toric code [DOI: 10.1126/science.abi8378](https://www.science.org/doi/10.1126/science.abi8378)

![image-20220514225831544](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220514225831544.png)



# 未来发展

类比电子计算机发展历程：

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526144448664.png" style="zoom:50%;" />

人类没有电子计算机之前，构造这种非常复杂的这个这个机器来干预测潮汐，

- 这种模拟计算机的一个缺点是，因为它是一个连续的变量，所以误差会累积

对于数字的计算机，能用纠错的方法，把噪音给取消掉。类似的，在量子计算中也进行纠错（Fault-Tolerant Quantum Computation）。接下来以Hamiltonian Simulation为例子说明一下

### Hamiltonian Simulation

Trotter formula方法：把哈密顿量拆解成多项
$$
H=A+B+C
$$

因为算符有对易问题，所以不能随便写成下面的形式，但是如果拆解成项数足够多，可以让误差比较小，那么演化可以写成下面的形式
$$
U=e^{-i(A+B+C) t}=\left(e^{-i A t / r} e^{-i B t / r} e^{-i C t / r}\right)^{r}
$$

把演化算符 $U$ 拆解成多个幺正算符的线性叠加(Linear combination of unitaries)
$$
U=\sum_{j} \beta_{j} V_{j}
$$

用这些方法进行量子化学的模拟，具体的一个例子比如“氮固化” （Elucidating reaction mechanisms on quantum computers [https://doi.org/10.1073/pnas.1619152114](https://doi.org/10.1073/pnas.1619152114) ）

![image-20220526145837310](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220526145837310.png)



### Quantum Phase Estimation

利用Quantum Phase Estimation计算系统的能谱。而基态能量是化学研究中非常受关注的一个东西。
$$
\begin{aligned}
\left|0^{m}\right\rangle|\psi\rangle & \stackrel{H^{\otimes m}}{\longrightarrow}\left(\frac{1}{\sqrt{M}} \sum_{k=0}^{M-1}|k\rangle\right) \otimes|\psi\rangle \\
\stackrel{C_{m}-U}{\longrightarrow} &\left(\frac{1}{\sqrt{M}} \sum_{k=0}^{M-1} \lambda^{k}|k\rangle\right) \otimes|\psi\rangle \\
&=\left(\frac{1}{\sqrt{M}} \sum_{k=0}^{M-1} w_{M}^{j k}|k\rangle\right) \otimes|\psi\rangle
\end{aligned}
$$

## 结论

本次演讲简单介绍了量子模拟的概念，和实验上的方案，最后是一些应用。

从长远来讲人们可能会做的一些更偏数字量子模拟的工作。






# 附录：相关资源



1. 费曼(Richard Feynman)最早提出的基本想法 

   - Simulating Physics with Computers http://www.cs.berkeley.edu/~christos/classics/Feynman.pdf", International Journal of Theoretical Physics, volume 21, 1982, p. 467-488, at p. 486
2. 冷原子 Cold atoms 主要参考 Quantum simulations with ultracold atoms in optical lattices
   - [DOI: 10.1126/science.aal3837](https://doi.org/10.1126/science.aal3837)
3. 离子阱 Trapped ions 主要参考：Programmable Quantum Simulations of Spin Systems with Trapped Ions
   - Rev. Mod. Phys. **93**, 025001(2021) 
   - [arxiv 链接](https://arxiv.org/abs/1912.07845) 
4. 量子模拟在拓扑序方面的应用
   - 哈佛组用里德堡原子模拟了 toric code形式的量子自旋液体  [DOI: 10.1126/science.abi8794](https://www.science.org/doi/10.1126/science.abi8794)
   - 谷歌的研究组用超导模拟了 toric code [DOI: 10.1126/science.abi8378](https://www.science.org/doi/10.1126/science.abi8378)
5. 量子模拟在量子化学的应用，具体的一个例子“氮固化” （Elucidating reaction mechanisms on quantum computers [https://doi.org/10.1073/pnas.1619152114](https://doi.org/10.1073/pnas.1619152114) ）





