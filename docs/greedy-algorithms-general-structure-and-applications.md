# 贪婪算法(一般结构和应用)

> 原文:[https://www . geesforgeks . org/greedy-algorithms-general-structure-and-applications/](https://www.geeksforgeeks.org/greedy-algorithms-general-structure-and-applications/)

贪婪算法按部就班地工作，并且总是选择能提供即时利润/收益的步骤。它选择“局部最优解”，而不考虑未来的后果。贪婪算法不一定总能得到全局最优解，因为它没有考虑整个数据。贪婪方法做出的选择没有考虑未来的数据和选择。在某些情况下，做出一个看起来正确的决定会给出最好的解决方案(贪婪)，但在其他情况下则不会。贪婪技术最适合于观察眼前的情况。

**所有贪婪算法都遵循一个基本结构:**

```
getOptimal(Item, arr[], int n)
  1) Initialize empty result : result = {}  
  2) While (All items are not considered)

      // We make a greedy choice to select
      // an item.
      i = SelectAnItem() 

      // If i is feasible, add i to the 
      // result
      if (feasible(i))
        result = result U i 
  3) return result
```

**为什么选择贪婪方法-**

贪婪方法有一些折衷，这可能使它适合于优化。一个突出的原因是立即实现最可行的解决方案。在活动选择问题(解释如下)中，如果在完成当前活动之前可以完成更多的活动，则这些活动可以在同一时间内执行。另一个原因是基于一个条件递归地划分一个问题，不需要组合所有的解。在活动选择问题中，“递归划分”步骤是通过只扫描一次项目列表并考虑某些活动来实现的。

贪婪选择性质:这个性质说的是全局最优解可以通过做出局部最优解(贪婪)来获得。贪婪算法做出的选择可能取决于早期的选择，但不取决于未来。它反复地做出一个又一个贪婪的选择，并将给定的问题简化为一个更小的问题。

最优子结构:如果问题的最优解包含子问题的最优解，则问题表现出最优子结构。这意味着我们可以解决子问题，并建立解决方案来解决更大的问题。

**注:**做出局部最优选择并不总是奏效。因此，贪婪算法不会总是给出最好的解决方案。

**贪婪进场的特点**
1。资源(利润、成本、价值等)有一个有序的列表。)
2。所有资源的最大化(最大利润、最大价值等))都拍了。
3。例如，在分数背包问题中，首先根据可用容量取最大值/重量。

**贪婪算法的应用**
1。寻找最优解([活动选择](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/)、[分数背包](https://www.geeksforgeeks.org/fractional-knapsack-problem/)、[作业排序](https://www.geeksforgeeks.org/job-sequencing-problem/)、[霍夫曼编码](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/))。
2。寻找像旅行商问题这样的 NP-Hard 问题的接近最优解。

**贪婪方法的优缺点**
**优点**

*   贪婪的方法很容易实现。
*   通常时间复杂度较低。
*   贪婪算法可以用于优化目的，或者在 NP-Hard 问题的情况下寻找接近优化的目标。

**劣势**T2】

*   局部最优解可能不总是全局最优的。

**标准贪婪算法:**