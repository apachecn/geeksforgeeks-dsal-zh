# 零和子序列数

> 原文:[https://www . geeksforgeeks . org/零和子序列数/](https://www.geeksforgeeks.org/number-of-subsequences-with-zero-sum/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是统计总和为 **0** 的子序列数量。
**举例:**

> **输入:** arr[] = {-1，2，-2，1}
> **输出:** 3
> 所有可能的子序列为{-1，1}、{2，-2}和{-1，2，-2，1 }
> T7】输入: arr[] = {-2，-4，-1，6，-2}
> **输出:** 2

**方法:**使用[递归](https://www.geeksforgeeks.org/recursion/)可以解决问题。递归地，我们从第一个索引开始，要么选择要在子序列中添加的数字，要么不选择索引处的数字。一旦索引超过 N，我们需要检查评估的和是否为 0，并且在子序列中取的数的计数应该至少为 1。如果是，那么我们简单地返回 1，加到路的数量上。
动态规划不能用来解决这个问题，因为和值可以是任何不可能存储在任何维度数组中的任何东西。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required sub-sequences
int countSubSeq(int i, int sum, int cnt,
                int a[], int n)
{

    // Base case
    if (i == n) {

        // Check if the sum is 0
        // and at least a single element
        // is in the sub-sequence
        if (sum == 0 && cnt > 0)
            return 1;
        else
            return 0;
    }
    int ans = 0;

    // Do not take the number in
    // the current sub-sequence
    ans += countSubSeq(i + 1, sum, cnt, a, n);

    // Take the number in the
    // current sub-sequence
    ans += countSubSeq(i + 1, sum + a[i],
                       cnt + 1, a, n);

    return ans;
}

// Driver code
int main()
{
    int a[] = { -1, 2, -2, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << countSubSeq(0, 0, 0, a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count
    // of the required sub-sequences
    static int countSubSeq(int i, int sum, int cnt,
                                    int a[], int n)
    {

        // Base case
        if (i == n)
        {

            // Check if the sum is 0
            // and at least a single element
            // is in the sub-sequence
            if (sum == 0 && cnt > 0)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }
        int ans = 0;

        // Do not take the number in
        // the current sub-sequence
        ans += countSubSeq(i + 1, sum, cnt, a, n);

        // Take the number in the
        // current sub-sequence
        ans += countSubSeq(i + 1, sum + a[i],
                                cnt + 1, a, n);

        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {-1, 2, -2, 1};
        int n = a.length;
        System.out.println(countSubSeq(0, 0, 0, a, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required sub-sequences
def countSubSeq(i, Sum, cnt, a, n):

    # Base case
    if (i == n):

        # Check if the Sum is 0
        # and at least a single element
        # is in the sub-sequence
        if (Sum == 0 and cnt > 0):
            return 1
        else:
            return 0
    ans = 0

    # Do not take the number in
    # the current sub-sequence
    ans += countSubSeq(i + 1, Sum, cnt, a, n)

    # Take the number in the
    # current sub-sequence
    ans += countSubSeq(i + 1, Sum + a[i],
                           cnt + 1, a, n)

    return ans

# Driver code
a = [-1, 2, -2, 1]
n = len(a)
print(countSubSeq(0, 0, 0, a, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required sub-sequences
    static int countSubSeq(int i, int sum,
                           int cnt, int []a, int n)
    {

        // Base case
        if (i == n)
        {

            // Check if the sum is 0
            // and at least a single element
            // is in the sub-sequence
            if (sum == 0 && cnt > 0)
            {
                return 1;
            }
            else
            {
                return 0;
            }
        }

        int ans = 0;

        // Do not take the number in
        // the current sub-sequence
        ans += countSubSeq(i + 1, sum, cnt, a, n);

        // Take the number in the
        // current sub-sequence
        ans += countSubSeq(i + 1, sum + a[i],
                                  cnt + 1, a, n);

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []a = {-1, 2, -2, 1};
        int n = a.Length;
        Console.Write(countSubSeq(0, 0, 0, a, n));
    }
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of the required sub-sequences
function countSubSeq($i, $sum, $cnt, $a, $n)
{

    // Base case
    if ($i == $n)
    {

        // Check if the sum is 0
        // and at least a single element
        // is in the sub-sequence
        if ($sum == 0 && $cnt > 0)
            return 1;
        else
            return 0;
    }
    $ans = 0;

    // Do not take the number in
    // the current sub-sequence
    $ans += countSubSeq($i + 1, $sum,
                        $cnt, $a, $n);

    // Take the number in the
    // current sub-sequence
    $ans += countSubSeq($i + 1, $sum + $a[$i],
                        $cnt + 1, $a, $n);

    return $ans;
}

// Driver code
$a = array( -1, 2, -2, 1 );
$n = count($a) ;

echo countSubSeq(0, 0, 0, $a, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of the required sub-sequences
function countSubSeq(i, sum, cnt, a, n)
{

    // Base case
    if (i == n) {

        // Check if the sum is 0
        // and at least a single element
        // is in the sub-sequence
        if (sum == 0 && cnt > 0)
            return 1;
        else
            return 0;
    }
    let ans = 0;

    // Do not take the number in
    // the current sub-sequence
    ans += countSubSeq(i + 1, sum, cnt, a, n);

    // Take the number in the
    // current sub-sequence
    ans += countSubSeq(i + 1, sum + a[i],
                       cnt + 1, a, n);

    return ans;
}

// Driver code
    let a = [ -1, 2, -2, 1 ];
    let n = a.length;
    document.write(countSubSeq(0, 0, 0, a, n));

</script>
```

**Output:** 

```
3
```