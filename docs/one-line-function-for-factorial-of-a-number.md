# 一个数的阶乘的一行函数

> 原文:[https://www . geeksforgeeks . org/一行函数换一个数的阶乘/](https://www.geeksforgeeks.org/one-line-function-for-factorial-of-a-number/)

[非负整数的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)，是所有小于或等于 n 的整数的乘积

```
Example :

Factorial of 6 is 6 * 5 * 4 * 3 * 2 * 1 which is 720.
```

我们可以借助**三元算子**或者递归中俗称的**条件算子**来求一行数字的阶乘。

## C++

```
// C++ program to find factorial of given number
#include<iostream>

int factorial(int n)
{
    // single line to find factorial
    return (n==1 || n==0) ? 1: n * factorial(n - 1);
}

// Driver Code
int main()
{
    int num = 5;
    printf ("Factorial of %d is %d", num, factorial(num));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find factorial of given number

import java.io.*;

class GFG {

    static int factorial(int n)
    {

        // single line to find factorial
        return (n == 1 || n == 0) ? 1 : n *
                                factorial(n - 1);
    }

    public static void main(String[] args)
    {

        int num = 5;

        System.out.println("Factorial of " + num +
                           " is " + factorial(num));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 program to find
# factorial of given number

def factorial(n):

    # single line to
    # find factorial
    return 1 if (n == 1 or n == 0) else n * factorial(n - 1);

# Driver Code
num = 5;
print("Factorial of", num,
      "is", factorial(num));

# This is contributed by mits
```

## C#

```
// C# program to find factorial
// of given number
using System;

class GFG
{

    // Function to calculate factorial
    static int factorial(int n)
    {

        // single line to find factorial
        return (n == 1 || n == 0) ?
                1 : n * factorial(n - 1);
    }

    public static void Main()
    {

        int num = 5;
        Console.WriteLine("Factorial of " + num +
                        " is " + factorial(num));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// factorial of given number

function factorial($n)
{
    // single line to find factorial
    return ($n==1 || $n==0) ? 1 :
            $n * factorial($n - 1);
}

// Driver Code
$num = 5;
echo "Factorial of ", $num,
     " is ", factorial($num);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find
// factorial of given number

function factorial(n)
{
    // single line to find factorial
    return (n == 1 || n == 0) ? 1 :
            n * factorial(n - 1);
}

// Driver Code
let num = 5;
document.write("Factorial of ", num,
     " is ", factorial(num));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
 Factorial of 5 is 120
```