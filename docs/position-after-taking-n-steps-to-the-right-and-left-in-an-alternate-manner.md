# 左右交替走 N 步后的位置

> 原文:[https://www . geeksforgeeks . org/交替向右和向左走 n 步后的位置/](https://www.geeksforgeeks.org/position-after-taking-n-steps-to-the-right-and-left-in-an-alternate-manner/)

给定三个整数 N、A 和 B，一个人站在 0 坐标，第一步 A 步向右移动，第二步 B 步向左移动，以此类推。任务是找出 N 步后他会在哪个坐标。
**例:**

> **输入:** N = 3，A = 5，B = 2
> **输出:** 8
> 向右 5，向左 2，向右 5，因此此人将在 8 结束。
> **输入:** N = 5，A = 1，B = 10
> **输出:** -17

**逼近:**由于人向右走奇数步，向左走偶数步，我们要找出两个方向的步数差。因此，得到的公式将是:

```

[((n+1)/2)*a - (n/2)*b]

```

以下是上述方法的实现:

## C++

```
// C++ program to find the last coordinate
// where it ends his journey
#include <bits/stdc++.h>
using namespace std;

// Function to return the last destination
int lastCoordinate(int n, int a, int b)
{
    return ((n + 1) / 2) * a - (n / 2) * b;
}

// Driver Code
int main()
{
    int n = 3, a = 5, b = 2;
    cout << lastCoordinate(n, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the last coordinate
// where it ends his journey
import java.util.*;

class solution
{

// Function to return the last destination
static int lastCoordinate(int n, int a, int b)
{
    return ((n + 1) / 2) * a - (n / 2) * b;
}

// Driver Code
public static void main(String args[])
{
    int n = 3, a = 5, b = 2;
    System.out.println(lastCoordinate(n, a, b));

}
}
```

## 计算机编程语言

```
# Python3 program to find the 
# last coordinate where it
# ends his journey 

# Function to return the
# last destination 
def lastCoordinate(n, a, b):
    return (((n + 1) // 2) * 
         a - (n // 2) * b)

# Driver Code 
n = 3
a = 5
b = 2

print(lastCoordinate(n, a, b))

# This code is contributed
# by Sanjit_Prasad
```

## C#

```
// C# program to find the last coordinate 
// where it ends his journey 
using System;

class GFG
{

// Function to return the last destination 
public static int lastCoordinate(int n, 
                                 int a, int b)
{
    return ((n + 1) / 2) * a - (n / 2) * b;
}

// Driver Code 
public static void Main(string[] args)
{
    int n = 3, a = 5, b = 2;
    Console.WriteLine(lastCoordinate(n, a, b));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the last coordinate
// where it ends his journey

// Function to return the last destination
function lastCoordinate($n, $a, $b)
{
    return (($n + 1) / 2) * $a - 
            (int)($n / 2) * $b;
}

// Driver Code
$n = 3; $a = 5; $b = 2;
echo lastCoordinate($n, $a, $b);

// This code is contributed by inder_verma..
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the last coordinate
// where it ends his journey

// Function to return the last destination
function lastCoordinate(n, a, b)
{
    return (parseInt(n + 1) / 2) * a - 
            parseInt(n / 2) * b;
}

// Driver Code
    let n = 3, a = 5, b = 2;
    document.write(lastCoordinate(n, a, b));

</script>
```

**Output:** 

```
8
```