# L 和 R 范围内所有偶数的和

> 原文:[https://www . geeksforgeeks . org/范围内所有偶数的总和-l 和-r/](https://www.geeksforgeeks.org/sum-of-all-even-numbers-in-range-l-and-r/)

给定两个整数 L 和 R，任务是找出 L 和 R 范围内所有偶数的和。
**例:**

```
Input: L = 2, R = 5 
Output: 6
2 + 4 = 6

Input: L = 3, R = 8
Output: 18
```

**方法-1:** 从 L 到 R 迭代，将该范围内所有偶数求和。
**方法-2:** 求从 L 到 R 的所有自然数的[和](https://www.geeksforgeeks.org/sum-of-all-natural-numbers-in-range-l-to-r/)，从中减去 L 到 R 范围内奇数自然数的[和。
**方法-3:**](https://www.geeksforgeeks.org/sum-of-all-odd-natural-numbers-in-range-l-and-r/) 

*   求 R 以内所有偶数的和，即 R 以内的偶数个数为 **R/2** 。
*   求 L-1 以内所有偶数的和，即 L-1 以内偶数的个数为 **(L-1)/2** 。
*   然后从 **sumuptoR** 中减去**sumupto**。

> 所有偶数到任意 N 的和为:
> **R*(R+1)** 其中 R = N/2

以下是上述方法的实现:

## C++

```
// C++ program to print the sum
// of all even numbers in range L and R
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of
// all natural numbers
int sumNatural(int n)
{
    int sum = (n * (n + 1));
    return sum;
}

// Function to return sum
// of even numbers in range L and R
int sumEven(int l, int r)
{
    return sumNatural(r/2) - sumNatural((l-1) / 2);
}

// Driver Code
int main()
{
    int l = 2, r = 5;
    cout << "Sum of Natural numbers from L to R is "
         << sumEven(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the sum
// of all even numbers in range L and R

import java.io.*;

class GFG {

// Function to return the sum of
// all natural numbers
static int sumNatural(int n)
{
    int sum = (n * (n + 1));
    return sum;
}

// Function to return sum
// of even numbers in range L and R
static int sumEven(int l, int r)
{
    return sumNatural(r/2) - sumNatural((l-1) / 2);
}

// Driver Code

    public static void main (String[] args) {

        int l = 2, r = 5;
        System.out.println ("Sum of Natural numbers from L to R is "+
         sumEven(l, r));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to print the sum
# of all even numbers in range L and R

# Function to return the sum 
# of all natural numbers
def sumNatural(n):
    sum = (n * (n + 1))
    return int(sum)

# Function to return sum
# of even numbers in range L and R
def sumEven(l, r):
    return (sumNatural(int(r / 2)) -
            sumNatural(int((l - 1) / 2)))

# Driver Code
l, r = 2, 5
print("Sum of Natural numbers",
             "from L to R is", sumEven(l, r))

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# program to print the sum
// of all even numbers in range L and R

using System;

public class GFG{

// Function to return the sum of
// all natural numbers
static int sumNatural(int n)
{
    int sum = (n * (n + 1));
    return sum;
}

// Function to return sum
// of even numbers in range L and R
static int sumEven(int l, int r)
{
    return sumNatural(r/2) - sumNatural((l-1) / 2);
}

// Driver Code

    static public void Main (){
            int l = 2, r = 5;
        Console.WriteLine("Sum of Natural numbers from L to R is "+
        sumEven(l, r));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the sum of
// all even numbers in range L and R

// Function to return the sum of
// all natural numbers
function sumNatural($n)
{
    $sum = ($n * ($n + 1));
    return $sum;
}

// Function to return sum of
// even numbers in range L and R
function sumEven($l, $r)
{
    return sumNatural((int)($r / 2)) -
           sumNatural((int)(($l - 1) / 2));
}

// Driver Code
$l = 2; $r = 5;
echo "Sum of Natural numbers " .
     "from L to R is " . sumEven($l, $r);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to print the sum
// of all even numbers in range L and R

// Function to return the sum of
// all natural numbers
function sumNatural(n)
{
    let sum = Math.floor(n * (n + 1));
    return sum;
}

// Function to return sum
// of even numbers in range L and R
function sumEven(l, r)
{
    return sumNatural(Math.floor(r/2)) - sumNatural(Math.floor(l-1) / 2);
}

// driver program

        let l = 2, r = 5;
        document.write ("Sum of Natural numbers from L to R is "+
         sumEven(l, r));

</script>
```

**Output:** 

```
Sum of Natural numbers from L to R is 6
```