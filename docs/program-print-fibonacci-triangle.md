# 打印斐波那契三角形的程序

> 原文:[https://www . geesforgeks . org/program-print-Fibonacci-triangle/](https://www.geeksforgeeks.org/program-print-fibonacci-triangle/)

给定 n(n < 10)的值，即行数，打印斐波那契三角形。

**示例:**

```
Input : n = 5 
Output :
1 
1 2 
3 5 8 
13 21 34 55 
89 144 233 377 610 

Input : n = 7
Output :
1 
1 2 
3 5 8 
13 21 34 55 
89 144 233 377 610 
987 1597 2584 4181 6765 10946 
17711 28657 46368 75025 121393 196418 317811 
```

[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是以下整数序列中的数字。
1，1，2，3，5，8，13，21，34，55，89，144，…..
在数学术语中，斐波那契数列 Fn 由递推关系定义

```
    Fn = Fn-1 + Fn-2
```

种子值为 F <sub>1</sub> = 1，F <sub>2</sub> = 1。

下面是上述模式的实现:

## C++

```
// C++ Implementation for
// Fibonacci triangle
#include <bits/stdc++.h>
using namespace std;

// function to fill Fibonacci Numbers
// in f[]
void fib(int f[], int N)
{
    // 1st and 2nd number of the
    // series are 1 and 1
    f[1] = 1;
    f[2] = 1;

    for (int i = 3; i <= N; i++)

        // Add the previous 2 numbers
        // in the series and store it
        f[i] = f[i - 1] + f[i - 2];
}

void fiboTriangle(int n)
{
    // Fill Fibonacci numbers in f[] using
    // fib(). We need N = n*(n+1)/2 Fibonacci
    // numbers to make a triangle of height
    // n
    int N = n * (n + 1) / 2;
    int f[N + 1];
    fib(f, N);

    // To store next Fibonacci Number to print
    int fiboNum = 1;

    // for loop to keep track of
    // number of lines
    for (int i = 1; i <= n; i++) {
        // For loop to keep track of
        // numbers in each line
        for (int j = 1; j <= i; j++)
            cout << f[fiboNum++] << " ";

        cout << endl;
    }
}

// Driver code
int main()
{
    int n = 5;
    fiboTriangle(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation for
// Fibonacci triangle
import java.io.*;

class GFG {

    // function to fill Fibonacci Numbers
    // in f[]
    static void fib(int f[], int N)
    {
        // 1st and 2nd number of the
        // series are 1 and 1
        f[1] = 1;
        f[2] = 1;

        for (int i = 3; i <= N; i++)

            // Add the previous 2 numbers
            // in the series and store it
            f[i] = f[i - 1] + f[i - 2];
    }

    static void fiboTriangle(int n)
    {
        // Fill Fibonacci numbers in f[] using
        // fib(). We need N = n*(n+1)/2 Fibonacci
        // numbers to make a triangle of height
        // n
        int N = n * (n + 1) / 2;
        int f[] = new int[N + 1];
        fib(f, N);

        // To store next Fibonacci
        // Number to print
        int fiboNum = 1;

        // for loop to keep track of
        // number of lines
        for (int i = 1; i <= n; i++) {
            // For loop to keep track of
            // numbers in each line
            for (int j = 1; j <= i; j++)
                System.out.print(f[fiboNum++] + " ");

            System.out.println();
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        fiboTriangle(n);
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 Implementation for
# Fibonacci triangle

# function to fill Fibonacci
# Numbers in f[]
def fib(f, N):

    # 1st and 2nd number of
    # the series are 1 and 1
    f[1] = 1
    f[2] = 1

    for i in range(3, N + 1):

        # Add the previous 2 numbers
        # in the series and store it
        f[i] = f[i - 1] + f[i - 2]

def fiboTriangle(n):

    # Fill Fibonacci numbers in
    # f[] using fib(). We need
    # N = n*(n + 1)/2 Fibonacci
    # numbers to make a triangle
    # of height n
    N = n * (n + 1) // 2
    f = [0] * (N + 1)
    fib(f, N)

    # To store next Fibonacci
    # Number to print
    fiboNum = 1

    # for loop to keep track of
    # number of lines
    for i in range(1, n + 1):

        # For loop to keep track of
        # numbers in each line
        for j in range(1, i + 1):

            print(f[fiboNum], " ", end="")
            fiboNum = fiboNum + 1

        print()

# Driver code
n = 5
fiboTriangle(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Implementation for
// Fibonacci triangle
using System;

class GFG {

    // function to fill Fibonacci Numbers
    // in f[]
    static void fib(int[] f, int N)
    {
        // 1st and 2nd number of the
        // series are 1 and 1
        f[1] = 1;
        f[2] = 1;

        for (int i = 3; i <= N; i++)

            // Add the previous 2 numbers
            // in the series and store it
            f[i] = f[i - 1] + f[i - 2];
    }

    static void fiboTriangle(int n)
    {
        // Fill Fibonacci numbers in f[] using
        // fib(). We need N = n*(n+1)/2 Fibonacci
        // numbers to make a triangle of height
        // n
        int N = n * (n + 1) / 2;
        int[] f = new int[N + 1];
        fib(f, N);

        // To store next Fibonacci
        // Number to print
        int fiboNum = 1;

        // for loop to keep track of
        // number of lines
        for (int i = 1; i <= n; i++) {
            // For loop to keep track of
            // numbers in each line
            for (int j = 1; j <= i; j++)
                Console.Write(f[fiboNum++] + " ");

            Console.WriteLine();
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        fiboTriangle(n);
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Implementation for
// Fibonacci triangle

// function to fill
// Fibonacci Numbers
// in f[]
function fib(&$f, $N)
{
    // 1st and 2nd number
    // of the series are
    // 1 and 1
    $f[1] = 1;
    $f[2] = 1;

    for ($i = 3;
         $i <= $N; $i++)

        // Add the previous
        // 2 numbers in the
        // series and store it
        $f[$i] = $f[$i - 1] +
                 $f[$i - 2];
}

function fiboTriangle($n)
{
    // Fill Fibonacci numbers
    // in f[] using fib(). We
    // need N = n*(n+1)/2
    // Fibonacci numbers to make
    // a triangle of height n
    $N = $n * ($n + 1) / 2;
    $f = array();
    fib($f, $N);

    // To store next
    // Fibonacci Number
    // to print
    $fiboNum = 1;

    // for loop to keep track
    // of number of lines
    for ($i = 1; $i <= $n; $i++)
    {
        // For loop to keep track
        // of numbers in each line
        for ($j = 1;$j <= $i; $j++)
            echo ($f[$fiboNum++] . " ");

        echo("\n");
    }
}

// Driver code
$n = 5;
fiboTriangle($n);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// JavaScript implementation for
// Fibonacci triangle

// Function to fill Fibonacci Numbers
// in f[]
function fib(f, N)
{

    // 1st and 2nd number of the
    // series are 1 and 1
    f[1] = 1;
    f[2] = 1;

    for(var i = 3; i <= N; i++)

        // Add the previous 2 numbers
        // in the series and store it
        f[i] = f[i - 1] + f[i - 2];
}

function fiboTriangle(n)
{

    // Fill Fibonacci numbers in f[] using
    // fib(). We need N = n*(n+1)/2 Fibonacci
    // numbers to make a triangle of height
    // n
    var N = (n * (n + 1)) / 2;
    var f = [...Array(N + 1)];
    fib(f, N);

    // To store next Fibonacci Number to print
    var fiboNum = 1;

    // for loop to keep track of
    // number of lines
    for(var i = 1; i <= n; i++)
    {
        // For loop to keep track of
        // numbers in each line
        for(var j = 1; j <= i; j++)
            document.write(f[fiboNum++] + " ");

        document.write("<br>");
    }
}

// Driver code
var n = 5;

fiboTriangle(n);

// This code is contributed by rdtank

</script>
```

**输出:**

```
1 
1 2 
3 5 8 
13 21 34 55 
89 144 233 377 610 
```