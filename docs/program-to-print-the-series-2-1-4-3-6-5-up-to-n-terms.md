# 程序打印系列 2、1、4、3、6、5、…。最多 N 个术语

> 原文:[https://www . geesforgeks . org/program-to-print-the-series-2-1-4-3-6-5-up-n-terms/](https://www.geeksforgeeks.org/program-to-print-the-series-2-1-4-3-6-5-up-to-n-terms/)

给定一个数字 N，任务是将下面的模式打印成 N 个术语:

> 2, 1, 4, 3, 6, 5, ….n 项

**例:**

```
Input: N = 4
Output: 2, 1, 4, 3

Explanation:
Nth Term = (N % 2 == 0) ? (N - 1) : (N + 1)
1st term = (1 % 2 == 0) ? (1 - 1) : (1 + 1)
         = (1 + 1)
         = 2
2nd term = (2 % 2 == 0) ? (2 - 1) : (2 + 1)
         = (2 - 1)
         = 1
3rd term = (3 % 2 == 0) ? (3 - 1) : (3 + 1)
         = (3 + 1)
         = 4
4th term = (4 % 2 == 0) ? (4 - 1) : (4 + 1)
         = (4 - 1)
         = 3
Therefore, Series = 2, 1, 4, 3

Input: N = 7
Output: 2, 1, 4, 3, 6, 5, 8
```

**公式:**

```
Nth Term = (N % 2 == 0) ? (N - 1) : (N + 1)
```

以下是上述问题的解决方案:

## C++

```
// C++ program to print the series
// 2, 1, 4, 3, 6, 5, …. up to N terms
#include <iostream>
using namespace std;

// Function to print the series
void printPattern(int N)
{

    for (int i = 1; i <= N; i++) {

        // Find and print the ith term
        cout <<" "<<((i % 2 == 0) ? (i - 1) : (i + 1));
    }
}

// Driver code
int main()
{

    // Get the value of N
    int N = 10;

    // Print the Series
    printPattern(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print the series
// 2, 1, 4, 3, 6, 5, …. up to N terms

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// Function to print the series
static void printPattern(int N)
{

    for (int i = 1; i <= N; i++) {

        // Find and print the ith term
        System.out.print(" "+((i % 2 == 0) ? (i - 1) : (i + 1)));
    }
}

// Driver code
public static void main(String args[])
{

    // Get the value of N
    int N = 10;

    // Print the Series
    printPattern(N);

}
}
```

## 蟒蛇 3

```
# Python program to print the series
# 2, 1, 4, 3, 6, 5, …. up to N terms

# Function to print the series
def printPattern(N):
    for i in range(1, N + 1):

        # Find and print the ith term
        print(i - 1 if i % 2 == 0
                    else i + 1, end = " ")

# Driver code
N = 10
printPattern(N)

# This code is contributed by Shrikant13
```

## C#

```
// C# program to print the series
// 2, 1, 4, 3, 6, 5, …. up to N terms
using System;

class GFG
{
// Function to print the series
public void printPattern(int N)
{

    for (int i = 1; i <= N; i++)
    {

        // Find and print the ith term
        int a = ((i % 2 == 0) ?
                      (i - 1) : (i + 1));
        Console.Write(" {0}", a);
    }
}

// Driver code
public static void Main()
{
    GFG g = new GFG();

    // Get the value of N
    int N = 10;

    // Print the Series
    g.printPattern(N);
}
}

// This code is contributed
// by Soumik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the series
// 2, 1, 4, 3, 6, 5, …. up to N terms

// Function to print the series
function printPattern($N)
{

    for ($i = 1; $i <= $N; $i++)
    {

        // Find and print the ith term
        echo " " . (($i % 2 == 0) ?
                    ($i - 1) : ($i + 1));
    }
}

// Driver code

// Get the value of N
$N = 10;

// Print the Series
printPattern($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// javascript program to print the series
// 2, 1, 4, 3, 6, 5, …. up to N terms

// Function to print the series
function printPattern( N)
{

    for (let i = 1; i <= N; i++)
    {

        // Find and print the ith term
        document.write(" " + ((i % 2 == 0) ? (i - 1) : (i + 1)));
    }
}

// Driver code

    // Get the value of N
    let N = 10;

    // Print the Series
    printPattern(N);

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
2 1 4 3 6 5 8 7 10 9
```