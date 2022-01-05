# 两个阶乘乘积中 0 的尾随数

> 原文:[https://www . geesforgeks . org/trading-number-0s-product-two-factories/](https://www.geeksforgeeks.org/trailing-number-0s-product-two-factorials/)

给定两个整数 N 或 M，求阶乘乘积(N！*M！)?
示例:

```
Input : N = 4, M = 5 
Output :  1
Explanation : 4! = 24, 5! = 120
Product has only 1 trailing 0.

Input : N = 127!, M = 57!
Output : 44
```

如[中所讨论的，N 中的零数！](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)可以通过递归地将 N 除以 5，然后将商相加来计算。

> 比如 N = 127，那么
> 127 中的 0 数！= 127/5+127/25+127/125+127/625
> = 25+5+1+0

N 中的 0 个数！= 31.同样，对于 M，我们可以计算并相加两者。
所以，通过以上我们可以得出 N 中零的个数！*M！等于 N 中零的个数之和！还有 M！。

> f(N) =楼层(n/5)+floor(n/5^2)+…floor(n/5^3)+…
> f(m)=楼层(x/5)+floor(m/5^2)+…floor(m/5^3)+…
> 那么答案是 f(N)+f(M)

## C++

```
// CPP program for count number of trailing zeros
// in N! * M!
#include <iostream>
using namespace std;

// Returns number of zeros in factorial n
int trailingZero(int x)
{
    // dividing x by powers of 5 and update count
    int i = 5, count = 0;
    while (x > i) {
        count = count + x / i;
        i = i * 5;
    }
    return count;
}

// Returns count of trailing zeros in M! x N!
int countProductTrailing(int M, int N)
{
   return trailingZero(N) + trailingZero(M);
}

// Driver program
int main()
{
    int N = 67, M = 98;
    cout << countProductTrailing(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for count number
// of trailing zeros in N! * M!
import java.io.*;

class GFG {

    // Returns number of zeros in factorial n
    static int trailingZero(int x)
    {
        // dividing x by powers
        // of 5 and update count
        int i = 5, count = 0;

        while (x > i) {

            count = count + x / i;
            i = i * 5;
        }
        return count;
    }

    // Returns count of trailing zeros in M! x N!
    static int countProductTrailing(int M, int N)
    {
    return trailingZero(N) + trailingZero(M);
    }

    // Driver program
    public static void main(String args[])
    {
        int N = 67, M = 98;
        System.out.println(countProductTrailing(N, M));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program for count
# number of trailing zeros
# in N ! * M !

# Returns number of zeros in
# factorial n
def trailingZero(x) :

    # Dividing x by powers of 5
    # and update count
    i = 5
    count = 0

    while (x > i) :
        count = count + x // i
        i = i * 5

    return count

# Returns count of trailing
# zeros in M ! x N !
def countProductTrailing(M, N) :
    return trailingZero(N) + trailingZero(M)

# Driver program
N = 67
M = 98
print(countProductTrailing(N, M))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Java program for count number
// of trailing zeros in N! * M!
using System;

class GFG {

    // Returns number of zeros in factorial n
    static int trailingZero(int x)
    {
        // dividing x by powers
        // of 5 and update count
        int i = 5, count = 0;

        while (x > i) {

            count = count + x / i;
            i = i * 5;
        }
        return count;
    }

    // Returns count of trailing zeros in M! x N!
    static int countProductTrailing(int M, int N)
    {
    return trailingZero(N) + trailingZero(M);
    }

    // Driver program
    public static void Main()
    {
        int N = 67, M = 98;
        Console.WriteLine(countProductTrailing(N, M));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for count number
// of trailing zeros in N! * M!

// Returns number of
// zeros in factorial n
function trailingZero($x)
{

    // dividing x by powers of
    // 5 and update count
    $i = 5; $count = 0;
    while ($x > $i)
    {
        $count = $count + (int)($x / $i);
        $i = $i * 5;
    }
    return $count;
}

// Returns count of trailing
// zeros in M! x N!
function countProductTrailing($M, $N)
{
    return trailingZero($N) + trailingZero($M);
}

// Driver Code
$N = 67; $M = 98;
echo(countProductTrailing($N, $M));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program for count number
// of trailing zeros in N! * M!

// Returns number of
// zeros in factorial n
function trailingZero(x)
{

    // dividing x by powers of
    // 5 and update count
    let i = 5;
    let count = 0;
    while (x > i)
    {
        count = count + parseInt(x / i);
        i = i * 5;
    }
    return count;
}

// Returns count of trailing
// zeros in M! x N!
function countProductTrailing(M, N)
{
    return trailingZero(N) + trailingZero(M);
}

// Driver Code
let N = 67;
let M = 98;
document.write(countProductTrailing(N, M));

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
 37
```