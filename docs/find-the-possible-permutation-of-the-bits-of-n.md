# 找出 N 位的可能排列

> 原文:[https://www . geeksforgeeks . org/find-the-the-the-the-of-bit-of-n/](https://www.geeksforgeeks.org/find-the-possible-permutation-of-the-bits-of-n/)

给定一个整数 **N** ，任务是找出 **N** 的位是否可以交替排列，即 **0101…** 或 **10101…** 。假设 **N** 表示为一个 **32** 位整数。
**示例:**

> **输入:** N = 23
> **输出:**否
> “0000000000000000000000000000000000111”是 23
> 的二进制表示，所需的比特排列是不可能的。
> **输入:** N = 524280
> **输出:**是
> 二进制(524280)=“0000000000011111111111000”，可通过
> 重排为“01010101010101010101010101010101”。

**方法:**由于给定的整数必须用 32 位表示，并且 1 的数量必须等于其二进制表示中的 0 的数量，才能满足给定的条件。因此，N 中的设置位数必须为 16，这可以使用 [__builtin_popcount()](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)
轻松计算。以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int TOTAL_BITS = 32;

// Function that returns true if it is
// possible to arrange the bits of
// n in alternate fashion
bool isPossible(int n)
{

    // To store the count of 1s in the
    // binary representation of n
    int cnt = __builtin_popcount(n);

    // If the number set bits and the
    // number of unset bits is equal
    if (cnt == TOTAL_BITS / 2)
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 524280;

    if (isPossible(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int TOTAL_BITS = 32;

// Function that returns true if it is
// possible to arrange the bits of
// n in alternate fashion
static boolean isPossible(int n)
{

    // To store the count of 1s in the
    // binary representation of n
    int cnt = Integer.bitCount(n);

    // If the number set bits and the
    // number of unset bits is equal
    if (cnt == TOTAL_BITS / 2)
        return true;
    return false;
}

// Driver code
static public void main (String []arr)
{
    int n = 524280;

    if (isPossible(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
TOTAL_BITS = 32;

# Function that returns true if it is
# possible to arrange the bits of
# n in alternate fashion
def isPossible(n) :

    # To store the count of 1s in the
    # binary representation of n
    cnt = bin(n).count('1');

    # If the number set bits and the
    # number of unset bits is equal
    if (cnt == TOTAL_BITS // 2) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    n = 524280;

    if (isPossible(n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int TOTAL_BITS = 32;

static int CountBits(int value)
{
    int count = 0;
    while (value != 0)
    {
        count++;
        value &= value - 1;
    }
    return count;
}

// Function that returns true if it is
// possible to arrange the bits of
// n in alternate fashion
static bool isPossible(int n)
{

    // To store the count of 1s in the
    // binary representation of n
    int cnt = CountBits(n);

    // If the number set bits and the
    // number of unset bits is equal
    if (cnt == TOTAL_BITS / 2)
        return true;
    return false;
}

// Driver code
public static void Main (String []arr)
{
    int n = 524280;

    if (isPossible(n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const TOTAL_BITS = 32;

function CountBits(value)
{
    let count = 0;
    while (value != 0)
    {
        count++;
        value &= value - 1;
    }
    return count;
}

// Function that returns true if it is
// possible to arrange the bits of
// n in alternate fashion
function isPossible(n)
{

    // To store the count of 1s in the
    // binary representation of n
    let cnt = CountBits(n);

    // If the number set bits and the
    // number of unset bits is equal
    if (cnt == parseInt(TOTAL_BITS / 2))
        return true;
    return false;
}

// Driver code
    let n = 524280;

    if (isPossible(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
Yes
```