量子纠错码简介

**时间：**2022年01月02日

**摘要：** 开头从经典纠错编码的一个例子过度到量子纠错编码。分类讨论了 $X$-型错误和$Z$-型错误对应的编码方式，以及合起来的Shor 编码。第二部分讲量子纠错的理论，讨论什么是一个好的量子编码。第三部分讲量子纠错编码有两种常见的方式1CSS编码 2稳定子编码。CSS编码中举了一些例子，如Toric code；稳定子编码中Gottesman-Knill 理论讨论了量子计算和经典计算的能力关系。最后一部分讨论了什么是可容错的量子计算。

**主讲人:** 黄金龙，UCSD在读博士生 

**主要研究领域:** 量子信息和多体系统

**记录人：**黄清扬；庄嘉培



[TOC]



# 概览


1. 从经典编码到量子编码 
2. 量子编码理论 
3. Calderbank-Shor-Steane编码 (CSS)  
4. 稳定子编码
5. 容错量子计算 



# 从经典编码到量子编码 

## 经典重复码  

经典编码有Hamming码等纠错编码，这里为了好理解，只介绍重复码  

#### 错误

假如小华要传递一个比特的信息(0或1)给小强，但是传输过程信息可能发生错误

- 0变成1
- 1变成0

#### 编码

为了纠错，我们可以用重复码 (repetition code)的方式，例如，一个比特的信息 $B =\{0,1\}$，我们把它编码到三比特中 $C_{3}=\{000,111\}$，用更多储存的代价来实现纠错编码

- $0 \rightarrow 000$ 用000代表0
- $1 \rightarrow 111$ 用111代表1

#### 传输

**传输：**然后我们把3个位的信息分离，防止被一锅端。等到需要读取的时候把3个集中在一起。

#### 解码

**解码原则**：服从多者

- 如果只发生一个物理比特错误翻转，那就可以纠错回来正确信息。
- 如果发生太多错误，就没办法纠错回来，所以纠错成功是有一定的概率的。

纠错成功的概率

1. 其中一个物理比特发生错误的概率是 $p$ 
2. 比特中两个或多个被翻转的概率为

$$
p_{e}=3 p^{2}(1-p)+p^{3}
$$





## 量子纠错码的挑战

1. 量子不可克隆定理 (No cloning theorem)
2. 连续误差 
3. 读取计算结果需要测量，但是测量会破坏量子态 

#### 不可克隆定理

> 什么是克隆量子态

对于任意量子态 $|\phi\rangle$，存在幺正变换 $U$
$$
U(|\phi\rangle \otimes|0\rangle)=|\phi\rangle \otimes|\phi\rangle
$$
把输入的 $|0\rangle$ 克隆成目标量子态 $|\phi\rangle$



> 不可克隆定理：不存在上述的克隆机器(幺正变换 $U$)

 



## 三量子比特编码

### 错误类型

介绍一种量子错误的类型，比特翻转错误(Bit flip error)

> 补充
>
> 对比量子比特的相干错误(coherent error)都可以分解成
> $$
> U(\delta \theta, \delta \phi)|\psi\rangle=\alpha_{I} 1 |\psi\rangle+\alpha_{X} X|\psi\rangle+\alpha_{Z} Z|\psi\rangle+\alpha_{X Z} X Z|\psi\rangle
> $$
> 所以研究两种
>
> - $X$-型错误 
> - $Z$-型错误 
>
> 就可以处理相干错误

比特翻转错误(Bit flip error)
$$
a|0\rangle+b|1\rangle \rightarrow a|1\rangle+b|0\rangle)
$$

- 又叫$X$-型错误，因为可以用 $X$-门来表示比特翻转错误  $|\psi\rangle \rightarrow X|\psi\rangle$
- 设发生翻转的概率是 $p$

### 编码方式

$$
\begin{aligned}
|0\rangle & \rightarrow\left|0_{L}\right\rangle \equiv|000\rangle \\
|1\rangle & \rightarrow\left|1_{L}\right\rangle \equiv|111\rangle
\end{aligned}
$$

一个任意量子比特编码下 $a|0\rangle+b|1\rangle \rightarrow a|000\rangle+b|111\rangle$

编码用的量子线路

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102133558364.png" style="zoom:50%;" />

### 差错症状 Syndrome diagnosis 

收到信息之后，我们需要根据测量来判断信息是否发生错误（这里假设错误不超过一个量子比特）

对于比特翻转信道, 对应于四个投影算子, 可有四种差错症状(error syndrome):
$$
\begin{array}{ll}P_{0} \equiv|000\rangle\langle 000|+| 111\rangle\langle 111| & \text { 没有差错 } \\ P_{1} \equiv|100\rangle\langle 100|+| 011\rangle\langle 011| & \text { 第一量子比特上比特翻转 } \\ P_{2} \equiv|010\rangle\langle 010|+| 101\rangle\langle 101| & \text { 第二量子比特上比特翻转 } \\ P_{3} \equiv|001\rangle\langle 001|+| 110\rangle\langle 110| & \text { 第三量子比特上比特翻转 }\end{array}
$$
举例来说，比特翻转出现在第一个量子比特上，破坏后的状态为 $a|100\rangle+b|011\rangle$，投影算子测量之后 $\left\langle\psi\left|P_{1}\right| \psi\right\rangle=1$. 我们可以看到

1. 差错症状测量不会引起状态的任何改变（在差错症状测量之前和之后的状态都为 $a|100\rangle+b|011\rangle$）
2. 差错症状测量不包含所被保护状态的信息 (比如量子态中的. $a$ 和 $b$ ).

### 恢复

> 检测到错误，怎么恢复到正确的量子比特？

以相位错误(Phase flip error)为例
$$
a|0\rangle+b|1\rangle \rightarrow a|0\rangle-b|1\rangle)
$$
相位错误可以用$Z$-门来表示 $ |\psi\rangle \rightarrow Z|\psi\rangle$  

#### 编码

用状态 $\left|0_{L}\right\rangle$ 和 $\left|1_{L}\right\rangle$ 作为逻辑 0 状态和逻辑 1 状态来保护相位翻转错误的量子比特信息
$$
\begin{aligned}|0\rangle & \rightarrow\left|0_{L}\right\rangle \equiv|+++\rangle \\|1\rangle & \rightarrow\left|1_{L}\right\rangle \equiv|---\rangle \end{aligned}
$$
其中

-  $|+\rangle \equiv(|0\rangle+|1\rangle) / \sqrt{2},|-\rangle \equiv(|0\rangle-|1\rangle) / \sqrt{2}$ 是新基底

为了转换到新基底，在纠错过程的适当位置上应用 Hadamard 门，如图

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102133745332.png" style="zoom:67%;" />



##  Shor 编码

> 前面说了对于一种类型的错误怎么编码纠错，如果同时有$X$-型错误和$Z$-型错误，怎么保护？ 

把前面讨论的两个方案结合起来

编码
$$
\begin{aligned}
|0\rangle \rightarrow\left|0_{L}\right\rangle & \equiv \frac{(|000\rangle+|111\rangle)(|000\rangle+|111\rangle)(|000\rangle+|111\rangle)}{2 \sqrt{2}} \\
|1\rangle  \rightarrow\left|1_{L}\right\rangle &\equiv \frac{(|000\rangle-|111\rangle)(|000\rangle-|111\rangle)(|000\rangle-|111\rangle)}{2 \sqrt{2}} .
\end{aligned}
$$
编码对应的量子线路

1. 前半部分是相位翻转错误(Phase flip error)对应的编码方式
2. 后半部分是比特翻转错误(Bit flip error)对应的编码方式

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102133848565.png" style="zoom:50%;" />





# 量子纠错的理论

### 概览

1. 量子态 $|\phi\rangle$ 经过幺正变换，编码到一个更大希尔伯特空间的子空间
2. 编码后的信息经过有噪声(noise)的通道
3. 使用syndrome测量
4. 恢复到原来的量子态 $|\phi\rangle$ 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211225154043573.png" style="zoom:50%;" />

### 好的量子编码

什么是一个好的量子编码，我们要求
$$
( R \circ \varepsilon )(\rho) \propto \rho
$$
其中

-  $\varepsilon$ 描述噪声
-  $R$ 描述差错检测和恢复

方程中写为“ $\propto$ ”而不是“ $=$ ”

- 如果 $\varepsilon$ 为保迹量子运算,那么是“ $=$ ”
- 感兴趣于纠错的非保迹量子运算如测量, 对这种情形取 “ $\propto$ ”是合适的



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102134048896.png" style="zoom:50%;" />

量子编码中 Hilbert 空间的封装:

- (a) 坏码, 具有非正交的、变形的空间; 
- (b) 好码，具有正交的、保形的空间.

### 量子纠错条件

-  $C$ 为一个量子码, 
-  令 $P$ 为到 $C$ 的投影算子.
-  设 $\varepsilon$ 为具有运算元 $\left\{E_{i}\right\}$ 的量子运算. 

则纠正 $C$ 上 $\varepsilon$ 的纠错运算 $R$ 存在的充分必要条件为, 对某个复数 Hermite 矩阵 $\alpha$ 成立
$$
P E_{i}^{\dagger} E_{j} P=\alpha_{i j} P
$$






# CSS编码  



量子纠错编码有两种常见的方式

1. Calderbank-Shor-Steane编码 (CSS) 
2. 稳定子编码

先讲CSS编码

## 定义CSS编码

对于向量 $e \in F _{2}^{n}$, 定义 
$$
X^{e}=X^{e_{1}} \otimes X^{e_{2}} \cdots \otimes X^{e_{n}}
$$
其中

- $X$ 是泡利算符(Pauli operators)
- 类似的 $Z^{e}=\otimes_{i} Z^{e_{i}}$

泡利算符的矩阵形式
$$
X=\left(\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right), Z=\left(\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right)
$$

### 举例 $n=3$

- 那么 $e =[1,0,0]$

$$
X^{e}= X  \otimes I \otimes I
$$

### 定义CSS编码

定义在 $n$ 量子比特上的量子CSS编码，是一个子空间
$$
C \subseteq H =\left( C ^{2}\right)^{\otimes n}
$$
子空间 $C$ 是通过两个比特串 $S_{x}, S_{z} \subseteq F _{2}^{n}$ 定义的，两个比特串之间要相互垂直 $S_{x} \perp S_{z}$ :
$$
\left.\left\{|\psi\rangle \in\left( C ^{2}\right)^{\otimes n}\left|X^{x}\right| \psi\right\rangle=|\psi\rangle \forall x \in S_{x}, Z^{z}|\psi\rangle=|\psi\rangle \forall z \in S_{z}\right\}
$$

## 例子

### 例子 1:

就是前面讲过的
$$
\begin{array}{l} 
S =\left\langle Z_{1} Z_{2}, Z_{2} Z_{3}\right\rangle \\
V_{S}=\operatorname{span}\{|000\rangle,|111\rangle\} .
\end{array}
$$

### 例子 2: Shor code

也是前面讲过的Shor code

- 9个量子比特
- 8个约束
- 最后只剩2维子空间

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102134457618.png" style="zoom:50%;" />

### 例子 3: Toric code

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102134603180.png" style="zoom:67%;" />

在甜甜圈形状的空间中定义晶格

- 每条晶格线上方一个自旋
- 定义算符 $v$ 在格点上
- 定义算符 $p$ 在四边上

子空间的4个基底向量
$$
S =\left\langle-\prod_{i \in v} Z_{i},-\prod_{i \in p} X_{i}, \forall v, p\right\rangle
$$

$$
V_{S}=\operatorname{span}\left\{\left|\Psi_{1}\right\rangle,\left|\Psi_{2}\right\rangle,\left|\Psi_{3}\right\rangle,\left|\Psi_{4}\right\rangle\right\}
$$

其中

-  $\left|\Psi_{1}\right\rangle=\sum \mid$ closed loops $\rangle $ 是所有闭合线路的组合。
   - 闭合路线的定义，自旋为1就画线，自旋为0不画线。
-  $\left|\Psi_{2}\right\rangle,\left|\Psi_{3}\right\rangle,\left|\Psi_{4}\right\rangle$ 通过对 $\left|\Psi_{1}\right\rangle$ 作用一些弦算子



# 稳定子编码 stabilizer code

稳定子编码是CSS编码的推广。用单量子比特定义一个泡利群
$$
G_{1} \equiv\{\pm I, \pm i I, \pm X, \pm i X, \pm Y, \pm i Y, \pm Z, \pm i Z\}
$$
如果是 $n$ 个量子比特
$$
G_{n}=\left\{e^{i \phi} A_{1} \otimes \cdots \otimes A_{n} \mid A_{j} \in G_{1} \forall j \in\{1, \ldots, n\}, \phi \in\{0, \pi / 2, \pi, 3 \pi / 2\}\right\}
$$
一个 $[n, k]$ 稳定子编码表示： $n$ 个物理比特来编码 $k$ 个逻辑比特

稳定子 $S$ 是 $G_{n}$ 的阿贝尔子群

编码空间 $V_{S}$ 的展开方式：$S$ 中所有本征值是 $+1$ 的本征向量

## 例子: the five qubit code

5个物理比特，4个约束，所以定义出的子空间是2维的
$$
\begin{array}{l}
X Z Z X I \\
I X Z Z X \\
X I X Z Z \\
Z X I X Z
\end{array}
$$
这个编码很重要，因为可以纠错任意单量子比特的错误 

## Gottesman-Knill theorem

符合以下条件的量子计算，可以在经典计算机上有效地模拟.

1. 计算基中的状态制备
2. 只有Hadamard 门、相位门、受控非门、Pauli 门
3. Pauli 群中观测量的测量
4. 允许以这样测量的结果为条件的经典控制



# 容错量子计算 

Fault-tolerant quantum computation

## Big picture:

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102134911978.png" style="zoom:50%;" />

错误发生的地方

1. 制备量子态的时候
2. 门操作的时候
3. 传输的时候
4. 测量的时候

所以需要对所有过程都要编码

![](https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220102134858391.png)



> 什么是可容错的？

定义一个过程的容错性具有这样一个性质, 如果过程中只有一个元件失 效, 那么失效在过程的每个编码后量子比特输出块中最多只引起一个差错. 

- 例如图中7个量子比特的线路，其中一个比特发生错误
- 经过编码后门中的任何基本运算，只能一个比特发生错误，这种错误不能扩散



## Threshold 定理

1. 如果每个错误的概率低于一个值  $p<p_{\text {th }}$
2. 一个包含 $p(n)$ 门的量子线路

要让发生错误的概率最多为 $\epsilon$，需要的纠错操作的次数
$$
O(\operatorname{poly}(\log p(n) / \epsilon) p(n))
$$


# 问答

### Q1 温度

1. Toric code只在绝对零度下有效
2. 非零度温度下，并且是2维的情况，是否稳定子可以纠错任意错误的发生？没有

### Q2 平台

Toric code如果是用超导平台实现，很难定义在Toric形状上，也就是周期性边界条件(PBC)。如果是定义在平面上，可以对应到Surface code

### Q3 优势

对BQP(有限错误量子多项式时间bounded error quantum polynomial time)里面的问题，存在一个使用量子电脑的算法（量子算法）花费多项式时间运作，并且有很高的几率回答正确的答案。对任何状况，回答错误答案的几率小于三分之一。

# 参考文献

1.  [1] Nielsen, Michael A., and Isaac Chuang. "Quantum computation and quantum information." (2002): 558-559
    - **This slide mainly follows Chapter 10 of [1].**
2.  [2] Roffe, Joschka. "Quantum error correction: an introductory guide." Contemporary Physics $60.3$ (2019): 226-245.
3.  [3] Breuckmann, Nikolas P., and Jens Niklas Eberhardt. "LDPC Quantum Codes." arXiv preprint arXiv:2103.06309 (2021).