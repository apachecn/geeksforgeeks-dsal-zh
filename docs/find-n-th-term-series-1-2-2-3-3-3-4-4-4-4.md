# 求数列 1 ^ 2 ^ 3 ^ 3 ^ 4 ^ 4 ^ 4 ^ 4 的第 n 项。

> 原文:[https://www . geesforgeks . org/find-n-th-term-series-1-2-2-3-3-3-4-4-4-4/](https://www.geeksforgeeks.org/find-n-th-term-series-1-2-2-3-3-3-4-4-4-4/)

给定系列 1 2 2 3 3 3 4 4 4 4 …，求级数的第 n 项。“格局”很明显。有一个“1”，两个“2”三个“3”等等。

示例:

```
Input : n = 5 
Output : 3

Input :  n = 7
Output : 4
```

一种**天真的方法**是运行两个循环，一个从 1 到 n，另一个从 1 到 I，并且对于内部循环的每次迭代保持一个计数，每当计数达到 n 时，我们可以打破这两个循环，I 将是我们的答案。
**时间复杂度:** O(n)

一个有效的方法是记下一个小的观察值:
诀窍是找到一个模式。
考虑给给定的序列编号如下:
1 在位置 1
2 在位置 2，3
3 在位置 4，5，6
4 在位置 7，8，9，10
等等……
注意各个值的最后位置形成一个序列。
**1、3、6、10、15、21……**
如果我们想要一个“第 n”项的公式，从反过来看开始。数字“n”最早出现在哪个术语中？把第一届定为“第 0 届”。“1”出现在术语 0 中，“2”出现在术语 1 中，“3”出现在术语 1+2=3 中，“4”出现在术语 1+2+3= 6 中，等等。数字“x”最早出现在术语 1+2+……+(x-2)+(x-1)= x(x-1)/2 中。
所以求解第 n 项我们得到 **n = x*(x-1)/2**
用[二次方程](https://www.geeksforgeeks.org/roots-quadratic-equation/)求解得到

> x = ( ( 1 + sqrt(1+8*n) )/2)

n 在每种情况下都是 **NOT** 一个整数，这意味着第 n 个数不是同一个整数序列的第一个，但是很明显第 n 个整数就是整数值。

## C++

```
// CPP program to find the nth term of the series
// 1 2 2 3 3 3 ...
#include <bits/stdc++.h>
using namespace std;

// function to solve the quadratic equation
int term(int n)
{
    // calculating the Nth term
    int x = (((1) + (double)sqrt(1 + (8 * n))) / 2);
    return x;
}

// driver code to check the above function
int main()
{
    int n = 5;
    cout << term(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the nth
// term of the series 1 2 2 3 3 3 ...
import java.io.*;

class Series {

    // function to solve the quadratic
    // equation
    static int term(int n)
    {
        // calculating the Nth term
        int x = (((1) + (int)Math.sqrt(1 +
                           (8 * n))) / 2);
        return x;
    }

    // driver code to check the above function
    public static void main (String[] args) {
        int n = 5;
        System.out.println(term(n));
    }
}

// This code is contributed by Chinmoy Lenka
```

## 蟒蛇 3

```
# Python program to find the nth term
# of the series 1 2 2 3 3 3 ...
import math

# function to solve the quadratic equation
def term( n ):

    # calculating the Nth term
    x = (((1) + math.sqrt(1 + (8 * n))) / 2)
    return x

# Driver code
n = 5
print(int(term(n)))

# This code is contributed by Sharad_Bhardwaj.
```

## C#

```
// C# program to find the nth
// term of the series 1 2 2 3 3 3 ...
using System;

class Series
{
    // function to solve the quadratic
    // equation
    static int term(int n)
    {
        // calculating the Nth term
        int x = (((1) + (int)Math.Sqrt(1 + (8 * n))) / 2);
        return x;
    }

    // driver code to check the above function
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(term(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// nth term of the series
// 1 2 2 3 3 3 ...

// function to solve the
// quadratic equation
function term($n)
{
    // calculating the Nth term
    $x = (((1) + (double)sqrt(1 +
                  (8 * $n))) / 2);
    return $x;
}

// Driver Code
$n = 5;
echo((int)term($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the nth
// term of the series 1 2 2 3 3 3 ...

// Function to solve the quadratic equation
function term(n)
{

    // Calculating the Nth term
    let x = parseInt(((1) + Math.sqrt(1 + (8 * n))) / 2);
    return x;
}

// Driver code
let n = 5;

document.write(term(n));

// This code is contributed by rishavmahato348

</script>
```

**输出:**

```
3
```

时间复杂度:O(log(n))作为 sqrt 函数取 O(log n)。