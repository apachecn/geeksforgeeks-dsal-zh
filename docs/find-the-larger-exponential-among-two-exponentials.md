# 求两个指数中较大的指数

> 原文:[https://www . geeksforgeeks . org/find-二指数中较大的指数/](https://www.geeksforgeeks.org/find-the-larger-exponential-among-two-exponentials/)

给定四个整数 **A** 、 **B** 、 **C** 和 **D** 。任务是找出 **A <sup>B</sup>** 和 **C <sup>D</sup>** 哪个更大。

**示例:**

> **输入:** A = 2，B = 5，C = 4，D = 2
> **输出:**2^5
> 2<sup>5</sup>= 32
> 4<sup>2</sup>= 16
> 
> **输入:** A = 8，B = 29，C = 60，d = 59
> T3】输出: 60^59

**天真法:**计算**A<sup>B</sup>T5**C<sup>D</sup>T9】的值，然后进行比较。当数值较大时，如 **562145 <sup>321457</sup>** ，该方法将失败。****

**高效途径:**使用 log，我们可以将术语写成 **log(A <sup>B</sup> )** 和 **log(C <sup>D</sup> )** ，也可以写成**B * log(A)****D * log(C)**。这些值比原始值更容易计算和比较。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include<bits/stdc++.h>
using namespace std;

// Function to find whether a^b is greater or c^d
void compareValues(int a, int b, int c, int d)
{

    // Find b * log(a)
    double log1 = log10(a);
    double num1 = log1 * b;

    // Find d * log(c)
    double log2 = log10(c);
    double num2 = log2 * d;

    // Compare both values
    if (num1 > num2)
        cout << a  << "^"  <<  b;
    else
        cout << c << "^" << d;
}

// Driver code
int main ()
{
    int a = 8, b = 29, c = 60, d = 59;
    compareValues(a, b, c, d);
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to find whether a^b is greater or c^d
    static void compareValues(int a, int b, int c, int d)
    {

        // Find b * log(a)
        double log1 = Math.log10(a);
        double num1 = log1 * b;

        // Find d * log(c)
        double log2 = Math.log10(c);
        double num2 = log2 * d;

        // Compare both values
        if (num1 > num2)
            System.out.println(a + "^" + b);
        else
            System.out.println(c + "^" + d);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 8, b = 29, c = 60, d = 59;
        compareValues(a, b, c, d);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to find whether
# a^b is greater or c^d
def compareValues(a, b, c, d):
# Find b * log(a)
    log1 = math.log10(a)
    num1 = log1 * b

    # Find d * log(c)
    log2 = math.log10(c)
    num2 = log2 * d

    # Compare both values
    if num1 > num2 :
        print(a, '^', b)
    else :
        print(c, '^', d)

# Driver code
a = 8
b = 29
c = 60
d = 59

# Function call
compareValues(a, b, c, d)

# This code is contributed by nidhiva
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find whether
    // a^b is greater or c^d
    static void compareValues(int a, int b,
                              int c, int d)
    {

        // Find b * log(a)
        double log1 = Math.Log10(a);
        double num1 = log1 * b;

        // Find d * log(c)
        double log2 = Math.Log10(c);
        double num2 = log2 * d;

        // Compare both values
        if (num1 > num2)
            Console.WriteLine(a + "^" + b);
        else
            Console.WriteLine(c + "^" + d);
    }

    // Driver code
    public static void Main ()
    {
        int a = 8, b = 29, c = 60, d = 59;
        compareValues(a, b, c, d);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find whether a^b is greater or c^d
function compareValues(a, b, c, d)
{

    // Find b * log(a)
    let log1 = Math.log(a) / Math.log(10);
    let num1 = log1 * b;

    // Find d * log(c)
    let log2 = Math.log(c) / Math.log(10);
    let num2 = log2 * d;

    // Compare both values
    if (num1 > num2)
        document.write(a + "^" + b);
    else
        document.write(c + "^" + d);
}

// Driver code
let a = 8, b = 29, c = 60, d = 59;
compareValues(a, b, c, d);

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
60^59
```