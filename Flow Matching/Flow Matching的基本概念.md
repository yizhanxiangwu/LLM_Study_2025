# Flow Matching 基本概念

## 1. 什么是 Flow Matching

Flow matching 是一种用于概率生成建模的新策略，主要用于高效训练生成型模型。其核心思想是直接匹配概率流（probability flow）的轨迹，而不是间接地最小化分布之间的距离（比如扩散模型中的 KL 散度）。

### 简单理解
与其让模型去"猜"如何将噪声变成目标数据，不如直接教会模型怎样从起点"流"向终点。

## 2. Flow Matching 与扩散模型有何区别？
* 扩散模型（Diffusion Model）
通过多步添加和去除噪声，把简单分布（如高斯噪声）映射为复杂数据分布。
训练过程通常通过最小化某种基于 KL 散度的损失。
* Flow Matching
直接拟合样本间的概率流（ODE路径），避免多次采样和复杂的反向推断。
理论基础来自概率连续流和 score-based 建模。
### 主要区别：
扩散模型通常需要大规模迭代采样；flow matching 强调端到端地学习流；
Flow matching 采样速度更快、理论更简洁。

## 思考与笔记

> **基本概念**
> 1. 生成模型
> 2. KL 散度 
> 3. ODE路径 
> 4. 概率连续流/score-based 模型

> **我的思考**
> 1. Flow Matching 看起来像是扩散模型的"简化版"，但实际效果可能更好？
> 2. 直接学习流轨迹 vs 间接最小化分布距离，这个思路很有意思
> 3. 需要进一步了解概率流（probability flow）的具体数学定义
> 4. 在 RAG 系统中，Flow Matching 如何帮助改进检索和生成过程？

> **待解决的问题：**
> - [ ] 概率流的数学定义和性质
> - [ ] Flow Matching 在文本生成中的具体应用
> - [ ] 与 Mamba 架构的结合方式
> - [ ] 在多模态场景下的表现

## 3. 数学框架与核心公式

### （1）ODE 形式建模概率流
用 ODE 形式建模概率流：  
$$\frac{d\mathbf{x}_t}{dt} = f_\theta(\mathbf{x}_t, t)$$

### （2）"流"即概率连续流（Probability Flow ODE）
若用 $q(x_t \mid x_0)$ 来描述数据从起点（如高斯噪声）到真实数据的路径，
则概率流满足如下 ODE：

$$\frac{dx_t}{dt} = f_\theta(x_t, t)$$

这里 $f_\theta$ 是我们要学习的神经网络。

### （3）Flow Matching 损失函数
Flow matching 提出的损失通常为：

$$\mathcal{L}_{FM} = \mathbb{E}\left[\| f_\theta(x_t, t) - \frac{dx_t}{dt} \|^2\right]$$

也就是说，模型学习去"模仿"真实样本流动的行为。

## 4. 推荐资源

- 论文: [Flow Matching for Generative Modeling](https://arxiv.org/abs/2306.00379)
- 代码: [官方GitHub](https://github.com/atong01/flow_matching)

## 5. 建议学习顺序

1. 学习生成建模基础（如GAN/扩散模型）
2. 快速阅读 Flow Matching 论文
3. 推导关键公式
4. 跑通官方代码demo
5. 对比扩散模型理解优劣
6. 深入进阶和实操实验 