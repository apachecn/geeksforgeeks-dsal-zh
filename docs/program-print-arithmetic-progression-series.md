# 程序打印等差数列

> 原文:[https://www . geesforgeks . org/program-print-算术-级数-series/](https://www.geeksforgeeks.org/program-print-arithmetic-progression-series/)

给定算术级数的第一项(a)、公共差(d)和整数 n，任务是打印级数。
**例:**

```
Input : a = 5, d = 2, n = 10
Output : 5 7 9 11 13 15 17 19 21 23
```

**进场:**

> 我们知道等差数列就像= 2，5，8，11，14。…
> 在本系列中，2 是该系列的陈述性术语。
> 公差= 5–2 = 3(系列中的公差)。
> 所以我们可以把级数写成:
> t1 = a1
> T2 = a1+(2-1)* d
> T3 = a1+(3-1)* d
> 。
> 。
> 。
> tn = a1 + (n-1) * d

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP Program to print an arithmetic
// progression series
#include <bits/stdc++.h>
using namespace std;

void printAP(int a, int d, int n)
{

// Printing AP by simply adding d
// to previous term.
int curr_term;
curr_term=a;
for (int i = 1; i <= n; i++)
{   cout << curr_term << " ";
    curr_term =curr_term + d;

}
}

// Driver code
int main()
{
    // starting number   
    int a = 2;

    // Common difference
    int d = 1;

    // N th term to be find
    int n = 5;

    printAP(a, d, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print an arithmetic
// progression series
class GFG
{
static void printAP(int a, int d, int n)
{

    // Printing AP by simply adding d
    // to previous term.
    int curr_term;
curr_term=a;
    for (int i = 1; i <= n; i++)
    { System.out.print(curr_term + " ");
    curr_term =curr_term + d;

    }
}

// Driver code
public static void main(String[] args)
{
// starting number
int a = 2;

// Common difference
int d = 1;

// N th term to be find
int n = 5;

printAP(a, d, n);
}
}
// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 Program to
# print an arithmetic
# progression series
def printAP(a,d,n):

      # Printing AP by simply adding d
      # to previous term.
      curr_term
curr_term=a

      for i in range(1,n+1):
print(curr_term, end=' ')
         curr_term =curr_term + d

# Driver code
a = 2    # starting number
d = 1    # Common difference
n = 5    # N th term to be find

printAP(a, d, n)

# This code is contributed
# by Azkia Anam.
```

## C#

```
// C# Program to print an arithmetic
// progression series
using System;

class GFG
{
    static void printAP(int a, int d, int n)
    {
        // Printing AP by simply adding
        // d to previous term.
        int curr_term;
curr_term=a;
        for (int i = 1; i <= n; i++)
            {
Console.Write(curr_term + " ");            
curr_term += d;

            }
    }

    // Driver code
    public static void Main()
    {
        // starting number
        int a = 2;

        // Common difference
        int d = 1;

        // N th term to be find
        int n = 5;

        printAP(a, d, n);
    }
}
// This code is contributed by vgt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print an arithmetic
// progression series

function printAP($a, $d, $n)
{

    // Printing AP by simply adding d
    // to previous term.
    $curr_term;
$curr_term=a;
    for ($i = 1; $i <= $n; $i++)
    {     echo($curr_term . " ");
        $curr_term += $d;

    }
}

// Driver code

// starting number
$a = 2;

// Common difference
$d = 1;

// N th term to be find
$n = 5;

printAP($a, $d, $n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to print an arithmetic 
// progression series

    function printAP(a, d, n)
    {

        // Printing AP by simply adding d
        // to previous term.
        let curr_term;
        curr_term=a;
        for (let i = 1; i <= n; i++)
        {   document.write(curr_term + " ");
            curr_term =curr_term + d;

        }
    }

    // Driver code

    // starting number    
    let a = 2; 

    // Common difference
    let d = 1; 

    // N th term to be find
    let n = 5; 

    printAP(a, d, n);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
2 3 4 5 6
```