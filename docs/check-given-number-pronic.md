# 检查给定的数字是否是 Pronic

> 原文:[https://www.geeksforgeeks.org/check-given-number-pronic/](https://www.geeksforgeeks.org/check-given-number-pronic/)

可以排列成矩形的数字称为[矩形数字(也称为 Pronic 数字)](https://www.geeksforgeeks.org/rectangular-numbers/)。前几个 Pronic 号码是:
0、2、6、12、20、30、42、56、72、90、110、132、156、182、210、240、272、306、342、380、420、462。。。。。。
Pronic 数是两个连续整数的乘积，即数字 n 是 x 和(x+1)的乘积。任务是检查和打印一定范围内的 Pronic 数字。
**例:**

```
Input  : 6
Output : Pronic Number
Explanation: 6 = 2 * 3 i.e 6 is a product
of two consecutive integers 2 and 3.

Input :56
Output :Pronic Number
Explanation: 56 = 7 * 8 i.e 56 is a product 
of two consecutive integers 7 and 8\. 

Input  : 8
Output : Not a Pronic Number
Explanation: 8 = 2 * 4 i.e 8 is a product of 
2 and 4 which are not consecutive integers.
```

## C++

```
// C/C++ program to check
// if a number is pronic
#include <iostream>
#include <math.h>
using namespace std;

// function to check
// Pronic Number
bool checkPronic(int x)
{

    for (int i = 0;
            i <= (int)(sqrt(x));
            i++)

        // Checking Pronic Number
        // by multiplying consecutive
        // numbers
        if (x == i * (i + 1))
        return true;

    return false;
}

// Driver Code
int main(void)
{
    // Printing Pronic Numbers
    // upto 200
    for (int i = 0; i <= 200; i++)
        if (checkPronic(i))
            cout << i << " ";

    return 0;
}

// This code is contributed
// by Nikita Tiwari.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check and
// Print Pronic Number upto 200
import java.io.*;
import java.util.*;
import java.math.*;

class GFG
{

    // function to check Pronic Number
    static boolean checkPronic(int x)
    {
        for (int i = 0;
             i <= (int)(Math.sqrt(x));
             i++)

            // Checking Pronic Number
            // by multiplying consecutive
            // numbers
            if (x == i * (i + 1))
                return true;

        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Printing Pronic
        // Numbers upto 200
        for (int i = 0; i <= 200; i++)
            if (checkPronic(i))
                System.out.print(i + " ");    
    }
}

// This code is contributed
// by Nikita Tiwari
```

## 计算机编程语言

```
# Python program to check
# and print Pronic Numbers
# upto 200
import math

# function to check
# Pronic Number
def checkPronic (x) :

    i = 0
    while ( i <= (int)(math.sqrt(x)) ) :

        # Checking Pronic Number
        # by multiplying consecutive
        # numbers
        if ( x == i * (i + 1)) :
            return True
        i = i + 1

    return False

# Driver Code

# Printing Pronic
# Numbers upto 200
i = 0
while (i <= 200 ) :
    if checkPronic(i) :
        print i,
    i = i + 1

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// Java program to check and
// Print Pronic Number upto 200
using System;

class GFG
{

    // function to check
    // Pronic Number
    static bool checkPronic(int x)
    {
        for (int i = 0;
                 i <= (int)(Math.Sqrt(x));
                 i++)

            // Checking Pronic Number by
            // multiplying consecutive numbers
            if (x == i * (i + 1))
                return true;

        return false;
    }

    // Driver Code
    public static void Main()
    {
        // Printing Pronic
        // Numbers upto 200
        for (int i = 0; i <= 200; i++)
            if (checkPronic(i))
                Console.Write(i + " ");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if a number is pronic

// function to check
// Pronic Number
function checkPronic($x)
{

    for ($i = 0;
         $i <= (sqrt($x));
         $i++)

        // Checking Pronic Number
        // by multiplying consecutive
        // numbers
        if ($x == $i * ($i + 1))
        return true;

    return false;
}

// Driver Code

// Printing Pronic
// Numbers upto 200
for ($i = 0; $i <= 200; $i++)
    if (checkPronic($i))
        echo $i , " ";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// if a number is pronic

// function to check
// Pronic Number
function checkPronic(x)
{

    for (var i = 0;
            i <= parseInt(Math.sqrt(x));
            i++)

        // Checking Pronic Number
        // by multiplying consecutive
        // numbers
        if (x == i * (i + 1))
        return true;

    return false;
}

// Driver Code

// Printing Pronic Numbers
// upto 200
for (var i = 0; i <= 200; i++)
    if (checkPronic(i))
        document.write(i + " ");

// This code is contributed by noob2000
</script>
```

**输出:**

```
0 2 6 12 20 30 42 56 72 90 110 132 156 182
```

本文由**尼基塔·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。