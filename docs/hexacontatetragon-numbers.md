# 六角体编号

> 原文:[https://www.geeksforgeeks.org/hexacontatetragon-numbers/](https://www.geeksforgeeks.org/hexacontatetragon-numbers/)

给定一个数字 **N** ，任务是找到 **N <sup>第</sup>T5】个六角数。** 

> 六角数是一类图形数。它有一个 64 边的多边形，叫做六角四边形。第 N 个六角点的个数是 64 个点，所有其他点都被一个共同的角包围并形成一个图案。前几个六连字符数字是 **1，64，189，376，625，936，…**

**例:**

> **输入:** N = 2
> **输出:** 64
> **说明:**
> 第二个六连字符数为 64。
> **输入:** N = 3
> **输出:** 189

**方法:**第 N 个六价数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}   ](img/e1b7be7ec1f82453b47cd0c23edff33f.png "Rendered by QuickLaTeX.com")

*   因此 64 边多边形的第 n 项是

> ![Tn =\frac{((64-2)n^2 - (64-4)n)}{2} =\frac{(62^2 - 60)}{2}  ](img/34ba3a0d532cdff1b6a12f53002f74b4.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to Find the
// Nth Hexacontatetragon Number
int HexacontatetragonNum(int n)
{
    return (62 * n * n - 60 * n) / 2;
}

// Driver Code
int main()
{
    int n = 3;
    cout << HexacontatetragonNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// Hexacontatetragon number
class GFG{

// Function to find the nth
// Hexacontatetragon number
static int HexacontatetragonNum(int n)
{
    return (62 * n * n - 60 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print(HexacontatetragonNum(n));
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation for above approach

# Function to Find the
# Nth Hexacontatetragon Number
def HexacontatetragonNum(n):

    return (62 * n * n - 60 * n) / 2;

# Driver Code
n = 3;
print(HexacontatetragonNum(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find N-th
// Hexacontatetragon number
using System;
class GFG{

// Function to find the nth
// Hexacontatetragon number
static int HexacontatetragonNum(int n)
{
    return (62 * n * n - 60 * n) / 2;
}

// Driver code
public static void Main()
{
    int n = 3;
    Console.Write(HexacontatetragonNum(n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find N-th
// Hexacontatetragon number

    // Function to find the nth
    // Hexacontatetragon number
    function HexacontatetragonNum( n) {
        return (62 * n * n - 60 * n) / 2;
    }

    // Driver code

        let n = 3;
        document.write(HexacontatetragonNum(n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
189
```

***时间复杂度:** O(1)*

**参考资料:**[https://en . Wikipedia . org/wiki/hexagon tetra](https://en.wikipedia.org/wiki/Hexacontatetragon)