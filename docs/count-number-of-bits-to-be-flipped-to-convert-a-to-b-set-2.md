# 计数要翻转的位数，将 A 转换为 B | Set-2

> 原文:[https://www . geesforgeks . org/count-要翻转的位数-转换-a 到 b-set-2/](https://www.geeksforgeeks.org/count-number-of-bits-to-be-flipped-to-convert-a-to-b-set-2/)

给定两个整数 **A** 和 **B** ，任务是计算将 **A** 转换为 **B** 所需翻转的位数。
**举例:**

> **输入:** A = 10，B = 7
> **输出:** 3
> 二进制(10) = 1010
> 二进制(7)= 0111
> **10**1**0**
> **01**1**1**
> 3 位需要翻转。
> **输入:** A = 8，B = 7
> **输出:** 4

**方法:**解决这个问题的方法已经讨论过了[这里](https://www.geeksforgeeks.org/count-number-of-bits-to-be-flipped-to-convert-a-to-b/)。这里，需要翻转的位数可以通过逐个匹配两个整数中的所有位来找到。如果所考虑的位不同，则递增计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of bits
// to be flipped to convert a to b
int countBits(int a, int b)
{

    // To store the required count
    int count = 0;

    // Loop until both of them become zero
    while (a || b) {

        // Store the last bits in a
        // as well as b
        int last_bit_a = a & 1;
        int last_bit_b = b & 1;

        // If the current bit is not same
        // in both the integers
        if (last_bit_a != last_bit_b)
            count++;

        // Right shift both the integers by 1
        a = a >> 1;
        b = b >> 1;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int a = 10, b = 7;

    cout << countBits(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to return the count of bits
// to be flipped to convert a to b
static int countBits(int a, int b)
{

    // To store the required count
    int count = 0;

    // Loop until both of them become zero
    while (a > 0 || b > 0)
    {

        // Store the last bits in a
        // as well as b
        int last_bit_a = a & 1;
        int last_bit_b = b & 1;

        // If the current bit is not same
        // in both the integers
        if (last_bit_a != last_bit_b)
            count++;

        // Right shift both the integers by 1
        a = a >> 1;
        b = b >> 1;
    }

    // Return the count
    return count;
}

// Driver code
public static void main(String[] args)
{
    int a = 10, b = 7;

    System.out.println(countBits(a, b));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of bits
# to be flipped to convert a to b
def countBits(a, b):

    # To store the required count
    count = 0

    # Loop until both of them become zero
    while (a or b):

        # Store the last bits in a
        # as well as b
        last_bit_a = a & 1
        last_bit_b = b & 1

        # If the current bit is not same
        # in both the integers
        if (last_bit_a != last_bit_b):
            count += 1

        # Right shift both the integers by 1
        a = a >> 1
        b = b >> 1

    # Return the count
    return count

# Driver code
a = 10
b = 7

print(countBits(a, b))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the count of bits
// to be flipped to convert a to b
static int countBits(int a, int b)
{

    // To store the required count
    int count = 0;

    // Loop until both of them become zero
    while (a > 0 || b > 0)
    {

        // Store the last bits in a
        // as well as b
        int last_bit_a = a & 1;
        int last_bit_b = b & 1;

        // If the current bit is not same
        // in both the integers
        if (last_bit_a != last_bit_b)
            count++;

        // Right shift both the integers by 1
        a = a >> 1;
        b = b >> 1;
    }

    // Return the count
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int a = 10, b = 7;

    Console.WriteLine(countBits(a, b));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of bits
// to be flipped to convert a to b
function countBits(a, b)
{

    // To store the required count
    var count = 0;

    // Loop until both of them become zero
    while (a || b) {

        // Store the last bits in a
        // as well as b
        var last_bit_a = a & 1;
        var last_bit_b = b & 1;

        // If the current bit is not same
        // in both the integers
        if (last_bit_a != last_bit_b)
            count++;

        // Right shift both the integers by 1
        a = a >> 1;
        b = b >> 1;
    }

    // Return the count
    return count;
}

// Driver code
    var a = 10, b = 7;
    document.write(countBits(a, b));

</script>
```

**Output:** 

```
3
```

时间复杂度:O(最小值(对数 a，对数 b))

辅助空间:0(1)