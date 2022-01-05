# 股票买卖最大化利润的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序换股票-买入-卖出-利润最大化/](https://www.geeksforgeeks.org/javascript-program-for-stock-buy-sell-to-maximize-profit/)

一只股票每天的成本是以数组的形式给出的，找出你在那些日子里通过买卖所能获得的最大利润。例如，如果给定的数组是{100，180，260，310，40，535，695}，则通过在第 0 天买入，在第 3 天卖出可以获得最大利润。再次在第 4 天买入，在第 6 天卖出。如果给定的一系列价格是按递减顺序排序的，那么就根本赚不到利润。

**天真的方法:**一个简单的方法是尝试在每一天盈利的时候买入股票并卖出，并不断更新到目前为止的最大利润。

下面是上述方法的实现:

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to return the maximum profit
// that can be made after buying and
// selling the given stocks
function maxProfit(price, start, end)
{
    // If the stocks can't be bought
    if (end <= start)
        return 0;

    // Initialise the profit
    let profit = 0;

    // The day at which the stock
    // must be bought
    for (let i = start; i < end; i++) 
    {
        // The day at which the
        // stock must be sold
        for (let j = i + 1; j <= end; j++) 
        {
            // If buying the stock at ith day and
            // selling it at jth day is profitable
            if (price[j] > price[i]) 
            {
                // Update the current profit
                let curr_profit = price[j] - price[i] + 
                                  maxProfit(price, 
                                            start, i - 1) + 
                                  maxProfit(price, 
                                            j + 1, end);

                // Update the maximum profit 
                // so far
                profit = Math.max(profit, 
                                  curr_profit);
            }
        }
    }
    return profit;
}

// Driver code
let price = [100, 180, 260, 310,
             40, 535, 695];
let n = price.length;
document.write(maxProfit(
               price, 0, n - 1));
</script>
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

## java 描述语言

```

<script>
// JavaScript program to implement 
// the above approach

// This function finds the buy sell
// schedule for maximum profit
function stockBuySell(price, n) 
{
    // Prices must be given for at 
    // least two days
    if (n == 1)
        return;

    // Traverse through given price array
    let i = 0;
    while (i < n - 1) 
    {
        // Find Local Minima
        // Note that the limit is (n-2) as we 
        // are comparing present element to 
        // the next element
        while ((i < n - 1) && 
               (price[i + 1] <= price[i]))
            i++;

        // If we reached the end, break
        // as no further solution possible
        if (i == n - 1)
            break;

        // Store the index of minima
        let buy = i++;

        // Find Local Maxima
        // Note that the limit is (n-1) as we 
        // are comparing to previous element
        while ((i < n) && 
              (price[i] >= price[i - 1]))
            i++;

        // Store the index of maxima
        let sell = i - 1;

        document.write(`Buy on day: ${buy}   
        Sell on day: ${sell}<br>`);
    }
}

// Driver code
// Stock prices on consecutive days
let price = [100, 180, 260, 
             310, 40, 535, 695];
let n = price.length;

// Function call
stockBuySell(price, n);

// This code is contributed by Potta Lokesh
</script>
```

**输出:**

```
Buy on day: 0     Sell on day: 3
Buy on day: 4     Sell on day: 6
```

**时间复杂度:**外环运行到我变成 n-1。内部两个循环在每次迭代中增加 I 的值。所以总的时间复杂度是 O(n)

更多详情请参考[股票买卖实现利润最大化](https://www.geeksforgeeks.org/stock-buy-sell/)整篇文章！