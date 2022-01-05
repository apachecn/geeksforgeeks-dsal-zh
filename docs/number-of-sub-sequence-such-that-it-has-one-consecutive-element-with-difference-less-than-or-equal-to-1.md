# 子序列的编号，使其具有一个差值小于或等于 1 的连续元素

> 原文:[https://www . geesforgeks . org/子序列数-这样它就有一个连续的差小于或等于 1 的元素/](https://www.geeksforgeeks.org/number-of-sub-sequence-such-that-it-has-one-consecutive-element-with-difference-less-than-or-equal-to-1/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是找出具有至少两个连续元素的子序列的数量，使得它们之间的绝对差值为 **≤ 1** 。

**示例:**

> **输入:** arr[] = {1，6，2，1}
> **输出:** 6
> {1，2}、{1，2，1}、{2，1}、{6，2，1}、{1，1}和{1，6，2，1}
> 是至少有一个连续对
> 差异小于或等于 1 的子序列。
> 
> **输入:** arr[] = {1，6，2，1，9}
> **输出:** 12

**天真的做法:**思路是找出所有可能的子序列，检查是否存在任何连续对差异≤1 的子序列，并增加计数。

**高效方法:**思路是迭代给定的数组，对于每个 ith-element，尝试找到以 ith element 作为其最后一个元素结束的所需子序列。
对于每个 I，我们希望使用 arr[i]，arr[i] -1，arr[i] + 1，因此我们将定义 2D 数组， **dp[][]** ，其中 dp[i][0]将包含不具有任何差小于 1 的连续对的子序列的数量，dp[i][1]包含具有任何差≤1 的连续对的子序列的数量。
同样，我们将维护两个变量 **required_subsequence** 和**not _ required _ subsequence**来维护至少有一个连续元素差异≤1 的子序列的计数和不包含任何连续元素差异≤1 的子序列的计数。

现在，考虑子阵列 arr[1] …。arr[i]，我们将执行以下步骤:

1.  通过在子序列中添加 ith 元素，计算没有任何差值小于 1 的连续对的子序列的数量。这些基本上是 dp[arr[i] + 1][0]、DP[arr[I]–1][0]和 dp[arr[i]][0]之和。
2.  至少有一个连续对的差至少为 1 且以 I 结尾的子序列总数等于找到的子序列总数，直到 I(只需在最后追加 arr[i])+在添加 arr[I]时变成至少有一个连续对的差小于 1 的子序列。
3.  在 i + 1(仅当前元素作为子序列)之前，不具有任何差小于 1 的连续对且结束于 i =不具有任何差小于 1 的连续对的总子序列。
4.  更新 required_subsequence、not_required_subsequence 和 dp[arr[i][0]]，最终答案将是 required_subsequence。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int N = 10000;

// Function to return the number of subsequences
// which have at least one consecutive pair
// with difference less than or equal to 1
int count_required_sequence(int n, int arr[])
{
    int total_required_subsequence = 0;
    int total_n_required_subsequence = 0;
    int dp[N][2];
    for (int i = 0; i < n; i++) {

        // Not required sub-sequences which
        // turn required on adding i
        int turn_required = 0;
        for (int j = -1; j <= 1; j++)
            turn_required += dp[arr[i] + j][0];

        // Required sub-sequence till now will be
        // required sequence plus sub-sequence
        // which turns required
        int required_end_i = (total_required_subsequence
                              + turn_required);

        // Similarly for not required
        int n_required_end_i = (1 + total_n_required_subsequence
                                - turn_required);

        // Also updating total required and
        // not required sub-sequences
        total_required_subsequence += required_end_i;
        total_n_required_subsequence += n_required_end_i;

        // Also, storing values in dp
        dp[arr[i]][1] += required_end_i;
        dp[arr[i]][0] += n_required_end_i;
    }

    return total_required_subsequence;
}

// Driver code
int main()
{
    int arr[] = { 1, 6, 2, 1, 9 };
    int n = sizeof(arr) / sizeof(int);

    cout << count_required_sequence(n, arr) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG
{

static int N = 10000;

// Function to return the number of subsequences
// which have at least one consecutive pair
// with difference less than or equal to 1
static int count_required_sequence(int n, int arr[])
{
    int total_required_subsequence = 0;
    int total_n_required_subsequence = 0;
    int [][]dp = new int[N][2];
    for (int i = 0; i < n; i++)
    {

        // Not required sub-sequences which
        // turn required on adding i
        int turn_required = 0;
        for (int j = -1; j <= 1; j++)
            turn_required += dp[arr[i] + j][0];

        // Required sub-sequence till now will be
        // required sequence plus sub-sequence
        // which turns required
        int required_end_i = (total_required_subsequence
                            + turn_required);

        // Similarly for not required
        int n_required_end_i = (1 + total_n_required_subsequence
                                - turn_required);

        // Also updating total required and
        // not required sub-sequences
        total_required_subsequence += required_end_i;
        total_n_required_subsequence += n_required_end_i;

        // Also, storing values in dp
        dp[arr[i]][1] += required_end_i;
        dp[arr[i]][0] += n_required_end_i;
    }

    return total_required_subsequence;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 6, 2, 1, 9 };
    int n = arr.length;

    System.out.println(count_required_sequence(n, arr));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np;

N = 10000;

# Function to return the number of subsequences
# which have at least one consecutive pair
# with difference less than or equal to 1
def count_required_sequence(n, arr) :

    total_required_subsequence = 0;
    total_n_required_subsequence = 0;
    dp = np.zeros((N,2));

    for i in range(n) :

        # Not required sub-sequences which
        # turn required on adding i
        turn_required = 0;
        for j in range(-1, 2,1) :
            turn_required += dp[arr[i] + j][0];

        # Required sub-sequence till now will be
        # required sequence plus sub-sequence
        # which turns required
        required_end_i = (total_required_subsequence
                            + turn_required);

        # Similarly for not required
        n_required_end_i = (1 + total_n_required_subsequence
                                - turn_required);

        # Also updating total required and
        # not required sub-sequences
        total_required_subsequence += required_end_i;
        total_n_required_subsequence += n_required_end_i;

        # Also, storing values in dp
        dp[arr[i]][1] += required_end_i;
        dp[arr[i]][0] += n_required_end_i;

    return total_required_subsequence;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 6, 2, 1, 9 ];
    n = len(arr);

    print(count_required_sequence(n, arr)) ;

# This code is contributed by AnkitRai01
```

## C#

```
using System;

public class GFG{

    static int N = 10000;

// Function to return the number of subsequences
// which have at least one consecutive pair
// with difference less than or equal to 1
static int count_required_sequence(int n, int[] arr)
{
    int total_required_subsequence = 0;
    int total_n_required_subsequence = 0;
    int [,]dp = new int[N,2];
    for (int i = 0; i < n; i++)
    {

        // Not required sub-sequences which
        // turn required on adding i
        int turn_required = 0;
        for (int j = -1; j <= 1; j++)
            turn_required += dp[arr[i] + j,0];

        // Required sub-sequence till now will be
        // required sequence plus sub-sequence
        // which turns required
        int required_end_i = (total_required_subsequence
                            + turn_required);

        // Similarly for not required
        int n_required_end_i = (1 + total_n_required_subsequence
                                - turn_required);

        // Also updating total required and
        // not required sub-sequences
        total_required_subsequence += required_end_i;
        total_n_required_subsequence += n_required_end_i;

        // Also, storing values in dp
        dp[arr[i],1] += required_end_i;
        dp[arr[i],0] += n_required_end_i;
    }

    return total_required_subsequence;
}

// Driver code
    static public void Main ()
    {

        int[] arr = { 1, 6, 2, 1, 9 };
        int n = arr.Length;

        Console.WriteLine(count_required_sequence(n, arr));

    }
}

// This code is contributed by rag2127.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var N = 10000;

// Function to return the number of subsequences
// which have at least one consecutive pair
// with difference less than or equal to 1
function count_required_sequence(n, arr)
{
    var total_required_subsequence = 0;
    var total_n_required_subsequence = 0;
    var dp = Array.from(Array(N), ()=> Array(2).fill(0));
    for (var i = 0; i < n; i++) {

        // Not required sub-sequences which
        // turn required on adding i
        var turn_required = 0;
        for (var j = -1; j <= 1; j++)
            turn_required += dp[arr[i] + j][0];

        // Required sub-sequence till now will be
        // required sequence plus sub-sequence
        // which turns required
        var required_end_i = (total_required_subsequence
                              + turn_required);

        // Similarly for not required
        var n_required_end_i = (1 + total_n_required_subsequence
                                - turn_required);

        // Also updating total required and
        // not required sub-sequences
        total_required_subsequence += required_end_i;
        total_n_required_subsequence += n_required_end_i;

        // Also, storing values in dp
        dp[arr[i]][1] += required_end_i;
        dp[arr[i]][0] += n_required_end_i;
    }

    return total_required_subsequence;
}

// Driver code
var arr = [ 1, 6, 2, 1, 9 ];
var n = arr.length;
document.write( count_required_sequence(n, arr) + "<br>");

</script>
```

**Output:** 

```
12
```