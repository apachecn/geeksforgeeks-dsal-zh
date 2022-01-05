# 找到过河的最小成本

> 原文:[https://www . geeksforgeeks . org/find-最小过河成本/](https://www.geeksforgeeks.org/find-the-minimum-cost-to-cross-the-river/)

给定一个整数 **N** ，这是需要过河的村民人数，但是最多只有一艘船 **2** 人可以在上面行驶。每个人 **i** 都要付出一些特定的代价**P<sub>I</sub>T9】才能独自在船上旅行。如果两个人 **i，j** 在船上旅行，那么他们必须支付 **max(P <sub>i</sub> ，P <sub>j</sub> )** 。任务是找到所有村民过河必须支付的最低金额。
**例:**** 

> **投入:**价格[] = {30，40，60，70}
> 产出: 220
> P <sub>1</sub> 和 P <sub>2</sub> 一起去(花费 40)
> P<sub>1</sub>回来(现在总花费 70)。
> 现在 P <sub>3</sub> 和 P <sub>4</sub> 一起去(总成本 140)
> P<sub>2</sub>回来(总成本 180)
> 最后 P <sub>1</sub> 和 P <sub>2</sub> 一起去(总成本 220)。
> **输入:**价格[] = {892，124}
> **输出:** 892

**途径:**两个最贵的人过河有两种方式:

*   他们俩轮流和最便宜的人过河。因此，总成本将是两个昂贵的人的成本+ 2 *(最便宜的人的成本)(由于回来)。
*   两个最便宜的人过河，最便宜的人回来。现在，2 个最贵的人过河，2 个最便宜的人回来。所以，总成本将是最便宜和最贵的人的成本加上第二便宜的人的 2 *成本。
*   总成本将是上述两种方式中的最小值。

> 让我们考虑一下我们上面用来理解方法的例子:
> P <sub>1</sub> = 30，P <sub>2</sub> = 40，P <sub>3</sub> = 60，P <sub>4</sub> = 70
> 按照第一种方法，P <sub>4</sub> 跟 P <sub>1</sub> 走，P <sub>1</sub> 回来(成本为 P<sub>4</sub>+P
> 现在，P <sub>3</sub> 跟 P <sub>1</sub> 走，P <sub>1</sub> 回来(本次乘坐费用为 P <sub>4</sub> +P <sub>1</sub> )。
> 所以，按照方法 1 派出两个最贵的人的总成本是 P<sub>4</sub>+2 * P<sub>1</sub>+P<sub>3</sub>= 190
> 按照第二种方法，P <sub>2</sub> 跟 P <sub>1</sub> 走，P <sub>1</sub> 回来(成本是 P <sub>2</sub> +P <sub>1</sub> )。
> 现在，P <sub>3</sub> 跟 P <sub>4</sub> 走，P <sub>2</sub> 回来(本次乘坐费用为 P <sub>4</sub> +P <sub>2</sub> )。
> 因此，按照方法 2 派遣两个最昂贵的人的总成本是 P<sub>4</sub>+2 * P<sub>2</sub>+P<sub>1</sub>= 180
> 因此，派遣 P <sub>3</sub> 和 P <sub>4</sub> 的成本将是 2 种方法中的最小值，即 180。
> 现在只剩下 P <sub>1</sub> 和 P <sub>2</sub> 了，我们要一起送，费用将
> 为 P <sub>2</sub> = 40。
> 那么，旅游总费用是 180 + 40 = 220。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to return the minimum cost
int minimumCost(ll price[], int n)
{

    // Sort the price array
    sort(price, price + n);
    ll totalCost = 0;

    // Calculate minimum price
    // of n-2 most costly person
    for (int i = n - 1; i > 1; i -= 2) {
        if (i == 2) {
            totalCost += price[2] + price[0];
        }
        else {

            // Both the ways as discussed above
            ll price_first = price[i] + price[0] + 2 * price[1];
            ll price_second = price[i] + price[i - 1] + 2 * price[0];
            totalCost += min(price_first, price_second);
        }
    }

    // Calculate the minimum price
    // of the two cheapest person
    if (n == 1) {
        totalCost += price[0];
    }
    else {
        totalCost += price[1];
    }

    return totalCost;
}

// Driver code
int main()
{
    ll price[] = { 30, 40, 60, 70 };
    int n = sizeof(price) / sizeof(price[0]);

    cout << minimumCost(price, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the minimum cost
    static long minimumCost(long price[], int n)
    {

        // Sort the price array
        Arrays.sort(price);

        long totalCost = 0;

        // Calculate minimum price
        // of n-2 most costly person
        for (int i = n - 1; i > 1; i -= 2)
        {
            if (i == 2)
            {
                totalCost += price[2] + price[0];
            }
            else
            {

                // Both the ways as discussed above
                long price_first = price[i] + price[0] + 2 * price[1];
                long price_second = price[i] + price[i - 1] + 2 * price[0];
                totalCost += Math.min(price_first, price_second);
            }
        }

        // Calculate the minimum price
        // of the two cheapest person
        if (n == 1)
        {
            totalCost += price[0];
        }
        else
        {
            totalCost += price[1];
        }

        return totalCost;
    }

    // Driver code
    public static void main (String[] args)
    {
        long price[] = { 30, 40, 60, 70 };
        int n = price.length;

        System.out.println(minimumCost(price, n));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the minimum cost
def minimumCost(price, n):

    # Sort the price array
    price = sorted(price)
    totalCost = 0

    # Calculate minimum price
    # of n-2 most costly person
    for i in range(n - 1, 1, -2):
        if (i == 2):
            totalCost += price[2] + price[0]

        else:

            # Both the ways as discussed above
            price_first = price[i] + price[0] + 2 * price[1]
            price_second = price[i] + price[i - 1] + 2 * price[0]
            totalCost += min(price_first, price_second)

    # Calculate the minimum price
    # of the two cheapest person
    if (n == 1):
        totalCost += price[0]

    else:
        totalCost += price[1]

    return totalCost

# Driver code

price = [30, 40, 60, 70]
n = len(price)

print(minimumCost(price, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum cost
    static long minimumCost(long []price, int n)
    {

        // Sort the price array
        Array.Sort(price);

        long totalCost = 0;

        // Calculate minimum price
        // of n-2 most costly person
        for (int i = n - 1; i > 1; i -= 2)
        {
            if (i == 2)
            {
                totalCost += price[2] + price[0];
            }
            else
            {

                // Both the ways as discussed above
                long price_first = price[i] + price[0] + 2 * price[1];
                long price_second = price[i] + price[i - 1] + 2 * price[0];
                totalCost += Math.Min(price_first, price_second);
            }
        }

        // Calculate the minimum price
        // of the two cheapest person
        if (n == 1)
        {
            totalCost += price[0];
        }
        else
        {
            totalCost += price[1];
        }

        return totalCost;
    }

    // Driver code
    public static void Main ()
    {
        long []price = { 30, 40, 60, 70 };
        int n = price.Length;

        Console.WriteLine(minimumCost(price, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum cost
    function minimumCost(price, n)
    {

        // Sort the price array
        price.sort();

        let totalCost = 0;

        // Calculate minimum price
        // of n-2 most costly person
        for (let i = n - 1; i > 1; i -= 2)
        {
            if (i == 2)
            {
                totalCost += price[2] + price[0];
            }
            else
            {

                // Both the ways as discussed above
                let price_first = price[i] + price[0] + 2 * price[1];
                let price_second = price[i] + price[i - 1] + 2 * price[0];
                totalCost += Math.min(price_first, price_second);
            }
        }

        // Calculate the minimum price
        // of the two cheapest person
        if (n == 1)
        {
            totalCost += price[0];
        }
        else
        {
            totalCost += price[1];
        }

        return totalCost;
    }

    let price = [ 30, 40, 60, 70 ];
    let n = price.length;

    document.write(minimumCost(price, n));

</script>
```

**Output:** 

```
220
```