# 根据航空旅行的重量计算要为行李支付的额外费用

> 原文:[https://www . geeksforgeeks . org/按重量计算航空旅行行李额外费用/](https://www.geeksforgeeks.org/calculate-extra-cost-to-be-paid-for-luggage-based-on-weight-for-air-travel/)

给定一个包含行李重量的 **N** 大小的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **重量[]** 。如果重量在 **W** 的阈值内，则不需要任何额外的成本。但是根据下表，在重量超过阈值后，他们需要支付额外的费用。任务是计算所需行李的额外费用。

<figure class="table">

| 超重范围 | 超重费用 |
|             0 – 50 |               100 |
|           51 – 100 |               200 |
|         101 – 150 |               300 |
|         151 – 200 |               500 |
|            > 200 |               1000 |

**示例:**

> **输入:**权重[] = {5，4，3，6}，W = 8
> **输出:** 0
> **说明:**无权重过阈值。因此不会产生额外的成本。
> 
> **输入:**权重[] = {120，135，280，60，300}，W = 90
> **输出:** 1700
> **说明:**权重 120 比阈值多 30。所以，它需要 100 的额外费用。
> 权重 135 比阈值多 45。所以，它需要 100 的额外费用。
> 权重 280 比阈值多 190。所以，它需要 500 的额外费用。
> 权重 300 比阈值多 210。所以，需要 1000 的额外费用。
> 权重 60 在阈值内。所以，它不需要成本。
> 额外总成本为(100 + 100 + 500 + 1000) = 1700

**进场:**进场基于以下观察。如果行李重量超过阈值 **W** ，则根据给定的表格，会产生额外费用。按照下面提到的步骤解决问题:

*   从头开始迭代数组。
    *   检查当前行李重量是否超过 **W** 。
        *   如果有，那么根据给定表格中的多余重量增加额外费用。
        *   否则继续迭代。
*   返回总的额外成本

下面是上述方法的实现，

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;

class GFG {

    // Function to calculate the extra cost
    static int weighingMachine(int N, int weight[], int W)
    {
        int amount = 0;

        // Loop to calculate the excess cost
        for (int i = 0; i < N; i++) {
            if (weight[i] - W > 0 
                && weight[i] - W <= 50)
                amount += 100;
            else if (weight[i] - W > 50
                     && weight[i] - W <= 100)
                amount += 200;
            else if (weight[i] - W > 100
                     && weight[i] - W <= 150)
                amount += 300;
            else if (weight[i] - W > 150
                     && weight[i] - W <= 200)
                amount += 500;
            else if (weight[i] - W > 200)
                amount += 1000;
        }
        return amount;
    }

    // Driver code
    public static void main(String[] args)
    {
        int weight[] = 
        { 120, 135, 280, 60, 300 };
        int N = 5;
        int W = 90;

        System.out.println(
          weighingMachine(N, weight, W));
    }
}
```

**Output**

```
1700

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

</figure>