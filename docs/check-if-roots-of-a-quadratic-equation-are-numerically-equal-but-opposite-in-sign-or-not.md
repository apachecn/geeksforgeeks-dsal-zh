# 检查二次方程的根在数值上是否相等但符号相反

> 原文:[https://www . geesforgeks . org/check-如果一个二次方程的根在数字上相等但在符号上相反/](https://www.geeksforgeeks.org/check-if-roots-of-a-quadratic-equation-are-numerically-equal-but-opposite-in-sign-or-not/)

给定二次方程![ax^{2} + bx + c=0    ](img/aeec9d8f81e94d615eb4e6527fb9c6e9.png "Rendered by QuickLaTeX.com")的系数(常数)，即 **a、b 和 c**；任务是检查由这些常数表示的方程的根在数字上是否相等，但在符号上是否相反。
**示例:**

> **输入:** a = 2，b = 0，c = -1
> **输出:**是
> **解释:**
> 给定的二次方程为![2x^{2}-2=0    ](img/1184ab65138a20067bde138de37dbfca.png "Rendered by QuickLaTeX.com")
> 其根为(1，-1)，数值相等但符号相反
> **输入:** a = 1，b = -5，c = 6
> **输出:**否
> **解释:**T20

**方法:**
检查根在数字上是否相等但符号相反:

> 二次方程:![ax^{2} + bx + c = 0    ](img/e639e31cf9cd793c892b70c095243d01.png "Rendered by QuickLaTeX.com")
> 设根为![\alpha    ](img/d41e9caba5f4ccbd71e1d25d64639f14.png "Rendered by QuickLaTeX.com")![\beta    ](img/a855a5efa261b30a8d907042c50376f3.png "Rendered by QuickLaTeX.com")
> 根之和= ![\alpha + \beta    ](img/37f108ce606b4315c196fba2dbf4d213.png "Rendered by QuickLaTeX.com") = ![\frac{-b}{a}    ](img/da4f09424d0c0317af8d8c3ccd582032.png "Rendered by QuickLaTeX.com")
> 由于根只在符号上相反，故![\alpha = -\beta    ](img/40032c0ed293a7e011457419ba63d1ec.png "Rendered by QuickLaTeX.com")
> 故
> ![-\beta + \beta = \frac{-b}{a}    ](img/a722a0057c7e1ce51768f00273b759c2.png "Rendered by QuickLaTeX.com")
> ![0 = \frac{-b}{a}    ](img/ca691f396c15f25536b406450f2751b5.png "Rendered by QuickLaTeX.com")
> ![b = 0    ](img/61d4ad7f0fcdda1fd10c7d6621150977.png "Rendered by QuickLaTeX.com")，即 x 的系数为 0。

因此，我们只需要检查 b 是否为 0，因为根在数字上相等，但符号相反。
以下是上述方法的实现:

## C++

```
// C++ program to check if roots
// of a Quadratic Equation are
// numerically equal but opposite
// in sign or not

#include <iostream>
using namespace std;

// Function to find the required answer
void checkSolution(int a, int b, int c)
{
    if (b == 0)
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
// of a Quadratic Equation are
// numerically equal but opposite
// in sign or not
import java.util.*;
class GFG{

// Function to find the required answer
static void checkSolution(int a, int b, int c)
{
    if (b == 0)
        System.out.print("Yes");
    else
        System.out.print("No");
}

// Driver code
public static void main(String args[])
{
    int a = 2, b = 0, c = 2;

    checkSolution(a, b, c);
}
}

// This code is contributed by Akanksha_Rai
```

## 蟒蛇 3

```
# Python3 program to check if roots
# of a quadratic equation are
# numerically equal but opposite
# in sign or not

# Function to find the required answer
def checkSolution(a, b, c):

    if b == 0:
        print("Yes")
    else:
        print("No")

# Driver code
a = 2
b = 0
c = 2

checkSolution(a, b, c)

# This code is contributed by divyamohan123
```

## C#

```
// C# program to check if roots
// of a Quadratic Equation are
// numerically equal but opposite
// in sign or not
using System;
class GFG{

// Function to find the required answer
static void checkSolution(int a, int b, int c)
{
    if (b == 0)
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main()
{
    int a = 2, b = 0, c = 2;

    checkSolution(a, b, c);
}
}

// This code is contributed by Akanksha_Rai
```

## java 描述语言

```
<script>

// Javascript program to check if roots
// of a Quadratic Equation are
// numerically equal but opposite
// in sign or not

// Function to find the required answer
function checkSolution(a, b, c)
{
    if (b == 0)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
a = 2, b = 0, c = 2;
checkSolution(a, b, c);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(1)*

***辅助空间:** O(1)*