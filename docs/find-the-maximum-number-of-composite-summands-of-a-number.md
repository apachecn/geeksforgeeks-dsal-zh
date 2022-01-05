# 求一个数的最大合成和数

> 原文:[https://www . geeksforgeeks . org/find-最大复合数-summands-of-number/](https://www.geeksforgeeks.org/find-the-maximum-number-of-composite-summands-of-a-number/)

给定一个整数 N(1<=N<=10^9).任务是将 N 表示为最大可能合成和数的和，如果没有这样的分裂，打印这个最大值，或者打印-1。可以有多个查询

**示例:**

```
Input : 12
Output : 3
Explanation : 12 can be written has 4 + 4 + 4 or 6 + 6 or 8 + 4
But, 4 + 4 + 4 has maximum number of summands.

Input : 7
Output : -1
```

**逼近**:注意最小合成数等于 4。所以在一个大数字的分裂中会有很多 4 是很符合逻辑的。让我们写出小数字(1 < =M < =N) dp <sub>N</sub> 是 N 的分裂中复合和的个数
让我们找出从 1 到 15 的所有数字的答案。几个观察结果:

1.  最佳分裂只有 4，6，9 个。
2.  多次使用 6 或 9 是无益的，因为 6 + 6 = 4 + 4 + 4，9 + 9 = 6 + 6 + 6。
3.  12，13，14，15 有有效的分裂。

让我们证明所有大于 15 的数在最优分裂中都有 4。让我们猜测它是不正确的。如果分裂中的最小数既不是 4，也不是 6，也不是 9，那么这个数通过归纳会有一些非平凡的分裂。
如果这个数字是 6 或 9，我们将减少这个数字的查询，那么我们迟早会得到一些小数字(小于或等于 15)。小数字没有分裂，或者分裂中包含 4(与第一个数字的极小性相矛盾)，或者包含 6 和 9。所以我们在任何情况下都有矛盾。
我们可以从任何大查询中减去 4，我们的解决方案是正确的。
如果我们的查询 n 是小数字，那么我们打印 dp <sub>n</sub> 。否则，让我们找到最小数 k，这样 n–4k 就是一个小数。然后打印 k+DP<sub>n</sub>–4k。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

const int maxn = 16;

// Function to generate the dp array
vector<int> precompute()
{
    vector<int> dp(maxn, -1);
    dp[0] = 0;

    for (int i = 1; i < maxn; ++i) {

        // combination of three integers
        for (auto j : vector<int>{ 4, 6, 9 }) {

            // take the maximum number of summands
            if (i >= j && dp[i - j] != -1) {
                dp[i] = max(dp[i], dp[i - j] + 1);
            }
        }
    }

    return dp;
}

// Function to find the maximum number of summands
int Maximum_Summands(vector<int> dp, int n)
{
    // If n is a smaller number, less than 16
    // return dp[n]
    if (n < maxn)
        return dp[n];

    else {

        // Else, find a minimal number t
        // as explained in solution
        int t = (n - maxn) / 4 + 1;
        return t + dp[n - 4 * t];
    }
}

// Driver code
int main()
{
    int n = 12;

    // Generate dp array
    vector<int> dp = precompute();

    cout << Maximum_Summands(dp, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

static int maxn = 16;

// Function to generate the dp array
static int[] precompute()
{
int dp[] = new int[maxn], arr[]={ 4, 6, 9 };

// initialize
for(int i = 0; i < maxn; i++)dp[i] = -1;

dp[0] = 0;

for (int i = 1; i < maxn; ++i)
{

    // combination of three integers
    for (int k = 0; k < 3; k++)
    {
        int j = arr[k];

        // take the maximum number of summands
        if (i >= j && dp[i - j] != -1)
        {
            dp[i] = Math.max(dp[i], dp[i - j] + 1);
        }
    }
}

return dp;
}

// Function to find the maximum number of summands
static int Maximum_Summands(int[] dp, int n)
{
// If n is a smaller number, less than 16
// return dp[n]
if (n < maxn)
    return dp[n];

else {

    // Else, find a minimal number t
    // as explained in solution
    int t = (n - maxn) / 4 + 1;
    return t + dp[n - 4 * t];
}
}

// Driver code
public static void main(String args[])
{
    int n = 12;

    // Generate dp array
    int[] dp = precompute();

    System.out.println(Maximum_Summands(dp, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the above approach
global maxn
maxn = 16

# Function to generate the dp array
def precompute():
    dp = [-1 for i in range(maxn)]
    dp[0] = 0

    v = [4, 6, 9]

    for i in range(1, maxn, 1):

        # combination of three integers
        for k in range(3):
            j = v[k]

            # take the maximum number of summands
            if (i >= j and dp[i - j] != -1):
                dp[i] = max(dp[i], dp[i - j] + 1)

    return dp

# Function to find the maximum number of summands
def Maximum_Summands(dp, n):

    # If n is a smaller number,
    # less than 16, return dp[n]
    if (n < maxn):
        return dp[n]

    else:

        # Else, find a minimal number t
        # as explained in solution
        t = int((n - maxn) / 4)+ 1
        return t + dp[n - 4 * t]

# Driver code
if __name__ == '__main__':
    n = 12

    # Generate dp array
    dp = precompute()

    print(Maximum_Summands(dp, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;

class GFG
{

static int maxn = 16;
static int[] dp = new int[maxn + 1];

// Function to generate the dp array
static void precompute()
{
    for(int i = 0; i <= maxn; i++)
    dp[i] = -1;
    dp[0] = 0;
    int[] vec = { 4, 6, 9 };
    for (int i = 1; i < maxn; ++i)
    {

        // combination of three integers
        foreach (int j in vec)
        {

            // take the maximum number of summands
            if (i >= j && dp[i - j] != -1)
            {
                dp[i] = Math.Max(dp[i], dp[i - j] + 1);
            }
        }
    }

}

// Function to find the maximum number of summands
static int Maximum_Summands(int n)
{
    // If n is a smaller number, less than 16
    // return dp[n]
    if (n < maxn)
        return dp[n];

    else
    {

        // Else, find a minimal number t
        // as explained in solution
        int t = (n - maxn) / 4 + 1;
        return t + dp[n - 4 * t];
    }
}

// Driver code
static void Main()
{
    int n = 12;

    // Generate dp array
    precompute();

    Console.WriteLine(Maximum_Summands(n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$maxn = 16;

// Function to generate the dp array
function precompute()
{
    $dp = array_fill(0, $GLOBALS['maxn'], -1);
    $dp[0] = 0;

    $v = array(4, 6, 9);
    for ($i = 1;
         $i < $GLOBALS['maxn']; ++$i)
    {

        // combination of three integers
        for ($k = 0; $k<3 ;$k++)
        {
            $j = $v[$k];

            // take the maximum number of summands
            if ($i >= $j && $dp[$i - $j] != -1)
            {
                $dp[$i] = max($dp[$i],
                              $dp[$i - $j] + 1);
            }
        }
    }

    return $dp;
}

// Function to find the maximum
// number of summands
function Maximum_Summands($dp, $n)
{
    // If n is a smaller number,
    // less than 16 return dp[n]
    if ($n < $GLOBALS['maxn'])
        return $dp[$n];

    else
    {

        // Else, find a minimal number t
        // as explained in solution
        $t = ($n - $GLOBALS['maxn']) / 4 + 1;
        return $t + $dp[$n - 4 * $t];
    }
}

// Driver code
$n = 12;

// Generate dp array
$dp = precompute();

echo Maximum_Summands($dp, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    let maxn = 16;

    // Function to generate the dp array
    function precompute()
    {
        let dp = new Array(maxn);
        let arr = [ 4, 6, 9 ];

        // initialize
        for(let i = 0; i < maxn; i++)
            dp[i] = -1;

        dp[0] = 0;

        for (let i = 1; i < maxn; ++i)
        {

            // combination of three integers
            for (let k = 0; k < 3; k++)
            {
                let j = arr[k];

                // take the maximum number of summands
                if (i >= j && dp[i - j] != -1)
                {
                    dp[i] = Math.max(dp[i], dp[i - j] + 1);
                }
            }
        }

        return dp;
    }

    // Function to find the maximum number of summands
    function Maximum_Summands(dp, n)
    {
        // If n is a smaller number, less than 16
        // return dp[n]
        if (n < maxn)
            return dp[n];

        else {

            // Else, find a minimal number t
            // as explained in solution
            let t = parseInt((n - maxn) / 4, 10) + 1;
            return t + dp[n - 4 * t];
        }
    }

    let n = 12;

    // Generate dp array
    let dp = precompute();

    document.write(Maximum_Summands(dp, n));

</script>
```

**Output:** 

```
3
```