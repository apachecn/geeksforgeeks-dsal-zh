# 可被所有可能的素数整除的最小 N 位数

> 原文:[https://www . geesforgeks . org/最小 n 位数可被所有可能的素数整除/](https://www.geeksforgeeks.org/smallest-n-digit-number-divisible-by-all-possible-prime-digits/)

给定一个整数 **N** ，任务是找到能被所有可能的素数整除的最小 **N** 位数，即 **2、3、5** 和 **7** 。如果不可能，打印 **-1** 。
**举例:**

> **输入:** N = 5
> **输出:** 10080
> **说明:** 10080 是能被 2、3、5、7 整除的最小五位数。
> **输入:** N = 3
> **输出:** 210

**方法:**
按照下面给出的步骤解决问题:

*   由于所有四个数字 **2，3，5，7** 都是素数，这意味着 **N** 也将被它们的乘积 **2 × 3 × 5 × 7 = 210** 整除
*   对于 **N < 3** ，不存在这样的数字。所以，打印 **-1** 。
*   对于 **N = 3** ，答案为 **210** 。
*   对于 **N > 3** ，需要进行以下计算:
    *   求余数 **R = 10 <sup>N-1</sup> % N** 。
    *   在**10<sup>N-1</sup>T5 中增加**210–R**。**

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach 
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of 
// n digits divisible by all prime digits
void minNum(int n)
{
    if (n < 3)
        cout << -1;
    else
        cout << (210 * ((int)(pow(10, n - 1) /
                                   210) + 1));
}

// Driver Code
int main()
{
    int n = 5;
    minNum(n);
    return 0;
}

// This code is contributed by amal kumar choubey
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the minimum number of
// n digits divisible by all prime digits
static void minNum(int n)
{
    if(n < 3)
        System.out.println(-1);
    else
        System.out.println(210 * (
            (int)(Math.pow(10, n - 1) / 210) + 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    minNum(n);
}
}

// This code is contributed by Stuti Pathak
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import *

# Function to find the minimum number of
# n digits divisible by all prime digits.
def minNum(n):
    if n < 3:
        print(-1)
    else:
        print(210 * (10**(n-1) // 210 + 1))

# Driver Code
n = 5
minNum(n)
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

// Function to find the minimum number of
// n digits divisible by all prime digits
static void minNum(int n)
{
    if (n < 3)
        Console.WriteLine(-1);
    else
        Console.WriteLine(210 *
           ((int)(Math.Pow(10, n - 1) / 210) + 1));
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    minNum(n);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach 

// Function to find the minimum number of 
// n digits divisible by all prime digits
function minNum(n)
{
    if (n < 3)
        document.write( -1);
    else
        document.write((210 * (parseInt(Math.pow(10, n - 1) /
                                   210) + 1)));
}

// Driver Code
var n = 5;
minNum(n);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
10080
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*