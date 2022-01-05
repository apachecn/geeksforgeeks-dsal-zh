# 120 边数

> 原文:[https://www.geeksforgeeks.org/120-gon-number/](https://www.geeksforgeeks.org/120-gon-number/)

给定一个 **N** 号，任务是找到 **N <sup>第</sup>T5【120-gon 号。** 

> 120 边数是一类图形数。它有一个 120 边的多边形，叫做 120 边。第 N 个 120 边数是 120 个数的点，所有其他点都被一个公共的共享角包围并形成一个图案。前几个 120 边的数字是 **1，120，357，712，1185，1776，…**

**例:**

> **输入:** N = 2
> **输出:** 120
> **说明:**
> 第二个 120-淋病号为 120。
> **输入:** N = 3
> **输出:** 357

**方法:**第 N 个 120 边数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}   ](img/e1b7be7ec1f82453b47cd0c23edff33f.png "Rendered by QuickLaTeX.com")

*   因此 120 边多边形的第 n 项为

> ![Tn =\frac{((120-2)n^2 - (120-4)n)}{2} =\frac{(118^2 - 116)}{2} ](img/436e174dc8f4ba0ed6f502ac1f42fee0.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ implementation for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the 
// nth 120-gon Number
int gonNum120(int n)
{
    return (118 * n * n - 116 * n) / 2;
}

// Driver Code
int main()
{
    int n = 3;
    cout << gonNum120(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to find the
// nth 120-gon Number
static int gonNum120(int n)
{
    return (118 * n * n - 116 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print(gonNum120(n));
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation for above approach

# Function to find the
# nth 120-gon Number
def gonNum120(n):

    return (118 * n * n - 116 * n) // 2;

# Driver Code
n = 3;
print(gonNum120(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function to find the
// nth 120-gon Number
static int gonNum120(int n)
{
    return (118 * n * n - 116 * n) / 2;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    Console.Write(gonNum120(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript implementation for above approach

// Function to find the 
// nth 120-gon Number
function gonNum120(n)
{
    return (118 * n * n - 116 * n) / 2;
}

// Driver Code
var n = 3;
document.write(gonNum120(n));

</script>
```

**Output:** 

```
357
```

**时间复杂度:** O(1)

**参考资料:**[https://en . Wikipedia . org/wiki/120-gon](https://en.wikipedia.org/wiki/120-gon)