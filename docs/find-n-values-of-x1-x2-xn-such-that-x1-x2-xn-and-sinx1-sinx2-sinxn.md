# 求 X1、X2、… Xn 的 N 值，使得 X1 < X2 < … < XN 和 sin(X1)<sin(X2)<…<sin(XN)

> 原文:[https://www . geesforgeks . org/find-n-values-of-x1-x2-xn-so-x1-x2-xn-and-sinx 1-sinx 2-sinx n/](https://www.geeksforgeeks.org/find-n-values-of-x1-x2-xn-such-that-x1-x2-xn-and-sinx1-sinx2-sinxn/)

给定一个数 **N** ，任务是求 X <sub>i</sub> 的 N 个整数值，使得**X<sub>1</sub><X<sub>2</sub><……<X<sub>N</sub>T11】和**sin(X<sub>1</sub>)<sin(X<sub>2</sub>)<……<sin(X <sub>**例:**</sub>**** 

> **输入:** N = 5
> **输出:**
> x1 = 0 sin(x1)= 0.000000
> x2 = 710 sin(x2)= 0.000060
> x3 = 1420 sin(x3)= 0.00011
> x4 = 0.0000

**方法:**思路是用 PI 的分数值(&PI)；即，**π= 355/113**，因为它给出了精确度为 0.000009%的π的最佳合理值。

```
As,
   PI = 355/113
=> 113*PI = 355
=> 2*(113*PI) = 710

As sin() function has a period of 2*PI,
Therefore sin(2*k*PI + Y) = sin(Y);
```

按照上面的等式得到数值**X<sub>1</sub><X<sub>2</sub><……<X<sub>N</sub>**和**sin(X<sub>1</sub>)<sin(X<sub>2</sub>)<……<sin(X<sub>N</sub>)**我们必须找到 sin(X)的值，增量为 710
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all such Xi s.t.
// all Xi and sin(Xi) are strictly
// increasing
void printSinX(int N)
{
    int Xi = 0;
    int num = 1;

    // Till N becomes zero
    while (N--) {

        cout << "X" << num << " = " << Xi;
        cout << " sin(X" << num << ") = "
             << fixed;

        // Find the value of sin() using
        // inbuilt function
        cout << setprecision(6)
             << sin(Xi) << endl;

        num += 1;

        // increment by 710
        Xi += 710;
    }
}

// Driver Code
int main()
{
    int N = 5;

    // Function Call
    printSinX(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print all such Xi s.t.
// all Xi and sin(Xi) are strictly
// increasing
static void printSinX(int N)
{
    int Xi = 0;
    int num = 1;

    // Till N becomes zero
    while (N-- > 0)
    {

        System.out.print("X" + num + " = " + Xi);
        System.out.print(" sin(X" + num + ") = ");

        // Find the value of sin() using
        // inbuilt function
        System.out.printf("%.6f", Math.sin(Xi));
        System.out.println();
        num += 1;

        // Increment by 710
        Xi += 710;
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;

    // Function Call
    printSinX(N);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to print all such Xi s.t.
# all Xi and sin(Xi) are strictly
# increasing
def printSinX(N):

    Xi = 0;
    num = 1;

    # Till N becomes zero
    while (N > 0):

        print("X", num, "=", Xi, end = " ");
        print("sin(X", num, ") =", end = " ");

        # Find the value of sin() using
        # inbuilt function
        print("{:.6f}".format(math.sin(Xi)), "\n");

        num += 1;

        # increment by 710
        Xi += 710;
        N = N - 1;

# Driver Code
N = 5;

# Function Call
printSinX(N)

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print all such Xi s.t.
// all Xi and sin(Xi) are strictly
// increasing
static void printSinX(int N)
{
    int Xi = 0;
    int num = 1;

    // Till N becomes zero
    while (N-- > 0)
    {
        Console.Write("X" + num + " = " + Xi);
        Console.Write(" sin(X" + num + ") = ");

        // Find the value of sin() using
        // inbuilt function
        Console.Write("{0:F6}", Math.Sin(Xi));
        Console.WriteLine();
        num += 1;

        // Increment by 710
        Xi += 710;
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;

    // Function Call
    printSinX(N);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print all such Xi s.t.
// all Xi and sin(Xi) are strictly
// increasing
function printSinX(N)
{
    let Xi = 0;
    let num = 1;

    // Till N becomes zero
    while (N-- > 0)
    {

        document.write("X" + num + " = " + Xi);
        document.write(" sin(X" + num + ") = ");

        // Find the value of sin() using
        // inbuilt function
        document.write(Math.sin(Xi).toFixed(6));
        document.write("<br/>");
        num += 1;

        // Increment by 710
        Xi += 710;
    }
}

// Driver Code

    let N = 5;

    // Function Call
    printSinX(N);

</script>
```

**Output:** 

```
X1 = 0 sin(X1) = 0.000000
X2 = 710 sin(X2) = 0.000060
X3 = 1420 sin(X3) = 0.000121
X4 = 2130 sin(X4) = 0.000181
X5 = 2840 sin(X5) = 0.000241
```

时间复杂度:0(N)

辅助空间:0(1)