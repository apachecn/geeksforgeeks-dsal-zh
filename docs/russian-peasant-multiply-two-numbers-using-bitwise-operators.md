# 俄罗斯农民(使用按位运算符将两个数字相乘)

> 原文:[https://www . geesforgeks . org/Russian-farmer-乘-两个数字-使用按位运算符/](https://www.geeksforgeeks.org/russian-peasant-multiply-two-numbers-using-bitwise-operators/)

给定两个整数，编写一个函数将它们相乘，而不使用乘法运算符。
两个数相乘还有很多其他的方法(比如看[这个](https://www.geeksforgeeks.org/multiply-two-numbers-without-using-multiply-division-bitwise-operators-and-no-loops/))。一个有趣的方法是[俄罗斯农民算法](http://en.wikipedia.org/wiki/Ancient_Egyptian_multiplication#Russian_peasant_multiplication)。这个想法是将第一个数字翻倍，将第二个数字重复减半，直到第二个数字不变成 1。在这个过程中，每当第二个数变成奇数，我们就把第一个数加到结果上(结果初始化为 0)
下面是简单的算法。

```
Let the two given numbers be 'a' and 'b'
1) Initialize result 'res' as 0.
2) Do following while 'b' is greater than 0
   a) If 'b' is odd, add 'a' to 'res'
   b) Double 'a' and halve 'b'
3) Return 'res'. 
```

## C++

```
#include <iostream>
using namespace std;

// A method to multiply two numbers using Russian Peasant method
unsigned int russianPeasant(unsigned int a, unsigned int b)
{
    int res = 0; // initialize result

    // While second number doesn't become 1
    while (b > 0)
    {
        // If second number becomes odd, add the first number to result
        if (b & 1)
            res = res + a;

        // Double the first number and halve the second number
        a = a << 1;
        b = b >> 1;
    }
    return res;
}

// Driver program to test above function
int main()
{
    cout << russianPeasant(18, 1) << endl;
    cout << russianPeasant(20, 12) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Russian Peasant Multiplication
import java.io.*;

class GFG
{
    // Function to multiply two
    // numbers using Russian Peasant method
    static int russianPeasant(int a, int b)
    {
        // initialize result
        int res = 0; 

        // While second number doesn't become 1
        while (b > 0)
        {
             // If second number becomes odd,
             // add the first number to result
             if ((b & 1) != 0)
                 res = res + a;

            // Double the first number
            // and halve the second number
            a = a << 1;
            b = b >> 1;
        }
        return res;
    }

    // driver program
    public static void main (String[] args)
    {
        System.out.println(russianPeasant(18, 1));
        System.out.println(russianPeasant(20, 12));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# A method to multiply two numbers
# using Russian Peasant method

# Function to multiply two numbers
# using Russian Peasant method
def russianPeasant(a, b):

    res = 0 # initialize result

    # While second number doesn't
    # become 1
    while (b > 0):

        # If second number becomes
        # odd, add the first number
        # to result
        if (b & 1):
            res = res + a

        # Double the first number
        # and halve the second
        # number
        a = a << 1
        b = b >> 1

    return res

# Driver program to test
# above function
print(russianPeasant(18, 1))
print(russianPeasant(20, 12))
# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program for Russian Peasant Multiplication
using System;

class GFG {

    // Function to multiply two
    // numbers using Russian Peasant method
    static int russianPeasant(int a, int b)
    {
        // initialize result
        int res = 0;

        // While second number doesn't become 1
        while (b > 0) {

            // If second number becomes odd,
            // add the first number to result
            if ((b & 1) != 0)
                res = res + a;

            // Double the first number
            // and halve the second number
            a = a << 1;
            b = b >> 1;
        }
        return res;
    }

    // driver program
    public static void Main()
    {
        Console.WriteLine(russianPeasant(18, 1));
        Console.WriteLine(russianPeasant(20, 12));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code to multiply two numbers
// using Russian Peasant method

// function returns the result
function russianPeasant($a, $b)
{

    // initialize result
    $res = 0;

    // While second number
    // doesn't become 1
    while ($b > 0)
    {

        // If second number becomes odd,
        // add the first number to result
        if ($b & 1)
            $res = $res + $a;

        // Double the first number and
        // halve the second number
        $a = $a << 1;
        $b = $b >> 1;
    }
    return $res;
}

    // Driver Code
    echo russianPeasant(18, 1), "\n";
    echo russianPeasant(20, 12), "\n";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// A method to multiply two numbers using Russian Peasant method
function russianPeasant(a, b)
{
    var res = 0; // initialize result

    // While second number doesn't become 1
    while (b > 0)
    {

        // If second number becomes odd, add the first number to result
        if (b & 1)
            res = res + a;

        // Double the first number and halve the second number
        a = a << 1;
        b = b >> 1;
    }
    return res;
}

// Driver program to test above function
document.write(russianPeasant(18, 1)+"<br>");
document.write(russianPeasant(20, 12));

    // This code is contributed by noob2000.
</script>
```

输出:

```
18
240
```

***时间复杂度:** O(log <sub>2</sub> b)*

***辅助空间:** O(1)*

**这是如何工作的？**
如果 b 为偶数，则 a*b 的值与(a*2)*(b/2)相同，否则值与((a*2)*(b/2) + a 相同。在 while 循环中，我们不断将“a”乘以 2，并将“b”除以 2。如果“b”在循环中变得奇怪，我们就把“a”加到“res”上。当“b”的值变成 1 时，“RES ”+“a”的值就给出了结果。
注意，当“b”是 2 的幂时，“res”将保持为 0，“a”将相乘。有关更多信息，请参见参考资料。
**参考:**
[http://mathforum.org/dr.math/faq/faq.peasant.html](http://mathforum.org/dr.math/faq/faq.peasant.html)
本文由**沙尔基·阿加瓦尔**整理。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息