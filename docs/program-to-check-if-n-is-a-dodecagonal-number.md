# 检查 N 是否为十二边形数的程序

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-is-a-十二边形-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-dodecagonal-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为[十二边形数字](https://www.geeksforgeeks.org/dodecagonal-number/)。如果数字 **N** 是十二边形数字，则打印**“是”**否则打印**“否”**。

> [**十二边形数字**](https://www.geeksforgeeks.org/dodecagonal-number/) 代表[十二边形](https://www.geeksforgeeks.org/dodecagonal-number/) ( **12 边多边形**)。前几个十二边形数字是 **1、12、33、64、105、156、217……**

**示例:**

> **输入:** N = 12
> **输出:**是
> **说明:**
> 第二个十二边形数是 12。
> 
> **输入:**N = 30
> T3】输出:否

**进场:**

1.十二边形数的第**K**项给出为
![K^{th} Term = 5*K^{2} - 4*K  ](img/3ea6d729845f7f85df81653eb8ca36f6.png "Rendered by QuickLaTeX.com")

2.因为我们必须检查给定的数是否可以表示为**十二边形数**。这可以通过以下方式进行检查:

> => ![N = 5*K^{2} - 4*K    ](img/0db06e74907772a01db73b8530749aba.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{4 + \sqrt{20*N + 16}}{10}  ](img/a4bdc0746b17f819b7c0c1675b5e9808.png "Rendered by QuickLaTeX.com")

3.如果用上述公式计算的 **K** 的值是一个整数，那么 **N** 就是一个十二边形数。

4.否则数字 **N** 不是十二边形数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if number N
// is a dodecagonal number or not
bool isdodecagonal(int N)
{
    float n
        = (4 + sqrt(20 * N + 16))
          / 10;

    // Condition to check if the
    // N is a dodecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 12;

    // Function call
    if (isdodecagonal(N)) {
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
import java.util.*;

class GFG{

// Function to check if number N
// is a dodecagonal number or not
static boolean isdodecagonal(int N)
{
    float n = (float) ((4 + Math.sqrt(20 * N +
                                      16)) / 10);

    // Condition to check if the
    // N is a dodecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void main(String[] args)
{

    // Given Number
    int N = 12;

    // Function call
    if (isdodecagonal(N))
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

# Function to check if number N
# is a dodecagonal number or not
def isdodecagonal(N):

    n = (4 + np.sqrt(20 * N + 16)) / 10

    # Condition to check if the
    # N is a dodecagonal number
    return (n - int(n)) == 0

# Driver Code
N = 12

# Function call
if (isdodecagonal(N)):
    print("Yes")
else:
    print("No")

# This code is contributed by PratikBasu
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if number N
// is a dodecagonal number or not
static bool isdodecagonal(int N)
{

    float n = (float) ((4 + Math.Sqrt(20 * N +
                                      16)) / 10);

    // Condition to check if the
    // N is a dodecagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void Main(string[] args)
{

    // Given number
    int N = 12;

    // Function call
    if (isdodecagonal(N))
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

// Function to check if number N
// is a dodecagonal number or not
function isdodecagonal(N)
{
    let n
        = (4 + Math.sqrt(20 * N + 16))
          / 10;

    // Condition to check if the
    // N is a dodecagonal number
    return (n - parseInt(n)) == 0;
}

// Driver Code
// Given Number
let N = 12;

// Function call
if (isdodecagonal(N))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*