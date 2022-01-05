# 求第一个数组的倍数和第二个数组的因子的数

> 原文:[https://www . geesforgeks . org/find-numbers-它是第一个数组和第二个数组的倍数/](https://www.geeksforgeeks.org/find-numbers-which-are-multiples-of-first-array-and-factors-of-second-array/)

给定两个数组 **A[]** 和 **B[]** ，任务是找出能被数组 **A[]** 的所有元素整除的整数，再将数组 **B[]** 的所有元素整除。

**示例:**

> **输入:** A[] = {1，2，2，4}，B[] = {16，32，64}
> **输出:** 4 8 16
> 4，8，16 是唯一的数字
> 是数组 A[]
> 所有元素的倍数，除了数组 B[]
> 
> **输入:** A[] = {2，3，6}，B[] = {42，84 }
> T3】输出: 6 42

**方法:**如果 **X** 是第一个数组所有元素的倍数，那么 **X** 必须是第一个数组所有元素的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 的倍数。
同样，如果 **X** 是第二个数组所有元素的因子，那么它一定是第二个数组所有元素的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的因子，这样的 **X** 只有在第二个数组的 GCD 被第一个数组的 LCM 整除的情况下才会存在。
如果可以整除，那么 **X** 可以是范围**【LCM，GCD】**中的任意值，该范围是 LCM 的倍数，并且均匀地划分 GCD。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the LCM of two numbers
int lcm(int x, int y)
{
    int temp = (x * y) / __gcd(x, y);
    return temp;
}

// Function to print the required numbers
void findNumbers(int a[], int n, int b[], int m)
{

    // To store the lcm of array a[] elements
    // and the gcd of array b[] elements
    int lcmA = 1, gcdB = 0;

    // Finding LCM of first array
    for (int i = 0; i < n; i++)
        lcmA = lcm(lcmA, a[i]);

    // Finding GCD of second array
    for (int i = 0; i < m; i++)
        gcdB = __gcd(gcdB, b[i]);

    // No such element exists
    if (gcdB % lcmA != 0) {
        cout << "-1";
        return;
    }

    // All the multiples of lcmA which are
    // less than or equal to gcdB and evenly
    // divide gcdB will satisfy the conditions
    int num = lcmA;
    while (num <= gcdB) {
        if (gcdB % num == 0)
            cout << num << " ";
        num += lcmA;
    }
}

// Driver code
int main()
{

    int a[] = { 1, 2, 2, 4 };
    int b[] = { 16, 32, 64 };

    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);

    findNumbers(a, n, b, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to return the LCM of two numbers
static int lcm(int x, int y)
{
    int temp = (x * y) / __gcd(x, y);
    return temp;
}

// Function to print the required numbers
static void findNumbers(int a[], int n,
                        int b[], int m)
{

    // To store the lcm of array a[] elements
    // and the gcd of array b[] elements
    int lcmA = 1, gcdB = 0;

    // Finding LCM of first array
    for (int i = 0; i < n; i++)
        lcmA = lcm(lcmA, a[i]);

    // Finding GCD of second array
    for (int i = 0; i < m; i++)
        gcdB = __gcd(gcdB, b[i]);

    // No such element exists
    if (gcdB % lcmA != 0)
    {
        System.out.print("-1");
        return;
    }

    // All the multiples of lcmA which are
    // less than or equal to gcdB and evenly
    // divide gcdB will satisfy the conditions
    int num = lcmA;
    while (num <= gcdB)
    {
        if (gcdB % num == 0)
            System.out.print(num + " ");
        num += lcmA;
    }
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 2, 4 };
    int b[] = { 16, 32, 64 };

    int n = a.length;
    int m = b.length;

    findNumbers(a, n, b, m);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd

# Function to return the LCM of two numbers
def lcm( x, y) :

    temp = (x * y) // gcd(x, y);
    return temp;

# Function to print the required numbers
def findNumbers(a, n, b, m) :

    # To store the lcm of array a[] elements
    # and the gcd of array b[] elements
    lcmA = 1; __gcdB = 0;

    # Finding LCM of first array
    for i in range(n) :
        lcmA = lcm(lcmA, a[i]);

    # Finding GCD of second array
    for i in range(m) :
        __gcdB = gcd(__gcdB, b[i]);

    # No such element exists
    if (__gcdB % lcmA != 0) :
        print("-1");
        return;

    # All the multiples of lcmA which are
    # less than or equal to gcdB and evenly
    # divide gcdB will satisfy the conditions
    num = lcmA;
    while (num <= __gcdB) :
        if (__gcdB % num == 0) :
            print(num, end = " ");

        num += lcmA;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 2, 4 ];
    b = [ 16, 32, 64 ];

    n = len(a);
    m = len(b);

    findNumbers(a, n, b, m);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to return the LCM of two numbers
static int lcm(int x, int y)
{
    int temp = (x * y) / __gcd(x, y);
    return temp;
}

// Function to print the required numbers
static void findNumbers(int []a, int n,
                        int []b, int m)
{

    // To store the lcm of array a[] elements
    // and the gcd of array b[] elements
    int lcmA = 1, gcdB = 0;

    // Finding LCM of first array
    for (int i = 0; i < n; i++)
        lcmA = lcm(lcmA, a[i]);

    // Finding GCD of second array
    for (int i = 0; i < m; i++)
        gcdB = __gcd(gcdB, b[i]);

    // No such element exists
    if (gcdB % lcmA != 0)
    {
        Console.Write("-1");
        return;
    }

    // All the multiples of lcmA which are
    // less than or equal to gcdB and evenly
    // divide gcdB will satisfy the conditions
    int num = lcmA;
    while (num <= gcdB)
    {
        if (gcdB % num == 0)
            Console.Write(num + " ");
        num += lcmA;
    }
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 1, 2, 2, 4 };
    int []b = { 16, 32, 64 };

    int n = a.Length;
    int m = b.Length;

    findNumbers(a, n, b, m);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find nth centered
// tridecagonal number
function __gcd(a, b)
{
    if (b == 0)
        return a;

    return __gcd(b, a % b);

}

// Function to return the LCM of two numbers
function lcm(x, y)
{
    var temp = (x * y) / __gcd(x, y);
    return temp;
}

// Function to print the required numbers
function findNumbers(a, n, b, m)
{

    // To store the lcm of array a[] elements
    // and the gcd of array b[] elements
    var lcmA = 1, gcdB = 0;

    // Finding LCM of first array
    for(var i = 0; i < n; i++)
        lcmA = lcm(lcmA, a[i]);

    // Finding GCD of second array
    for(var i = 0; i < m; i++)
        gcdB = __gcd(gcdB, b[i]);

    // No such element exists
    if (gcdB % lcmA != 0)
    {
        document.write("-1");
        return;
    }

    // All the multiples of lcmA which are
    // less than or equal to gcdB and evenly
    // divide gcdB will satisfy the conditions
    var num = lcmA;
    while (num <= gcdB)
    {
        if (gcdB % num == 0)
            document.write(num + " ");

        num += lcmA;
    }
}

// Driver code
var a = [ 1, 2, 2, 4 ];
var b = [ 16, 32, 64 ];

var n = a.length;
var m = b.length;

findNumbers(a, n, b, m);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
4 8 16
```