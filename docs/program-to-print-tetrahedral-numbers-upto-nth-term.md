# 打印第 n 项四面体数字的程序

> 原文:[https://www . geesforgeks . org/program-to-print-四面体-numbers-up-n-term/](https://www.geeksforgeeks.org/program-to-print-tetrahedral-numbers-upto-nth-term/)

**先决条件:**

*   [三角数字](https://www.geeksforgeeks.org/triangular-numbers/)
*   [四面体数](https://www.geeksforgeeks.org/tetrahedral-numbers/)

给定一个值 n，任务是打印四面体数序列直到第 n <sup>个</sup>项。
**例:**

```
Input: 5
Output: 1  4  10  20  35

Input: 10
Output: 1  4  10  20  35  56  84  120  165  220 
```

**方法一:使用三角数级数:**
这个问题很容易用 N <sup>次</sup>四面体数等于前 N 个三角数之和来解决。
我们来看看三角四面体数系列。

```
To print series upto 5th term:
Triangular Numbers  =  1        3          6             10                  15
Tetrahedral numbers =  1        4          10            20                  35 
                 i.e  (1)    (1 + 3)  (1 + 3 + 6)  (1 + 3 + 6 + 10)  (1 + 3 + 6 + 10 + 35)   
```

使用公式![\frac{N \times (N + 1)}{2}    ](img/6b2d6d9bf69cc1c6ca117893196975d1.png "Rendered by QuickLaTeX.com")
计算第 N <sup>个</sup>个三角数，这样，通过生成三角数并将其与之前生成的所有三角数之和相加来打印四面体数系列。
以下是上述方法的实施:

## C++

```
// C++ program to generate tetrahedral
// number series
#include <bits/stdc++.h>
using namespace std;

// function to generate nth triangular
// number
long findTriangularNumber(int n)
{
    return (n * (n + 1)) / 2;
}

// function to print tetrahedral number
// series up to n
void printSeries(int n)
{
    // Initialize prev as 0\. It stores
    // the sum of all previously generated
    // triangular number
    int prev = 0;
    int curr;

    // Loop to print series
    for (int i = 1; i <= n; i++)
    {
        // Find ith triangular number
        curr = findTriangularNumber(i);

        // Add ith triangular number to
        // sum of all previously generated
        // triangular number to get ith
        // tetrahedral number
        curr = curr + prev;
        cout << curr << " ";

        // Update sum of all previously
        // generated triangular number
        prev = curr;
    }
}

// Driver code
int main()
{
    int n = 10;

    // function call to print series
    printSeries(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate tetrahedral
// number series
import java.io.*;

class GFG {

    // function to generate nth triangular
    // number
    static long findTriangularNumber(int n)
    {
        return (n * (n + 1)) / 2;
    }

    // function to print tetrahedral number
    // series up to n
    static void printSeries(int n)
    {
        // Initialize prev as 0\. It store
        // the sum of all previously generated
        // triangular number
        long prev = 0;
        long curr;

        // Loop to print series
        for (int i = 1; i <= n; i++)
        {
            // Find ithh triangular number
            curr = findTriangularNumber(i);

            // Add ith triangular number to
            // sum of all previously generated
            // triangular number to get ith
            // tetrahedral number
            curr = curr + prev;
            System.out.print(curr + " ");

            // Update sum of all previously
            // generated triangular number
            prev = curr;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        // function call to print series
        printSeries(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to generate
# tetrahedral number series

# function to generate nth
# triangular number
def findTriangularNumber(n):
    return (n * (n + 1)) / 2

# function to print tetrahedral
# number series up to n
def printSeries(n):

    # Initialize prev as 0.
    # It stores the sum of all
    # previously generated
    # triangular number
    prev = 0

    # Loop to print series
    for i in range(1, n+1):

        # Find ith triangular number
        curr = findTriangularNumber(i)

        # Add ith triangular number
        # to sum of all previously
        # generated triangular number
        # to get ith tetrahedral number
        curr = int(curr + prev)
        print(curr, end = ' ')

        # Update sum of all previously
        # generated triangular number
        prev = curr

# Driver code
n = 10

# function call to
# print series
printSeries(n)

# This code is contributed by Mahadev.
```

## C#

```
// C# program to generate tetrahedral
// number series
using System;

public class GFG{

    // function to generate nth triangular
    // number
    static long findTriangularNumber(int n)
    {
        return (n * (n + 1)) / 2;
    }

    // function to print tetrahedral number
    // series up to n
    static void printSeries(int n)
    {
        // Initialize prev as 0\. It store
        // the sum of all previously generated
        // triangular number
        long prev = 0;
        long curr;

        // Loop to print series
        for (int i = 1; i <= n; i++)
        {
            // Find ithh triangular number
            curr = findTriangularNumber(i);

            // Add ith triangular number to
            // sum of all previously generated
            // triangular number to get ith
            // tetrahedral number
            curr = curr + prev;
            Console.Write(curr + " ");

            // Update sum of all previously
            // generated triangular number
            prev = curr;
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 10;

        // function call to print series
        printSeries(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate tetrahedral
// number series

// function to generate nth triangular
// number
function findTriangularNumber($n)
{
    return ($n * ($n + 1)) / 2;
}

// function to print tetrahedral number
// series up to n
function printSeries($n)
{
    // Initialize prev as 0\. It store
    // the sum of all previously generated
    // triangular number
    $prev = 0;
    $curr;

    // Loop to print series
    for ($i = 1; $i <= $n; $i++)
    {
        // Find ithh triangular number
        $curr = findTriangularNumber($i);

        // Add ith triangular number to
        // sum of all previously generated
        // triangular number to get ith
        // tetrahedral number
        $curr = $curr + $prev;
        echo($curr . " ");

        // Update sum of all previously
        // generated triangular number
        $prev = $curr;
    }
}

// Driver code
$n = 10;

// function call to print series
printSeries($n);
?>
```

## java 描述语言

```
<script>
// Javascript program to generate tetrahedral
// number series

// function to generate nth triangular
// number
function findTriangularNumber(n)
{
    return (n * (n + 1)) / 2;
}

// function to print tetrahedral number
// series up to n
function printSeries(n)
{

    // Initialize prev as 0\. It stores
    // the sum of all previously generated
    // triangular number
    var prev = 0;
    var curr;

    // Loop to print series
    for (var i = 1; i <= n; i++)
    {
        // Find ith triangular number
        curr = findTriangularNumber(i);

        // Add ith triangular number to
        // sum of all previously generated
        // triangular number to get ith
        // tetrahedral number
        curr = curr + prev;
        document.write( curr + " ");

        // Update sum of all previously
        // generated triangular number
        prev = curr;
    }
}

// Driver code
var n = 10;

// function call to print series
printSeries(n);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
1 4 10 20 35 56 84 120 165 220
```

**时间复杂度:** O(n)
**方法二:利用四面体数公式:**
公式求 n <sup>th</sup> 四面体数:![\frac{N\times (N+1)\times (N+2)}{6}    ](img/dd72584c1fbf299e91a7e0ab82631e05.png "Rendered by QuickLaTeX.com")
以下是所需实现:

## C++

```
// C++ program to generate series of
// tetrahedral numbers
#include <bits/stdc++.h>
using namespace std;

// function to print tetrahedral
// number series up to n
void printSeries(int n)
{

    // loop to print series
    for (int i = 1; i <= n; i++)
    {
        // Calculate and print ith
        // tetrahedral number
                int num = i * (i + 1) * (i + 2) / 6;
        cout << num << " ";
    }
}

// Driver code
int main()
{
    int n = 10;

    // function call to print series
    printSeries(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate series of
// tetrahedral numbers
import java.io.*;

class GFG {

    // function to print tetrahedral
    // number series up to n
    static void printSeries(int n)
    {

        // loop to print series
        for (int i = 1; i <= n; i++)
        {
            // Calculate and print ith
            // tetrahedral number
            int num = i * (i + 1) * (i + 2) / 6;

            System.out.print(num + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 10;

        // function call to print series
        printSeries(n);
    }
}
```

## 蟒蛇 3

```
# Python3 code to print tetrahedral
# numbers series up to n

# function to print tetrahedral series up to n
def printSeries(n):

    # loop to print series
    for i in range(1, n + 1):

        # Calculate and print ith
        # Tetrahedral number
        num = i * (i + 1) * (i + 2) // 6

        print(num, end =' ')

# Driver code
n = 10

# function call to print series
printSeries(n)
```

## C#

```
// C# program to generate series of
// tetrahedral numbers
using System;

public class GFG{

    // function to print tetrahedral
    // number series up to n
    static void printSeries(int n)
    {

        // loop to print series
        for (int i = 1; i <= n; i++)
        {
            // Calculate and print ith
            // tetrahedral number
            int num = i * (i + 1) * (i + 2) / 6;

            Console.Write(num + " ");
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 10;

        // function call to print series
        printSeries(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to generate series of
// tetrahedral numbers

// function to print tetrahedral
// number series up to n
function printSeries($n)
{

    // loop to print series
    for ($i = 1; $i <= $n; $i++)
    {
        // Calculate and print ith
        // tetrahedral number
        $num = $i * ($i + 1) * ($i + 2) / 6;
        echo ($num . " ");
    }
}

// Driver code
$n = 10;

// function call to print series
printSeries($n);

?>
```

## java 描述语言

```
<script>

// Javascript program to generate series of
// tetrahedral numbers

    // function to print tetrahedral
    // number series up to n
    function printSeries(n)
    {
      let i;

        // loop to print series
        for (i = 1; i <= n; i++)
        {
            // Calculate and print ith
            // tetrahedral number
            let num = i * (i + 1) * ((i + 2) / 6);

            document.write(num + " ");
        }
    }

// driver program

        let n = 10;

        // function call to print series
        printSeries(n);

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1 4 10 20 35 56 84 120 165 220
```