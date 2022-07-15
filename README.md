## Audio-visual nvigation

| Name          | pdf                                                          | github                                           | description                                                  |
| ------------- | :----------------------------------------------------------- | :----------------------------------------------- | ------------------------------------------------------------ |
| soundspaces   | [**SoundSpaces: Audio-Visual Navigation in 3D Environments**](https://scontent-hkg4-2.xx.fbcdn.net/v/t39.8562-6/10000000_225707052822142_3554026592703488763_n.pdf?_nc_cat=100&ccb=1-7&_nc_sid=ad8a9d&_nc_ohc=IycUF2sAw5kAX_fXrtY&_nc_ht=scontent-hkg4-2.xx&oh=00_AT-0SXodwx2wCx_UrfeW8Tl-5abiG5LFjQzz_DJ0sr0DXA&oe=62D592BC) | https://github.com/facebookresearch/sound-spaces |                                                              |
| soundspaces2.0 | [**Soundspaces 2.0: A Simulation Platform for Visual-Acoustic Learning**](https://arxiv.org/pdf/2206.08312.pdf) | https://github.com/facebookresearch/sound-spaces |                                                              |
|               | [**Few-Shot Audio-Visual Learning of Environment Acoustics**](https://arxiv.org/pdf/2206.04006.pdf) |                                                  | RIR prediction.Infer arbitrary RIRs having observed only a small number of echoes and images in the space. |

## Relate task

| Name                                       | pdf                                                          | github | description                                                  |
| ------------------------------------------ | ------------------------------------------------------------ | ------ | ------------------------------------------------------------ |
| Audio-Aware Mobile Robot Navigation（SIM） | [**Learning to Listen and Move: An Implementation of Audio-Aware Mobile Robot Navigation in Complex Indoor Environment**](https://github.com/yyf17/awesome-embodied-intelligent/blob/main/Learning_to_Listen_and_Move_An_Implementation_of_Audio-Aware_Mobile_Robot_Navigation_in_Complex_Indoor_Environment.pdf) |        | RTAB-Map for agent position,Separately training autoencoder(denoise)+SIM(get relative x,y),ROS navigation stack for global path planning. |





## SoundSpaces: Audio-Visual Navigation in 3D Environments

### Introduction

模拟机器人在真实世界里移动应该是一个多感官的体验，但是今天的这种embodied agent大多是没有听觉的，仅仅依靠视觉去感官去感受环境。本文创造了一种能够在复杂的视听觉环境下进行的视听导航，通过听和看，智能体agent可以移动到目标物体。并且提出了一种多模态的强化学习方法能够使智能体通过自主的视听观察实现导航，并且能够探测物体表面的几何特征意味着声音的反射。检测并且跟随声音源，也就是soundspaces数据集是第一个能够基于几何声学模拟器的产品，包含两个公开的数据集Matterport3D and Replica,我们使用了Habitat来支撑新的传感器使得在任何一组扫描得到的真实环境能够插入任意的声音源。实验结果显示声音能够大幅提高视觉的自主导航能力。

### Motivation

声音是帮助理解真实物理世界的关键，受到一些应用场景的启发(声纳，通过回声来推测物理表面等)，声音可以对视觉信息起到一个很好的辅助作用，另外，在导航任务中当目标体在视觉之外时，只能通过听觉来进行导航。可以想象出两类的导航任务场景,AudioGoal,AudioPointGoal

### Contributions

我们提出了一种多模态的RL方法，从视听观察流中端到端地训练导航策略。比较重要的一点是我们对于声音的观测必须包含agent的当前的位置以及角度信息以及当前的物理3D环境。为了做到这一点作者团队介绍了在Matterport3D和Replica下预计算的声音渲染Soundspaces，ra



## Learning to Listen and Move: An Implementation of Audio-Aware Mobile Robot Navigation in Complex Indoor Environment

### Introduction

提出的框架主要基于两点: 

声音推理模块（SIM），将感知到的声学信息映射到给定的物理空间几何地图。

路径规划器，生成从机器人当前位置到声源估计位置的路径。

现有的研究主要存在两点限制：

（1）机器人往往接收到很多叠加的声音，因此要求机器人必须能够从混合声音中复原出感兴趣的声音去抛弃无用的声音。

（2）使用真实的机器人来进行彻底的受控实验是一项非常大的挑战。因此使用模拟器和真实世界的实现存在一个较大的差异。

考虑到这些限制，我们想到使用DNNs对于audio-aware navigation task有建立起环境中的声学线索和地图中存在的几何学信息线索的能力。

这项任务主要分为两大关键步骤：

（1）声源定位SSL：难度在于复杂和多变的环境。传统的技术包含从声学信号中清晰的提取特征time-difference-of-arrival (TDOA) or inter-microphone intensity difference (IID)这些特征没能提供在嘈杂环境下足够的远处的声学信号表示信息。相反，现代的方法使用DNNs对于环境中的背景噪声以及回声具有较好的鲁棒性。

（2）路径规划

实验假定机器人知道环境地图并且他必须使用这个地图来估计他在环境中的姿势(?)，机器人被随机放置在一个位置并且录制声音信息。文章提出的架构处理声学信息并且定位声源。

最终由一个path planner来生成从当前位置到声音源的轨迹

### Contributions

（1）提出了一个Audio-Aware Navigation framework.提出的方法在物理系统上已经实现，在复杂的工业环境下得到验证并且和其他的baselines有显著的改善。

（2）提出了Sound Inference Module(SIM) for high resolution SSL.这个模块可以被任何具有SLAM（cameras,range lasers,sonar）能力的机器人使用。

(3)引入了一个能够评估可靠性的指标。通过声源定位错误以及路径长度来测量可靠性。

### RELATE WORK

**A.*Map-Based Navigation***

传统的方法需要借助复杂的传感器来生成地图，本文提出的框架给机器人提供了声学能力能够有效的对声音源头进行定位。

**B.*Audio-Visual Navigation in Unseen Environments***

最近在自主性的视听任务中的研究主要集中在结合声学和视觉线索达到在未见过的环境中进行导航的目的。Gan通过声音的输入来定位声音源头的位置和raw RGB来规划最优的路径。C hen 使用原始的视听输入来预测下一步的最优策略。另外，Chen 还提出了一种基于路径点的技术伴随着声学记忆来增强视听导航任务的表现。而且Chen还利用包含目标的空间和语义属性的目标的描述符介绍语义视听导航。这些研究确认了音频信息是一个强大的导航信息可以被智能的移动机器人进行自主导航。

**C.*Sound Source Localization (SSL)***

过去的声源定位集中于不同的信号处理方法，主要是直接估计终点的方向和距离来定位声音源头。比较普遍的技术包括beamforming,Generalized Cross- Correlation with Phase Transform (GCC-PHAT), Multiple Signal Classification (MUSIC),最近，深度学习方法被用来估计DoA(direction of arrival)。相反的，这篇文章中提出的方法能够在给定的参考图中定位到声源的绝对坐标。这个方案也可以结合SLAM（namely acousutic SLAM,aSLAM）,aSLAMaSLAM是一种用于定位移动麦克风阵列轨迹的技术，同时定位周围声源。本文提出的框架超越了这一点，因为机器人必须将感知到的声学信号与构建的环境几何地图联系起来，并规划最佳路径。

### AUDIO-AWARE NAVIGATION

**A.RTAB-Map**

RTAB-Map [23] is used to construct the 3-D structure of the environment. It utilizes a combination of the robot’s odometry and on-board depth camera to simultaneously generate a map, localize in it and plan paths. **The current position of the robot Im is obtained from RTAB-Map.**

**B.Feature Extraction**

sample rate: 16000

frame size: 1000 ms

stft:

​	fft size:1024

​    hop_length:512	

normalize to  [0,1]

get 256 x 256 complex-valued matrix

use auto-encoder to  extract low-dimensional feature embeddings from the audio spectrogram.

the structure of AE:

​	encoder: 

 		8 convolutional  layers,Leaky-Relu activation and BN

​    decoder: 

​		与 encoder 结构对称

  minimizes the MSE between original input normalized spectrogram and the reconstructed spectrogram.

**C.Sound INference Module(SIM)**

为了能够计算到声音源头的相对位置，使用欧几里得距离来训练SIM，SIM包含了四个全连接层，除了最后一层每个全连接层之后包含一个RELU,最后一个使用tanh

 The optimizer used is ADAM , with a learning rate of 1×10−3 and a batch size of 64. For better loss convergence, the ground truth relative positions are normalized to [−1,1]. 

### Conclusion

Enhancement module  is help for Audio-Aware Mobile Robot Navigation 



​	



