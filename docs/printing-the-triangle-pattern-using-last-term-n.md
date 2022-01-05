# 使用最后一项 N

打印三角形图案

> 原文:[https://www . geesforgeks . org/printing-the-triangle-pattern-use-last-term-n/](https://www.geeksforgeeks.org/printing-the-triangle-pattern-using-last-term-n/)

给定一个数字 N，它代表三角形模式的最后一项。任务是打印从 1 到 N 的三角形图案，这样每行就完成了。
三角形图案如下:

```
   1
  2 3
 4 5 6
7 8 9 10
.
.
```

**例:**

```
Input: N = 3
Output:
 1
2 3

Input: N = 7
Output:
   1
  2 3
 4 5 6

7 will not be printed as 
it would result in an incomplete row
```

**进场:**

*   从给定的最后一项 n 中找出完整的行数
    *   As:
        对于最大高度= 1，最后一项为 1
        对于最大高度= 2，最后一项为 3
        对于最大高度= 3，最后一项为 6
    *   所以最后一项形成了一个模式: [1，3，6，10，15，…](https://www.geeksforgeeks.org/sum-series-1-3-6-10-triangular-numbers/)
    *   因此，[数列 1、3、6、10、15 的第 n 项，……](https://www.geeksforgeeks.org/find-nth-term-series-136101521/)T2【A(n)= 1+2+3+4……+(n–1)+n
        = n(n+1)/2
        即 A(n)是前 n 个自然数之和。
    *   所以在

```
A(n) = n(n + 1) / 2
A(n) represents the last term (as per our problem),
and n represents the max height of the Triangle
```

*   因此，这可以看作:

```
Last term = height (height + 1) / 2
```

*   因此，

```
height = (-1 + sqrt(1 + 8*lastTerm)) / 2
```

*   找到最大高度后，就可以轻松打印三角形图案了。

以下是上述方法的实现:

## C++

```
// C++ code for printing the
// Triangle Pattern using last term N

#include <bits/stdc++.h>
using namespace std;

// Function to demonstrate printing pattern
void triangle(int n)
{
    // number of spaces
    int k = 2 * n - 2;

    // character to be printed
    int ch = 1;

    // outer loop to handle number of rows
    // n in this case
    for (int i = 0; i < n; i++) {

        // inner loop to handle number spaces
        // values changing acc. to requirement
        for (int j = 0; j < k; j++)
            cout << " ";

        // decrementing k after each loop
        k = k - 1;

        // inner loop to handle number of columns
        // values changing acc. to outer loop
        for (int j = 0; j <= i; j++) {
            // printing stars
            cout << ch++ << " ";
        }

        // ending line after each row
        cout << endl;
    }
}

// Function to find the max height
// or the number of lines
// in the triangle pattern
int maxHeight(int n)
{
    return (((int)sqrt(1 + 8.0 * n)) - 1) / 2;
}

// Driver Function
int main()
{
    int N = 9;
    triangle(maxHeight(N));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for printing the
// Triangle Pattern using last term N
import java.util.*;

class GFG
{

// Function to demonstrate printing pattern
static void triangle(int n)
{
    // number of spaces
    int k = 2 * n - 2;

    // character to be printed
    int ch = 1;

    // outer loop to handle number of rows
    // n in this case
    for (int i = 0; i < n; i++)
    {

        // inner loop to handle number spaces
        // values changing acc. to requirement
        for (int j = 0; j < k; j++)
            System.out.print(" ");

        // decrementing k after each loop
        k = k - 1;

        // inner loop to handle number of columns
        // values changing acc. to outer loop
        for (int j = 0; j <= i; j++)
        {
            // printing stars
            System.out.print(ch++ + " ");
        }

        // ending line after each row
        System.out.println();
    }
}

// Function to find the max height
// or the number of lines
// in the triangle pattern
static int maxHeight(int n)
{
    return (((int)Math.sqrt(1 + 8.0 * n)) - 1) / 2;
}

// Driver Code
public static void main(String[] args)
{
    int N = 9;
    triangle(maxHeight(N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code for printing the
# Triangle Pattern using last term N
from math import sqrt

# Function to demonstrate printing pattern
def triangle(n) :

    # number of spaces
    k = 2 * n - 2;

    # character to be printed
    ch = 1;

    # outer loop to handle number of rows
    # n in this case
    for i in range(n) :

        # inner loop to handle number spaces
        # values changing acc. to requirement
        for j in range(k) :
            print(" ", end = "");

        # decrementing k after each loop
        k = k - 1;

        # inner loop to handle number of columns
        # values changing acc. to outer loop
        for j in range(i + 1) :

            # printing stars
            print(ch, end = " ");
            ch += 1;

        # ending line after each row
        print()

# Function to find the max height
# or the number of lines
# in the triangle pattern
def maxHeight(n) :
    ans = (sqrt(1 + 8.0 * n) - 1) // 2;
    return int(ans);

# Driver Code
if __name__ == "__main__" :

    N = 9;
    triangle(maxHeight(N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# code for printing the
// Triangle Pattern using last term N
using System;

class GFG
{

// Function to demonstrate printing pattern
static void triangle(int n)
{
    // number of spaces
    int k = 2 * n - 2;

    // character to be printed
    int ch = 1;

    // outer loop to handle number of rows
    // n in this case
    for (int i = 0; i < n; i++)
    {

        // inner loop to handle number spaces
        // values changing acc. to requirement
        for (int j = 0; j < k; j++)
            Console.Write(" ");

        // decrementing k after each loop
        k = k - 1;

        // inner loop to handle number of columns
        // values changing acc. to outer loop
        for (int j = 0; j <= i; j++)
        {
            // printing stars
            Console.Write(ch++ + " ");
        }

        // ending line after each row
        Console.WriteLine();
    }
}

// Function to find the max height
// or the number of lines
// in the triangle pattern
static int maxHeight(int n)
{
    return (((int)Math.Sqrt(1 + 8.0 * n)) - 1) / 2;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 9;
    triangle(maxHeight(N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript code for printing the
// Triangle Pattern using last term N

// Function to demonstrate printing pattern
function triangle(n)
{

    // number of spaces
    var k = 2 * n - 2;

    // character to be printed
    var ch = 1;

    // outer loop to handle number of rows
    // n in this case
    for (var i = 0; i < n; i++) {

        // inner loop to handle number spaces
        // values changing acc. to requirement
        for (var j = 0; j < k; j++)
            document.write(" ");

        // decrementing k after each loop
        k = k - 1;

        // inner loop to handle number of columns
        // values changing acc. to outer loop
        for (var j = 0; j <= i; j++) {
            // printing stars
            document.write(ch++ + " ");
        }

        // ending line after each row
        document.write("<br>");
    }
}

// Function to find the max height
// or the number of lines
// in the triangle pattern
function maxHeight(n)
{
    return parseInt(((parseInt(Math.sqrt(1 + 8.0 * n))) - 1) / 2);
}

// Driver Function
var N = 9;
triangle(maxHeight(N));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
    1 
   2 3 
  4 5 6
```