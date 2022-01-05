# 程序切换数字 N 的第 K 位

> 原文:[https://www . geesforgeks . org/program-to-toggle-k-th-bit-of-a-number-n/](https://www.geeksforgeeks.org/program-to-toggle-k-th-bit-of-a-number-n/)

给定一个数字 N，任务是清除这个数字 N 的第 K 位。如果第 K 位是 0，那么将其设置为 1，如果是 1，那么将其设置为 0。

**例:**

```
Input: N = 5, K = 2
Output: 7
5 is represented as 101 in binary
and has its second bit 0, so toggling
it will result in 111 i.e. 7.

Input: N = 5, K = 1
Output: 4
5 is represented as 101 in binary
and has its first bit is 1, so toggling
it will result in 100 i.e. 4.
```

**方法:**

*   Because the XOR of the unset and set bits produces the set bits, the XOR of the set and set bits produces the unset bits. Therefore, performing bitwise XOR of any bit and the set bit will result in the switching of the bit, that is

```
Any bit <bitwise XOR> Set bit = Toggle

which means,
0 ^ 1 = 1
1 ^ 1 = 0
```

*   . Therefore, in order to switch a bit, it is the best idea to perform bit-by-bit difference between digital and reset bits.

```
n = n ^ 1 << k
OR
n ^= 1 << k

where k is the bit that is to be cleared
```

下面是上述方法的实现:

## C++

```
// C++ program to toggle K-th bit of a number N
#include<bits/stdc++.h>
using namespace std;

// Function to toggle the kth bit of n
int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}

// Driver code
int main()
{
    int n = 5, k = 2;
    cout << toggleBit(n, k) << endl;

    return 0;
}

// This code is contributed by noob2000
```

## C

```
// C program to toggle K-th bit of a number N

#include <stdio.h>

// Function to toggle the kth bit of n
int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}

// Driver code
int main()
{
    int n = 5, k = 2;

    printf("%d\n", toggleBit(n, k));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle K-th bit of a number N
class GFG
{

// Function to toggle the kth bit of n
static int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}

// Driver code
public static void main(String []args)
{
    int n = 5, k = 2;

    System.out.printf("%d\n", toggleBit(n, k));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to clear K-th bit
# of a number N

# Function to toggle the kth bit of n
def toggleBit(n, k) :

    return (n ^ (1 << (k - 1)));

# Driver code
if __name__ == "__main__" :

    n = 5; k = 2;

    print(toggleBit(n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to toggle K-th bit of a number N
using System;

class GFG
{

// Function to toggle the kth bit of n
static int toggleBit(int n, int k)
{
    return (n ^ (1 << (k - 1)));
}

// Driver code
public static void Main(String []args)
{
    int n = 5, k = 2;

    Console.WriteLine("{0}", toggleBit(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to toggle K-th bit of a number N

// Function to toggle the kth bit of n
function toggleBit(n, k)
{
    return (n ^ (1 << (k - 1)));
}

// Driver code
var n = 5, k = 2;
document.write( toggleBit(n, k));

// This code is contributed by famously.
</script>
```

**Output:** 

```
7
```

时间复杂度:0(1)

辅助空间:0(1)