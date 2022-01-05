# 求给定基数 B 中最多 N 位数字的总数

> 原文:[https://www . geesforgeks . org/find-给定基数 b 中最多 n 位数的数字总数/](https://www.geeksforgeeks.org/find-the-total-count-of-numbers-up-to-n-digits-in-a-given-base-b/)

给定两个整数 **N** 和 **B** ，任务是找到基数 B 的自然数计数，直到 **N** 位数。

**示例:**

> **输入:** N = 2，B = 10
> **输出:** 99
> **说明:**
> 1，2，3，4，5，6，7，8，9 为基数 10 的 1 位数自然数。
> 10，11，12……99 是基数 10 的两位自然数
> 所以，总数= 9 + 90 = 99
> 
> **输入:** N = 2，B = 16
> **输出:** 255
> **说明:**
> 共有 240 个两位十六进制数和 15 个一位十六进制数。
> 因此，240 + 15 = 255。

**方法:**仔细观察，以 B 为基数的 N 位数字的计数是一个几何级数，第一项是**(B–1)**和 **B** 的共同比值。
因此，

> 第 N 项=基数 B 中 N 位数的自然数=(B–1)* B<sup>N–1</sup>T2】

最后，通过从 1 到 N 迭代一个循环，并使用上述公式计算第 i <sup>项和第</sup>项，可以计算出基数 B 中所有自然数的计数，直到 N 位。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the count
// of natural numbers upto N digits

#include <bits/stdc++.h>

using namespace std;

// Function to return the count of
// natural numbers upto N digits
int count(int N, int B)
{
    int sum = 0;

    // Loop to iterate from 1 to N
    // and calculating number of
    // natural numbers for every 'i'th digit.
    for (int i = 1; i <= N; i++) {
        sum += (B - 1) * pow(B, i - 1);
    }
    return sum;
}

// Driver Code
int main()
{
    int N = 2, B = 10;
    cout << count(N, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the count
// of natural numbers upto N digits

class GFG{

// Function to return the count of
// natural numbers upto N digits
static int count(int N, int B)
{
    int sum = 0;

    // Loop to iterate from 1 to N
    // and calculating number of
    // natural numbers for every 'i'th digit.
    for (int i = 1; i <= N; i++){
        sum += (B - 1) * Math.pow(B, i - 1);
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, B = 10;
    System.out.print(count(N, B));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to find the count
# of natural numbers up to N digits

from math import pow

# Function to return the count of
# natural numbers upto N digits
def count(N, B):
    sum = 0

    # Loop to iterate from 1 to N
    # and calculating number of
    # natural numbers for every 'i'th digit.
    for i in range(1, N+1):
        sum += (B - 1) * pow(B, i - 1)
    return sum

# Driver Code
if __name__ == '__main__':
    N = 2
    B = 10
    print(int(count(N, B)))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# implementation to find the count
// of natural numbers upto N digits
using System;
using System.Collections.Generic;
class GFG{

// Function to return the count of
// natural numbers upto N digits
static int count(int N, int B)
{
    int sum = 0;

    // Loop to iterate from 1 to N
    // and calculating number of
    // natural numbers for every
    // 'i'th digit.
    for(int i = 1; i <= N; i++)
    {
       sum += (int)((B - 1) * Math.Pow(B, i - 1));
    }
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, B = 10;

    Console.Write(count(N, B));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to find the count
// of natural numbers upto N digits

// Function to return the count of
// natural numbers upto N digits
function count(N, B)
{
    var sum = 0;

    // Loop to iterate from 1 to N and
    // calculating number of natural
    // numbers for every 'i'th digit.
    for(var i = 1; i <= N; i++)
    {
        sum += (B - 1) * Math.pow(B, i - 1);
    }
    return sum;
}

// Driver code
var N = 2, B = 10;

document.write(count(N, B));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
99
```

***时间复杂度:**O(N)*T4】