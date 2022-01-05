# 找到系列 1 的第 n 个术语 2 2 4 4 4 4 8 8 8 8 8 8…

> 原文:[https://www . geeksforgeeks . org/find-n 系列术语-1-2-2-4-4-4-4-8-8-8-8-8-8-8-8-8/](https://www.geeksforgeeks.org/find-nth-term-of-the-series-1-2-2-4-4-4-4-8-8-8-8-8-8-8-8/)

给定一个数字 n，任务是找到数列的第 n 项

> 1 2 2 4 4 4 4 8 8 8 8 8 8 8 8 …

**例:**

```
Input: n = 9
Output: 8

Input: n = 1025
Output: 1024
```

**天真的方法:**

1.  运行从 i = 0 到 n 的循环
2.  内循环增量 I 乘以 i+k
3.  内循环增量 k 乘以 2*k
4.  当 I 小于 n 时，运行以上循环
5.  返回 k/2 作为结果

**复杂度:** log(n)
以下是上述方法的实现:

## C++

```
// CPP Program to find Nth term

#include <bits/stdc++.h>
using namespace std;

// Function that will return nth term
int getValue(int n)
{
    int i = 0, k = 1;

    while (i < n) {
        i = i + k;
        k = k * 2;
    }

    return k / 2;
}

// Driver Code
int main(void)
{

    // Get n
    int n = 9;

    // Get the value
    cout << getValue(n) << endl;

    // Get n
    n = 1025;

    // Get the value
    cout << getValue(n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Nth term

class GFG
{

    // Function that will return nth term
    static int getValue(int n)
    {
        int i = 0, k = 1;

        while (i < n) {
            i = i + k;
            k = k * 2;
        }

        return k / 2;
    }

    // Driver Code
    public static void main(String []args)
    {

        // Get n
        int n = 9;

        // Get the value
        System.out.println(getValue(n));

        // Get n
        n = 1025;

        // Get the value
        System.out.println(getValue(n));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find Nth term

# Function that will return nth term
def getValue(n):

    i = 0;
    k = 1;

    while (i < n):
        i = i + k;
        k = k * 2;

    return int(k / 2);

# Driver Code

# Get n
n = 9;

# Get the value
print(getValue(n));

# Get n
n = 1025;

# Get the value
print(getValue(n));

# This code is contributed by mits
```

## C#

```
// C# Program to find Nth term

using System;
class GFG
{

    // Function that will return nth term
    static int getValue(int n)
    {
        int i = 0, k = 1;

        while (i < n) {
            i = i + k;
            k = k * 2;
        }

        return k / 2;
    }

    // Driver Code
    public static void Main()
    {

        // Get n
        int n = 9;

        // Get the value
        Console.WriteLine(getValue(n));

        // Get n
        n = 1025;

        // Get the value
        Console.WriteLine(getValue(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Nth term

// Function that will return nth term
function getValue($n)
{
    $i = 0; $k = 1;

    while ($i < $n)
    {
        $i = $i + $k;
        $k = $k * 2;
    }

    return (int)$k / 2;
}

// Driver Code

// Get n
$n = 9;

// Get the value
echo getValue($n),"\n";

// Get n
$n = 1025;

// Get the value
echo getValue($n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript Program to find Nth term

// Function that will return nth term
function getValue(n)
{
    let i = 0, k = 1;

    while (i < n) {
        i = i + k;
        k = k * 2;
    }

    return parseInt(k / 2);
}

// Driver Code

    // Get n
    let n = 9;

    // Get the value
    document.write(getValue(n) + "<br>");

    // Get n
    n = 1025;

    // Get the value
    document.write(getValue(n) + "<br>");

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
8
1024
```

**有效途径:**这个问题可以用 O(1)时间复杂度来解决。
让序列的第 n <sup>个</sup>项等于 2 <sup>m</sup>
![1+2+4+8+.... +2^{m-1} < n \\ 2^m -1 <n \\ 2^m < n+1 \\ m < log_2 (n+1)\\     ](img/21fb8af4e7b5501b9f117315033fc3c6.png "Rendered by QuickLaTeX.com")
以下是上述方法的实现:

## C++

```
// CPP Program to find Nth term

#include <bits/stdc++.h>
using namespace std;

// Function that will return nth term
int getValue(int n)
{
    // Find log of n+1 on base 2
    int result = (floor)(log(n + 1) / log(2));

    return pow(2, result);
}

// Driver Code
int main(void)
{
    // Get n
    int n = 9;

    // Get the value
    cout << getValue(n) << endl;

    // Get n
    n = 1025;

    // Get the value
    cout << getValue(n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Nth term

import java.lang.*;
import java.lang.Math;
import java.io.*;

class GFG {
    // Function that will return nth term
static double getValue(double n)
{
    // Find log of n+1 on base 2
 double result =(Math.floor(Math.log(n + 1) / Math.log(2)));

    return Math.pow(2, result);
}

// Driver Code
    public static void main (String[] args) {
    // Get n
    double n = 9;
    // Get the value
    System.out.println (getValue(n));
    // Get n
    n = 1025;
    // Get the value
        System.out.println (getValue(n));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to find Nth term
import math

# Function that will return nth term
def getValue(n):

    # Find log of n+1 on base 2
    result = int(math.floor(math.log(n + 1) /
                            math.log(2)))
    return int(math.pow(2, result))

# Driver code
n = 9
print(getValue(n))

n = 1025
print(getValue(n))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# Program to find Nth term
using System;

class GFG
{
    // Function that will return nth term
    static double getValue(double n)
    {
        // Find log of n+1 on base 2
        double result =(Math.Floor(Math.Log(n + 1) / Math.Log(2)));
        return Math.Pow(2, result);
    }

    // Driver Code
    public static void Main ()
    {
        // Get n
        double n = 9;

        // Get the value
        Console.WriteLine(getValue(n));

        // Get n
        n = 1025;

        // Get the value
        Console.WriteLine (getValue(n));
    }
}

// This code is contributed by SoM15242
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Nth term
// Function that will return nth term
function getValue($n)
{
    // Find log of n+1 on base 2
    $result = (int)(log($n + 1) / log(2));

    return pow(2, $result);
}

// Driver Code

// Get n
$n = 9;

// Get the value
echo getValue($n), "\n";

// Get n
$n = 1025;

// Get the value
echo getValue($n), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
 // Javascript Program to find Nth term

// Function that will return nth term
function getValue(n)
{
    // Find log of n+1 on base 2
    let result = Math.floor(Math.log(n + 1) / Math.log(2));

    return Math.pow(2, result);
}

// Driver Code
// Get n
let n = 9;

// Get the value
document.write(getValue(n) + "<br>");

// Get n
n = 1025;

// Get the value
document.write(getValue(n));

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
8
1024
```