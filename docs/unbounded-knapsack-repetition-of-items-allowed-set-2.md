# 无界背包(允许重复物品)|第 2 套

> 原文:[https://www . geesforgeks . org/无界-背包-物品重复-允许-集合-2/](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-of-items-allowed-set-2/)

给定整数 **W** ，数组**val【】**和**wt【】**，其中**val【I】**和**wt【I】**是 i <sup>第</sup>项的值和权重，任务是计算使用不超过 **W** 的权重可以获得的最大值。
***注:**每个重量可以包含多次。*

**示例:**

> **输入:** W = 4，val[] = {6，18}，wt[] = {2，3}
> **输出:** 18
> **解释:**通过两次选择 2 <sup>和</sup>项，可以获得的最大值为 18。
> 
> **输入:** W = 50，val[] = {6，18}，wt[] = {2，3}
> **输出:** 294

**天真方法:**参考[之前的帖子](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/)使用传统的无界背包算法解决问题。
***时间复杂度:** O(N * W)
**辅助空间:** O(W)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   假设 **i <sup>th</sup>** 指数给出了给定数据中单位重量的最大值，在 **O(n)** 中很容易找到。
*   对于任何重量 **X** ，大于或等于**重量【I】**，最大可达值将是**DP【X–重量【I】】+价值【I】**。
*   我们可以使用传统算法计算从 **0** 到**wt【I】**的 **dp[]** 的值，并且我们还可以计算我们可以放入 W 权重的 **i <sup>th</sup>** 项的实例数量。
*   所以需要的答案是**值[i] * (W/wt[i]) + dp[W%wt[i]]** 。

下面是新算法的实现。

## 蟒蛇 3

```
# Python Program to implement the above approach

from fractions import Fraction

# Function to implement optimized
# Unbounded Knapsack algorithm
def unboundedKnapsackBetter(W, val, wt):

    # Stores most dense item
    maxDenseIndex = 0

    # Find the item with highest unit value
    # (if two items have same unit value then choose the lighter item)
    for i in range(1, len(val)):

      if Fraction(val[i], wt[i]) \
            > Fraction(val[maxDenseIndex], wt[maxDenseIndex]) \
             or (Fraction(val[i], wt[i]) == Fraction(val[maxDenseIndex], wt[maxDenseIndex]) \
             and wt[i] < wt[maxDenseIndex] ):

        maxDenseIndex = i

    dp = [0 for i in range(W + 1)]

    counter = 0
    breaked = False
    for i in range(W + 1):
        for j in range(len(wt)):

            if (wt[j] <= i):
                dp[i] = max(dp[i], dp[i - wt[j]] + val[j])

        if i - wt[maxDenseIndex] >= 0 \
            and dp[i] - dp[i-wt[maxDenseIndex]] == val[maxDenseIndex]:

            counter += 1

            if counter>= wt[maxDenseIndex]:

                breaked = True
                # print(i)
                break
        else:
            counter = 0

    if not breaked:
        return dp[W]
    else:
        start = i - wt[maxDenseIndex] + 1
        times = (W - start) // wt[maxDenseIndex]
        index = (W - start) % wt[maxDenseIndex] + start
        return (times * val[maxDenseIndex] + dp[index])

# Driver Code
W = 100
val = [10, 30, 20]
wt = [5, 10, 15]

print(unboundedKnapsackBetter(W, val, wt))
```

**Output:**

```
300

```

***时间复杂度** : O( N + min(wt[i]，W) * N)
**辅助空间:** O(W)*