# 系列 1、17、98、354 的第 n 项……

> 原文:[https://www . geesforgeks . org/program-find-n-th-term-series-11798354/](https://www.geeksforgeeks.org/program-find-n-th-term-series-11798354/)

给定一个数列 1，17，98，354 ……求这个数列的第 n 项。
级数基本代表前 n 个自然数的 4 次幂之和。第一学期是 1 <sup>4</sup> 的总和。第二项为两个数之和即(1 <sup>4</sup> + 2 <sup>4</sup> = 17)，第三项即(1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>= 98)等等。

**示例:**

```
Input : 5
Output : 979

Input : 7
Output : 4676 
```

**天真方法:**
一个简单的解决方法是将前 n 个自然数的 4 次幂相加。通过迭代，我们可以很容易地找到级数的第 n 项。
以下是上述方法的实施:

## C++

```
// CPP program to find n-th term of
// series
#include <iostream>
using namespace std;

// Function to find the nth term of series
int sumOfSeries(int n)
{
    // Loop to add 4th powers
    int ans = 0;
    for (int i = 1; i <= n; i++)
        ans += i * i * i * i;

    return ans;
}

// Driver code
int main()
{
    int n = 4;
    cout << sumOfSeries(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th term of
// series
import java.io.*;

class GFG {

    // Function to find the nth term of series
    static int sumOfSeries(int n)
    {
        // Loop to add 4th powers
        int ans = 0;
        for (int i = 1; i <= n; i++)
            ans += i * i * i * i;

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4;
        System.out.println(sumOfSeries(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# n-th term of
# series

# Function to find the
# nth term of series
def sumOfSeries(n) :
    # Loop to add 4th powers
    ans = 0
    for i in range(1, n + 1) :
        ans = ans + i * i * i * i

    return ans

# Driver code
n = 4
print(sumOfSeries(n))
```

## C#

```
// C# program to find n-th term of
// series
using System;
class GFG {

    // Function to find the
    // nth term of series
    static int sumOfSeries(int n)
    {

        // Loop to add 4th powers
        int ans = 0;
        for (int i = 1; i <= n; i++)
            ans += i * i * i * i;

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(sumOfSeries(n));
    }
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// n-th term of series

// Function to find the
// nth term of series
function sumOfSeries( $n)
{
    // Loop to add 4th powers
    $ans = 0;
    for ( $i = 1; $i <= $n; $i++)
        $ans += $i * $i * $i * $i;

    return $ans;
}

// Driver code
$n = 4;
echo sumOfSeries($n);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th term of
// series

// Function to find the nth term of series
function sumOfSeries( n)
{
    // Loop to add 4th powers
    let ans = 0;
    for (let i = 1; i <= n; i++)
        ans += i * i * i * i;

    return ans;
}

// Driver Code

let n = 4;
document.write(sumOfSeries(n));

</script>
```

**Output :** 

```
354
```