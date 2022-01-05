# 翻转两个给定数字的设置位的计数总和的位

> 原文:[https://www . geeksforgeeks . org/两个给定数字的位数总和的翻转位/](https://www.geeksforgeeks.org/flip-bits-of-the-sum-of-count-of-set-bits-of-two-given-numbers/)

给定两个数字 **A** 和 **B** ，任务是统计 **A** 和 **B** 中的设定位数，并翻转所得和的位数。

**示例:**

> **输入:** A = 5，B = 7
> **输出:** 2
> **说明:**
> A 的二进制表示为 101。
> B 的二进制表示为 111。
> A 和 B 中设置位的计数= 2 + 3 = 5。
> 所得和的二进制表示= 101
> 翻转和的位，得到的数为(010) <sub>2</sub> = 2。
> 因此，要求输出为 2。
> 
> **输入:** A = 76，B = 35
> **输出:** 1
> **解释:**
> A 的二进制表示为 1001100
> B 的二进制表示为 100011
> A 和 B 中的设置位计数= 3 + 3 = 6
> 所得到的和的二进制表示= 110
> 翻转和的位，得到的数为(001) <sub>2
> 因此，要求输出为 1。</sub>

**天真方法:**解决这个问题的想法是首先[遍历两个数字的二进制表示](https://www.geeksforgeeks.org/check-bits-number-set/)，然后[计算两个数字中设置位的数量](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。最后，将它们相加并[反转结果数的位](https://www.geeksforgeeks.org/program-to-invert-bits-of-a-number-efficiently/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// set bits in integer
int countSetBits(int n)
{
    // Variable for counting set bits
    int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to invert bits of a number
int invertBits(int n)
{
    // Calculate number of bits of N-1;
    int x = log2(n);

    int m = 1 << x;
    m = m | m - 1;
    n = n ^ m;

    return n;
}

// Function to invert the sum
// of set bits in A and B
void invertSum(int A, int B)
{

    // Stores sum of set bits
    int temp = countSetBits(A)
               + countSetBits(B);
    cout << invertBits(temp) << endl;
}

// Driver Code
int main()
{
    int A = 5;
    int B = 7;

    invertSum(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count number of
// set bits in integer
static int countSetBits(int n)
{

    // Variable for counting set bits
    int count = 0;

    while (n != 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to invert bits of a number
static int invertBits(int n)
{

    // Calculate number of bits of N-1;
    int x = (int)(Math.log(n) / Math.log(2));

    int m = 1 << x;
    m = m | m - 1;
    n = n ^ m;

    return n;
}

// Function to invert the sum
// of set bits in A and B
static void invertSum(int A, int B)
{

    // Stores sum of set bits
    int temp = countSetBits(A) +
               countSetBits(B);

    System.out.print(invertBits(temp));
}

// Driver Code
static public void main(String args[])
{
    int A = 5;
    int B = 7;

    invertSum(A, B);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to count number of
# set bits in integer
def countSetBits(n):

    # Variable for counting set bits
    count = 0

    while (n != 0):
        n &= (n - 1)
        count += 1

    return count

# Function to invert bits of a number
def invertBits(n):

    # Calculate number of bits of N-1;
    x = (int)(math.log(n) / math.log(2))

    m = 1 << x
    m = m | m - 1
    n = n ^ m

    return n

# Function to invert the sum
# of set bits in A and B
def invertSum(A, B):

    # Stores sum of set bits
    temp = countSetBits(A) + countSetBits(B)

    print(invertBits(temp))

# Driver Code
A = 5
B = 7

invertSum(A, B)

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count number of
// set bits in integer
static int countSetBits(int n)
{

    // Variable for counting set bits
    int count = 0;
    while (n != 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to invert bits of a number
static int invertBits(int n)
{

    // Calculate number of bits of N-1;
    int x = (int)Math.Log(n, 2);

    int m = 1 << x;
    m = m | m - 1;
    n = n ^ m;

    return n;
}

// Function to invert the sum
// of set bits in A and B
static void invertSum(int A, int B)
{

    // Stores sum of set bits
    int temp = countSetBits(A) +
               countSetBits(B);

    Console.WriteLine(invertBits(temp));
}

// Driver Code
static void Main()
{
    int A = 5;
    int B = 7;

    invertSum(A, B);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count number of
// set bits in integer
function countSetBits(n)
{

    // Variable for counting set bits
    var count = 0;

    while (n != 0)
    {
        n &= (n - 1);
        count++;
    }
    return count;
}

// Function to invert bits of a number
function invertBits(n)
{

    // Calculate number of bits of N-1;
    var x = parseInt((Math.log(n) /
                      Math.log(2)));

    var m = 1 << x;
    m = m | m - 1;
    n = n ^ m;

    return n;
}

// Function to invert the sum
// of set bits in A and B
function invertSum(A, B)
{

    // Stores sum of set bits
    var temp = countSetBits(A) +
               countSetBits(B);

    document.write(invertBits(temp));
}

// Driver Code
var A = 5;
var B = 7;

invertSum(A, B);

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*