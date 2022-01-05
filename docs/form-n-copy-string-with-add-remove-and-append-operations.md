# 通过添加、删除和追加操作形成 N-copy 字符串

> 原文:[https://www . geesforgeks . org/form-n-copy-string-with-add-remove-append-operations/](https://www.geeksforgeeks.org/form-n-copy-string-with-add-remove-and-append-operations/)

当一个字符串由字母“G”的 N 个副本组成时，它被称为 N 副本字符串。即“GGGG”是一个 4 份的字符串，因为它包含 4 份字母“G”。最初，我们有一个空字符串，可以对其执行以下三个操作:

1.  **加**单个字母‘G’，成本为 x
2.  **去掉**单个字母‘G’，代价为 x
3.  **将到目前为止形成的字符串附加到自身，成本为 Y，即我们有字符串“GG”，我们可以将其附加到自身，使“GGGG”
    给定 N，X 和 Y，使用上述操作找到生成 N 副本字符串的最小成本**

**例:**

> **输入:N = 4，X = 2，Y = 1**
> **输出:4**
> **解释:**
> 1)最初，字符串它是空的，我们执行一个 Add 操作形成字符串‘G’。
> 2)接下来，我们执行类型 3 的操作，并形成字符串“GG”。
> 3)我们再次执行操作 3 并形成“GGGG”，这是所需的 N 拷贝字符串。
> **成本**= X+Y+Y = 2+1+1 =**4**
> **输入:N = 4，X = 1，Y = 3**
> **输出:4**
> 我们可以连续进行 4 次加法运算，形成‘GGGG’。
> **成本**= X+X+X+X = 1+1+1+1 =**4**

这个问题可以用动态规划方法来解决。
如果我们仔细分析这些操作，很容易看出，我们只有在存在比所需数量更多的副本时才执行移除操作，这只能是在此移除操作之前涉及类型 3 的操作时的情况，因为如果在此之前存在类型 1 的操作，那么它是没有意义的，因为连续的添加和移除操作只会增加成本，而不会在我们的字符串中引入任何新的副本。
因此我们可以说我们有以下操作，
1)添加单个字符“G”，带有成本 X
2)将字符串追加到自身，然后移除单个字符“G”，带有成本 Y + X
3)将字符串追加到自身，带有成本 Y
**注**:现在我们参考这些修改后的操作
现在，它可以用 O(n) DP 方法来解决。

> 让 dp[i]代表形成 i-copy 字符串
> 的最小成本，则状态转换可以是:
> 1)如果 I 是奇数，
> 情况 1:在 **(i-1)复制字符串**
> 中添加一个字符情况 2:在 **((i+1)/2)复制字符串**
> 上执行类型 2 的操作，即**DP[I]= min(DP[I–1]+X， dp[(i + 1) / 2)] + Y + X)**
> 2)如果 I 为偶数
> 情况 1:在 **(i-1)中添加一个字符-复制字符串**，
> 情况 2:在**(I/2)-复制字符串**
> 上执行类型 3 的操作，即**DP[I]= min(DP[I–1]+X，dp[i / 2] + Y)**

## C++

```
// CPP code to find minimum cost to form a
// N-copy string
#include <bits/stdc++.h>

using namespace std;

// Returns the minimum cost to form a n-copy string
// Here, x -> Cost to add/remove a single character 'G'
// and y-> cost to append the string to itself
int findMinimumCost(int n, int x, int y)
{
    int* dp = new int[n + 1];

    // Base Case: to form a 1-copy string we
    // need to perform an operation of type
    // 1(i.e Add)
    dp[1] = x;

    for (int i = 2; i <= n; i++) {
        if (i & 1) {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 2 operation
            //        on ((i + 1) / 2)-copy string
            dp[i] = min(dp[i - 1] + x, dp[(i + 1) / 2] + y + x);
        }
        else {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 3 operation on
            //        (i/2)-copy string
            dp[i] = min(dp[i - 1] + x, dp[i / 2] + y);
        }
    }
    return dp[n];
}

// Driver Code
int main()
{
    int n = 4, x = 2, y = 1;
    cout << findMinimumCost(n, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find minimum cost to form a
// N-copy string
class Solution
{

// Returns the minimum cost to form a n-copy string
// Here, x -> Cost to add/remove a single character 'G'
// and y-> cost to append the string to itself
static int findMinimumCost(int n, int x, int y)
{
    int dp[] = new int[n + 1];

    // Base Case: to form a 1-copy string we
    // need to perform an operation of type
    // 1(i.e Add)
    dp[1] = x;

    for (int i = 2; i <= n; i++) {
        if ((i & 1)!=0) {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 2 operation
            //        on ((i + 1) / 2)-copy string
            dp[i] = Math.min(dp[i - 1] + x, dp[(i + 1) / 2] + y + x);
        }
        else {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 3 operation on
            //        (i/2)-copy string
            dp[i] = Math.min(dp[i - 1] + x, dp[i / 2] + y);
        }
    }
    return dp[n];
}

// Driver Code
public static void main(String args[])
{
    int n = 4, x = 2, y = 1;
    System.out.println( findMinimumCost(n, x, y));

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 code to find minimum cost to
# form a N-copy string

# function returns the minimum cost to
# form a n-copy string Here, x->Cost to
# add/remove a single character 'G' and
# y->cost to append the string to itself

def findMinimumCost(n, x, y):
    dp = [0 for i in range(n + 1)]

    # base case: ro form a 1-copy string
    #  we need tp perform an operation
    # of type 1(i,e Add)
    dp[1] = x

    for i in range(2, n + 1):
        if i & 1:
            # case1\. Perform a Add operation
            #        on (i-1)copy string
            # case2\. perform a type 2 operation
            #        on((i+1)/2)-copy string
            dp[i] = min(dp[i - 1] + x,
                        dp[(i + 1) // 2] + y + x)
        else:

            # case1\. Perform a Add operation
            #        on (i-1)-copy string
            # case2\. Perform a type # operation
            #        on (i/2)-copy string
            dp[i] = min(dp[i - 1] + x,
                        dp[i // 2] + y)

    return dp[n]

# Driver code
n, x, y = 4, 2, 1

print(findMinimumCost(n, x, y))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# code to find minimum cost to form a
// N-copy string
using System;

class GFG
{

// Returns the minimum cost to form a n-copy string
// Here, x -> Cost to add/remove a single character 'G'
// and y-> cost to append the string to itself
static int findMinimumCost(int n, int x, int y)
{
    int[] dp = new int[n + 1];

    // Base Case: to form a 1-copy string we
    // need to perform an operation of type
    // 1(i.e Add)
    dp[1] = x;

    for (int i = 2; i <= n; i++)
    {
        if ((i & 1)!=0)
        {

            // Case1\. Perform a Add operation on
            //     (i-1)-copy string,
            // Case2\. Perform a type 2 operation
            //     on ((i + 1) / 2)-copy string
            dp[i] = Math.Min(dp[i - 1] + x,
                             dp[(i + 1) / 2] + y + x);
        }
        else
        {

            // Case1\. Perform a Add operation on
            //     (i-1)-copy string,
            // Case2\. Perform a type 3 operation on
            //     (i/2)-copy string
            dp[i] = Math.Min(dp[i - 1] + x,
                             dp[i / 2] + y);
        }
    }
    return dp[n];
}

// Driver Code
public static void Main()
{
    int n = 4, x = 2, y = 1;
    Console.WriteLine(findMinimumCost(n, x, y));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find minimum cost to form a
// N-copy string

// Returns the minimum cost to form a n-copy
// string. Here, x -> Cost to add/remove a
// single character 'G' and y-> cost to
// append the string to itself
function findMinimumCost($n, $x, $y)
{
    $dp[$n + 1] = array();

    // Base Case: to form a 1-copy string
    // we need to perform an operation of
    // type 1(i.e Add)
    $dp[1] = $x;

    for ($i = 2; $i <= $n; $i++)
    {
        if ($i & 1)
        {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 2 operation
            //        on ((i + 1) / 2)-copy string
            $dp[$i] = min($dp[$i - 1] + $x,
                          $dp[($i + 1) / 2] + $y + $x);
        }
        else
        {

            // Case1\. Perform a Add operation on
            //        (i-1)-copy string,
            // Case2\. Perform a type 3 operation on
            //        (i/2)-copy string
            $dp[$i] = min($dp[$i - 1] + $x,
                          $dp[$i / 2] + $y);
        }
    }
    return $dp[$n];
}

// Driver Code
$n = 4;
$x = 2;
$y = 1;
echo findMinimumCost($n, $x, $y);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

    // Javascript code to find minimum cost to form a 
    // N-copy string

    // Returns the minimum cost to form a n-copy string
    // Here, x -> Cost to add/remove a single character 'G'
    // and y-> cost to append the string to itself
    function findMinimumCost(n, x, y)
    {
        let dp = new Array(n + 1);

        // Base Case: to form a 1-copy string we
        // need to perform an operation of type 
        // 1(i.e Add)
        dp[1] = x;

        for (let i = 2; i <= n; i++) {
            if ((i & 1)!=0) {

                // Case1\. Perform a Add operation on 
                //        (i-1)-copy string,
                // Case2\. Perform a type 2 operation 
                //        on ((i + 1) / 2)-copy string
                dp[i] = Math.min(dp[i - 1] + x, dp[parseInt((i + 1) / 2, 10)] + y + x);
            }
            else {

                // Case1\. Perform a Add operation on 
                //        (i-1)-copy string,
                // Case2\. Perform a type 3 operation on
                //        (i/2)-copy string
                dp[i] = Math.min(dp[i - 1] + x, dp[parseInt(i / 2, 10)] + y);
            }
        }
        return dp[n];
    }

    let n = 4, x = 2, y = 1;
    document.write(findMinimumCost(n, x, y));

</script>
```

**输出:**

```
4
```

**时间复杂度**O(n)
T3】辅助空间 O(n)