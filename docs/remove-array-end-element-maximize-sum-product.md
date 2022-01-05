# 移除数组结束元素，使乘积之和最大化

> 原文:[https://www . geesforgeks . org/remove-array-end-element-maximum-sum-product/](https://www.geeksforgeeks.org/remove-array-end-element-maximize-sum-product/)

给定一个正整数数组。我们可以从两端中的任何一端移除元素，即从数组的左侧或右侧移除。每次我们移除一个元素，分数都会增加元素的值*(已经移除的元素数+ 1)。任务是找到通过移除所有元素可以获得的最大分数。
**例:**

```
Input : arr[] = { 1, 3, 1, 5, 2 }.
Output : 43
Remove 1 from left side (score = 1*1 = 1)
then remove 2, score = 1 + 2*2 = 5
then remove 3, score = 5 + 3*3 = 14
then remove 1, score = 14 + 1*4 = 18
then remove 5, score = 18 + 5*5 = 43.

Input :  arr[] = { 1, 2 }
Output : 5.
```

想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。制作一个名为 dp[][]的 2D 矩阵，用 0 初始化，其中 dp[i][j]表示从数组的索引 I 到索引 j 的最大得分值。因此，我们的最终结果将存储在 dp[0][n-1]中。
现在，dp[i][j]的值将是 arr[i] *(已经移除的元素数+ 1) + dp[i+ 1][j]或 arr[j] *(已经移除的元素数+1)+DP[I][j–1]的最大值。
以下是本办法的实施:

## C++

```
// CPP program to find maximum score we can get
// by removing elements from either end.
#include <bits/stdc++.h>
#define MAX 50
using namespace std;

int solve(int dp[][MAX], int a[], int low, int high,
                                          int turn)
{
    // If only one element left.
    if (low == high)
        return a[low] * turn;

    // If already calculated, return the value.
    if (dp[low][high] != 0)
        return dp[low][high];

    // Computing Maximum value when element at
    // index i and index j is to be choosed.
    dp[low][high] = max(a[low] * turn + solve(dp, a,
                            low + 1, high, turn + 1),
                        a[high] * turn + solve(dp, a,
                           low, high - 1, turn + 1));

    return dp[low][high];
}

// Driven Program
int main()
{
    int arr[] = { 1, 3, 1, 5, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int dp[MAX][MAX];
    memset(dp, 0, sizeof(dp));

    cout << solve(dp, arr, 0, n - 1, 1) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum score we can get
// by removing elements from either end.

public class GFG {

    static final int MAX = 50;

    static int solve(int dp[][], int a[], int low, int high,
            int turn) {
        // If only one element left.
        if (low == high) {
            return a[low] * turn;
        }

        // If already calculated, return the value.
        if (dp[low][high] != 0) {
            return dp[low][high];
        }

        // Computing Maximum value when element at
        // index i and index j is to be choosed.
        dp[low][high] = Math.max(a[low] * turn + solve(dp, a,
                low + 1, high, turn + 1),
                a[high] * turn + solve(dp, a,
                        low, high - 1, turn + 1));

        return dp[low][high];
    }

// Driven Program
    public static void main(String args[]) {
        int arr[] = {1, 3, 1, 5, 2};
        int n = arr.length;

        int dp[][] = new int[MAX][MAX];

        System.out.println(solve(dp, arr, 0, n - 1, 1));

    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to find maximum
# score we can get by removing
# elements from either end.
MAX = 50

def solve(dp, a, low, high, turn):

    # If only one element left.
    if (low == high):
        return a[low] * turn

    # If already calculated,
    # return the value.
    if (dp[low][high] != 0):
        return dp[low][high]

    # Computing Maximum value when element 
    # at index i and index j is to be choosed.
    dp[low][high] = max(a[low] * turn + solve(dp, a,
                          low + 1, high, turn + 1),
                        a[high] * turn + solve(dp, a,
                          low, high - 1, turn + 1));

    return dp[low][high]

# Driver Code
if __name__ == "__main__":
    arr = [ 1, 3, 1, 5, 2 ]
    n = len(arr)

    dp = [[0 for x in range(MAX)]
             for y in range(MAX)]

    print(solve(dp, arr, 0, n - 1, 1))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find maximum score we can get
// by removing elements from either end.
using System;

class GFG
{
    static int MAX = 50;

    static int solve(int[,] dp, int[] a, int low,
                            int high, int turn)
    {
        // If only one element left.
        if (low == high)
            return a[low] * turn;

        // If already calculated, return the value.
        if (dp[low, high] != 0)
            return dp[low, high];

        // Computing Maximum value when element at
        // index i and index j is to be choosed.
        dp[low,high] = Math.Max(a[low] * turn + solve(dp, a,
                                low + 1, high, turn + 1),
                            a[high] * turn + solve(dp, a,
                            low, high - 1, turn + 1));

        return dp[low, high];
    }

    // Driven code
    static void Main()
    {
        int[] arr = new int[]{ 1, 3, 1, 5, 2 };
        int n = arr.Length;

        int[,] dp = new int[MAX,MAX];
        for(int i = 0; i < MAX; i++)
            for(int j = 0; j < MAX; j++)
                dp[i, j] = 0;

        Console.Write(solve(dp, arr, 0, n - 1, 1));
    }
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum score we can
// get by removing elements from either end.

$MAX = 50 ;

function solve($dp, $a, $low, $high, $turn)
{
    // If only one element left.
    if ($low == $high)
        return $a[$low] * $turn;

    // If already calculated, return the value.
    if ($dp[$low][$high] != 0)
        return $dp[$low][$high];

    // Computing Maximum value when element at
    // index i and index j is to be choosed.
    $dp[$low][$high] = max($a[$low] * $turn +
                     solve($dp, $a, $low + 1,
                           $high, $turn + 1),
                           $a[$high] * $turn +
                     solve($dp, $a, $low, $high -
                                 1, $turn + 1));

    return $dp[$low][$high];
}

// Driver Code
$arr = array(1, 3, 1, 5, 2 ) ;
$n = count($arr) ;

$dp = array() ;
for($i = 0; $i < $MAX ; $i++)
{
    $dp[$i] = array_fill($i, $MAX, 0) ;
}

echo solve($dp, $arr, 0, $n - 1, 1);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum score we can get
// by removing elements from either end.

let MAX = 50;

    function solve(dp, a, low, high,
            turn) {
        // If only one element left.
        if (low == high) {
            return Math.floor(a[low] * turn);
        }

        // If already calculated, return the value.
        if (dp[low][high] != 0) {
            return dp[low][high];
        }

        // Computing Maximum value when element at
        // index i and index j is to be choosed.
        dp[low][high] = Math.max(Math.floor(a[low] * turn )+ solve(dp, a,
                low + 1, high, turn + 1),
                Math.floor(a[high] * turn) + solve(dp, a,
                        low, high - 1, turn + 1));

        return dp[low][high];
    }

// driver function

        let arr = [1, 3, 1, 5, 2];
        let n = arr.length;

        let dp = new Array(MAX);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        for (var i = 0; i < dp.length; i++) {
        for (var j = 0; j < dp.length; j++) {
            dp[i][j] = 0;
        }
        }

        document.write(solve(dp, arr, 0, n - 1, 1));

   // This code is contributed by susmitakundugoaldanga.
</script>   
```

**输出:**

```
43
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。