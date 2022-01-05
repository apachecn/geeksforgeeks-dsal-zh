# 七龙珠号码

> 原文:[https://www.geeksforgeeks.org/heptacontagon-number/](https://www.geeksforgeeks.org/heptacontagon-number/)

给定一个数字 **N** ，任务是找到**N<sup>th</sup>T5[七角数字](https://en.wikipedia.org/wiki/Heptacontagon)。** 

> 一个[七角数](https://en.wikipedia.org/wiki/Heptacontagon)是一类图形数。它有一个 70 边的多边形，叫做七边形。第 N 个七点计数是 70 个点，所有其他的点都围绕着一个共同的角，形成一个图案。前几个七连字符数字是 **1，70，207，412……**

**例:**

> **输入:** N = 2
> **输出:** 70
> **说明:**
> 第二个七连串数字是 70。
> **输入:** N = 3
> **输出:** 207

**方法:**第 N 个十七碳数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}   ](img/e1b7be7ec1f82453b47cd0c23edff33f.png "Rendered by QuickLaTeX.com")

*   因此 70 边多边形的第 n 项是

> ![Tn =\frac{((70-2)n^2 - (70-4)n)}{2} =\frac{(68n^2 - 66)}{2} ](img/f790f840525ebd3b62ab702989b37194.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Finding the nth heptacontagon number
int heptacontagonNum(int n)
{
    return (68 * n * n - 66 * n) / 2;
}

// Driver code
int main()
{
    int N = 3;

    cout << "3rd heptacontagon Number is = "
         << heptacontagonNum(N);

    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

// Finding the nth heptacontagon Number
int heptacontagonNum(int n)
{
    return (68 * n * n - 66 * n) / 2;
}

// Driver code
int main()
{
    int N = 3;
    printf("3rd heptacontagon Number is = %d",
           heptacontagonNum(N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Finding the nth heptacontagon number
static int heptacontagonNum(int n)
{
    return (68 * n * n - 66 * n) / 2;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    System.out.println("3rd heptacontagon Number is = " +
                                    heptacontagonNum(N));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for above approach

# Finding the nth heptacontagon Number
def heptacontagonNum(n):

    return (68 * n * n - 66 * n) // 2;

# Driver code
N = 3;
print("3rd heptacontagon Number is =",
                 heptacontagonNum(N));

# This code is contributed by Akanksha_Rai
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Finding the nth heptacontagon number
static int heptacontagonNum(int n)
{
    return (68 * n * n - 66 * n) / 2;
}

// Driver Code
public static void Main()
{
    int N = 3;
    Console.Write("3rd heptacontagon Number is = " +
                               heptacontagonNum(N));
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Finding the nth heptacontagon number
function heptacontagonNum(n)
{
    return (68 * n * n - 66 * n) / 2;
}

// Driver code

var N = 3;   
document.write("3rd heptacontagon Number is = " + heptacontagonNum(N));

</script>
```

**Output:** 

```
3rd heptacontagon Number is = 207
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**参考资料:**[https://en . Wikipedia . org/wiki/hetaconagon](https://en.wikipedia.org/wiki/Heptacontagon)