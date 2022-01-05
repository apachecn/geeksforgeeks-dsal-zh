# 无限背包(允许重复物品)

> 原文:[https://www . geesforgeks . org/无界-背包-重复-物品-允许/](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/)

给定一个背包重量 **W** 和一套具有一定价值*价值<sub>I</sub>T7】和重量*wt<sub>I</sub>T11】的 **n** 物品，我们需要精确计算出能够补足这个数量的最大数量。这与[经典背包问题](https://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)不同，这里允许我们使用一个物品的无限个实例。
**示例:****

```
Input : W = 100
       val[]  = {1, 30}
       wt[] = {1, 50}
Output : 100
There are many ways to fill knapsack.
1) 2 instances of 50 unit weight item.
2) 100 instances of 1 unit weight item.
3) 1 instance of 50 unit weight item and 50
   instances of 1 unit weight items.
We get maximum value with option 2.

Input : W = 8
       val[] = {10, 40, 50, 70}
       wt[]  = {1, 3, 4, 5}       
Output : 110 
We get maximum value with one unit of
weight 5 and one unit of weight 3.
```

这是一个无界背包问题，因为我们可以使用任何资源的一个或多个实例。可以使用一个简单的 1D 数组，比如 dp[W+1]，使得 dp[i]存储使用背包的所有物品和 I 容量所能达到的最大值。请注意，我们在这里使用的是 1D 阵列，这与我们使用 2D 阵列的经典背包不同。这里的项目数量从不改变。我们总是有所有可用的项目。
我们可以用下面的公式递归计算 dp[]

```
dp[i] = 0
dp[i] = max(dp[i], dp[i-wt[j]] + val[j] 
                   where j varies from 0 
                   to n-1 such that:
                   wt[j] <= i

result = d[W]
```

以下是上述想法的实现。

## C++

```
// C++ program to find maximum achievable value
// with a knapsack of weight W and multiple
// instances allowed.
#include<bits/stdc++.h>
using namespace std;

// Returns the maximum value with knapsack of
// W capacity
int unboundedKnapsack(int W, int n,
                       int val[], int wt[])
{
    // dp[i] is going to store maximum value
    // with knapsack capacity i.
    int dp[W+1];
    memset(dp, 0, sizeof dp);

    // Fill dp[] using above recursive formula
    for (int i=0; i<=W; i++)
      for (int j=0; j<n; j++)
         if (wt[j] <= i)
            dp[i] = max(dp[i], dp[i-wt[j]] + val[j]);

    return dp[W];
}

// Driver program
int main()
{
    int W = 100;
    int val[] = {10, 30, 20};
    int wt[] = {5, 10, 15};
    int n = sizeof(val)/sizeof(val[0]);

    cout << unboundedKnapsack(W, n, val, wt);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum achievable
// value with a knapsack of weight W and
// multiple instances allowed.
public class UboundedKnapsack
{

    private static int max(int i, int j)
    {
            return (i > j) ? i : j;
    }

    // Returns the maximum value with knapsack
    // of W capacity
    private static int unboundedKnapsack(int W, int n,
                                int[] val, int[] wt)
    {

        // dp[i] is going to store maximum value
        // with knapsack capacity i.
        int dp[] = new int[W + 1];

        // Fill dp[] using above recursive formula
        for(int i = 0; i <= W; i++){
            for(int j = 0; j < n; j++){
                if(wt[j] <= i){
                    dp[i] = max(dp[i], dp[i - wt[j]] +
                                val[j]);
                }
            }
        }
        return dp[W];
    }

    // Driver program
    public static void main(String[] args)
    {
        int W = 100;
        int val[] = {10, 30, 20};
        int wt[] = {5, 10, 15};
        int n = val.length;
        System.out.println(unboundedKnapsack(W, n, val, wt));
    }
}
// This code is contributed by Aditya Kumar
```

## 蟒蛇 3

```
# Python3 program to find maximum
# achievable value with a knapsack
# of weight W and multiple instances allowed.

# Returns the maximum value
# with knapsack of W capacity
def unboundedKnapsack(W, n, val, wt):

    # dp[i] is going to store maximum
    # value with knapsack capacity i.
    dp = [0 for i in range(W + 1)]

    ans = 0

    # Fill dp[] using above recursive formula
    for i in range(W + 1):
        for j in range(n):
            if (wt[j] <= i):
                dp[i] = max(dp[i], dp[i - wt[j]] + val[j])

    return dp[W]

# Driver program
W = 100
val = [10, 30, 20]
wt = [5, 10, 15]
n = len(val)

print(unboundedKnapsack(W, n, val, wt))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find maximum achievable
// value with a knapsack of weight W and
// multiple instances allowed.
using System;

class UboundedKnapsack {

    private static int max(int i, int j)
    {
            return (i > j) ? i : j;
    }

    // Returns the maximum value
    // with knapsack of W capacity
    private static int unboundedKnapsack(int W, int n,
                                  int []val, int []wt)
    {

        // dp[i] is going to store maximum value
        // with knapsack capacity i.
        int []dp = new int[W + 1];

        // Fill dp[] using above recursive formula
        for(int i = 0; i <= W; i++){
            for(int j = 0; j < n; j++){
                if(wt[j] <= i){
                    dp[i] = Math.Max(dp[i], dp[i -
                                        wt[j]] + val[j]);
                }
            }
        }
        return dp[W];
    }

    // Driver program
    public static void Main()
    {
        int W = 100;
        int []val = {10, 30, 20};
        int []wt = {5, 10, 15};
        int n = val.Length;
        Console.WriteLine(unboundedKnapsack(W, n, val, wt));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// achievable value with a
// knapsack of weight W and
// multiple instances allowed.

// Returns the maximum value
// with knapsack of W capacity
function unboundedKnapsack($W, $n,
                           $val, $wt)
{
    // dp[i] is going to store
    // maximum value with
    // knapsack capacity i.
    for($i = 0; $i <= $W; $i++)
        $dp[$i] = 0;

    $ans = 0;

    // Fill dp[] using above
    // recursive formula
    for ($i = 0; $i <= $W; $i++)
    for ($j = 0; $j < $n; $j++)
        if ($wt[$j] <= $i)
            $dp[$i] = max($dp[$i],
                          $dp[$i - $wt[$j]] +
                                   $val[$j]);

    return $dp[$W];
}

// Driver Code
$W = 100;
$val = array(10, 30, 20);
$wt = array(5, 10, 15);
$n = count($val); //sizeof($val)/sizeof($val[0]);

echo unboundedKnapsack($W, $n,
                       $val, $wt);

// This code is contributed
// by shiv_bhakt
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum achievable
    // value with a knapsack of weight W and
    // multiple instances allowed.

    function max(i, j)
    {
            return (i > j) ? i : j;
    }

    // Returns the maximum value
    // with knapsack of W capacity
    function unboundedKnapsack(W, n, val, wt)
    {

        // dp[i] is going to store maximum value
        // with knapsack capacity i.
        let dp = new Array(W + 1);
        dp.fill(0);

        // Fill dp[] using above recursive formula
        for(let i = 0; i <= W; i++){
            for(let j = 0; j < n; j++){
                if(wt[j] <= i){
                    dp[i] = Math.max(dp[i], dp[i - wt[j]] + val[j]);
                }
            }
        }
        return dp[W];
    }

    let W = 100;
    let val = [10, 30, 20];
    let wt = [5, 10, 15];
    let n = val.length;
    document.write(unboundedKnapsack(W, n, val, wt));

</script>
```

**输出:**

```
300
```

本文使用来自[](https://www.facebook.com/Shubh1307)****舒巴姆·乔希**和**阿希什·库马尔**的输入进行编辑。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。**