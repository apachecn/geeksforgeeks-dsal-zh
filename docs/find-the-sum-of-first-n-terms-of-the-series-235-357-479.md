# 求数列 2*3*5，3*5*7，4*7*9 的前 N 项之和，…

> 原文:[https://www . geesforgeks . org/find-the-sum-first-n-terms-of-series-235-357-479/](https://www.geeksforgeeks.org/find-the-sum-of-first-n-terms-of-the-series-235-357-479/)

给定一个整数 **N** ，任务是找到系列的第一个 **N** 项的和:

> (2 * 3 * 5)，(3 * 5 * 7)，(4 * 7 * 9)，…

**例:**

> **输入:** N = 3
> **输出:**387
> S<sub>3</sub>=(2 * 3 * 5 * 7)+(4 * 7 * 9)= 30+105+252 = 387
> **输入:** N = 5
> **输出:** 1740

**方式:**让本系列的 **N <sup>第</sup>T5】项为**T<sub>N</sub>T9】。通过观察系列的 **N <sup>第</sup>** 项可以很容易地找到系列的总和:**** 

> **T<sub>n</sub>T3】= { n<sup>第 2、3、4、…}个</sup>期限* {n <sup>第 3、5、7、…}个</sup>期限* {n <sup>第</sup>个【T5、7、9、…}个
> T<sub>n</sub>T14】=(n+1)*(2 * n+1)*(2 * n+3)
> **T【T17****

前 n 项之和( **S <sub>n</sub>** )可由
找到

> **s**=σ **<sub>**=σ【4n】**</sub>**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program to find sum of the
// first n terms of the given series
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of the
// first n terms of the given series
int calSum(int n)
{
    // As described in the approach
    return (n * (2 * n * n * n + 12 * n * n + 25 * n + 21)) / 2;
}

// Driver code
int main()
{
    int n = 3;
    cout << calSum(n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find sum of the
// first n terms of the given series
class GFG {

    // Function to return the sum of the
    // first n terms of the given series
    static int calSum(int n)
    {

        // As described in the approach
        return (n * (2 * n * n * n + 12 * n * n + 25 * n + 21)) / 2;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 3;
        System.out.println(calSum(n));
    }
}
```

## **计算机编程语言**

```
# C++ program to find sum of the
# first n terms of the given series

# Function to return the sum of the
# first n terms of the given series
def calSum(n):

    # As described in the approach
    return (n*(2 * n*n * n + 12 * n*n + 25 * n + 21))/2;

# Driver Code
n = 3
print(calSum(n))
```

## **C#**

```
// C# program to find sum of the
// first n terms of the given series
using System;

class GFG {

    // Function to return the sum of the
    // first n terms of the given series
    static int calSum(int n)
    {

        // As described in the approach
        return (n * (2 * n * n * n + 12 * n * n + 25 * n + 21)) / 2;
    }

    // Driver code
    static public void Main()
    {
        int n = 3;
        Console.WriteLine(calSum(n));
    }
}
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP script to find sum of the
// first n terms of the given series

// Function to return the sum of the
// first n terms of the given series
function calculateSum($n)
{

    // As described in the approach
    return ($n*(2*$n*$n*$n+12*$n*$n+25*$n+21))/2;
}

// Driver code
$n = 3;
echo calculateSum($n);

?>
```

## **java 描述语言**

```
<script>
// Javascript program to find sum of the
// first n terms of the given series

    // Function to return the sum of the
    // first n terms of the given series
    function calSum( n) {

        // As described in the approach
        return (n * (2 * n * n * n + 12 * n * n + 25 * n + 21)) / 2;
    }

    // Driver Code
    let n = 3;
    document.write(calSum(n));

// This code is contributed by 29AjayKumar
</script>
```

****Output:** 

```
387
```**