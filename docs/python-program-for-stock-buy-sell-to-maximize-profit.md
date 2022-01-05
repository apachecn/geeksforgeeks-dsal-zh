# Python 程序，用于股票买卖以实现利润最大化

> 原文:[https://www . geesforgeks . org/python-程序换股票-买入-卖出-利润最大化/](https://www.geeksforgeeks.org/python-program-for-stock-buy-sell-to-maximize-profit/)

一只股票每天的成本是以数组的形式给出的，找出你在那些日子里通过买卖所能获得的最大利润。例如，如果给定的数组是{100，180，260，310，40，535，695}，则通过在第 0 天买入，在第 3 天卖出可以获得最大利润。再次在第 4 天买入，在第 6 天卖出。如果给定的一系列价格是按递减顺序排序的，那么就根本赚不到利润。

**天真的方法:**一个简单的方法是尝试在每一天盈利的时候买入股票并卖出，并不断更新到目前为止的最大利润。

下面是上述方法的实现:

## 蟒蛇 3

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
                curr_profit = price[j] - price[i] +
                              maxProfit(price, 
                                        start, i - 1)+ 
                              maxProfit(price, 
                                        j + 1, end);

                # Update the maximum profit so far
                profit = max(profit, curr_profit);

    return profit;

# Driver code
if __name__ == '__main__':
    price = [100, 180, 260, 
             310, 40, 535, 695];
    n = len(price);
    print(maxProfit(price, 0, n - 1));
# This code is contributed by Rajput-Ji
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

## 蟒蛇 3

```
# Python3 Program to find 
# best buying and selling days

# This function finds the buy sell
# schedule for maximum profit
def stockBuySell(price, n):

    # Prices must be given for at 
    # least two days
    if (n == 1):
        return

    # Traverse through given price array
    i = 0
    while (i < (n - 1)):

        # Find Local Minima
        # Note that the limit is (n-2) as 
        # we are comparing present element 
        # to the next element
        while ((i < (n - 1)) and 
                (price[i + 1] <= price[i])):
            i += 1

        # If we reached the end, break
        # as no further solution possible
        if (i == n - 1):
            break

        # Store the index of minima
        buy = i
        i += 1

        # Find Local Maxima
        # Note that the limit is (n-1) as we are
        # comparing to previous element
        while ((i < n) and 
               (price[i] >= price[i - 1])):
            i += 1

        # Store the index of maxima
        sell = i - 1

        print("Buy on day: ",buy,"    ",
                "Sell on day: ",sell)

# Driver code

# Stock prices on consecutive days
price = [100, 180, 260, 
         310, 40, 535, 695]
n = len(price)

# Function call
stockBuySell(price, n)
# This is code contributed by SHUBHAMSINGH10
```

**输出:**

```
Buy on day: 0     Sell on day: 3
Buy on day: 4     Sell on day: 6
```

**时间复杂度:**外环运行到我变成 n-1。内部两个循环在每次迭代中增加 I 的值。所以总的时间复杂度是 O(n)

**谷峰进场:**

在这种方法中，我们只需要找到下一个更大的元素，并从当前元素中减去它，这样差异就会不断增加，直到达到最小值。如果序列是递减序列，那么最大可能利润为 0。

## 蟒蛇 3

```
# Python3 program for the 
# above approach
def max_profit(prices: list, 
               days: int) -> int:
    profit = 0

    for i in range(1, days):

        # Checks if elements are adjacent 
        # and in increasing order
        if prices[i] > prices[i-1]:

            # Difference added to 'profit'
            profit += prices[i] - prices[i-1]

    return profit

# Driver Code
if __name__ == '__main__':

    # Stock prices on consecutive days
    prices = [100, 180, 260, 
              310, 40, 535, 695]

    # Function call
    profit = max_profit(prices, len(prices))
    print(profit)

 # This code is contributed by vishvofficial.
```

**输出:**

```
865
```

**时间复杂度**:O(n)
T3】辅助 T5】空间: O(1)

更多详情请参考[股票买卖实现利润最大化](https://www.geeksforgeeks.org/stock-buy-sell/)整篇文章！