# 交替斐波那契数

> 原文:[https://www.geeksforgeeks.org/alternate-fibonacci-numbers/](https://www.geeksforgeeks.org/alternate-fibonacci-numbers/)

给出一个数字 N，打印交替的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到第 N 个斐波那契。

**示例:**

```
Input :  N = 7
Output : 0 1 3 8 

Input  : N = 15
Output : 0 1 3 8 21 55 144 377 
```

阅读下面文章中的**方法 2**:[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)

**逼近:**采用**动态规划**逼近。继续存储先前计算的斐波那契数，并使用前两个来存储下一个斐波那契数。

## C++

```
// Alternate Fibonacci Series using Dynamic Programming
#include <bits/stdc++.h>
using namespace std;

void alternateFib(int n)
{
    if (n < 0)
      return;

    /* 0th and 1st number of the series are 0 and 1*/
    int f1 = 0;
    int f2 = 1;

    cout << f1 << " ";
    for (int i = 2; i <= n; i++) {
         int f3 = f2 + f1;

         if (i % 2 == 0)
            cout << f3 << " ";

         f1 = f2;
         f2 = f3;
    }
}

int main()
{
    int N = 15;
    alternateFib(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Alternate Fibonacci Series
// using Dynamic Programming
import java.io.*;

class GFG
{
static void alternateFib(int n)
{
    if (n < 0)
    return;

    /* 0th and 1st number of the
       series are 0 and 1*/
    int f1 = 0;
    int f2 = 1;

    System.out.print(f1 + " ");
    for (int i = 2; i <= n; i++)
    {
        int f3 = f2 + f1;

        if (i % 2 == 0)
            System.out.print(f3 + " ");

        f1 = f2;
        f2 = f3;
    }
}

// Driver Code
public static void main (String[] args)
{
    int N = 15;
    alternateFib(N);
}
}

// This code is contributed
// by chandan_jnu.
```

## 蟒蛇 3

```
# Alternate Fibonacci Series
# using Dynamic Programming
def alternateFib(n):
    if (n < 0):
        return -1;

    # 0th and 1st number of
    # the series are 0 and 1
    f1 = 0;
    f2 = 1;

    print(f1, end = " ");
    for i in range(2, n + 1):
        f3 = f2 + f1;

        if (i % 2 == 0):
            print(f3, end = " ");

        f1 = f2;
        f2 = f3;

# Driver Code
N = 15;
alternateFib(N);

# This code is contributed by mits
```

## C#

```
// Alternate Fibonacci Series
// using Dynamic Programming
using System;

class GFG
{
static void alternateFib(int n)
{
    if (n < 0)
    return;

    /* 0th and 1st number of
    the series are 0 and 1*/
    int f1 = 0;
    int f2 = 1;

    Console.Write(f1 + " ");
    for (int i = 2; i <= n; i++)
    {
        int f3 = f2 + f1;

        if (i % 2 == 0)
            Console.Write(f3 + " ");

        f1 = f2;
        f2 = f3;
    }
}

// Driver Code
public static void Main ()
{
    int N = 15;
    alternateFib(N);
}
}

// This code is contributed
// by chandan_jnu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Alternate Fibonacci Series
// using Dynamic Programming
function alternateFib($n)
{
    if ($n < 0)
    return;

    /* 0th and 1st number of
    the series are 0 and 1*/
    $f1 = 0;
    $f2 = 1;

    echo $f1 . " ";
    for ($i = 2; $i <= $n; $i++)
    {
        $f3 = $f2 + $f1;

        if ($i % 2 == 0)
            echo $f3 . " ";

        $f1 = $f2;
        $f2 = $f3;
    }
}

// Driver Code
$N = 15;
alternateFib($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Alternate Fibonacci Series
// using Dynamic Programming
function alternateFib(n)
{
    if (n < 0)
        return;

    // 0th and 1st number of the
    // series are 0 and 1
    var f1 = 0;
    var f2 = 1;

    document.write(f1 + " ");
    for(i = 2; i <= n; i++)
    {
        var f3 = f2 + f1;

        if (i % 2 == 0)
            document.write(f3 + " ");

        f1 = f2;
        f2 = f3;
    }
}

// Driver Code
var N = 15;

alternateFib(N);

// This code is contributed by gauravrajput1

</script>
```

**Output:** 

```
0 1 3 8 21 55 144 377
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)