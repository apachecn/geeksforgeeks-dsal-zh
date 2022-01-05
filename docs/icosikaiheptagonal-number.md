# icosikaiheptangonal 编号

> 原文:[https://www.geeksforgeeks.org/icosikaiheptagonal-number/](https://www.geeksforgeeks.org/icosikaiheptagonal-number/)

给定一个数字 **N** ，任务是找到**N<sup>th</sup>T5【icosikaiheptangenal 号。** 

> icosikaiheptagonal 数是一类图形数。它有一个 27 边的多边形，叫做 icosikaiheptagon。第 N 个 icosikaiheptagonal 数字计数是 27 个点的数量，所有其他点被一个公共共享角包围并形成一个图案。前几个 icosikaiheptagonol 数字是 **1、27、78、154……**

**例:**

> **输入:** N = 2
> **输出:** 27
> **解释:**
> 第二个 icosikaiheptagonol 数为 27。
> **输入:** N = 3
> **输出:** 78

**方法:**第 N 个 icosikaiheptagonal 数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}   ](img/e1b7be7ec1f82453b47cd0c23edff33f.png "Rendered by QuickLaTeX.com")

*   因此 27 边多边形的第 n 项为

> ![Tn =\frac{((27-2)n^2 - (27-4)n)}{2} =\frac{(25n^2 - 23n)}{2}   ](img/0d96112ea3b79ace31a2f7881f1c439b.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program to find N-th
// icosikaiheptagonal number
#include <bits/stdc++.h>

using namespace std;
// Function to find the nth
// icosikaiheptagonal Number
int icosikaiheptagonalNum(int n)
{
    return (25 * n * n - 23 * n) / 2;
}

// Driver code
int main()
{
    int n = 3;

    cout << "3rd icosikaiheptagonal Number is "
         << icosikaiheptagonalNum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// icosikaiheptagonal number
class GFG{

// Function to find the nth
// icosikaiheptagonal number
static int icosikaiheptagonalNum(int n)
{
    return (25 * n * n - 23 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    System.out.print("3rd icosikaiheptagonal Number is " +
                                icosikaiheptagonalNum(n));
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program to find N-th
# icosikaiheptagonal number

# Function to find the nth
# icosikaiheptagonal Number
def icosikaiheptagonalNum(n):

    return (25 * n * n - 23 * n) // 2;

# Driver code
n = 3;
print("3rd icosikaiheptagonal Number is ",
                icosikaiheptagonalNum(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to find N-th
// icosikaiheptagonal number
using System;

class GFG{

// Function to find the nth
// icosikaiheptagonal number
static int icosikaiheptagonal(int n)
{
    return (25 * n * n - 23 * n) / 2;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.Write("3rd icosikaiheptagonal Number is " +
                                icosikaiheptagonal(n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// javascript program to find N-th
// icosikaiheptagonal number

// Function to find the nth
// icosikaiheptagonal Number
function icosikaiheptagonalNum( n)
{
    return (25 * n * n - 23 * n) / 2;
}

// Driver code
let n = 3;
    document.write("3rd icosikaiheptagonal Number is "+ icosikaiheptagonalNum(n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
3rd icosikaiheptagonal Number is 78
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**参考:**T2】http://www.2dcurves.com/line/linep.html