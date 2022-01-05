# Python |肯德尔秩相关系数

> 原文:[https://www . geesforgeks . org/python-Kendall-rank-correlation-coefficient/](https://www.geeksforgeeks.org/python-kendall-rank-correlation-coefficient/)

**什么是相关性检验？**
两个变量之间的关联强度被称为相关性检验。例如，如果我们想知道父亲和儿子的身高之间是否有关系，可以计算相关系数来回答这个问题。

如需了解更多相关信息，请参考[。](https://www.geeksforgeeks.org/mathematics-covariance-and-correlation/)

**相关分析方法:**
相关主要有两种类型:

*   **参数相关–皮尔逊相关(r) :** 它测量两个变量(x 和 y)之间的线性相关性，被称为参数相关测试，因为它取决于数据的分布。
*   **非参数相关–肯德尔(τ)**和 **[斯皮尔曼(ρ)](https://www.geeksforgeeks.org/program-spearmans-rank-correlation/):**它们是基于秩的相关系数，被称为非参数相关。

**肯德尔秩相关系数公式:**

<center>![\tau=\frac{\text { Number of concordant pairs-Number of discordant pairs }}{n(n-1) / 2}](img/602572736574c2d2e8c16ce20d962fab.png "Rendered by QuickLaTeX.com")</center>

哪里，

*   **一致对:**遵循该性质的一对观测值(x1，y1)和(x2，y2)
    *   x1 > x2 和 y1 > y2 或
    *   x1 < x2 和 y1 < y2
*   **不一致对:**遵循该属性的一对观测值(x1，y1)和(x2，y2)
    *   x1 > x2 和 y1 < y2 或
    *   x1 < x2 and y1 > y2
*   **n:** 样本总数

**注:**对其 **x1 = x2** 和 **y1 = y2** 未被归类为一致或不一致的配对被忽略。

**例:**我们来考虑下表中两位专家对食物项目的排名。

| 项目 | 专家 1 | 专家 2 |
| --- | --- | --- |
| one | one | one |
| Two | Two | three |
| three | three | six |
| four | four | Two |
| five | five | seven |
| six | six | four |
| seven | seven | five |

表格显示，对于项目 1，专家 1 给出等级 1，而专家 2 也给出等级 1。类似地，对于项目 2，专家 1 给出等级 2，而专家 2 给出等级 3，以此类推。

**第一步:**
首先，根据公式，我们要找到一致对的个数和不一致对的个数。所以看看第 1 行和第 2 行。让专家-1、 *x1 = 1* 和 *x2 = 2* 。同样对于专家-2， *y1 = 1* 和 *y2 = 3* 。所以条件 *x1 < x2* 和 *y1 < y2* 满足，我们可以说项-1 和项-2 行是一致对。

同样，看看第 2 行和第 4 行。让专家-1、 *x1 = 2* 、 *x2 = 4* 。同样，对于专家-2， *y1 = 3* 和 *y2 = 2* 。所以条件 *x1 < x2* 和 *y1 > y2* 满足，我们可以说项-2 和项-4 行是不一致的对。

像这样，通过比较每一行，你可以计算出一致和不一致对的数量。下表给出了完整的解决方案。

| one |  |  |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Two | C |  |  |  |  |  |  |
| three | C | C |  |  |  |  |  |
| four | C | **D** | **D** |  |  |  |  |
| five | C | C | C | C |  |  |  |
| six | C | C | C | **D** | **D** |  |  |
| seven | C | C | C | C | **D** | **D** |  |
|  | one | Two | three | four | five | six | seven |

**第二步:**
所以从上表我们发现，
一致对的数量为:15
不一致对的数量为:6
样本/项目总数为:7

因此，通过应用肯德尔秩相关系数公式
 **τ=(15–6)/21 = 0.42857**

这个结果表明，如果它基本上是高的，那么这两位专家之间有一个广泛的共识。否则，如果专家-1 完全不同意专家-2，你甚至可能得到负值。

**kendaltau():**Python 函数计算 Python 中的 Kendall 秩相关系数

> 语法:
> kendalltau(x，y)
> 
> *   x，y:长度相同的数字列表

**代码:** Python 程序说明肯德尔等级相关性

## 计算机编程语言

```
# Import required libraries
from scipy.stats import kendalltau

# Taking values from the above example in Lists
X = [1, 2, 3, 4, 5, 6, 7]
Y = [1, 3, 6, 2, 7, 4, 5]

# Calculating Kendall Rank correlation
corr, _ = kendalltau(X, Y)
print('Kendall Rank correlation: %.5f' % corr)

# This code is contributed by Amiya Rout
```

**输出:**

```
Kendall Rank correlation: 0.42857
```