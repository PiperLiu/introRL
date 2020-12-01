# 1993年的分层强化学习：Feudal Reinforcement Learning
## 概括
1992年没有深度学习，人们研究RL的思路与现在并不相同。但不可否认，提出“分层强化学习”是解决“泛化、学习速度”等问题的一个很好的思路。

Feudal 类似从宏观到微观地去分层指挥，这里有一点值得注意，那就是“层层封装”，A-B-C，C只去执行B给他下达的目标（或者说感受以此设计的奖励机制），而不去管A的；此外，对于接收的信息也是这样，C看不到A的信息。

这符合人的决策过程：比如打篮球，我的战略（第一层）是一对一盯防；接着我便执行这个“战略”：对位的对手是一个投手，因此我执行的微观策略（第二层）是贴近他防守，干扰他跑位、接球、投篮；至于具体如何做，那一半都是下意识和我的体能、技术所决定的（第三层），比如防守动作、跟着跑的临场判断等。

作者说，对于强化学习来讲，这种学习方式无疑更高：可能开始训练时，会有从低向上的影响，但是之后，便会是从上至下的指挥，毕竟上层动作少（可以理解为，宏观策略就那么几个），且起到决定性作用。

那么，这对现在的RL有什么启发吗？
- 目前我觉得启发不大，因为我们有 n-step 自举更好地回溯到达重点的影响 和 Deep Learning 的泛化；
- 此外，我认为如何设计宏观目标的“指挥”是一个超级难点。原因如下。

比如自动驾驶，现在的宏观层面的动作是超车，那么对于执行层面，怎样才算超车呢？超车之后，奖励值是多少呢？为了超车而与别的车刮碰，这个怎么算奖励值呢？“超车”这个宏观目标选定的不合理，根本没有办法完成，对于执行层面的奖励机制该如何设置呢？

## 1 INTRODUCTION
1992年，强化学习面临的瓶颈：
- **时间上的限制** ：快速学习（那个年代的算力可想而知）
- **分解任务** ：找子任务，更容易学习（我怀疑，是那个年代没有深度学习，因此需要手动提取特征值，划分任务、简化任务）
- **探索** （在我看来，探索与利用的平衡是交互环境中学习绕不开的难点）
- **泛化** ：显而易见，表格型RL很难做到泛化

本文提出的分层强化学习，也是要解决这四个问题。

## 2 FEUDAL CONTROL
开头的两句话，我认为算是较为核心地概括了控制机制：We sought to build a system that mirrored the hierarchical aspects of a feudal fiefdom, since this is one extreme for models of control. Managers are given absolute power over their sub-managers – they can set them tasks and reward and punish them entirely as they see fit.

翻译：我们试图建立一个极端的控制模式，将参考封建封地那样的等级制度。（**我的理解：我的附庸的附庸，不是我的附庸？**）管理者对于其附庸有绝对的管理权力，他们可以为他们的附庸制定任务、奖励机制。

有两条原则：
- Reward Hiding
- Information Hiding

### Reward Hiding
层层封装。我的理解是：加入有三层A、B、C，那么C只去完成B为其设定的指标，不管A为B设定的指标。“我的附庸的附庸，不是我的附庸。”——来自中学历史教科书，讲述欧洲中世纪封建制度部分。

### Information Hiding
有限的信息。分层封装的不仅仅是奖励与目标，决策的信息也是。这样更类似社会中的决策机制。

原文：Information is hidden both downwards – sub-managers do not know the task the super-manager has set the manager – and upwards – a super-manager does not know what choices its manager has made to satisfy its command. However managers do need to know the satisfaction conditions for the tasks they set and some measure of the actual cost to the system for achieving them using the sub-managers and tasks it picked on any particular occasion.

翻译：信息被从上至下、从下至上地隐藏了起来。对于从上至下：下层管理者并不知道上层管理者给中层管理者设了什么任务；对于从下至上：上层管理者并不知道中层管理者具体做了什么。（**不管你怎么干，满足我要求就行**）然而，中层管理者必须要了解：如何满足其设置的任务、如满足其任务的条件、用下层管理者完成任务对系统的损耗的衡量办法。（tasks it picked on any particular occasion 我没有翻译）

## 3 THE MAZE TASK
使用 MAZE TASK 作为案例。

![](https://github.com/PiperLiu/introRL/blob/master/papers/notes/images/2020120101.png)

如上，“U”型代表屏障。3-(3,3)是目的地。

### 动作
所有智能体都有五个动作：
- 向东走一步
- 向西走一步
- 向南走一步
- 向北走一步
- 什么都不干

除了两个：
- 对于最高层的智能体，其动作只有：什么都不干
- 对于最低层的智能体，其动作只有：东南西北

### 状态
两个特征之
- 自己所处的地点（在本层的粒度中的地点）
- 上层的指令

### 奖励
（这是我个人的理解，不确认是正确的，欢迎私信我。因为通篇没用公式，并不知道具体是怎么迭代的）

当下层移动，造成本层的状态改变，我们更新本层的 Q 值。具体更新多少，根据本层的所走路径的长度来计算（具体怎么算？文章里没有说明。我怀疑就是把每层都是为一个单独的 Maze Task ，换个状态，就 -1）。**并且，只有当状态转换是尊重自己的意愿时，才进行 Q 值的更新。**

**因为我们之前设置了约束：上层管理者只能从下层管理者的劳动成果中获取学习经验。**

我的理解是，如果下层没听话，达到的目标不对，那上层这次动作就不算。

## 4 DISCUSSION
结果的图就不放了，自然是本文提出的方法比传统 Q-Learning （不分层）效率高。

为什么？作者说，对于强化学习来讲，这种学习方式无疑更高：可能开始训练时，会有从低向上的影响，但是之后，便会是从上至下的指挥，毕竟上层动作少（可以理解为，宏观策略就那么几个），且起到决定性作用。
