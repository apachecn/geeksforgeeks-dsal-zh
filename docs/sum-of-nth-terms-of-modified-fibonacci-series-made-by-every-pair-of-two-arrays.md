# 每对两个数组构成的修正斐波那契数列的第 n 项之和

> 原文:[https://www . geeksforgeeks . org/第 n 项之和-修改后的斐波那契数列-由每对两个数组构成/](https://www.geeksforgeeks.org/sum-of-nth-terms-of-modified-fibonacci-series-made-by-every-pair-of-two-arrays/)

给定两个相同大小 m 的数组 A 和 B，你必须找到像斐波那契数列的第 n 个项的和(每个项的值是前两个项的和)，A 的每个元素作为第一个，B 的每个元素作为第二个。
**例:**

```
Input : {1, 2, 3}, {4, 5, 6}, n = 3
Output : 63
Explanation : 
A[] = {1, 2, 3};
B[] = {4, 5, 6};
n = 3;
All the possible series upto 3rd terms are: 
We have considered every possible pair of A 
and B and generated third term using sum of
previous two terms.
1, 4, 5
1, 5, 6
1, 6, 7
2, 4, 6
2, 5, 7
2, 6, 8
3, 4, 7
3, 5, 8
3, 6, 9
sum = 5+6+7+6+7+8+7+8+9 = 63

Input : {5, 8, 10}, {6, 89, 5}
Output : 369
```

**天真的方法**是取数组 A 和 B 的每一对，用它们做一个斐波那契数列。
一个**高效的方法**是基于下面的想法。

> 将原始斐波那契数列存储在数组中，并将第一项乘以 origin _ fib[n-2]，将第二项乘以 origin _ fib[n-1]。
> 数组 A 的每一个元素以及 B 都将出现 m 次，所以将它们乘以 m .
> (m *(B[I]* origin _ fib[n-1])+(m *(A[I]* origin _ fib[n-2])

通过使用有效的方法，它可以写成

```
original_fib[]={0, 1, 1, 2, 3, 5, 8};
A[] = {1, 2, 3};
B[] = {4, 5, 6};
n = 3;
for (i to m)
    sum = sum + 3*(B[i]*original_fib[2]) + 3*(A[i]*original_fib[1])
```

以下是上述方法的实现:

## C++

```
// CPP program to find sum of n-th terms
// of a Fibonacci like series formed using
// first two terms of two arrays.
#include <bits/stdc++.h>
using namespace std;

int sumNth(int A[], int B[], int m, int n)
{

    int res = 0;

    // if sum of first term is required
    if (n == 1) {
        for (int i = 0; i < m; i++)
            res = res + A[i];
    }

    // if sum of second term is required
    else if (n == 2) {
        for (int i = 0; i < m; i++)
            res = res + B[i] * m;
    }

    else {
        // fibonacci series used to find the
        // nth term of every series
        int f[n];
        f[0] = 0, f[1] = 1;
        for (int i = 2; i < n; i++)
            f[i] = f[i - 1] + f[i - 2];

        for (int i = 0; i < m; i++) {

            // as every b[i] term appears m times and
            // every a[i] term also appears m times
            res = res + (m * (B[i] * f[n - 1])) +
                        (m * (A[i] * f[n - 2]));
        }
    }

    return res;
}

int main()
{
    // m is the size of the array
    int A[] = { 1, 2, 3 };
    int B[] = { 4, 5, 6 };
    int n = 3;
    int m = sizeof(A)/sizeof(A[0]);
    cout << sumNth(A, B, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of n-th terms
// of a Fibonacci like series formed using
// first two terms of two arrays.

public class GFG {

    static int sumNth(int A[], int B[], int m, int n)
    {

        int res = 0;

        // if sum of first term is required
        if (n == 1) {
            for (int i = 0; i < m; i++)
                res = res + A[i];
        }

        // if sum of second term is required
        else if (n == 2) {
            for (int i = 0; i < m; i++)
                res = res + B[i] * m;
        }

        else {
            // fibonacci series used to find the
            // nth term of every series
            int f[] = new int[n];
            f[0] = 0;
            f[1] = 1;
            for (int i = 2; i < n; i++)
                f[i] = f[i - 1] + f[i - 2];

            for (int i = 0; i < m; i++) {

                // as every b[i] term appears m times and
                // every a[i] term also appears m times
                res = res + (m * (B[i] * f[n - 1])) +
                            (m * (A[i] * f[n - 2]));
            }
        }

        return res;
    }

    public static void main(String args[])
    {
         // m is the size of the array
        int A[] = { 1, 2, 3 };
        int B[] = { 4, 5, 6 };
        int n = 3;
        int m = A.length;
        System.out.println(sumNth(A, B, m, n));

    }
    // This code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 program to find sum of
# n-th terms of a Fibonacci like
# series formed using first two
# terms of two arrays.
def sumNth(A, B, m, n):

    res = 0;

    # if sum of first term is required
    if (n == 1):
        for i in range(m):
            res = res + A[i];

    # if sum of second term is required
    elif (n == 2):
        for i in range(m):
            res = res + B[i] * m;

    else:

        # fibonacci series used to find
        # the nth term of every series
        f = [0] * n;
        f[0] = 0;
        f[1] = 1;
        for i in range(2, n):
            f[i] = f[i - 1] + f[i - 2];

        for i in range(m):

            # as every b[i] term appears m
            # times and every a[i] term also
            # appears m times
            res = (res + (m * (B[i] * f[n - 1])) +
                         (m * (A[i] * f[n - 2])));

    return res;

# Driver code

# m is the size of the array
A = [1, 2, 3 ];
B = [4, 5, 6 ];
n = 3;
m = len(A);
print(sumNth(A, B, m, n));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of
// n-th terms of a Fibonacci
// like series formed using
// first two terms of two arrays.
using System;

class GFG
{
static int sumNth(int[] A, int[] B,
                  int m, int n)
{

    int res = 0;

    // if sum of first term is required
    if (n == 1)
    {
        for (int i = 0; i < m; i++)
            res = res + A[i];
    }

    // if sum of second term is required
    else if (n == 2)
    {
        for (int i = 0; i < m; i++)
            res = res + B[i] * m;
    }

    else
    {
        // fibonacci series used to find
        // the nth term of every series
        int[] f = new int[n];
        f[0] = 0;
        f[1] = 1;
        for (int i = 2; i < n; i++)
            f[i] = f[i - 1] + f[i - 2];

        for (int i = 0; i < m; i++)
        {

            // as every b[i] term appears m
            // times and every a[i] term also
            // appears m times
            res = res + (m * (B[i] * f[n - 1])) +
                        (m * (A[i] * f[n - 2]));
        }
    }

    return res;
}

// Driver Code
public static void Main(String[] args)
{
    // m is the size of the array
    int[] A = { 1, 2, 3 };
    int[] B = { 4, 5, 6 };
    int n = 3;
    int m = A.Length;
    Console.WriteLine(sumNth(A, B, m, n));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of n-th terms
// of a Fibonacci like series formed using
// first two terms of two arrays.
function sumNth(&$A, &$B, &$m, &$n)
{

    $res = 0;

    // if sum of first term is required
    if ($n == 1)
    {
        for ($i = 0; $i < $m; $i++)
            $res = $res + $A[$i];
    }

    // if sum of second term is required
    else if ($n == 2)
    {
        for ($i = 0; $i < $m; $i++)
            $res = $res + $B[$i] * $m;
    }

    else
    {
        // fibonacci series used to find
        // the nth term of every series
        $f = array();
        $f[0] = 0;
        $f[1] = 1;
        for ($i = 2; $i < $n; $i++)
            $f[$i] = $f[$i - 1] + $f[$i - 2];

        for ($i = 0; $i < $m; $i++)
        {

            // as every b[i] term appears m times
            // and every a[i] term also appears m times
            $res = $res + ($m * ($B[$i] * $f[$n - 1])) +
                          ($m * ($A[$i] * $f[$n - 2]));
        }
    }

    return $res;
}

// Driver code

// m is the size of the array
$A = array(1, 2, 3 );
$B = array(4, 5, 6 );
$n = 3;
$m = sizeof($A);
echo (sumNth($A, $B, $m, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript program to find sum of n-th terms
// of a Fibonacci like series formed using
// first two terms of two arrays.

    function sumNth(A , B , m , n)
    {
        var res = 0;

        // if sum of first term is required
        if (n == 1)
        {
            for (let  i = 0; i < m; i++)
                res = res + A[i];
        }

        // if sum of second term is required
        else if (n == 2)   
        {
            for (let i = 0; i < m; i++)
                res = res + B[i] * m;
        }

        else
        {

            // fibonacci series used to find the
            // nth term of every series
            var f = Array(n).fill(0);
            f[0] = 0;
            f[1] = 1;
            for (let i = 2; i < n; i++)
                f[i] = f[i - 1] + f[i - 2];

            for (i = 0; i < m; i++)
            {

                // as every b[i] term appears m times and
                // every a[i] term also appears m times
                res = res + (m * (B[i] * f[n - 1])) + (m * (A[i] * f[n - 2]));
            }
        }
        return res;
    }

        // m is the size of the array
        var A = [ 1, 2, 3 ];
        var B = [ 4, 5, 6 ];
        var n = 3;
        var m = A.length;
        document.write(sumNth(A, B, m, n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
63
```