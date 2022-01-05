# N 的除数的几何平均值的整数部分

> 原文:[https://www . geeksforgeeks . org/整数部分 n 的几何平均数/](https://www.geeksforgeeks.org/integer-part-of-the-geometric-mean-of-the-divisors-of-n/)

给定一个整数 **N** ，任务是求 **N** 的除数的几何平均值的整数部分。**几何平均值**是一种特殊类型的平均值，我们将数字相乘，然后取平方根(对于两个数字)、立方根(对于三个数字)等等。

> **例:**
> **输入:** N = 4
> **输出:**2
> 4 的除数为 1、2 和 4
> 几何平均数=(1 * 2 * 4)<sup>(1/3)</sup>= 8<sup>(1/3)</sup>= 2
> **输入:** N = 16
> **输出:** 8
> 除数

**方法:**可以观察到 **N** 的值会形成一个系列，如 **1，1，1，2，2，2，2，2，3，3，3，3，3，3，3，3，3，3，…..**其**n<sup>th</sup>T9【术语】为 **⌊√n⌋** 。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the integer
// part of the geometric mean
// of the divisors of n
int geometricMean(int n)
{
    return sqrt(n);
}

// Driver code
int main()
{
    int n = 16;

    cout << geometricMean(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the integer
// part of the geometric mean
// of the divisors of n
static int geometricMean(int n)
{
    return (int) Math.sqrt(n);
}

// Driver code
public static void main(String []args)
{
    int n = 16;
    System.out.println(geometricMean(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to return the integer
# part of the geometric mean
# of the divisors of n
def geometricMean(n) :

    return int(sqrt(n));

# Driver code
if __name__ == "__main__" :

    n = 16;

    print(geometricMean(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;   

class GFG
{

// Function to return the integer
// part of the geometric mean
// of the divisors of n
static int geometricMean(int n)
{
    return (int) Math.Sqrt(n);
}

// Driver code
public static void Main(String []args)
{
    int n = 16;
    Console.WriteLine(geometricMean(n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the integer
// part of the geometric mean
// of the divisors of n
function geometricMean(n)
{
    return Math.sqrt(n);
}

// Driver code
var n = 16;
document.write(geometricMean(n));

</script>
```

**Output:** 

```
4
```