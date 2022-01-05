# 比较 m^n 和 n^m 的程序

> 原文:[https://www.geeksforgeeks.org/program-to-compare-mn-and-nm/](https://www.geeksforgeeks.org/program-to-compare-mn-and-nm/)

给定两个正整数 **m** 和 **n** ，任务是编写一个程序，检查 m^n 是否大于、小于或等于 n^m.
**示例:**

> 输入:m = 3，n = 10
> 输出:m^n > n^m
> 说明:大于 10^3=1000
> 的 3^10=59049 输入:m = 987654321，n = 123456987
> 输出:m^n < n^m

一种天真的方法是计算 m^n 和 n^m，当 m 和 n 非常大时会导致溢出。
一个**有效的方法**是使用**日志**解决这个问题。

> 给定 LHS = m^n 和 RHS = n^m.
> 在两边取对数后，LHS = n*log(m)和 RHS = m*log(n)
> 然后比较 LHS 和 RHS。

## C++

```
// CPP program to compare which is greater
// m^n or n^m 
#include <bits/stdc++.h>
using namespace std;

// function to compare m^n and n^m
void check(unsigned long long m, unsigned long long int n)
    {
        // m^n
        double RHS = m * (double)log(n);

        // n^m
        double LHS = n * (double)log(m);

        if ( LHS > RHS )
            cout << "m^n > n^m";

        else if ( LHS < RHS )
            cout << "m^n < n^m";

        else
            cout << "m^n = n^m";
    }

// Drivers Code
int main() {

    unsigned long long m = 987654321, n = 123456987;

    // function call to compare m^n and n^m
    check(m, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compare which
// is greater m^n or n^m
import java .io.*;

class GFG
{
// function to compare
// m^n and n^m
static void check(long m, long n)
{
    // m^n
    double RHS = m * (double)Math.log(n);

    // n^m
    double LHS = n * (double)Math.log(m);

    if (LHS > RHS)
        System.out.print("m^n > n^m");

    else if (LHS < RHS)
    System.out.print("m^n < n^m");

    else
        System.out.print("m^n = n^m");
}

// Driver Code
static public void main (String[] args)
{
    long m = 987654321, n = 123456987;

    // function call to
    // compare m^n and n^m
    check(m, n);
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to compare
# which is greater m^n or n^m
import math

# function to compare
# m^n and n^m
def check( m, n):

    # m^n
    RHS = m * math.log(n);

    # n^m
    LHS = n * math.log(m);

    if (LHS > RHS):
        print("m^n > n^m");

    elif (LHS < RHS):
        print("m^n < n^m");

    else:
        print("m^n = n^m");

# Driver Code
m = 987654321;
n = 123456987;

# function call to
# compare m^n and n^m
check(m, n);

# This code is contributed by mits
```

## C#

```
// C# program to compare which 
// is greater m^n or n^m
using System;

class GFG
{
// function to compare
// m^n and n^m
static void check(ulong m, ulong n)
{
    // m^n
    double RHS = m * (double)Math.Log(n);

    // n^m
    double LHS = n * (double)Math.Log(m);

    if (LHS > RHS)
        Console.Write("m^n > n^m");

    else if (LHS < RHS)
    Console.Write("m^n < n^m");

    else
        Console.Write("m^n = n^m");
}

// Driver Code
static public void Main ()
{
    ulong m = 987654321, n = 123456987;

    // function call to
    // compare m^n and n^m
    check(m, n);

}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compare 
// which is greater m^n or n^m

// function to compare
// m^n and n^m
function check( $m, $n)
{
    // m^n
    $RHS = $m * log($n);

    // n^m
    $LHS = $n * log($m);

    if ( $LHS > $RHS )
        echo "m^n > n^m";

    else if ( $LHS < $RHS )
    echo "m^n < n^m";

    else
        echo "m^n = n^m";
}

// Driver Code
$m = 987654321;
$n = 123456987;

// function call to
// compare m^n and n^m
check($m, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// javascript program to compare which
// is greater m^n or n^m

// function to compare
// m^n and n^m

function check( m,  n)
{
    // m^n
    var RHS = m * Math.log(n);

    // n^m
    var LHS = n * Math.log(m);

    if (LHS > RHS){
        document.write("m^n > n^m");
    }
    else if (LHS < RHS) {
    document.write("m^n < n^m");
    }

    else {
        document.write("m^n = n^m");
    }
}

// Driver Code

     var m = 987654321 ; 
     var n = 123456987;

    // function call to
    // compare m^n and n^m
    check(m, n);

</script>
```

**输出:**

```
m^n < n^m
```