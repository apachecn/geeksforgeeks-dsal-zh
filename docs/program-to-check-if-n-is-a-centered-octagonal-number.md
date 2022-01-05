# 程序检查 N 是否是一个居中的八边形数字

> 原文:[https://www . geesforgeks . org/program-to-check-if-n-a-centered-八角形-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-centered-octagonal-number/)

给定一个整数 **N** ，任务是检查它是否是一个[中心八角数](https://www.geeksforgeeks.org/centered-octagonal-number/)。如果编号 **N** 是一个居中的八角形编号，则打印**“是”**否则打印**“否”**。

> [**【居中八边形】数字**](https://www.geeksforgeeks.org/centered-octagonal-number/) 代表一个八边形，在连续的八边形层中，一个点位于中心，其他点围绕中心点。前几个居中的八边形数字是 1，9，25，49，81，121，169，225，289，361 …

**示例:**

> **输入:** N = 9
> **输出:**是
> **说明:**
> 秒居中八角数为 9。
> **输入:** 16
> **输出:**否

**进场:**

1.**中心八角形编号**的 **K <sup>第</sup>T3】项给出为
![K^{th} Term = 4*K^{2} - 4*K + 1  ](img/3982561282392e2b50dd213bf894b2c3.png "Rendered by QuickLaTeX.com")**

2.因为我们必须检查给定的数是否可以表示为一个[中心八角数](https://www.geeksforgeeks.org/centered-octagonal-number/)。这可以通过以下方式进行检查–

> => ![N = {4*K^{2} - 4*K + 1}     ](img/fbc2e7bfdf00bb81b67e157bc8ce0f23.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{1 + \sqrt{N}}{2}  ](img/a61a5b15f53cdeb59dd0cd893eb5ebc4.png "Rendered by QuickLaTeX.com")

3.如果用上述公式计算的 **K** 的值是一个整数，那么 **N** 就是一个中心八角数。

4.否则 **N** 不是一个中心八角数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to check if the number N
// is a Centered Octagonal number
bool isCenteredOctagonal(int N)
{
    float n
        = (1 + sqrt(N))
          / 2;

    // Condition to check if the number
    // is a Centered Octagonal number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 9;

    // Function call
    if (isCenteredOctagonal(N)) {
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

// Function to check if the number N
// is a centered octagonal number
static boolean isCenteredOctagonal(int N)
{
    float n = (float) ((1 + Math.sqrt(N)) / 2);

    // Condition to check if the number
    // is a centered octagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void main(String[] args)
{

    // Given Number
    int N = 9;

    // Function call
    if (isCenteredOctagonal(N))
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
# is a centered octagonal number
def isCenteredOctagonal(N):

    n = (1 + np.sqrt(N)) / 2

    # Condition to check if N
    # is a centered octagonal number
    return (n - int(n)) == 0

# Driver Code
N = 9

# Function call
if (isCenteredOctagonal(N)):
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

// Function to check if the number N
// is a centered octagonal number
static bool isCenteredOctagonal(int N)
{
    float n = (float) ((1 + Math.Sqrt(N)) / 2);

    // Condition to check if the number
    // is a centered octagonal number
    return (n - (int)n) == 0;
}

// Driver Code
public static void Main(string[] args)
{

    // Given Number
    int N = 9;

    // Function call
    if (isCenteredOctagonal(N))
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

// javascript program for the above approach

// Function  to check if the number N
// is a Centered Octagonal number
function isCenteredOctagonal( N)
{
    let n
        = (1 + Math.sqrt(N))
          / 2;

    // Condition to check if the number
    // is a Centered Octagonal number
    return (n - parseInt(n)) == 0;
}

// Driver Code

    // Given Number
    let N = 9;

    // Function call
    if (isCenteredOctagonal(N)) {
         document.write( "Yes");
    }
    else {
        document.write( "No");
    }

    // This code contributed by aashish1995

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*