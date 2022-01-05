# 求数列第 n 项的程序-2，4，-6，8……。

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-2-4-6-8/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-the-series-2-4-6-8/)

给定一个数字 **N** ，任务是找到以下系列的**N**项。

> -2，4，-6，8……

**例:**

```
Input: n=4
Output: 8

Input: n=3
Output: -6
```

**方法:**通过清楚地检查该系列，我们可以找到该系列的 **Tn** 项，在 Tn 的帮助下，我们可以找到期望的结果。

> **Tn** =-2 + 4 -6 +8 …..
> 我们可以看到这里奇数项为负，偶数项为正
> **Tn**= 2(-1)<sup>n</sup>n
> T9】Tn=(-1)<sup>n</sup>2n

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// nth term of the given series
long Nthterm(int n)
{

    // nth term
    int Tn = pow(-1, n) * 2 * n;

    return Tn;
}

// Driver code
int main()
{
    int n = 3;

    cout << Nthterm(n);

    return 0;
}
```

## 计算机编程语言

```
# Python3 implementation of the approach 

# Function to return the nth term of the given series 
def Nthterm(n): 

    # nth term 
    Tn = ((-1)**n) * (2 * n)

    return Tn; 

# Driver code 
n = 3
print(Nthterm(n))
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.lang.*;
import java.io.*;

public class GFG {

    // Function to return the nth term of the given series
    static int NthTerm(int n)
    {
        int Tn
            = ((int)Math.pow(-1, n)) * 2 * n;

        return Tn;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        System.out.println(NthTerm(n));
    }
}
```

## C#

```
// C# implementation of the approach
using System;
public class GFG {

    // Function to return the nth term of the given series
    static int NthTerm(int n)
    {

        int Tn
            = ((int)Math.Pow(-1, n) * 2 * n);

        return Tn;
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.WriteLine(NthTerm(n));
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

    $Tn = (pow(-1, $n)) * (2*n); 

    // nth term of the given series 
    return $Tn; 

} 

// Driver code 
$n = 3; 
echo Nthterm($n); 
?> 
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the
// nth term of the given series
function Nthterm( n)
{

    // nth term
    let Tn = Math.pow(-1, n) * 2 * n;

    return Tn;
}

// Driver Function

    // get the value of N
    let N = 3;

    // Calculate and print the Nth term
    document.write( Nthterm(N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
-6
```