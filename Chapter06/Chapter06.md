时间晶体



**时间：**2022年02月13日

**摘要：** 介绍时间上有周期性结构的系统——时间晶体。本文着重分类介绍， 根据量子和经典分类，根据离散和连续分类。每一类简要介绍并给出一些参考文献。

**主讲人:**  郭铁城

**主要研究领域:**  

**个人主页:** 

**记录人：**黄清扬；庄嘉培



[TOC]





1. Introduction
   - Concept
   - Classification
2. Continuous time crystal
3. Discrete time crystal
4. Discussion



# 概览



> 类比于空间晶体，有周期性的空间结构，那么时间上如果有类似的周期性结构呢？

1. 时间晶体的概念是Frank Wilczek在2012年提出

   - F. Wilczek, Phys. Rev. Lett. 109,160401 (2012).
   - A. Shapere and F. Wilczek, Phys. Rev. Lett.109,160402(2012).

2. Frank Wilczek关于时间晶体的概念遭到很多学者的挑战，其中Bruno在2013年提出根据no-go theorem，指出量子时间晶体是不可行的

   - P. Bruno, Phys. Rev. Lett. 111,070402 (2013).
   - P. Nozières, EPL (Europhysics Letters) 103, 57008 (2013).

3. 但是时间晶体这个概念很吸引人，2015年，Watanabe 和 Oshikawa (简称WO)提出了他们对量子时间晶体的定义。

   而且提出了他们定义的no-go theorem：如果没有长程相互作用，Watanabe 和 Oshikawa 定义的量子时间晶体也是不可行的。

   - H. Watanabe and M. Oshikawa, Phys. Rev. Lett. $114,251603(2015)$

4. 需要指出的是，前面两种对时间晶体的定义，都是连续时间平移对称性的破缺情况下。但是人们还是很感兴趣，离散时间平移对称性的破缺情况下的时间晶体。

   - (连续 $\rightarrow$ 离散)





### 时间晶体的分类

原始概念，时间维度上有没有一个类似空间结构的这种周期性结构。

根据量子和经典分类

1. Classical time crystal
2. quantum time crystal

根据离散和连续分类

1. Continuous time crystal (CTC); 
2. discrete time crystal (DTC)



本次分享主要包含

|            | quantum      | Classical |
| ---------- | ------------ | --------- |
| Continuous | $\checkmark$ |           |
| discrete   | $\checkmark$ |           |



### 量子动力学

两种常见的量子动力学，是时间晶体研究的**出发点**

1. 薛定谔方程
   $$
   i \frac{d}{d t}|\psi\rangle=H|\psi\rangle
   $$

2. Lindblad 主方程（与外界有耦合，考虑耗散）

$$
\begin{aligned}
\dot{\rho}(t)=&L \rho
\\=&-i[H, \rho(t)]+\sum_{\mu}\left(2 L_{\mu} \rho L_{\mu}^{\dagger}-L_{\mu}^{\dagger} L_{\mu} \rho-\rho L_{\mu}^{\dagger} L_{\mu}\right)
\end{aligned}
$$

其中

-  Lindblad 主方程描述系统和外界环境耦合，导致系统发生耗散
-  $L_{\mu}$ 是 jump 算子
-  描述密度矩阵的演化
-  方程的两个部分
   - $-i[H, \rho(t)]$ 这部分和薛定谔方程一样的
   - 第二项描述系统和外界环境耦合



## 离散时间晶体 (DTC)的定义

一个系统的哈密顿量如果是时间周期的
$$
\hat{H}(t+T)=\hat{H}(t)
$$

- 也就是说过一段时间 $T$后，哈密顿量会变回原来的样子。
- 这种系统又叫Floquet系统

对于物理观察量 $\hat{O}$，在某个时刻系统对 $\hat{O}$ 的 $f(t)=\langle\psi(t)|\hat{O}| \psi(t)\rangle, \hat{O}$ 如果是周期性函数
$$
f(t+n T)=f(t)
$$
而且其中 $n \neq 1$ ，那么我们可以说，系统态 $|\psi\rangle$ 是周期为 $n T$ 的离散时间晶体(DTC) discrete time crystal

近年的发展主要是离散时间晶体(DTC)，而且一般有一些要求

1. 周期要有足够长的时间
2. Robustness，对抗噪声



## 离散和连续的对比

- Continuous time crystal (CTC); 系统的哈密顿量**不含时**，所以说它的时间的周期就是任意的，也就是它有一个连续的时间周期。
- Discrete time crystal (DTC)：系统的哈密顿量**含时**，过了一个大 T 时间之后，系统的哈密顿量就会演化回去。
  - 观测量也有周期，但是周期和系统的哈密顿量的周期不一样

| TC type     | Governing mechanism | State            |
| ----------- | ------------------- | ---------------- |
| Wilczek     | Field eq.           | Ground state     |
| WO          | Schrödinger eq.     | Ground state     |
| Dissipation | Lindblad eq.        | Stationary state |

$$
\begin{array}{l}
\text { Table: Different types of quantum continuous time crystal }
\end{array}
$$

| TC type         | Governing eq.   | Thermalization           |
| --------------- | --------------- | ------------------------ |
| MBL DTC         | Schrodinger eq. | MBL                      |
| Prethermal DTC  | Schrodinger eq. | Prethermalization        |
| Clean DTC       | Schrodinger eq. | Integrability, classical |
| Scar DTC        | Schrodinger eq. | Many-body scar           |
| Dissipative DTC | Lindblad eq.    |                          |



$$
\begin{array}{l}
\text { Table: Different types of quantum discrete time crystal }
\end{array}
$$

# 连续时间晶体 (CTC)

CTC连续的有三种类别

| TC type     | Governing mechanism | State            |
| ----------- | ------------------- | ---------------- |
| Wilczek     | Field eq.           | Ground state     |
| WO          | Schrodinger eq.     | Ground state     |
| Dissipation | Lindblad eq.        | Stationary state |

$$
\begin{array}{l}
\text { Table: Different types of quantum continuous time crystal }
\end{array}
$$

### 1- Wilczek type:

- 考虑一个环里面充满 BEC（玻色–爱因斯坦凝聚） 的一团波色气体。
  - 基态处于一种孤子的状态。
  - 孤子在环里面转动，过一个时间段之后他就回来原来的点，再过一段这个小球他又回来
- Wilczek根据这个系统提出时间晶体
  - 孤子密度流周期性转动确实是这个整个系统BEC的一个基态。（后来的文章否认了这个）
- Phys. Rev. Lett. 123, 250402 (2019) 在Wilczek基础上考虑一些非线性，相互作用规范场。认为存在时间晶体结构。
  - Phys. Rev. Lett. 124, 178901 (2020).又有文章提出争论，所以现在**还没有一个明确的结论**。



1. F. Wilczek, Phys. Rev. Lett. $109,160401(2012)$.
2. P. Öhberg and E. M. Wright, Phys. Rev. Lett. 123, 250402 (2019). "Quantum time crystals and interacting gauge theories in atomic Bose-Einstein condensates."
3. A. Syrwid, A. Kosior, and K. Sacha, Phys. Rev. Lett. 124, 178901 (2020). Comment on "Quantum Time Crystals and Interacting Gauge Theories in Atomic Bose-Einstein Condensates"



### 2- WO type:

- Phys. Rev. Lett. 114, 251603 (2015) 关联函数，对时间 T 如果说有一个周期性的结构
  - 那么这个系统的基态就叫做一个时间晶体的物质态
  - 严格的限制：相互作用形式不是太长的相互作用的形式，那么不会有非反的空间周期性结构。
- Phys. Rev. Lett. 123,210602(2019). 人为构造长程相互作用的模型



1. H. Watanabe and M. Oshikawa, Phys. Rev. Lett. 114, 251603 (2015).
2. V. K. Kozin and O. Kyriienko, Phys. Rev. Lett. 123,210602(2019).
3. T.-C. Guo and L. You, arxiv: 2008.10188

### 3-Dissipation:

- 考虑的不是一个基态，它考虑是一个稳态 

- 考虑了和外界有个耦合

  - 一般在这种有耗散的 Lindblad  主方程的演化下，会趋于一个稳态，就不会随时间来变化。
  - 19 年Jaksch这两篇文章里面，他们找到这种形式的哈密顿量，使得观测量是周期性震荡的结构

  



1. B. Buča, J. Tindall, and D. Jaksch, Nat. Commun. 10, $1730(2019)$.
2. B. Buča and D. Jaksch, Phys. Rev. Lett. 123, 260401 (2019).

## 主要介绍WO type

哈密顿量的一个基态，用来计算两点关联函数(The two-time correlation function):
$$
\lim _{N \rightarrow \infty}\langle\hat{\phi}(t) \hat{\phi}(0)\rangle \equiv \lim _{N \rightarrow \infty}\langle\hat{\Phi}(t) \hat{\Phi}(0)\rangle / V^{2}=f(t)
$$
其中

-  $\hat{\phi} \equiv \hat{\Phi} / V$ 是局域序参数(local or coarse-grained order parameter).
-  $\hat{\Phi}(t) \equiv \int_{V} d^{d} x \hat{\phi}(\vec{x}, t)$ 是序参数的积分

推广到不除以系统体积 $V^{2}$ 的情况 
$$
\lim _{N \rightarrow \infty}\langle\hat{\Phi}(t) \hat{\Phi}(0)\rangle=F(t)
$$


### Twisted Vector

*Tiecheng Guo and Li You, arxiv:2008.10188*

为了看清两点关联函数，我们先做一些推导
$$
\begin{aligned}
f(t) &=\lim _{V \rightarrow \infty}\left\langle\psi_{0}\left|e^{i \hat{H} t} \hat{\phi}(0) e^{-i \hat{H} t} \hat{\phi}(0)\right| \psi_{0}\right\rangle \\
&=\lim _{V \rightarrow \infty} e^{i \epsilon_{0} t}\left\langle v\left|e^{-i \hat{H} t}\right| v\right\rangle \\
&=\lim _{V \rightarrow \infty} \sum_{j=0}^{\infty} c_{j} e^{-i\left(\epsilon_{j}-\epsilon_{0}\right) t},
\end{aligned}
$$
其中

-  $c_{j} \equiv\left|a_{j}\right|^{2}$ 表示扭曲矢量的一个权重(weight of the ground state twisted vector)
-  $c_{0}$ the corresponding ground state weight, 
-  and $c_{j}($ with $j>0)$ the excited state weight.



什么是扭曲矢量 twisted vector？

- 局域序参数 $\hat{\phi}(0)$ 作用到基态 $|\psi(0)\rangle$ 上 
- 作用的结果会让波函数在整个希尔波的空间里面有一个转动

$$
|v\rangle \equiv \hat{\phi}(0)|\psi(0)\rangle=\sum_{i=0}^{\infty} a_{i}\left|\psi_{i}\right\rangle
$$

然后一步是扭曲矢量在能量本征态上的展开 $|v\rangle =\sum_{i=0}^{\infty} a_{i}\left|\psi_{i}\right\rangle$。其中 $c_{j} \equiv\left|a_{j}\right|^{2}$

#### Physical meaning

所以回到前面公式
$$
f(t)=\lim _{V \rightarrow \infty} \sum_{j=0}^{\infty} c_{j} e^{-i\left(\epsilon_{j}-\epsilon_{0}\right) t}
$$
可以看出

1. $f(t)$ 是一系列傅里叶分量的一个叠加。 
2. $\left(\epsilon_{j}-\epsilon_{0}\right)$ 是不同能级和基态的差距，相当于傅里叶分量的频率。
3. 所以如果想要去找时间晶体的状态， $f(t)$ 是一个周期性的结构，我们就需要对 $\left(\epsilon_{j}-\epsilon_{0}\right)$ 进行约束。
4. 换个角度，如果有一个时间晶体，它关联函数的周期以及它的振幅的物理意义是什么？
   - 物理意义与能级差，扭曲矢量有关系
5. 知道物理意义帮助大家更寻找时间晶体
   - 从数值计算的情况下，它可以直接省去你演化了很长时间的计算代价。



# 离散时间晶体 (DTC)

#### 定义

对于一个具有哈密顿 $\hat{H}(t+T)=\hat{H}(t)$,的量子多体（Floquet）系统来说，我们说该系统具有周期为$T$的时间平移对称性，如果符合以下条件
$$
f(t+n T)=f(t), n \neq 1,
$$
其中

- $f(t)=\langle\psi(t)|\hat{O}| \psi(t)\rangle, \hat{O}$ 是物理观测量
- 那么我们说系统中 $|\psi\rangle$ 是周期 $n T$ 的离散时间晶体 DTC  

## Thermalization 热化

$$
\begin{array}{l}
\begin{array}{lll}
 \text { TC type } & \text { Governing eq. } & \times \text { Thermalization } \\
 \text { MBL DTC } & \text { Schrödinger eq. } & \text { MBL } \\
\text { Prethermal DTC } & \text { Schrödinger eq. } & \text { Prethermalization } \\
\text { Clean DTC } & \text { Schrödinger eq. } & \text { Integrability, classical } \\
\text { Scar DTC } & \text { Schrödinger eq. } & \text { Many-body scar } \\
\text { Dissipative DTC } & \text { Lindblad eq. } & \\
\end{array}\\
\text { Table: Different types of quantum discrete time crystal }
\end{array}
$$

本征态热化假设 Eigenstate Thermalization Hypothesis ( ETH )

- 量子态在一个哈密顿量下进行演化，那么最后这个态都会趋于一个热化的态。
- 热化的态是指，在长时间情况下，末态不含初态的任何信息。

大家都会比较感兴趣违反 ETH 假设的情形

1. 可积系统 (Integrability)
2. 多体局域化(many body localization, *MBL*)
3. 冷原子领域中的Many-body scar
4. 前面那些是静态哈密顿量，这里要找Floquet系统中违反 ETH 的情形

### 一些参考文献

#### MBL

1. C. W. von Keyserlingk, V. Khemani, and S. L. Sondhi, Phys. Rev. B 94, 085112 (2016)
2. N. Y. Yao, A. C. Potter, I.-D. Potirniche, and A. Vish- wanath, Phys. Rev. Lett. 118, 030401 (2017).
   d
3. J. Zhang, P. W. Hess, A. Kyprianidis, P. Becker, A. Lee, J. Smith, G. Pagano, I.-D. Potirniche, A. C. Potter, A. Vishwanath, N. Y. Yao, and C. Monroe, Nature (London) 543,217 (2017)
4. S. Choi, J. Choi, R. Landig, G. Kucsko, H. Zhou, J. Isoya, F. Jelezko, S. Onoda, H. Sumiya, V. Khemani, C. von Keyserlingk, N. Y. Yao, E. Demler, and M. D. Lukin, Nature (London) 543, 221 (2017).
5. Mi, X., Ippoliti, M., Quintana, C. et al. Time-crystalline eigenstate order on a quantum processor. Nature $601,531-536$ $(2022)$

#### pre-thermal

1. T.-S. Zeng and D. N. Sheng. Physical Review B $96.9$ (2017): 094202 .
2. Kyprianidis, Antonis, et al. "Observation of a prethermal discrete time crystal." Science $372.6547$ (2021): 1192-1196.

#### clean

1. B. Huang, Y.-H. Wu, and W. V. Liu, Phys. Rev. Lett. 120, 110603 (2018).
2. C.-h. Fan, D. Rossini, H.-X. Zhang, J.-H. Wu, M. Artoni, and G. C. La Rocca, Phys. Rev. A $101,013417(2020)$.
3. F. Machado, D. V. Else, G. D. Kahanamoku-Meyer, C. Nayak, and N. Y. Yao, Phys. Rev. X $10,011043(2020)$.
4. A. Pizzi, J. Knolle, and A. Nunnenkamp, Higher-order and fractional discrete time crystals in clean long-range interacting systems, Nature communications 12,1 (2021)

#### open system

1. Z. Gong, R. Hamazaki, and M. Ueda, Phys. Rev. Lett. 120,040404 (2018)
2. F. M. Gambetta, F. Carollo, M. Marcuzzi, J. P. Garrahan, and I. Lesanovsky, Phys. Rev. Lett. 122, 015701 (2019).
3. A. Riera-Campeny, M. Moreno-Cardoner, and A. Sanpera, Quantum 4, 270 (2020).
4. A. Lazarides, S. Roy, F. Piazza, and R. Moessner, Phys. Rev. Research 2, 022002 (2020).
5. J. G. Cosme, J. Skulte, and L. Mathey, Phys. Rev. A 100,053615 (2019).



### Discussion on MBL time crystal

2021年的讨论 ”MBL 时间晶体是不是一个真正的是一个时间晶体？”

- Khemani, Vedika, Roderich Moessner, and S. L. Sondhi. "A comment on" Discrete time crystals: rigidity, criticality, and realizations"." arXiv preprint arXiv:2109.00551 (2021).
- Yao, Norman Y., et al. "Reply to Comment on" Discrete Time Crystals: Rigidity Criticality and Realizations"." arXiv preprint arXiv:2109.07485 (2021).



## 例子Spin-mixing Dynamics in Spinor BEC

参考 A. Pizzi, J. Knolle, and A. Nunnenkamp, Higher-order and fractional discrete time crystals in clean long-range interacting systems, Nature communications 12,1 (2021)


自旋是1的 Bose-Einstein condensate (BEC)在单模近似下(SMA假设每个原子它的波函数都是一样的) 可以用以下哈密顿量描述
$$
\begin{aligned}
\hat{H}=& \frac{c_{2}}{2 N}\left[\left(2 \hat{N}_{0}-1\right)\left(\hat{N}_{1}+\hat{N}_{-1}\right)+2\left(\hat{a}_{1}^{\dagger} \hat{a}_{-1}^{\dagger} \hat{a}_{0} \hat{a}_{0}+\text { h.c. }\right)\right] \\
&-p\left(\hat{N}_{1}-\hat{N}_{-1}\right)+q\left(\hat{N}_{1}+\hat{N}_{-1}\right)
\end{aligned}
$$
其中

-  $\hat{a}_{m_{F}}\left(m_{F}=0, \pm 1\right)\left(\hat{a}_{m_{F}}^{\dagger}\right)$ 是产生湮灭算符
-  基态波函数 $\left|F=1, m_{F}\right\rangle$ 
-  数量算符 $\hat{N}_{m_{F}}=\hat{a}_{m_{F}}^{\dagger} \hat{a}_{m_{F}}$. 总数 $\hat{N}=\hat{N}_{1}+\hat{N}_{0}+\hat{N}_{-1}$ 守恒
-  控制参数只控制 $q$ ，并且$q$ 是含时间的 

### Mean-field Dynamics

直接计算这个哈密顿量的演化是非常耗时间的。

所以可以用平均场动力学(Mean-field Dynamics)计算(Physical Review A, 2005, 72(1): 013602)
$$
\begin{aligned}
\dot{\rho}_{0} &=\frac{2 c}{\hbar} \rho_{0} \sqrt{\left(1-\rho_{0}\right)^{2}-m^{2}} \sin \theta \\
\dot{\theta} &=-\frac{2 q}{\hbar}+\frac{2 c}{\hbar}\left[\left(1-2 \rho_{0}\right)+\frac{\left(1-\rho_{0}\right)\left(1-2 \rho_{0}\right)-m^{2}}{\sqrt{\left(1-\rho_{0}\right)^{2}-m^{2}}} \cos \theta\right]
\end{aligned}
$$
其中

-  $\rho_{i}(i=+1,0,-1)$ is the atomic fractional population for spin state $|F=1, i\rangle,$
-  $ \theta=\theta_{+}{ }_{1}+\theta_{-1}-2 \theta_{0}$ is the spinor phase,
-  $m=\rho_{+1}-\rho_{-1}$ is the BEC's magnetization.


Floquet驱动
$$
q=\eta\left(1+\sin \left(\frac{2 \pi}{T} t\right)\right)
$$
初始态
$$
\begin{aligned}
\rho_{0} &=\rho_{0}\left(q_{\text {init }}\right) \\
\theta &=0
\end{aligned}
$$
其中 
$$
\rho_{0}\left(q_{\text {init }}\right)=\left\{\begin{array}{ll}
0, & q_{\text {init }}<-2, \\
\frac{1}{2}+\frac{1}{4} q_{\text {init }}, & -2 \leq q_{\text {init }} \leq 2, \\
1, & q_{\text {init }}>2,
\end{array}\right.
$$
$q_{\text {init }}=0, T=1$

计算得到的结果 Higher and franctional-order discrete time crystal.

- 傅里叶变换后得到频谱
- 图中出现的平台 $n$ 如果是整数就是整数时间晶体，如果 $n$ 是分数就是分数时间晶体

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220407001508574.png" style="zoom:80%;" />

图中的平台中，取$n=3$ 来画出以下图片

- 左图看出大概是一个周期性的演化。
- 右图可以看到有个主峰
  - 主峰的高低和系统的尺度 $N$ 的大小有关，也就是有限尺度会影响。
  - 旁边还有一个小的尖峰，这文章里面就把它叫做一个 glassy 的行为，就是它会有一点点的破坏。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220407002027388.png" style="zoom:80%;" />

# Conclusion and outlook

介绍了量子时间晶体(quantum time crystal)的概念 

1. 主要是WO类型的连续时间晶体
2. 例子：旋律BEC中给出了整数和分数时间晶体 

展望

1. Floquet系统的热化机制
2. 离散时间晶体有什么应用？
3. 非平衡态在整个希尔伯特空间中的演化

# 附录：相关资源

本次演讲中，参考文献结合在演讲中，所以不需要单独列出。



