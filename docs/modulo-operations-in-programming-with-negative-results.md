# 负结果编程中的模运算

> 原文:[https://www . geeksforgeeks . org/负结果编程中的模运算/](https://www.geeksforgeeks.org/modulo-operations-in-programming-with-negative-results/)

在编程中，在一个整数被另一个整数除之后，[模运算](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)给出除法的余数或**有符号余数**。它是编程时最常用的[运算符之一。本文讨论模运算何时以及为什么会产生负结果。](https://www.geeksforgeeks.org/operators-c-c/)

**示例:**

*   在 [C](https://www.geeksforgeeks.org/c-programming-language/) 中， **3 % 2** 返回 **1** 。但是 **-3 % 2** 是 **-1** ， **3 % -2** 给出 **1** 。
*   [Python 中](https://www.geeksforgeeks.org/python-programming-language/)， **-3 % 2** 为 **1** ， **3 % -2** 为 **-1** 。

因此，很明显 **-3 % 2** 的相同表达式在不同的编程语言中给出了不同的结果。这个结果更多是和数学有关，而不是和编程有关。这里提到的数学将有助于更容易地理解这些问题。
要理解为什么会出现这种情况，需要一点关于欧几里德除法的知识以及与[模运算](https://www.geeksforgeeks.org/modular-arithmetic/)相关的几点。

[**<u>欧几里德除法</u>**](https://www.geeksforgeeks.org/euclids-division-algorithm-real-numbers-class-10-maths/) **:** 在算术中，**欧几里德除法**或余数除法是将一个整数(被除数)除以另一个整数(除数)的过程，其方式是产生一个商和一个小于除数的余数。

给定两个整数 **a** 和 **b** (其中 **b ≠ 0** )，存在唯一的整数 **q** 和 **r** ，使得:

> **a = bq+r**(**0≤r<| b |**)
> 其中， **|b|** 表示 **b** 的绝对值。

在上式中，四个整数中的每一个都有自己的名字，即，

*   **一个**叫做**红利**。
*   **b** 叫做**除数**。
*   **q** 叫做**商**。
*   **r** 被称为**余数**。

**例如:**

*   如果 **a** = 9 且 **b** = 4，则 **q** = 2 且 **r** = 1，因为 9 = 4 × 2 + 1。
*   如果 **a** = -9 和 **b** = 4，那么 **q** = -3 和 **r** = 3，因为-9 = 4 × -3 + 3。
*   如果 **a** = 9 和 **b** = -4，那么 **q** = -2 和 **r** = 1，因为 9 = -4 × -2 + 1。
*   如果 **a** = -9 和 **b** = -4，那么 **q** = 3 和 **r** = 3，因为-9 = -4 × 3 + 3。

以上例子的解释:

*   第一个例子不言自明，因为 **9/4** 给出了**商** 2 和**余数** 1。
*   第二个例子 **(-9/4)** 给出了**商** **-3** 而不是 **-2** 。之所以会这样，是因为如果我们把 **-2** 作为**商**，那么 **-9 = 4 × -2 + (-1)** 。生成的 **-1** 的剩余部分不满足**欧几里德除法**的条件。这并没有让 **-9/4** = **-2** 出错，只是这不是我们在这种情况下需要的。

[**<u>模算术</u>**](https://www.geeksforgeeks.org/modular-arithmetic/) **:** 在数学中，**模算术**是一个整数的算术系统，其中数字在达到某个值时“环绕”，称为模。

**同余:**给定任意整数 **N** ，称为一个模，两个整数 **a** 和 **b** 被称为同余模 **N** ，如果它们在除以 **N** 时产生相同的余数，即，

> **a = pN + r** 和 **b = qN + r** ，其中 **0 ≤ r < |N|** 为*共同余数。*

同余模 **N** 表示为 **a ≡ b (mod N)**
，其中括号表示 **(mod N)** 适用于整个等式，而不仅仅是右侧(此处为 **b** )。

**示例:**

*   -5≥2(mod 7)
*   -14≥19(mod 11)

分析第一个例子。**-5 = 7×-1+2****2 = 7×0+2**。当被 **7** 除时， **-5** 和 **2** 留下相同的余数 **2** 。因此，它们彼此一致。
同理，**-14 = 11×-2+8****19 = 11×1+8**。 **-14** 和 **19** 除以 **11** 后，剩下相同的余数 **8** 。因此，它们彼此一致。

**<u>同余类</u> :** 假设**一个 mod N** 在除以 **N** 时剩下一个余数 **r** ，满足条件 **0 ≤ r < |N|** 。与 **a 模 N** 全等的所有整数的集合称为整数 **a 模 N** 的同余类。**例如:**

*   3 模 2 的同余类是{…，-5，-3，-1，1，3，5，7，… }。
*   7 mod 4 的同余类是{…，-9，-5，-1，3，7，11，… }。

从整数**的同余类中选择任意整数作为该类的代表。在数学中，属于该类的最小正残数、最小非负整数被选为代表。**例如:****

*   同余类 3 mod 2 的代表是 1。
*   同余类 7 mod 4 的代表是 3。

选择最小正残差是因为它是在**欧几里德除法**之后产生的余数。

**代表由编程语言选择:**

*   如果 **a** 和 **N** 都是正数，那么在所有的编程语言中， **a mod N** 就是欧几里德除法的余数。然而，当 **a** 或 **N** 为负或两者都为负时，观察到结果的差异。 **a mod N** 的答案则取决于编程语言所使用的 **a mod N** 的实现。所有编程语言产生的余数都遵循一定的标准，即 **|r| < |N|** 。
*   然而，如果余数非零，这仍然会留下符号模糊，那么余数有两种可能的选择，一种是负的(a mod N 同余类的最大负元素)和另一种是正的(a mod NT2 同余类的最小正元素)。其他元素不满足 **|r| < |N|** 的标准。
*   这就是为什么 **-3 mod 2** 在 **C** 和 **Python** 中执行时会有不同的结果。两者都产生了正确的结果。他们只是没有输出数学选择的代表**一个 mod N** 。
*   在 **C** 中， **-3 mod 2** 返回 **-1** ，是 **-3 mod 2** 的成员类。但是 **Python** 返回 **1** ，又是 **-3 mod 2** 的成员类。同样，两个答案都返回满足给定条件 **|r| < |N|** 。

**<u>%在编程语言中的实现</u> :** 许多编程语言，如 [**C**](https://www.geeksforgeeks.org/c-programming-language/) 、 [**C++**](https://www.geeksforgeeks.org/c-plus-plus/) 、 [**Java**](https://www.geeksforgeeks.org/java/) 、 [**JavaScript**](https://www.geeksforgeeks.org/javascript-tutorial/) 使用与下面给出的实现类似的实现。余数根据等式返回

> **r = a–N * trunc(a/N)**

以下是上述解释的实现:

## C++14

```
// C++14 program to illustrate modulo
// operations using the above equation
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return the remainder of a % n
int truncMod(int a, int n)
{

    // (a / n) implicitly gives
    // the truncated result
    int q = a / n;

    return a - n * q;
}

// Driver Code
int main()
{
    int a, b;

    // Modulo of two positive numbers
    a = 9;
    b = 4;
    cout << a << " % "
         << b << " = "
         << truncMod(a, b) << endl;

    // Modulo of a negative number
    // by a positive number
    a = -9;
    b = 4;
    cout << a << " % "
         << b << " = "
         << truncMod(a, b) << endl;

    // Modulo of a positive number
    // by a negative number
    a = 9;
    b = -4;
    cout << a << " % "
         << b << " = "
         << truncMod(a, b) << endl;

    // Modulo of two negative numbers
    a = -9;
    b = -4;
    cout << a << " % "
         << b << " = "
         << truncMod(a, b) << endl;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate modulo
// operations using the above equation
class GFG {

    // Function to calculate and
    // return the remainder of a % n
    static int truncMod(int a, int n)
    {
        // (a / n) implicitly gives
        // the truncated result
        int q = a / n;

        return a - n * q;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a, b;

        // Modulo of two positive numbers
        a = 9;
        b = 4;
        System.out.println(a + " % " + b + " = "
                           + truncMod(a, b));

        // Modulo of a negative number
        // by a positive number
        a = -9;
        b = 4;
        System.out.println(a + " % " + b + " = "
                           + truncMod(a, b));

        // Modulo of a positive number
        // by a negative number
        a = 9;
        b = -4;
        System.out.println(a + " % " + b + " = "
                           + truncMod(a, b));

        // Modulo of two negative numbers
        a = -9;
        b = -4;
        System.out.println(a + " % " + b + " = "
                           + truncMod(a, b));
    }
}
```

## 蟒蛇 3

```
# Python3 program to illustrate modulo
# operations using the above equation

# Function to calculate and
# return the remainder of a % n
def truncMod(a, n):

    # (a / n) implicitly gives
    # the truncated result
    q = a // n
    return a - n * q

# Driver Code
if __name__ == '__main__':

    # Modulo of two positive numbers
    a = 9
    b = 4
    print(a,"%",b,"=",truncMod(a, b))

    # Modulo of a negative number
    # by a positive number
    a = -9
    b = 4
    print(a,"%",b,"=",truncMod(a, b))

    # Modulo of a positive number
    # by a negative number
    a = 9
    b = -4
    print(a,"%",b,"=",truncMod(a, b))

    # Modulo of two negative numbers
    a = -9
    b = -4
    print(a,"%",b,"=",truncMod(a, b))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to calculate and
  // return the remainder of a % n
  static int truncMod(int a, int n)
  {

    // (a / n) implicitly gives
    // the truncated result
    int q = a / n;
    return a - n * q;
  }

  // Driver Code
  static public void Main()
  {

    int a, b;

    // Modulo of two positive numbers
    a = 9;
    b = 4;
    Console.WriteLine(a + " % " + b + " = "
                      + truncMod(a, b));

    // Modulo of a negative number
    // by a positive number
    a = -9;
    b = 4;
    Console.WriteLine(a + " % " + b + " = "
                      + truncMod(a, b));

    // Modulo of a positive number
    // by a negative number
    a = 9;
    b = -4;
    Console.WriteLine(a + " % " + b + " = "
                      + truncMod(a, b));

    // Modulo of two negative numbers
    a = -9;
    b = -4;
    Console.WriteLine(a + " % " + b + " = "
                      + truncMod(a, b));
  }
}

// This code is contributed by snjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program to illustrate modulo
// operations using the above equation

// Function to calculate and
    // return the remainder of a % n
function truncMod(a,n)
{
    // (a / n) implicitly gives
        // the truncated result
        let q = Math.round(a / n);

        return a - (n * q);
}

let a, b;
// Modulo of two positive numbers
a = 9;
b = 4;
document.write(a + " % " + b + " = "
                   + truncMod(a, b)+"<br>");

// Modulo of a negative number
// by a positive number
a = -9;
b = 4;
document.write(a + " % " + b + " = "
                   + truncMod(a, b)+"<br>");

// Modulo of a positive number
// by a negative number
a = 9;
b = -4;
document.write(a + " % " + b + " = "
                   + truncMod(a, b)+"<br>");

// Modulo of two negative numbers
a = -9;
b = -4;
document.write(a + " % " + b + " = "
                   + truncMod(a, b)+"<br>");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
9 % 4 = 1
-9 % 4 = -1
9 % -4 = 1
-9 % -4 = -1
```