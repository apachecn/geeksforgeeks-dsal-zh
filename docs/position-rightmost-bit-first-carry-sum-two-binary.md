# 两个二进制数之和中第一个进位的最右位的位置

> 原文:[https://www . geesforgeks . org/position-最右位-第一位-进位-和-二进制/](https://www.geeksforgeeks.org/position-rightmost-bit-first-carry-sum-two-binary/)

给定两个非负整数 **a** 和 **b** 。问题是在 **a** 和 **b** 的二进制加法中找到产生进位的最右位的位置。

示例:

```
Input : a = 10, b = 2
Output : 2
(10)<sub>10</sub> = (1010)2
(2)<sub>10</sub> = (10)2.
  1010
+   10
As highlighted, 1st carry bit from the right 
will be generated at position '2'.

Input : a = 10, b = 5
Output : 0
'0' as no carry bit will be generated.
```

**逼近:**步骤如下:

1.  Calculate **number** = a & B. 。
2.  Find the position of the rightmost setting bit [in the number .](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)

## c++

```
// C++ implementation to find the position of
// rightmost bit where a carry is generated first
#include <bits/stdc++.h>
using namespace std;

typedef unsigned long long int ull;

// function to find the position of
// rightmost set bit in 'n'
unsigned int posOfRightmostSetBit(ull n)
{
    return log2(n & -n) + 1;
}

// function to find the position of rightmost
// bit where a carry is generated first
unsigned int posOfCarryBit(ull a, ull b)
{
    return posOfRightmostSetBit(a & b);
}

// Driver program to test above
int main()
{
    ull a = 10, b = 2;
    cout << posOfCarryBit(a, b);
    return 0;
}
```

## Java

```
// Java implementation to find the position of
// rightmost bit where a carry is generated first
class GFG {

    // function to find the position of
    // rightmost set bit in 'n'
    static int posOfRightmostSetBit(int n)
    {
        return (int)(Math.log(n & -n) / Math.log(2)) + 1;
    }

    // function to find the position of rightmost
    // bit where a carry is generated first
    static int posOfCarryBit(int a, int b)
    {
        return posOfRightmostSetBit(a & b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 10, b = 2;

        System.out.print(posOfCarryBit(a, b));
    }
}

// This code is contributed by Anant Agarwal.
```

## python 3

```
# Python3 implementation to find the position of
# rightmost bit where a carry is generated first

import math

# function to find the position of
# rightmost set bit in 'n'
def posOfRightmostSetBit( n ):
    return int(math.log2(n & -n) + 1)

# function to find the position of rightmost
# bit where a carry is generated first
def posOfCarryBit( a , b ):
    return posOfRightmostSetBit(a & b)

# Driver program to test above
a = 10
b = 2
print(posOfCarryBit(a, b))

# This code is contributed by "Sharad_Bhardwaj".
```

T32】c#T3T36】JavascriptT4】T40】

**输出:**

```
2
```