# 将所有位翻转到最右侧设置位左侧形成的数字

> 原文:[https://www . geeksforgeeks . org/number-通过将所有位翻转到最右侧集合位的左侧形成/](https://www.geeksforgeeks.org/number-formed-by-flipping-all-bits-to-the-left-of-rightmost-set-bit/)

给定一个**整数 N** ，任务是将所有的位翻转到最右边设置位的左边，并打印生成的数字。

**示例:**

> **输入:** N = 10
> **输出:** 6
> **解释:**
> 10(二进制 1010)
> 将所有位向左翻转到最右边的设置位(索引 2)
> - > 6(二进制 0110)
> 
> **输入:** N = 120
> **输出:** 8
> **解释:**
> 120(二进制 1111000)
> 将所有位向左翻转到最右边的设置位(索引 3)
> - > 8(二进制 0001000)

**天真方法:**
要解决上面提到的问题，我们将遵循下面给出的步骤:

*   将给定的整数转换为二进制形式，并将每个位存储到数组中。
*   遍历数组并在第一次出现 1 后断开。
*   将所有位翻转到该索引的左侧。将二进制序列转换成十进制数并返回。

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效方法:**
为了优化上述方法，我们将尝试使用**按位运算符**。

1.  我们从最右侧找到设置的位位置，即 LSB 和总位数。
2.  将给定的数与所有设置位的总数等于总位数的数进行异或运算。
3.  我们不想将最右边的位从设置位翻转过来。因此，我们再次对所有设置位的总数等于第一位的数进行异或运算

下面是上述方法的实现:

## C++

```
// C++ program to find the
// integer formed after flipping
// all bits to the left of the
// rightmost set bit
#include <bits/stdc++.h>
using namespace std;

int totCount;
int firstCount;

// Function to get the total count
void getTotCount(int num)
{
    totCount = 1;
    firstCount = 1;
    int temp = 1;

    // Moving until we get
    // the rightmost set bit
    while ((num & temp) == 0)
    {
        temp = temp << 1;
        totCount += 1;
    }

    firstCount = totCount;
    temp = num >> totCount;

    // To get total number
    // of bits in a number
    while (temp != 0)
    {
        totCount += 1;
        temp = temp >> 1;
    }
}

// Function to find the integer formed
// after flipping all bits to the left
// of the rightmost set bit
int flipBitsFromRightMostSetBit(int num)
{

    // Find the total count of bits and
    // the rightmost set bit
    getTotCount(num);

    // XOR given number with the
    // number which has is made up
    // of only totbits set
    int num1 = num ^ ((1 << totCount) - 1);

    // To avoid flipping the bits
    // to the right of the set bit,
    // take XOR with the number
    // made up of only set firstbits
    num1 = num1 ^ ((1 << firstCount) - 1);

    return num1;
}

// Driver Code
int main()
{
    int n = 120;

    cout << flipBitsFromRightMostSetBit(n)
         << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// integer formed after flipping
// all bits to the left of the
// rightmost set bit
import java.util.*;

class GFG{

static int totCount;
static int firstCount;

// Function to get the total count
static void getTotCount(int num)
{
    totCount = 1;
    firstCount = 1;
    int temp = 1;

    // Moving until we get
    // the rightmost set bit
    while ((num & temp) == 0)
    {
        temp = temp << 1;
        totCount += 1;
    }

    firstCount = totCount;
    temp = num >> totCount;

    // To get total number
    // of bits in a number
    while (temp != 0)
    {
        totCount += 1;
        temp = temp >> 1;
    }
}

// Function to find the integer formed
// after flipping all bits to the left
// of the rightmost set bit
static int flipBitsFromRightMostSetBit(int num)
{

    // Find the total count of bits and
    // the rightmost set bit
    getTotCount(num);

    // XOR given number with the
    // number which has is made up
    // of only totbits set
    int num1 = num ^ ((1 << totCount) - 1);

    // To avoid flipping the bits
    // to the right of the set bit,
    // take XOR with the number
    // made up of only set firstbits
    num1 = num1 ^ ((1 << firstCount) - 1);

    return num1;
}

// Driver Code
public static void main (String[] args)
{
    int n = 120;

    System.out.println(
        flipBitsFromRightMostSetBit(n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the
# integer formed after flipping
# all bits to the left of the
# rightmost set bit

# Function to get the total count
def getTotCount(num):
    totCount = 1
    firstCount = 1

    temp = 1

    # Moving until we get
    # the rightmost set bit
    while (not(num & temp)):
        temp = temp << 1
        totCount += 1
    firstCount = totCount

    temp = num >> totCount

    # To get total number
    # of bits in a number
    while (temp):
        totCount += 1
        temp = temp >> 1

    return totCount, firstCount

# Function to find the integer formed
# after flipping all bits to the left
# of the rightmost set bit
def flipBitsFromRightMostSetBit(num):

    # Find the total count of bits and
    # the rightmost set bit
    totbit, firstbit = getTotCount(num)

    # XOR given number with the
    # number which has is made up
    # of only totbits set

    num1 = num ^ ((1 << totbit) - 1)

    # To avoid flipping the bits
    # to the right of the set bit,
    # take XOR with the number
    # made up of only set firstbits

    num1 = num1 ^ ((1 << firstbit) - 1)

    return num1

if __name__=='__main__':
    n = 120
    print(flipBitsFromRightMostSetBit(n))
```

## C#

```
// C# program to find the
// integer formed after flipping
// all bits to the left of the
// rightmost set bit
using System;

class GFG{

static int totCount;
static int firstCount;

// Function to get the total count
static void getTotCount(int num)
{
    totCount = 1;
    firstCount = 1;
    int temp = 1;

    // Moving until we get
    // the rightmost set bit
    while ((num & temp) == 0)
    {
        temp = temp << 1;
        totCount += 1;
    }

    firstCount = totCount;
    temp = num >> totCount;

    // To get total number
    // of bits in a number
    while (temp != 0)
    {
        totCount += 1;
        temp = temp >> 1;
    }
}

// Function to find the integer formed
// after flipping all bits to the left
// of the rightmost set bit
static int flipBitsFromRightMostSetBit(int num)
{

    // Find the total count of bits and
    // the rightmost set bit
    getTotCount(num);

    // XOR given number with the
    // number which has is made up
    // of only totbits set
    int num1 = num ^ ((1 << totCount) - 1);

    // To avoid flipping the bits
    // to the right of the set bit,
    // take XOR with the number
    // made up of only set firstbits
    num1 = num1 ^ ((1 << firstCount) - 1);

    return num1;
}

// Driver Code
public static void Main (string[] args)
{
    int n = 120;

    Console.Write(
        flipBitsFromRightMostSetBit(n));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript program to find the
// integer formed after flipping
// all bits to the left of the
// rightmost set bit
let totCount;
let firstCount;

// Function to get the total count
function getTotCount(num)
{
    totCount = 1;
    firstCount = 1;
    let temp = 1;

    // Moving until we get
    // the rightmost set bit
    while ((num & temp) == 0)
    {
        temp = temp << 1;
        totCount += 1;
    }

    firstCount = totCount;
    temp = num >> totCount;

    // To get total number
    // of bits in a number
    while (temp != 0)
    {
        totCount += 1;
        temp = temp >> 1;
    }
}

// Function to find the integer formed
// after flipping all bits to the left
// of the rightmost set bit
function flipBitsFromRightMostSetBit(num)
{

    // Find the total count of bits and
    // the rightmost set bit
    getTotCount(num);

    // XOR given number with the
    // number which has is made up
    // of only totbits set
    let num1 = num ^ ((1 << totCount) - 1);

    // To avoid flipping the bits
    // to the right of the set bit,
    // take XOR with the number
    // made up of only set firstbits
    num1 = num1 ^ ((1 << firstCount) - 1);

    return num1;
}

// Driver Code
let n = 120;

document.write(flipBitsFromRightMostSetBit(n));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*