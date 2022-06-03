量子线路与量子过程的经典模拟

**时间：**2021年12月19日

**摘要：** 第一部分介绍什么是经典计算和可逆计算。第二部分是结合计算库Yao来介绍量子计算。第三部分是介绍基于张量网络的量子线路模拟。在各个部分中，都介绍了基础计算门和通用门的概念。量子计算部分介绍的Deutsch-Jozsa算法突出量子计算的优势。

**主讲人:** 刘金国，哈佛大学博士后，17年于南京大学获得博士学位

**主要研究领域:** 研究方向为张量网络、自动微分与量子模拟。

**个人主页:** https://giggleliu.github.io/

邮箱: jingguoliu@g.harvard.edu

**记录人：**黄清扬；庄嘉培



[TOC]



# 概览

在一般的课本中也许会先告诉经典计算的基本门，然后过渡到量子门。本次讲座中刘老师在中间多介绍了一个可逆计算。可逆计算在本次讲座中用到的矩阵和向量表示，其实和一般量子计算的矩阵和向量表示几乎一样。或者说量子计算包含可逆计算，并有所推广。

1. 经典计算
2. 可逆计算
3. 量子计算



## 背景知识

要理解这次课程，最好先了解下面一些量子力学的背景知识

- $|\psi\rangle$ 表示一个量子态
- $H$ 是哈密顿量，它决定了量子态是怎么演化的 $|\psi(t)\rangle=e^{-i H t}|\psi(0)\rangle$
- $O$ 是一个观测量，用一个厄密算符表示。对这个观测量进行测量，得到的期望值表示为 $\langle O \rangle=\langle\psi| O | \psi\rangle$
- $X, Y,$  $Z$  是泡利算符 

$$
X=\left[\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right], Y=\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right],Z=\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]
$$

如果对这些知识想要深入了解，可以看下面两本书

1. J.J. Sakurai."Modern Quantum Mechanics." 是讲量子力学的一本很好的教材，特别是前三章。
2. Nielsen, Michael A., and Isaac Chuang. "Quantum computation and quantum information." (2002): 558-559. 是量子计算的经典书籍。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211424655.png" style="zoom:50%;" />







# 经典计算

经典计算中，基础组成单元——逻辑门

- 非门（NOT）
- 与门（ AND）
- 或门（ OR）
- 异或门（XOR）

逻辑门的真值表

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211504637.png" style="zoom:50%;" />

这是逻辑门是基础单元，可以用来构造各种计算。比如加法器

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211526463.png" style="zoom:50%;" />

全加器的真值表

FULL_ADDER $(\operatorname{cin}, a, b) \rightarrow$ cout, $c$
$$
\begin{array}{l}
000 \rightarrow 00 \\
001 \rightarrow 01 \\
010 \rightarrow 01 \\
011 \rightarrow 10 \\
100 \rightarrow 01 \\
101 \rightarrow 10 \\
110 \rightarrow 10 \\
111 \rightarrow 11
\end{array}
$$

解读：

- 左边3位表示输入，三个是独立的，没有进位概念。
- 右边是有进位的概念，比如输入有两个1，输出就会进位变成10。这里的进位是二进制的。



## 通用门(Univeral gate)

本次讲座会经常出现通用门(Univeral gate)的概念，如果有个门集合是通用门集合，那么任何逻辑表示都可以用这个通用门集合的门进行组合来表示。

> 个人理解笔记：如果有通用门，就像你建房子，你只要批量建几个砖头，其他任何形状都用这些砖头搭建起来。相反，如果任何逻辑表示，你都要去建立一个对应的门，这会非常麻烦，因为有些门可能在物理上很难实现，这时候用通用门等效表示，在工程上会得到极大的便利。

一些常见的通用门

- $\{N A N D\}$
- $\{N O R\}$
- \{NOT, AND\}
- $\{N O T, O R\}$

### 例子

与非门的真值表

NAND =
$$
\begin{array}{l}
00 \rightarrow 1 \\
01 \rightarrow 1 \\
10 \rightarrow 1 \\
11 \rightarrow 0
\end{array}
$$


$\operatorname{NOT}(x)=\operatorname{NAND}(x, x)$
$\operatorname{AND}(x, y)=\operatorname{NOT}(\operatorname{NAND}(x, y))$
OR $(x, y)=\operatorname{NAND}($ NOT $(x)$, NOT $(y))$



# 可逆计算

可逆门(Reversible Gates)的要求

1. 输入的数量要等于输出的数量 
2. 可逆门的真值表是置换(permutation)

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211743830.png" style="zoom:67%;" />

**可逆计算的计算能力，和不可能计算的计算能力其实是等价的**



## 基础可逆门

接下来我们介绍几个重要的可逆门

1. NOT gate $-> X$ gate
2. Controlled not gate
3. AND gate $->$ Toffoli gate
4. NAND gate
5. Or gate



### NOT gate $-> X$ gate

在可逆计算中，与经典计算的非门有个对应，是 $ X$ 门（在量子计算中也是用 $ X$ 门）

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211816955.png" style="zoom:50%;" />
$$
\begin{array}{l}
0 \rightarrow 1 \\
1 \rightarrow 0
\end{array}
$$

在可逆计算中，表示真值表的方式和经典的不一样。对于一个0态，用独热码(one hot)向量表示
$$
|0\rangle=\left[\begin{array}{l}
1 \\
0
\end{array}\right]
$$
类似的，对于态1的独热码
$$
|1\rangle=\left[\begin{array}{l}
0 \\
1
\end{array}\right]
$$
所以经典计算的非门在这里，可以用一个置换矩阵（ $ X$ 门）来作用到输入态上
$$
X=\left[\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right]
$$

$$
|\psi\rangle_{\text {out }}=X|\psi\rangle_{\text {in }}
$$

> 补充笔记
> $$
> X|0\rangle=\left[\begin{array}{ll}
> 0 & 1 \\
> 1 & 0
> \end{array}\right]\left[\begin{array}{l}
> 1 \\
> 0
> \end{array}\right]=\left[\begin{array}{l}
> 0 \\
> 1
> \end{array}\right]=|1\rangle
> $$
> 前后翻转了 $X|0\rangle=|1\rangle$



### 控制非门

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219211947504.png" style="zoom:33%;" />

控制非门（Controlled not gate, or CNOT gate），在非门的基础上加一个控制位

- 当控制门是 0 的时候，非门不起作用
  - $00 \rightarrow 00$
  - $01 \rightarrow 01$

- 当控制门是 1 的时候，非门起作用
  - $10 \rightarrow 11$
  - $11 \rightarrow 10$

控制非门用矩阵表示

$$
C N O T=\left[\begin{array}{llll}
1 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 \\
0 & 1 & 0 & 0
\end{array}\right]
$$
输入态用独热码(one hot)向量表示
$$
|00\rangle=\left[\begin{array}{l}
1 \\
0 \\
0 \\
0
\end{array}\right]
$$

$$
\begin{array}{l}
|01\rangle=\left[\begin{array}{l}
0 \\
1 \\
0 \\
0
\end{array}\right] \\
|10\rangle=\left[\begin{array}{l}
0 \\
0 \\
1 \\
0
\end{array}\right] \\
|11\rangle=\left[\begin{array}{l}
0 \\
0 \\
0 \\
1
\end{array}\right]
\end{array}
$$



### AND gate $->$ Toffoli gate

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212047213.png" style="zoom:33%;" />

Toffoli门，有三路输入和三路输出。如果前两位置都是1，它将倒置第三位，否则所有位保持不变。

所以Toffoli门也叫controlled-controlled-not gate双控制非门
$$
\begin{array}{l}
000 \rightarrow 000 \\
001 \rightarrow 001 \\
010 \rightarrow 010 \\
011 \rightarrow 011 \\
100 \rightarrow 100 \\
101 \rightarrow 101 \\
110 \rightarrow 111 \\
111 \rightarrow 110
\end{array}
$$

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212144010.png" style="zoom:50%;" />

Toffoli门的矩阵表示

- 只有最后两位是置换的

$$
\text { Toffoli }=\left[\begin{array}{cccccccc}
1 & 0 & 0 & 0 & 0 & 0 & 0 & 0 \\
0 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 1 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 1 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0 & 0 & 0 & 1 & 0
\end{array}\right]
$$

### NAND gate

与非门的线路表示

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212221919.png" style="zoom:50%;" />

### Or gate

或门

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211225010635346.png" style="zoom:50%;" />





### Reversible Full Adder

有了前面的基础门的介绍，这里可以构造一个可逆的全加法器

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212317690.png" style="zoom: 50%;" />





### A 4 bit binary adder

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212409137.png" style="zoom:80%;" />

### Adder with uncomputing

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212502025.png" style="zoom:80%;" />

This is compute-copy-uncompute, it can bring polynomial overhead in time/space.

## 通用可逆门

和前面经典计算中的类似，在可逆计算中，我们也能找到通用的可逆门

- \{Toffoli\}
- \{Fredkin\}

举个例子，用Toffoli制备 CNOT, NOT

#### CNOT

1. Toffoli门，有三路输入和三路输出。
2. 把第一位设为1
3. Toffoli门如果前两位置都是1，它将倒置第三位，否则所有位保持不变。所以
   - 第二位 a=1，则倒置第三位
   - 第二位 a=0，则保持不变
4. 所以第二位的作用相当于控制非门中的控制比特
5. 所以可以用Toffoli制备 CNOT

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212547573.png" style="zoom: 33%;" />

#### NOT 

1. Toffoli门，有三路输入和三路输出。
2. 把前面两位设为1
3. Toffoli门如果前两位置都是1，它将倒置第三位
4. 所以第三位会被倒置，也就是非门
5. 所以可以用Toffoli制备 NOT

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211219212720097.png" style="zoom: 33%;" />

## 可逆VS不可逆

- 可逆计算 在时间和空间上是多项式的(polynomial overhead)
- 可逆计算在能量上更加有效。因为根据Landauer's principle，每擦除一个比特的信息，就要至少  $k_{b} T$  能量，有兴趣的话可以查文献(arxiv: 1803.02789)



# 量子计算

量子计算的优越性

- 前面说到**可逆计算**和**不可逆计算**解决问题的能力是等价的
- 量子计算可以解决可逆/不可逆不能解决的问题。
  - 比如判断一个函数是平衡函数还是常函数(Balancea or constant?)
  - 这个问题其实就是Deutsch-Jozsa算法解决的问题，Deutsch-Jozsa算法体现了量子计算的优越性。



本节概览

1. 介绍一个计算库 Yao
2. 用这个计算库Yao开构建量子加分器
3. 用量子算法Deutsch-Jozsa算法解决Balancea or constant的问题
4. 基于张量网络的量子线路模拟





## 介绍计算库Yao

计算库Yao是用编程语言Julia写的。

#### 为什么选择Julia?

高级语言，高性能计算，动态编程。很适合科学计算。

#### 关于Yao 

Yao的目的

- 设计量子算法
- 量子计算教育

Yao是中科院王磊，张潘老师，还有本次演讲的刘老师，罗秀哲等人写的。想要了解详情可以查看论文或者网站

- 论文(arXiv:1912.10877)
- 网站  [https://yaoquantum.org/](https://yaoquantum.org/)

## 用Yao介绍量子计算

导入Yao库的语法

```julia
using Yao , YaoPlots
```

这部分Yao的详细介绍很琐碎，如果有兴趣深入了解的，可以查看视频，或者论文或者网站上的导览教程

- 论文(arXiv:1912.10877)
- 网站  [https://yaoquantum.org/](https://yaoquantum.org/)

我只介绍个人觉得重要的概念



### 量子态

一个量子态的表示方式

- 用归一化向量表示
- 向量中的元素是复数
- 这个向量是在希尔伯特空间中



### 通用量子门

和前面的类似，在量子算中，我们也能找到通用的量子门，例如

- \{Toffoli, H\}
- \{CNOT, H, S, T\}

其中H表示Hadamard门

$$
H =\frac{1}{\sqrt{2}}\left(\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right)
$$
Hadamard矩阵写成外积的形式
$$
H =\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|)
$$
这里探究一下Hadamard矩阵对量子态 $|0\rangle$ 的作用
$$
\begin{aligned}
H |0\rangle &=\frac{1}{\sqrt{2}}(|0\rangle\langle 0|+| 0\rangle\langle 1|+| 1\rangle\langle 0|-| 1\rangle\langle 1|)|0\rangle \\
&=\frac{1}{\sqrt{2}}(|0\rangle\langle 0 \mid 0\rangle+|0\rangle\langle 1 \mid 0\rangle+|1\rangle\langle 0 \mid 0\rangle-|1\rangle\langle 1 \mid 0\rangle) \\
&=\frac{|0\rangle+|1\rangle}{\sqrt{2}}
\end{aligned}
$$
类似的
$$
H|1\rangle=\frac{|0\rangle-|1\rangle}{\sqrt{2}}
$$
也就是说，Hadamard门可以制造叠加态



Hadamard门作用到一个量子态上两次，就回到原来的量子态上

1. 我们知道作用一次 $H|0\rangle=\frac{|0\rangle+|1\rangle}{\sqrt{2}}$
2. 作用两次 $H H|0\rangle=H\frac{|0\rangle+|1\rangle}{\sqrt{2}}=|0\rangle$



### 例子

用Yao可以构建哈密顿量，比如Heisenberg模型

## Deutsch-Jozsa算法

Deutsch-Jozsa算法可以体现量子计算的优越性，它处理的问题是Balancea or constant?

> 给定输入和输出，如何快捷地判断 f(x) 是属于常数函数，或是平衡函数。

### 常数或平衡

我们先介绍什么是常数函数，什么是平衡函数。

1. 常数函数(constant function)
   - 不论输入是0还是1，输出都是 f(x)=0 
   - 不论输入是0还是1，输出都是 f(x)=1 
2. 平衡函数(balanced function)有两种情况
   - 恒等函数(identity function)：输入是0，输出是 f(0)=0 ，输入是1，输出是 f(1)=1 
   - 翻转函数(bit flip function)：输入是0，输出是 f(0)=1 ，输入是1，输出是 f(1)=0 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211225022333452.png" style="zoom:50%;" />

常数函数和平衡函数的一个区别特征是

- 平衡函数(balanced function)对于不同的输入，输出0和1是各一半
- 常数函数(constant function)对于不同的输入，输出的都一样

### Deutsch算法

Deutsch-Josza算法是Deutsch算法的推广，

- Deutsch算法是解决输入一位的问题
- Deutsch-Josza算法是解决输入 x 是一个由 0 和 1 组成的 n 个字符串的问题。

所以为了容易理解，我先计算Deutsch算法，以下面一个例子来介绍

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200513083111541.png" alt="image-20200513083111541" style="zoom:50%;" />

对于这个线路图，过程如下

1. 对第一位的初始态 $|0\rangle$ 作用一个Hadamard门。输出 $\frac{|0\rangle+|1\rangle}{\sqrt{2}}$
2. 第一位输出的$\frac{|0\rangle+|1\rangle}{\sqrt{2}}$ 和第二位的初始态 $|0\rangle$  一起被 一个作用于两个量子位的幺正运算输出 $U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle$

> 补充笔记
>
> 这里用到了一个作用于两个量子位的幺正运算$U_{f}$
> $$
> U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle
> $$
> 这个门的作用是
>
> - 第一位的量子比特保持不变
> - 第二位量子比特 $y $ 和函数产生新的输出 $y \otimes f(x)$
>
> 

假如 $f(x)$ 是恒等函数，过程计算如下
$$
\begin{aligned}
U_{f}\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle
&=\frac{1}{\sqrt{2}}\left(U_{f}|00\rangle+U_{f}|10\rangle\right)
\\&=\frac{|0,0 \oplus f(0)\rangle+|1,0 \oplus f(1)\rangle}{\sqrt{2}}
\\&=\frac{|00\rangle+|11\rangle}{\sqrt{2}}
\end{aligned}
$$
其中

- $0 \oplus 0=1 \oplus 1=0$ 
- $0 \oplus 1=1 \oplus 0=1$ 

更一般的输出如下
$$
U_{f}\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle=\frac{|0, f(0)\rangle+|1, f(1)\rangle}{\sqrt{2}}
$$



### Deutsch-Josza算法

Deutsch-Josza算法是Deutsch算法的推广，Deutsch-Josza算法是全过程如下
$$
\left|\psi_{\text {out}}\right\rangle=(H^{\otimes n} \otimes I) U_{f}(H^{\otimes n} \otimes H)|0\rangle^{\otimes n}|1\rangle
$$

接下来详细讲解这个公式的过程

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20200513095343202.png" alt="image-20200513095343202" style="zoom:50%;" />





#### 1. 初始化

我们输入 $n$ 个状态 $|0 \rangle$ 的量子比特态，和一个 $|1 \rangle$ 的量子比特态。

每个态都作用一个Hadamard门
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=&\left(H^{\otimes n}\right)\left(|0\rangle^{\otimes n}\right) \otimes(H|1\rangle) \\
=&\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
\end{aligned}
$$

#### 2. U门

使用 $U_{f}$ 门
$$
U_{f}|x, y\rangle=|x, y \otimes f(x)\rangle
$$
最后一个量子比特态 $|1 \rangle$ 扮演着公式中 $y$ 的角色，经过 $U_{f}$ 门输出是
$$
\left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x}(-1)^{f(x)}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$

#### 3. Hadamard门

第三步是Hadamard门作用到前 $n$ 个态 $|x\rangle$ 上
$$
H^{\otimes n}|x\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{y}(-1)^{x \cdot y}|y\rangle
$$

最后输出是
$$
\left|\psi_{\text {out}}\right\rangle=\frac{1}{2^{n}} \sum_{y} \sum_{x}(-1)^{x \cdot y+f(x)}|y\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
$$

#### 4. 判断

测量输出，现在前 $n$ 个态是 $|y\rangle$ 

- 如果前 $n$ 个态 $|y\rangle$ 的测量结果全都是0，那么 $f(x)$ 是常数函数
- 如果前 $n$ 个态 $|y\rangle$ 的测量结果有至少一个1或者更多的1，那么 $f(x)$ 是常数函数

### 例子

**题目**

  考虑两比特的输入，函数是$f(x)=1 .$ 写出详细的过程展示Deutsch-Josza算法下线路输出量子态 $|y\rangle=|00\rangle$ 

------

**解答**

初始态输入 $\left|\psi_{i n}\right\rangle=|0\rangle|0\rangle|1\rangle .$ 运用 Hadamard门作用到态上
$$
\begin{aligned}
\left|\psi^{\prime}\right\rangle=&H ^{\otimes 3}|0\rangle|0\rangle|1\rangle
\\=&\frac{1}{2 \sqrt{2}}(|000\rangle-|001\rangle+|010\rangle-|011\rangle+|100\rangle-|101\rangle+|110\rangle-|111\rangle)
\end{aligned}
$$

> $$
> \begin{aligned}
> \left|\psi^{\prime}\right\rangle=&\frac{1}{\sqrt{2^{n}}} \sum_{x \in\{0,1\}^{n}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\\
> =&\frac{1}{\sqrt{2^{2}}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\\
> =&\frac{1}{2\sqrt{2}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(|0\rangle-|1\rangle\right)\\
> =&\frac{1}{2\sqrt{2}} \sum_{x \in\{0,1\}^{2}}|x\rangle\left(|0\rangle-|1\rangle\right)
> \end{aligned}
> $$
>
> 求和的 $x \in\{0,1\}^{2}$ 可能性包含
>
> - $|x\rangle=|00\rangle$ 
> - $|x\rangle=|01\rangle$ 
> - $|x\rangle=|10\rangle$ 
> - $|x\rangle=|11\rangle$ 

运用 $U_{f}$ 门作用到上面的态上
$$
\begin{aligned}
\left|\psi^{\prime \prime}\right\rangle=& U_{f}\left|\psi^{\prime}\right\rangle
\\=&\frac{1}{2 \sqrt{2}}U_{f}(|000\rangle-|001\rangle+|010\rangle-|011\rangle+|100\rangle-|101\rangle+|110\rangle-|111\rangle)
\\=&\frac{1}{2 \sqrt{2}}(|001\rangle-|000\rangle+|011\rangle-|010\rangle+|101\rangle-|100\rangle+|111\rangle-|110\rangle)
\end{aligned}
$$
其中第二步用到逻辑关系 $f(x)=1 .$ 

> 补充过程
> $$
> \left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{n}}} \sum_{x}(-1)^{f(x)}|x\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
> $$
>
> $$
> \left|\psi^{\prime \prime}\right\rangle=\frac{1}{\sqrt{2^{2}}} \sum_{x}(-1)^{1}|00\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
> $$
>
> 求和的 $x \in\{0,1\}^{2}$ 可能性包含
>
> - $|x\rangle=|00\rangle$ 
> - $|x\rangle=|01\rangle$ 
> - $|x\rangle=|10\rangle$ 
> - $|x\rangle=|11\rangle$ 
>
> 如果不用通用公式，而是直接计算，结果是？
> $$
> \begin{aligned}
> U _{ f }|000\rangle &=|0,0 \oplus f (0),0\rangle+|0,0, \oplus f (0)\rangle \\
> &=|010\rangle+|001\rangle
> \end{aligned}
> $$
> 还是？
> $$
> \begin{aligned}
> U _{ f }|000\rangle &=|0,0 \oplus f (0),0 \oplus f (0)\rangle\\
> &=|011\rangle 
> \end{aligned}
> $$
> 经过验算，我认为是后者

最后一步是把 $H^{\otimes 2}$ 作用到前面两个量子比特上
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{2 \sqrt{2}}\left[\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle\right.\\
&+\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle
\\&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle+|1\rangle}{\sqrt{2}}\right)|0\rangle \\&+\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|1\rangle-\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)|0\rangle
\end{aligned}
$$
展开所有项得到
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle= \frac{1}{4 \sqrt{2}}&[(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|1\rangle-(|00\rangle+|01\rangle+|10\rangle+|11\rangle)|0\rangle\\
&+(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|1\rangle-(|00\rangle-|01\rangle+|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|1\rangle-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)|0\rangle \\
&+(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|1\rangle-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)|0\rangle]
\end{aligned}
$$
把这些项的第三位提取公因式 $(|0\rangle-|1\rangle / \sqrt{2})$ 得到
$$
\begin{aligned}
\left|\psi_{\text {out}}\right\rangle=& \frac{1}{4}\left[-(|00\rangle+|01\rangle+|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\right.\\
&-(|00\rangle-|01\rangle+|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&-(|00\rangle+|01\rangle-|10\rangle-|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right) \\
&\left.-(|00\rangle-|01\rangle-|10\rangle+|11\rangle)\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)\right]
\\ =&-|00\rangle\left(\frac{|0\rangle-|1\rangle}{\sqrt{2}}\right)
\end{aligned}
$$
测量前两位量子比特得到 $00,$ 确认这是常数函数



## 量子加法器

用Yao写一个量子加法器Quantum adder

> 详情见视频

# 基于张量网络的量子线路模拟

- 对于一些问题用经典计算就可以处理
- 有些问题用量子计算处理才更加有效
- 有没有问题是介于两种之间？有的，用张量网络

## 指数问题

对于一个比特的向量
$$
v_{i}=\left(\begin{array}{l}
a_{i} \\
b_{i}
\end{array}\right)
$$
多比特的量子态，是用各个二分量向量张量积(tensor products)

$$
\left|\psi_{1}\right\rangle = v_{1} \otimes v_{2} \otimes \ldots \otimes v_{n}
$$

> 补充笔记（向量的张量积(tensor products)）
>
> 二量子比特态可以写成两个单量子比特态之间的张量积(tensor products)
> $$
> | a \rangle \otimes| b \rangle
> $$
> 二量子比特态总共有4种可能
> $$
> |00\rangle,|01\rangle,|10\rangle,|11\rangle
> $$
> 如果用向量表示
> $$
> \begin{array}{l}
> |01\rangle=\left(\begin{array}{l}
> 1 \\
> 0
> \end{array}\right) \otimes\left(\begin{array}{l}
> 0 \\
> 1
> \end{array}\right)=\left(\begin{array}{l}
> 0 \\
> 1 \\
> 0 \\
> 0
> \end{array}\right) \\
> |11\rangle=\left(\begin{array}{l}
> 0 \\
> 1
> \end{array}\right) \otimes\left(\begin{array}{l}
> 0 \\
> 1
> \end{array}\right)=\left(\begin{array}{l}
> 0 \\
> 0 \\
> 0 \\
> 1
> \end{array}\right)
> \end{array}
> $$



我们看到了向量的张量积(tensor products)，如果是n个量子比特的量子态，向量从长度就是 $2^{n}$ 。是指数增长的，一般计算机是受不了较大的指数增长。类似的，量子态的内积也是

假如有两个量子态
$$
\left|\psi_{1}\right\rangle=v_{1} \otimes v_{2} \otimes \ldots \otimes v_{n}
$$
$$
\left|\psi_{2}\right\rangle=w_{1} \otimes w_{2} \otimes \ldots \otimes w_{n}
$$
他们的内积

$$
\left\langle\psi_{2} \mid \psi_{1}\right\rangle=\sum_{s \in\{0,1\}^{n}} \prod_{i=1}^{n}\left(v_{i}\right)_{s_{i}}\left(w_{i}\right)_{s_{i}}
$$
可以看出来是指数增长级别的项。

有一种解决方法，把求和号和连乘号对换
$$
\left\langle\psi_{2} \mid \psi_{1}\right\rangle=\prod_{i=1}^{n} \sum_{s_{i} \in\{0,1\}}\left(v_{i}\right)_{s_{i}}\left(w_{i}\right)_{s_{i}}
$$
这样计算就是线性级别的项

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211225025304950.png" style="zoom:50%;" />

这样做是更高效的，把这个思路应用到量子线路的模拟中



## 求和乘积网络

求下面值

$$
\left\langle\psi_{2}|U| \psi_{1}\right\rangle
$$
其中 $U$ 是你的线路

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20211225025749477.png" style="zoom:50%;" />

前面说的 $\left\langle\psi_{2} \mid \psi_{1}\right\rangle$ 和这里的 $\left\langle\psi_{2}|U| \psi_{1}\right\rangle$ 本质都是同一类运算，叫做 sum product 

- 图上输入态是一个乘积态
- 把相应的指标进行连接，这其实是一个张量网络表示
- 一个张量网络表示可以用爱因斯坦求和表示

这部分刘老师觉得没有完全准备好，推荐几篇文章都是很好的文章大家回去自己看

1.  Markov, Igor L., and Yaoyun Shi. "Simulating quantum computation by contracting tensor networks." SIAM Journal on Computing 38.3 (2008): 963-981. https://epubs.siam.org/doi/abs/10.1137/050644756
2.  Pan, Feng, Keyang Chen, and Pan Zhang. "Solving the sampling problem of the Sycamore quantum supremacy circuits." arXiv preprint arXiv:2111.03011 (2021).   https://arxiv.org/abs/2111.03011
3.  Gao, Xun, et al. "Limitations of Linear Cross-Entropy as a Measure for Quantum Advantage." arXiv preprint arXiv:2112.01657 (2021). https://arxiv.org/abs/2112.01657

# 附录：相关资源

文中提到的参考资料小结

背景知识可以参考的两本书

1. J.J. Sakurai."Modern Quantum Mechanics." 是讲量子力学的一本很好的教材，特别是前三章。
2. Nielsen, Michael A., and Isaac Chuang. "Quantum computation and quantum information." (2002): 558-559. 是量子计算的经典书籍。

量子计算模拟库Yao

- 论文(arXiv:1912.10877)
- 网站  [https://yaoquantum.org/](https://yaoquantum.org/)

基于张量网络的量子线路模拟

1.  Markov, Igor L., and Yaoyun Shi. "Simulating quantum computation by contracting tensor networks." SIAM Journal on Computing 38.3 (2008): 963-981. https://epubs.siam.org/doi/abs/10.1137/050644756
2.  Pan, Feng, Keyang Chen, and Pan Zhang. "Solving the sampling problem of the Sycamore quantum supremacy circuits." arXiv preprint arXiv:2111.03011 (2021).   https://arxiv.org/abs/2111.03011
3.  Gao, Xun, et al. "Limitations of Linear Cross-Entropy as a Measure for Quantum Advantage." arXiv preprint arXiv:2112.01657 (2021). https://arxiv.org/abs/2112.01657