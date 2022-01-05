# 求数列 0，3/1，8/3，15/5 的第 n 项的程序……..

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-0-3-1-8-3-15-5/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-the-series-0-3-1-8-3-15-5/)

给定一个数字 **N** ，任务是找到以下系列的**N**项。

> 0、3/1、8/3、15/5……

**例:**

```
Input:  n=4
Output: 15/5

Input: n=3
Output: 8/3
```

**方法:**通过清楚地检查该系列，我们可以找到该系列的 **Tn** 项，在 Tn 的帮助下，我们可以找到期望的结果。

> **Tn** =0 + 3/1 +8/3 +15/5……
> 我们可以看到这里奇数项为负，偶数项为正
> **Tn**=((n<sup>2</sup>-1)/(2 * n-3))

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the nth term of the given series
void Nthterm(int n)
{

    // nth term
    int numerator = pow(n, 2) - 1;
    int denominator = 2 * n - 3;
    cout << numerator << "/" << denominator;
}

// Driver code
int main()
{
    int n = 3;

    Nthterm(n);

    return 0;
}
```

## 计算机编程语言

```
# Python3 implementation of the approach 

# Function to return the nth term of the given series 
def Nthterm(n): 

    # nth term 
    numerator = n**2-1
    denominator = 2 * n-3

    print(numerator, "/", denominator)

# Driver code 
n = 3
Nthterm(n)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

public class GFG {

    // Function to return the nth term of the given series
    static void NthTerm(int n)
    {
        int numerator
            = ((int)Math.pow(n, 2)) - 1;
        int denominator = 2 * n - 3;
        System.out.println(numerator + "/" + denominator);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        NthTerm(n);
    }
}
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to return the nth term of the given series
    static void NthTerm(int n)
    {

        int numerator
            = ((int)Math.Pow(n, 2)) - 1;
        int denominator = 2 * n - 3;
        Console.WriteLine(numerator + "/" + denominator);
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        NthTerm(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the nth term of the given series
function Nthterm($n)
{

    $numerator = (pow($n, 2)) -1;
    $denominator=2*$n-3;

    echo $numerator, "/", $denominator;
    return $Tn;

}

// Driver code
$n = 3;
Nthterm($n);
?>  
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the nth term of the given series
function Nthterm( n)
{

    // nth term
    let numerator = Math.pow(n, 2) - 1;
    let denominator = 2 * n - 3;
     document.write( numerator + "/" + denominator);
}

// Driver code
let n = 3;

    Nthterm(n);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
8/3
```