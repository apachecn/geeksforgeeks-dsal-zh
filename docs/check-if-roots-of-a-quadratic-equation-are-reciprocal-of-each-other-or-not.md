# 检查一个二次方程的根是否互为倒数

> 原文:[https://www . geeksforgeeks . org/check-如果一个二次方程的根是互不可逆的/](https://www.geeksforgeeks.org/check-if-roots-of-a-quadratic-equation-are-reciprocal-of-each-other-or-not/)

给定三个数字 **A，B，C** ，代表一个二次方程![Ax^{2} + Bx + C = 0    ](img/4c92dd3544152625fa4c57a540d2dfb0.png "Rendered by QuickLaTeX.com")的系数(常数)，任务是检查由这些常数代表的方程的根是否相互倒数。
**示例:**

> **输入:** A = 2，B = -5，C = 2
> **输出:**是
> **说明:**
> 给定的二次方程为![2x^{2} - 2 = 0    ](img/eb047e84090941afb59d3aacec3307a3.png "Rendered by QuickLaTeX.com")。
> 它的根是(1，1/1)根，它们是互易的。
> **输入:** A = 1，B = -5，C = 6
> **输出:**否
> **说明:**
> 给定的二次方程是![x^{2} - 5x + 6 = 0    ](img/24ee63de46726b9c7f67452819a7d056.png "Rendered by QuickLaTeX.com")。
> 它的根是(2，3)根，它们不是互易的。

**做法:**思路是用二次根的概念来解决问题。我们可以通过以下方式来表达检查一个根是否是另一个根的倒数所需的条件:

1.  让方程的根为![\alpha    ](img/d41e9caba5f4ccbd71e1d25d64639f14.png "Rendered by QuickLaTeX.com")和![\frac{1}{\alpha}    ](img/82fd8cbdcb226c7d8d3911b342e4777e.png "Rendered by QuickLaTeX.com")。
2.  上述方程的根的乘积由![\alpha    ](img/d41e9caba5f4ccbd71e1d25d64639f14.png "Rendered by QuickLaTeX.com") * ![\frac{1}{\alpha}    ](img/82fd8cbdcb226c7d8d3911b342e4777e.png "Rendered by QuickLaTeX.com")给出。
3.  已知根的乘积是 C/A，因此要求的条件是 **C = A** 。

下面是上述方法的实现:

## C++

```
// C++ program to check if roots
// of a Quadratic Equation are
// reciprocal of each other or not

#include <iostream>
using namespace std;

// Function to check if the roots
// of a quadratic equation are
// reciprocal of each other or not
void checkSolution(int a, int b, int c)
{
    if (a == c)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    int a = 2, b = 0, c = 2;

    checkSolution(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if roots
// of a quadratic equation are
// reciprocal of each other or not
class GFG{

// Function to check if the roots 
// of a quadratic equation are
// reciprocal of each other or not
static void checkSolution(int a, int b, int c)
{
    if (a == c)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
    int a = 2, b = 0, c = 2;

    checkSolution(a, b, c);
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program to check if roots
# of a Quadratic Equation are
# reciprocal of each other or not

# Function to check if the roots
# of a quadratic equation are
# reciprocal of each other or not
def checkSolution(a, b, c):

    if (a == c):
        print("Yes");
    else:
        print("No");

# Driver code
a = 2; b = 0; c = 2;
checkSolution(a, b, c);

# This code is contributed by Code_Mech
```

## C#

```
// C# program to check if roots
// of a quadratic equation are
// reciprocal of each other or not
using System;
class GFG{

// Function to check if the roots
// of a quadratic equation are
// reciprocal of each other or not
static void checkSolution(int a, int b, int c)
{
    if (a == c)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}

// Driver code
public static void Main()
{
    int a = 2, b = 0, c = 2;

    checkSolution(a, b, c);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to check if roots
    // of a Quadratic Equation are
    // reciprocal of each other or not

    // Function to check if the roots
    // of a quadratic equation are
    // reciprocal of each other or not
    function checkSolution(a, b, c)
    {
        if (a == c)
            document.write("Yes");
        else
            document.write("No");
    }

    let a = 2, b = 0, c = 2;

    checkSolution(a, b, c);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*