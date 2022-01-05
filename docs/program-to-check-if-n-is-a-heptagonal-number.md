# 检查 N 是否为七边数的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-is-a-七边形-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-heptagonal-number/)

给定一个整数 **N** ，任务是检查 **N** 是否为[七边数](https://www.geeksforgeeks.org/heptagonal-number/)。如果数字 **N** 是七边形数字，则打印**“是”**否则打印**“否”**。

> [**七边数**](https://www.geeksforgeeks.org/heptagonal-number/) 代表七边，属于具象数。七边形有七个角、七个顶点和七条边的多边形。前几个七边形数字是 **1、7、18、34、55、81、…**

**示例:**

> **输入:** N = 7
> **输出:**是
> **说明:**
> 第二个七边数为 7。
> 
> **输入:**N = 30
> T3】输出:否

**进场:**

*   七边形数的第**K**项给出为
    ![K^{th} Term = \frac{5*K^{2} - 3*K}{2}     ](img/f3946fafdc58e47355ea2620205eea94.png "Rendered by QuickLaTeX.com")
*   因为我们必须检查给定的数是否可以表示为七边数。这可以检查为:

> => ![N = \frac{5*K^{2} - 3*K}{2}     ](img/a7a1fc139e086b72f2377669d27e5b90.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{3 + \sqrt{40*N + 9}}{10}     ](img/3517960c6f4cb2e4e93ae29d8740aeda.png "Rendered by QuickLaTeX.com")

*   如果用上述公式计算的 **K** 的值是一个整数，那么 **N** 就是一个七边数。
*   否则 **N** 不是七边数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N is a
// Heptagonal number
bool isheptagonal(int N)
{
    float n
        = (3 + sqrt(40 * N + 9))
          / 10;

    // Condition to check if the
    // number is a heptagonal number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 7;

    // Function call
    if (isheptagonal(N)) {
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
import java.io.*;
import java.util.*;

class GFG {

// Function to check if N
// is a heptagonal number
public static boolean isheptagonal(int N)
{
    double n = (3 + Math.sqrt(40 * N + 9)) / 10;

    // Condition to check if the number
    // is a heptagonal number
    return (n - (int)n) == 0;
}

// Driver code
public static void main(String[] args)
{

    // Given Number
    int N = 7;

    // Function call
    if (isheptagonal(N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if N is a
# heptagonal number
def isheptagonal(N):

    n = (3 + math.sqrt(40 * N + 9)) / 10

    # Condition to check if the
    # number is a heptagonal number
    return (n - int(n)) == 0

# Driver Code
N = 7

# Function call
if (isheptagonal(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by Shubham_Coder
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to check if N
// is a heptagonal number
public static bool isheptagonal(int N)
{
    double n = (3 + Math.Sqrt(40 * N + 9)) / 10;

    // Condition to check if the number
    // is a heptagonal number
    return (n - (int)n) == 0;
}

// Driver code
public static void Main(String[] args)
{

    // Given Number
    int N = 7;

    // Function call
    if (isheptagonal(N))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if N is a
// Heptagonal number
function isheptagonal(N)
{
    var n = (3 + Math.sqrt(40 * N + 9))
          / 10;

    // Condition to check if the
    // number is a heptagonal number
    return (n - parseInt(n)) == 0;
}

// Given Number
var N = 7;
// Function call
if (isheptagonal(N)) {
    document.write("Yes");
}
else {
    document.write("No");
}

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)

**辅助空间:** O(1)