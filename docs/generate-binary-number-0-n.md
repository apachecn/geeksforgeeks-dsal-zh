# 生成从 0 到 n 的所有二进制数

> 原文:[https://www.geeksforgeeks.org/generate-binary-number-0-n/](https://www.geeksforgeeks.org/generate-binary-number-0-n/)

给定一个正整数 n，生成从 0 到 n 的所有二进制数。

**示例:**

```
Input :  5
Output : 0  1  10  11  100  101    
Binary numbers are 0(0), 1(1), 2(10), 
3(11), 4(100) and 5(101).

Input : 10
Output : 0 1  10  11  100   101  110  
         111  1000  1001  1010

```

这个程序简单的使用预定义的函数( [itoa()在 C++中](https://www.geeksforgeeks.org/implement-itoa/))来转换你想要的基数。所以简单的使用了这些函数并将二进制数转换为由三个值组成。

## C++

```
// CPP function to generate all binary number
// from 0 to given number n
#include<iostream>
#include<stdlib.h>
using namespace std;

// Maximum length of generated binary number
const int MAX = 100;

// CPP function to generate all binary number 
// for given number n
char binaryGenerator(int n)
{
    char a[MAX];

    for (int i = 0; i <= n; i++) {

        // use define function itoa() to convert 
        // in given base
        // a is char[] array where value store
        // 2  is base, which convert.
        itoa(i, a, 2);

        cout << a << endl;
    }
}

// Driven program
int main()
{
    int n = 10;
    binaryGenerator(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java function to generate 
// all binary number from 
// 0 to given number n
import java.io.*;

class GFG
{ 
    static String itoa(int x, 
                       int base)
    {
        boolean negative = false;
        String s = "";
        if (x == 0)
            return "0";
        negative = (x < 0);
        if (negative)
            x = -1 * x;
        while (x != 0) 
        {
            // add char to
            // front of s
            s = (x % base) + s; 

            // integer division 
            // gives quotient
            x = x / base; 
        }
        if (negative)
            s = "-" + s;
        return s;
    }

    // function to generate
    // all binary number 
    // for given number n
    static void binaryGenerator(int n)
    {
        System.out.print("0 ");
        for (int i = 1; i <= n; i++)
        {

            // use define function 
            // itoa() to convert 
            // in given base
            // a is char[] array 
            // where value store
            // 2 is base, which convert.
            String a = new String(itoa(i, 2));

            System.out.print(a.substring(
                        0, a.length()) + " ");
        }
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;
        binaryGenerator(n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python function to generate 
# all binary number from 
# 0 to given number n

def itoa(x, base) :

    negative = False
    s = ""
    if (x == 0) :
        return "0"
    negative = (x < 0)
    if (negative) :
        x = -1 * x
    while (x != 0) :

        # add char to
        # front of s
        s = str(x % base) + s 

        # integer division 
        # gives quotient
        x = int(x / base) 

    if (negative) :
        s = "-" . s

    return s

# function to generate
# all binary number 
# for given number n
def binaryGenerator(n) :

    print ("0 ", end = "")
    for i in range(1, n + 1) :

        # use define function 
        # itoa() to convert 
        # in given base
        # a is char[] array 
        # where value store
        # 2 is base, which convert.
        a = itoa(i, 2)

        print ("{} ".format(a[0:]), end = "") 

# Driver Code
n = 10
binaryGenerator(n)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# function to generate 
// all binary number from 
// 0 to given number n
using System;

class GFG
{ 
    static String itoa(int n, 
                       int radix) 
    {
        if(0 == n)
            return "0";

        var index = 10;
        var buffer = new char[1 + index];
        var xlat = "0123456789abcdefghijklmnopqrstuvwxyz";

        for(int r = Math.Abs(n), q; r > 0; r = q) 
        {
            q = Math.DivRem(r, radix, out r);
            buffer[index -= 1] = xlat[r];
        }

        if(n < 0) 
        {
            buffer[index -= 1] = '-';
        }

        return new String(buffer, index, 
                          buffer.Length - 
                                 index);
    }

    // function to generate
    // all binary number 
    // for given number n
    static void binaryGenerator(int n)
    {
        string a = "";
        Console.Write("0 ");
        for (int i = 1; i <= n; i++)
        {

            // use define function 
            // itoa() to convert 
            // in given base
            // a is char[] array 
            // where value store
            // 2 is base, which convert.
            a = itoa(i, 2);

            Console.Write(a.Substring(
                          0, a.Length - 1) + " ");
        }
    }

    // Driver Code
    static void Main()
    {
        int n = 10;
        binaryGenerator(n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP function to generate 
// all binary number from 
// 0 to given number n

function itoa($x, $base)
{
    $negative = false;
    $s = "";
    if ($x == 0)
        return "0";
    $negative = ($x < 0);
    if ($negative)
        $x = -1 * $x;
    while ($x != 0) 
    {
        // add char to
        // front of s
        $s = ($x % $base) . $s; 

        // integer division 
        // gives quotient
        $x = intval($x / $base); 
    }
    if ($negative)
        $s = "-" . $s;

    return $s;
}

// function to generate
// all binary number 
// for given number n
function binaryGenerator($n)
{
    echo ("0 ");
    for ($i = 1; $i <= $n; $i++)
    {
        // use define function 
        // itoa() to convert 
        // in given base
        // a is char[] array 
        // where value store
        // 2 is base, which convert.
        $a = itoa($i, 2);

        echo (substr($a, 0) . " ");
    }
}

// Driver Code
$n = 10;
binaryGenerator($n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

**输出:**

```
 0  1  10  11  100   101  110  111  1000  1001  1010

```