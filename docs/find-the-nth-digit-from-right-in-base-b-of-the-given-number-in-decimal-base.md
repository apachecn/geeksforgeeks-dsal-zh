# 在十进制基数

中找到给定数字的从右到 B 的第 n 个数字

> 原文:[https://www . geeksforgeeks . org/find-从十进制给定数字的基数-b 的右数开始计算/](https://www.geeksforgeeks.org/find-the-nth-digit-from-right-in-base-b-of-the-given-number-in-decimal-base/)

给定一个以十进制为基数的数字 **A** ，任务是从基数最后一位 **B**
**中找出 **N <sup>第</sup>T5】位数字【示例:**** 

> **输入:** A = 100，N = 3，B = 4
> **输出:** 2
> **说明:**
> (100)<sub>4</sub>= 1210
> 3<sup>rd</sup>倒数第二位是 2
> **输入:** A = 50，N = 3，B = 5
> **输出:** 2

**方法:**想法是通过将数字除以 B(N–1)次跳过 B 中的[给定数字的(N-1)位，然后返回当前数字与 B 的模，从右边得到 N <sup>第</sup>位。
以下是上述方法的实现:](https://www.geeksforgeeks.org/given-number-n-decimal-base-find-number-digits-base-base-b/) 

## C++

```
// C++ Implementation to find Nth digit
// from right in base B

#include <iostream>
using namespace std;

// Function to compute Nth digit
// from right in base B
int nthDigit(int a, int n, int b)
{

    // Skip N-1 Digits in Base B
    for (int i = 1; i < n; i++)
        a = a / b;

    // Nth Digit from right in Base B
    return a % b;
}

// Driver Code
int main()
{
    int a = 100;
    int n = 3;
    int b = 4;
    cout << nthDigit(a, n, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to find Nth digit
// from right in base B
import java.util.*;

class GFG
{

// Function to compute Nth digit
// from right in base B
static int nthDigit(int a, int n, int b)
{

    // Skip N-1 Digits in Base B
    for (int i = 1; i < n; i++)
        a = a / b;

    // Nth Digit from right in Base B
    return a % b;
}

// Driver Code
public static void main(String[] args)
{
    int a = 100;
    int n = 3;
    int b = 4;
    System.out.print(nthDigit(a, n, b));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Ptyhon3 Implementation to find Nth digit
# from right in base B

# Function to compute Nth digit
# from right in base B
def nthDigit(a, n, b):

    # Skip N-1 Digits in Base B
    for i in range(1, n):
        a = a // b

    # Nth Digit from right in Base B
    return a % b

# Driver Code
a = 100
n = 3
b = 4
print(nthDigit(a, n, b))

# This code is contributed by ApurvaRaj
```

## C#

```
// C# Implementation to find Nth digit
// from right in base B
using System;

class GFG
{

    // Function to compute Nth digit
    // from right in base B
    static int nthDigit(int a, int n, int b)
    {

        // Skip N-1 Digits in Base B
        for (int i = 1; i < n; i++)
            a = a / b;

        // Nth Digit from right in Base B
        return a % b;
    }

    // Driver Code
    public static void Main()
    {
        int a = 100;
        int n = 3;
        int b = 4;
        Console.Write(nthDigit(a, n, b));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript Implementation to find Nth digit
// from right in base B

// Function to compute Nth digit
// from right in base B
function nthDigit(a, n, b)
{

    // Skip N-1 Digits in Base B
    for (var i = 1; i < n; i++)
        a = parseInt(a / b);

    // Nth Digit from right in Base B
    return a % b;
}

// Driver Code
var a = 100;
var n = 3;
var b = 4;
document.write(nthDigit(a, n, b));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(1)