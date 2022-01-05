# 检查 N 是否为十进制数的程序

> 原文:[https://www . geeksforgeeks . org/program-to-check-if-n-is-a-decagonal-number/](https://www.geeksforgeeks.org/program-to-check-if-n-is-a-decagonal-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为[十边形数字](https://www.geeksforgeeks.org/decagonal-number/)。如果数字 **N** 是十边形数字，则打印**“是”**否则打印**“否”**。

> [**十边形数**](https://www.geeksforgeeks.org/decagonal-numbers/) 是一个将三角形和正方形的概念扩展到十边形(10 边多边形)的图形数。**第 n 个**十边形数字计算 n 个嵌套十边形图案中的点数，所有十边形共享一个公共角，其中图案中的**和**十边形具有由相互间隔一个单位的 **i 个点**组成的边。前几个十边形数字是 **1，10，27，52，85，126，175，…**

**例:**

> **输入:** N = 10
> **输出:**是
> **说明:**
> 第二个十边形数为 10。
> **输入:** N = 30
> **输出:**否

**进场:**

1.  十边形数字的第**K**项给出为
    ![K^{th} Term = 4*K^{2} - 3*K     ](img/ec39d98ffdfa04cdbf093a514496f75b.png "Rendered by QuickLaTeX.com")

2.  因为我们必须检查给定的数字是否可以表示为**十边形数字**。可以勾选为:

> => ![N = 4*K^{2} - 3*K     ](img/217c2a7da7721d896da136da3202ebde.png "Rendered by QuickLaTeX.com")
> = > ![K = \frac{3 + \sqrt{16*N + 9}}{8}     ](img/8747ecee767ac9999f246c447e988636.png "Rendered by QuickLaTeX.com")

2.  如果使用上述公式计算的 **K** 的值是整数，那么 **N** 是十边形数。
3.  否则 **N** 不是十进制数。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if N is a
// Decagonal Number
bool isdecagonal(int N)
{
    float n
        = (3 + sqrt(16 * N + 9))
          / 8;

    // Condition to check if the
    // number is a decagonal number
    return (n - (int)n) == 0;
}

// Driver Code
int main()
{
    // Given Number
    int N = 10;

    // Function call
    if (isdecagonal(N)) {
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
import java.lang.Math;

class GFG{

// Function to check if N is a
// decagonal number
public static boolean isdecagonal(int N)
{
    double n = (3 + Math.sqrt(16 * N + 9)) / 8;

    // Condition to check if the
    // number is a decagonal number
    return (n - (int)n) == 0;
}

// Driver code   
public static void main(String[] args)
{

    // Given number
    int N = 10;

    // Function call
    if (isdecagonal(N))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by divyeshrabadiya07   
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to check if N is a
# decagonal number
def isdecagonal(N):

    n = (3 + math.sqrt(16 * N + 9)) / 8

    # Condition to check if the
    # number is a decagonal number
    return (n - int(n)) == 0

# Driver Code
if __name__=='__main__':

    # Given number
    N = 10

    # Function Call
    if isdecagonal(N):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if N
// is a decagonal Number
static bool isdecagonal(int N)
{
    double n = (3 + Math.Sqrt(16 * N + 9)) / 8;

    // Condition to check if the
    // number is a decagonal number
    return (n - (int)n) == 0;
}

// Driver Code
static public void Main ()
{

    // Given Number
    int N = 10;

    // Function call
    if (isdecagonal(N))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by ShubhamCoder
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to check if N is a
// Decagonal Number
function isdecagonal( N)
{
    let n
        = (3 + Math.sqrt(16 * N + 9))
          / 8;

    // Condition to check if the
    // number is a decagonal number
    return (n - parseInt(n)) == 0;
}

// Driver Code

    // Given Number
    let N = 10;

    // Function Call
    if (isdecagonal(N)) {
        document.write( "Yes");
    }
    else {
        document.write( "No");
    }

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*