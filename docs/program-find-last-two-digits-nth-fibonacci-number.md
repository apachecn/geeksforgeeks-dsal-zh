# 程序查找第 n 个斐波那契数的最后两位数字

> 原文:[https://www . geesforgeks . org/program-find-最后两位数-第 n 位-斐波那契数/](https://www.geeksforgeeks.org/program-find-last-two-digits-nth-fibonacci-number/)

给定一个数字“n”，编写一个函数打印第 n 个(n 也可以是一个大数字)斐波那契数的最后两位数字。
**例:**

```
Input : n = 65
Output : 65

Input : n = 365
Output : 65
```

[推荐:请先在“<u>”上解，再进行解。</u>](https://practice.geeksforgeeks.org/problems/yeh-karo-toh-maane/0)

<u>一个**简单的解决方法**是找到第 n 个[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)并打印它的最后两位数字。但是 N 可能非常大，所以它不会工作。
A **更好的解决方案**是利用第 300 个斐波那契数后的最后两位数开始重复的事实。
1)求 m = n % 300。
2)返回第 m 个斐波那契数。</u> 

## <u>C++</u>

```
// Program to find last two digits of n-th
// Fibonacci number
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Fills f[] with first 300 fibonacci numbers
void precomput(ll f[])
{
    /* 0th and 1st number of the series are 0 and 1*/
    f[0] = 0;
    f[1] = 1;

    /* Add the previous 2 numbers in the series
       and store last two digits of result */
    for (ll i = 2; i < 300; i++)
        f[i] = (f[i-1] + f[i-2])%100;
}

// Returns last two digits of n'th Fibonacci
// Number
int findLastDigit(ll f[], int n)
{
    return f[n%300];
}

/* Driver program to test above function */
int main ()
{
    // Precomputing units digit of first 300
    // Fibonacci numbers
    ll f[300] = {0};
    precomput(f);

    ll n = 1;
    cout << findLastDigit(f, n) << endl;
    n = 61;
    cout << findLastDigit(f, n) << endl;
    n = 7;
    cout << findLastDigit(f, n) << endl;
    n = 67;
    cout << findLastDigit(f, n) << endl;
    return 0;
}
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Program to find last two digits of
// n-th Fibonacci number
import java.util.Arrays;
class GFG {

    // Fills f[] with first 300
    // fibonacci numbers
    static void precomput(long f[])
    {
        /* 0th and 1st number of the
        series are 0 and 1*/
        f[0] = 0;
        f[1] = 1;

        /* Add the previous 2 numbers in
        the series and store last two
        digits of result */
        for (int i = 2; i < 300; i++)
            f[i] = (f[i-1] + f[i-2]) % 100;
    }

    // Returns last two digits of n'th
    // Fibonacci Number
    static long findLastDigit(long f[], int n)
    {
        return (f[(n%300)]);
    }

    /* Driver program to test above function */
    public static void main (String args[])
    {
        // Precomputing units digit of
        // first 300 Fibonacci numbers
        long f[] = new long[300];
        Arrays.fill(f,0);
        precomput(f);

        int n = 1;
        System.out.println(findLastDigit(f, n));
        n = 61;
        System.out.println(findLastDigit(f, n));
        n = 7;
        System.out.println(findLastDigit(f, n));
        n = 67;
        System.out.println(findLastDigit(f, n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## <u>蟒蛇 3</u>

```
# Python code to find last two
# digits of n-th Fibonacci number

def precomput(f):

    # 0th and 1st number of the series
    # are 0 and 1
    f.append(0)
    f.append(1)

    # Add the previous 2 numbers in the series
    # and store last two digits of result
    for i in range(2,300):
        f.append((f[i-1] + f[i-2]) % 100)

# Returns last two digits of
# n'th Fibonacci Number    
def findLastDigit(f,n):
    return f[n%300]

# driver code
f = list()
precomput(f)
n = 1
print(findLastDigit(f, n))
n = 61
print(findLastDigit(f, n))
n = 7
print(findLastDigit(f, n))
n = 67
print(findLastDigit(f, n))

# This code is contributed by "Abhishek Sharma 44"
```

## <u>C#</u>

```
// Program to find last two digits of
// n-th Fibonacci number
using System;

class GFG {

    // Fills f[] with first 300
    // fibonacci numbers
    static void precomput(long []f)
    {

        /* 0th and 1st number of the
        series are 0 and 1*/
        f[0] = 0;
        f[1] = 1;

        /* Add the previous 2 numbers in
        the series and store last two
        digits of result */
        for (int i = 2; i < 300; i++)
            f[i] = (f[i-1] + f[i-2]) % 100;
    }

    // Returns last two digits of n'th
    // Fibonacci Number
    static long findLastDigit(long []f, int n)
    {
        return (f[(n % 300)]);
    }

    /* Driver program to test above function */
    public static void Main ()
    {

        // Precomputing units digit of
        // first 300 Fibonacci numbers
        long []f = new long[300];
        precomput(f);

        int n = 1;
        Console.WriteLine(findLastDigit(f, n));

        n = 61;
        Console.WriteLine(findLastDigit(f, n));

        n = 7;
        Console.WriteLine(findLastDigit(f, n));

        n = 67;
        Console.WriteLine(findLastDigit(f, n));
    }
}

// This code is contributed by anuj_67.
```

## <u>服务器端编程语言（Professional Hypertext Preprocessor 的缩写）</u>

```
<?php
// Program to find last two
// digits of n-th Fibonacci
// number

// Fills f[] with first
// 300 fibonacci numbers
function precomput()
{
    /* 0th and 1st number of
    the series are 0 and 1*/
    $f[0] = 0;
    $f[1] = 1;

    /* Add the previous 2 numbers
    in the series and store last
    two digits of result */
    for ($i = 2; $i < 300; $i++)
        $f[$i] = ($f[$i - 1] +
                  $f[$i - 2]) % 100;

    return $f;
}

// Returns last two digits
// of n'th Fibonacci Number
function findLastDigit($f, $n)
{
    return $f[$n % 300];
}

// Driver code

// Precomputing units digit
// of first 300 Fibonacci numbers
$f = precomput();

$n = 1;
echo findLastDigit($f, $n) . "\n";
$n = 61;
echo findLastDigit($f, $n) . "\n";
$n = 7;
echo findLastDigit($f, $n) . "\n";
$n = 67;
echo findLastDigit($f, $n) . "\n";

// This code is contributed by mits.
?>
```

## <u>java 描述语言</u>

```
<script>

// Program to find last two digits of n-th
// Fibonacci number

// Fills f[] with first 300 fibonacci numbers
function precomput(f)
{
    /* 0th and 1st number of the series are 0 and 1*/
    f[0] = 0;
    f[1] = 1;

    /* Add the previous 2 numbers in the series
    and store last two digits of result */
    for (let i = 2; i < 300; i++)
        f[i] = (f[i-1] + f[i-2])%100;
}

// Returns last two digits of n'th Fibonacci
// Number
function findLastDigit(f, n)
{
    return f[n%300];
}

/* Driver program to test above function */

    // Precomputing units digit of first 300
    // Fibonacci numbers
    let f = new Uint8Array(300);
    precomput(f);

    let n = 1;
    document.write(findLastDigit(f, n) + "<br>");
    n = 61;
    document.write(findLastDigit(f, n) + "<br>");
    n = 7;
    document.write(findLastDigit(f, n) + "<br>");
    n = 67;
    document.write(findLastDigit(f, n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

<u>**输出:**</u>

```
1
61
13
53
```