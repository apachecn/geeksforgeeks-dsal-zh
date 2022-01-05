# N 个城市间可能的最小出行成本

> 原文:[https://www . geeksforgeeks . org/n 城市间最小可能旅行成本/](https://www.geeksforgeeks.org/minimum-possible-travel-cost-among-n-cities/)

直线道路上有 **N** 个城市，每个城市之间相隔 **1** 个单位的距离。你必须登车到达 **(N + 1) <sup>第</sup>个**城市。第一个 城市将花费**C【I】**美元来行驶 **1** 单位的距离。换句话说，从**I<sup>th</sup>T19】城市到**j<sup>th</sup>T23】城市的旅行费用是**ABS(I–j)* C【I】**美元。任务是找到从城市 **1** 到城市 **(N + 1)** 即最后一个城市以外的最小出行成本。
**举例:****** 

> **输入:** C[] = {3，5，4}
> **输出:** 9
> 从第一个城市登车的公交成本最低
> 所以将用于出行(N + 1)单位。
> **输入:** C[] = {4，7，8，3，4}
> **输出:** 18
> 在第一个城市上车然后在第四个城市换乘
> 公交车。
> (3 * 4) + (2 * 3) = 12 + 6 = 18

**途径:**途径很简单，只需乘坐目前为止成本最低的公交车出行即可。每当发现一辆成本更低的公共汽车，就从那个城市换一辆。以下是解决步骤:

1.  先从第一个城市开始，成本**C【1】**。
2.  前往下一个城市，直到找到一个费用低于上一个城市(我们旅行的城市，比如说 T2)的城市。
3.  将成本计算为**ABS(j–I)* C[I]**，并将其加入到目前为止的总成本中。
4.  重复前面的步骤，直到遍历完所有城市。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost to
// travel from the first city to the last
int minCost(vector<int>& cost, int n)
{

    // To store the total cost
    int totalCost = 0;

    // Start from the first city
    int boardingBus = 0;

    for (int i = 1; i < n; i++) {

        // If found any city with cost less than
        // that of the previous boarded
        // bus then change the bus
        if (cost[boardingBus] > cost[i]) {

            // Calculate the cost to travel from
            // the currently boarded bus
            // till the current city
            totalCost += ((i - boardingBus) * cost[boardingBus]);

            // Update the currently boarded bus
            boardingBus = i;
        }
    }

    // Finally calculate the cost for the
    // last boarding bus till the (N + 1)th city
    totalCost += ((n - boardingBus) * cost[boardingBus]);
    return totalCost;
}

// Driver code
int main()
{
    vector<int> cost{ 4, 7, 8, 3, 4 };
    int n = cost.size();

    cout << minCost(cost, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum cost to
// travel from the first city to the last
static int minCost(int []cost, int n)
{

    // To store the total cost
    int totalCost = 0;

    // Start from the first city
    int boardingBus = 0;

    for (int i = 1; i < n; i++)
    {

        // If found any city with cost less than
        // that of the previous boarded
        // bus then change the bus
        if (cost[boardingBus] > cost[i])
        {

            // Calculate the cost to travel from
            // the currently boarded bus
            // till the current city
            totalCost += ((i - boardingBus) * cost[boardingBus]);

            // Update the currently boarded bus
            boardingBus = i;
        }
    }

    // Finally calculate the cost for the
    // last boarding bus till the (N + 1)th city
    totalCost += ((n - boardingBus) * cost[boardingBus]);
    return totalCost;
}

// Driver code
public static void main(String[] args)
{
    int []cost = { 4, 7, 8, 3, 4 };
    int n = cost.length;

    System.out.print(minCost(cost, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cost to
# travel from the first city to the last
def minCost(cost, n):

    # To store the total cost
    totalCost = 0

    # Start from the first city
    boardingBus = 0

    for i in range(1, n):

        # If found any city with cost less than
        # that of the previous boarded
        # bus then change the bus
        if (cost[boardingBus] > cost[i]):

            # Calculate the cost to travel from
            # the currently boarded bus
            # till the current city
            totalCost += ((i - boardingBus) *
                          cost[boardingBus])

            # Update the currently boarded bus
            boardingBus = i

    # Finally calculate the cost for the
    # last boarding bus till the (N + 1)th city
    totalCost += ((n - boardingBus) *
                  cost[boardingBus])
    return totalCost

# Driver code
cost = [ 4, 7, 8, 3, 4]
n = len(cost)

print(minCost(cost, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum cost to
// travel from the first city to the last
static int minCost(int []cost, int n)
{

    // To store the total cost
    int totalCost = 0;

    // Start from the first city
    int boardingBus = 0;

    for (int i = 1; i < n; i++)
    {

        // If found any city with cost less than
        // that of the previous boarded
        // bus then change the bus
        if (cost[boardingBus] > cost[i])
        {

            // Calculate the cost to travel from
            // the currently boarded bus
            // till the current city
            totalCost += ((i - boardingBus) *
                          cost[boardingBus]);

            // Update the currently boarded bus
            boardingBus = i;
        }
    }

    // Finally calculate the cost for the
    // last boarding bus till the (N + 1)th city
    totalCost += ((n - boardingBus) *
                  cost[boardingBus]);
    return totalCost;
}

// Driver code
public static void Main(String[] args)
{
    int []cost = { 4, 7, 8, 3, 4 };
    int n = cost.Length;

    Console.Write(minCost(cost, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the minimum cost to
    // travel from the first city to the last
    function minCost(cost , n) {

        // To store the total cost
        var totalCost = 0;

        // Start from the first city
        var boardingBus = 0;

        for (i = 1; i < n; i++) {

            // If found any city with cost less than
            // that of the previous boarded
            // bus then change the bus
            if (cost[boardingBus] > cost[i]) {

                // Calculate the cost to travel from
                // the currently boarded bus
                // till the current city
                totalCost += ((i - boardingBus) * cost[boardingBus]);

                // Update the currently boarded bus
                boardingBus = i;
            }
        }

        // Finally calculate the cost for the
        // last boarding bus till the (N + 1)th city
        totalCost += ((n - boardingBus) * cost[boardingBus]);
        return totalCost;
    }

    // Driver code

        var cost = [ 4, 7, 8, 3, 4 ];
        var n = cost.length;

        document.write(minCost(cost, n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
18
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)