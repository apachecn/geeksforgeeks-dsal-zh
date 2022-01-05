# 过生活问题

> 原文:[https://www.geeksforgeeks.org/lead-a-life-problem/](https://www.geeksforgeeks.org/lead-a-life-problem/)

你将在俄罗斯的萨马拉工作几天。每天都有新的单位工作工资和新的单位食物成本。工作 1 单位消耗 1 单位能量，吃 1 单位食物增加 1 单位能量。以下是你工作的一些说明:

*   你到达的时候没有钱，但是精力充沛。
*   你永远不会有比到达时更多的能量，也永远不会是消极的。
*   你可以每天做任何量的工作(可能根本不做任何工作)，只受你精力的限制。
*   当你的能量为零时，你就不能工作。你可以每天吃任何数量的食物(可能根本没有任何食物)，受限于你拥有的金钱。
*   当你的钱为零时，你不能吃东西。你可以在一天结束时吃东西，吃完东西就不能回去工作了。
*   你可以第二天回去工作。

你真正的目标是带着尽可能多的钱回家。计算你能带回家的最大金额。

**示例:**

> **输入:** N = 3，收益=[1，2，4]，成本[]=[1，3，6]，E = 5
> **输出:** 20
> **说明:**
> 第 1 天:1 个单位工作值 1，1 个单位食物成本 1。今天没有上班的经济动力。
> 第 2 天:1 个单位工作赚 2，1 个单位食物花 3。因此，你花在吃饭上的钱比总收入还多，所以这一天没有去上班的经济动机。
> 第三天:你每单位工作赚 4 个单位。今天食物的价格无关紧要，因为你下班后就直接回家了。
> 你把所有的精力都花在工作上，工资是 5 × 4 = 20 单位钱，回家不买晚饭。
> 
> **输入:** N=2，收益=[1，2]，成本=[1，4]，E=5
> **输出:**利润总额= 0 + 10 = 10
> **说明:**
> 第一天:跳过
> 第二天:5*2=10

**方法:**方法是遍历给定的**收益**数组和**成本**数组，计算每天的净利润。以下是步骤:

1.  对于**收益【】**和**成本【】**中的每个元素，将**收益【I】**与**成本【I】**进行比较。
2.  如果**收入【I】小于或等于成本【I】**，那么**就跳过当天的工作**，因为费用成本大于收入。因此，根本没有利润。
3.  如果**收益【I】大于成本【I】**，将当天收益乘以总能量单位计算总收益，然后减去当天食物成本和能量单位的乘积，计算当天利润。
4.  如果有最后一个工作日，那么通过将当天的收入乘以总能量单位来计算总收入，这将是你当天的利润，因为工作不再需要更多的能量。
5.  打印上述步骤后的利润总额。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function that calculates the profit
// with the earning and cost of expenses
int calculateProfit(int n, int* earnings,
                    int* cost, int e)
{
    // To store the total Profit
    int profit = 0;

    // Loop for n number of days
    for (int i = 0; i < n; i++) {

        int earning_per_day = 0;
        int daily_spent_food = 0;

        // If last day, no need to buy food
        if (i == (n - 1)) {
            earning_per_day = earnings[i] * e;
            profit = profit + earning_per_day;
            break;
        }

        // Else buy food to gain
        // energy for next day
        if (cost[i] < earnings[i]) {

            // Update earning per day
            earning_per_day = earnings[i] * e;
            daily_spent_food = cost[i] * e;

            // Update profit with daily spent
            profit = profit + earning_per_day
                     - daily_spent_food;
        }
    }

    // Print the profit
    cout << profit << endl;
}

// Driver Code
int main()
{
    // Given days
    int n = 4;

    // Given earnings
    int earnings[] = { 1, 8, 6, 7 };

    // Given cost
    int cost[] = { 1, 3, 4, 1 };

    // Given energy e
    int e = 5;

    // Function Call
    calculateProfit(n, earnings, cost, e);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function that calculates the profit
// with the earning and cost of expenses
static void calculateProfit(int n, int []earnings,
                            int []cost, int e)
{

    // To store the total Profit
    int profit = 0;

    // Loop for n number of days
    for(int i = 0; i < n; i++)
    {
        int earning_per_day = 0;
        int daily_spent_food = 0;

        // If last day, no need to buy food
        if (i == (n - 1))
        {
            earning_per_day = earnings[i] * e;
            profit = profit + earning_per_day;
            break;
        }

        // Else buy food to gain
        // energy for next day
        if (cost[i] < earnings[i])
        {

            // Update earning per day
            earning_per_day = earnings[i] * e;
            daily_spent_food = cost[i] * e;

            // Update profit with daily spent
            profit = profit + earning_per_day -
                              daily_spent_food;
        }
    }

    // Print the profit
    System.out.print(profit + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given days
    int n = 4;

    // Given earnings
    int earnings[] = { 1, 8, 6, 7 };

    // Given cost
    int cost[] = { 1, 3, 4, 1 };

    // Given energy e
    int e = 5;

    // Function call
    calculateProfit(n, earnings, cost, e);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that calculates the profit
# with the earning and cost of expenses
def calculateProfit(n, earnings, cost, e):

    # To store the total Profit
    profit = 0;

    # Loop for n number of days
    for i in range(n):
        earning_per_day = 0;
        daily_spent_food = 0;

        # If last day, no need to buy food
        if (i == (n - 1)):
            earning_per_day = earnings[i] * e;
            profit = profit + earning_per_day;
            break;

        # Else buy food to gain
        # energy for next day
        if (cost[i] < earnings[i]):

            # Update earning per day
            earning_per_day = earnings[i] * e;
            daily_spent_food = cost[i] * e;

            # Update profit with daily spent
            profit = (profit + earning_per_day -
                               daily_spent_food);

    # Print the profit
    print(profit);

# Driver Code
if __name__ == '__main__':

    # Given days
    n = 4;

    # Given earnings
    earnings = [ 1, 8, 6, 7 ];

    # Given cost
    cost = [ 1, 3, 4, 1 ];

    # Given energy e
    e = 5;

    # Function call
    calculateProfit(n, earnings, cost, e);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that calculates the profit
// with the earning and cost of expenses
static void calculateProfit(int n, int []earnings,
                            int []cost, int e)
{

    // To store the total Profit
    int profit = 0;

    // Loop for n number of days
    for(int i = 0; i < n; i++)
    {
        int earning_per_day = 0;
        int daily_spent_food = 0;

        // If last day, no need to buy food
        if (i == (n - 1))
        {
            earning_per_day = earnings[i] * e;
            profit = profit + earning_per_day;
            break;
        }

        // Else buy food to gain
        // energy for next day
        if (cost[i] < earnings[i])
        {

            // Update earning per day
            earning_per_day = earnings[i] * e;
            daily_spent_food = cost[i] * e;

            // Update profit with daily spent
            profit = profit + earning_per_day -
                              daily_spent_food;
        }
    }

    // Print the profit
    Console.Write(profit + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given days
    int n = 4;

    // Given earnings
    int []earnings = { 1, 8, 6, 7 };

    // Given cost
    int []cost = { 1, 3, 4, 1 };

    // Given energy e
    int e = 5;

    // Function call
    calculateProfit(n, earnings, cost, e);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function that calculates the profit
// with the earning and cost of expenses
function calculateProfit(n, earnings, cost, e)
{

    // To store the total Profit
    let profit = 0;

    // Loop for n number of days
    for(let i = 0; i < n; i++)
    {
        let earning_per_day = 0;
        let daily_spent_food = 0;

        // If last day, no need to buy food
        if (i == (n - 1))
        {
            earning_per_day = earnings[i] * e;
            profit = profit + earning_per_day;
            break;
        }

        // Else buy food to gain
        // energy for next day
        if (cost[i] < earnings[i])
        {

            // Update earning per day
            earning_per_day = earnings[i] * e;
            daily_spent_food = cost[i] * e;

            // Update profit with daily spent
            profit = profit + earning_per_day -
                              daily_spent_food;
        }
    }

    // Print the profit
    document.write(profit );
}

// Driver Code

     // Given days
    let n = 4;

    // Given earnings
    let earnings = [ 1, 8, 6, 7 ];

    // Given cost
    let cost = [ 1, 3, 4, 1 ];

    // Given energy e
    let e = 5;

    // Function call
    calculateProfit(n, earnings, cost, e);

</script>
```

**Output:** 

```
70
```

***时间复杂度:** O(N)，其中 N 为天数*
***辅助空间:** O(1)*