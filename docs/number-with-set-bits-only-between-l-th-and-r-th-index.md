# 仅在第 L 和第 R 索引之间设置位的数字

> 原文:[https://www . geesforgeks . org/number-with-set-bits-only-介于-l-th 和-r-th-index/](https://www.geeksforgeeks.org/number-with-set-bits-only-between-l-th-and-r-th-index/)

给定 L 和 R，任务是找到在二进制表示中，第 L 和第 R 个索引之间的所有位都被设置，其余位不被设置的数字。二进制表示是 32 位。

**示例:**

> **输入:** L = 2，R = 5
> **输出:** 60
> **说明:**二进制表示为
> 0..0111100 = > 60
> 
> **输入:** L = 1，R = 3
> **输出:** 14
> **说明:**二进制表示为
> 0..01110 = > 14

**天真法:**求数的天真法是从 i = L 迭代到 i = R，计算 2 <sup>i</sup> 的所有次方之和。
下面的程序说明了天真的方法:

## C++

```
// CPP program to print the integer
// with all the bits set in range L-R
// Naive Approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the integer
// with all the bits set in range L-R
int getInteger(int L, int R)
{

    int number = 0;

    // iterate from L to R
    // and add all powers of 2
    for (int i = L; i <= R; i++)
        number += pow(2, i);

    return number;
}

// Driver Code
int main()
{
    int L = 2, R = 5;
    cout << getInteger(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// integer with all the bits
// set in range L-R Naive Approach
import java.io.*;

class GFG
{

// Function to return the
// integer with all the
// bits set in range L-R
static int getInteger(int L,
                      int R)
{
    int number = 0;

    // iterate from L to R
    // and add all powers of 2
    for (int i = L; i <= R; i++)
        number += Math.pow(2, i);

    return number;
}

// Driver Code
public static void main (String[] args)
{
    int L = 2, R = 5;
    System.out.println(getInteger(L, R));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to print the integer
# with all the bits set in range L-R
# Naive Approach
from math import pow

# Function to return the integer
# with all the bits set in range L-R
def getInteger(L, R):
    number = 0

    # iterate from L to R
    # and add all powers of 2
    for i in range(L, R + 1, 1):
        number += pow(2, i)

    return number

# Driver Code
if __name__ == '__main__':
    L = 2
    R = 5
    print(int(getInteger(L, R)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to print the
// integer with all the bits
// set in range L-R Naive Approach
using System;

class GFG
{
// Function to return the
// integer with all the
// bits set in range L-R
static int getInteger(int L,
                      int R)
{
    int number = 0;

    // iterate from L to R
    // and add all powers of 2
    for (int i = L; i <= R; i++)
        number += (int)Math.Pow(2, i);

    return number;
}

// Driver Code
public static void Main ()
{
    int L = 2, R = 5;
    Console.Write(getInteger(L, R));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the integer with all
// the bits set in range
// L-R Naive Approach

// Function to return the
// integer with all the
// bits set in range L-R
function getInteger($L, $R)
{
    $number = 0;

    // iterate from L to R
    // and add all powers of 2
    for ($i = $L; $i <= $R; $i++)
        $number += pow(2, $i);

    return $number;
}

// Driver Code
$L = 2;
$R = 5;
echo getInteger($L, $R);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

// Javascript program to print the integer
// with all the bits set in range L-R
// Naive Approach

// Function to return the integer
// with all the bits set in range L-R
function getInteger(L, R)
{

    var number = 0;

    // iterate from L to R
    // and add all powers of 2
    for (var i = L; i <= R; i++)
        number += Math.pow(2, i);

    return number;
}

// Driver Code
var L = 2, R = 5;
document.write( getInteger(L, R));

</script>
```

**输出:**

```
60
```

一种**有效的方法**是计算所有(R)位从右边设置的数，然后减去所有(L-1)位从右边设置的数，得到所需的数。

1.用下面的公式计算右边所有 R 位的个数。

```
(1 << (R+1)) - 1.
```

2.从右边减去所有(L-1)设定位的数字。

```
(1<<L) - 1 
```

因此，计算((1 <

> **(1<<(R+1))-(1<<L)**

下面的程序说明了有效的方法:

## C++

```
// CPP program to print the integer
// with all the bits set in range L-R
// Efficient Approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the integer
// with all the bits set in range L-R
int setbitsfromLtoR(int L, int R)
{
    return (1 << (R + 1)) - (1 << L);
}

// Driver Code
int main()
{
    int L = 2, R = 5;
    cout << setbitsfromLtoR(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// the integer with all
// the bits set in range
// L-R Efficient Approach
import java.io.*;

class GFG
{

// Function to return the
// integer with all the
// bits set in range L-R
static int setbitsfromLtoR(int L,
                           int R)
{
    return (1 << (R + 1)) -
           (1 << L);
}

// Driver Code
public static void main (String[] args)
{
    int L = 2, R = 5;
    System.out.println(setbitsfromLtoR(L, R));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 蟒蛇 3

```
# Python3 program to print
# the integer with all the
# bits set in range L-R
# Efficient Approach

# Function to return the
# integer with all the
# bits set in range L-R
def setbitsfromLtoR(L, R):

    return ((1 << (R + 1)) -
            (1 << L))

# Driver Code
L = 2
R = 5
print(setbitsfromLtoR(L, R))

# This code is contributed
# by Smita
```

## C#

```
// C# program to print
// the integer with all
// the bits set in range
// L-R Efficient Approach
using System;

class GFG
{
// Function to return the
// integer with all the
// bits set in range L-R
static int setbitsfromLtoR(int L,
                           int R)
{
    return (1 << (R + 1)) -
           (1 << L);
}

// Driver Code
public static void Main ()
{
    int L = 2, R = 5;
    Console.WriteLine(setbitsfromLtoR(L, R));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the integer with all
// the bits set in range
// L-R Efficient Approach

// Function to return the
// integer with all the
// bits set in range L-R
function setbitsfromLtoR($L, $R)
{
    return (1 << ($R + 1)) -   
           (1 << $L);
}

// Driver Code
$L = 2;
$R = 5;
echo setbitsfromLtoR($L, $R);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>

// Javascript program to print the integer
// with all the bits set in range L-R
// Efficient Approach

// Function to return the integer
// with all the bits set in range L-R
function setbitsfromLtoR(L, R)
{
    return (1 << (R + 1)) - (1 << L);
}

// Driver Code
var L = 2, R = 5;
document.write( setbitsfromLtoR(L, R));

// This code is contributed by famously.
</script>
```

**输出:**

```
60
```

**时间复杂度**:O(1)
T3】辅助空间 : O(1)