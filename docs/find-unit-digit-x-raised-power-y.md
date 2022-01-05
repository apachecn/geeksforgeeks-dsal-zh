# 求 x 升 y 次方的单位数字

> 原文:[https://www . geesforgeks . org/find-unit-digit-x-raised-power-y/](https://www.geeksforgeeks.org/find-unit-digit-x-raised-power-y/)

给定两个数字 x 和 y，求 x <sup>y</sup> 的单位数字。

**示例:**

```
Input  : x = 2, y = 1
Output : 2
Explanation
2^1 = 2 so units digit is 2.

Input : x = 4, y = 2
Output : 6
Explanation
4^2 = 16 so units digit is 6.
```

**方法 1(简单)**计算 x <sup>y</sup> 的值，并找到其最后一位数字。此方法会导致 x 和 y 值稍大的溢出。
**方法 2(有效)**
1)找到 x 的最后一位。
2)在模 10 下计算 x^y 并返回其值。

## C++

```
// Efficient C++ program to
// find unit digit of x^y.
#include <bits/stdc++.h>
using namespace std;

// Returns unit digit of x
// raised to power y
int unitDigitXRaisedY(int x, int y)
{
    // Initialize result as 1 to
    // handle case when y is 0.
    int res = 1;

    // One by one multiply with x
    // mod 10 to avoid overflow.
    for (int i = 0; i < y; i++)
        res = (res * x) % 10;

    return res;
}

// Driver program
int main()
{ 
   cout << unitDigitXRaisedY(4, 2);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find
// unit digit of x^y.
import java.io.*;

class GFG {
    // Returns unit digit of x raised to power y
    static int unitDigitXRaisedY(int x, int y)
    {
        // Initialize result as 1 to
        // handle case when y is 0.
        int res = 1;

        // One by one multiply with x
        // mod 10 to avoid overflow.
        for (int i = 0; i < y; i++)
            res = (res * x) % 10;

        return res;
    }

    // Driver program
    public static void main(String args[])throws IOException
    {
    System.out.println(unitDigitXRaisedY(4, 2));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 code to find
# unit digit of x^y.

# Returns unit digit of
# x raised to power y
def unitDigitXRaisedY( x , y ):

    # Initialize result as 1 to
    # handle case when y is 0.
    res = 1

    # One by one multiply with x
    # mod 10 to avoid overflow.
    for i in range(y):
        res = (res * x) % 10

    return res

# Driver program
print( unitDigitXRaisedY(4, 2))

# This code is contributed by Abhishek Sharma44.
```

## C#

```
// Efficient Java program to find
// unit digit of x^y.
using System;

class GFG
{
    // Returns unit digit of x raised to power y
    static int unitDigitXRaisedY(int x, int y)
    {
        // Initialize result as 1 to
        // handle case when y is 0.
        int res = 1;

        // One by one multiply with x
        // mod 10 to avoid overflow.
        for (int i = 0; i < y; i++)
            res = (res * x) % 10;

        return res;
    }

    // Driver program
    public static void Main()
    {
    Console.WriteLine(unitDigitXRaisedY(4, 2));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to
// find unit digit of x^y.

// Returns unit digit of x
// raised to power y
function unitDigitXRaisedY($x, $y)
{
    // Initialize result as 1 to
    // handle case when y is 0.
    $res = 1;

    // One by one multiply with x
    // mod 10 to avoid overflow.
    for ($i = 0; $i < $y; $i++)
        $res = ($res * $x) % 10;

    return $res;
}

// Driver Code
echo(unitDigitXRaisedY(4, 2));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to
// find unit digit of x^y.

// Returns unit digit of x
// raised to power y
function unitDigitXRaisedY(x, y)
{

    // Initialize result as 1 to
    // handle case when y is 0.
    let res = 1;

    // One by one multiply with x
    // mod 10 to avoid overflow.
    for(let i = 0; i < y; i++)
        res = (res * x) % 10;

    return res;
}

// Driver Code
document.write(unitDigitXRaisedY(4, 2));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
6
```

进一步优化:我们可以在 Log y 中计算[模幂。](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)

**方法 3(直接基于最后一位数字的循环性质)**
该方法取决于 x 最后一位数字的循环性，即

```
x   |  power 2  |  power 3  |   power 4  | Cyclicity  
0   | .................................. |  .... repeat with 0
1   | .................................. |  .... repeat with 1
2   |     4     |     8     |      6     | .... repeat with 2
3   |     9     |     7     |      1     | .... repeat with 3
4   |     6     |....................... |  .... repeat with 4
5   | .................................. |  .... repeat with 5
6   | .................................. |  .... repeat with 6
7   |     9     |     3     |      1     | .... repeat with 7
8   |     4     |     2     |      6     | .... repeat with 8
9   |     1     | ...................... |  .... repeat with 9 
```

所以这里我们直接用 4 来模幂 y，因为这是所有数字重复开始后的最后一次幂
之后，我们简单地用数字 x 的最后一位幂，然后我们得到产生的数字的单位位。

## C++

```
// C++ code to find the unit digit of x
// raised to power y.
#include<iostream>
#include<math.h>
using namespace std;

// find unit digit
int unitnumber(int x, int y)
{
    // Get last digit of x
    x = x % 10;

    // Last cyclic modular value
    if(y!=0)
        y = y % 4 + 4;

    // here we simply return the
    // unit digit or the power
    // of a number
    return (((int)(pow(x, y))) % 10);
}

int main()
{
    int x = 133, y = 5;

    // get unit digit number here we pass
    // the unit  digit of x and the last
    // cyclicity number that is y%4
    cout << unitnumber(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the unit
// digit of x  raised to power y.
import java.io.*;
import java.util.*;

class GFG {

    // find unit digit
    static int unitnumber(int x, int y)
    {
        // Get last digit of x
        x = x % 10;

        // Last cyclic modular value
        if(y!=0)
             y = y % 4 + 4;

        // here we simply return the
        // unit digit or the power
        // of a number
        return (((int)(Math.pow(x, y))) % 10);
    }

    public static void main (String[] args)
    {
        int x = 133, y = 5;

        // get unit digit number here we pass
        // the unit digit of x and the last
        // cyclicity number that is y%4
        System.out.println(unitnumber(x, y));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 code to find the unit  
# digit of x raised to power y.
import math

# Find unit digit
def unitnumber(x, y):

    # Get last digit of x
    x = x % 10

    # Last cyclic modular value
    if y!=0:
         y = y % 4 + 4

    # Here we simply return 
    # the unit digit or the 
    # power of a number
    return (((int)(math.pow(x, y))) % 10)

# Driver code
x = 133; y = 5

# Get unit digit number here we pass
# the unit digit of x and the last
# cyclicity number that is y%4
print(unitnumber(x, y))

# This code is contributed by Gitanjali.
```

## C#

```
// C# code to find the unit
// digit of x raised to power y.
using System;

class GFG {

    // find unit digit
    static int unitnumber(int x, int y)
    {
        // Get last digit of x
        x = x % 10;

        // Last cyclic modular value
        if(y!=0)
             y = y % 4 + 4;

        // here we simply return the
        // unit digit or the power
        // of a number
        return (((int)(Math.Pow(x, y))) % 10);
    }

    // Driver code
    public static void Main ()
    {
        int x = 133, y = 5;

        // get unit digit number here we pass
        // the unit digit of x and the last
        // cyclicity number that is y%4
        Console.WriteLine(unitnumber(x, y));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the unit
// digit of x raised to power y.

// find unit digit
function unitnumber($x, $y)
{
    // Get last digit of x
    $x = $x % 10;

    // Last cyclic modular value
    if($y!=0)
        $y = $y % 4 + 4;

    // here we simply return the
    // unit digit or the power
    // of a number
    return (((int)(pow($x, $y))) % 10);
}

// Driver code
$x = 133; $y = 5;

// get unit digit number here we pass
// the unit digit of x and the last
// cyclicity number that is y%4
echo(unitnumber($x, $y));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript code to find the unit
// digit of x raised to power y.

// find unit digit
function unitnumber(x, y)
{

    // Get last digit of x
    x = x % 10;

    // Last cyclic modular value
    if (y != 0)
        y = y % 4 + 4;

    // here we simply return the
    // unit digit or the power
    // of a number
    return ((parseInt(Math.pow(x, y))) % 10);
}

// Driver code
let x = 133;
let y = 5;

// get unit digit number here we pass
// the unit digit of x and the last
// cyclicity number that is y%4
document.write(unitnumber(x, y));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
3
```

感谢 [**DevanshuAgarwal**](https://auth.geeksforgeeks.org/profile.php?user=DevanshuAgarwal) 提出上述解决方案。
**如何处理大数？**
[a^b 最后一位数字的高效方法为大数](https://www.geeksforgeeks.org/find-last-digit-of-ab-for-large-numbers/)