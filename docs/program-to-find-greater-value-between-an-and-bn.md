# 在 a^n 和 b^n 之间寻找更大价值的程序

> 原文:[https://www . geesforgeks . org/program-to-find-更大的价值-介于 an 和 bn 之间/](https://www.geeksforgeeks.org/program-to-find-greater-value-between-an-and-bn/)

给定三个整数 a、b 和 n，任务是找出 a <sup>n</sup> 和 b <sup>n</sup> 之间的较大值。
**例:**

> **输入:** a = 3，b = 4，n = 5
> **输出:** b^n 大于 a^n
> 值 a <sup>n</sup> 为 243，b <sup>n</sup> 为 1024。
> 所以，b <sup>n</sup> 大于 a <sup>n</sup> 。
> **输入:** a = -3，b = 2，n = 4
> **输出:** a^n 大于 b^n
> a<sup>n</sup>值为 243，b <sup>n</sup> 值为 16。
> 所以，a <sup>n</sup> 大于 b <sup>n</sup> 。

**基本方法:**对于 a、b 和 n 的每个值，计算 a <sup>n</sup> 和 b <sup>n</sup> 的值。然后比较获得的结果，并根据输出显示。
当 a、b、n 的值较大时，就会出现这种方法的问题，对于 a、n 的值较大时，计算 a <sup>n</sup> 会超出整数的限制，从而导致整数溢出。
**更好的方法**是检查 n 的值

*   如果 n 是偶数，那么计算 a 和 b 的绝对值。
*   如果 n 是奇数，那么取给定值。
*   现在检查 a 是否等于 b。如果是，打印 0。
*   如果 a 大于 b，打印 1。
*   否则，打印 2。

## C++

```
// C++ code for finding greater
// between the a^n and b^n
#include <bits/stdc++.h>
using namespace std;

// Function to find the greater value
void findGreater(int a, int b, int n)
{
    // If n is even
    if (!(n & 1)) {

        a = abs(a);
        b = abs(b);
    }
    if (a == b)
        cout << "a^n is equal to b^n";

    else if (a > b)
        cout << "a^n is greater than b^n";

    else
        cout << "b^n is greater than a^n";
}

// Driver code
int main()
{
    int a = 12, b = 24, n = 5;
    findGreater(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code for finding greater
// between the a^n and b^n
import java.io.*;

class GFG
{
    // Function to find
    // the greater value
    static void findGreater(int a,
                            int b, int n)
{
    // If n is even
    if (!((n & 1) > 0))
    {

        a = Math.abs(a);
        b = Math.abs(b);
    }
    if (a == b)
        System.out.println("a^n is " +
                           "equal to b^n");

    else if (a > b)
        System.out.println("a^n is greater " +
                                  "than b^n");

    else
        System.out.println("b^n is greater " +
                                  "than a^n");
}

// Driver code
public static void main (String[] args)
{
int a = 12, b = 24, n = 5;
findGreater(a, b, n);
}
}

// This code is contributed
// by shiv_bhakt.
```

## 蟒蛇 3

```
# Python3 code for finding greater
# between the a^n and b^n
import math

# Function to find the greater value
def findGreater(a, b, n):

    # If n is even
    if ((n & 1) > 0):

        a = abs(a);
        b = abs(b);
    if (a == b):
        print("a^n is equal to b^n");

    elif (a > b):
        print("a^n is greater than b^n");

    else:
        print("b^n is greater than a^n");

# Driver code
a = 12;
b = 24;
n = 5;
findGreater(a, b, n);

# This code is contributed by mits
```

## C#

```
// C# code for finding greater
// between the a^n and b^n
using System;

class GFG
{
    // Function to find
    // the greater value
    static void findGreater(int a,
                            int b,
                            int n)
    {
    // If n is even
    if (!((n & 1) > 0))
    {

        a = Math.Abs(a);
        b = Math.Abs(b);
    }

    if (a == b)
        Console.WriteLine("a^n is " +
                          "equal to b^n");

    else if (a > b)
        Console.WriteLine("a^n is greater " +
                                 "than b^n");

    else
        Console.WriteLine("b^n is greater " +
                                 "than a^n");
}

// Driver code
public static void Main()
{
    int a = 12, b = 24, n = 5;
    findGreater(a, b, n);
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for finding greater
// between the a^n and b^n

// Function to find
// the greater value
function findGreater($a, $b, $n)
{
    // If n is even
    if (!($n & 1))
    {

        $a = abs($a);
        $b = abs($b);
    }
    if ($a == $b)
        echo "a^n is equal to b^n";

    else if ($a > $b)
        echo "a^n is greater than b^n";

    else
        echo "b^n is greater than a^n";
}

// Driver code
$a = 12; $b = 24; $n = 5;
findGreater($a, $b, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript code for finding greater
// between the a^n and b^n

    // Function to find
    // the greater value
    function findGreater(a , b , n)
    {
        // If n is even
        if (!((n & 1) > 0)) {

            a = Math.abs(a);
            b = Math.abs(b);
        }
        if (a == b)
            document.write("a^n is " + "equal to b^n");

        else if (a > b)
            document.write("a^n is greater " + "than b^n");

        else
            document.write("b^n is greater " + "than a^n");
    }

    // Driver code

        var a = 12, b = 24, n = 5;
        findGreater(a, b, n);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
b^n is greater than a^n
```