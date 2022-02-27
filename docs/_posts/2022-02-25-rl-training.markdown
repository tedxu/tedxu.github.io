---
layout: post
title: 训练强化学习模型
date: '2022-02-25 19:52:16 +0800'
categories: 'reinforcement learning' 
published: true
---

# 参考来源

[1] Barto, R. S. S. A. G. (2013). Reinforcement Learning - An Introduction. In *The MIT Press* (Vol. 84). 

[2] Slivkins, A. (2019). Introduction to Multi-Armed Bandits. *Foundations and Trends® in Machine Learning*, *12*(1–2), 1–286.

[3] Mnih, V., Kavukcuoglu, K., Silver, D., Rusu, A. A., Veness, J., Bellemare, M. G., … Hassabis, D. (2015). Human-level control through deep reinforcement learning. *Nature*, *518*(7540), 529–533.

# 强化学习

强化学习是这样一种机器学习，它定义了 “智能体 - 环境” 这样一个问题抽象，通过智能体对环境的交互来学习其交互本身。它学习的是一种 “决策”，而不是某种 “输入- 输出” 关联 （就像大部分统计学习做的那样）。

一部分关联研究针对 “多连杆赌博机（Multi-Armed Bandits，或 MAB）问题”，形成了很多深入的研究成果[2]。MAB 主要关注在统计学角度寻求问题的解析解。另一个方向是研究各种算法获取问题的数值解。

我们通常讨论的 “训练” 是数值解的范畴。数值解的方法使用马尔可夫过程作为其数学模型，从贝尔曼等式可得

$$ \begin{align} v_\pi(s) &= \mathbb E_\pi [G_t | S_t = s]\\ &= \mathbb E_\pi [\sum_{k=0}^\infty \gamma^k R_{t+k+1} | S_t = s] \\ &= \mathbb E_\pi [R_{t+1 + } \gamma\sum_{k=0}^\infty \gamma^k R_{t+k+2} | S_t = s] \\ &= \sum_a \pi(a | s) \sum_{s', r} p(s',r | s, a) (r + \gamma v_\pi (s')) \\ \end{align} $$

状态 $s$ 的价值 $v$ 可以从其后继状态 $s'$ 迭代计算出来。在一个强化学习问题中，状态价值 $v$ 和策略 $\pi$ 都是未知的，确定两个其一即可用于决策（选择价值高的行动，或者策略决定的更高概率的行动）。强化学习的算法因此分为3种：

1. 值方法（Value based methods）学习价值函数，典型的值方法是 Q-learning。
2. 策略方法（Policy based methods）学习策略，典型的策略方法是 Policy gradient。
3. 行动-评论方法（Actor-critic methods）同时学习价值函数和策略，典型的方法是 A2C、DDPG。

# 强化学习训练是很难的

尽管有各种各样的学习算法，强化学习训练在当前仍然是很难的。

第一个难点是对人的挑战，强化学习区别于深度学习，训练的规模、问题定位方法、解决问题的节奏和传统的机器学习方法有很大不同。[Lessons Learned Reproducing a Deep Reinforcement Learning Paper](http://amid.fish/reproducing-deep-rl?fbclid=IwAR1VPZm3FSTrV8BZ4UdFc2ExZy0olusmaewmloTPhpA4QOnHKRI2LLOz3mM) 这篇文章描述了强化学习在工程实践上的体验。一个体验是因为其递归特性，某些小问题会被迅速放大，导致没有结果；另一个体验是，特别针对深度强化学习，当前需要大量训练数据，花费大量金钱和时间，才有可能产出有意义的模型。因此，强化学习训练要求工程师想得更多，而不是试得更多。而 [Deep Reinforcement Learning Doesn't Work Yet](https://www.alexirpan.com/2018/02/14/rl-hard.html) 这篇雄文则对深度强化学习整体都抱悲观态度。

第二个难点来自于强化学习模型本身。因为行为（action）带来的奖励（reward）不是同时发生的，可能会经历较长的一段时间间隔，这带来两个问题：i）每个行为对应的奖励方差大，造成结果不稳定，ii）需要足够好的训练数据，考虑到很多场景是无策略（Off-policy）的训练，这意味着需要大量训练数据。[部分实验](http://amid.fish/reproducing-deep-rl?fbclid=IwAR1VPZm3FSTrV8BZ4UdFc2ExZy0olusmaewmloTPhpA4QOnHKRI2LLOz3mM)表明，使用 DQN 训练[弹球游戏](https://gym.openai.com/envs/Pong-v0/)到一般玩家水平就要花上数天，这仅仅包含训练程序运行的时间。

# DQN

DQN 是引爆当代强化学习热潮的一个重要算法。它基本上是一个 Q-learning，区别在于使用深度网络来学习 Q-function。DQN 那篇著名的论文[3]以 Atari 游戏为例，使用相同的算法在大部分游戏中都获得了等价于资深玩家的水平，而用于学习 Q-function 的输入仅仅是一幅幅游戏图像。

以 Atari 游戏作为用例，事实上是巧妙的选择，这有两个好处：

1. 区别于围棋之类的博弈，Atari 游戏的状态（游戏图像）空间非常大，很难应用过去简单的算法。深度网络在 CV 上的成功是很好的结合点。
2. Atari 可以编写程序自动运行，而不像其他博弈通常需要人为参与，或需要相当长时间，这可以让 DQN 获取大量训练数据。

双向 DQN （DDQN）（Van Hasselt, H., Guez, A., & Silver, D. (2016). Deep reinforcement learning with double Q-Learning. *30th AAAI Conference on Artificial Intelligence, AAAI 2016*.）是 DQN 的一个变种，用于优化 DQN 估计的 Q value 偏大的情况。

DQN 在实践中不是常用的算法，一年后名声大噪的 AlphaGo 并没有使用 DQN，它使用的是 Policy Gradient。

# Policy Gradient

tbd

# 上手强化学习训练

[Gym](https://gym.openai.com/) 是 [OpenAI](https://www.openai.com/) 的一个强化学习库，它定义了 “智能体 - 环境” 互动的框架，附带了多个典型的机器学习案例，包括 Cartpole、Atari 游戏等。

[Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/#) 则是构建在 Gym 上的一套强化学习算法集合。