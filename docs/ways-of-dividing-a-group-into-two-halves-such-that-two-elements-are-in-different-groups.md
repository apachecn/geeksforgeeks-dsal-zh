# 将一个组分成两半的方法，使得两个元素处于不同的组中

> 原文:[https://www . geeksforgeeks . org/将一个组分成两半的方法，这样两个元素就处于不同的组中/](https://www.geeksforgeeks.org/ways-of-dividing-a-group-into-two-halves-such-that-two-elements-are-in-different-groups/)

给定 2n 个女孩，随机分成两个子组，每个子组包含 n 个女孩。任务是计算可以组成小组的方法的数量，这样两个漂亮的女孩就可以分成不同的小组。
**例:**

> **输入:**4
> T3】输出: 4
> 设组为 r1、r2、b1、b2 其中 b1、b2 为美少女
> 组为:((r1、b1) (r2、b2))、((r1、b2) (r2、b1))、((r2、b2) (r1、b1))、((r2、b1) (r1、b2))
> **输入:** 8
> **输出:** 40

**方式:**有两种方式，两个漂亮的女生分在不同的组中，每种方式对应剩余的(2n–2)个女生可以分成两组![{2n-2}_C_{n-1}    ](img/fae817579b2ea291f668ec2e811b85f9.png "Rendered by QuickLaTeX.com")T3【因此方式总数为 2 *![{2n-2}_C_{n-1}    ](img/fae817579b2ea291f668ec2e811b85f9.png "Rendered by QuickLaTeX.com")T5**实现代码:**

## C++

```
// CPP Program to count
// Number of ways in which two
// Beautiful girls are in different group
#include <bits/stdc++.h>
using namespace std;

// This function will
// return the factorial of a given number
int factorial(int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
        result = result * i;
    return result;
}

// This function will calculate nCr of given
// n and r
int nCr(int n, int r)
{
    return factorial(n) / (factorial(r) * factorial(n - r));
}

// This function will
// Calculate number of ways
int calculate_result(int n)
{
    int result = 2 * nCr((n - 2), (n / 2 - 1));
    return result;
}

// Driver Code
int main(void)
{
    int a = 2, b = 4;
    cout << calculate_result(2 * a) << endl;
    cout << calculate_result(2 * b) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
   //Java Program to count
// Number of ways in which two
// Beautiful girls are in different group

import java.io.*;

class GFG {

// This function will
// return the factorial of a given number
static int factorial(int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
        result = result * i;
    return result;
}

// This function will calculate nCr of given
// n and r
static int nCr(int n, int r)
{
    return factorial(n) / (factorial(r) * factorial(n - r));
}

// This function will
// Calculate number of ways
static int calculate_result(int n)
{
    int result = 2 * nCr((n - 2), (n / 2 - 1));
    return result;
}

// Driver Code

    public static void main (String[] args) {
        int a = 2, b = 4;
    System.out.println( calculate_result(2 * a));
    System.out.print(calculate_result(2 * b));

    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 Program to count
# Number of ways in which two
# Beautiful girls are in different group

# This function will
# return the factorial of a
# given number
def factorial(n) :

    result = 1
    for i in range(1, n + 1) :
        result *= i

    return result

# This function will calculate nCr of given
# n and r
def nCr(n, r) :

    return (factorial(n) // (factorial(r)
            * factorial(n - r)))

# This function will
# Calculate number of ways
def calculate_result(n) :

    result = 2 * nCr((n -2), (n // 2 - 1))

    return result

# Driver code
if __name__ == "__main__" :

    a, b = 2, 4
    print(calculate_result(2 * a))
    print(calculate_result(2 * b))

# This code is contributed by
# ANKITRAI1
```

## C#

```
//C# Program to count
// Number of ways in which two
// Beautiful girls are in different groupusing System;

using System;

public class GFG {

// This function will
// return the factorial of a given number
static int factorial(int n)
{
    int result = 1;
    for (int i = 1; i <= n; i++)
        result = result * i;
    return result;
}

// This function will calculate nCr of given
// n and r
static int nCr(int n, int r)
{
    return factorial(n) / (factorial(r) * factorial(n - r));
}

// This function will
// Calculate number of ways
static int calculate_result(int n)
{
    int result = 2 * nCr((n - 2), (n / 2 - 1));
    return result;
}

// Driver Code

    public static void Main () {
        int a = 2, b = 4;
    Console.WriteLine( calculate_result(2 * a));
    Console.Write(calculate_result(2 * b));

    }
}

// This code is contributed by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count Number
// of ways in which two Beautiful
// girls are in different group

// This function will return
// the factorial of a given number
function factorial($n)
{
    $result = 1;
    for ($i = 1; $i <= $n; $i++)
        $result = $result * $i;
    return $result;
}

// This function will calculate
// nCr of given n and r
function nCr($n, $r)
{
    return factorial($n) / (factorial($r) *
                            factorial($n - $r));
}

// This function will
// Calculate number of ways
function calculate_result($n)
{
    $result = 2 * nCr(($n - 2),
                      ($n / 2 - 1));
    return $result;
}

// Driver Code
$a = 2;
$b = 4;
echo calculate_result(2 * $a) . "\n";
echo calculate_result(2 * $b) . "\n";

// This Code is contributed by mits
?>
```

## java 描述语言

```
// Javascript Program to count Number
// of ways in which two Beautiful
// girls are in different group

// This function will return
// the factorial of a given number
function factorial(n)
{
    let result = 1;
    for (let i = 1; i <= n; i++)
        result = result * i;
    return result;
}

// This function will calculate
// nCr of given n and r
function nCr(n, r)
{
    return factorial(n) / (factorial(r) *
                            factorial(n - r));
}

// This function will
// Calculate number of ways
function calculate_result(n)
{
    let result = 2 * nCr((n - 2),
                    (n / 2 - 1));
    return result;
}

// Driver Code
let a = 2;
let b = 4;
document.write(calculate_result(2 * a) + "<br>");
document.write(calculate_result(2 * b) + "<br>");

// This Code is contributed by gfgking
```

**Output:** 

```
4
40
```

**时间复杂度:** O(N)

**辅助空间:** O(1)