量子互文

# 概览

- **时间：**2022年01月20日
- **摘要：**  在本期讨论中，将简单地回顾量子关联这个概念。量子关联刻画了经过量子测量后，不能被经 典物理、理论（比如一般的随机过程，或被称为隐变量理论、实在论模型）描述的统计结果。具体地, 我们将讨论量子非局域性和量子互文。我们会通过一种不需要太多量子力学知识就能理解的方式介绍这些概念。然后我们会讨论量子关联在机器学习, 特别是在语言翻译中的潜在应用。我们希望通过这次讨论, 让大家能感受到研究量子力学基础问题也可能对日常生活中的问题产生应用
- **主讲人:**  皓勋 
  - 北大本科，清华博士，现为哈佛大学博士后
- **主要研究领域:**  量子信息及其应用
- **个人主页:** 
- **记录人：**黄清扬；庄嘉培





[TOC]





这个报告中想讨论些什么

- 量子性远比随机性和不确定性要丰富的一个概念 (no-go theorem for hidden variable theory, quantum non-locality)
- 量子纠缠并不能超光速的传信息
- 一些量子系统会有更多的记忆能力 (这是因为量子互文quantum contextuality这一种量子关联)
- 这些概念如何在序列模拟中的应用



## 参考文献

1. 本次分享的主要参考文献：Chapter 2 of "Alber G, Beth T, Horodecki M, Horodecki P, Horodecki R, Rötteler M, Weinfurter H, Werner R, Zeilinger A. Quantum information: An introduction to basic theoretical concepts and experiments. Springer"
2. Wikipedia on quantum contextuality: https://en.wikipedia.org/wiki/Quantum_pseudo-telepathy
3. 演讲者的原创工作 My own work on quantum correlation \& generative models "Gao $X$, Anschuetz ER, Wang ST, Cirac Jl, Lukin MD. Enhancing generative models via quantum correlations. arXiv preprint arXiv:2101.08354. 2021 Jan 20." \& "Anschuets ER, HY Hu, JL Huang, Gao X. In preparation"





主要集中在讨论量子性(quantumness)是什么，讨论它跟经典力学的关系。

- 这里的经典力学其实是更广义的，它不得不光指牛顿力学，它还包括一些比如说最一般的随机过程
- 主要讨论量子力学是超出经典的部分，这些就叫做**量子关联**。

# 量子信息VS经典信息

### 一个重要的问题

> 量子信息本质上它是一种很不一样的信息，还是它本身只是经典信息的一个特例？

关于这个问题的回答其实就是理解量子机器能力的关键所在，

- 如果这个问题的回答是的话，那么我们就没有必要去建造比如说量子计算机，因为本质上量子信息它也是一种经典信息。然后我们也可以在他们之间互相转化。
- 但是如果这个回答是否的话，那么力量子的机器会提供更强大的能力在信息处理的问题上。

### 思想实验

做一些思想实验，假设量子信息和经典信息可以互相转换

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406100933246.png" style="zoom:50%;" />

- 这个设备 $P$ 是一个从经典的比特，到量子比特的一个转化。在量子力学中，这个其实叫做**量子态制备**。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406101110140.png" style="zoom:50%;" />

- 上面过程的反向的过程中反向过程 $M$ 是把一些量子的比特，转化成了一些经典的比特。这个过程在量子力学中叫做**测量**

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406101316452.png" style="zoom:50%;" />

- 把上面两个过程组合起来，形成classical teleportation。
  1. 这个机器的作用：有一些量子系统，通过某个设备把它转化成经典信息，然后我们通过发送经典信息给另一方，另一方会根据这些信息制备这样一个量子态。
  2. 假想传输过程是没有损失的。没有损失的意思是如果我们前后做一些统计测试，然后我们分辨不出来区别

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406101749950.png" style="zoom:50%;" />

- 在上面classical teleportation基础上，多一份经典信息复制再转换成量子信息。这个机器称为quantum copier
  1. 因为从输入和输出角度看，一份量子信息输入，两份量子信息输出。



<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406102649131.png" style="zoom:50%;" />

- 在quantum copier的基础上，添加两个经典测量
  1. 比如 A 可以是位置测量， B 可以是动量测量。
  2. 也就是说如果我们有一个量子复制机的话，我们就可以做一个**关联测量**。用数学表示
     - $\sum_{b} \operatorname{Pr}(a, b \mid A, B)=\operatorname{Pr}(a \mid A)$ (the probability if just measuring $A$ )
     - $\sum_{a} \operatorname{Pr}(a, b \mid A, B)=\operatorname{Pr}(b \mid B)$ (the probability if just measuring $B$ )
  3. 在量子力学中，或者傅里叶变换中，动量和位置，时间和频率，关联测量是不可能的。



### 隐变量

- quantum copiers $\Rightarrow$ 关联测量
- 关联测量 $\cancel{\Rightarrow}$ quantum copier 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406104724196.png" style="zoom: 50%;" />

量子信息可以转化成经典信息的时候，有两种方式可以去讨论

1. 过程是确定性的：给一个量子态，然后我就可以获得它的完整描述。
   - 就是所谓的量子克隆。
2. 过程是不确定的：给一个量子态，每一次测量我都得到不一样的经典信息。
   - 这个就是更弱版本的量子复制机，这个其实就已经足够推出关联测量
   - 这里的不确定性其实就是所谓的**隐变量**。

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406101316452.png" style="zoom:50%;" />

前面说到的过程，量子信息 $\Rightarrow$ 经典信息 $\Rightarrow$ 量子信息，如果传输是无损的，中间的经典信息就是一种隐变量 hidden variable $\lambda$

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406165429756.png" style="zoom:50%;" />

如果有隐变量的话，其实能给出关联测量

- 如果这就是测量 $a, b$ 的话，那么我们就可以给出 $A, B$ 的信息。
- 用数学严格化形式：$\lambda \in\left\{\lambda_{1}, \cdots, \lambda_{i}, \cdots\right\}$, a quantum state is actually a distribution $p(\lambda)$ over $\lambda$ the above discussion of measurement: $\lambda_{i}(A)=a_{i} \& \lambda_{i}(B)=b_{i}$

小结

>  如果量子信息是一种经典信息的话，也说它有隐变量理论的话，就会存在一个关联的测量。



# 量子纠缠

用刚才我们讨论过的关联测量的这个概念，和量子纠缠结合起来讨论。

1. 如果我们考虑量子力学的关于纠缠态的一些测量统计的结果是成立的
2. 我们同时又假设有关联测量的存在，也就说有有隐变量理论的存在

那我们将会有超光速度通讯能力，下面我们给出具体的推导。

### Alice 和 Bob 的通讯游戏

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406170512080.png" style="zoom:50%;" />

#### 图片情景解释

1. 假设现在有Alic和 Bob 两个人
2. 共享一个纠缠态 $S$
3. Alic想去给 Bob 一个通讯的信息
   - 想发送+1的话，他就测 $A_{1}$
   - 想发送-1的话，他就测 $A_{2}$
4. 假设Bob有关联测量的能力，就是他可以直接测 $B_{1} \& B_{2}$，得到 $b_{1}$ $b_{2}$ 的统计结果
   - Bob 的目标：他想用超过1/2 的概率去知道Alic发送的是+1还是-1 

Bob关联测量的数学表达
$$
\begin{aligned}
\sum_{b_{1}} \operatorname{Pr}\left(a_{i}, b_{1}, b_{2} \mid A_{i}, B_{1} \& B_{2}\right)=\operatorname{Pr}\left(a_{i}, b_{2} \mid A_{i}, B_{2}\right) \\
\sum_{b_{2}} \operatorname{Pr}\left(a_{i}, b_{1}, b_{2} \mid A_{i}, B_{1} \& B_{2}\right)=\operatorname{Pr}\left(a_{i}, b_{1} \mid A_{i}, B_{1}\right)
\end{aligned}
$$

#### 概率计算

 Bob怎么来猜爱丽丝的选择的。

1. 如果测到 $b_{1}=b_{2}$ 的话，那么 Bob 就猜Alice测了$A_{1}$
2. 否则猜Alice测了$A_{1}$

假设Alice测了$A_{1}$，Bob猜对的概率
$$
\begin{aligned}
&\sum_{a_{1}, b_{1}, b_{2}}\left|\frac{b_{1}+b_{2}}{2}\right|\left|a_{1}\right| \operatorname{Pr}\left(a_{1}, b_{1}, b_{2} \mid A_{1}, B_{1} \& B_{2}\right) \\ \geq &\frac{1}{2} \sum_{a_{1}, b_{1}, b_{2}}\left(b_{1}+b_{2}\right) a_{1} \operatorname{Pr}\left(a_{1}, b_{1}, b_{2} \mid A_{1}, B_{1} \& B_{2}\right)
\\=&\frac{1}{2}\left(\sum_{a_{1}, b_{1}} a_{1} b_{1} \operatorname{Pr}\left(a_{1}, b_{1} \mid A_{1}, B_{1}\right)+\sum_{a_{1}, b_{2}} a_{1} b_{2} \operatorname{Pr}\left(a_{1}, b_{2}\mid A_{1}, B_{2}\right)\right)\\:=& \frac{1}{2}\left(C\left(A_{1}, B_{1}\right)+C\left(A_{1}, B_{2}\right)\right)
\end{aligned}
$$
假设Alice测了$A_{2}$，Bob猜对的概率
$$
\begin{aligned}
&\sum_{a_{2}, b_{1}, b_{2}}\left|\frac{b_{1}-b_{2}}{2}\right|\left|a_{2}\right| \operatorname{Pr}\left(a_{2}, b_{1}, b_{2} \mid A_{2}, B_{1} \& B_{2}\right) \\\geq&\frac{1}{2}\left(C\left(A_{2}, B_{1}\right)-C\left(A_{2}, B_{2}\right)\right)
\\\geq& \frac{1}{2} \cdot \frac{1}{2}\left(C\left(A_{1}, B_{1}\right)+C\left(A_{1}, B_{2}\right)\right)+\frac{1}{2} \cdot \frac{1}{2}\left(C\left(A_{2}, B_{1}\right)-C\left(A_{2}, B_{2}\right)\right)
\\=&\frac{1}{4}\left(C\left(A_{1}, B_{1}\right)+C\left(A_{1}, B_{2}\right)+C\left(A_{2}, B_{1}\right)-C\left(A_{2}, B_{2}\right)\right)
\\:=& \frac{\beta}{4} \text { (Bell's correlation) }
\end{aligned}
$$

#### 小结

Bob可以猜对Alice正确的概率$\geq \frac{\beta}{4}$ 

1. 如果是隐变量理论，对于任何$A_{1}, A_{2}, B_{1}, B_{2}$，$\beta\leq 2$（这是著名的贝尔不等式）
2. 如果是量子力学，对于某些选择$A_{1}, A_{2}, B_{1}, B_{2}$，$\beta=2\sqrt{2}$

所以隐变量理论和量子力学的预测是**不能同时成立**。

贝尔关联，又称量子非局域性，一种超越任何经典关联的关联关系

### CHSH game

贝尔关联的另一种理解——CHSH game

- 经典理论预测的成功概率: $\leq 0.75$
- 量子理论预测的成功概率: $\approx 0.85$



# 量子互文

### 游戏例子

九宫格要求格子中数字

- 每一行数字的乘积必须是+1
- 每一列数字的乘积必须是-1

如图的例子

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406181426128.png" style="zoom:50%;" />

尝试后发现都是失败，所以说这个游戏在这个约束下，没有一个成功的办法。

#### 量子版本

量子版本在九宫格里填的是算符

- 每一行算符的乘积必须是正的单位矩阵(identity)  
- 每一列算符的乘积必须是负的单位矩阵
- 额外的要求：这些算符必须有关联测量。在量子力学中，关联测量它就意味着这些算符之间互相是对易的。

我们可以找到一些算符的解

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220603201939263.png" style="zoom:67%;" />

其中

- $I=\left(\begin{array}{ll}
  0 & 1 \\
  1 & 0
  \end{array}\right)$
- $X=\left(\begin{array}{ll}0 & 1 \\ 1 & 0\end{array}\right)$
- $Z=\left(\begin{array}{cc}1 & 0 \\ 0 & -1\end{array}\right)$

$X$ 和 $Z$ 类似于二维版本的位置和动量的关系，因为他们是通过一个傅里叶变换 $\frac{1}{\sqrt{2}}\left(\begin{array}{cc}1 & 1 \\ 1 & -1\end{array}\right)$ 联系起来

### 互文

> - 所以在经典中我们找不到解，在量子版本中找得到解
> - 解的存在不存在，也可以定义一个类似于贝尔关联的 $\beta$ ，这里我们可以叫成**互文的关联**。
>
> 

定义
$$
\begin{aligned}
\beta=& C\left(O_{11}, O_{12}, O_{13}\right)+C\left(O_{21}, O_{22}, O_{23}\right)+C\left(O_{31}, O_{32}, O_{33}\right) \\
&-C\left(O_{11}, O_{21}, O_{31}\right)-C\left(O_{12}, O_{22}, O_{32}\right)-C\left(O_{13}, O_{23}, O_{33}\right)
\end{aligned}
$$
其中

- $O_{i j}$ 表示第 $i$ 行，第 $j$ 列的算符

解的存在不存在，给出不等式

- 隐变量理论: $\beta \leq 4$
- 量子理论: $\beta=6$

#### 小结

1. 由于量子互文的存在，如果一个隐变量里面试图去描述这个量子系统的话，他就需要去记住更多的信息。
   - 比如例子中需要记住到底是在哪一个框，在哪一个 context 下
   - 这个跟**语言问题**很像(语言问题中上下文相关性)，这也是为什么有"量子互文"这样一个名字。



## 序列模型

序列生成模型

1. 测 X 观测量，给出测量结果 Y 
2. 测量之后系统有可能会被扰动，体现在 $h_{i}$ 的变化上
3. 系统演化由这个参数 $W^{\text {hh }}$ 来刻画。
4. 测量带来的扰动，就是前面说的测不准原理，我们把这个情况也包进去，然后包进来的话 

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406200024687.png" style="zoom:50%;" />

- 对于离散模型：例如隐马尔可夫模型（hidden Markov model） 
- 对于连续变量模型。例如递归神经网络（RNN）

这个模型有一些应用，比如语言翻译问题(translation problem)

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406201008931.png" style="zoom:50%;" />

### 演讲者的模型

和上图类似，做一些替换

1. $x$ 观测量
2. $y$ 测量结果
3. $W$ 训练参数
4. $h \rightarrow|h\rangle$ 携带信息的量子态

#### 结果-1 表达能力

最近有一些结果证明了同样是这样一个图示，$h$ 是经典的隐变量还是量子态，他们之间的表达能力是有区别的。

- 量子模型需要$N$隐藏的神经元/量子比特作为latent variables；
- 任何经典模型至少需要$N^{2}$隐藏的神经元/比特隐变量。

#### 结果-2 应用翻译

应用到英语到西班牙语的翻译

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406202303318.png" style="zoom:50%;" />

<img src="https://jptanjing.oss-cn-beijing.aliyuncs.com/img/image-20220406202317607.png" style="zoom:50%;" />

1. 最早的模型QRNN

   - 对照的模型：RNN: gated-recurrent-unit (GRU), a variant of LSTM

2. 都是用了 20 个神经元

3. 从图上看出，QRNN的翻译结果更好

   

## 附录：相关资源

- 本次分享的主要参考文献：Chapter 2 of "Alber G, Beth T, Horodecki M, Horodecki P, Horodecki R, Rötteler M, Weinfurter H, Werner R, Zeilinger A. Quantum information: An introduction to basic theoretical concepts and experiments. Springer"
- Wikipedia on quantum contextuality: https://en.wikipedia.org/wiki/Quantum_pseudo-telepathy
- 演讲者的原创工作 My own work on quantum correlation \& generative models "Gao $X$, Anschuetz ER, Wang ST, Cirac Jl, Lukin MD. Enhancing generative models via quantum correlations. arXiv preprint arXiv:2101.08354. 2021 Jan 20." \& "Anschuets ER, HY Hu, JL Huang, Gao X. In preparation"

