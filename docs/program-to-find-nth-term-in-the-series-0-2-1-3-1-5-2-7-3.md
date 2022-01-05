# 程序寻找数列 0，2，1，3，1，5，2，7，3 中的第 n 项，…

> 原文:[https://www . geesforgeks . org/program-to-find-n-term-in-series-0-2-1-3-1-5-2-7-3/](https://www.geeksforgeeks.org/program-to-find-nth-term-in-the-series-0-2-1-3-1-5-2-7-3/)

给定一个数字 N，任务是编写一个程序来寻找下面系列中的第 N 项:

> **0、2、1、3、1、5、2、7、3、…**

**例:**

```
Input: N = 5
Output: 1

Input: N = 10
Output: 11
```

仔细看系列，发现系列是 2 个系列的混合:

1.  给定数列中奇数位置的项构成斐波那契数列。
2.  给定数列中偶数位置的项构成一系列素数。

现在，要解决上面给出的问题，首先检查输入的数字 N 是偶数还是奇数。

*   如果是奇数，设置 N=(N/2) + 1(因为有两个系列并行运行)并找到第 [N <sup>个</sup>斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。
*   如果 N 为偶数，只需设置 N=N/2，求[第 N 个素数](https://www.geeksforgeeks.org/prime-numbers/)。

以下是上述方法的实现:

## C++

```
// CPP program to find N-th term
// in the series
#include<bits/stdc++.h>
#define MAX 1000
using namespace std;

// Function to find Nth Prime Number
int NthPrime(int n)
{
    int count = 0;
    for (int i = 2; i <= MAX; i++) {
        int check = 0;
        for (int j = 2; j <= sqrt(i); j++) {
            if (i % j == 0) {
                check = 1;
                break;
            }
        }
        if (check == 0)
            count++;

        if (count == n) {
            return i;
            break;
        }
    }
}

// Function to find Nth Fibonacci Number
int NthFib(int n)
{
    // Declare an array to store
    // Fibonacci numbers.
    int f[n + 2];
    int i;

    // 0th and 1st number of the
    // series are 0 and 1
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {
        f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Function to find N-th term
// in the series
void findNthTerm(int n)
{
    // If n is even
    if (n % 2 == 0) {
        n = n / 2;
        n = NthPrime(n);
        cout << n << endl;
    }

    // If n is odd
    else {
        n = (n / 2) + 1;
        n = NthFib(n - 1);
        cout << n << endl;
    }
}

// Driver code
int main()
{
    int X = 5;
    findNthTerm(X);

    X = 10;
    findNthTerm(X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find N-th
// term in the series
class GFG
{

static int MAX = 1000;

// Function to find Nth Prime Number
static int NthPrime(int n)
{
int count = 0;
int i;
for (i = 2; i <= MAX; i++)
{
    int check = 0;
    for (int j = 2; j <= Math.sqrt(i); j++)
    {
        if (i % j == 0)
        {
            check = 1;
            break;
        }
    }
    if (check == 0)
        count++;

    if (count == n)
    {
        return i;

    }
}
    return 0;
}

// Function to find Nth Fibonacci Number
static int NthFib(int n)
{
// Declare an array to store
// Fibonacci numbers.
int []f = new int[n + 2];
int i;

// 0th and 1st number of the
// series are 0 and 1
f[0] = 0;
f[1] = 1;

for (i = 2; i <= n; i++)
{
    f[i] = f[i - 1] + f[i - 2];
}

return f[n];
}

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
// If n is even
if (n % 2 == 0)
{
    n = n / 2;
    n = NthPrime(n);
    System.out.println(n);
}

// If n is odd
else
{
    n = (n / 2) + 1;
    n = NthFib(n - 1);
    System.out.println(n);
}
}

// Driver code
public static void main(String[] args)
{
    int X = 5;
    findNthTerm(X);

    X = 10;
    findNthTerm(X);
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find N-th
# term in the series

# import sqrt method from math module
from math import sqrt

# Globally declare constant value
MAX = 1000

# Function to find Nth Prime Number
def NthPrime(n) :

    count = 0
    for i in range(2, MAX + 1) :

        check = 0
        for j in range(2, int(sqrt(i)) + 1) :

            if i % j == 0 :
                check = 1
                break

        if check == 0 :
            count += 1

        if count == n :
            return i
            break

# Function to find Nth Fibonacci Number
def NthFib(n) :

    # Create a list of size n+2
    # to store Fibonacci numbers.
    f = [0] * (n + 2)

    # 0th and 1st number of the
    # series are 0 and 1
    f[0], f[1] = 0, 1

    for i in range(2, n + 1) :

        f[i] = f[i - 1] + f[i - 2]

    return f[n]

# Function to find N-th
# term in the series
def findNthTerm(n) :

    # If n is even
    if n % 2 == 0 :
        n //= 2
        n = NthPrime(n)
        print(n)

    # If n is odd
    else :
        n = (n // 2) + 1
        n = NthFib(n - 1)
        print(n)

# Driver code
if __name__ == "__main__" :

    X = 5

    # function calling
    findNthTerm(X)

    X = 10
    findNthTerm(X)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find N-th term
// in the series
using System;

class GFG
{
static int MAX = 1000;

// Function to find Nth Prime Number
static int NthPrime(int n)
{
int count = 0;
int i;
for ( i = 2; i <= MAX; i++)
{
    int check = 0;
    for (int j = 2; j <= Math.Sqrt(i); j++)
    {
        if (i % j == 0)
        {
            check = 1;
            break;
        }
    }
    if (check == 0)
        count++;

    if (count == n)
    {
        return i;
    }
}
    return 0;
}

// Function to find Nth Fibonacci Number
static int NthFib(int n)
{

// Declare an array to store
// Fibonacci numbers.
int []f = new int[n + 2];
int i;

// 0th and 1st number of the
// series are 0 and 1
f[0] = 0;
f[1] = 1;

for (i = 2; i <= n; i++)
{
    f[i] = f[i - 1] + f[i - 2];
}

return f[n];
}

// Function to find N-th term
// in the series
static void findNthTerm(int n)
{
// If n is even
if (n % 2 == 0)
{
    n = n / 2;
    n = NthPrime(n);
    Console.WriteLine(n);
}

// If n is odd
else
{
    n = (n / 2) + 1;
    n = NthFib(n - 1);
    Console.WriteLine(n);
}
}

// Driver code
public static void Main()
{
    int X = 5;
    findNthTerm(X);

    X = 10;
    findNthTerm(X);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// N-th term in the series
$MAX = 1000;

// Function to find
// Nth Prime Number
function NthPrime($n)
{
    global $MAX;
    $count = 0;
    for ($i = 2; $i <= $MAX; $i++)
    {
        $check = 0;
        for ($j = 2;
             $j <= sqrt($i); $j++)
        {
            if ($i % $j == 0)
            {
                $check = 1;
                break;
            }
        }
        if ($check == 0)
            $count++;

        if ($count == $n)
        {
            return $i;
            break;
        }
    }
}

// Function to find
// Nth Fibonacci Number
function NthFib($n)
{
    // Declare an array to store
    // Fibonacci numbers.
    $f = array($n + 2);

    // 0th and 1st number of
    // the series are 0 and 1
    $f[0] = 0;
    $f[1] = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        $f[$i] = $f[$i - 1] +
                 $f[$i - 2];
    }

    return $f[$n];
}

// Function to find N-th
// term in the series
function findNthTerm($n)
{
    // If n is even
    if ($n % 2 == 0)
    {
        $n = $n / 2;
        $n = NthPrime($n);
        echo $n . "\n";
    }

    // If n is odd
    else
    {
        $n = ($n / 2) + 1;
        $n = NthFib($n - 1);
        echo $n . "\n";
    }
}

// Driver code
$X = 5;
findNthTerm($X);

$X = 10;
findNthTerm($X);

// This Code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find N-th term
// in the series

let  MAX =1000;
// Function to find Nth Prime Number
function NthPrime( n)
{
    let count = 0;
    for (let i = 2; i <= MAX; i++) {
        let check = 0;
        for (let j = 2; j <= Math.sqrt(i); j++) {
            if (i % j == 0) {
                check = 1;
                break;
            }
        }
        if (check == 0)
            count++;

        if (count == n) {
            return i;
            break;
        }
    }
}

// Function to find Nth Fibonacci Number
function NthFib( n)
{
    // Declare an array to store
    // Fibonacci numbers.
    var f=new Int16Array(n+2).fill(0);

    let i;

    // 0th and 1st number of the
    // series are 0 and 1
    f[0] = 0;
    f[1] = 1;

    for (i = 2; i <= n; i++) {
        f[i] = f[i - 1] + f[i - 2];
    }

    return f[n];
}

// Function to find N-th term
// in the series
function findNthTerm( n)
{
    // If n is even
    if (n % 2 == 0) {
        n = n / 2;
        n = NthPrime(n);
        document.write(n +"<br/>");
    }

    // If n is odd
    else {
        n = parseInt(n / 2) + 1;
        n = NthFib(n - 1);
        document.write(n +"<br/>");
    }
}

// Driver code

    let X = 5;
    findNthTerm(X);

    X = 10;
    findNthTerm(X);

// This code contributed by aashish1995

</script>
```

**Output:** 

```
1
11
```