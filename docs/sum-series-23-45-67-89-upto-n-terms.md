# 系列 2/3–4/5+6/7–8/9+——截止条款的总和

> 原文:[https://www . geesforgeks . org/sum-series-23-45-67-89-upto-n-terms/](https://www.geeksforgeeks.org/sum-series-23-45-67-89-upto-n-terms/)

给定 n 的值，求级数(2/3)–(4/5)+(6/7)–(8/9)+–––––––多达 n 项的和。
**例:**

```
Input : n = 5
Output : 0.744012
Series : (2 / 3) - (4 / 5) + (6 / 7) - (8 / 9) + (10 / 11)

Input : n = 7
Output : 0.754268
Series : (2 / 3) - (4 / 5) + (6 / 7) - (8 / 9) +
         (10 / 11) - (12 / 13) + (14 / 15)
```

## C++

```
// C++ program to find
// sum of given series
#include <bits/stdc++.h>
using namespace std;

// Function to find sum of series
// up-to n terms
double seriesSum(int n)
{
    // initializing counter by 1
    int i = 1;

    // variable to calculate result
    double res = 0.0;
    bool sign = true;

    // while loop until nth term
    // is not reached
    while (n > 0)
    {
        n--;

        // boolean type variable
        // for checking validation
        if (sign) {
            sign = !sign;
            res = res + (double)++i / ++i;
        }
        else {
            sign = !sign;
            res = res - (double)++i / ++i;
        }
    }

    return res;
}

// Driver Code
int main()
{
    int n = 5;
    cout << seriesSum(n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// sum of given series
import java.io.*;

class GFG {

    // Function to find sum of series
    // up-to n terms
    static double seriesSum(int n)
    {

    // initializing counter by 1
    int i = 1;

    // variable to calculate result
    double res = 0.0;
    boolean sign = true;

    // while loop until nth term
    // is not reached
    while (n > 0)
    {
        n--;

        // boolean type variable
        // for checking validation
        if (sign)
        {
            sign = !sign;
            res = res + (double)++i / ++i;
        }

        else
        {
            sign = !sign;
            res = res - (double)++i / ++i;
        }
    }

    return res;
}

    // Driver Code
    public static void main (String[] args) {

        int n = 5;

        System.out.print(seriesSum(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program to find
# sum of given series

# Function to find
# sum of series
# up-to n terms
def seriesSum(n):

    # initializing
    # counter by 1
    i = 1;

    # variable to
    # calculate result
    res = 0.0;
    sign = True;

    # while loop until nth
    # term is not reached
    while (n > 0):
        n = n - 1;

        # boolean type variable
        # for checking validation
        if (sign):
            sign = False;
            res = res + (i + 1) / (i + 2);
            i = i + 2;
        else:
            sign = True;
            res = res - (i + 1) / (i + 2);
            i = i + 2;

    return res;

# Driver Code
n = 5;
print(round(seriesSum(n), 6));

# This code is contributed
# by mits
```

## C#

```
// C# program to find
// sum of given series
using System;

class GFG {

    // Function to find sum of
    // series up-to n terms
    static double seriesSum(int n)
    {

    // initializing counter by 1
    int i = 1;

    // variable to calculate result
    double res = 0.0;
    bool sign = true;

    // while loop until nth term
    // is not reached
    while (n > 0)
    {
        n--;

        // boolean type variable
        // for checking validation
        if (sign)
        {
            sign = !sign;
            res = res + (double)++i / ++i;
        }

        else
        {
            sign = !sign;
            res = res - (double)++i / ++i;
        }
    }

    return res;
}

    // Driver Code
    public static void Main () {

        int n = 5;
        Console.Write(seriesSum(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sum of given series

// Function to find sum of series
// up-to n terms
function seriesSum($n)
{
    // initializing counter by 1
    $i = 1;

    // variable to calculate result
    $res = 0.0;
    $sign = true;

    // while loop until nth term
    // is not reached
    while ($n > 0)
    {
        $n--;

        // boolean type variable
        // for checking validation
        if ($sign) {
            $sign = !$sign;
            $res = $res + (double)++$i / ++$i;
        }
        else {
            $sign = !$sign;
            $res = $res - (double)++$i / ++$i;
        }
    }

    return $res;
}

// Driver Code
$n = 5;
echo(seriesSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript program to find
// sum of given series

// Function to find sum of series
// up-to n terms
function seriesSum( n)
{
    // initializing counter by 1
    let i = 1;

    // variable to calculate result
    let res = 0.0;
    let sign = true;

    // while loop until nth term
    // is not reached
    while (n > 0)
    {
        n--;

        // boolean type variable
        // for checking validation
        if (sign) {
            sign = !sign;
            res = res + ++i / ++i;
        }
        else {
            sign = !sign;
            res = res - ++i / ++i;
        }
    }

    return res;
}
// Driver Code
let n = 5 ;
   document.write(seriesSum(n).toFixed(6)) ;

// This code contributed by aashish1995

</script>
```

**输出:**

```
0.744012
```