# 不使用*、/和–

打印前 n 个自然数的正方形

> 原文:[https://www . geesforgeks . org/print-squares-first-n-natural-numbers-不使用/](https://www.geeksforgeeks.org/print-squares-first-n-natural-numbers-without-using/)

给定一个自然数“n”，不使用*、/和-打印前 n 个自然数的平方。
**例:**

```
Input:  n = 5
Output: 0 1 4 9 16

Input:  n = 6
Output: 0 1 4 9 16 25
```

**强烈建议尽量减少浏览器，先自己试试这个。**
**方法一:**思路是利用之前的平方值计算下一个平方。考虑以下 x 的平方和(x-1)之间的关系。我们知道(x-1)的平方是(x-1)<sup>2</sup>–2 * x+1。我们可以把 x <sup>2</sup> 写成

```
x2 = (x-1)2 + 2*x - 1 
x2 = (x-1)2 + x + (x - 1)
```

在编写迭代程序时，我们可以跟踪 x 的先前值，并将 x 的当前值和先前值加到 square 的当前值上。这样我们甚至不用“-”运算符。
以下是上述方法的实施:

## C++

```
// C++ program to print squares of first 'n' natural numbers
// without using *, / and -
#include<iostream>
using namespace std;

void printSquares(int n)
{
    // Initialize 'square' and previous value of 'x'
    int square = 0, prev_x = 0;

    // Calculate and print squares
    for (int x = 0; x < n; x++)
    {
        // Update value of square using previous value
        square = (square + x + prev_x);

        // Print square and update prev for next iteration
        cout << square << " ";
        prev_x = x;
    }
}

// Driver program to test above function
int main()
{
   int n = 5;
   printSquares(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print squares
// of first 'n' natural numbers
// without using *, / and
import java.io.*;

class GFG
{
static void printSquares(int n)
{
    // Initialize 'square' and
    // previous value of 'x'
    int square = 0, prev_x = 0;

    // Calculate and
    // print squares
    for (int x = 0; x < n; x++)
    {
        // Update value of square
        // using previous value
        square = (square + x + prev_x);

        // Print square and update
        // prev for next iteration
        System.out.print( square + " ");
        prev_x = x;
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 5;
    printSquares(n);
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python 3 program to print squares of first
# 'n' natural numbers without using *, / and -
def printSquares(n):

    # Initialize 'square' and previous
    # value of 'x'
    square = 0; prev_x = 0;

    # Calculate and print squares
    for x in range(0, n):

        # Update value of square using
        # previous value
        square = (square + x + prev_x)

        # Print square and update prev 
        # for next iteration
        print(square, end = " ")
        prev_x = x

# Driver Code
n = 5;
printSquares(n);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C#  program to print squares
// of first 'n' natural numbers
// without using *, / and
using System;

public class GFG{

    static void printSquares(int n)
{
    // Initialize 'square' and
    // previous value of 'x'
    int square = 0, prev_x = 0;

    // Calculate and
    // print squares
    for (int x = 0; x < n; x++)
    {
        // Update value of square
        // using previous value
        square = (square + x + prev_x);

        // Print square and update
        // prev for next iteration
        Console.Write( square + " ");
        prev_x = x;
    }
}

// Driver Code

    static public void Main (){
        int n = 5;
        printSquares(n);
    }
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print squares
// of first 'n' natural numbers
// without using *, / and -

function printSquares($n)
{

    // Initialize 'square' and
    // previous value of 'x'
    $square = 0; $prev_x = 0;

    // Calculate and
    // print squares
    for ($x = 0; $x < $n; $x++)
    {

        // Update value of square
        // using previous value
        $square = ($square + $x + $prev_x);

        // Print square and update
        // prev for next iteration
        echo $square, " ";
        $prev_x = $x;
    }
}

    // Driver Code
    $n = 5;
    printSquares($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// JavaScript program to print squares of first 'n' natural numbers
// without using *, / and -

    function printSquares(n)
    {
        // Initialize 'square' and previous value of 'x'
        let square = 0, prev_x = 0;

        // Calculate and print squares
        for (let x = 0; x < n; x++)
        {
            // Update value of square using previous value
            square = (square + x + prev_x);

            // Print square and update prev for next iteration
            document.write(square + " ");
            prev_x = x;
        }
    }

    // Driver program to test above function

   let n = 5;
   printSquares(n);

// This code is contributed by Surbhi Tyagi

</script>
```

输出:

```
0 1 4 9 16
```

时间复杂度:0(n)

辅助空间:0(1)

**方法二:**前 n 个奇数之和是从 1 到 n 的自然数的平方，比如 1，1+3，1+3+5，1+3+5+7，1+3+5+7+9，…。
以下是基于上述概念的程序。感谢 Aadithya Umashanker 和 raviteja 提出这种方法。

## C++

```
// C++ program to print squares of first 'n' natural numbers
// without using *, / and -
#include<iostream>
using namespace std;

void printSquares(int n)
{
    // Initialize 'square' and first odd number
    int square = 0, odd = 1;

    // Calculate and print squares
    for (int x = 0; x < n; x++)
    {
        // Print square
        cout << square << " ";

        // Update 'square' and 'odd'
        square = square + odd;
        odd = odd + 2;
    }
}

// Driver program to test above function
int main()
{
   int n = 5;
   printSquares(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// squares of first 'n'
// natural numbers without
// using *, / and -
import java.io.*;

class GFG
{
static void printSquares(int n)
{
    // Initialize 'square'
    // and first odd number
    int square = 0, odd = 1;

    // Calculate and
    // print squares
    for (int x = 0; x < n; x++)
    {
        // Print square
        System.out.print(square +
                           " " );

        // Update 'square'
        // and 'odd'
        square = square + odd;
        odd = odd + 2;
    }
}

// Driver Code
public static void main (String[] args)
{
    int n = 5;
    printSquares(n);
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# Python3 program to print squares
# of first 'n' natural numbers
# without using *, / and -

def printSquares(n):

    # Initialize 'square' and
    # first odd number
    square = 0
    odd = 1

    # Calculate and print squares
    for x in range(0 , n):

        # Print square
        print(square, end= " ")

        # Update 'square' and 'odd'
        square = square + odd
        odd = odd + 2

# Driver Code
n = 5;
printSquares(n)

# This code is contributed
# by Rajput-Ji
```

## C#

```
// C# program to print squares of first 'n'
// natural numbers without using *, / and -
using System;

class GFG
{
static void printSquares(int n)
{
    // Initialize 'square'
    // and first odd number
    int square = 0, odd = 1;

    // Calculate and
    // print squares
    for (int x = 0; x < n; x++)
    {
        // Print square
        Console.Write(square + " " );

        // Update 'square'
        // and 'odd'
        square = square + odd;
        odd = odd + 2;
    }
}

// Driver Code
public static void Main ()
{
    int n = 5;
    printSquares(n);
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print squares
// of first 'n' natural numbers
// without using *, / and -
function printSquares($n)
{
    // Initialize 'square' and
    // first odd number
    $square = 0; $odd = 1;

    // Calculate and print squares
    for ($x = 0; $x < $n; $x++)
    {
        // Print square
        echo $square , " ";

        // Update 'square' and 'odd'
        $square = $square + $odd;
        $odd = $odd + 2;
    }
}

// Driver Code
$n = 5;
printSquares($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// Javascript program to print squares of first 'n' natural numbers
// without using *, / and -

function printSquares(n)
{
    // Initialize 'square' and first odd number
    let square = 0, odd = 1;

    // Calculate and print squares
    for (let x = 0; x < n; x++)
    {
        // Print square
        document.write(square + " ");

        // Update 'square' and 'odd'
        square = square + odd;
        odd = odd + 2;
    }
}

// Driver program to test above function
let n = 5;
printSquares(n);

// This code is contributed by subham348.
</script>
```

**输出:**

```
0 1 4 9 16
```

时间复杂度:0(n)

辅助空间:0(1)

本文由**沙钦**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息