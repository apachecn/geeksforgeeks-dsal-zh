# 集合覆盖问题|集合 1(贪婪近似算法)

> 原文:[https://www . geesforgeks . org/set-cover-problem-set-1-greedy-approach-algorithm/](https://www.geeksforgeeks.org/set-cover-problem-set-1-greedy-approximate-algorithm/)

给定一个由 n 个元素组成的宇宙 U，U 的子集集合 S = {S <sub>1</sub> 、S <sub>2</sub> …、S <sub>m</sub> }其中每个子集 S <sub>i</sub> 都有一个相关的成本。找到一个覆盖所有美国元素的最小成本的美国子集合

示例:

```
   U = {1,2,3,4,5}
   S = {S1,S2,S3}

   S1 = {4,1,3},    Cost(S1) = 5
   S2 = {2,5},      Cost(S2) = 10
   S3 = {1,4,3,2},  Cost(S3) = 3

Output: Minimum cost of set cover is 13 and 
        set cover is {S2, S3}

There are two possible set covers {S1, S2} with cost 15
and {S2, S3} with cost 13.

```

**为什么有用？**
这是卡普的 NP 完全问题之一，在 1972 年被证明是这样。其他应用:边覆盖、顶点覆盖
有趣的例子:IBM 发现计算机病毒(维基百科)
Elements- 5000 已知病毒
set-9000 连续 20 个字节以上的病毒子串，在‘好’代码中找不到。
找到一套 180 的封面。搜索这 180 个子串就足以验证已知计算机病毒的存在。

另一个例子:考虑通用汽车需要购买一定数量的各种供应品，并且有供应商为不同的材料组合提供各种交易(供应商 A: 2 吨钢+ 500 块瓷砖，价格为 x 美元；供应商 B: 1 吨钢+ 2000 块瓷砖，y 美元；等等。).您可以使用集合覆盖来找到获得所有材料的最佳方式，同时将成本降至最低
来源:[http://math.mit.edu/~goemans/18434S06/setcover-tamara.pdf](http://math.mit.edu/~goemans/18434S06/setcover-tamara.pdf)

**Set Cover 是 NP-Hard:**
这个问题没有多项式时间的解，因为这个问题是一个已知的 NP-Hard 问题。有一个多项式时间的贪婪近似算法，贪婪算法提供了一个 Logn 近似算法。

**2-近似贪婪算法:**
让 U 成为元素的宇宙，{S <sub>1</sub> 、S <sub>2</sub> 、… S <sub>m</sub> 成为 U 和 Cost 的子集集合(S <sub>1</sub> )、C(S <sub>2</sub> )、… Cost(S <sub>m</sub> )成为子集的 Cost。

```
1) Let I represents set of elements included so far.  Initialize I = {}

2) Do following while I is not same as U.
    a) Find the set Si in {S1, S2, ... Sm} whose cost effectiveness is 
       smallest, i.e., the ratio of cost C(Si) and number of newly added 
       elements is minimum. 
       Basically we pick the set for which following value is minimum.
           Cost(Si) / |Si - I|
    b) Add elements of above picked Si to I, i.e.,  I = I U Si

```

**例:**
让我们考虑一下上面的例子来理解贪婪算法。

*第一次迭代:*
I = {}

S <sub>1</sub> 的每新元素成本=成本(S<sub>1</sub>)/| S<sub>1</sub>–I | = 5/3

S <sub>2</sub> 的每新元素成本=成本(S<sub>2</sub>)/| S<sub>2</sub>–I | = 10/2

S <sub>3</sub> 的每新元素成本=成本(S<sub>3</sub>)/| S<sub>3</sub>–I | = 3/4

由于 S <sub>3</sub> 有最小值 S <sub>3</sub> 相加，我变成{1，4，3，2}。

*第二次迭代:*
I = {1，4，3，2}

S <sub>1</sub> =成本(S<sub>1</sub>)/| S<sub>1</sub>–I | = 5/0
注意 S <sub>1</sub> 没有给 I 增加任何新元素

S <sub>2</sub> =成本(S<sub>2</sub>)/| S<sub>2</sub>–I | = 10/1
注意 S <sub>2</sub> 只加 5 到 I

贪婪算法为上述例子提供了最优解，但它可能不会一直提供最优解。考虑下面的例子。

```
S1 = {1, 2}
S2 = {2, 3, 4, 5}
S3 = {6, 7, 8, 9, 10, 11, 12, 13}
S4 = {1, 3, 5, 7, 9, 11, 13}
S5 = {2, 4, 6, 8, 10, 12, 13}

Let the cost of every set be same.

The greedy algorithm produces result as {S3, S2, S1}

The optimal solution is {S4, S5} 
```

**证明上述贪婪算法是 Logn 近似。**
让 OPT 成为最优解的代价。假设(k-1)元素在上述贪婪算法的迭代之前被覆盖。第 k 个元素的成本< = opt (n-k+1)(注意，一个元素的成本是通过它的集合除以元素添加集合的数量来计算的)。我们是如何得到这个结果的？因为 k 还没有被覆盖，所以在贪婪算法的当前步骤之前，有一个 s <sub>i 还没有被覆盖，它就在 OPT 中。由于贪婪算法选择最具成本效益的 S <sub>i</sub> ，因此所选集合中的每元素成本必须小于 OPT 除以剩余元素。因此第 k 个元素<的成本= opt |u-i|(注意 u-i 是贪婪算法中一组尚未覆盖的元素)。n-k+1 的值 n - (k-1)。</sub>

```
Cost of Greedy Algorithm = Sum of costs of n elements 
                        [putting k = 1, 2..n in above formula]
                         <= 1 2 (opt n + opt(n-1) ... opt n) <="OPT(1" ...... [since .. ≈ log n] * logn pre>Source:
[http://math.mit.edu/~goemans/18434S06/setcover-tamara.pdf](http://math.mit.edu/~goemans/18434S06/setcover-tamara.pdf)This article is contributed by **Harshit**. Please write comments if you find anything incorrect, or you want to share more information about the topic discussed above.=>=>=>
```