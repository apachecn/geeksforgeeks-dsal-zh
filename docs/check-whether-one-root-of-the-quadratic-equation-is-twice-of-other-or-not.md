# 检查二次方程的一根是否是另一根的两倍

> 原文:[https://www . geesforgeks . org/check-二次方程的一次根是否为二次根/](https://www.geeksforgeeks.org/check-whether-one-root-of-the-quadratic-equation-is-twice-of-other-or-not/)

给定三个数字 **A，B，C** ，代表一个二次方程![Ax^{2} + Bx + C = 0   ](img/bb71b6a28492c45e6e31522c6932e889.png "Rendered by QuickLaTeX.com")的系数(常数)，任务是检查由这些常数代表的方程的一个根是否是另一个的两倍。
**示例:**

> **输入:** A = 1，B = -3，C = 2
> **输出:**是
> **说明:**
> 给定的二次方程是![x^{2} - 3x + 2 = 0   ](img/dae35231dd7a04db09b170b4bcf531f0.png "Rendered by QuickLaTeX.com")
> 它的根是(1，2)。![2 = 2 * 1   ](img/99b5dd8dfc9fec22c84506c7d890fa60.png "Rendered by QuickLaTeX.com")
> **输入:** A = 1，B = -5，C = 6
> **输出:** No
> **解释:**
> 给定的二次方程是![x^{2} - 5x + 6 = 0   ](img/c884a3770656dca3655c6cc361c4ca4d.png "Rendered by QuickLaTeX.com")
> 它的根是(2，3)。![3 \ne 2 * 2   ](img/86f2f92632fbab87a0e67e580b2db445.png "Rendered by QuickLaTeX.com")或![2 \ne 2 * 3   ](img/5aa2f1a0521f7cef6e8df8f118eead14.png "Rendered by QuickLaTeX.com")

**做法:**思路是用二次根的概念来解决问题。我们可以通过:
来表达检查一个根是否是另一个根的两倍所需的条件

1.  根之和= ![\alpha   ](img/5fe293dbd8ac4f63d9e1264e49a8ce59.png "Rendered by QuickLaTeX.com") + ![2*\alpha   ](img/92aa7dcebf7702b64ccfc02392dd791e.png "Rendered by QuickLaTeX.com") = 3 ![\alpha   ](img/5fe293dbd8ac4f63d9e1264e49a8ce59.png "Rendered by QuickLaTeX.com")。该值等于:

> ![\frac{-b}{a}   ](img/25f7034daf21f09b987e0228dfe677b2.png "Rendered by QuickLaTeX.com")

1.  同样，根的乘积= ![\alpha   ](img/5fe293dbd8ac4f63d9e1264e49a8ce59.png "Rendered by QuickLaTeX.com") * ![2*\alpha   ](img/92aa7dcebf7702b64ccfc02392dd791e.png "Rendered by QuickLaTeX.com") = 2 ![\alpha^2   ](img/07cbeb35b92065973c2dac6405139054.png "Rendered by QuickLaTeX.com")。该值等于:

> ![\frac{c}{a}   ](img/e3fe9b14043e56b7cf3bcc26cbd19b32.png "Rendered by QuickLaTeX.com")

1.  我们可以解上面两个方程![3 * \alpha = \frac{-b}{a}   ](img/09311765474891fc3cb52d59a1d5ab41.png "Rendered by QuickLaTeX.com")和![2 * \alpha^2 = \frac{c}{a}   ](img/ebb4005311b5c5472e2c51a39f7cdd65.png "Rendered by QuickLaTeX.com")得到条件:

> ![2b^2 = 9 * a * c   ](img/6889abcffb453c8d882be3c2cfd4422a.png "Rendered by QuickLaTeX.com")

1.  因此，为了使根的第一个假设成立，上述条件需要成立。因此，对于给定的系数，我们简单地检查上述条件是否成立。

以下是上述方法的实现:

## C++

```
// C++ program to check if one root
// of a Quadratic Equation is
// twice of other or not

#include <iostream>
using namespace std;

// Function to find the required answer
void checkSolution(int a, int b, int c)
{
    if (2 * b * b == 9 * a * c)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    int a = 1, b = 3, c = 2;

    checkSolution(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if one root
// of a quadratic equation is
// twice of other or not
class GFG{

// Function to find the required answer
static void checkSolution(int a, int b, int c)
{
    if (2 * b * b == 9 * a * c)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int a = 1, b = 3, c = 2;

    checkSolution(a, b, c);
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 program to check if one root
# of a Quadratic Equation is
# twice of other or not

# Function to find the required answer
def checkSolution(a, b, c):

    if (2 * b * b == 9 * a * c):
        print("Yes");
    else:
        print("No");

# Driver code
a = 1; b = 3; c = 2;
checkSolution(a, b, c);

# This code is contributed by Code_Mech
```

## C#

## java 描述语言

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*