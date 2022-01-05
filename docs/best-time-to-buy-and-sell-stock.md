# 买卖股票的最佳时间

> 原文:[https://www . geesforgeks . org/最佳买卖股票时间/](https://www.geeksforgeeks.org/best-time-to-buy-and-sell-stock/)

**<u>第一类:最多允许一笔交易</u>**

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **价格[]** ，代表不同日期股票的价格，任务是使用最多允许一次交易的交易找到不同日期买卖股票的最大可能利润。

***注:**股票必须先买后卖。*

**示例:**

> **输入:**价格[] = {7，1，5，3，6，4]
> **输出:** 5
> **说明:**
> 该股最低价格在 2 <sup>日</sup>日，即价格= 1。从第 2 天开始，股票的最高价格见证在第 5<sup>天，即价格= 6。
> 因此，最大可能利润= 6–1 = 5。</sup>
> 
> **输入:**价格[] = {7，6，4，3，1}
> **输出:** 0
> **说明:**由于数组是递减顺序，不存在解决问题的可能方式。

**方法:**给定的问题可以基于寻找在较大数目之前出现的较小数目的两个阵列元素之间的[最大差值的思想来解决。因此，这个问题可以简化为为每对指数 **i** 和 **j、**找到**max⁡(prices[j]−prices[i】)**,使得 **j > i** 。](https://www.geeksforgeeks.org/maximum-difference-between-two-elements/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find maximum profit possible
// by buying and selling at most one stack
int findMaximumProfit(vector<int>& prices, int i, int k,
                      bool buy, vector<vector<int> >& v)
{
    // If no stock can be chosen
    if (i >= prices.size() || k <= 0)
        return 0;

    if (v[i][buy] != -1)
        return v[i][buy];

    // If a stock is already bought
    if (buy) {
        return v[i][buy]
               = max(-prices[i]
                         + findMaximumProfit(prices, i + 1,
                                             k, !buy, v),
                     findMaximumProfit(prices, i + 1, k,
                                       buy, v));
    }

    // Otherwise
    else {
        // Buy now
        return v[i][buy]
               = max(prices[i]
                         + findMaximumProfit(
                             prices, i + 1, k - 1, !buy, v),
                     findMaximumProfit(prices, i + 1, k,
                                       buy, v));
    }
}

// Function to find the maximum
// profit in the buy and sell stock
int maxProfit(vector<int>& prices)
{

    int n = prices.size();
    vector<vector<int> > v(n, vector<int>(2, -1));

    // buy = 1 because atmost one
    // transaction is allowed
    return findMaximumProfit(prices, 0, 1, 1, v);
}

// Driver Code
int main()
{
    // Given prices
    vector<int> prices = { 7, 1, 5, 3, 6, 4 };

    // Function Call to find the
    // maximum profit possible by
    // buying and selling a single stock
    int ans = maxProfit(prices);

    // Print answer
    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find maximum profit possible
// by buying and selling at most one stack
static int findMaximumProfit(int[] prices, int i, int k,
                             int buy, int[][] v)
{

    // If no stock can be chosen
    if (i >= prices.length || k <= 0)
        return 0;

    if (v[i][buy] != -1)
        return v[i][buy];

    // If a stock is already bought
    // Buy now
    int nbuy;
    if (buy == 1)
        nbuy = 0;
    else
        nbuy = 1;
    if (buy == 1)
    {
        return v[i][buy] = Math.max(-prices[i] +
         findMaximumProfit(prices, i + 1, k, nbuy, v),
         findMaximumProfit(prices, i + 1, k, (int)(buy), v));
    }

    // Otherwise
    else
    {

        // Buy now
        if (buy == 1)
            nbuy = 0;
        else
            nbuy = 1;
        return v[i][buy] = Math.max(prices[i] +
         findMaximumProfit(prices, i + 1, k - 1, nbuy, v),
         findMaximumProfit(prices, i + 1, k, buy, v));
    }
}

// Function to find the maximum
// profit in the buy and sell stock
static int maxProfit(int[] prices)
{
    int n = prices.length;
    int[][] v = new int[n][2];

    for(int i = 0; i < v.length; i++)
    {
        v[i][0] = -1;
        v[i][1] = -1;
    }

    // buy = 1 because atmost one
    // transaction is allowed
    return findMaximumProfit(prices, 0, 1, 1, v);
}

// Driver Code
public static void main(String[] args)
{

    // Given prices
    int[] prices = { 7, 1, 5, 3, 6, 4 };

    // Function Call to find the
    // maximum profit possible by
    // buying and selling a single stock
    int ans = maxProfit(prices);

    // Print answer
    System.out.println(ans);
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find maximum profit possible
# by buying and selling at most one stack
def findMaximumProfit(prices, i,  k,
                      buy, v):

    # If no stock can be chosen
    if (i >= len(prices) or k <= 0):
        return 0

    if (v[i][buy] != -1):
        return v[i][buy]

    # If a stock is already bought
    if (buy):
        v[i][buy] = max(-prices[i]
                        + findMaximumProfit(prices, i + 1,
                                            k, not buy, v),
                        findMaximumProfit(prices, i + 1, k,
                                          buy, v))
        return v[i][buy]

    # Otherwise
    else:
        # Buy now
        v[i][buy] = max(prices[i]
                        + findMaximumProfit(
            prices, i + 1, k - 1, not buy, v),
            findMaximumProfit(prices, i + 1, k,
                              buy, v))
        return v[i][buy]

# Function to find the maximum
# profit in the buy and sell stock
def maxProfit(prices):

    n = len(prices)
    v = [[-1 for x in range(2)]for y in range(n)]

    # buy = 1 because atmost one
    # transaction is allowed
    return findMaximumProfit(prices, 0, 1, 1, v)

# Driver Code
if __name__ == "__main__":

    # Given prices
    prices = [7, 1, 5, 3, 6, 4]

    # Function Call to find the
    # maximum profit possible by
    # buying and selling a single stock
    ans = maxProfit(prices)

    # Print answer
    print(ans)
```

## C#

```
// C# program for above approach
using System;

class GFG
{

// Function to find maximum profit possible
// by buying and selling at most one stack
static int findMaximumProfit(int[] prices, int i, int k,
                             int buy, int[,] v)
{

    // If no stock can be chosen
    if (i >= prices.Length || k <= 0)
        return 0;

    if (v[i, buy] != -1)
        return v[i, buy];

    // If a stock is already bought
    // Buy now
    int nbuy;
    if (buy == 1)
        nbuy = 0;
    else
        nbuy = 1;
    if (buy == 1)
    {
        return v[i, buy] = Math.Max(-prices[i] +
         findMaximumProfit(prices, i + 1, k, nbuy, v),
         findMaximumProfit(prices, i + 1, k, (int)(buy), v));
    }

    // Otherwise
    else
    {

        // Buy now
        if (buy == 1)
            nbuy = 0;
        else
            nbuy = 1;
        return v[i, buy] = Math.Max(prices[i] +
         findMaximumProfit(prices, i + 1, k - 1, nbuy, v),
         findMaximumProfit(prices, i + 1, k, buy, v));
    }
}

// Function to find the maximum
// profit in the buy and sell stock
static int maxProfit(int[] prices)
{
    int n = prices.Length;
    int[,] v = new int[n, 2];

    for(int i = 0; i < n; i++)
    {
        v[i, 0] = -1;
        v[i, 1] = -1;
    }

    // buy = 1 because atmost one
    // transaction is allowed
    return findMaximumProfit(prices, 0, 1, 1, v);
}

// Driver Code
public static void Main()
{

    // Given prices
    int[] prices = { 7, 1, 5, 3, 6, 4 };

    // Function Call to find the
    // maximum profit possible by
    // buying and selling a single stock
    int ans = maxProfit(prices);

    // Print answer
    Console.Write(ans);

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to find maximum profit possible
// by buying and selling at most one stack
function findMaximumProfit(prices, i, k, buy, v) {

    // If no stock can be chosen
    if (i >= prices.length || k <= 0)
        return 0;

    if (v[i][buy] != -1)
        return v[i][buy];

    // If a stock is already bought
    // Buy now
    let nbuy;
    if (buy == 1)
        nbuy = 0;
    else
        nbuy = 1;
    if (buy == 1) {
        return v[i][buy] = Math.max(-prices[i] +
            findMaximumProfit(prices, i + 1, k, nbuy, v),
            findMaximumProfit(prices, i + 1, k, buy, v));
    }

    // Otherwise
    else {

        // Buy now
        if (buy == 1)
            nbuy = 0;
        else
            nbuy = 1;
        return v[i][buy] = Math.max(prices[i] +
            findMaximumProfit(prices, i + 1, k - 1, nbuy, v),
            findMaximumProfit(prices, i + 1, k, buy, v));
    }
}

// Function to find the maximum
// profit in the buy and sell stock
function maxProfit(prices) {
    let n = prices.length;
    let v = new Array(n).fill(0).map(() => new Array(2).fill(-1))

    // buy = 1 because atmost one
    // transaction is allowed
    return findMaximumProfit(prices, 0, 1, 1, v);
}

// Driver Code

// Given prices
let prices = [7, 1, 5, 3, 6, 4];

// Function Call to find the
// maximum profit possible by
// buying and selling a single stock
let ans = maxProfit(prices);

// Print answer
document.write(ans);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
5
```

***时间复杂度:** O(N)其中 N 是给定数组的长度。*
***辅助空间:** O(N)*

[**<u>二类:允许无限交易</u>**](https://www.geeksforgeeks.org/stock-buy-sell/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **价格[]** ，代表不同日期股票的价格，任务是使用允许任意数量交易的交易找到不同日期买卖股票的最大可能利润。

**示例:**

> **输入:**价格[] = {7，1，5，3，6，4}
> **输出:** 7
> **说明:**
> 2<sup>日</sup>购买。价格= 1。
> 3<sup>日</sup>日卖出。价格= 5。
> 因此，利润= 5–1 = 4。
> 4<sup>日购买。价格= 3。
> 5<sup>日卖出。价格= 6。
> 因此，利润= 4+(6–3)= 7。</sup></sup>
> 
> **输入:**价格= {1，2，3，4，5}
> **输出:** 4
> **说明:**
> 在 1 <sup>日</sup>购买。价格= 1。
> 第 5 天卖出。价格= 5。
> 因此，利润= 5–1 = 4。

**方法:**想法是保持一个布尔值，表示当前是否有任何正在进行的购买。如果是，那么在目前的状态下，股票可以出售以实现利润最大化，或者在不出售股票的情况下转移到下一个价格。否则，如果没有交易发生，可以不买*而买当前股票或移到下一个价格。*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum
// profit possible by buying or
// selling stocks any number of times
int find(int ind, vector<int>& v, bool buy,
         vector<vector<int> >& memo)
{

    // No prices left
    if (ind >= v.size())
        return 0;

    // Already found
    if (memo[ind][buy] != -1)
        return memo[ind][buy];

    // Already bought, now sell
    if (buy) {
        return memo[ind][buy]
               = max(-v[ind] + find(ind + 1, v, !buy, memo),
                     find(ind + 1, v, buy, memo));
    }

    // Otherwise, buy the stock
    else {
        return memo[ind][buy]
               = max(v[ind] + find(ind + 1, v, !buy, memo),
                     find(ind + 1, v, buy, memo));
    }
}

// Function to find the maximum
// profit possible by buying and
// selling stocks any number of times
int maxProfit(vector<int>& prices)
{
    int n = prices.size();
    if (n < 2)
        return 0;

    vector<vector<int> > v(n + 1, vector<int>(2, -1));
    return find(0, prices, 1, v);
}

// Driver Code
int main()
{

    // Given prices
    vector<int> prices = { 7, 1, 5, 3, 6, 4 };

    // Function Call to calculate
      // maximum profit possible
    int ans = maxProfit(prices);

    // Print the total profit
    cout << ans << endl;
    return 0;
}
```

**Output**

```
7
```

***时间复杂度:** O(N)其中 N 是给定数组的长度。*
***辅助空间:** O(N)*

[**<u>三类:最多允许两笔交易</u>**](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-stock-at-most-twice-set-2/?ref=rp)

**问题:**给定一个长度为 **N** 的数组**价格【】**，表示不同日期股票的价格。任务是使用最多允许两次交易的交易来寻找在不同日期买卖股票的最大可能利润。

**注:**股票必须先买后卖。

> ***输入:**价格[] = {3，3，5，0，0，3，1，4}*
> ***输出:** 6*
> ***解释:***
> *第 4 天买入，第 6 天卖出= >利润= 3 0 = 3*
> *第 7 天买入，第 8 天卖出= >利润= 4 1 = 3 【T19*
> 
> ***输入:**价格[] = {1，2，3，4，5}*
> ***输出:** 4*
> ***解释:***
> *第 1 天买入，第 6 天卖出= >利润= 5 1 = 4*
> *因此，总利润= 4*

**方法:**按照上述方法可以解决问题。现在，如果交易次数等于 2，那么当前利润就可以是想要的答案。同样，通过将所有可能的答案记录到动力定位表中来尝试它们。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find the maximum
// profit in the buy and sell stock
int find(vector<int>& prices, int ind, bool buy, int c,
         vector<vector<vector<int> > >& memo)
{
    // If buy =1 means buy now
    // else sell
    if (ind >= prices.size() || c >= 2)
        return 0;
    if (memo[ind][buy] != -1)
        return memo[ind][buy];

    // Already bought, sell now
    if (buy) {
        return memo[ind][buy]
               = max(-prices[ind]
                         + find(prices, ind + 1, !buy, c,
                                memo),
                     find(prices, ind + 1, buy, c, memo));
    }

    // Can buy stocks
    else {
        return memo[ind][buy]
               = max(prices[ind]
                         + find(prices, ind + 1, !buy,
                                c + 1, memo),
                     find(prices, ind + 1, buy, c, memo));
    }
}

// Function to find the maximum
// profit in the buy and sell stock
int maxProfit(vector<int>& prices)
{
    // Here maximum two transaction are allowed

    // Use 3-D vector because here
    // three states are there: i,k,buy/sell
    vector<vector<vector<int> > > memo(
        prices.size(),
        vector<vector<int> >(2, vector<int>(2, -1)));

    // Answer
    return find(prices, 0, 1, 0, memo);
}

// Driver Code
int main()
{

    // Given prices
    vector<int> prices = { 3, 3, 5, 0, 0, 3, 1, 4 };

    // Function Call
    int ans = maxProfit(prices);

    // Answer
    cout << ans << endl;
    return 0;
}
```

**Output**

```
6
```