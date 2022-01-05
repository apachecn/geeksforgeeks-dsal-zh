# 不使用 Shridharacharya 公式时 a + b + c = 0 的二次方程的根

> 原文:[https://www . geeksforgeeks . org/二次方程的根-当-a-b-c-0-不使用-shridharya-formula/](https://www.geeksforgeeks.org/roots-of-the-quadratic-equation-when-a-b-c-0-without-using-shridharacharya-formula/)

给定三个整数 **a** 、 **b** 和 **c** ，使得 **a + b + c = 0** 。任务是求一个二次方程的根 **ax <sup>2</sup> + bx + c = 0** 。
**示例:**

> **输入:** a = 1，b = 2，c = -3
> **输出:** 1，-3
> **输入:** a = -5，b = 3，c = 2
> **输出:** 1，-2.5

**逼近:**当 **a + b + c = 0** 时，则方程的根 **ax <sup>2</sup> + bx + c = 0** 始终为 **1** 和 **c / a** 。
例如

> 取 a = 3，b = 2，c = -5，这样 a + b + c = 0
> 现在，方程为 3x<sup>2</sup>+2x–5 = 0
> 求解 x，
> 3x<sup>2</sup>+5x–3x–5 = 0
> x *(3x+5)-1 *(3x+5)= 0
> (x–1)*(3x+5)= 0
> **x = 1，x = (-5 / 3) =**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the roots of the
// quadratic equation when a + b + c = 0
void printRoots(long a, long b, long c)
{
    cout << 1 << ", " << c / (a * 1.0);
}

// Driver code
int main()
{
    long a = 2;
    long b = 3;
    long c = -5;
    printRoots(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to print the roots of the
    // quadratic equation when a + b + c = 0
    static void printRoots(long a, long b, long c)
    {
        System.out.println(1 + ", " + c / (a * 1.0));
    }

    // Driver Code
    public static void main (String[] args)
    {
        long a = 2;
        long b = 3;
        long c = -5;
        printRoots(a, b, c);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the roots of the
# quadratic equation when a + b + c = 0
def printRoots(a, b, c):
    print(1, ",", c / (a * 1.0))

# Driver code
a = 2
b = 3
c = -5
printRoots(a, b, c)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the roots of the
// quadratic equation when a + b + c = 0
static void printRoots(long a, long b, long c)
{
    Console.WriteLine("1, " + c / (a * 1.0));
}

// Driver code
public static void Main()
{
    long a = 2;
    long b = 3;
    long c = -5;
    printRoots(a, b, c);
}
}

// This code is contributed by Nidhi
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the roots of the
// quadratic equation when a + b + c = 0
function printRoots($a, $b, $c)
{
    echo "1";
    echo ", ";
    echo $c / ($a * 1.0);
}

// Driver code
$a = 2;
$b = 3;
$c = -5;
printRoots($a, $b, $c);

// This code is contributed by Naman_Garg.
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to print the roots of the
// quadratic equation when a + b + c = 0
function printRoots(a, b, c)
{
    document.write(1 + ", " + c / (a * 1.0));
}

// Driver code
var a = 2;
var b = 3;
var c = -5;
printRoots(a, b, c);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1, -2.5
```

**时间复杂度:** O(1)