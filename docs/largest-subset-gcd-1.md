# GCD 1 的最大子集

> 原文:[https://www.geeksforgeeks.org/largest-subset-gcd-1/](https://www.geeksforgeeks.org/largest-subset-gcd-1/)

给定 n 个整数，我们需要求 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 等于 1 的最大子集的大小。
输入约束:

```
n <= 10^5
A[i] <= 10^5
```

示例:

```
Input : A = {2, 3, 5}
Output : 3

Input : A = {3, 18, 12}
Output : -1
```

## 天真的解决方案:

我们找到所有可能子集的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) ，找到 GCD 为 1 的最大子集。花费的总时间将等于评估所有可能子集的 GCD 所花费的时间。总的可能子集是 2 <sup>n</sup> 。在最坏的情况下，子集内有 n 个元素，计算其 GCD 所需的时间为 n * log(n)
保存当前子集所需的额外空间为 O(n)

```
Time complexity : O(n * log(n) * 2^n)
Space Complexity : O(n)
```

## 优化的操作系统解决方案:

假设我们找到一个 GCD 为 1 的子集，如果我们给它添加一个新元素，那么 GCD 仍然是 1。因此，如果一个子集存在 GCD 1，那么整个集合的 GCD 也是 1。因此，我们首先找到完备集的 GCD，如果它的 1，那么完备集就是那个子集，否则不存在 GCD 为 1 的子集。

## C++

```
// C++ program to find size of the largest subset with GCD 1
#include <iostream>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Function to find largest subset with GCD 1
int largestGCD1Subset(int A[], int n)
{
    // finding gcd of whole array
    int currentGCD = A[0];
    for (int i=1; i<n; i++)
    {
        currentGCD = gcd(currentGCD, A[i]);

        // If current GCD becomes 1 at any momemnt,
        // then whole array has GCD 1.
        if (currentGCD == 1)
            return n;
    }

    return 0;
}

// Driver program to test above function
int main()
{
    int A[] = {2, 18, 6, 3};
    int n = sizeof(A)/sizeof(A[0]);
    cout << largestGCD1Subset(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find size of the
// largest subset with GCD 1
import java.*;

class GFG {

    // Function to return gcd of
    // a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find largest
    // subset with GCD 1
    static int largestGCD1Subset(int A[],
                                   int n)
    {

        // finding gcd of whole array
        int currentGCD = A[0];

        for (int i=1; i<n; i++)
        {
            currentGCD =
                    gcd(currentGCD, A[i]);

            // If current GCD becomes 1
            // at any momemnt, then whole
            // array has GCD 1.
            if (currentGCD == 1)
                return n;
        }

        return 0;
    }

    // Driver code
    public static void main (String[] args)
    {
        int A[] = {2, 18, 6, 3};
        int n =A.length;

        System.out.println(
                  largestGCD1Subset(A, n) );
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to find size of the
# largest subset with GCD 1

# Function to return gcd of a and b
def gcd( a, b):

    if (a == 0):
        return b

    return gcd(b%a, a)

# Function to find largest subset
# with GCD 1
def largestGCD1Subset(A, n):

    # finding gcd of whole array
    currentGCD = A[0];
    for i in range(1, n):

        currentGCD = gcd(currentGCD, A[i])

        # If current GCD becomes 1 at
        # any momemnt, then whole
        # array has GCD 1.
        if (currentGCD == 1):
            return n
    return 0

# Driver code
A = [2, 18, 6, 3]
n = len(A)
print (largestGCD1Subset(A, n))

# This code is Contributed by Sam007.
```

## C#

```
// C# program to find size of the
// largest subset with GCD 1
using System;

public class GFG {

    // Function to return gcd of
    // a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to find largest subset
    // with GCD 1
    static int largestGCD1Subset(int []A,
                                   int n)
    {

        // finding gcd of whole array
        int currentGCD = A[0];
        for (int i = 1; i < n; i++)
        {
            currentGCD =
                    gcd(currentGCD, A[i]);

            // If current GCD becomes 1 at
            // any momemnt, then whole
            // array has GCD 1.
            if (currentGCD == 1)
                return n;
        }

        return 0;
    }

    // Driver method
    public static void Main()
    {
        int []A = {2, 18, 6, 3};
        int n = A.Length;

        Console.Write(
              largestGCD1Subset(A, n));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// php program to find size of the
// largest subset with GCD 1

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to find largest subset
// with GCD 1
function largestGCD1Subset($A, $n)
{

    // finding gcd of whole array
    $currentGCD = $A[0];
    for ( $i = 1; $i < $n; $i++)
    {
        $currentGCD =
           gcd($currentGCD, $A[$i]);

        // If current GCD becomes 1
        // at any momemnt, then
        // whole array has GCD 1.
        if ($currentGCD == 1)
            return $n;
    }

    return 0;
}

// Driver program
$A = array(2, 18, 6, 3);
$n = sizeof($A);
echo largestGCD1Subset($A, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find size of the
// largest subset with GCD 1

// Function to return gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find largest subset
// with GCD 1
function largestGCD1Subset(A, n)
{

    // finding gcd of whole array
    let currentGCD = A[0];
    for ( let i = 1; i < n; i++)
    {
        currentGCD =
           gcd(currentGCD, A[i]);

        // If current GCD becomes 1
        // at any momemnt, then
        // whole array has GCD 1.
        if (currentGCD == 1)
            return n;
    }

    return 0;
}

// Driver program
let A = [2, 18, 6, 3];
let n = A.length;
document.write(largestGCD1Subset(A, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
4
```

```
Time Complexity : O(n* log(n))
Space Complexity : O(1)
```

本文由 [**普拉蒂克·查哈尔**](https://pratik-chhajer.github.io/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。