# 求给定递推关系的第 n 项

> 原文:[https://www . geeksforgeeks . org/find-第 n 个给定重复项关系/](https://www.geeksforgeeks.org/find-nth-term-of-a-given-recurrence-relation/)

设 **a <sub>n</sub>** 为一个数列，由递推关系 **a <sub>1</sub> =1** 和**a<sub>n+1</sub>/a<sub>n</sub>= 2<sup>n</sup>**定义。任务是为给定的 **n** 找到**日志 <sub>2</sub> (a <sub>n</sub> )** 的值。
**举例:**

```
Input: 5
Output: 10
Explanation: 
log2(an) = (n * (n - 1)) / 2
= (5*(5-1))/2
= 10

Input: 100
Output: 4950
```

![\frac{a_{n+1}}{a_{n}}=2^{n}   ](img/ff791db4a85b0efcddd14b94ac2207b4.png "Rendered by QuickLaTeX.com")
![\frac{a_{n}}{a_{n-1}}=2^{n-1}   ](img/d0817f862edd6c46103a7448bc2b468d.png "Rendered by QuickLaTeX.com")
![.   ](img/1302a351ba2053d25a6b6c5ec4044d97.png "Rendered by QuickLaTeX.com")
![.   ](img/1302a351ba2053d25a6b6c5ec4044d97.png "Rendered by QuickLaTeX.com")
![.   ](img/1302a351ba2053d25a6b6c5ec4044d97.png "Rendered by QuickLaTeX.com")
![\frac{a_{2}}{a_{1}}=2^{1}   ](img/3af3d7c85de2006fe41c53e737d3c294.png "Rendered by QuickLaTeX.com")，我们将以上所有相乘，以达到
![\frac{a_{n+1}}{a_{n}}\;.\;\frac{a_{n}}{a_{n-1}}=2^{n-1}\;.\;.\;.\;\frac{a_{2}}{a_{1}}=2^{n+(n-1)+...+1}   ](img/c588661e6ffd79d7eeff4c88ae49bcdb.png "Rendered by QuickLaTeX.com")
![\frac{a_{n+1}}{a_{n}}=2^{\frac{n(n+1)}{2}}   ](img/542f7bad9b52df501a1acc92cad1543e.png "Rendered by QuickLaTeX.com")
自![1+2+3+...+(n-1)+n=\frac{n(n+1)}{2}   ](img/ad5a70fb357f21433d2960fd61f4ca34.png "Rendered by QuickLaTeX.com")起。然后
![a_{n+1}=2^{\frac{n(n+1)}{2}}\;.a_{1}=2^{\frac{n(n+1)}{2}}   ](img/a74fd79df330452f037d1301713ad843.png "Rendered by QuickLaTeX.com")。
用 n+1 代替 n: ![a_{n}=2^{\frac{n(n-1)}{2}}   ](img/6c49a5693a2fa47e1a1bf5a861fcf3dc.png "Rendered by QuickLaTeX.com")
所以，![log_{2}(a_{n})=\frac{n(n-1)}{2}   ](img/cdfec516058bfdfda93621ccd46f5dbc.png "Rendered by QuickLaTeX.com")
以下是上述方法的实施。

## C++

```
// C++ program to find nth term of
// a given recurrence relation

#include <bits/stdc++.h>
using namespace std;

// function to return required value
int sum(int n)
{

    // Get the answer
    int ans = (n * (n - 1)) / 2;

    // Return the answer
    return ans;
}

// Driver program
int main()
{

    // Get the value of n
    int n = 5;

    // function call to print result
    cout << sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth term
// of a given recurrence relation
import java.util.*;

class solution
{
static int sum(int n)
{
    // Get the answer
    int ans = (n * (n - 1)) / 2;

    // Return the answer
    return ans;
}

// Driver code
public static void main(String arr[])
{

    // Get the value of n
    int n = 5;

    // function call to print result
    System.out.println(sum(n));
}
}
//This code is contributed byte
//Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find nth
# term of a given recurrence
# relation

# function to return
# required value
def sum(n):

    # Get the answer
    ans = (n * (n - 1)) / 2;

    # Return the answer
    return ans

# Driver Code

# Get the value of n
n = 5

# function call to prresult
print(int(sum(n)))

# This code is contributed by Raj
```

## C#

```
// C# program to find nth term
// of a given recurrence relation
using System;

class GFG
{
static int sum(int n)
{
    // Get the answer
    int ans = (n * (n - 1)) / 2;

    // Return the answer
    return ans;
}

// Driver code
public static void Main()
{

    // Get the value of n
    int n = 5;

    // function call to print result
    Console.WriteLine(sum(n));
}
}

// This code is contributed byte
// inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find nth term of
// a given recurrence relation

// function to return required value
function sum($n)
{

    // Get the answer
    $ans = ($n * ($n - 1)) / 2;

    // Return the answer
    return $ans;
}

// Driver Code

// Get the value of n
$n = 5;

// function call to print result
echo sum($n);

// This code is contributed by
// inder_verma
?>
```

## java 描述语言

```
<script>
// Javascript program to find nth term of
// a given recurrence relation

// function to return required value
function sum(n)
{

    // Get the answer
    let ans = parseInt((n * (n - 1)) / 2);

    // Return the answer
    return ans;
}

// Driver program

// Get the value of n
let n = 5;

// function call to print result
document.write(sum(n));

// This code is contributed by subham348.
</script>
```

**Output:** 

```
10
```

**时间复杂度:O(1)**