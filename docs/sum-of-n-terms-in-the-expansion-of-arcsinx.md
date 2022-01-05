# 反正弦(x)

展开式中 N 项之和

> 原文:[https://www . geeksforgeeks . org/n-terms-sum-in-expansion-of-arcsinx/](https://www.geeksforgeeks.org/sum-of-n-terms-in-the-expansion-of-arcsinx/)

给定两个整数 **N** 和 **X** ，任务是使用扩展到 **N** 项找到 [Arcsin(x)](https://en.wikipedia.org/wiki/Inverse_trigonometric_functions) 的值。
**举例:**

> **输入:** N = 4，X = 0.5
> **输出:** 0.5233863467
> 对
> x = 0.5 的反正弦(X)展开的前 4 项之和为 0.5233863467。
> **输入:** N = 8，X = -0.5
> **输出:** -0.5233948501

**逼近:**反正弦(x)的展开式由:
![arcsin(x) = x + (1/2).(x^3)/3 + ((1.3)/(2.4)).(x^5)/5 + .....  ](img/2be6a495400bb26833198fdffbcdd8cf.png "Rendered by QuickLaTeX.com")
**给出注:*****| x |<1***
上述展开式是用两个保持分子和分母的变量求解的。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the arcsin(x)
void find_Solution(double x, int n)
{
    double sum = x, e = 2, o = 1, p = 1;
    for (int i = 2; i <= n; i++) {

        // The power to which 'x' is raised
        p += 2;

        sum += (double)(o / e) * (double)(pow(x, p) / p);

        // Numerator value
        o = o * (o + 2);

        // Denominator value
        e = e * (e + 2);
    }
    cout << setprecision(10) << sum;
}

// Driver code
int main()
{
    double x = -0.5;

    if (abs(x) >= 1) {
        cout << "Invalid Input\n";
        return 0;
    }

    int n = 8;
    find_Solution(x, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.io.*;

class GFG
{

// Function to find the arcsin(x)
static void find_Solution(double x, int n)
{
    double sum = x, e = 2, o = 1, p = 1;
    for (int i = 2; i <= n; i++)
    {

        // The power to which 'x' is raised
        p += 2;

        sum += (double)(o / e) *
               (double)(Math.pow(x, p) / p);

        // Numerator value
        o = o * (o + 2);

        // Denominator value
        e = e * (e + 2);
    }
    System.out.println (sum);
}

// Driver code
public static void main (String[] args)
{
    double x = -0.5;

    if (Math.abs(x) >= 1)
    {
        System.out.println ("Invalid Input");
    }

    int n = 8;
    find_Solution(x, n);
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the arcsin(x)
def find_Solution(x, n):
    Sum = x
    e = 2
    o = 1
    p = 1
    for i in range(2, n + 1):

        # The power to which 'x' is raised
        p += 2

        Sum += (o / e) * (pow(x, p) / p)

        # Numerator value
        o = o * (o + 2)

        # Denominator value
        e = e * (e + 2)
    print(round(Sum, 10))

# Driver code
x = -0.5

if (abs(x) >= 1):
    print("Invalid Input\n")

n = 8
find_Solution(x, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to find the arcsin(x)
static void find_Solution(double x, int n)
{
    double sum = x, e = 2, o = 1, p = 1;
    for (int i = 2; i <= n; i++)
    {

        // The power to which 'x' is raised
        p += 2;

        sum += (double)(o / e) *
               (double)(Math.Pow(x, p) / p);

        // Numerator value
        o = o * (o + 2);

        // Denominator value
        e = e * (e + 2);
    }
    Console.WriteLine(sum);
}

// Driver code
public static void Main (String[] args)
{
    double x = -0.5;

    if (Math.Abs(x) >= 1)
    {
        Console.WriteLine("Invalid Input");
    }

    int n = 8;
    find_Solution(x, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find the arcsin(x)
function find_Solution(x, n)
{
    let sum = x, e = 2, o = 1, p = 1;
    for (let i = 2; i <= n; i++) {

        // The power to which 'x' is raised
        p += 2;

        sum += (o / e) * (Math.pow(x, p) / p);

        // Numerator value
        o = o * (o + 2);

        // Denominator value
        e = e * (e + 2);
    }
    document.write(sum.toFixed(10));
}

// Driver code

    let x = -0.5;

    if (Math.abs(x) >= 1) {
        document.write("Invalid Input<br>");
    }

    let n = 8;
    find_Solution(x, n);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
-0.5233948501
```