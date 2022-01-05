# 给定一个数组和三个数字，最大化(x * a[i]) + (y * a[j]) + (z * a[k])

> 原文:[https://www . geesforgeks . org/given-array-三个数-maximum-x-ai-y-aj-z-AK/](https://www.geeksforgeeks.org/given-array-three-numbers-maximize-x-ai-y-aj-z-ak/)

给定 n 个整数的数组和三个整数 x，y 和 z，最大化(x * a[i]) + (y * a[j]) + (z * a[k])的值，其中 i ≤ j ≤ k。

**示例:**

```
Input : arr[] = {-1, -2, -3, -4, -5} 
         x = 1 
         y = 2 
         z = -3 
Output: 12
Explanation: The maximized values is 
(1 * -1) + (2 * -1) + ( -3 * -5) = 12 

Input: arr[] = {1, 2, 3, 4, 5} 
       x = 1 
       y = 2  
       z = 3 
Output: 30 
(1*5 + 2*5 + 3*5) = 30
```

一个**简单的解决方案**是运行三个嵌套循环来迭代所有三元组。对于每个三元组，计算所需的值并跟踪最大值，最后返回相同的值。

一个**有效的解决方案**是预先计算值，并使用额外的空间存储它们。第一个关键观察是 i ≤ j ≤ k，所以 x*a[i]永远是左最大值，z*a[k]永远是右最大值。创建一个左数组，存储每个元素的左最大值。创建一个正确的数组，在这里我们为每个元素存储正确的最大值。然后对于每个元素，计算函数可能的最大值。对于任何索引 ind，该位置的最大值总是(left[ind] + j * a[ind] + right[ind])，找到数组中每个元素的最大值，这就是你的答案。

下面是上述方法的实现

## C++

```
// CPP program to find the maximum value of
// x*arr[i] + y*arr[j] + z*arr[k]
#include <bits/stdc++.h>
using namespace std;

// function to maximize the condition
int maximizeExpr(int a[], int n, int x, int y,
                                        int z)
{
    // Traverse the whole array and compute
    // left maximum for every index.
    int L[n];
    L[0] = x * a[0];
    for (int i = 1; i < n; i++)
        L[i] = max(L[i - 1], x * a[i]);

    // Compute right maximum for every index.
    int R[n];
    R[n-1] = z * a[n-1];
    for (int i = n - 2; i >= 0; i--)
        R[i] = max(R[i + 1], z * a[i]);

    // Traverse through the whole array to
    // maximize the required expression.
    int ans = INT_MIN;
    for (int i = 0; i < n; i++)
          ans = max(ans, L[i] + y * a[i] + R[i]);

    return ans;
}

// driver program to test the above function
int main()
{
   int a[] = {-1, -2, -3, -4, -5};
   int n = sizeof(a)/sizeof(a[0]);
   int x = 1, y = 2 , z = -3;
   cout << maximizeExpr(a, n, x, y, z) << endl;
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum value
// of x*arr[i] + y*arr[j] + z*arr[k]
import java.io.*;

class GFG {

    // function to maximize the condition
    static int maximizeExpr(int a[], int n, int x,
                             int y, int z)
    {
        // Traverse the whole array and compute
        // left maximum for every index.
        int L[] = new int[n];
        L[0] = x * a[0];
        for (int i = 1; i < n; i++)
            L[i] = Math.max(L[i - 1], x * a[i]);

        // Compute right maximum for every index.
        int R[] = new int[n];
        R[n - 1] = z * a[n - 1];
        for (int i = n - 2; i >= 0; i--)
            R[i] = Math.max(R[i + 1], z * a[i]);

        // Traverse through the whole array to
        // maximize the required expression.
        int ans = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++)
            ans = Math.max(ans, L[i] + y * a[i] +
                                         R[i]);

        return ans;
    }

    // driver program to test the above function
    public static void main(String[] args)
    {
    int a[] = {-1, -2, -3, -4, -5};
    int n = a.length;
    int x = 1, y = 2 , z = -3;
    System.out.println(maximizeExpr(a, n, x, y, z));
    }
}
// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 program to find
# the maximum value of
# x*arr[i] + y*arr[j] + z*arr[k]
import sys

# function to maximize
# the condition
def maximizeExpr(a, n, x, y, z):

    # Traverse the whole array
    # and compute left maximum
    # for every index.
    L = [0] * n
    L[0] = x * a[0]
    for i in range(1, n):
        L[i] = max(L[i - 1], x * a[i])

    # Compute right maximum
    # for every index.
    R = [0] * n
    R[n - 1] = z * a[n - 1]
    for i in range(n - 2, -1, -1):
        R[i] = max(R[i + 1], z * a[i])

    # Traverse through the whole
    # array to maximize the
    # required expression.
    ans = -sys.maxsize
    for i in range(0, n):
        ans = max(ans, L[i] + y *
                       a[i] + R[i])

    return ans

# Driver Code
a = [-1, -2, -3, -4, -5]
n = len(a)
x = 1
y = 2
z = -3
print(maximizeExpr(a, n, x, y, z))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find the maximum value
// of x*arr[i] + y*arr[j] + z*arr[k]
using System;

class GFG {

    // function to maximize the condition
    static int maximizeExpr(int []a, int n,
                       int x, int y, int z)
    {

        // Traverse the whole array and
        // compute left maximum for every
        // index.
        int []L = new int[n];
        L[0] = x * a[0];
        for (int i = 1; i < n; i++)
            L[i] = Math.Max(L[i - 1], x * a[i]);

        // Compute right maximum for
        // every index.
        int []R = new int[n];
        R[n - 1] = z * a[n - 1];
        for (int i = n - 2; i >= 0; i--)
            R[i] = Math.Max(R[i + 1], z * a[i]);

        // Traverse through the whole array to
        // maximize the required expression.
        int ans = int.MinValue;
        for (int i = 0; i < n; i++)
            ans = Math.Max(ans, L[i] +
                             y * a[i] + R[i]);

        return ans;
    }

    // driver program to test the
    // above function
    public static void Main()
    {
        int []a = {-1, -2, -3, -4, -5};
        int n = a.Length;
        int x = 1, y = 2 , z = -3;

        Console.WriteLine(
              maximizeExpr(a, n, x, y, z));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// maximum value of
// x*arr[i]+ y*arr[j] + z*arr[k]

// function to maximize
// the condition
function maximizeExpr($a, $n,
                      $x, $y, $z)
{
    // Traverse the whole array
    // and compute left maximum
    // for every index.
    $L = array();
    $L[0] = $x * $a[0];
    for ($i = 1; $i < $n; $i++)
        $L[$i] = max($L[$i - 1],
                     $x * $a[$i]);

    // Compute right maximum
    // for every index.
    $R = array();
    $R[$n - 1] = $z * $a[$n - 1];
    for ($i = $n - 2; $i >= 0; $i--)
        $R[$i] = max($R[$i + 1],
                     $z * $a[$i]);

    // Traverse through the whole
    // array to maximize the
    // required expression.
    $ans = PHP_INT_MIN;
    for ($i = 0; $i < $n; $i++)
        $ans = max($ans, $L[$i] +
                   $y * $a[$i] + $R[$i]);

    return $ans;
}

// Driver Code
$a = array(-1, -2, -3, -4, -5);
$n = count($a);
$x = 1; $y = 2 ; $z = -3;
echo maximizeExpr($a, $n, $x, $y, $z);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to find the maximum value
// of x*arr[i] + y*arr[j] + z*arr[k]

    // function to maximize the condition
    function maximizeExpr(a , n , x , y , z)
    {

        // Traverse the whole array and compute
        // left maximum for every index.
        var L = Array(n).fill(0);
        L[0] = x * a[0];
        for (i = 1; i < n; i++)
            L[i] = Math.max(L[i - 1], x * a[i]);

        // Compute right maximum for every index.
        var R = Array(n).fill(0);
        R[n - 1] = z * a[n - 1];
        for (i = n - 2; i >= 0; i--)
            R[i] = Math.max(R[i + 1], z * a[i]);

        // Traverse through the whole array to
        // maximize the required expression.
        var ans = Number.MIN_VALUE;
        for (i = 0; i < n; i++)
            ans = Math.max(ans, L[i] + y * a[i] + R[i]);

        return ans;
    }

    // Driver program to test the above function
        var a = [ -1, -2, -3, -4, -5 ];
        var n = a.length;
        var x = 1, y = 2, z = -3;
        document.write(maximizeExpr(a, n, x, y, z));

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
12
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

本文由 [**Raj**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。