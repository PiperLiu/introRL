# RL论文阅读
书写一些 RL 基础理论方面的论文阅读心得。

## 目录
- [分层强化学习hierarchical-RL](#hierarchical-RL)

## hierarchical-RL
目录：
- Feudal Reinforcement Learning, 1993 [概括](#hierar_1) [笔记](./notes/Feudal_Reinforcement_Learning.md)

参考资料：
- [分层强化学习survey](https://zhuanlan.zhihu.com/p/267524544)
- [YangShengqi：保存一些自己看过的论文](https://github.com/YangShengqi/paper/tree/master/Reinforcement%20Learning/hierarchical)

### Feudal Reinforcement Learning, 1993
<a id='hierar_1'></a>
DAYAN P, HINTON G, 1993. Feudal Reinforcement Learning[J/OL]. Advances in neural information processing systems, : 271–278. http://www.cs.utoronto.ca/~hinton/absps/dh93.pdf.

1992年没有深度学习，人们研究RL的思路与现在并不相同。但不可否认，提出“分层强化学习”是解决“泛化、学习速度”等问题的一个很好的思路。

Feudal 类似从宏观到微观地去分层指挥，这里有一点值得注意，那就是“层层封装”，A-B-C，C只去执行B给他下达的目标（或者说感受以此设计的奖励机制），而不去管A的；此外，对于接收的信息也是这样，C看不到A的信息。

这符合人的决策过程：比如打篮球，我的战略（第一层）是一对一盯防；接着我便执行这个“战略”：对位的对手是一个投手，因此我执行的微观策略（第二层）是贴近他防守，干扰他跑位、接球、投篮；至于具体如何做，那一半都是下意识和我的体能、技术所决定的（第三层），比如防守动作、跟着跑的临场判断等。

作者说，对于强化学习来讲，这种学习方式无疑更高：可能开始训练时，会有从低向上的影响，但是之后，便会是从上至下的指挥，毕竟上层动作少（可以理解为，宏观策略就那么几个），且起到决定性作用。

那么，这对现在的RL有什么启发吗？
- 目前我觉得启发不大，因为我们有 n-step 自举更好地回溯到达重点的影响 和 Deep Learning 的泛化；
- 此外，我认为如何设计宏观目标的“指挥”是一个超级难点。原因如下。

比如自动驾驶，现在的宏观层面的动作是超车，那么对于执行层面，怎样才算超车呢？超车之后，奖励值是多少呢？为了超车而与别的车刮碰，这个怎么算奖励值呢？“超车”这个宏观目标选定的不合理，根本没有办法完成，对于执行层面的奖励机制该如何设置呢？

