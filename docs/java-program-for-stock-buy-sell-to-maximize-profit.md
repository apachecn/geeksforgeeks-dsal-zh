# 用于股票买卖以最大化利润的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序换股票-买入-卖出-利润最大化/](https://www.geeksforgeeks.org/java-program-for-stock-buy-sell-to-maximize-profit/)

一只股票每天的成本是以数组的形式给出的，找出你在那些日子里通过买卖所能获得的最大利润。例如，如果给定的数组是{100，180，260，310，40，535，695}，则通过在第 0 天买入，在第 3 天卖出可以获得最大利润。再次在第 4 天买入，在第 6 天卖出。如果给定的一系列价格是按递减顺序排序的，那么就根本赚不到利润。

**天真的方法:**一个简单的方法是尝试在每一天盈利的时候买入股票并卖出，并不断更新到目前为止的最大利润。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG{

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
static int maxProfit(int price[], 
                     int start, int end)
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
                int curr_profit = price[j] - price[i] + 
                                  maxProfit(price, 
                                            start, i - 1) + 
                                  maxProfit(price, 
                                            j + 1, end);

                // Update the maximum profit so far
                profit = Math.max(profit, 
                                  curr_profit);
            }
        }
    }
    return profit;
}

// Driver code
public static void main(String[] args)
{
    int price[] = {100, 180, 260, 310,
                   40, 535, 695};
    int n = price.length;
    System.out.print(maxProfit(
                     price, 0, n - 1));
}
}
// This code is contributed by PrinciRaj1992
```

**输出:**

```
865
```

**高效方法:**如果只允许我们买卖一次，那么我们可以使用以下算法。[两个元素之间的最大差异](https://www.geeksforgeeks.org/maximum-difference-between-two-elements/)。在这里，我们可以多次买卖。
下面是这个问题的算法。

1.  找到局部最小值并将其存储为起始索引。如果不存在，返回。
2.  找到局部极大值。并将其存储为结束索引。如果我们到达终点，将终点设置为终点索引。
3.  更新解决方案(增加买卖对的计数)
4.  如果没有到达终点，重复上述步骤。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find best buying and 
// selling days
import java.util.ArrayList;

// Solution structure
class Interval 
{
    int buy, sell;
}

class StockBuySell 
{
    // This function finds the buy sell 
    // schedule for maximum profit
    void stockBuySell(int price[], int n)
    {
        // Prices must be given for at least 
        // two days
        if (n == 1)
            return;

        int count = 0;

        // Solution array
        ArrayList<Interval> sol = 
                  new ArrayList<Interval>();

        // Traverse through given price array
        int i = 0;
        while (i < n - 1) 
        {
            // Find Local Minima. Note that the 
            // limit is (n-2) as we are comparing 
            // present element to the next element.
            while ((i < n - 1) && 
                   (price[i + 1] <= price[i]))
                i++;

            // If we reached the end, break as no 
            // further solution possible
            if (i == n - 1)
                break;

            Interval e = new Interval();
            e.buy = i++;
            // Store the index of minima

            // Find Local Maxima.  Note that the 
            // limit is (n-1) as we are comparing 
            // to previous element
            while ((i < n) && 
                   (price[i] >= price[i - 1]))
                i++;

            // Store the index of maxima
            e.sell = i - 1;
            sol.add(e);

            // Increment number of buy/sell
            count++;
        }

        // print solution
        if (count == 0)
            System.out.println(
            "There is no day when buying the stock " + 
            "will make profit");
        else
            for (int j = 0; j < count; j++)
                System.out.println(
                "Buy on day: " + sol.get(j).buy + 
                "        " + "Sell on day : " + 
                sol.get(j).sell);

        return;
    }

    // Driver code
    public static void main(String args[])
    {
        StockBuySell stock = new StockBuySell();

        // stock prices on consecutive days
        int price[] = {100, 180, 260, 
                       310, 40, 535, 695};
        int n = price.length;

        // function call
        stock.stockBuySell(price, n);
    }
}
// This code is contributed by Mayank Jaiswal
```

**输出:**

```
Buy on day: 0     Sell on day: 3
Buy on day: 4     Sell on day: 6
```

**时间复杂度:**外环运行到我变成 n-1。内部两个循环在每次迭代中增加 I 的值。所以总的时间复杂度是 O(n)

**谷峰进场:**

在这种方法中，我们只需要找到下一个更大的元素，并从当前元素中减去它，这样差异就会不断增加，直到达到最小值。如果序列是递减序列，那么最大可能利润为 0。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG 
{
    static int maxProfit(int prices[], 
                         int size)
    {    
        // maxProfit adds up the difference 
        // between adjacent elements if they 
        // are in increasing order
        int maxProfit = 0;

        // The loop starts from 1 as its 
        // comparing with the previous
        for (int i = 1; i < size; i++)
            if (prices[i] > prices[i - 1])
                maxProfit += prices[i] - prices[i - 1];
        return maxProfit;
    }

    // Driver code
    public static void main(String[] args)
    {    
        // stock prices on consecutive days
        int price[] = {100, 180, 260, 
                       310, 40, 535, 695};
        int n = price.length;

        // function call
        System.out.println(maxProfit(price, n));
    }
}
// This code is contributed by rajsanghavi9.
```

**输出:**

```
865
```

**时间复杂度**:O(n)
T3】辅助 T5】空间: O(1)

本文由 [Ashish Anand](https://www.facebook.com/aasshishh?fref=ts) 编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。