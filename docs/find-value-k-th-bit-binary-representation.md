# 求二进制表示中第 k 位的值

> 原文:[https://www . geesforgeks . org/find-value-k-th-bit-binary-presentation/](https://www.geeksforgeeks.org/find-value-k-th-bit-binary-representation/)

给定数字 n 和 k (1 <= k <= 32)，求 n 的二进制表示中第 k 位的值。位从右(最低有效位)到左(最高有效位)编号。

**示例:**

```
Input : 
n = 13, k = 2
Output : 
0
Explanation:
Binary representation of 13 is 1101.
Second bit from right is 0.

Input :  
n = 14, k = 3
Output : 
1
Explanation:
Binary representation of 14 is 1110.
Third bit from right is 1.
```

**进场:**
1)找一个除第 k 个位置外全为 0 的数字。我们使用(1 < < (k-1))得到这个数字。例如，如果 k = 3，那么(1 < < 2)给我们(00..00100).
2)用 n 对上述获得的数进行按位“与”运算，找出 n 中的第 k 位是否置位。

下面是上述方法的实现:

## C++

```
// CPP program to find k-th bit from right
#include <bits/stdc++.h>
using namespace std;

void printKthBit(unsigned int n, unsigned int k)
{
    cout << ((n & (1 << (k - 1))) >> (k - 1));
}

// Driver Code
int main()
{
    unsigned int n = 13, k = 2;

    // Function Call
    printKthBit(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// k-th bit from right
import java.io.*;

class GFG {
    static void printKthBit(long n, long k)
    {
        System.out.println(
            ((n & (1 << (k - 1))) >> (k - 1)));
    }

    // Driver Code
    public static void main(String[] args)
    {
        long n = 13, k = 2;

        // Function Call
        printKthBit(n, k);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find
# k-th bit from right

def printKthBit(n, k):

    print((n & (1 << (k - 1))) >> (k - 1))

# Driver Code
n = 13
k = 2

# Function Call
printKthBit(n, k)

# This code is contributed by Smitha
```

## C#

```
// C# program to find k-th bit from right
using System;

class GFG {

    static void printKthBit(long n, long k)
    {
        Console.WriteLine((n & (1 << (k - 1))) >> (k - 1));
    }

    // Driver Code
    public static void Main()
    {
        long n = 13, k = 2;

        // Function Call
        printKthBit(n, k);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// k-th bit from right

function printKthBit($n, $k)
{
    echo ($n & (1 << ($k - 1)));
}

// Driver Code
$n = 13; $k = 2;
printKthBit($n, $k);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find k-th bit from right

function printKthBit(n, k)
{
    document.write((n & (1 << (k - 1))) >> (k - 1));
}

// Driver Code
var n = 13, k = 2;

// Function Call
printKthBit(n, k);

</script>
```

**Output :** 

```
0
```