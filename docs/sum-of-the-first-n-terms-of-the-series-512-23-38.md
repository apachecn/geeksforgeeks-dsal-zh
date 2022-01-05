# 级数 5，12，23，38…的前 N 项之和。

> 原文:[https://www . geeksforgeeks . org/系列第一 n 项之和-512-23-38/](https://www.geeksforgeeks.org/sum-of-the-first-n-terms-of-the-series-512-23-38/)

给定一个数字 N，任务是找出下面系列的前 N 项之和:

> Sn = 5 + 12 + 23 + 38 + …最多 n 个术语

**例:**

```
Input: N = 2
Output: 17
5 + 12
= 17

Input: N = 4 
Output: 80
5 + 12 + 23 + 38
= 78
```

**方法:**让第 n 项用 tn 表示。
这个问题可以很容易地借助于这些类型级数的一个通式，
上面给出的级数是一个二次级数。它们是特殊的，因为这个数列的连续项的差将是算术级数。
通式如下:

```
General Formula = a*(n^2) + b*n + c
```

现在，通过将级数的前 3 项放在通式中，我们可以得到 a，b 和 c 的值

```
Sn = 5 + 12 + 30 + 68 + ......
tn = 2 * (n^2) + n + 2
Sn = 2 * (n * (n+1) * (2 * n+1)/6) + n * (n+1)/2 + 2 * (n)
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

    return 2 * (n * (n + 1) * (2 * n + 1) / 6)
               + n * (n + 1) / 2 + 2 * (n);
}

// Driver code
int main()
{
    // number of terms to be included in sum
    int n = 3;

    // find the Sn
    cout << "Sum = " << calculateSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of first n terms

import java.io.*;

class GFG {

// Function to calculate the sum
 static int calculateSum(int n)
{

    return 2 * (n * (n + 1) * (2 * n + 1) / 6)
            + n * (n + 1) / 2 + 2 * (n);
}

// Driver code

    public static void main (String[] args) {
        // number of terms to be included in sum
    int n = 3;

    // find the Sn
    System.out.print( "Sum = " + calculateSum(n));
    }
}
// This code is contributed
// by  anuj_67..
```

## 蟒蛇 3

```
# Python program to find
# sum of first n terms

# Function to calculate the sum
def calculateSum(n) :

    return (2 * (n * (n + 1) *
           (2 * n + 1) // 6) + n *
           (n + 1) // 2 + 2 * (n))

# Driver code    
if __name__ == "__main__" :

    # number of terms to be
    # included in sum
    n = 3

    # find the Sn
    print("Sum =",calculateSum(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find sum
// of first n terms
using System;

class GFG
{

// Function to calculate the sum
static int calculateSum(int n)
{

    return 2 * (n * (n + 1) * (2 * n + 1) / 6) +
                n * (n + 1) / 2 + 2 * (n);
}

// Driver code
public static void Main ()
{
    // number of terms to be
    // included in sum
    int n = 3;

    // find the Sn
    Console.WriteLine("Sum = " + calculateSum(n));
}
}

// This code is contributed
// by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of first n terms

// Function to calculate the sum
function calculateSum($n)
{

    return 2 * ($n * ($n + 1) *
            (2 * $n + 1) / 6) +
                $n * ($n + 1) /
                2 + 2 * ($n);
}

// Driver code

// number of terms to
// be included in sum
$n = 3;

// find the Sn
echo "Sum = " . calculateSum($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of first n terms

// Function to calculate the sum
function calculateSum(n)
{

    return 2 * (n * (n + 1) * (2 * n + 1) / 6)
            + n * (n + 1) / 2 + 2 * (n);
}

// Driver code
    // number of terms to be included in sum
    let n = 3;

    // find the Sn
    document.write("Sum = " + calculateSum(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Sum = 40
```