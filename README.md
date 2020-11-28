# Notes for RL Video Lectures
## Catalog
- [周博磊老师的视频课程](#Bolei_Zhou)
- [RLChina的视频课程](#RLChina)
- [论文阅读笔记](#./papers/README.md)

## Overview for Each Course
### Bolei_Zhou
周博磊老师的视频课程，我将其定位为：
- 中规中矩、系统的`深度强化学习`入门课程；
- 与强化学习圣经书 Introduction 同，其也是从马尔可夫决策过程与 `value-based(DQN)` 入手，但弥补了圣经书中`深度强化学习`与`近年来成果`的缺失；
- 关于 SOTA 的两条发展线，见下表；
- 在 SOTA 的内容后，讲解了`基于模型的强化学习`、`模仿学习`和`大规模强化学习（分布式系统）`，算是科普了；
- 没有关于 MARL 多智能体的内容。

此外，`周老师所汇总的资源极其优质`，课程中会提及经典论文对应的代码库、基础概念的 web-demo 等。因此，我打算二刷，并且将重点集中在实践上。

课程目录见 [link](#Zhou-Readme) ，我的笔记见 [notes](./notes/README.md) 。

### RLChina
华人强化学习顶尖学者社区 RLChina 举办的公益活动，质量很高，且将注意力集中在了`弥补 MARL 这部分资料缺失的短板`，可以理解为各个先进领域的讲座：
- 除去开头的基础知识铺垫，包含：
  - 将推理模型应用于控制 Control as Inference ；
  - 模仿学习 Imitation Learning ；
  - 稀疏奖励下的强化学习 Learning with Sparse Rewards ；
  - 博弈论 Game Theory Basic ；
  - 多智能体系统 Multi-agent Systems 及 MARL 的扩展（共4节）。
- 多智能体部分，将在最后一部分介绍崭新的思路：使用物理中的 Mean-Field 理论，去研究大规模智能体控制。

2020年8月份的课程，很新，当时没有看直播（直播不能自己调节进度）。会在2020年12月份前完成课程笔记。

课程目录见 [link](./RLChina/notes/README.md) ，我的笔记见 [notes](./RLChina/notes/README.md) 。

# Zhou-Readme
![teaser](asset/teaser.png)
## Overview
This short RL course introduces the basic knowledge of reinforcement learning. Slides are made in English and lectures are given by [Bolei Zhou](http://bzhou.ie.cuhk.edu.hk/) in Mandarin. The course is for personal educational use only. Please open an issue if you spot some typos or errors in the slides. 

## Course Schedule
The course is scheduled as follows. There are 10 lectures in total, where the first one was premiered on 16 March 2020 and the last one was finished on 25 May 2020. Thanks for watching and may ReinForce be with you!

|            	  | Topic                                      	  | Resources |
|--------------	|----------------------------------------------	|----------	|
|  Lecture1 	| Overview (课程概括与RL基础)                                   	|[slide](lecture1.pdf), Youtube([part1](https://www.youtube.com/watch?v=IkEF4LpH5Ys), [part2](https://www.youtube.com/watch?v=Qu8CPnnwplM)), B站([上集](https://www.bilibili.com/video/BV1LE411G7Xj/), [下集](https://www.bilibili.com/video/BV1g7411Z7SJ/))  |
|  Lecture2 	| Markov Decision Process (马尔科夫决策过程)                    	| [slide](lecture2.pdf), Youtube([part1](https://www.youtube.com/watch?v=6yE9XiIB3hQ), [part2](https://www.youtube.com/watch?v=MIZbocCu7Sk)), B站([上集](https://www.bilibili.com/video/BV1g7411m7Ms/), [下集](https://www.bilibili.com/video/BV1u7411m7rh/)) |
|  Lecture3 	| Model-free Prediction and Control (无模型的预测和控制)          	|  [slide](lecture3.pdf), Youtube([part1](https://www.youtube.com/watch?v=Duj1U73yHik), [part2](https://www.youtube.com/watch?v=sfkhinBjGGY)), B站([上集](https://www.bilibili.com/video/BV1N7411Q7aJ/), [下集](https://www.bilibili.com/video/BV1N7411Q7M6/)) |
|  Lecture4 	| Value Function Approximation (价值函数近似)               	|[slide](lecture4.pdf), Youtube([part1](https://www.youtube.com/watch?v=YdWsnB-u8PQ), [part2](https://www.youtube.com/watch?v=fGIaFlbBFxk)), B站([上集](https://www.bilibili.com/video/BV11V411f7bi/), [下集](https://www.bilibili.com/video/BV1w54y1d7se/))  |
|  Lecture5 	| Policy Optimization: Foundation (策略优化基础篇)             |[slide](lecture5.pdf), Youtube([part1](https://www.youtube.com/watch?v=ProKaoyduFY), [part2](https://www.youtube.com/watch?v=MWXazkQkTlk)), B站([上集](https://www.bilibili.com/video/BV1fZ4y1x7mp/), [下集](https://www.bilibili.com/video/BV1ia4y1x7Va/))            	|
|  Lecture6 	| Policy Optimization: State of the art (策略优化进阶篇)      	|[slide](lecture6.pdf), Youtube([part1](https://youtu.be/4YIdjLh-MJs), [part2](https://youtu.be/HOpiQWM0PCA)), B站([上集](https://www.bilibili.com/video/BV1s64y1M7AW/), [下集](https://www.bilibili.com/video/BV1EK41157fD/))  |
|  Lecture7 	| Model-based RL (基于环境模型的RL)                             	|[slide](lecture7.pdf), [Youtube](https://youtu.be/2Cy8ZX16pBU), [B站](https://www.bilibili.com/video/BV1hV411d7Sg/)|
|  Lecture8 	| Imitation Learning (模仿学习)                         	|[slide](lecture8.pdf), [Youtube](https://youtu.be/Sqvn6RxU8qk), [B站](https://www.bilibili.com/video/BV17k4y1k7Gu/)           	|
| Lecture9 	| Distributed systems for RL (分布式系统) 	|[slide](lecture9.pdf), [Youtube](https://youtu.be/PyHGeFFfaWk), [B站](https://www.bilibili.com/video/BV1bi4y147Rv/)           	|
| Lecture10 	| RL in a nutshell (课程结局篇)|[slide](lecture10.pdf), [Youtube](https://youtu.be/bDGmKVKAdHg), [B站](https://www.bilibili.com/video/BV1si4y1s7oQ/)           	|
| Bonus 1 	| DeepMind's AlphaStar Explained (剖析星际争霸AI) by [Zhenghao Peng](https://github.com/pengzhenghao)|[slide](lecture_alphastar.pdf), [Youtube](https://youtu.be/5qp0VNC_iOc), [B站](https://www.bilibili.com/video/BV1wa4y1e74G/)           	|
