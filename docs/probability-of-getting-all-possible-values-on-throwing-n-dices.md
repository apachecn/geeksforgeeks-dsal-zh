# 投掷 N 个骰子获得所有可能值的概率

> 原文:[https://www . geeksforgeeks . org/投掷 n 骰子获得所有可能值的概率/](https://www.geeksforgeeks.org/probability-of-getting-all-possible-values-on-throwing-n-dices/)

给定一个表示骰子点数的整数 **N** ，任务是找出将 **N** 个骰子扔在一起可以得到的每个可能值的概率。

**示例:**

> **输入:** N = 1
> **输出:**
> 1:0.17
> 2:0.17
> 3:0.17
> 4:0.17
> 5:0.17
> 6:0.17
> **说明:**掷骰子时，从[1，6]开始的所有数值出现在顶部的概率为 1/6 = 0.17
> 
> **输入:** N = 2
> **输出:**
> 2:0.028
> 3:0.056
> 4:0.083
> 5:0.11
> 6:0.14
> 7:0.17
> 8:0.14
> 9:0.11
> 10:0.083
> 11:0.056【T11

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和 [DP 表](https://www.geeksforgeeks.org/tabulation-vs-memoization/)存储每个可能值的概率。

*   存储投掷 1 个骰子时出现的所有 6 个数字的概率。
*   现在，对于 N=2，在[2，12]之间的所有可能和的概率等于加起来的两个数各自概率的乘积之和。例如，

> 掷出 2 个骰子概率为 4 =(概率为 1 ) *(概率为 3) +(概率为 2) *(概率为 2) +(概率为 3 ) *(概率为 1)

*   因此对于 N 个骰子，

> 和的概率 S =(1 的概率)*(使用 N -1 个骰子 S–1 的概率)+(2 的概率)*(使用 N-1 个骰子 S–2 的概率)+ …..+(6 的概率)*(使用 N -1 个骰子的 S–6 的概率)

*   因此，为了解决这个问题，我们需要使用自上而下的方法从 2 到 N 填充 dp[][]表，使用以下关系:

> dp[i][x] = dp[1][y] + dp[i-1][z]，其中 x = y + z，I 表示骰子数

*   显示为 N 存储的所有概率作为答案。

下面是上述方法的实现:

## C++

```
// C++ Program to calculate
// the probability of
// all the possible values
// that can be obtained
// throwing N dices

#include <bits/stdc++.h>
using namespace std;

void dicesSum(int n)
{
    // Store the probabilities
    vector<map<int, double> > dp(n + 1);
    // Precompute the probabilities
    // for values possible using 1 dice
    dp[1] = { { 1, 1 / 6.0 },
              { 2, 1 / 6.0 },
              { 3, 1 / 6.0 },
              { 4, 1 / 6.0 },
              { 5, 1 / 6.0 },
              { 6, 1 / 6.0 } };

    // Compute the probabilities
    // for all values from 2 to N
    for (int i = 2; i <= n; i++) {
        for (auto a1 : dp[i - 1]) {
            for (auto a2 : dp[1]) {
                dp[i][a1.first + a2.first]
                    += a1.second * a2.second;
            }
        }
    }
    // Print the result
    for (auto a : dp[n]) {
        cout << a.first << " "
             << setprecision(2)
             << a.second
             << endl;
    }
}

// Driver code
int main()
{
    int n = 2;
    dicesSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// the probability of all the
// possible values that can
// be obtained throwing N dices
import java.io.*;
import java.util.*;

class GFG{

static void dicesSum(int n)
{

    // Store the probabilities
    double[][] dp = new double[n + 1][6 * n + 1];

    // Precompute the probabilities
    // for values possible using 1 dice
    for(int i = 1; i <= 6; i++)
        dp[1][i] = 1 / 6.0;

    // Compute the probabilities
    // for all values from 2 to N
    for(int i = 2; i <= n; i++)
        for(int j = i - 1; j <= 6 * (i - 1); j++)
            for(int k = 1; k <= 6; k++)
            {
                dp[i][j + k] += (dp[i - 1][j] *
                                 dp[1][k]);
            }

    // Print the result
    for(int i = n; i <= 6 * n; i++)
    {
        System.out.println(i + " " +
                           Math.round(dp[n][i] * 1000.0) /
                                                 1000.0);
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 2;

    dicesSum(n);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program to calculate
# the probability of all the
# possible values that can
# be obtained throwing N dices
def diceSum(n):

    # Initialize a 2d array upto
    # (n*total sum possible) sum
    # with value 0
    dp = [[ 0 for j in range(n * 6)]
              for i in range(n + 1)]

    # Store the probability in a
    # single throw for 1,2,3,4,5,6
    for i in range(6):
        dp[1][i] = 1 / 6

    # Compute the probabilities
    # for all values from 2 to N
    for i in range(2, n + 1):
        for j in range(len(dp[i - 1])):
            for k in range(6):

                if (dp[i - 1][j] != 0 and
                    dp[i - 1][k] != 0):
                    dp[i][j + k] += (dp[i - 1][j] *
                                     dp[1][k])

    # Print the result
    for i in range(len(dp[n]) - n + 1):
        print("%d %0.3f" % (i + n, dp[n][i]))

# Driver code
n = 2

# Call the function
diceSum(n)

# This code is contributed by dipesh99kumar
```

## C#

```
// C# program to calculate
// the probability of all the
// possible values that can
// be obtained throwing N dices
using System;
class GFG {

    static void dicesSum(int n)
    {

        // Store the probabilities
        double[,] dp = new double[n + 1,6 * n + 1];

        // Precompute the probabilities
        // for values possible using 1 dice
        for(int i = 1; i <= 6; i++)
            dp[1,i] = 1 / 6.0;

        // Compute the probabilities
        // for all values from 2 to N
        for(int i = 2; i <= n; i++)
            for(int j = i - 1; j <= 6 * (i - 1); j++)
                for(int k = 1; k <= 6; k++)
                {
                    dp[i,j + k] += (dp[i - 1,j] *
                                     dp[1,k]);
                }

        // Print the result
        for(int i = n; i <= 6 * n; i++)
        {
            Console.WriteLine(i + " " +
                               Math.Round(dp[n,i] * 1000.0) /
                                                     1000.0);
        }
    }

  static void Main() {
    int n = 2;

    dicesSum(n);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program to calculate
// the probability of all the
// possible values that can
// be obtained throwing N dices

function dicesSum(n)
{

    // Store the probabilities
    let dp = new Array(n+1);
    for (var i = 0; i < dp.length; i++) {
    dp[i] = new Array(2);
    }
    for (var i = 0; i < dp.length; i++) {
    for (var j = 0; j < 6 * n + 1; j++) {
        dp[i][j] = 0;
    }
    }

    // Precompute the probabilities
    // for values possible using 1 dice
    for(let i = 1; i <= 6; i++)
        dp[1][i] = 1 / 6.0;

    // Compute the probabilities
    // for all values from 2 to N
    for(let i = 2; i <= n; i++)
        for(let j = i - 1; j <= 6 * (i - 1); j++)
            for(let k = 1; k <= 6; k++)
            {
                dp[i][j + k] += (dp[i - 1][j] *
                                 dp[1][k]);
            }

    // Prlet the result
    for(let i = n; i <= 6 * n; i++)
    {
        document.write(i + " " +
                     Math.round(dp[n][i] * 1000.0) /
                                    1000.0 + "<br/>");
    }
}
  // Driver Code

    let n = 2;

    dicesSum(n);

</script>
```

**Output:** 

```
2 0.028
3 0.056
4 0.083
5 0.11
6 0.14
7 0.17
8 0.14
9 0.11
10 0.083
11 0.056
12 0.028
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间:*O(N<sup>2</sup>)*