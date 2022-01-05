# 根与给定方程的根互为倒数的二次方程

> 原文:[https://www . geeksforgeeks . org/二次方程-其根是给定方程的根的倒数/](https://www.geeksforgeeks.org/quadratic-equation-whose-roots-are-reciprocal-to-the-roots-of-given-equation/)

给定三个整数 **A、B** 和 **C** 表示一个二次方程 **Ax <sup>2</sup> + Bx + C = 0** 的系数，任务是找出根与给定方程的根互为倒数的二次方程。

**示例:**

> **输入:** A = 1，B = -5，C = 6
> **输出:** (6)x^2 +(-5)x + (1) = 0
> **解释:**
> 给定的二次方程 x<sup>2</sup>–5x+6 = 0。
> 上式的根是 2，3。
> 这些根的倒数是 1/2，1/3。
> 因此，有这些倒数根的二次方程为 6x<sup>2</sup>–5x+1 = 0。
> 
> **输入:** A = 1，B = -7，C = 12
> **输出:** (12)x^2 +(-7)x + (1) = 0

**做法:**思路是用二次根的概念来解决问题。按照以下步骤解决问题:

*   考虑方程 **Ax <sup>2</sup> + Bx + C = 0** 的根为 **p，q.**
*   上述方程的根的乘积由 **p * q = C / A.** 给出
*   上述方程的根之和由 **p + q = -B / A.** 给出
*   所以根的倒数是 **1/p，1/q**
*   这些倒数根的乘积是 **1/p * 1/q = A / C.**
*   这些倒数根之和为 **1/p + 1/q = -B / C.**
*   如果已知根的和与积，二次方程可以是**x<sup>2</sup>–(根的和)x +(根的积)= 0。**
*   求解上述方程时，二次方程变为 **Cx <sup>2</sup> + Bx + A = 0。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the quadratic
// equation having reciprocal roots
void findEquation(int A, int B, int C)
{
    // Print quadratic equation
    cout << "(" << C << ")"
         << "x^2 +(" << B << ")x + ("
         << A << ") = 0";
}

// Driver Code
int main()
{
    // Given coefficients
    int A = 1, B = -5, C = 6;

    // Function call to find the quadratic
    // equation having reciprocal roots
    findEquation(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the quadratic
// equation having reciprocal roots
static void findEquation(int A, int B, int C)
{

    // Print quadratic equation
    System.out.print("(" + C + ")" + 
                "x^2 +(" + B + ")x + (" +
                           A + ") = 0");
}

// Driver Code
public static void main(String args[])
{

    // Given coefficients
    int A = 1, B = -5, C = 6;

    // Function call to find the quadratic
    // equation having reciprocal roots
    findEquation(A, B, C);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the quadratic
# equation having reciprocal roots
def findEquation(A, B, C):

    # Print quadratic equation
    print("(" + str(C)  + ")" +
     "x^2 +(" + str(B) + ")x + (" +
                str(A) + ") = 0")

# Driver Code
if __name__ == "__main__":

    # Given coefficients
    A = 1
    B = -5
    C = 6

    # Function call to find the quadratic
    # equation having reciprocal roots
    findEquation(A, B, C)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the quadratic
// equation having reciprocal roots
static void findEquation(int A, int B, int C)
{
    // Print quadratic equation
    Console.Write("(" + C + ")" + 
             "x^2 +(" + B + ")x + (" +
                        A + ") = 0");
}

// Driver Code
public static void Main()
{

    // Given coefficients
    int A = 1, B = -5, C = 6;

    // Function call to find the quadratic
    // equation having reciprocal roots
    findEquation(A, B, C);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

        // Javascript program for the above approach

        // Function to find the quadratic
        // equation having reciprocal roots
        function findEquation(A, B, C)
        {
            // Print quadratic equation
            document.write("(" + C + ")" +
                "x^2 +(" + B +
                ")x + (" + A + ") = 0")

        }

        // Driver Code

        // Given coefficients
        let A = 1, B = -5, C = 6;

        // Function call to find the quadratic
        // equation having reciprocal roots
        findEquation(A, B, C);

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
(6)x^2 +(-5)x + (1) = 0
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)