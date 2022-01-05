# 复数的模数

> 原文:[https://www.geeksforgeeks.org/modulus-of-a-complex-number/](https://www.geeksforgeeks.org/modulus-of-a-complex-number/)

给定一个[复数](https://www.geeksforgeeks.org/complex-numbers-c-set-1/) **z** ，任务是确定这个复数的模。

**注:**给定复数 **z = a + ib** 模量用 **|z|** 表示，定义为![\left | z \right | = \sqrt{a^{2}+b^{2}}](img/299a38627401817f5b7403c8865e41a7.png "Rendered by QuickLaTeX.com")

**示例:**

> **输入:**z = 3+4i
> T3】输出:5
> | z | =(3<sup>2</sup>+4<sup>2</sup>)<sup>1/2</sup>=(9+16)<sup>1/2</sup>= 5
> 
> **输入:**z = 6–8i
> **输出:** 10
> **解释:**
> | z | =(6<sup>2</sup>+(-8)<sup>2</sup>)<sup>1/2</sup>=(36+64)<sup>1/2</sup>= 10

**方法:**对于给定的复数 **z = x + iy** :

1.  分别求实部和虚部，x 和 y。

    ```
    If z = x +iy

    Real part = x
    Imaginary part = y

    ```

2.  分别求 x 和 y 的平方。

    ```
    Square of Real part = x2
    Square of Imaginary part = y2

    ```

3.  求计算的平方和。

    ```
    Sum = Square of Real part 
          + Square of Imaginary part
        = x2 + y2

    ```

4.  求计算总和的平方根。这将是给定复数的模数

以下是上述方法的实现:

## C++

```
// C++ program to find the
// Modulus of a Complex Number

#include <bits/stdc++.h>
using namespace std;

// Function to find modulus
// of a complex number
void findModulo(string s)
{
    int l = s.length();
    int i, modulus = 0;

    // Storing the index of '+'
    if (s.find('+') < l) {
        i = s.find('+');
    }
    // Storing the index of '-'
    else {
        i = s.find('-');
    }

    // Finding the real part
    // of the complex number
    string real = s.substr(0, i);

    // Finding the imaginary part
    // of the complex number
    string imaginary = s.substr(i + 1, l - 1);

    int x = stoi(real);
    int y = stoi(imaginary);

    cout << sqrt(x * x + y * y) << "\n";
}

// Driver code
int main()
{
    string s = "3+4i";

    findModulo(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// Modulus of a Complex Number
import java.util.*;

class GFG{

// Function to find modulus
// of a complex number
static void findModulo(String s)
{
    int l = s.length();
    int i, modulus = 0;

    // Storing the index of '+'
    if (s.contains("+")) {
        i = s.indexOf("+");
    }

    // Storing the index of '-'
    else {
        i = s.indexOf("-");
    }

    // Finding the real part
    // of the complex number
    String real = s.substring(0, i);

    // Finding the imaginary part
    // of the complex number
    String imaginary = s.substring(i + 1, l-1);

    int x = Integer.parseInt(real);
    int y = Integer.parseInt(imaginary);

    System.out.print(Math.sqrt(x * x + y * y)+ "\n");
}

// Driver code
public static void main(String[] args)
{
    String s = "3+4i";

    findModulo(s);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to find the
# Modulus of a Complex Number
from math import sqrt

# Function to find modulus
# of a complex number
def findModulo(s):
    l = len(s)
    modulus = 0

    # Storing the index of '+'
    if ( '+' in s ):
        i = s.index('+')

    # Storing the index of '-'
    else:
        i = s.index('-')

    # Finding the real part
    # of the complex number
    real = s[0:i]

    # Finding the imaginary part
    # of the complex number
    imaginary = s[i + 1:l - 1]

    x = int(real)
    y = int(imaginary)

    print(int(sqrt(x * x + y * y)))

# Driver code
if __name__ == '__main__':
    s = "3+4i"

    findModulo(s)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to find the
// Modulus of a Complex Number
using System;

public class GFG{

// Function to find modulus
// of a complex number
static void findModulo(String s)
{
    int l = s.Length;
    int i;

    // Storing the index of '+'
    if (s.Contains("+")) {
        i = s.IndexOf("+");
    }

    // Storing the index of '-'
    else {
        i = s.IndexOf("-");
    }

    // Finding the real part
    // of the complex number
    String real = s.Substring(0, i);

    // Finding the imaginary part
    // of the complex number
    String imaginary = s.Substring(i + 1, l-i - 2);

    int x = Int32.Parse(real);
    int y = Int32.Parse(imaginary);

    Console.Write(Math.Sqrt(x * x + y * y)+ "\n");
}

// Driver code
public static void Main(String[] args)
{
    String s = "3+4i";

    findModulo(s);
}
}
// This code contributed by sapnasingh4991
```

**Output:**

```
5

```