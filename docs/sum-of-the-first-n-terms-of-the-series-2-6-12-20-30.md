# 数列 2、6、12、20、30 的前 N 项之和。

> 原文:[https://www . geesforgeks . org/系列第一个 n 项之和-2-6-12-20-30/](https://www.geeksforgeeks.org/sum-of-the-first-n-terms-of-the-series-2-6-12-20-30/)

给定一个数字 N，任务是找出下面系列的前 N 项之和:

> Sn = 2 + 6 + 12 + 20 + 30 …截止条款

**例:**

```
Input: N = 2
Output: 8
2 + 6
= 8

Input: N = 4 
Output: 40
2 + 6+ 12 + 20
= 40
```

**方法:**让第 n 项用 tn 表示。
这个问题很容易通过将每个术语拆分如下来解决:

```
Sn = 2 + 6 + 12 + 20 + 30......
Sn = (1+1^2) + (2+2^2) + (3+3^2) + (4+4^2) +......
Sn = (1 + 2 + 3 + 4 + ...unto n terms) + (1^2 + 2^2 + 3^2 + 4^2 + ...upto n terms)
```

我们观察到锡可以分解成两个系列的总和。
因此，前 n 项之和如下所示:

```
Sn = (1 + 2 + 3 + 4 + ...unto n terms) + (1^2 + 2^2 + 3^2 + 4^2 + ...upto n terms)
Sn = n*(n + 1)/2 + n*(n + 1)*(2*n + 1)/6
```

**以下是上述方法的实施:**

## C++

```
// C++ program to find sum of first n terms
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
int calculateSum(int n)
{

    return n * (n + 1) / 2 + n *
            (n + 1) * (2 * n + 1) / 6;
}

// Driver code
int main()
{
    // number of terms to be
    // included in the sum
    int n = 3;

    // find the Sn
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of first n terms

import java.util.*;
import java.lang.*;
import java.io.*;
class GFG
{

// Function to calculate the sum
static int calculateSum(int n)
{

    return n * (n + 1) / 2 + n * 
            (n + 1) * (2 * n + 1) / 6;
}

// Driver code
public static void main(String args[])
{
    // number of terms to be
    // included in the sum
    int n = 3;

    // find the Sn
    System.out.print("Sum = " + calculateSum(n));

}
}
```

## 蟒蛇 3

```
# Python program to find sum of
# first n terms

# Function to calculate the sum
def calculateSum(n):
    return (n * (n + 1) // 2 + n *
           (n + 1) * (2 * n + 1) // 6)

# Driver code

# number of terms to be
# included in the sum
n = 3

# find the Sum
print("Sum = ", calculateSum(n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find sum of
// first n terms
using System;

class GFG
{

// Function to calculate the sum
static int calculateSum(int n)
{

    return n * (n + 1) / 2 + n *
               (n + 1) * (2 * n + 1) / 6;
}

// Driver code
public static void Main()
{
    // number of terms to be
    // included in the sum
    int n = 3;

    // find the Sn
    Console.WriteLine("Sum = " +
                       calculateSum(n));
}
}

// This code is contributed by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms

// Function to calculate the sum
function calculateSum($n)
{
    return $n * ($n + 1) / 2 + $n *
                ($n + 1) * (2 * $n + 1) / 6;
}

// Driver code

// number of terms to be
// included in the sum
$n = 3;

// find the Sn
echo "Sum = " , calculateSum($n);

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of first n terms

// Function to calculate the sum
function calculateSum(n)
{

    return n * (n + 1) / 2 + n *
            (n + 1) * (2 * n + 1) / 6;
}

// Driver code

    // number of terms to be
    // included in the sum
    let n = 3;

    // find the Sn
    document.write("Sum = " + calculateSum(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Sum = 20
```