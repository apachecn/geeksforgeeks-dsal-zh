# 居中十边形数字

> 原文:[https://www.geeksforgeeks.org/centered-decagonal-number/](https://www.geeksforgeeks.org/centered-decagonal-number/)

给定一个数 n，求第 n 个居中的十边形数。
一个**居中十边形数字**是一个居中的比喻数字，代表一个十边形，中间有一个点，其他点都以连续的十边形形式围绕着它。来源[【维基】](https://en.wikipedia.org/wiki/Centered_decagonal_number)。

![Center Decagonal number](img/d619c70b15d39ca16a878aad8503f0b9.png)

前几个居中的十边形数字是:
1，11，31，61，101，151，211，281，361，451，551，661…………
**示例:**

```
Input :  3
Output : 31

Input : 6
Output : 151
```

在数学中，第 n 个**项的以十边形为中心的数由
给出**

下面是上述思想的基本实现。

## C++

```
// Program to find nth
// centered decagonal
// number
#include <bits/stdc++.h>
using namespace std;

// Centered decagonal
// number function

int centereddecagonalnum(int n)
{
    // Formula to calculate nth
    // centered decagonal number &
    // return it into main function.
    return (5 * n * n + 5 * n + 1);
}

// Driver Code
int main()
{
    int n = 5;
    cout << n << "th centered decagonal"
                          << "number: ";
    cout << centereddecagonalnum(n);
    cout << endl;
    n = 9;
    cout << n << "th centered decagonal"
                          << "number: ";
    cout << centereddecagonalnum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find nth
// centered decagonal number
import java.io.*;

class GFG
{

    // Centered decagonal
    // number function
    static int centereddecagonalnum(int n)
    {

    // Formula to calculate nth
    // centered decagonal number &
    // return it into main function.
    return (5 * n * n + 5 * n + 1);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 5;
        System.out.print(n + "th centered " +
                       "decagonal number: ");
        System.out.println(centereddecagonalnum(n));

        n = 9;
        System.out.print(n + "th centered " +
                       "decagonal number: ");
        System.out.println(centereddecagonalnum(n));
    }
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# Program to find nth
# centered decagonal number

# Centered decagonal
# number function
def centereddecagonalnum(n) :

    # Formula to calculate
    # nth centered decagonal
    # number & return it
    # into main function.
    return (5 * n * n +
            5 * n + 1)

# Driver Code
if __name__ == '__main__' :

    n = 5
    print(n,"th centered decagonal " +
                          "number : ",
              centereddecagonalnum(n))

    n = 9
    print(n,"th centered decagonal " +
                          "number : ",
              centereddecagonalnum(n))

# This code is contributed by m_kit
```

## C#

```
// Program to find nth
// centered decagonal
// number
using System;

class GFG
{
// Centered decagonal
// number function
static int centereddecagonalnum(int n)
{
    // Formula to calculate nth
    // centered decagonal number &
    // return it into main function.
    return (5 * n * n + 5 * n + 1);
}

// Driver Code
static public void Main ()
{
int n = 5;
Console.Write(n + "th centered decagonal"+
                              "number: ");
Console.WriteLine(centereddecagonalnum(n));

n = 9;
Console.Write(n + "th centered decagonal"+
                              "number: ");
Console.WriteLine(centereddecagonalnum(n));
}
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find nth
// centered decagonal number

// Centered decagonal
// number function
function centereddecagonalnum($n)
{
    // Formula to calculate
    // nth centered decagonal
    // number & return it
    // into main function.
    return (5 * $n * $n +
            5 * $n + 1);
}

// Driver Code
$n = 5;
echo $n , "th centered decagonal",
                       "number: ";
echo centereddecagonalnum($n);
echo "\n";

$n = 9;
echo $n , "th centered decagonal",
                       "number: ";
echo centereddecagonalnum($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript Program to find nth
// centered decagonal number

// Centered decagonal
// number function
function centereddecagonalnum(n)
{

    // Formula to calculate nth
    // centered decagonal number &
    // return it into main function.
    return (5 * n * n + 5 * n + 1);
}

// Driver Code
var n = 5;
document.write(n + "th centered " +
               "decagonal number: ");
document.write(centereddecagonalnum(n) + "<br>");

n = 9;
document.write(n + "th centered " +
               "decagonal number: ");
document.write(centereddecagonalnum(n));

// This code is contributed by Kirti

</script>
```

**输出**

```
5th centered decagonalnumber: 151
9th centered decagonalnumber: 451
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)