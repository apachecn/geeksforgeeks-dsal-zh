# 求前 N 个奇数斐波那契数之和

> 原文:[https://www . geeksforgeeks . org/find-Fibonacci-numbers-Fibonacci-numbers-Fibonacci-numbers 之和/](https://www.geeksforgeeks.org/find-the-sum-of-first-n-odd-fibonacci-numbers/)

给定一个数，N .求前 N 个奇数斐波那契数的和。
**注**:答案可能很大，所以以 10^9+7.为模打印答案

**示例**:

```
Input : N = 3
Output : 5
Explanation : 1 + 1 + 3

Input : 6
Output : 44
Explanation : 1 + 1 + 3 + 5 + 13 + 21
```

**逼近** :
奇数斐波那契数列为:

```
1, 1, 3, 5, 13, 21, 55, 89......
```

奇数斐波那契数列的前缀和为:

```
1, 2, 5, 10, 23, 44, 99, 188.....
```

前 N 个奇数斐波那契数之和的公式为:

> a(n)= a(n-1)+4 * a(n-2)–4 * a(n-3)+a(n-4)–a(n-5)对于 n>5

下面是上述方法的实现:

## C++

```
// CPP program to Find the sum of
// first N odd Fibonacci numbers
#include <bits/stdc++.h>
using namespace std;

#define mod 1000000007

// Function to calculate sum of first
// N odd Fibonacci numbers
long long sumOddFibonacci(int n)
{
    long long Sum[n + 1];

    // base values
    Sum[0] = 0;
    Sum[1] = 1;
    Sum[2] = 2;
    Sum[3] = 5;
    Sum[4] = 10;
    Sum[5] = 23;

    for (int i = 6; i <= n; i++) {
        Sum[i] = ((Sum[i - 1] + (4 * Sum[i - 2]) % mod -
                  (4 * Sum[i - 3]) % mod + mod) % mod +
                  (Sum[i - 4] - Sum[i - 5] + mod) % mod) % mod;
    }

    return Sum[n];
}

// Driver code
int main()
{
    long long n = 6;

    cout << sumOddFibonacci(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to Find the sum of
// first N odd Fibonacci numbers

import java.io.*;

class GFG {
    static int mod =1000000007;

// Function to calculate sum of first
// N odd Fibonacci numbers
static  int sumOddFibonacci(int n)
{
     int Sum[]=new int[n + 1];

    // base values
    Sum[0] = 0;
    Sum[1] = 1;
    Sum[2] = 2;
    Sum[3] = 5;
    Sum[4] = 10;
    Sum[5] = 23;

    for (int i = 6; i <= n; i++) {
        Sum[i] = ((Sum[i - 1] + (4 * Sum[i - 2]) % mod -
                (4 * Sum[i - 3]) % mod + mod) % mod +
                (Sum[i - 4] - Sum[i - 5] + mod) % mod) % mod;
    }

    return Sum[n];
}

// Driver code

    public static void main (String[] args) {

    int n = 6;
    System.out.println(sumOddFibonacci(n));
    }
//This Code is Contributed by Sachin   
}
```

## 蟒蛇 3

```
# Python3 program to Find the sum of
# first N odd Fibonacci numbers
mod = 1000000007 ;

# Function to calculate sum of
# first N odd Fibonacci numbers
def sumOddFibonacci(n):

    Sum=[0]*(n + 1);

    # base values
    Sum[0] = 0;
    Sum[1] = 1;
    Sum[2] = 2;
    Sum[3] = 5;
    Sum[4] = 10;
    Sum[5] = 23;

    for i in range(6,n+1):
        Sum[i] = ((Sum[i - 1] +
                    (4 * Sum[i - 2]) % mod -
                    (4 * Sum[i - 3]) % mod +
                    mod) % mod + (Sum[i - 4] -
                    Sum[i - 5] + mod) % mod) % mod;

    return Sum[n];

# Driver code
n = 6;
print(sumOddFibonacci(n));

# This code is contributed by mits
```

## C#

```
// C#  program to Find the sum of
// first N odd Fibonacci numbers

using System;

public class GFG{

static int mod =1000000007;
// Function to calculate sum of first
// N odd Fibonacci numbers
static int sumOddFibonacci(int n)
{
    int []Sum=new int[n + 1];

    // base values
    Sum[0] = 0;
    Sum[1] = 1;
    Sum[2] = 2;
    Sum[3] = 5;
    Sum[4] = 10;
    Sum[5] = 23;

    for (int i = 6; i <= n; i++) {
        Sum[i] = ((Sum[i - 1] + (4 * Sum[i - 2]) % mod -
                (4 * Sum[i - 3]) % mod + mod) % mod +
                (Sum[i - 4] - Sum[i - 5] + mod) % mod) % mod;
    }

    return Sum[n];
}

// Driver code

    static public void Main (){
        int n = 6;
    Console.WriteLine(sumOddFibonacci(n));
    }
//This Code is Contributed by Sachin    
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Find the sum of
// first N odd Fibonacci numbers
$mod = 1000000007 ;

// Function to calculate sum of
// first N odd Fibonacci numbers
function sumOddFibonacci($n)
{
    global $mod;
    $Sum[$n + 1] = array();

    // base values
    $Sum[0] = 0;
    $Sum[1] = 1;
    $Sum[2] = 2;
    $Sum[3] = 5;
    $Sum[4] = 10;
    $Sum[5] = 23;

    for ($i = 6; $i <= $n; $i++)
    {
        $Sum[$i] = (($Sum[$i - 1] +
                    (4 * $Sum[$i - 2]) % $mod -
                    (4 * $Sum[$i - 3]) % $mod +
                    $mod) % $mod + ($Sum[$i - 4] -
                    $Sum[$i - 5] + $mod) % $mod) % $mod;
    }

    return $Sum[$n];
}

// Driver code
$n = 6;
echo sumOddFibonacci($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
// javascript  program to Find the sum of
// first N odd Fibonacci numbers

    var mod = 1000000007;

    // Function to calculate sum of first
    // N odd Fibonacci numbers
    function sumOddFibonacci(n) {
        var Sum = Array(n + 1).fill(0);

        // base values
        Sum[0] = 0;
        Sum[1] = 1;
        Sum[2] = 2;
        Sum[3] = 5;
        Sum[4] = 10;
        Sum[5] = 23;

        for (i = 6; i <= n; i++) {
            Sum[i] = ((Sum[i - 1] + (4 * Sum[i - 2]) % mod - (4 * Sum[i - 3]) % mod + mod) % mod
                    + (Sum[i - 4] - Sum[i - 5] + mod) % mod) % mod;
        }

        return Sum[n];
    }

    // Driver code

        var n = 6;
        document.write(sumOddFibonacci(n));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
44
```