# 求给定数组中最长的类斐波那契子数组

> 原文:[https://www . geeksforgeeks . org/find-给定数组中最长的类似斐波那契的子数组/](https://www.geeksforgeeks.org/find-the-longest-fibonacci-like-subarray-of-the-given-array/)

给定一个由 **N** 个元素组成的数组，任务是找到最长的类似斐波那契数列的子数组。
类似斐波那契数列的子数列定义为这样的数列:

```
A[i]=A[i-1]+A[i-2] where i>2

and, A[1] and A[2] can be anything.
```

**例:**

```
Input : N = 5, arr[] = {2, 4, 6, 10, 2}
Output : 4
The sub-array 2, 4, 6, 10 is Fibonacci like.

Input : N = 3, arr[] = {0, 0, 0}
Output : 3
The entire array is Fibonacci-like.
```

**方法:**
想法是观察任何长度小于或等于 2 的数组都是类似斐波那契的。现在，对于长度大于 2 的数组:

1.  保持变量 **len** 初始化为 2，变量 **mx** 存储到目前为止的最大长度。
2.  从第三个索引开始遍历数组。
3.  如果斐波那契数列可以扩展到这个指数，即如果 a[i] = a[i-1] + a[i-2]
    *   然后将变量 **len** 的值增加 1。
    *   否则将变量**透镜**重新初始化为 2。
    *   将 mx 和 len 的最大值存储在当前迭代的变量 mx 中。

以下是上述方法的实现:

## C++

```
// C++ program to find length of longest
// Fibonacci-like subarray

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// longest Fibonacci-like subarray
int longestFibonacciSubarray(int n, int a[])
{
    // Any 2 terms are Fibonacci-like
    if (n <= 2)
        return n;

    int len = 2;

    int mx = INT_MIN;

    for (int i = 2; i < n; i++) {

        // If previous subarray can be extended
        if (a[i] == a[i - 1] + a[i - 2])
            len++;

        // Any 2 terms are Fibonacci-like
        else
            len = 2;

        // Find the maximum length
        mx = max(mx, len);
    }

    return mx;
}

// Driver Code
int main()
{
    int n = 5;
    int a[] = {2, 4, 6, 10, 2};

    cout << longestFibonacciSubarray(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of longest
// Fibonacci-like subarray
class GFG
{

    // Function to find the length of the
    // longest Fibonacci-like subarray
    static int longestFibonacciSubarray(int n, int a[])
    {
        // Any 2 terms are Fibonacci-like
        if (n <= 2)
            return n;

        int len = 2;

        int mx = Integer.MIN_VALUE;

        for (int i = 2; i < n; i++)
        {

            // If previous subarray can be extended
            if (a[i] == a[i - 1] + a[i - 2])
                len++;

            // Any 2 terms are Fibonacci-like
            else
                len = 2;

            // Find the maximum length
            mx = Math.max(mx, len);
        }
        return mx;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        int a[] = {2, 4, 6, 10, 2};

        System.out.println(longestFibonacciSubarray(n, a));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 program to find Length of
# longest Fibonacci-like subarray

# Function to find the Length of the
# longest Fibonacci-like subarray
def longestFibonacciSubarray(n, a):

    # Any 2 terms are Fibonacci-like
    if (n <= 2):
        return n

    Len = 2

    mx = -10**9

    for i in range(2, n):

        # If previous subarray can be extended
        if (a[i] == a[i - 1] + a[i - 2]):
            Len += 1

        # Any 2 terms are Fibonacci-like
        else:
            Len = 2

        # Find the maximum Length
        mx = max(mx, Len)

    return mx

# Driver Code
n = 5
a = [2, 4, 6, 10, 2]

print(longestFibonacciSubarray(n, a))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find length of longest
// Fibonacci-like subarray
using System;

class GFG
{

    // Function to find the length of the
    // longest Fibonacci-like subarray
    static int longestFibonacciSubarray(int n, int[] a)
    {
        // Any 2 terms are Fibonacci-like
        if (n <= 2)
            return n;

        int len = 2;

        int mx = int.MinValue;

        for (int i = 2; i < n; i++)
        {

            // If previous subarray can be extended
            if (a[i] == a[i - 1] + a[i - 2])
                len++;

            // Any 2 terms are Fibonacci-like
            else
                len = 2;

            // Find the maximum length
            mx = Math.Max(mx, len);
        }
        return mx;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 5;
        int[] a = {2, 4, 6, 10, 2};

        Console.WriteLine(longestFibonacciSubarray(n, a));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length of longest
// Fibonacci-like subarray

// Function to find the length of the
// longest Fibonacci-like subarray
function longestFibonacciSubarray($n, $a)
{
    // Any 2 terms are Fibonacci-like
    if ($n <= 2)
        return $n;

    $len = 2;

    $mx = PHP_INT_MIN;

    for ($i = 2; $i < $n; $i++)
    {

        // If previous subarray can be extended
        if ($a[$i] == $a[$i - 1] + $a[$i - 2])
            $len++;

        // Any 2 terms are Fibonacci-like
        else
            $len = 2;

        // Find the maximum length
        $mx = max($mx, $len);
    }

    return $mx;
}

// Driver Code
$n = 5;
$a = array(2, 4, 6, 10, 2);

echo longestFibonacciSubarray($n, $a);

// This code is contributed
// by Akanksha Rai   
?>
```

## java 描述语言

```
<script>

// javascript program to find length of longest
// Fibonacci-like subarray

    // Function to find the length of the
    // longest Fibonacci-like subarray
    function longestFibonacciSubarray( n,  a)
    {
        // Any 2 terms are Fibonacci-like
        if (n <= 2)
            return n;

        var len = 2;

        var mx = Number.MIN_VALUE;

        for (var i = 2; i < n; i++)
        {

            // If previous subarray can be extended
            if (a[i] == a[i - 1] + a[i - 2])
                len++;

            // Any 2 terms are Fibonacci-like
            else
                len = 2;

            // Find the maximum length
            mx = Math.max(mx, len);
        }
        return mx;
    }

    // Driver Code

        var n = 5;
        var a = [2, 4, 6, 10, 2];

        document.write(longestFibonacciSubarray(n, a));

  // This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N)
T3】辅助空间 : O(1)