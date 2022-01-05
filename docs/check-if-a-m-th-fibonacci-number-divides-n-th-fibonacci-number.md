# 检查第 M 个斐波那契数是否除以第 N 个斐波那契数

> 原文:[https://www . geesforgeks . org/check-if-a-m-th-Fibonacci-number-divides-n-th-Fibonacci-number/](https://www.geeksforgeeks.org/check-if-a-m-th-fibonacci-number-divides-n-th-fibonacci-number/)

给定两个数字 M 和 N，任务是检查第 M 个和第 N 个[斐波那契](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)数字是否完美地相互除。
**例:**

> **输入:** M = 3，N = 6
> **输出:**是
> F(3) = 2，F(6) = 8 和 F(6) % F(3) = 0
> **输入:** M = 2，N = 9
> **输出:**否

一种天真的方法是找到第 N 个和第 M 个斐波那契数，并检查它们是否完全可分。
一种**有效的方法**是使用[斐波那契属性](https://www.geeksforgeeks.org/interesting-facts-fibonacci-numbers/)来确定结果。如果 m 完美地除 n，那么 F <sub>m</sub> 也完美地除 F <sub>n</sub> ，否则就不会。
**异常:**当 N 为 2 时，总是有可能为 Fibo <sub>2</sub> 为 1，即每隔一个 Fibonacci 数除一次。
以下是上述方法的实施:

## C++

```
// C++ program to check if
// M-th fibonacci divides N-th fibonacci
#include <bits/stdc++.h>
using namespace std;

void check(int n, int m)
{
    // exceptional case for F(2)
    if (n == 2 || m == 2 || n % m == 0) {
        cout << "Yes" << endl;
    }
    // if none of the above cases,
    // hence not divisible
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    int m = 3, n = 9;
    check(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if M-th fibonacci
// divides N-th fibonacci
import java.io.*;

class GFG
{
static void check(int n, int m)
{
    // exceptional case for F(2)
    if (n == 2 || m == 2 ||
        n % m == 0)
    {
        System.out.println( "Yes");
    }

    // if none of the above cases,
    // hence not divisible
    else
    {
        System.out.println( "No");
    }
}

// Driver Code
public static void main (String[] args)
{
    int m = 3, n = 9;
    check(n, m);
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to
# check if M-th fibonacci
# divides N-th fibonacci

def check(n, m):

    # exceptional case for F(2)
    if (n == 2 or m == 2 or
        n % m == 0) :
        print( "Yes" )

    # if none of the above
    # cases, hence not divisible
    else :
        print( "No" )

# Driver Code
m = 3
n = 9
check(n, m)

# This code is contributed
# by Smitha
```

## C#

```
// C# program to check
// if M-th fibonacci
// divides N-th fibonacci
using System;

class GFG
{
static void check(int n, int m)
{
    // exceptional case for F(2)
    if (n == 2 || m == 2 ||
        n % m == 0)
    {
         Console.WriteLine( "Yes");
    }

    // if none of the above cases,
    // hence not divisible
    else
    {
        Console.WriteLine( "No");
    }
}

// Driver Code
public static void Main ()
{
    int m = 3, n = 9;
    check(n, m);
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if M-th fibonacci
// divides N-th fibonacci

function check($n, $m)
{
    // exceptional case for F(2)
    if ($n == 2 || $m == 2 ||
        $n % $m == 0)
    {
        echo "Yes" , "\n";
    }

    // if none of the above cases,
    // hence not divisible
    else
    {
        echo "No" ," \n";
    }
}

// Driver Code
$m = 3; $n = 9;
check($n, $m);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// M-th fibonacci divides N-th fibonacci

function check(n, m)
{
    // exceptional case for F(2)
    if (n == 2 || m == 2 || n % m == 0) {
        document.write("Yes" + "<br>");
    }
    // if none of the above cases,
    // hence not divisible
    else {
        document.write("No" + "<br>");
    }
}

// Driver Code

    let m = 3, n = 9;
    check(n, m);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(1)。