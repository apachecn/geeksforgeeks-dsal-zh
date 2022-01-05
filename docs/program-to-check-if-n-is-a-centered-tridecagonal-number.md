# 检查 N 是否为中心三叉数的程序

> 原文:[https://www . geeksforgeeks . org/program-to-check-if-n-is-a-centered-tridecagonal-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-centered-tridecagonal-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为[中心三叉戟数字](https://www.geeksforgeeks.org/centered-tridecagonal-number/)。如果数字 **N** 是居中的三叉戟数字，则打印**“是”**否则打印**“否”**。

> [**【居中三叉编号】**](https://www.geeksforgeeks.org/centered-tridecagonal-number/) 代表连续三叉( **13 边多边形**)图层中位于中心的一个点和围绕中心点的其他点。前几个居中的三叉戟数字是 **1、14、40、79……**

**示例:**

> **输入:** N = 14
> **输出:**是
> **说明:**
> 秒心三叉戟号为 14。
> 
> **输入:**N = 30
> T3】输出:否

**进场:**

1.中心三叉戟编号的第**K**项为
![K^{th} Term = \frac{{13*K^{2} - 13*K + 2}}{2}     ](img/e8a355166e453dbf82f365a02f992cfa.png "Rendered by QuickLaTeX.com")

2.因为我们必须检查给定的数是否可以表示为一个[中心三叉数](https://www.geeksforgeeks.org/centered-tridecagonal-number/)。这可以通过以下方式进行检查:

> => ![N = \frac{{13*K^{2} - 13*K + 2}}{2}     ](img/07f3557ce3317e96db42f3625c1b9163.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{13 + \sqrt{104*N + 65}}{26}  ](img/a87ee157c493bc3cdef44923d671858c.png "Rendered by QuickLaTeX.com")

3.如果用上述公式计算出的 **K** 的值是一个整数，那么 **N** 就是一个居中的三叉数。

4.否则数字 **N** 不是一个中心三叉戟数字。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number N
// is a Centered tridecagonal number
bool isCenteredtridecagonal(int N)
{
    float n
        = (13 + sqrt(104 * N + 65))
          / 26;

    // Condition to check if the N
    // is a Centered tridecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 14;

    // Function call
    if (isCenteredtridecagonal(N)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the number N
// is a centered tridecagonal number
static boolean isCenteredtridecagonal(int N)
{
    float n = (float) ((13 + Math.sqrt(104 * N +
                                       65)) / 26);

    // Condition to check if the N
    // is a centered tridecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void main(String[] args)
{

    // Given Number
    int N = 14;

    // Function call
    if (isCenteredtridecagonal(N))
    {
        System.out.print("Yes");
    }
    else
    {
        System.out.print("No");
    }
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for the above approach
import numpy as np

# Function to check if the number N
# is a centered tridecagonal number
def isCenteredtridecagonal(N):

    n = (13 + np.sqrt(104 * N + 65)) / 26

    # Condition to check if N
    # is centered tridecagonal number
    return (n - int(n)) == 0

# Driver Code
N = 14

# Function call
if (isCenteredtridecagonal(N)):
    print ("Yes")
else:
    print ("No")

# This code is contributed by PratikBasu
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the number N
// is a centered tridecagonal number
static bool isCenteredtridecagonal(int N)
{
    float n = (float) ((13 + Math.Sqrt(104 * N +
                                       65)) / 26);

    // Condition to check if the N
    // is a centered tridecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void Main(string[] args)
{

    // Given Number
    int N = 14;

    // Function call
    if (isCenteredtridecagonal(N))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if the number N
// is a Centered tridecagonal number
function isCenteredtridecagonal(N)
{
    let n
        = (13 + Math.sqrt(104 * N + 65))
          / 26;

    // Condition to check if the N
    // is a Centered tridecagonal number
    return (n - parseInt(n)) == 0;
}

// Driver Code
// Given Number
let N = 14;

// Function call
if (isCenteredtridecagonal(N)) {
    document.write("Yes");
}
else {
    document.write("No");
}

// This code is contributed by subham348.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*