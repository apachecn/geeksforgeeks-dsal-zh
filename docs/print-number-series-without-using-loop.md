# 不使用任何循环打印编号系列

> 原文:[https://www . geesforgeks . org/print-number-series-not-use-loop/](https://www.geeksforgeeks.org/print-number-series-without-using-loop/)

**问题–**给定两个数字 N 和 K，我们的任务是从 N 中减去一个数字 K，直到数字(N)大于零，一旦 N 变成负或零，我们就开始加 K，直到那个数字变成原来的数字(N)。
**注意:**不允许使用任何循环。
**例:**

```
Input : N = 15 K = 5  
Output : 15 10 5 0 1 5 10 15

Input : N = 20 K = 6
Output : 20 14 8 2 -4 2 8 14 20 
```

**解释–**我们可以用**递归**的思想来做，就是我们一次又一次的调用函数，直到 N 大于零(在每次的函数调用中，我们用 K 减去 N)。一旦数字变成负数或零，我们开始在每个函数调用中添加 K，直到数字变成原始数字。这里我们使用一个函数进行加法和减法，但是为了在加法和减法之间切换，我们使用了一个布尔**标志**。

## C++

```
// C++ program to Print Number
// series without using loop
#include <iostream>

using namespace std;

// function print series
// using recursion
void PrintNumber(int N, int Original, int K, bool flag)
{

    // print the number
    cout << N << " ";

    // change flag if number
    // become negative
    if (N <= 0)
        flag = !flag;

    // base condition for
    // second_case (Adding K)
    if (N == Original && !flag)

        return;

    // if flag is true
    // we subtract value until
    // number is greater then zero
    if (flag == true) {

        PrintNumber(N - K, Original, K, flag);

        return;
    }

    // second case (Addition )
    if (!flag) {

        PrintNumber(N + K, Original, K, flag);

        return;
    }
}

// driver program
int main()
{

    int N = 20, K = 6;

    PrintNumber(N, N, K, true);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Print Number
// series without using loop

import java.io.*;
import java.util.*;

class GFG
{
    public static void PrintNumber(int N, int Original, int K, boolean flag)
    {

        // print the number
        System.out.print(N + " ");

        // change flag if number
        // become negative
        if (N <= 0)
            flag = !flag;

        // base condition for
        // second_case (Adding K)
        if (N == Original && !flag)

            return;

        // if flag is true
        // we subtract value until
        // number is greater then zero
        if (flag == true)
        {
            PrintNumber(N - K, Original, K, flag);
            return;
        }

        // second case (Addition )
        if (!flag)
        {
            PrintNumber(N + K, Original, K, flag);
            return;
        }
    }

    public static void main (String[] args)
    {
        int N = 20, K = 6;
        PrintNumber(N, N, K, true);
    }
}
// This code is contributed by Mohit Gupta_OMG
```

## 蟒蛇 3

```
# Python program to Print Number
# series without using loop

def PrintNumber(N, Original, K, flag):
    #print the number
    print(N, end = " ")

    # change flag if number
    # become negative

    if (N <= 0):
        if(flag==0):
            flag = 1
        else:
            flag = 0

    # base condition for
    # second_case (Adding K)

    if (N == Original and (not(flag))):
        return

    # if flag is true
    # we subtract value until
    # number is greater then zero

    if (flag == True):
        PrintNumber(N - K, Original, K, flag)
        return

    # second case (Addition )
    if (not(flag)):
        PrintNumber(N + K, Original, K, flag);
        return

N = 20
K = 6
PrintNumber(N, N, K, True)

# This code is contributed by Mohit Gupta_OMG
```

## C#

```
// C# program to Print Number
// series without using loop
using System;

public class GFG {

    // function print series
    // using recursion
    static void PrintNumber(int N,
             int Original, int K, bool flag)
    {

        // print the number
        Console.Write(N + " ");

        // change flag if number
        // become negative
        if (N <= 0)
            flag = !flag;

        // base condition for
        // second_case (Adding K)
        if (N == Original && !flag)
            return;

        // if flag is true
        // we subtract value until
        // number is greater then zero
        if (flag == true)
        {
            PrintNumber(N - K, Original, K,
                                      flag);
            return;
        }

        // second case (Addition )
        if (!flag)
        {
            PrintNumber(N + K, Original, K,
                                      flag);
            return;
        }
    }

    // driver program
    static public void Main ()
    {
        int N = 20, K = 6;

        PrintNumber(N, N, K, true);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Print Number
// series without using loop

// function print series
// using recursion
function PrintNumber($N, $Original,
                     $K, $flag)
{

    // print the number
    echo($N . " ");

    // change flag if number
    // become negative
    if ($N <= 0)
        $flag = !$flag;

    // base condition for
    // second_case (Adding K)
    if ($N == $Original && !$flag)

        return;

    // if flag is true
    // we subtract value until
    // number is greater then zero
    if ($flag == true) {

        PrintNumber($N - $K, $Original,
                         $K, $flag);

        return;
    }

    // second case (Addition )
    if (!$flag) {

        PrintNumber($N + $K, $Original,
                         $K, $flag);

        return;
    }
}

// Driver Code
$N = 20; $K = 6;

PrintNumber($N, $N, $K, true);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to Print Number
// series without using loop

// function print series
// using recursion
function PrintNumber(N, Original,
                    K, flag)
{

    // print the number
    document.write(N + " ");

    // change flag if number
    // become negative
    if (N <= 0)
        flag = !flag;

    // base condition for
    // second_case (Adding K)
    if (N == Original && !flag)

        return;

    // if flag is true
    // we subtract value until
    // number is greater then zero
    if (flag == true) {

        PrintNumber(N - K, Original,
                        K, flag);

        return;
    }

    // second case (Addition )
    if (!flag) {

        PrintNumber(N + K, Original,
                        K, flag);

        return;
    }
}

// Driver Code
let N = 20, K = 6;

PrintNumber(N, N, K, true);

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
20 14 8 2 -4 2 8 14 20 
```