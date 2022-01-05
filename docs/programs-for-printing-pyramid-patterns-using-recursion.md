# 使用递归打印金字塔图案的程序

> 原文:[https://www . geesforgeks . org/programs-for-printing-金字塔-patterns-use-recursion/](https://www.geeksforgeeks.org/programs-for-printing-pyramid-patterns-using-recursion/)

本文旨在给出一个用于图案印刷的[递归实现](https://www.geeksforgeeks.org/recursion/)。

*   **Simple triangle mode:**

## c++

T0T33】JavaT35

```
// Java code to demonstrate star pattern
import java.io.*;

class GFG
{

// function to print a row
static void printn(int num)
{
    // base case
    if (num == 0)
        return;
    System.out.print ("* ");

    // recursively calling printn()
    printn(num - 1);
}

// function to print the pattern
static void pattern(int n, int i)
{
    // base case
    if (n == 0)
        return;
    printn(i);
    System.out.println();

    // recursively calling pattern()
    pattern(n - 1, i + 1);
}

// Driver code
public static void main (String[] args)
{

    int n = 5;
    pattern(n, 1);
}
}

// This code is contributed by ajit.
```

T36

## python 3

T39

```
# Python3 code to demonstrate star pattern

# function to print a row
def printn(num):

    # base case
    if (num == 0):
        return
    print("*", end = " ")

    # recursively calling printn()
    printn(num - 1)

# function to print the pattern
def pattern(n, i):

    # base case
    if (n == 0):
        return
    printn(i)
    print("\n", end = "")

    # recursively calling pattern()
    pattern(n - 1, i + 1)

# Driver Code
if __name__ == '__main__':
    n = 5
    pattern(n, 1)

# This code is contributed by
# Surendra_Gangwar
```

T40

## C #

```
// C# code to demonstrate star pattern
using System;

class GFG
{

// function to print a row
static void printn(int num)
{
    // base case
    if (num == 0)
        return;
    Console.Write("* ");

    // recursively calling printn()
    printn(num - 1);
}

// function to print the pattern
static void pattern(int n, int i)
{
    // base case
    if (n == 0)
        return;
    printn(i);
    Console.WriteLine();

    // recursively calling pattern()
    pattern(n - 1, i + 1);
}

// Driver code
static public void Main ()
{
    int n = 5;
    pattern(n, 1);
}
}

// This code is contributed by akt_mit.
```

## PHP

```
<?php
// PHP code to demonstrate star pattern

// Function to print a row
function printn($num)
{
    // base case
    if ($num == 0)
        return;
    echo "* ";

    // recursively calling printn()
    printn($num - 1);
}

// function to print the pattern
function pattern($n, $i)
{
    // base case
    if ($n == 0)
        return;
    printn($i);
    echo "\n";

    // recursively calling pattern()
    pattern($n - 1, $i + 1);
}

// Driver Code
$n = 5;
pattern($n, 1);

// This code is contributed by @Tushil..
?>
```

## Javascript

```
<script>

// JavaScript code to demonstrate star pattern

    // function to print a row
    function printn(num) {
        // base case
        if (num == 0)
            return;
        document.write("* ");

        // recursively calling printn()
        printn(num - 1);
    }

    // function to print the pattern
    function pattern(n , i) {
        // base case
        if (n == 0)
            return;
        printn(i);
        document.write("<br/>");

        // recursively calling pattern()
        pattern(n - 1, i + 1);
    }

    // Driver code

        var n = 5;
        pattern(n, 1);

// This code is contributed by aashish1995

</script>
```

**输出:**

```
* 
* * 
* * * 
* * * * 
* * * * *
```

T57】

**180 度旋转后:**

T67】c++

```
// C# code to demonstrate star pattern
using System;

class GFG
{

// function to print spaces
static void print_space(int space)
{
    // base case
    if (space == 0)
        return;
    Console.Write(" " + " ");

    // recursively calling print_space()
    print_space(space - 1);
}

// function to print asterisks
static void print_asterisk(int asterisk)
{
    // base case
    if (asterisk == 0)
        return;
    Console.Write("* ");

    // recursively calling print_asterisk()
    print_asterisk(asterisk - 1);
}

// function to print the pattern
static void pattern(int n, int num)
{
    // base case
    if (n == 0)
        return;
    print_space(n - 1);
    print_asterisk(num - n + 1);
    Console.WriteLine();

    // recursively calling pattern()
    pattern(n - 1, num);
}

// Driver code
public static void Main()
{
    int n = 5;
    pattern(n, n);
}
}

// This code is contributed by Akanksha Rai
```

## PHP

```
<?php
// PHP code to demonstrate star pattern
// function to print spaces
function print_space($space)
{
    // base case
    if ($space == 0)
        return;
    echo " ",
            " ";

    // recursively calling print_space()
    print_space($space - 1);
}

// function to print asterisks
function print_asterisk($asterisk)
{
    // base case
    if ($asterisk == 0)
        return;
    echo "* ";

    // recursively calling print_asterisk()
    print_asterisk($asterisk - 1);
}

// function to print the pattern
function pattern($n, $num)
{
    // base case
    if ($n == 0)
        return;
    print_space($n - 1);
    print_asterisk(($num - $n) + 1);
    echo "\n";

    // recursively calling pattern()
    pattern($n - 1, $num);
}

// Driver Code
$n = 5;
pattern($n, $n);

// This code is contributed by @Tushil.
?>
```

## Javascript

```
<script>
// javascript code to demonstrate star pattern

    // function to print spaces
    function print_space(space) {
        // base case
        if (space == 0) {
            return;
        }
        document.write(" " + "  ");

        // recursively calling print_space()
        print_space(space - 1);
    }

    // function to print asterisks
    function print_asterisk(asterisk) {
        // base case
        if (asterisk == 0) {
            return;
        }
        document.write("* ");

        // recursively calling print_asterisk()
        print_asterisk(asterisk - 1);
    }

    // function to print the pattern
    function pattern(n , num) {
        // base case
        if (n == 0) {
            return;
        }
        print_space(n - 1);
        print_asterisk(num - n + 1);
        document.write("<br/>");

        // recursively calling pattern()
        pattern(n - 1, num);
    }

    // Driver code

        var n = 5;
        pattern(n, n);

// This code contributed by aashish1995
</script>
```

**输出:**

```
        * 
      * * 
    * * * 
  * * * * 
* * * * *
```

*   T100] Printing Pyramid:

## c++

```
    * 
   * * 
  * * * 
 * * * * 
* * * * *
```