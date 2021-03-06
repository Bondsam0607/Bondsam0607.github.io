---
layout: page
title: 网络理论基础
tags: 学校
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<!--more-->


## 第二章 通信信源模型和M/M/1排队系统

- 泊松过程
	- 定理2-1
	- 性质2-1 ： 可加性
	- 性质2-2 ： 可分性
- 泊松过程和负指数分布的关系
	- 性质2-3 ： 无记忆特性
	- 性质2-4
	- 定理2-2 ： 泊松过程和负指数分布的关系
- 生灭过程
	- 定义
	- 稳态分布
	- 定理2-3：极限定理
- M/M/1排队系统
	- 排队系统的数学描述
	- 排队系统的分析
	- Little公式
	- M/M/1
	- 定理2-5

泊松过程描述规定时间内到达多少个呼叫流

负指数分布描述两个呼叫流之间的时间间隔

### 一、泊松过程

泊松过程过程的性质：

$$P_k(a,a+t)=P_k(t)$$

$$\sum_{k=0}^{\infty}p_k(t)=1$$

#### 定理2-1

对于Poisson呼叫流，长度为$$t$$的时间内到达$$k$$个呼叫的概率$$p_k(t)$$服从Poisson分布，即

$$p_k(t)=\frac{(\lambda t)^k}{k!}e^{-\lambda t}$$

其中$$\lambda > 0$$为常数，表示平均到达率。

Poisson过程在任何时间区间内的到达率都是一样。

#### 性质2-1 ： 可加性

m个Poisson流的参数分别是$$\lambda_1, \lambda_2, ... ,\lambda_m$$，且相互独立

则合并流仍然为Poisson流，且

$$\lambda = \lambda_1 + \lambda_2 + ... + \lambda_m$$

说明独立的Poisson过程是可加的。

#### 性质2-2 ： 可分性

性质2-1的反性质，参数为$$\lambda = \lambda_1 + \lambda_2$$ 的Poisson流到达交换局A后，被分解成两个独立的Poisson流，参数分别为$$\lambda_1$$和$$\lambda_2$$。

### 二、负指数分布

若随机变量$$X$$满足

$$P\{X>=t\}=e^{-\lambda t}, t>=0$$

这个分布被称为参数$$\lambda$$的负指数分布

其概率密度函数为：

$$f_x(t)=\lambda e^{-\lambda t}, t>=0$$

#### 性质2-3 ：无记忆特性

假定$$X$$服从参数为$$\lambda$$的负指数分布，对于任意$$t,s>=0$$有

$$P\{X>=t+s|X>=t\}=P\{X>=s\}$$

#### 性质2-4

假设$$T_1,T_2$$为相互独立的两个负指数分布，参数分别为$$\lambda_1 , \lambda_2$$，令$$T=min(T_1,T_2)$$

1. $$T$$是一个以$$\lambda_1 + \lambda_2$$为参数的负指数分布
2. $$T$$的分布和$$T_i$$谁是较小数无关
3. $$P\{T_1<T_2|T=t\}=\frac{\lambda_1}{\lambda_1 + \lambda_2}$$

**性质2-4.3的证明**

概率分布函数为

$$T_1: \lambda_1 e^{-\lambda_1 t}$$

$$T_2: \lambda_2 e^{-\lambda_2 t}$$

$$\int\int\lambda_1\lambda_2e^{-\lambda_1x-\lambda_2y}dxdy\\=\int_{0}^{\infty}\lambda_1e^{-\lambda_1x}dx\int_{x}^{\infty}e^{-\lambda_2y}dy\\=\int_{0}^{\infty}\lambda_1e^{-\lambda_1x}e^{-\lambda_2x}dx\\=\frac{\lambda_1}{\lambda_1+\lambda_2}$$

#### 定理2-2 ： 泊松过程和负指数分布的关系

一个随机过程是参数$$\lambda$$的Poisson过程的充要条件是呼叫到达间隔$$X_i,i=1,2...$$相互独立，且服从相同参数$$\lambda$$的负指数分布

### 三、生灭过程

生灭过程的极限解或稳态解有很简单的形式

#### 定义

$$N(t)$$表示在时刻$$t$$的状态，$$N(t)=k$$，称为在$$t$$时刻系统处于状态$$k$$。

<img src="../images/Network_Theory/markov.png" width="60%"/>

#### 稳态分布

记$$p_{ik}(t)$$为系统从状态$$i$$经过时间$$t$$后转移到$$k$$的条件概率

$$p_{ik}(t)>=0, \sum_{k=0}^{\infty}p_{ik}(t)=1$$

<img src="../images/Network_Theory/markov.png" width="60%"/>

$$p_k(t+\Delta t)=\sum_{i=0}^{\infty}p_i(t)p_{ik}(\Delta t) \\ =p_k(t)(1-(\lambda_k+\mu_k)\Delta t+o(t))+p_{k-1}(t)(\lambda_{k-1}\Delta t+o(t))+p_{k+1}(t)(\mu_{k+1}\Delta t+o(t))+o(\Delta t)$$

**Kolmogorov方程**

$$\frac{dp_k(t)}{dt}=-(\lambda_k+\mu_k)p_k(t)+\lambda_{k-1}p_{k-1}(t)+\mu_{k+1}p_{k+1}(t)$$

当t趋于∞时，$$\frac{dp_k(t)}{dt}=0$$

设$$Z_k=\lambda_{k-1}p_{k-1}-\mu_kp_k$$

则有 $$Z_k=Z_{k+1}$$

则有 $$\lambda_{k-1}p_{k-1} = \mu_kp_k$$

即 $$p_k=\frac{\lambda_{k-1}}{\mu_k}p_{k-1}$$

令 $$\theta_k=\frac{\lambda_0 \lambda_1 ... \lambda_{k-1}}{\mu_1 \mu_2 ... \mu_k}, k>=1 $$

得 $$p_k = \theta_k p_0, k=1,2,3...$$

由 $$\sum_{k=0}^{\infty}p_k=1$$

$$p_0\sum_{k=0}^{\infty}\theta_k=1$$

#### 定理2-3 ： 极限定理

对有限状态的生灭过程，或对满足$$\sum_k\theta_k<\infty, \sum_k\frac{1}{\lambda_k \theta_k}=\infty$$的生灭过程，稳态分布存在，且与初始条件无关。

### 四、M/M/1排队系统

#### 数学描述

三个方面

- 输入过程
- 服务时间
- 排队方式

<img src="../images/Network_Theory/sequence.png" width="60%"/>

如上图所示，$$t_1,t_2$$表示顾客到达排队系统的到达时间间隔，$$\tau_1,\tau_2$$表示不同顾客的服务时间。满足以下假设：

- $$t_i$$独立同分布
- $$\tau_i$$独立同分布
- $$t_i$$和$$\tau_i$$独立

输入过程和服务时间可以分别使用一个分布来表示

排队方式包括：
- FIFO或LIFO
- 队列容量：对顾客总数的限制

#### 排队系统的分析

到达率： $$\lambda=\frac{1}{E[t]}$$

服务率（离去率）： $$\mu = \frac{1}{E[\tau]}$$

#### Little公式

Little公式描述了任意排队系统中满足的关系

- $$N$$表示系统中平均顾客数
- $$T$$表示顾客在系统中的平均时间
- $$\lambda$$表示单位时间到达系统的顾客数

$$N=\lambda T$$

#### M/M/1

M表示负指数分布，1表示服务员数目，缺省表示容量无限大和FIFO方式

假设M/M/1的到达过程符合$$\lambda$$的Possion过程，服务时间是参数为$$\mu$$的负指数分布

<img src="/images/Network_Theory/MM1.png" width="60%"/>

令$$\rho = \frac{\lambda}{\mu}$$

所以$$p_k=\rho^kp_0$$

当$$\rho<1$$时，是一个等比数列

由$$p_0 \sum_{k=0}^{\infty}\rho^k = 1$$

由$$\sum_{k=0}^{\infty}\rho^k=\frac{1-\rho^\infty}{1-\rho}=\frac{1}{1-\rho}$$

$$p_0 \sum_{k=0}^{\infty}\rho^k=p_0 \frac{1}{1-\rho}=\frac{p_0}{1-\rho}=1$$

$$p_0=1-\rho\\p_k=\rho^k(1-\rho)$$

#### 定理2-5

M/M/1排队系统在稳态时，顾客在系统中停留时间$$s$$服从参数为$$\mu-\lambda$$的负指数分布。

## 第三章 Erlang拒绝和等待系统

- 电话网指标介绍
	- 电话交换系统
		- 业务量
		- 呼叫量
		- 时间阻塞率
		- 呼损
	- 数据交换系统
		- 交换时延
		- 排队时延
		- 服务时延
	- 电话网和数据网的性能评估
		- 电话网：全网平均呼损
		- 数据网：全网平均时延

### 一、电话网指标介绍

电话网包含电话交换系统和数据交换系统

#### 电话交换系统

<img src="../images/Network_Theory/tele_ex.png" width="60%"/>

##### 业务量

定义：业务量描述了在一定时间内，该s条线路被占用的总时间。

如果第$$r$$条信道被占用$$Q_r$$秒，则$$s$$条信道上的**业务量**为：

$$Q=\sum_{r=1}^{s}Q_r$$

##### 呼叫量

$$呼叫量=\frac{\mbox{业务量}}{\mbox{观察时间}}=\frac{Q}{T}$$

呼叫量的单位为$$erl$$，是个无量纲的单位。

**对于从外界到达交换系统的呼叫流，无限话源的称为Erlang系统，有限话源的称为Engset系统。**

##### 时间阻塞率

当$$s$$条中继线全部繁忙时，系统处于阻塞状态。

$$时间阻塞率p_s=\frac{\mbox{阻塞时间}}{\mbox{观察时间}}$$

##### 呼损

呼叫阻塞率/呼损：拒绝呼叫次数占总呼叫次数的比例。

呼损$$p_c=\frac{\mbox{被拒绝的呼叫次数}}{\mbox{总呼叫次数}}$$

一般$$p_s\approx p_c$$,如果到达的呼叫流为Poisson过程，有$$p_s=p_c$$

#### 数据交换系统

<img src="/images/Network_Theory/data_ex.png" width="60%"/>

- 信息被截为变长分组，在每条入线上，有不同的到达率。
- 分组包到达交换系统后，根据路由表完成交换到达相应的出口
- 产生出线冲突时，会排成队列，依次得到服务

##### 数据交换系统的时延

- 交换时延一般固定且较小
- 排队时延可变
- 服务时延与包长有关

**排队时延和服务时延合称系统时间**

#### 电话网和数据网的性能评估

##### 电话网——全网平均呼损

$$\mbox{全网平均呼损}=\frac{\sum_{i<j}a_{ij}P_{i,j}}{\sum_{i<j}a_{ij}}$$

其中$$a_{i,j},1<=i,j<=n$$为任意两点之间的呼叫量，$$p_{i,j},1<=i,j<=n$$为其中的呼损

##### 数据网——全网平均时延

$$\mbox{全网平均时延}=\frac{\sum_{i\neq j}\lambda_{ij}T_{ij}}{\sum_{i\neq j}\lambda_{ij}}$$

### 二、Erlang即时拒绝系统

#### MMs系统

**M/M/s状态转移图**

<img src="../images/Network_Theory/mms.png" width="60%"/>

根据稳态分布规律：$$p_k = \frac{1}{k!}(\frac{\lambda}{\mu})^kp_0, k=1,2,...,s$$

令 $$a = \frac{\lambda}{\mu}$$

得：$$p_k = \frac{1}{k!}a^kp_0$$

根据归一性：$$\sum_{k=0}^{s}\frac{1}{k!}a^kp_0=1$$

得：$$p_0=\frac{1}{\sum_{k=0}^{s}\frac{a^r}{r!}}$$

#### Erlang公式

稳态分布为: $$p_k=\frac{\frac{a^k}{k!}}{\sum_{r=0}^{s}\frac{a^r}{r!}}, k=0,1,...,s$$

**Erlang-B公式**：$$B(s,a)=\frac{\frac{a^s}{s!}}{\sum_{r=0}^{s}\frac{a^r}{r!}}, a = \frac{\lambda}{\mu}$$

该公式指的是系统的时间阻塞率

#### M/M/$$\infty$$

<img src="../images/Network_Theory/mmi.png" width="60%"/>

令$$a=\frac{\lambda}{\mu}$$

则$$p_k=(\frac{\lambda}{\mu})^k\frac{1}{k!}p_0=\frac{a^k}{k!}p_0$$

由$$\sum_{k=0}^{\infty}p_k=1$$

得$$p_0=e^{-a}$$

所以$$p_k=\frac{a^k}{k!}e^{-a}$$

该式子服从参数为a的柏松分布，如果k为系统中的呼叫数，则其平均队长$$E[N]$$和方差$$Var[N]$$同为a

系统通过的呼叫量为被占用的平均中继线数

通过的呼叫量为$$a'=\sum_{k=1}^{s}=a[1-B(s,a)]$$

<img src="../images/Network_Theory/callamount.png" width="60%"/>

每条中继线平均承载的呼叫量为$$\eta=\eta_s=\frac{a'}{s}$$

#### 大群化效应

在同样时间阻塞率下，分散的中继线群承载的总呼叫量小于中继线集中后承载的呼叫量。

### 三、Erlang等待制系统

系统有s条中继线，如果呼叫到来时系统中没有空闲的中继线，该呼叫不被拒绝而是等待。

- 计算稳态分布
- 计算一个呼叫到来时需要等待的概率
- 等待时间的分布、均值

<img src="../images/Network_Theory/wait.png" width="60%"/>

#### 计算稳态分布

设$$p_k$$为稳态分布，$$a=\frac{\lambda}{\mu}$$，则

$$\begin{equation}
p_k=\left\{\begin{aligned}
\frac{a^k}{k!}p_0 & , & 0\leq k <s\\
\frac{a^k}{s!s^{k-s}}p_0 & , & k\geq s
\end{aligned}
\right.
\end{equation}$$

根据概率归一性

$$\frac{1}{p_0}=\sum_{k=0}^{s-1}\frac{a^k}{k!}+\frac{a^s}{s!}\sum_{k=s}^{\infty}(\frac{a}{s})^{k-s}$$

在$$a<s$$时，该系统有稳态，且

$$p_0=\frac{1}{\sum_{k=0}^{s-1}\frac{a^k}{k!}+\frac{a^s}{s!}\frac{1}{1-\frac{a}{s}}}$$

#### 计算等待概率

设w为呼叫需要等待的时间

$$p(w>0)\\=\sum_{k=s}^{\infty}p_k=\frac{a^s}{s!}p_0\sum_{k=s}^{\infty}(\frac{a}{s})^k\\=\frac{a^s}{s!}\frac{p_0}{1-\frac{a}{s}} , a<s$$

上式为$$C(s,a)=\frac{a^s}{s!}\frac{p_0}{1-\frac{a}{s}}$$, **Erlang-C公式**

该公式用来计算一个呼叫需要等待的概率

#### 等待时间的分布、均值

**均值**
平均呼叫数：$$E[N]=\frac{\rho}{1-\rho}C(s,a)+a$$
其中$$\rho=\frac{a}{s}$$
根据Little公式：$$N=\lambda T$$
得：$$E[w]=E[N]/\lambda = \frac{C(s,a)}{s\mu -\lambda}$$

**分布**
$$p_k\{w>t\}$$表示呼叫到达时系统中有k个顾客的情况下等待时间的概率。
$$p\{w>t\}=C(s,a)e^{-(s\mu - \lambda )t}$$

### 四、一般混合制的MMs系统

系统中有s个服务员，系统容量为n。到达的呼叫流为参数$$\lambda$$的Poisson过程，服务时间服从参数为$$\mu$$的负指数分布。

<img src="../images/Network_Theory/mmsn.png" width="60%"/>

#### 稳态分布

根据极限定理：

$$\begin{equation}
p_k=\left\{\begin{aligned}
\frac{a^k}{k!}p_0 & , & 0\leq k <s\\
\frac{a^k}{s!s^{k-s}}p_0 & , & s\leq k \leq n
\end{aligned}
\right.
\end{equation}$$

根据概率归一性：

$$\frac{1}{p_0}=\sum_{k=0}^{s-1}\frac{a^k}{k!}+\frac{a^s}{s!}\frac{s}{s-a}[1-(\frac{a}{s})^{n-s+1}]$$

#### 时间阻塞率

呼叫需要等待的概率：

$$p\{w>0\}=C_n(s,a)=\sum_{k=s}^{n}p_k=\frac{a^s}{s!}\frac{s}{s-a}[1-(\frac{a}{s})^{n-s+1}]p_0$$

时间阻塞率为：

$$p_n=B_n(s,a)=\frac{a^n}{s!s^{n-s}}p_0$$

## 第四章 通信网性能分析

### 一、介绍

1. Erlang公式可以计算局部呼损，但在以下情况不适用：

	- 交换机的中继线群不是全利用度
	- 用户数目有限
	- 大量重复呼叫流
	- 大量迂回呼叫流

2. 本章主要计算网络平均呼损和网络平均时延

### 二、重复呼叫流

重复呼叫流一般不是Poisson流，但是可以近似为Poisson流

原始呼叫流为$$a$$，由于重复呼叫增加的呼叫量为$$\Delta a$$，总呼叫量为$$a_R$$

$$a_R=a+\Delta a$$

被拒绝的呼叫量为$$a_RB(s,a_R)$$

设$$\rho$$为$$\Delta a$$占被拒绝的呼叫量的比例。

则：$$a_R=a+\rho a_RB(s,a_R)$$

根据该公式可以迭代求出$$a_R$$

### 三、溢出呼叫流

网络中端点有两条路由，第二条路由承载第一路由上溢出的呼叫流。

溢出呼叫流不是Poisson过程。

#### 溢出呼叫流的统计特征

溢出呼叫流的统计特征：

均值$$\alpha=aB(s,a)$$，方差$$\nu=\alpha(1-\alpha+\frac{a}{s+1+\alpha-a})$$

峰值因子：$$z=\frac{\nu}{\alpha}$$

#### 溢出呼叫流呼损的近似计算方法

1. 计算$$z=\frac{\nu}{\alpha}$$

2. 令$$a=\nu+3z(z-1),s=\frac{a(\alpha+z)}{\alpha+z-1}-\alpha-1$$

3. s向下取整

4. 重新计算$$a=\frac{(s+\alpha+1)(\alpha+z-1)}{\alpha+z}$$

5. 呼损为$$B(s+c,a)$$

### 四、电话网络平均呼损的计算

#### 多边转接

$$p_{AB}=1-\prod_{i=1}^{n}(1-p_i)$$

#### 多路迂回

$$p_{AB}=\prod_{i=1}^{n}p_i$$

### 五、数据网络的平均时延

平均系统时间：

$$T=\frac{1}{\frac{c}{b}-\lambda}$$

c为线路速率，b为平均包长，$$\lambda$$为到达率