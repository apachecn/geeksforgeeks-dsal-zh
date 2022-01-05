# 程序寻找数列 0，5，18，39，67，105，150，203 的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-the-n-term-of-series-0-5-18-39-67-105-150-203/](https://www.geeksforgeeks.org/program-to-find-the-nth-term-of-the-series-0-5-18-39-67-105-150-203/)

给定一个数字 n，任务是编写一个程序来找到下面系列的第 n 项:

> 0，5，18，39，67，105，150，203，…(N 个术语)

**例:**

```
Input: N = 4
Output: 82
For N = 4
4th Term = ( 4 * 4 * 4 - 7 * 4 + 3) 
         = 39

Input: N = 10
Output: 332
```

**方法:**本系列的广义第 n 项:

下面是需要的实现:

## C++

```
// CPP program to find the N-th term of the series:
// 0, 5, 18, 39, 67, 105, 150, 203, ...
#include <iostream>
#include <math.h>
using namespace std;

// calculate Nth term of series
int nthTerm(int n)
{
    return 4 * pow(n, 2) - 7 * n + 3;
}

// Driver code
int main()
{
    int N = 4;

    cout << nthTerm(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the N-th term of the series:
// 0, 5, 18, 39, 67, 105, 150, 203,

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// calculate Nth term of series
static int nthTerm(int n)
{
    return 4 * (int)Math.pow(n, 2) - 7 * n + 3;
}

// Driver code
public static void  main(String args[])
{
    int N = 4;

    System.out.print(nthTerm(N));
}
}
```

## 蟒蛇 3

```
# Python 3 program to find the
# N-th term of the series:
# 0, 5, 18, 39, 67, 105, 150, 203, ...

# calculate Nth term of series
def nthTerm(n):

    return 4 * pow(n, 2) - 7 * n + 3

# Driver code
N = 4

print(nthTerm(N))

# This code is contributed by ash264
```

## C#

```
// C# program to find the
// N-th term of the series:
// 0, 5, 18, 39, 67, 105, 150, 203,
using System;

class GFG
{
// calculate Nth term of series
static int nthTerm(int n)
{
    return 4 * (int)Math.Pow(n, 2) -
                        7 * n + 3;
}

// Driver code
static public void Main ()
{
    int N = 4;

    Console.Write(nthTerm(N));
}
}

// This code is contributed by Raj
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// N-th term of the series:
// 0, 5, 18, 39, 67, 105, 150, 203, ...

// calculate Nth term of series
function nthTerm($n)
{
    return 4 * pow($n, 2) -
           7 * $n + 3;
}

// Driver code
$N = 4;

echo nthTerm($N);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the N-th term of the series:
// 0, 5, 18, 39, 67, 105, 150, 203, ...

// calculate Nth term of series
function nthTerm( n)
{
    return 4 * Math.pow(n, 2) - 7 * n + 3;
}
// driver code
  // declaration of number of terms
   let N = 4;
   document.write( nthTerm(N) );

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
39
```

**时间复杂度:** O(1)