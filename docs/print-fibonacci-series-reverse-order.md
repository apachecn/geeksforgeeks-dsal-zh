# 逆序打印斐波那契数列

> 原文:[https://www . geesforgeks . org/print-Fibonacci-series-reverse-order/](https://www.geeksforgeeks.org/print-fibonacci-series-reverse-order/)

给定一个数字 n，然后以相反的顺序打印 n 个斐波那契数列的项。

示例:

```
Input : n = 5
Output : 3 2 1 1 0

Input : n = 8
Output : 13 8 5 3 2 1 1 0
```

**算法**

> **1)** 声明一个大小为 n 的数组。
> **2)** 分别初始化**a【0】**和**a【1】**到 **0** 和 **1** 。
> **3)** 运行从 **2** 到 **n-1** 的循环，并将**a【I-2】**和**a【I-1】**的
> 之和存储在**a【I】**中。
> **4)** 按相反顺序打印数组。

## C++

```
// CPP Program to print Fibonacci
// series in reverse order
#include <bits/stdc++.h>
using namespace std;

void reverseFibonacci(int n)
{
    int a[n];

    // assigning first and second elements
    a[0] = 0;
    a[1] = 1;

    for (int i = 2; i < n; i++) {

        // storing sum in the
        // preceding location
        a[i] = a[i - 2] + a[i - 1];
    }

    for (int i = n - 1; i >= 0; i--) {

        // printing array in
        // reverse order
        cout << a[i] << " ";
    }
}

// Driver function
int main()
{
    int n = 5;
    reverseFibonacci(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print Fibonacci
// series in reverse order
import java.io.*;

class GFG {

    static void reverseFibonacci(int n)
    {
        int a[] = new int[n];

        // assigning first and second elements
        a[0] = 0;
        a[1] = 1;

        for (int i = 2; i < n; i++)
        {

            // storing sum in the
            // preceding location
            a[i] = a[i - 2] + a[i - 1];
        }

        for (int i = n - 1; i >= 0; i--)
        {

            // printing array in
            // reverse order
            System.out.print(a[i] +" ");
        }
    }

    // Driver function
    public static void main(String[] args)
    {
        int n = 5;
        reverseFibonacci(n);

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 Program to print Fibonacci
# series in reverse order

def reverseFibonacci(n):

    a = [0] * n

    # assigning first and second elements
    a[0] = 0
    a[1] = 1

    for i in range(2, n): 

        # storing sum in the
        # preceding location
        a[i] = a[i - 2] + a[i - 1]

    for i in range(n - 1, -1 , -1): 

        # printing array in
        # reverse order
        print(a[i],end=" ")

# Driver function
n = 5
reverseFibonacci(n)
```

## C#

```
// C# Program to print Fibonacci
// series in reverse order
using System;

class GFG {

    static void reverseFibonacci(int n)
    {
        int []a = new int[n];

        // assigning first and second elements
        a[0] = 0;
        a[1] = 1;

        for (int i = 2; i < n; i++)
        {

            // storing sum in the
            // preceding location
            a[i] = a[i - 2] + a[i - 1];
        }

        for (int i = n - 1; i >= 0; i--)
        {

            // printing array in
            // reverse order
            Console.Write(a[i] +" ");
        }
    }

    // Driver function
    public static void Main()
    {
        int n = 5;
        reverseFibonacci(n);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print Fibonacci
// series in reverse order

function reverseFibonacci($n)
{

    // assigning first and
    // second elements
    $a[0] = 0;
    $a[1] = 1;

    for ($i = 2; $i < $n; $i++)
    {

        // storing sum in the
        // preceding location
        $a[$i] = $a[$i - 2] +
                 $a[$i - 1];
    }

    for ($i = $n - 1; $i >= 0; $i--)
    {

        // printing array in
        // reverse order
        echo($a[$i] . " ");
    }
}

// Driver COde
$n = 5;
reverseFibonacci($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print Fibonacci
// series in reverse order
function reverseFibonacci(n)
{
    let a = [];

    // Assigning first and second elements
    a[0] = 0;
    a[1] = 1;

    for(let i = 2; i < n; i++)
    {

        // Storing sum in the
        // preceding location
        a[i] = a[i - 2] + a[i - 1];
    }

    for(let i = n - 1; i >= 0; i--)
    {

        // Printing array in
        // reverse order
        document.write(a[i] + " ");
    }
}

// Driver Code
let n = 5;

reverseFibonacci(n);

// This code is contributed by avijitmondal1998

</script>
```

**输出:**

```
3 2 1 1 0
```

**时间复杂度:** O(n)

**辅助空间:** O(n)