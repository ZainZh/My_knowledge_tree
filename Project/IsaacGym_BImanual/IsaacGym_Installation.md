# IsaacGym安装与简单使用



IsaacGym 是一个通过端到端GPU加速提供强化学习计算的平台。通过将模拟与计算过程转移到GPU上，跳过了CPU的应用瓶颈。大大提高了计算与训练速度。同时官网表明未来会支持Omniverse，有着广阔的应用前景。

关于IsaacGym原理的论文，有兴趣的小伙伴们可以看：

> https://arxiv.org/pdf/2108.10470.pdf

[TOC]



## Installation

### 配置要求



> Ubuntu 18.04, or 20.04.
> Python 3.6, 3.7, or 3.8
> Minimum recommended NVIDIA driver version: 470.74 (470 or above required)
> Minimum required hardware: NVIDIA Pascal or later GPU with at least 8gb of VRAM

推荐使用anaconda创建对应环境，免配置乱七八糟的。

> https://www.anaconda.com/products/distribution

配置环境命令：`conda create -n (your env name) python==3.8` 

### 官方网站

> https://developer.nvidia.com/isaac-gym

1.虽然是免费软件，但是也要加入Nvidia会员，点击页面中间Member area进行注册下载。

<img src="pics/截屏2022-07-05 下午9.47.21 (2).png" alt="截屏2022-07-05 下午9.47.21 (2)" style="zoom:50%;" />

2.进入后点击绿色下载按钮进行下载。

<img src="pics/截屏2022-07-05 下午9.49.18 (2).png" alt="截屏2022-07-05 下午9.49.18 (2)" style="zoom:50%;" />

3. 安装PyTorch (https://pytorch.org/get-started/locally/)

   进入你刚刚通过anaconda创建好的环境后在这个环境下安装。环境隔离的好处是可以让你把你每个月project所需要的包与环境隔离开不至于冲突。不然有的要求python3.8 有的要求3.7。来来回回卸载安装并不现实。

   > conda activate <your env name>
   >
   > ```
   > conda install pytorch torchvision torchaudio -c pytorch
   > ```

4. 安装isaacgym

   进入到你下载的文件夹

   > cd ./isaacgym/python
   >
   > pip install -e.

5. 测试安装

   进入/isaacgym/python/examples 文件夹。

   > cd examples && python ant.py num_envs=9

​		如果出来一堆小蚂蚁的界面。 恭喜你安装成功。

6. 安装强化学习范例

   在preview3中，IsaacGym的官方将原本集成在安装包中的强化学习实例删除了，取而代之的是一个新的仓库，有需要的要单独安装。examples里的只是一些利用了Gym模拟器搭建的小任务。

   仓库地址：https://github.com/NVIDIA-Omniverse/IsaacGymEnvs

   将仓库克隆到IsaacGym路径下

   > git clone https://github.com/NVIDIA-Omniverse/IsaacGymEnvs
   >
   > pip install -e.

   同样的，安装好后

   > python train.py task=FrankaCabinet headless=False num_envs=9

​	   如果能看到9个机械臂在训练拉柜子的画面，congrats!

 7. 开发文档

    因为还没正式发布？所以文档是在下载的IsaacGym文件夹里，路径是：

    > isaac/isaacgym/docs/api/python/gym_py.html

## 优秀IsaacGym项目

> legged_arm:[leggedrobotics/legged_gym: Isaac Gym Environments for Legged Robots (github.com)](https://github.com/leggedrobotics/legged_gym)
>
> Scooter control :https://github.com/guichristmann/thormang3-gogoro-PPO
>
> DexterousHands: https://github.com/ZainZh/DexterousHands

当然我自己也有在做一个基于双臂强化学习的项目，不过因为项目还没做完，论文还没发完，code就先不开源了。占个坑，等做好了来分享。

## 官方论坛

> https://forums.developer.nvidia.com/c/agx-autonomous-machines/isaac/isaac-gym/322

论坛里很多大神，开发者也会经常回复大家的问题，pretty cool。
