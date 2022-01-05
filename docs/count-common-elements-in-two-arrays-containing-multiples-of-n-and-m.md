# 计算包含 N 和 M 的倍数的两个数组中的公共元素

> 原文:[https://www . geesforgeks . org/count-common-elements in-two-array-包含 n 和 m 的倍数/](https://www.geeksforgeeks.org/count-common-elements-in-two-arrays-containing-multiples-of-n-and-m/)

给定两个数组，第一个数组包含小于或等于 k 的整数 n 的倍数，类似地，第二个数组包含小于或等于 k 的整数 m 的倍数。
**例:**

> **输入:** n=2 m=3 k=9
> **输出:** 1
> 第一个数组应为= [ 2，4，6，8 ]
> 第二个数组应为= [ 3，6，9 ]
> 6 是唯一的公共元素
> **输入:** n=1 m=2 k=5
> **输出:** 2

**方法:**
求 n 和 m 的 **LCM** 由于 LCM 是 n 和 m 的最小公倍数，所以 LCM 的所有倍数在两个数组中都是公共的。小于或等于 k 的 LCM 的倍数等于 k/(LCM(m，n))。
要找到 lcm，首先用欧氏算法计算两个数的 GCD，n，m 的 LCM 为 n*m/gcd(n，m)。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

using namespace std;

// Recursive function to find
// gcd using euclidean algorithm
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find lcm
// of two numbers using gcd
int lcm(int n, int m)
{
    return (n * m) / gcd(n, m);
}

// Driver code
int main()
{
    int n = 2, m = 3, k = 5;

    cout << k / lcm(n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Recursive function to find
// gcd using euclidean algorithm
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find lcm
// of two numbers using gcd
static int lcm(int n, int m)
{
    return (n * m) / gcd(n, m);
}

// Driver code
public static void main(String[] args)
{
    int n = 2, m = 3, k = 5;

    System.out.print( k / lcm(n, m));
}
}

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Recursive function to find
# gcd using euclidean algorithm
def gcd(a, b) :

    if (a == 0) :
        return b;

    return gcd(b % a, a);

# Function to find lcm
# of two numbers using gcd
def lcm(n, m) :

    return (n * m) // gcd(n, m);

# Driver code
if __name__ == "__main__" :

    n = 2; m = 3; k = 5;

    print(k // lcm(n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Recursive function to find
// gcd using euclidean algorithm
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find lcm
// of two numbers using gcd
static int lcm(int n, int m)
{
    return (n * m) / gcd(n, m);
}

// Driver code
public static void Main(String[] args)
{
    int n = 2, m = 3, k = 5;

    Console.WriteLine( k / lcm(n, m));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// javascript implementation of the above approach
// Recursive function to find
// gcd using euclidean algorithm
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to find lcm
// of two numbers using gcd
function lcm(n, m)
{
    return (n * m) / gcd(n, m);
}

// Driver code

var n = 2, m = 3, k = 5;

document.write( parseInt(k / lcm(n, m)));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
0
```

**时间复杂度:** O(log(min(n，m)))