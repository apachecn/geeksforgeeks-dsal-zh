# 清除数字 N 的第 K 位的程序

> 原文:[https://www . geesforgeks . org/program-to-clear-k-th-bit-of-number-n/](https://www.geeksforgeeks.org/program-to-clear-k-th-bit-of-a-number-n/)

给定一个数字 N，任务是清除这个数字 N 的第 K 位。如果第 K 位是 1，那么清除它到 0，如果它是 0，那么保持它不变。
**例:**

```
Input: N = 5, K = 1
Output: 4
5 is represented as 101 in binary
and has its first bit 1, so clearing
it will result in 100 i.e. 4.

Input: N = 5, K = 2
Output: 5
5 is represented as 101 in binary
and has its second bit is already 0,
so clearing it will result in 101 i.e. 5.
```

**进场:**

*   因为具有复位位的任何位的逐位“与”导致复位位，即

```
Any bit <bitwise AND> Reset bit = Reset bit

which means,
0 & 0 = 0
1 & 0 = 0
```

*   因此，为了清除一个位，最好对带有复位位的数字进行按位“与”运算。

```
n = n & ~(1 << k)
OR
n &= ~(1 << k)

where k is the bit that is to be cleared
```

以下是上述方法的实现:

## C

```
// C program to clear K-th bit of a number N

#include <stdio.h>

// Function to clear the kth bit of n
int clearBit(int n, int k)
{
    return (n & (~(1 << (k - 1))));
}

// Driver code
int main()
{
    int n = 5, k = 1;

    printf("%d\n", clearBit(n, k));

    return 0;
}
```

## C++

```
// C++ program to clear K-th bit of a number N

#include <bits/stdc++.h>
using namespace std;

// Function to clear the kth bit of n
int clearBit(int n, int k)
{
    return (n & (~(1 << (k - 1))));
}

// Driver code
int main()
{
    int n = 5, k = 1;

    cout<<clearBit(n, k)<<endl;

    return 0;
}

// This code is contributed by rutvik_56.
```

## 蟒蛇 3

```
# Python3 program to clear
# K-th bit of a number N

# Function to clear the kth bit of n
def clearBit(n, k):
    return (n & ( ~(1 << (k - 1))))

# Driver code
n = 5
k = 1

print(clearBit(n, k))

# This code is contributed
# by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to clear K-th bit of a number N
class GFG
{

    // Function to clear the kth bit of n
    static int clearBit(int n, int k)
    {
        return (n & (~(1 << (k - 1))));
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 5, k = 1;

        System.out.println(clearBit(n, k));
    }
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# program to clear K-th bit of a number N
using System;

class GFG
{

    // Function to clear the kth bit of n
    static int clearBit(int n, int k)
    {
        return (n & (~(1 << (k - 1))));
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 5, k = 1;

        Console.WriteLine(clearBit(n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to clear K-th bit of a number N

// Function to clear the kth bit of n
function clearBit(n, k)
{
    return (n & (~(1 << (k - 1))));
}

// Driver code
var n = 5, k = 1;
document.write( clearBit(n, k));

</script>
```

**Output:** 

```
4
```

时间复杂度:0(1)

辅助空间:0(1)