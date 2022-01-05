# 通过两个给定长度的跳跃达到数字

> 原文:[https://www . geeksforgeeks . org/通过两个给定长度的跳跃达到数字/](https://www.geeksforgeeks.org/reach-the-numbers-by-making-jumps-of-two-given-lengths/)

给定整数 **k** 、 **d1** 、 **d2** 和整数数组 **arr[]** 。从编号 **k** 开始，您可以进行大小为 **d1** 和 **d2** 的跳跃，即从 **k** 开始的所有可能的移动为:

*   **k + d1** 和**k–D1**
*   **k + d2** 和**k–D2**

任务是找到数组中的哪些数字可以从 **k** 到达，进行任意数量的跳转，并且任意给定的跳转大小为 **d1** 或 **d2** 。对于每个号码打印 **1** 如果可以到达，则打印 **0** 。
**举例:**

> **输入:** k = 10，d1 = 4，d2 = 6，arr[] = {10，15，20}
> **输出:** 1 0 1
> 10 可从 k 到达，无需额外移动。
> k+D1+D2 = 10+4+6 = 20
> **输入:** k = 8，d1 = 3，d2 = 2，arr[] = {9，4}
> **输出:** 1 1

**方法:**通过跳跃 **d1** 或 **d2** 从 **k** 可到达的任何数字 **x** 将采用 **x = k + (i * d1) + (j * d2)** 的形式，其中 **i** 和 **j** 是整数。
让**D1****D2**的 GCD 为 **gcd** 。因为， **gcd** 将 **d1** 和 **d2** 分开。因此我们可以写出 **d1 = m1 * gcd** 和 **d2 = m2 * gcd** ，其中 **m1** 和 **m2** 为整数
和**x = k+gcd *(I * m1+j * m2)= k+M * gcd**。
因此，从 **k** 可到达的任何数字 **x** 都应该满足**(x–k)% gcd = 0**。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function that returns the vector containing the
// result for the reachability of the required numbers
void reachTheNums(int nums[], int k, int d1, int d2, int n)
{
    int i, ans[n] = { 0 };
    int gcd = __gcd(d1, d2);

    for (i = 0; i < n; i++) {
        int x = nums[i] - k;

        // If distance x is coverable
        if (x % gcd == 0)
            ans[i] = 1;
        else
            ans[i] = 0;
    }

    for (i = 0; i < n; i++)
        cout << ans[i] << " ";
}

// Driver code
int main()
{
    // Numbers to be checked for reachability
    int nums[] = { 9, 4 };
    int n = sizeof(nums) / sizeof(nums[0]);
    // Starting number K
    int k = 8;

    // Sizes of jumps d1 and d2
    int d1 = 3, d2 = 2;

    reachTheNums(nums, k, d1, d2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;
class GFG {
// Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0 
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);
        return __gcd(a, b-a);
    }

// Function that returns the vector containing the
// result for the reachability of the required numbers
static void reachTheNums(int nums[], int k, int d1, int d2, int n)
{
    int i;
    int ans[] = new int[n];
    int gcd = __gcd(d1, d2);

    for (i = 0; i < n; i++) {
        int x = nums[i] - k;

        // If distance x is coverable
        if (x % gcd == 0)
            ans[i] = 1;
        else
            ans[i] = 0;
    }

    for (i = 0; i < n; i++)
        System.out.print(ans[i] + " ");
}

// Driver code

    public static void main (String[] args) {
        // Numbers to be checked for reachability
    int nums[] = { 9, 4 };
    int n =nums.length;
    // Starting number K
    int k = 8;

    // Sizes of jumps d1 and d2
    int d1 = 3, d2 = 2;

    reachTheNums(nums, k, d1, d2, n);
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function that returns the vector
# containing the result for the reachability
# of the required numbers
def reachTheNums(nums, k, d1, d2, n):

    ans = [0 for i in range(n)]

    gcd = mt.gcd(d1, d2)

    for i in range(n):
        x = nums[i] - k

        # If distance x is coverable
        if (x % gcd == 0):
            ans[i] = 1
        else:
            ans[i] = 0

    for i in range(n):
        print(ans[i], end = " ")

# Driver code

# Numbers to be checked for
# reachability
nums = [9, 4]
n = len(nums)

# Starting number K
k = 8

# Sizes of jumps d1 and d2
d1, d2 = 3, 2

reachTheNums(nums, k, d1, d2, n)

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# implementation of the above approach

using System ;

class GFG {

    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
        return b;
        if (b == 0)
        return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a-b, b);

        return __gcd(a, b-a);
    }

    // Function that returns the vector containing the
    // result for the reachability of the required numbers
    static void reachTheNums(int []nums, int k, int d1, int d2, int n)
    {
        int i;
        int []ans = new int[n];
        int gcd = __gcd(d1, d2);

        for (i = 0; i < n; i++) {
            int x = nums[i] - k;

            // If distance x is coverable
            if (x % gcd == 0)
                ans[i] = 1;
            else
                ans[i] = 0;
        }

        for (i = 0; i < n; i++)
            Console.Write(ans[i] + " ");
    }

    // Driver code
    public static void Main () {
        // Numbers to be checked for reachability
    int []nums = { 9, 4 };
    int n =nums.Length;
    // Starting number K
    int k = 8;

    // Sizes of jumps d1 and d2
    int d1 = 3, d2 = 2;

    reachTheNums(nums, k, d1, d2, n);
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// gcd function
function GCD($a, $b)
{
    if ($b == 0)
        return $a;
    return GCD($b, $a % $b);
}

// Function that returns the vector
// containing the result for the
// reachability of the required numbers
function reachTheNums($nums, $k, $d1,
                             $d2, $n)
{
    $i = 0; $ans = array(0, 0);
    $gcd = GCD($d1, $d2);

    for ($i = 0; $i < $n; $i++)
    {
        $x = $nums[$i] - $k;

        // if distance x is coverable
        if ($x % $gcd == 0)
            $ans[$i] = 1;
        else
            $ans[$i] = 0;
    }

    for ($i = 0; $i < $n; $i++)
    echo $ans[$i] . " ";
}

// Driver Code

// Numbers to be checked for reachability
$nums = array(9, 4);
$n = 2;

// Starting number $K
$k = 8;

// Sizes of jumps $d1 and $d2
$d1 = 3; $d2 = 2;

reachTheNums($nums, $k, $d1, $d2, $n);

// This code is contributed by Adesh Singh1
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Recursive function to return gcd of a and b
    function __gcd(a , b)
    {

        // Everything divides 0
        if (a == 0)
            return b;
        if (b == 0)
            return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Function that returns the vector containing the
    // result for the reachability of the required numbers
    function reachTheNums(nums , k , d1 , d2 , n)
    {
        var i;
        var ans = Array(n).fill(0);
        var gcd = __gcd(d1, d2);

        for (let i = 0; i < n; i++)
        {
            var x = nums[i] - k;

            // If distance x is coverable
            if (x % gcd == 0)
                ans[i] = 1;
            else
                ans[i] = 0;
        }

        for (let i = 0; i < n; i++)
            document.write(ans[i] + " ");
    }

    // Driver code

    // Numbers to be checked for reachability
    var nums = [ 9, 4 ];
    var n = nums.length;

    // Starting number K
    var k = 8;

    // Sizes of jumps d1 and d2
    var d1 = 3, d2 = 2;

    reachTheNums(nums, k, d1, d2, n);

// This code is contributed by aashish1995.
</script>
```

**Output:** 

```
1 1
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)