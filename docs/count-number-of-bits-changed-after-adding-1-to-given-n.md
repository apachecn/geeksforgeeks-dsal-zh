# 计数给定 N 加 1 后改变的位数

> 原文:[https://www . geesforgeks . org/count-给定 n 加 1 后改变的位数/](https://www.geeksforgeeks.org/count-number-of-bits-changed-after-adding-1-to-given-n/)

给定一个整数![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")。任务是找出给定数字加 1 后改变的位数。
**示例** :

```
Input : N = 5
Output : 2
After adding 1 to 5 it becomes 6.
Binary representation of 5 is 101.
Binary representation of 6 is 110.
So, no. of bits changed is 2.

Input : N = 1
Output : 2
```

有三种方法可以在给定值 N 加 1 后得到的结果中找到改变的位数:

*   **方法 1:** 给定整数加 1，比较 N 的位数和相加后的结果，统计不匹配的位数。
*   **方法 2:** 如果将 1 加到 N，则改变的总位数由从右数第一个零的位置定义，即 LSB 为零。在这种情况下，1 被加到 1 上，然后它被改变，并将进位 1 传递到它的下一位，但是如果 1 被加到 0 上，则只有 0 变为 1，并且不再传递进位。
*   **方法 3:** 当给定数加 1 时，要找出改变的位数，进行 n 和 n+1 的异或运算，[计算结果异或值中的设定位数](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)。

以下是**方法 3** 的实施情况:

## C++

```
// CPP program to find the number
// of changed bit
#include <bits/stdc++.h>
using namespace std;

// Function to find number of changed bit
int findChangedBit(int n)
{
    // Calculate xor of n and n+1
    int XOR = n ^ (n + 1);

    // Count set bits in xor value
    int result = __builtin_popcount(XOR);

    // Return the result
    return result;
}

// Driver function
int main()
{
    int n = 6;
    cout << findChangedBit(n) << endl;

    n = 7;
    cout << findChangedBit(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of changed bit
class GFG
{

// Function to find number of changed bit
static int findChangedBit(int n)
{
    // Calculate xor of n and n+1
    int XOR = n ^ (n + 1);

    // Count set bits in xor value
    int result = Integer.bitCount(XOR);

    // Return the result
    return result;
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    System.out.println(findChangedBit(n));

    n = 7;
    System.out.println(findChangedBit(n));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the number
# of changed bit

# Function to find number of changed bit
def findChangedBit(n):

    # Calculate xor of n and n+1
    XOR = n ^ (n + 1)

    # Count set bits in xor value
    result = bin(XOR).count("1")

    # Return the result
    return result

# Driver Code
if __name__ == '__main__':
    n = 6
    print(findChangedBit(n))

    n = 7
    print(findChangedBit(n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number
// of changed bit
using System;

class GFG
{

// Function to find number of changed bit
static int findChangedBit(int n)
{
    // Calculate xor of n and n+1
    int XOR = n ^ (n + 1);

    // Count set bits in xor value
    int result = bitCount(XOR);

    // Return the result
    return result;
}
static int bitCount(int x)
{

    // To store the count
    // of set bits
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int n = 6;
    Console.WriteLine(findChangedBit(n));

    n = 7;
    Console.WriteLine(findChangedBit(n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of changed bit

// Function to find number of changed bit
function findChangedBit(n)
{
    // Calculate xor of n and n+1
    let XOR = n ^ (n + 1);

    // Count set bits in xor value
    let result = bitCount(XOR);

    // Return the result
    return result;
}

function bitCount(x)
{

    // To store the count
    // of set bits
    let setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Driver function
    let n = 6;
    document.write(findChangedBit(n) + "<br>");

    n = 7;
    document.write(findChangedBit(n));

</script>
```

**Output:** 

```
1
4
```