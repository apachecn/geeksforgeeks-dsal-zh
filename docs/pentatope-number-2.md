# 五胞胎号

> 原文:[https://www.geeksforgeeks.org/pentatope-number-2/](https://www.geeksforgeeks.org/pentatope-number-2/)

给定一个数字 n，任务是编写一个程序来寻找第 n 个五元数。五元数是[类比喻数](https://en.wikipedia.org/wiki/Figurate_number)，可以表示为规则和离散的几何图形。在[帕斯卡三角形的](https://en.wikipedia.org/wiki/Pascal%27s_triangle)中，从右到左或从左到右从第 5 项第 1 行 4 6 4 1 开始的任何一行的第 5 个单元格中的数字是**彭托普数字**。
**举例:**

> 输入:5
> 输出:70
> 输入:8
> 输出:1001

前几个五元数是:
1，5，15，35，70，126，210，330，495，715，1001……
第 n 个五元数的公式:

## C++

```
// C++ Program to find the
// nth Pentatope Number
#include <bits/stdc++.h>
using namespace std;

// Function that returns nth
// pentatope number
int pentatopeNum(int n)
{
    return (n * (n + 1) * (n + 2) * (n + 3)) / 24;
}

// Drivers Code
int main()
{
    // For 5th PentaTope Number
    int n = 5;
    cout << pentatopeNum(n) << endl;

    // For 11th PentaTope Number
    n = 11;
    cout << pentatopeNum(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// nth Pentatope Number
import java.io.*;

class GFG
{

// Function that returns nth
// pentatope number
static int pentatopeNum(int n)
{
    return (n * (n + 1) *
           (n + 2) * (n + 3)) / 24;
}
// Driver Code
public static void main (String[] args)
{
// For 5th PentaTope Number
int n = 5;
System.out.println(pentatopeNum(n));

// For 11th PentaTope Number
n = 11;
System.out.println(pentatopeNum(n));

}
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# Python3 program to find
# nth Pentatope number

# Function to calculate
# Pentatope number
def pentatopeNum(n):

    # Formula to calculate nth
    # Pentatope number
    return (n * (n + 1) *
                (n + 2) *
                (n + 3) // 24)

# Driver Code
n = 5
print(pentatopeNum(n))
n = 11
print(pentatopeNum(n))

# This code is contributed
# by ajit.
```

## C#

```
// C# Program to find the
// nth Pentatope Number
using System;

class GFG
{

// Function that returns
// nth pentatope number
static int pentatopeNum(int n)
{
    return (n * (n + 1) *
           (n + 2) * (n + 3)) / 24;
}

// Driver Code
static public void Main(String []args)
{

// For 5th PentaTope Number
int n = 5;

Console.WriteLine(pentatopeNum(n));

// For 11th PentaTope Number
n = 11;

Console.WriteLine(pentatopeNum(n));
}
}
// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// nth Pentatope Number

// Function that returns
// nth pentatope number
function pentatopeNum($n)
{
    return ($n * ($n + 1) *
                 ($n + 2) *
                 ($n + 3)) / 24;
}

// Driver Code

// For 5th PentaTope Number
$n = 5;
echo pentatopeNum($n), "\n";

// For 11th PentaTope Number
$n = 11;
echo pentatopeNum($n), "\n" ;

// This code is contributed
// by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript  Program to find the
// nth Pentatope Number

// Function that returns
// nth pentatope number
function pentatopeNum(n)
{
    return (n * (n + 1) *
                (n + 2) *
                (n + 3)) / 24;
}

// Driver Code

// For 5th PentaTope Number
let n = 5;
document.write( pentatopeNum(n)+"<br>");

// For 11th PentaTope Number
n = 11;
document.write( pentatopeNum(n));

// This code is contributed by sravan kumar

</script>
```

**Output :** 

```
70
1001
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)

**参考资料:**[https://en . Wikipedia . org/wiki/penttope _ number](https://en.wikipedia.org/wiki/Pentatope_number)