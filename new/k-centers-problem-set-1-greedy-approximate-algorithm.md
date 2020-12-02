# K 中心问题| 设置 1（贪婪近似算法）

> 原文： [https://www.geeksforgeeks.org/k-centers-problem-set-1-greedy-approximate-algorithm/](https://www.geeksforgeeks.org/k-centers-problem-set-1-greedy-approximate-algorithm/)

给定 n 个城市以及每对城市之间的距离，请选择 k 个城市来放置仓库（或 ATM 或 Cloud Server），以使城市到仓库（或 ATM 或 Cloud Server）的最大距离最小。

例如，考虑以下四个城市，分别为 0、1、2 和 3，以及它们之间的距离，如何在这四个城市之间放置 2 个 ATM，以使城市到 ATM 的最大距离最小。

![kcenters1](img/31fdca6e93489553fc51d0cb77097c54.png)

由于该问题是已知的 NP-Hard 问题，因此没有多项式时间解可用于该问题。 有一个多项式时间贪婪近似算法，贪婪算法提供的解决方案永远不会比最佳解决方案大两倍。 仅当城市之间的距离遵循[三角不等式](http://en.wikipedia.org/wiki/Triangle_inequality)（两个点之间的距离始终小于到第三点的距离之和）时，贪婪解决方案才有效。

**2-近似贪婪算法**：
1）任意选择第一个中心。

2）使用以下条件选择剩余的 k-1 个中心。
令 c1，c2，c3，... ci 为已选择的中心。 通过选择距已选择
的中心最远的城市（即点 p 的最大值为
的最大值）来选择
第（i + 1）个中心， dist（p，c2），dist（p，c3），…。 dist（p，ci）]

![greedyAlgo](img/3c36fed023d9cfc254e69c97f514ccc2.png)

**示例（在上图中的 k = 3）**
a）令第一个任意选择的顶点为 0。

b）下一个顶点是 1，因为 1 是距离 0 的最远顶点。

c）剩余的城市是 2 和 3。计算它们与已选择的中心的距离（0 和 1）。 贪婪算法基本上计算以下值。

从 2 到已经考虑的中心的所有距离中的最小值
Min [dist（2，0），dist（2，1）] = Min [7，8] = 7

从 3 到已考虑的中心的所有距离中的最小值
Min [dist（3，0），dist（3，1）] = Min [6，5] = 5

计算完上述值后，选择城市 2，因为对应于 2 的值最大。

请注意，对于 k = 2，贪婪算法无法提供最佳解决方案，因为这只是一个近似算法，其边界是最佳算法的两倍。

**证明以上贪婪算法为 2 近似值。**
在最佳解决方案中，让 OPT 为城市到市中心的最大距离。 我们需要证明，从贪婪算法获得的最大距离是 2 * OPT。

证明可以使用矛盾来完成。

a）假设从最远点到所有中心的距离> 2·OPT。

b）这意味着所有中心之间的距离也> 2·OPT。

c）我们有 k + 1 个点，每对之间的距离> 2·OPT。

d）每个点都具有最佳解决方案的中心，并且距它的距离<= OPT。

e）在最优解中存在一对具有相同中心 X 的点（鸽子洞原理：k 个最优中心，k + 1 个点）

f）它们之间的距离最大为 2·OPT（三角形不等式），这是一个矛盾。

**来源**：
[http://algo2.iti.kit.edu/vanstee/courses/kcenter.pdf](http://algo2.iti.kit.edu/vanstee/courses/kcenter.pdf)

本文由 **Harshit** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

