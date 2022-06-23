# Deep Residual Learning for Image Recognition

> paper link: https://openaccess.thecvf.com/content_cvpr_2016/papers/He_Deep_Residual_Learning_CVPR_2016_paper.pdf

- 研究摘要

- 研究问题

- 相关工作缺陷

- 解决办法

- 其他相关文献

- 疑问点

  ## 研究摘要

  在深度神经网络的训练中，网络深度的增加会使得训练结果的误差增大，本文通过提出一种利用残差训练的方式来提高训练的精度，使得模型的优化更加容易，准确。同时复杂度也没有提高很多。

  

  ## 研究问题

  深度卷积网络为图像分类领域带来了一系列突破，而同时最近的证据表明神经网络的的层数深度十分重要，越深的网络层数可以处理更复杂的模型。但是在网络层数的加深过程中，出现了一个退化问题，Vanishing/exploding gradients 在从一开始就阻止了收敛。而同时，更深的层会导致更高的训练误差。图一显示了这个问题，更高的层数得到了更大的训练误差。

  

  ![image-20220623162157623](E:\其他文件\Documents\Desktop\work at cuhk\Read-more-papers\paper\Image Processing\Resnet\pics\image-20220623162157623.png)

  ​             																	             图一

  所以，在本文中提出了一个深度残差学习框架来解决该问题，`F(x)=H(x)-x`,在原来任务引入`H(x)`进入下一层的基础上改进为引入`H(x)`进入下一个weight layer后优化输出再进入下一weight layer，同时与本体`x`相加。 （need to improve later）

  ![image-20220623163808593](E:\其他文件\Documents\Desktop\work at cuhk\Read-more-papers\paper\Image Processing\Resnet\pics\image-20220623163808593.png)

  这样做有两个好处：

  - 残差与本体相比数据量与复杂度降低了很多，对于神经网络来说很容易优化。而将本体简单的丢入训练网络中会得到很高的训练误差。
  - 这个残差深度网可以很容易的在网络深度的增加中获得精度，产生的结果会大大优于以前的网络。

  这个网络在许多比赛中都获得了很好的训练效果，表明了方法的有效性。

  

  ## 相关工作缺陷

  ### 残差

  ### 短路连接

  
