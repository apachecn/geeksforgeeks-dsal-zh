# 二十边形数

> 原文:[https://www.geeksforgeeks.org/icosihexagonal-number/](https://www.geeksforgeeks.org/icosihexagonal-number/)

给定一个编号 **N** ，任务是找到**N<sup>th</sup>T5[Icosihexagon 编号](https://en.wikipedia.org/wiki/Icosihexagon)。** 

> 一个 [Icosihexagon 数](https://en.wikipedia.org/wiki/Icosihexagon)是一类图形数。它有一个 26 边的多边形，叫做 Icosihexagon。第 N 个 Icosihexagonal 数字计数是 26 个点的数量，所有其他点被一个公共共享角包围并形成一个图案。前几个 Icosihexagonol 数字是 **1、26、75、148……**

**例:**

> **输入:** N = 2
> **输出:** 26
> **解释:**
> 第二个 Icosihexagonol 数是 26。
> **输入:** N = 3
> **输出:** 75

**方法:**第 N 个正交数由公式给出:

*   s 边多边形的第 n 项= ![\frac{((s-2)n^2 - (s-4)n)}{2}     ](img/0abf7eeeb36d988fc99c1364dd143b8b.png "Rendered by QuickLaTeX.com")

*   因此 26 边多边形的第 n 项为

> ![Tn =\frac{((26-2)n^2 - (26-4)n)}{2} =\frac{(24n^2 - 22n)}{2} ](img/4f0a18d595d1f7b4912311ddaef9f316.png "Rendered by QuickLaTeX.com")

以下是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Finding the nth Icosihexagonal Number
int IcosihexagonalNum(int n)
{
    return (24 * n * n - 22 * n) / 2;
}

// Driver Code
int main()
{
    int n = 3;
    cout << "3rd Icosihexagonal Number is = "
         << IcosihexagonalNum(n);

    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

// Finding the nth Icosihexagonal Number
int IcosihexagonalNum(int n)
{
    return (24 * n * n - 22 * n) / 2;
}

// Driver program to test above function
int main()
{
    int n = 3;
    printf("3rd Icosihexagonal Number is = %d",
           IcosihexagonalNum(n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Finding the nth icosihexagonal number
public static int IcosihexagonalNum(int n)
{
    return (24 * n * n - 22 * n) / 2;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println("3rd Icosihexagonal Number is = " +
                                    IcosihexagonalNum(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for above approach

# Finding the nth Icosihexagonal Number
def IcosihexagonalNum(n):

    return (24 * n * n - 22 * n) // 2

# Driver Code
n = 3
print("3rd Icosihexagonal Number is = ",
                   IcosihexagonalNum(n))

# This code is contributed by divyamohan123
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Finding the nth icosihexagonal number
public static int IcosihexagonalNum(int n)
{
    return (24 * n * n - 22 * n) / 2;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine("3rd Icosihexagonal Number is = " +
                                   IcosihexagonalNum(n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for above approach

// Finding the nth Icosihexagonal Number
function IcosihexagonalNum( n)
{
    return (24 * n * n - 22 * n) / 2;
}

// Driver code
let n = 3;
document.write("3rd Icosihexagonal Number is " + IcosihexagonalNum(n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
3rd Icosihexagonal Number is = 75
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*

**参考资料:**[https://en . Wikipedia . org/wiki/icsihasexabgon](https://en.wikipedia.org/wiki/Icosihexagon)