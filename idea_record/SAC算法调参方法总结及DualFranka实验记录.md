# SAC算法调参方法总结及DualFranka实验记录
最近在isaacgym中训练一个off-policy的franka机械臂抓取任务时遇到了一点困难。在Nvidia3090显卡下，默认参数训练的结果又慢又差![Image](https://pic4.zhimg.com/80/v2-143e52ce88a47efaebe5245edbf729c6.png)
可以看到在默认参数下训练了十个小时后才开始涨起，而且训练到max_epoch后也没能收敛。所以写一下网上看到的SAC调参方法，并顺便做一个实验记录吧。
- [SAC算法调参方法总结及DualFranka实验记录](#sac算法调参方法总结及dualfranka实验记录)
  - [影响SAC算法的训练参数](#影响sac算法的训练参数)
    - [通用参数](#通用参数)
    - [特有参数](#特有参数)
  - [默认参数训练轮](#默认参数训练轮)
    - [参数](#参数)
    - [结果](#结果)
  - [第一训练轮](#第一训练轮)
    - [参数](#参数-1)
    - [结果](#结果-1)
  - [第二训练轮](#第二训练轮)
    - [参数](#参数-2)
    - [结果](#结果-2)
  - [参考链接](#参考链接)

## 影响SAC算法的训练参数
### 通用参数
1. gamma因子（$\gamma$）
   $\gamma$因子在算法中起到的作用是描述智能体在训练过程中所需要考虑的步长。$\gamma$取0表示完全不考虑未来对现在的影响。而当$\gamma$取为1时表现为无穷远的未来表现也会影响到现在的奖励。这两种显然都是不合理的。
   通常$\gamma$的选取方法遵循以下经验公式。
   $$
   \gamma=0.1^{1/t_{len}}
   $$
   $t_{len}$表示为你希望考虑的步数。通常$\gamma$取0.95-0.99。
2. batch size
   batch size就是批次大小。一般选择网络宽度相同或者略大。本实验中网络宽度为256，选择batch size从$2^{10}$ 到 $2^{12}$之间。
3. replay buffer size.
   在off-policy中，replaybuffer被用来存储旧有样本。过小会导致过去经验吸取不足，过大会造成训练过慢。推荐参数$10^5$ 到 $10^{6}$。
### 特有参数
1. actor learning rate
   网络参数的学习率（actor）一般取e^-4到e^-5之间
2. critic learning rate
    同上
3. alpha learning rate
   温度系数学习率一般要和网络参数的学习率保持一致
4. target entropy coef
   目标墒系数。关于这个系数有个经验公式
   $$
   target_{entropy}  = -log(action.shape)
   $$
   因为在本次任务在，action的尺寸大小为18，经过计算target entropy为-1.5
   而在rl-games的code中
   $$
   target_{entrop}y=targetentropycoef*（-action.shape）
   $$
   target entropy coef近似取0.1
5. reward scale
    一般要保证奖励落在-1000到1000中，取0.05
6. network
   选取的默认，如何选取还要研究，有Relu和elu两种。
## 默认参数训练轮
### 参数
|  参数名 | 数值 |
|---|---|
| gamma | 0.99 |
| batch size |1024  |
|  replaybuffer size|1e5  |
| actor learning rate |3e-5  |
|  critic learning rate| 3e-4 |
| alpha learning rate | 3e-4 |
| target entropy coef | 0.5|
| reward scale|1.0|
|activate|elu|
|layer|[256,128,64]|
### 结果
|  结果 | 描述 |
|---|---|
| 结果 | fail |
| training time |20h  |
|  reward|2e-4  |
| 收敛时间 |12h  |
![Image](https://pic4.zhimg.com/80/v2-143e52ce88a47efaebe5245edbf729c6.png)

## 第一训练轮
### 参数
|  参数名 | 数值 |
|---|---|
| gamma | 0.95 |
| batch size |2048  |
|  replaybuffer size|2^18 |
| actor learning rate |3e-5  |
|  critic learning rate| 3e-4 |
| alpha learning rate | 3e-4 |
| target entropy coef | 0.1|
| reward scale|0.05|
|activate|elu|
|layer|[256,128,64]|
### 结果
|  结果 | 描述 |
|---|---|
| 结果 |  |

## 第二训练轮
### 参数
|  参数名 | 数值 |
|---|---|
| gamma | 0.96 |
| batch size |2048  |
|  replaybuffer size|10^6 |
| actor learning rate |5e-4  |
|  critic learning rate| 5e-4 |
| alpha learning rate | 5e-3 |
| target entropy coef | 0.1|
| reward scale|0.05|
|activate|Relu|
|layer|[256,128,64]|
### 结果
|  结果 | 描述 |
|---|---|
| 结果 |  |

## 参考链接
曾伊言：
> https://zhuanlan.zhihu.com/p/345353294

雨泽：
> https://zhuanlan.zhihu.com/p/434495366