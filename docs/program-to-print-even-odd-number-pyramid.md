# 打印偶数奇数金字塔的程序

> 原文:[https://www . geesforgeks . org/程序转打印-偶数-奇数-金字塔/](https://www.geeksforgeeks.org/program-to-print-even-odd-number-pyramid/)

给定总行数为 n，任务是打印给定的图案。

> *
> 1 *
> * 2 *
> 1 * 3 *
> * 2 * 4 *
> 1 * 3 * 5 *
> 2 * 4 * 6 *
> 1 * 3 * 5 * 7 *
> 2 * 4 * 6 * 8 *
> 1 * 3 * 5 * 7 * 9 *
> 。
> 。

**例:**

```
Input: n = 5
Output:
*
1*
*2*
1*3*
*2*4*

Input: n = 10
Output:
*
1*
*2*
1*3*
*2*4*
1*3*5*
*2*4*6*
1*3*5*7*
*2*4*6*8*
1*3*5*7*9*
```

以下是上述问题的解决方案:

## C++

```
// CPP program to print Even Odd Number Pyramid

#include <iostream>
using namespace std;

// function for creating pattern
void Pattern(int n)
{
    // Initialization
    int i, j, k;
    for (i = 1; i <= n; i++) {

        for (j = 1, k = i; j <= i; j++, k--) {

            if (k % 2 == 0) {

                // displaying the numbers
                cout << j;
            }
            else {

                // displaying the stars
                cout << "*";
            }
        }
        cout << "\n";
    }
}

// driver code
int main()
{

    // Get n
    int n = 5;

    // Print the pattern
    Pattern(n);

    return 0;
}
```

## C

```
// C program to print Even Odd Number Pyramid

#include <stdio.h>

// function for creating pattern
void Pattern(int n)
{
    // Initialization
    int i, j, k;
    for (i = 1; i <= n; i++) {
        for (j = 1, k = i; j <= i; j++, k--) {
            if (k % 2 == 0) {

                // displaying the numbers
                printf("%d", j);
            }
            else {

                // displaying the stars
                printf("*");
            }
        }
        printf("\n");
    }
}

// driver code
int main()
{

    // Get n
    int n = 5;

    // Print the pattern
    Pattern(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print above pattern

import java.util.Scanner;

class Pattern {
    static void display(int n)
    {

        int i, j, k;
        for (i = 1; i <= n; i++) {

            for (j = 1, k = i; j <= i; j++, k--) {

                if (k % 2 == 0) {
                    // displaying the numbers
                    System.out.print(j);
                }
                else {
                    // displaying the stars
                    System.out.print("*");
                }
            }
            System.out.print("\n");
        }
    }
    // Driver Code
    public static void main(String[] args)
    {

        // Get n
        int n = 5;

        // Print the pattern
        display(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print above pattern
def display(n):
    for i in range(1, n + 1):
        k = i
        for j in range(1, i + 1):
            if k % 2 == 0:

                # Displaying the numbers
                print(j, end = '')
            else:

                # Displaying the stars
                print('*', end = '')
            k -= 1
        print()

# Driver Code

# Get n
n = 5

# Print the pattern
display(n)

# This code is contributed by SamyuktaSHegde
```

## C#

```
// C# program to print above pattern
using System;

class GFG
{
static void display(int n)
{

    int i, j, k;
    for (i = 1; i <= n; i++)
    {

        for (j = 1, k = i; j <= i; j++, k--)
        {

            if (k % 2 == 0)
            {
                // displaying the numbers
                Console.Write(j);
            }
            else
            {
                // displaying the stars
                Console.Write("*");
            }
        }
        Console.Write("\n");
    }
}

// Driver Code
public static void Main()
{

    // Get n
    int n = 5;

    // Print the pattern
    display(n);
}
}

// This code is contributed by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program to print
// above pattern

function display($n)
{
    // Initialization
    $i;
    $j;
    $k;

    for($i=1; $i<=$n; $i++)
    {
        for($j=1, $k=$i; $j<=$i; $j++, $k--)
        {
            if($k%2==0){

            // displaying the numbers
               echo $j;
}
            else{

            // displaying the stars
                echo "*";
}
        }
        echo "\n";
    }
}

// Driver Code

// Get n
$n = 5;

// Print the pattern
display($n);

?>
```

## java 描述语言

```
<script>

// Javascript program to print Even Odd Number Pyramid

// function for creating pattern
function Pattern(n)
{
    // Initialization
    var i, j, k;
    for (i = 1; i <= n; i++) {

        for (j = 1, k = i; j <= i; j++, k--) {

            if (k % 2 == 0) {

                // displaying the numbers
                document.write( j);
            }
            else {
                // displaying the stars
                document.write("*");
            }
        }
        document.write("<br>");
    }
}

// driver code
// Get n
var n = 5;

// Print the pattern
Pattern(n);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
*
1*
*2*
1*3*
*2*4*
```