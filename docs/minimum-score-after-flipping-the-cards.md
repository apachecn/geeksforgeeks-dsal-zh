# 翻牌后的最低分

> 原文:[https://www . geesforgeks . org/翻牌后最低分数/](https://www.geeksforgeeks.org/minimum-score-after-flipping-the-cards/)

给定每张卡片的正面和背面印有正整数的卡片(可能不同)。任何数量的牌都可以翻转，然后我们从一副牌中选择一张。如果所选卡片背面写的数字 *X* 不在任何卡片的前面，那么我们说数字 *X* 就好。任务是找到最小的好数字。如果没有号码好，则打印 *0* 。

**注意:**一次翻转会交换卡片上的正面和背面号码，即正面的数值现在在背面，反之亦然。

**示例:**

> **输入:**正面= [1，2，4，4，7，8]，背面= [1，3，4，1，3，9]
> **输出:** 2
> 如果我们翻第二张牌，正面是[1，3，4，4，7，8]，背面是[1，2，4，1，3，9]。
> 现在，我们选择第二张卡，背面有 2 号，它不在任何其他卡的正面，所以 2 是好的。
> 
> **输入:**正面= [1，2，3，4，5]，背面= [6，7，8，9，10]
> **输出:** 1

**进场:**

*   如果一张牌的正面和背面写着相同的数值 *K* ，那么 *K* 就不可能是答案，因为不管你翻牌多少次，结果都是一样的。
*   每一张正面和背面写有不同数字的卡片都是答案的候选，因为无论数字 *K* 在`front`阵列中重复多少次，只要翻转所有卡片，那么就不会再有正面写有 *K* 的卡片了，然后我们可以简单地选择背面写有 *K* 的任何卡片(最小)，它就是答案。
*   现在问题简化为找到所有的数字 **K1，K2，…，Kn** ，这样它们就不会在任何卡片上重复，然后在写在 **K1，K2，…，Kn** 背面的所有数字中找到最小值。
*   如果结果不可能，则打印 *0* 。

下面是上述方法的实现:

```
# Python3 iomplementation of the approach
import itertools

MAX = 9999

def flipgame(fronts, backs):

    same = {k for i, k in enumerate(fronts) if k == backs[i]}

    # Initialize answer to arbitrary value
    ans = MAX

    for k in itertools.chain(fronts, backs):
        if k not in same:
            ans = min(ans, k)

    # Return final answer
    return ans % MAX

# Driver Code
fronts = [1, 2, 4, 4, 7]
backs = [1, 3, 4, 1, 3]
print(flipgame(fronts, backs))
```

**Output:**

```
2

```