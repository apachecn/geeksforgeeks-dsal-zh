# 股票买卖实现利润最大化

> 原文:[https://www.geeksforgeeks.org/stock-buy-sell/](https://www.geeksforgeeks.org/stock-buy-sell/)

一只股票每天的成本是以数组的形式给出的，找出你在那些日子里通过买卖所能获得的最大利润。例如，如果给定的数组是{100，180，260，310，40，535，695}，则通过在第 0 天买入，在第 3 天卖出可以获得最大利润。再次在第 4 天买入，在第 6 天卖出。如果给定的一系列价格是按递减顺序排序的，那么就根本赚不到利润。

**天真的方法:**一个简单的方法是尝试在每一天盈利的时候买入股票并卖出，并不断更新到目前为止的最大利润。

下面是上述方法的实现:

## c++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
int maxProfit(int price[], int start, int end)
{

    // If the stocks can't be bought
    if (end <= start)
        return 0;

    // Initialise the profit
    int profit = 0;

    // The day at which the stock
    // must be bought
    for (int i = start; i < end; i++) {

        // The day at which the
        // stock must be sold
        for (int j = i + 1; j <= end; j++) {

            // If buying the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i]) {

                // Update the current profit
                int curr_profit = price[j] - price[i]
                                  + maxProfit(price, start, i - 1)
                                  + maxProfit(price, j + 1, end);

                // Update the maximum profit so far
                profit = max(profit, curr_profit);
            }
        }
    }
    return profit;
}

// Driver code
int main()
{
    int price[] = { 100, 180, 260, 310,
                    40, 535, 695 };
    int n = sizeof(price) / sizeof(price[0]);

    cout << maxProfit(price, 0, n - 1);

    return 0;
}
```

## Java

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
static int maxProfit(int price[], int start, int end)
{

    // If the stocks can't be bought
    if (end <= start)
        return 0;

    // Initialise the profit
    int profit = 0;

    // The day at which the stock
    // must be bought
    for (int i = start; i < end; i++)
    {

        // The day at which the
        // stock must be sold
        for (int j = i + 1; j <= end; j++)
        {

            // If buying the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i])
            {

                // Update the current profit
                int curr_profit = price[j] - price[i]
                                + maxProfit(price, start, i - 1)
                                + maxProfit(price, j + 1, end);

                // Update the maximum profit so far
                profit = Math.max(profit, curr_profit);
            }
        }
    }
    return profit;
}

// Driver code
public static void main(String[] args)
{
    int price[] = { 100, 180, 260, 310,
                    40, 535, 695 };
    int n = price.length;

    System.out.print(maxProfit(price, 0, n - 1));
}
}

// This code is contributed by PrinciRaj1992
```

## python 3

```
# Python3 implementation of the approach

# Function to return the maximum profit
# that can be made after buying and
# selling the given stocks
def maxProfit(price, start, end):

    # If the stocks can't be bought
    if (end <= start):
        return 0;

    # Initialise the profit
    profit = 0;

    # The day at which the stock
    # must be bought
    for i in range(start, end, 1):

        # The day at which the
        # stock must be sold
        for j in range(i+1, end+1):

            # If buying the stock at ith day and
            # selling it at jth day is profitable
            if (price[j] > price[i]):

                # Update the current profit
                curr_profit = price[j] - price[i] +\
                            maxProfit(price, start, i - 1)+ \
                            maxProfit(price, j + 1, end);

                # Update the maximum profit so far
                profit = max(profit, curr_profit);

    return profit;

# Driver code
if __name__ == '__main__':
    price = [100, 180, 260, 310, 40, 535, 695];
    n = len(price);

    print(maxProfit(price, 0, n - 1));

# This code is contributed by Rajput-Ji
```

## c#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
static int maxProfit(int []price, int start, int end)
{

    // If the stocks can't be bought
    if (end <= start)
        return 0;

    // Initialise the profit
    int profit = 0;

    // The day at which the stock
    // must be bought
    for (int i = start; i < end; i++)
    {

        // The day at which the
        // stock must be sold
        for (int j = i + 1; j <= end; j++)
        {

            // If buying the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i])
            {

                // Update the current profit
                int curr_profit = price[j] - price[i]
                                + maxProfit(price, start, i - 1)
                                + maxProfit(price, j + 1, end);

                // Update the maximum profit so far
                profit = Math.Max(profit, curr_profit);
            }
        }
    }
    return profit;
}

// Driver code
public static void Main(String[] args)
{
    int []price = { 100, 180, 260, 310,
                    40, 535, 695 };
    int n = price.Length;

    Console.Write(maxProfit(price, 0, n - 1));
}
}

// This code is contributed by PrinciRaj1992
```

## Javascript

```
<script>

// Javascript implementation of the approach

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
function maxProfit( price, start, end)
{

    // If the stocks can't be bought
    if (end <= start)
        return 0;

    // Initialise the profit
    let profit = 0;

    // The day at which the stock
    // must be bought
    for (let i = start; i < end; i++) {

        // The day at which the
        // stock must be sold
        for (let j = i + 1; j <= end; j++) {

            // If buying the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i]) {

                // Update the current profit
                let curr_profit = price[j] - price[i]
                                  + maxProfit(price, start, i - 1)
                                  + maxProfit(price, j + 1, end);

                // Update the maximum profit so far
                profit = Math.max(profit, curr_profit);
            }
        }
    }
    return profit;
}

    // Driver program

    let price = [ 100, 180, 260, 310,
                    40, 535, 695 ];
    let n = price.length;

    document.write(maxProfit(price, 0, n - 1));

</script>
```

**输出**

```
865
```