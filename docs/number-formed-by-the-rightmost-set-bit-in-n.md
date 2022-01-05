# 由 N 中最右边的设置位形成的数字

> 原文:[https://www . geesforgeks . org/number-由 n 中最右边的 set 位构成/](https://www.geeksforgeeks.org/number-formed-by-the-rightmost-set-bit-in-n/)

给定一个整数 **N** ，任务是找到一个取 **N** 中最右边的置位形成的整数 **M** ，即 **M** 中唯一的置位将是 **N** 中最右边的置位，其余位将被取消置位。
**举例:**

> **输入:** N = 7
> **输出:** 1
> 7 = 111，最后一个设置位形成的数字为 001 即 1。
> **输入:** N = 10
> **输出:**2
> 10 = 1010->0010 = 2
> **输入:** N = 16
> **输出:** 16

**进场:**

*   存储**x = n&(n–1)**，这将在 **n** 中从右侧取消第一个设置位。
*   现在，更新 **n = n ^ x** 以设置已更改的位，并取消设置所需整数的所有其他位。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the integer formed
// by taking the rightmost set bit in n
int firstSetBit(int n)
{

    // n & (n - 1) unsets the first set
    // bit from the right in n
    int x = n & (n - 1);

    // Take xor with the original number
    // The position of the 'changed bit'
    // will be set and rest will be unset
    return (n ^ x);
}

// Driver code
int main()
{
    int n = 12;

    cout << firstSetBit(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class geeks
{

    // Function to return the integer formed
    // by taking the rightmost set bit in n
    public static int firstSetBit(int n)
    {

        // n & (n - 1) unsets the first set
        // bit from the right in n
        int x = n & (n-1);

        // Take xor with the original number
        // The position of the 'changed bit'
        // will be set and rest will be unset
        return (n ^ x);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 12;
        System.out.println(firstSetBit(n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the integer formed
# by taking the rightmost set bit in n
def firstSetBit(n):

    # n & (n - 1) unsets the first set
    # bit from the right in n
    x = n & (n - 1)

    # Take xor with the original number
    # The position of the 'changed bit'
    # will be set and rest will be unset
    return (n ^ x)

# Driver code
n = 12

print(firstSetBit(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class geeks
{

    // Function to return the integer formed
    // by taking the rightmost set bit in n
    public static int firstSetBit(int n)
    {

        // n & (n - 1) unsets the first set
        // bit from the right in n
        int x = n & (n-1);

        // Take xor with the original number
        // The position of the 'changed bit'
        // will be set and rest will be unset
        return (n ^ x);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 12;
        Console.WriteLine(firstSetBit(n));
    }
}

// This code is contributed by
// anuj_67..
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the integer formed
// by taking the rightmost set bit in n
function firstSetBit(n)
{

    // n & (n - 1) unsets the first set
    // bit from the right in n
    let x = n & (n - 1);

    // Take xor with the original number
    // The position of the 'changed bit'
    // will be set and rest will be unset
    return (n ^ x);
}

// Driver code
    let n = 12;
    document.write(firstSetBit(n));

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(1)

**辅助空间:** O(1)