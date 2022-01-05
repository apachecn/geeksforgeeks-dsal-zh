# 根为给定方程根的 K 倍的二次方程

> 原文:[https://www . geeksforgeeks . org/二次方程-其根是给定方程的根的 k 倍/](https://www.geeksforgeeks.org/quadratic-equation-whose-roots-are-k-times-the-roots-of-given-equation/)

给定三个整数 **A** 、 **B** 和 **C** 表示一个[二次方程 **Ax <sup>2</sup> + Bx + C = 0**](https://www.geeksforgeeks.org/program-to-find-the-roots-of-quadratic-equation/) 和一个正整数 **K** 的系数，任务是求根为给定方程的 **K 倍**的二次方程的系数。

**示例:**

> **输入:** A = 1，B = 2，C = 1，K = 2
> **输出:** 1 4 4
> **解释:**
> 给定的二次方程 x <sup>2</sup> + 2x + 1 = 0。
> 上述方程的根为-1、-1。
> 这些根的两倍是-2、-2。
> 因此，带根(-2，-2)的二次方程为 x <sup>2</sup> + 4x + 4 = 0。
> 
> **输入:** A = 1，B = -7，C = 12，K = 2
> T3】输出: 1 -14 48

**方法:**给定的问题可以通过使用二次根的[概念来解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/quadratic-equation-whose-roots-are-reciprocal-to-the-roots-of-given-equation/)

*   让方程**Ax<sup>2</sup>+Bx+C = 0**T5】的根分别为 **P** 和 **Q** 。
*   然后，上述方程的根的乘积由 **P * Q = C / A** 给出，上述方程的根的和由 **P + Q = -B / A** 给出。
*   因此，所需方程的根的乘积等于:

> **(K * P)*(K * Q)= K<sup>2</sup>* P * Q =(K<sup>2</sup>* C)/A**

*   同样，所需方程的根之和为 **2 * K (-B / C)** 。
*   因此，所需的二次方程等于:

> **x<sup>2</sup>–(根的总和)x +(根的乘积)= 0**
> 
> **=>ax<sup>2</sup>+(kb)x+(k<sup>2</sup>c = 0**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the quadratic
// equation whose roots are K times
// the roots of the given equation
void findEquation(int A, int B, int C,
                  int K)
{
    // Print quadratic equation
    cout << A << " " << K * B
         << " " << K * K * C;
}

// Driver Code
int main()
{
    int A = 1, B = 2, C = 1, K = 2;

    findEquation(A, B, C, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the quadratic
// equation whose roots are K times
// the roots of the given equation
static void findEquation(int A, int B,
                         int C, int K)
{

    // Print quadratic equation
    System.out.print(A + " " + K * B +
                      " " + K * K * C);
}

// Driver Code
public static void main(String []args)
{
    int A = 1, B = 2, C = 1, K = 2;

    findEquation(A, B, C, K);
}
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the quadratic
# equation whose roots are K times
# the roots of the given equation
def findEquation(A, B, C, K):

    # Prquadratic equation
    print(A, K*B, K*K*C)

# Driver Code
if __name__ == '__main__':
    A, B, C, K = 1, 2, 1, 2

    findEquation(A, B, C, K)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the quadratic
// equation whose roots are K times
// the roots of the given equation
static void findEquation(int A, int B,
                         int C, int K)
{

    // Print quadratic equation
    Console.Write(A + " " + K * B +
                      " " + K * K * C);
}

// Driver Code
public static void Main()
{
    int A = 1, B = 2, C = 1, K = 2;

    findEquation(A, B, C, K);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the quadratic
// equation whose roots are K times
// the roots of the given equation
function findEquation(A, B, C, K)
{

    // Print quadratic equation
    document.write( A + " " + K * B
         + " " + K * K * C);
}

// Driver Code
var A = 1, B = 2, C = 1, K = 2;
findEquation(A, B, C, K);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1 4 4
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)