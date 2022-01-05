# 检查加号完美数字的程序

> 原文:[https://www . geesforgeks . org/program-check-plus-perfect-number/](https://www.geeksforgeeks.org/program-check-plus-perfect-number/)

给定一个**n 位**数字 x，检查它是否是一个正完全数。如果一个数等于其数字的 n 次方的和，则该数为正完全数。

**例:**

```
Input : x  = 371
Output : Yes
Explanation :  
Number of digits n = 3
(3*3*3) + (7*7*7) + (1*1*1) = 371

Input : x = 9474
Output : Yes
Explanation : 
Number of digits n = 4
(9*9*9*9) + (4*4*4*4) + (7*7*7*7) + 
(4*4*4*4) = 9474

Input : x = 9473
Output : No
Explanation : 
Number of digits n = 4
(9*9*9*9) + (4*4*4*4) + (7*7*7*7) +
(3*3*3*3) != 9474
```

下面是检查一个数是否是正完全数的实现。

## c++

```
// CPP implementation to check
// if the number is plus perfect
// or not
#include <bits/stdc++.h>
using namespace std;

// function to check plus perfect number
bool checkplusperfect(int x)
{
    int temp = x;

    // calculating number of digits
    int n = 0;
    while (x != 0) {
        x /= 10;
        n++;
    }  

    // calculating plus perfect number
    x = temp;
    int sum = 0;
    while (x != 0) {
        sum += pow(x % 10, n);
        x /= 10;
    }

    // checking whether number
    // is plus perfect or not
    return (sum == temp);
}

// driver program
int main()
{   
    int x = 9474;
    if (checkplusperfect(x))
        cout << "Yes";
    else
        cout << "No";       
    return 0;
}
```

## Java

```
// java implementation to check
// if the number is plus perfect
// or not
import java.io.*;

class GFG {

    // function to check plus perfect number
    static boolean checkplusperfect(int x)
    {
        int temp = x;

        // calculating number of digits
        int n = 0;
        while (x != 0)
        {
            x /= 10;
            n++;
        }

        // calculating plus perfect number
        x = temp;
        int sum = 0;
        while (x != 0)
        {
            sum += Math.pow(x % 10, n);
            x /= 10;
        }

        // checking whether number
        // is plus perfect or not
        return (sum == temp);
    }

    // Driver program
    public static void main (String[] args)
    {
        int x = 9474;
        if (checkplusperfect(x))
            System.out.println ( "Yes");
        else
            System.out.println ( "No");

    }
}

// This code is contributed by vt_m
```

## python 3

T2

## c#

T21

```
// C# implementation to check
// if the number is plus perfect
// or not
using System;

class GFG {

    // function to check plus perfect number
    static bool checkplusperfect(int x)
    {
        int temp = x;

        // calculating number of digits
        int n = 0;
        while (x != 0)
        {
            x /= 10;
            n++;
        }

        // calculating plus perfect number
        x = temp;
        int sum = 0;
        while (x != 0)
        {
            sum += (int)Math.Pow(x % 10, n);
            x /= 10;
        }

        // checking whether number
        // is plus perfect or not
        return (sum == temp);
    }

    // Driver program
    public static void Main ()
    {
        int x = 9474;
        if (checkplusperfect(x))
            Console.WriteLine ( "Yes");
        else
            Console.WriteLine ( "No");

    }
}

// This code is contributed by vt_m
```

## PHP

```
<?php
// PHP implementation to check
// if the number is plus perfect
// or not

// function to check plus
// perfect number
function checkplusperfect($x)
{
    $temp = $x;

    // calculating number
    // of digits
    $n = 0;
    while ($x != 0)
    {
        $x /= 10;
        $n++;
    }

    // calculating plus
    // perfect number
    $x = $temp;
    $sum = 0;
    while ($x != 0)
    {
        $sum += pow($x % 10, $n);
        $x /= 10;
    }

    // checking whether number
    // is plus perfect or not
    return ($sum == $temp);
}

    // Driver Code
    $x = 9474;
    if (checkplusperfect(!$x))
        echo "Yes";
    else
        echo "No";

// This code is contributed by ajit
?>
```

## Javascript

```
<script>

// Javascript implementation to check
// if the number is plus perfect
// or not

// Function to check plus perfect number
function checkplusperfect(x)
{
    let temp = x;

    // Calculating number of digits
    let n = 0;

    while (x != 0)
    {
        x = parseInt(x / 10);
        n++;
    }  

    // Calculating plus perfect number
    x = temp;
    let sum = 0;

    while (x != 0)
    {
        sum += Math.pow(x % 10, n);
        x = parseInt(x/10);
    }

    // Checking whether number
    // is plus perfect or not
    return (sum == temp);
}

// Driver Code
let x = 9474;

if (checkplusperfect(x))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by souravmahato348

</script>
```

**输出:**

```
Yes
```