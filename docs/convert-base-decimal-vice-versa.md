# 从任意基数转换为十进制，反之亦然

> 原文:[https://www . geesforgeks . org/convert-base-decimal-反之亦然/](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)

给定一个数字及其基数，将其转换为十进制。数字的基数可以是任何可以用 0 到 9 和 A 到 z 表示所有数字的东西。A 的值是 10，B 的值是 11，以此类推。写一个函数把数字转换成十进制。

**示例:**

```
Input number is given as string and output is an integer.

Input: str = "1100", base = 2 
Output: 12

Input: str = "11A", base = 16
Output: 282

Input: str = "123",  base = 8
Output: 83 
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
我们总是可以用下面的公式从任意基数转换成十进制。

```
"str" is input number as a string 
"base" is the base of the input number.

Decimal Equivalent is,
  1*str[len-1] + base*str[len-2] + (base)2*str[len-3] + ...
```

下面是上述公式的实现。

## C

```
// C program to convert a number from any base
// to decimal
#include <stdio.h>
#include <string.h>

// To return value of a char. For example, 2 is
// returned for '2'.  10 is returned for 'A', 11
// for 'B'
int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to convert a number from given base 'b'
// to decimal
int toDeci(char *str, int base)
{
    int len = strlen(str);
    int power = 1; // Initialize power of base
    int num = 0;  // Initialize result
    int i;

    // Decimal equivalent is str[len-1]*1 +
    // str[len-2]*base + str[len-3]*(base^2) + ...
    for (i = len - 1; i >= 0; i--)
    {
        // A digit in input number must be
        // less than number's base
        if (val(str[i]) >= base)
        {
           printf("Invalid Number");
           return -1;
        }

        num += val(str[i]) * power;
        power = power * base;
    }

    return num;
}

// Driver code
int main()
{
    char str[] = "11A";
    int base = 16;
    printf("Decimal equivalent of %s in base %d is "
           " %d\n", str, base, toDeci(str, base));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// a number from any base
// to decimal
import java.io.*;

class GFG
{
// To return value of a char.
// For example, 2 is returned
// for '2'. 10 is returned
// for 'A', 11 for 'B'
static int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to convert a
// number from given base
// 'b' to decimal
static int toDeci(String str,
                  int base)
{
    int len = str.length();
    int power = 1; // Initialize
                   // power of base
    int num = 0; // Initialize result
    int i;

    // Decimal equivalent is
    // str[len-1]*1 + str[len-2] *
    // base + str[len-3]*(base^2) + ...
    for (i = len - 1; i >= 0; i--)
    {
        // A digit in input number
        // must be less than
        // number's base
        if (val(str.charAt(i)) >= base)
        {
        System.out.println("Invalid Number");
        return -1;
        }

        num += val(str.charAt(i)) * power;
        power = power * base;
    }

    return num;
}

// Driver code
public static void main (String[] args)
{
    String str = "11A";
    int base = 16;
    System.out.println("Decimal equivalent of "+
                        str + " in base "+ base +
                                     " is "+ " "+
                              toDeci(str, base));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python program to convert a
# number from any base to decimal

# To return value of a char.
# For example, 2 is returned
# for '2'. 10 is returned for 'A',
# 11 for 'B'
def val(c):
    if c >= '0' and c <= '9':
        return ord(c) - ord('0')
    else:
        return ord(c) - ord('A') + 10;

# Function to convert a number
# from given base 'b' to decimal
def toDeci(str,base):
    llen = len(str)
    power = 1 #Initialize power of base
    num = 0     #Initialize result

    # Decimal equivalent is str[len-1]*1 +
    # str[len-2]*base + str[len-3]*(base^2) + ...
    for i in range(llen - 1, -1, -1):

        # A digit in input number must
        # be less than number's base
        if val(str[i]) >= base:
            print('Invalid Number')
            return -1
        num += val(str[i]) * power
        power = power * base
    return num

# Driver code
strr = "11A"
base = 16
print('Decimal equivalent of', strr,
              'in base', base, 'is',
                 toDeci(strr, base))

# This code is contributed
# by Sahil shelangia
```

## C#

```
// C# program to convert
// a number from any base
// to decimal
using System;

class GFG
{
// To return value of a char.
// For example, 2 is returned
// for '2'. 10 is returned
// for 'A', 11 for 'B'
static int val(char c)
{
    if (c >= '0' && c <= '9')
        return (int)c - '0';
    else
        return (int)c - 'A' + 10;
}

// Function to convert a
// number from given base
// 'b' to decimal
static int toDeci(string str,
                  int b_ase)
{
    int len = str.Length;
    int power = 1; // Initialize
                   // power of base
    int num = 0; // Initialize result
    int i;

    // Decimal equivalent is
    // str[len-1]*1 + str[len-2] *
    // base + str[len-3]*(base^2) + ...
    for (i = len - 1; i >= 0; i--)
    {
        // A digit in input number
        // must be less than
        // number's base
        if (val(str[i]) >= b_ase)
        {
        Console.WriteLine("Invalid Number");
        return -1;
        }

        num += val(str[i]) * power;
        power = power * b_ase;
    }

    return num;
}

// Driver code
public static void Main ()
{
    string str = "11A";
    int b_ase = 16;
    Console.WriteLine("Decimal equivalent of "+
                     str + " in base "+ b_ase +
                  " is " + toDeci(str, b_ase));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert a number from
// any base to decimal

// To return value of a char. For example,
// 2 is returned for '2'. 10 is returned
// for 'A', 11 for 'B'
function val($c)
{
    if ($c >= '0' && $c <= '9')
        return ord($c) - ord('0');
    else
        return ord($c) - ord('A') + 10;
}

// Function to convert a number from given
// base 'b' to decimal
function toDeci($str, $base)
{
    $len = strlen($str);
    $power = 1; // Initialize power of base
    $num = 0; // Initialize result

    // Decimal equivalent is str[len-1]*1 +
    // str[len-2]*base + str[len-3]*(base^2) + ...
    for ($i = $len - 1; $i >= 0; $i--)
    {
        // A digit in input number must be
        // less than number's base
        if (val($str[$i]) >= $base)
        {
            print("Invalid Number");
            return -1;
        }

        $num += val($str[$i]) * $power;
        $power = $power * $base;
    }

    return $num;
}

// Driver code
$str = "11A";
$base = 16;
print("Decimal equivalent of $str " .
      "in base $base is " . toDeci($str, $base));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to convert
// a number from any base
// to decimal

// To return value of a char.
// For example, 2 is returned
// for '2'. 10 is returned
// for 'A', 11 for 'B'
function val(c)
{
    if (c >= '0'.charCodeAt() &&
        c <= '9'.charCodeAt())
        return (c - '0'.charCodeAt());
    else
        return (c - 'A'.charCodeAt() + 10);
}

// Function to convert a
// number from given base
// 'b' to decimal
function toDeci(str, b_ase)
{
    let len = str.length;

    // Initialize
    // power of base
    let power = 1;

    // Initialize result
    let num = 0;
    let i;

    // Decimal equivalent is
    // str[len-1]*1 + str[len-2] *
    // base + str[len-3]*(base^2) + ...
    for(i = len - 1; i >= 0; i--)
    {

        // A digit in input number
        // must be less than
        // number's base
        if (val(str[i].charCodeAt()) >= b_ase)
        {
            document.write("Invalid Number");
            return -1;
        }

        num += val(str[i].charCodeAt()) * power;
        power = power * b_ase;
    }
    return num;
}

// Driver code
let str = "11A";
let b_ase = 16;

document.write("Decimal equivalent of "+
               str + " in base "+ b_ase +
               " is " + toDeci(str, b_ase));

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Decimal equivalent of 11A in base 16 is 282
```

**怎么做反转？**
让给定的输入十进制数为“输入数”，目标基数为“基数”。我们反复用基数除 inputNum，并存储余数。我们最终反转得到的字符串。下面是 C 实现。

## C

```
// C Program to convert decimal to any given base
#include <stdio.h>
#include <string.h>

// To return char for a value. For example '2'
// is returned for 2\. 'A' is returned for 10\. 'B'
// for 11
char reVal(int num)
{
    if (num >= 0 && num <= 9)
        return (char)(num + '0');
    else
        return (char)(num - 10 + 'A');
}

// Utility function to reverse a string
void strev(char *str)
{
    int len = strlen(str);
    int i;
    for (i = 0; i < len/2; i++)
    {
        char temp = str[i];
        str[i] = str[len-i-1];
        str[len-i-1] = temp;
    }
}

// Function to convert a given decimal number
// to a base 'base' and
char* fromDeci(char res[], int base, int inputNum)
{
    int index = 0;  // Initialize index of result

    // Convert input number is given base by repeatedly
    // dividing it by base and taking remainder
    while (inputNum > 0)
    {
        res[index++] = reVal(inputNum % base);
        inputNum /= base;
    }
    res[index] = '\0';

    // Reverse the result
    strev(res);

    return res;
}

// Driver program
int main()
{
    int inputNum = 282, base = 16;
    char res[100];
    printf("Equivalent of %d in base %d is "
           " %s\n", inputNum, base, fromDeci(res, base, inputNum));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert decimal to any given base
import java.lang.*;
import java.io.*;
import java.util.*;

class GFG
{

// To return char for a value. For
// example '2' is returned for 2.
// 'A' is returned for 10\. 'B' for 11
static char reVal(int num)
{
    if (num >= 0 && num <= 9)
        return (char)(num + 48);
    else
        return (char)(num - 10 + 65);
}

// Function to convert a given decimal number
// to a base 'base' and
static String fromDeci(int base1, int inputNum)
{
    String s = "";

    // Convert input number is given
    // base by repeatedly dividing it
    // by base and taking remainder
    while (inputNum > 0)
    {
        s += reVal(inputNum % base1);
        inputNum /= base1;
    }
    StringBuilder ix = new StringBuilder();

        // append a string into StringBuilder input1
        ix.append(s);

    // Reverse the result
    return new String(ix.reverse());
}

// Driver code
public static void main (String[] args)
{
    int inputNum = 282, base1 = 16;
    System.out.println("Equivalent of " + inputNum +
                            " in base "+base1+" is " +
                            fromDeci(base1, inputNum));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 Program to convert decimal to
# any given base

# To return char for a value. For example
# '2' is returned for 2\. 'A' is returned
# for 10\. 'B' for 11
def reVal(num):

    if (num >= 0 and num <= 9):
        return chr(num + ord('0'));
    else:
        return chr(num - 10 + ord('A'));

# Utility function to reverse a string
def strev(str):

    len = len(str);
    for i in range(int(len / 2)):
        temp = str[i];
        str[i] = str[len - i - 1];
        str[len - i - 1] = temp;

# Function to convert a given decimal
# number to a base 'base' and
def fromDeci(res, base, inputNum):

    index = 0; # Initialize index of result

    # Convert input number is given base
    # by repeatedly dividing it by base
    # and taking remainder
    while (inputNum > 0):
        res+= reVal(inputNum % base);
        inputNum = int(inputNum / base);

    # Reverse the result
    res = res[::-1];

    return res;

# Driver Code
inputNum = 282;
base = 16;
res = "";
print("Equivalent of", inputNum, "in base",
       base, "is", fromDeci(res, base, inputNum));

# This code is contributed by mits
```

## C#

```
// C# Program to convert decimal to any given base
using System;
using System.Collections;

class GFG
{

// To return char for a value. For
// example '2' is returned for 2.
// 'A' is returned for 10\. 'B' for 11
static char reVal(int num)
{
    if (num >= 0 && num <= 9)
        return (char)(num + 48);
    else
        return (char)(num - 10 + 65);
}

// Function to convert a given decimal number
// to a base 'base' and
static string fromDeci(int base1, int inputNum)
{
    string s = "";

    // Convert input number is given
    // base by repeatedly dividing it
    // by base and taking remainder
    while (inputNum > 0)
    {
        s += reVal(inputNum % base1);
        inputNum /= base1;
    }
    char[] res = s.ToCharArray();

    // Reverse the result
    Array.Reverse(res);
    return new String(res);
}

// Driver code
static void Main()
{
    int inputNum = 282, base1 = 16;
    Console.WriteLine("Equivalent of " + inputNum +
                            " in base "+base1+" is " +
                            fromDeci(base1, inputNum));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to convert decimal to
// any given base

// To return char for a value. For example '2'
// is returned for 2\. 'A' is returned for 10.
// 'B' for 11
function reVal($num)
{
    if ($num >= 0 && $num <= 9)
        return chr($num + ord('0'));
    else
        return chr($num - 10 + ord('A'));
}

// Utility function to reverse a string
function strev($str)
{
    $len = strlen($str);
    for ($i = 0; $i < $len / 2; $i++)
    {
        $temp = $str[$i];
        $str[$i] = $str[$len - $i - 1];
        $str[$len - $i - 1] = $temp;
    }
}

// Function to convert a given decimal
// number to a base 'base' and
function fromDeci($res, $base, $inputNum)
{
    $index = 0; // Initialize index of result

    // Convert input number is given base
    // by repeatedly dividing it by base
    // and taking remainder
    while ($inputNum > 0)
    {
        $res.= reVal($inputNum % $base);
        $inputNum = (int)($inputNum / $base);
    }

    // Reverse the result
    $res = strrev($res);

    return $res;
}

// Driver Code
$inputNum = 282;
$base = 16;
$res = "";
print("Equivalent of $inputNum in base $base is " .
                 fromDeci($res, $base, $inputNum));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript Program to convert decimal to any given base

    // To return char for a value. For
    // example '2' is returned for 2.
    // 'A' is returned for 10\. 'B' for 11
    function reVal(num)
    {
        if (num >= 0 && num <= 9)
            return String.fromCharCode(num + 48);
        else
            return String.fromCharCode(num - 10 + 65);
    }

    // Function to convert a given decimal number
    // to a base 'base' and
    function fromDeci(base1, inputNum)
    {
        let s = "";

        // Convert input number is given
        // base by repeatedly dividing it
        // by base and taking remainder
        while (inputNum > 0)
        {
            s += reVal(inputNum % base1);
            inputNum = parseInt(inputNum / base1, 10);
        }
        let res = s.split('');

        // Reverse the result
        res.reverse();
        return res.join("");
    }

    let inputNum = 282, base1 = 16;
    document.write("Equivalent of " + inputNum +
                            " in base "+base1+" is " +
                            fromDeci(base1, inputNum));

// This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Equivalent of 282 in base 16 is  11A
```

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息