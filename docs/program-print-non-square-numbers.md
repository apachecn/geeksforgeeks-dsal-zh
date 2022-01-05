# 程序打印非正方形数字

> 原文:[https://www . geesforgeks . org/program-print-non-square-numbers/](https://www.geeksforgeeks.org/program-print-non-square-numbers/)

写一个程序打印前 n 个非正方数(非完美正方)。

**示例:**

```
Input : 5
Output : 2 3 5 6 7

Input : 10
Output : 2 3 5 6 7 8 10 11 12 13
```

一种**天真的方法**是遍历所有从 1 到 n 的数字，对于每个数字，检查它是否是完美的正方形。如果不是完美的正方形，就打印出来。

## C++

```
// CPP program to print first n
// non-square numbers.
#include <bits/stdc++.h>
using namespace std;

// Function to check perfect square
bool isPerfectSquare(int n)
{
    if (n < 0)
        return false;

    int root = round(sqrt(n)));
    return n == root * root;
}

// function to print all
// non square number
void printnonsquare(int n)
{
    // variable which stores the
    // count
    int count = 0;
    for (int i = 1; count < n; ++i) {

        // not perfect square
        if (!isPerfectSquare(i)) {
            cout << i << " ";
            count++;
        }
    }
}
int main()
{
    int n = 10;
    printnonsquare(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first n
// non-square numbers.
import java.io.*;
import java.math.*;

class GFG {

    // Function to check perfect square
    static boolean isPerfectSquare(int n)
    {
       if (n < 0)
          return false;

       int root = Math.round((int)(Math.sqrt(n)));
       return n == root * root;
    }

    // function to print all
    // non square number
    static void printnonsquare(int n)
    {
        // variable which stores the
        // count
        int count = 0;
        for (int i = 1; count < n; ++i) {

            // not perfect square
            if (!isPerfectSquare(i)) {

                System.out.print(i + " ");
                count++;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        printnonsquare(n);
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to print
# first n non-square numbers.
import math

# Function to check perfect
# square
def isPerfectSquare(n) :

    if (n < 0) :
        return False

    root = round(math.sqrt(n))

    return (n == root * root)

# function to print all
# non square number
def printnonsquare(n) :

    # variable which stores the
    # count
    count = 0
    i = 1

    while(count < n) :

        # Not perfect square
        if (isPerfectSquare(i)== False) :
            print(i, end =" ")
            count = count + 1

        i = i + 1

n = 10
printnonsquare(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print first n
// non-square numbers.
using System;

class GFG
{
// Function to check perfect square
static bool isPerfectSquare(int n)
{
if (n < 0)
    return false;

double root = Math.Round((double )(Math.Sqrt(n)));
return n == root * root;
}

// function to print all
// non square number
static void printnonsquare(int n)
{
    // variable which stores the
    // count
    int count = 0;
    for (int i = 1; count < n; ++i)
    {

        // not perfect square
        if (!isPerfectSquare(i))
        {
            Console.Write(i + " ");
            count++;
        }
    }
}

// Driver code

static public void Main ()
{
    int n = 10;
    printnonsquare(n);
}
}

// This code is contributed by jit_t
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// CPP program to print first
// n non-square numbers.

// Function to check
// perfect square
function isPerfectSquare($n)
{
    if ($n < 0)
        return false;

    $root = round(sqrt($n));
    return $n == $root * $root;
}

// function to print all
// non square number
function printnonsquare($n)
{
    // variable which
    // stores the count
    $count = 0;
    for ($i = 1; $count < $n; ++$i)
    {

        // not perfect square
        if (!isPerfectSquare($i))
        {
            echo $i ." ";
            $count++;
        }
    }
}

// Driver Code
$n = 10;
printnonsquare($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print first n
// non-square numbers.

   // Function to check perfect square
    function isPerfectSquare(n)
    {
       if (n < 0)
          return false;

       let root = Math.round((Math.sqrt(n)));
       return n == root * root;
    }

    // function to print all
    // non square number
    function printnonsquare(n)
    {
        // variable which stores the
        // count
        let count = 0;
        for (let i = 1; count < n; ++i) {

            // not perfect square
            if (!isPerfectSquare(i)) {

                        document.write(i + " ");
                count++;
            }
        }
    }

// Driver code

        let n = 10;
        printnonsquare(n);

</script>
```

**输出:**

```
2 3 5 6 7 8 10 11 12 13
```

我们可以通过使用下面的公式
**F(n)= n+floor(1/2+sqrt(n))**
来改进上面的算法，通过应用这个函数我们得到第 n 个非平方数。
配方来源及证明: [Quora](https://www.quora.com/The-sequence-of-non-square-numbers-which-are-not-perfect-squares-i-e-2-3-5-6-7-8-10-can-be-obtained-by-the-formula-F-n-n+floor-0-5-+-sqrt-n-How-do-we-prove-this)

下面是上述方法的实现。

## C++

```
// CPP program to print first n
// non square number
#include <bits/stdc++.h>

// Returns n-th non-square number.
int nonsquare(int n)
{
    return n + (int)(0.5 + sqrt(n));
}

void printNonSquare(int n)
{
    // loop to print non squares
    // below n
    for (int i = 1; i <= n; i++)
        printf("%d ", nonsquare(i));
}

int main()
{
    int n = 10;
    printNonSquare(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first n
// non-square numbers.
import java.io.*;
import java.math.*;

class GFG {

    // Returns n-th non-square number.
    static int nonsquare(int n)
    {
        return n + (int)(0.5 + (Math.sqrt(n)));
    }

    static void printNonSquare(int n)
    {
        // loop to print non squares
        // below n
        for (int i = 1; i <= n; i++)
            System.out.print(nonsquare(i)+" ");
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        printNonSquare(n);
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to print
# first n non-square numbers.
import math

# Returns n-th non-square
# number.
def nonsquare(n) :

    return n + (int)(0.5 + math.sqrt(n))

def printNonSquare(n) :

    # loop to print non
    # squares below n
    for i in range(1, n + 1) :
        print(nonsquare(i), end = " ")

n = 10
printNonSquare(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print first n
// non-square numbers.
using System;

class GFG
{

    // Returns n-th non-square number.
    static int nonsquare(int n)
    {
        return n + (int)(0.5 + (Math.Sqrt(n)));
    }

    static void printNonSquare(int n)
    {
        // loop to print non squares
        // below n
        for (int i = 1; i <= n; i++)
            Console.Write(nonsquare(i)+" ");
    }

    // Driver code
    public static void Main()
    {
        int n = 10;
        printNonSquare(n);
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print first n
// non square number

// Returns n-th non-square number.
function nonsquare($n)
{
    return $n + (int)(0.5 + sqrt($n));
}

function printNonSquare($n)
{
    // loop to print non squares
    // below n
    for ($i = 1; $i <= $n; $i++)
        printf(nonsquare($i) . " ");
}

// Driver Code
$n = 10;
printNonSquare($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to print first n
// non square number

// Returns n-th non-square number.
function nonsquare(n)
{
    return n + parseInt(0.5 + Math.sqrt(n));
}

function printNonSquare(n)
{

    // loop to print non squares
    // below n
    for (let i = 1; i <= n; i++)
        document.write(nonsquare(i) + " ");
}

// Driver Code
let n = 10;
printNonSquare(n);

// This code is contributed by gfgking.
</script>
```

**输出:**

```
2 3 5 6 7 8 10 11 12 13
```

一个**替代解**是基于两个正方形之间的非正方形的数量总是偶数的事实。
两个连续数字 k 和 k+1 之间的非平方数计数为
=(k+1)<sup>2</sup>–k<sup>2</sup>+1
= 2k
1-4，4-9，9-16 之间的非平方数计数分别为 2，4，6，…。这些是偶数。

下面是上述方法的实现。

## C++

```
// CPP program to print first n
// non square number
#include <assert.h>
#include <math.h>
#include <stdio.h>

void printNonSquare(int n)
{
    int curr_count = 2, num = 2, count = 0;
    while (count < n) {

        // Print curr_count numbers. curr_count
        // is current gap between two square numbers.
        for (int i = 0; i < curr_count &&
                        count < n; i++) {
            printf("%d ", num);
            count++;
            num++;
        }

        // skip a square number.
        num++;

        // Count of next non-square numbers
        // is next even number.
        curr_count += 2;
    }
}

int main()
{
    int n = 10;
    printNonSquare(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first n
// non-square numbers.
import java.io.*;
import java.math.*;

class GFG {

    static void printNonSquare(int n)
    {
        int curr_count = 2, num = 2, count = 0;
        while (count < n) {

            // Print curr_count numbers. curr_count is
            //  current gap between two square numbers.
            for (int i = 0; i < curr_count &&
                                count < n; i++) {

                System.out.print( num+" ");

                count++;
                num++;
            }

            // skip a square number.
            num++;

            // Count of next non-square
            // numbers is next even number.
            curr_count += 2;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        printNonSquare(n);
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to print
# first n non-square numbers.
import math

# Returns n-th non-square
# number.
def printNonSquare(n) :

    curr_count = 2
    num = 2
    count = 0

    while (count < n) :

        # Print curr_count numbers.
        # curr_count is current gap
        # between two square numbers.
        i = 0

        while(i < curr_count and count < n) :

            print(num, end = " ")
            count = count + 1
            num = num + 1
            i = i + 1

        # skip a square number.
        num = num + 1

        # Count of next non-square
        # numbers is next even number.
        curr_count = curr_count + 2

n = 10
printNonSquare(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print
// first n non-square
// numbers.
using System;

class GFG
{
static void printNonSquare(int n)
{
    int curr_count = 2,
        num = 2, count = 0;
    while (count < n)
    {

        // Print curr_count
        // numbers. curr_count
        // is current gap between
        // two square numbers.
        for (int i = 0; i < curr_count &&
                            count < n; i++)
        {
            Console.Write(num + " ");

            count++;
            num++;
        }

        // skip a square number.
        num++;

        // Count of next
        // non-square numbers
        // is next even number.
        curr_count += 2;
    }
}

// Driver code
static public void Main ()
{
    int n = 10;
    printNonSquare(n);
}
}

// This code is contributed
// by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print first n
// non-square numbers.
function printNonSquare($n)
{
    $curr_count = 2; $num = 2; $count = 0;
    while ($count < $n)
    {

        // Print curr_count numbers. curr_count is
        // current gap between two square numbers.
        for ($i = 0; $i < $curr_count &&
                          $count < $n; $i++)
        {
            echo($num . " ");

            $count++;
            $num++;
        }

        // skip a square number.
        $num++;

        // Count of next non-square
        // numbers is next even number.
        $curr_count += 2;
    }
}

// Driver code
$n = 10;
printNonSquare($n);

// This code is contributed by Mukul Singh.
?>
```

## java 描述语言

```
<script>

// Javascript program to print first
// n non-square numbers.
function printNonSquare(n)
{
    let curr_count = 2, num = 2, count = 0;
    while (count < n)
    {

        // Print curr_count
        // numbers. curr_count
        // is current gap between
        // two square numbers.
        for(let i = 0;
                i < curr_count && count < n;
                i++)
        {
            document.write(num + " ");

            count++;
            num++;
        }

        // Skip a square number.
        num++;

        // Count of next
        // non-square numbers
        // is next even number.
        curr_count += 2;
    }
}

// Driver code
let n = 10;

printNonSquare(n);

// This code is contributed by decode2207

</script>
```

**输出:**

```
2 3 5 6 7 8 10 11 12 13
```