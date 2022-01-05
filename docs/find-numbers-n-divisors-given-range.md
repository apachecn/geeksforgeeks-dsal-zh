# 找出给定范围内有 n 因子的数

> 原文:[https://www . geesforgeks . org/find-numbers-n-除数-给定范围/](https://www.geeksforgeeks.org/find-numbers-n-divisors-given-range/)

给定三个整数 a，b，n，你的任务是打印 a 和 b 之间的数，包括它们也有 n 个除数。如果一个数总共有 n 个除数，包括 1 和它自己，那么这个数叫做 n 除数。
**例:**

```
Input  : a = 1, b = 7, n = 2
Output : 4
There are four numbers with 2 divisors in 
range [1, 7]. The numbers are 2, 3, 5, and 7.
```

**天真的方法:**
天真的方法是检查 a 和 b 之间的所有数字，其中有多少是 n 除数这样做[找出每个数字的每个除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)。如果它等于 n，那么它就是一个 n 除数
**有效方法:**
任何数都可以用它的素因子分解的形式写成，让这个数是 x 和 p1，p2..pm 是除以 x 的质数，所以 x = P1<sup>E1</sup>* p2<sup>E2</sup>…。pm <sup>em</sup> 其中 e1，e2…em 是素数 p1，p2…pm 的指数，所以 x 的除数将是(E1+1)*(E2+1)……*(em+1)。
现在第二个观察是对于大于 sqrt(x)的素数，它们的指数不能超过 1。让我们通过矛盾来证明这一点假设在 x 的素分解中有一个大于 sqrt(x)的素数 p，它的指数 e 大于 1(e>= 2)所以 P^E sqrt(x)所以 P^E > (sqrt(x)) <sup>E</sup> 和 E > = 2 所以 P <sup>E</sup> 将总是大于 x
第三个观察是在 x 的素分解中大于 sqrt(x)的素数将总是这也可以用上述矛盾来类似地证明。
现在来解决这个问题
**第一步:**应用[筛埃拉托斯特尼](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)计算素数直到 sqrt(b)。
**第二步:**遍历从 a 到 b 的每个数，通过重复将该数除以素数并使用公式 number of disors(x)=(E1+1)*(E2+1)…，计算该数中每个素数的指数。(em+1)。
**第三步:**如果除以小于等于该数平方根的所有素数后，如果数>为 1，这意味着有一个大于其平方根的素数被除，其指数将始终为 1，如上所述。

## C++

```
// C++ program to count numbers with n divisors
#include<bits/stdc++.h>
using namespace std;

// applying sieve of eratosthenes
void sieve(bool primes[], int x)
{
    primes[1] = false;

    // if a number is prime mark all its multiples
    // as non prime
    for (int i=2; i*i <= x; i++)
    {
        if (primes[i] == true)
        {
            for (int j=2; j*i <= x; j++)
                primes[i*j] = false;
        }
    }
}

// function that returns numbers of number that have
// n divisors in range from a to b. x is sqrt(b) + 1.
int nDivisors(bool primes[], int x, int a, int b, int n)
{
    // result holds number of numbers having n divisors
    int result = 0;

    // vector to hold all the prime numbers between 1
    // ans sqrt(b)
    vector <int> v;
    for (int i = 2; i <= x; i++)
        if (primes[i] == true)
            v.push_back (i);

    // Traversing all numbers in given range
    for (int i=a; i<=b; i++)
    {
        // initialising temp as i
        int temp = i;

        // total holds the number of divisors of i
        int total = 1;
        int j = 0;

        // we need to use that prime numbers that
        // are less than equal to sqrt(temp)
        for (int k = v[j]; k*k <= temp; k = v[++j])
        {
            // holds the exponent of k in prime
            // factorization of i
            int count = 0;

            // repeatedly divide temp by k till it is
            // divisible and accordingly increase count
            while (temp%k == 0)
            {
                count++;
                temp = temp/k;
            }

            // using the formula  no.of divisors =
            // (e1+1)*(e2+1)....
            total = total*(count+1);
        }

        // if temp is not equal to 1 then there is
        // prime number in prime factorization of i
        // greater than sqrt(i)
        if (temp != 1)
            total = total*2;

        // if i is a ndvisor number increase result
        if (total == n)
            result++;
    }
    return result;
}

// Returns count of numbers in [a..b] having
// n divisors.
int countNDivisors(int a, int b, int n)
{
    int x = sqrt(b) + 1;

    // primes[i] = true if i is a prime number
    bool primes[x];

    // initialising each number as prime
    memset(primes, true, sizeof(primes));
    sieve(primes, x);

    return nDivisors(primes, x, a, b, n);
}

// driver code
int main()
{
    int a = 1, b = 7, n = 2;
    cout << countNDivisors(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers with n divisors
import java.util.*;

class GFG{
// applying sieve of eratosthenes
static void sieve(boolean[] primes, int x)
{
    primes[1] = true;

    // if a number is prime mark all its multiples
    // as non prime
    for (int i=2; i*i <= x; i++)
    {
        if (primes[i] == false)
        {
            for (int j=2; j*i <= x; j++)
                primes[i*j] = true;
        }
    }
}

// function that returns numbers of number that have
// n divisors in range from a to b. x is sqrt(b) + 1.
static int nDivisors(boolean[] primes, int x, int a, int b, int n)
{
    // result holds number of numbers having n divisors
    int result = 0;

    // vector to hold all the prime numbers between 1
    // ans sqrt(b)
    ArrayList<Integer> v=new ArrayList<Integer>();
    for (int i = 2; i <= x; i++)
        if (primes[i] == false)
            v.add(i);

    // Traversing all numbers in given range
    for (int i=a; i<=b; i++)
    {
        // initialising temp as i
        int temp = i;

        // total holds the number of divisors of i
        int total = 1;
        int j = 0;

        // we need to use that prime numbers that
        // are less than equal to sqrt(temp)
        for (int k = v.get(j); k*k <= temp; k = v.get(++j))
        {
            // holds the exponent of k in prime
            // factorization of i
            int count = 0;

            // repeatedly divide temp by k till it is
            // divisible and accordingly increase count
            while (temp%k == 0)
            {
                count++;
                temp = temp/k;
            }

            // using the formula no.of divisors =
            // (e1+1)*(e2+1)....
            total = total*(count+1);

        }

        // if temp is not equal to 1 then there is
        // prime number in prime factorization of i
        // greater than sqrt(i)
        if (temp != 1)
            total = total*2;

        // if i is a ndvisor number increase result
        if (total == n)
            result++;
    }
    return result;
}

// Returns count of numbers in [a..b] having
// n divisors.
static int countNDivisors(int a, int b, int n)
{
    int x = (int)Math.sqrt(b) + 1;

    // primes[i] = true if i is a prime number
    boolean[] primes=new boolean[x+1];

    // initialising each number as prime
    sieve(primes, x);

    return nDivisors(primes, x, a, b, n);
}

// driver code
public static void main(String[] args)
{
    int a = 1, b = 7, n = 2;
    System.out.println(countNDivisors(a, b, n));

}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to count numbers
# with n divisors
import math;

# applying sieve of eratosthenes
def sieve(primes, x):
    primes[1] = False;

    # if a number is prime mark all
    # its multiples as non prime
    i = 2;
    while (i * i <= x):
        if (primes[i] == True):
            j = 2;
            while (j * i <= x):
                primes[i * j] = False;
                j += 1;
        i += 1;

# function that returns numbers of number
# that have n divisors in range from a to b.
# x is sqrt(b) + 1.
def nDivisors(primes, x, a, b, n):

    # result holds number of numbers
    # having n divisors
    result = 0;

    # vector to hold all the prime
    # numbers between 1 and sqrt(b)
    v = [];
    for i in range(2, x + 1):
        if (primes[i]):
            v.append(i);

    # Traversing all numbers in given range
    for i in range(a, b + 1):

        # initialising temp as i
        temp = i;

        # total holds the number of
        # divisors of i
        total = 1;
        j = 0;

        # we need to use that prime numbers that
        # are less than equal to sqrt(temp)
        k = v[j];
        while (k * k <= temp):

            # holds the exponent of k in prime
            # factorization of i
            count = 0;

            # repeatedly divide temp by k till it is
            # divisible and accordingly increase count
            while (temp % k == 0):
                count += 1;
                temp = int(temp / k);

            # using the formula no.of divisors =
            # (e1+1)*(e2+1)....
            total = total * (count + 1);
            j += 1;
            k = v[j];

        # if temp is not equal to 1 then there is
        # prime number in prime factorization of i
        # greater than sqrt(i)
        if (temp != 1):
            total = total * 2;

        # if i is a ndivisor number
        # increase result
        if (total == n):
            result += 1;
    return result;

# Returns count of numbers in [a..b]
# having n divisors.
def countNDivisors(a, b, n):
    x = int(math.sqrt(b) + 1);

    # primes[i] = true if i is a prime number
    # initialising each number as prime
    primes = [True] * (x + 1);
    sieve(primes, x);

    return nDivisors(primes, x, a, b, n);

# Driver code
a = 1;
b = 7;
n = 2;
print(countNDivisors(a, b, n));

# This code is contributed by mits
```

## C#

```
// C# program to count numbers with n divisors
using System.Collections;
using System;
class GFG{
// applying sieve of eratosthenes
static void sieve(bool[] primes, int x)
{
    primes[1] = true;

    // if a number is prime mark all its multiples
    // as non prime
    for (int i=2; i*i <= x; i++)
    {
        if (primes[i] == false)
        {
            for (int j=2; j*i <= x; j++)
                primes[i*j] = true;
        }
    }
}

// function that returns numbers of number that have
// n divisors in range from a to b. x is sqrt(b) + 1.
static int nDivisors(bool[] primes, int x, int a, int b, int n)
{
    // result holds number of numbers having n divisors
    int result = 0;

    // vector to hold all the prime numbers between 1
    // ans sqrt(b)
    ArrayList v=new ArrayList();
    for (int i = 2; i <= x; i++)
        if (primes[i] == false)
            v.Add(i);

    // Traversing all numbers in given range
    for (int i=a; i<=b; i++)
    {
        // initialising temp as i
        int temp = i;

        // total holds the number of divisors of i
        int total = 1;
        int j = 0;

        // we need to use that prime numbers that
        // are less than equal to sqrt(temp)
        for (int k = (int)v[j]; k*k <= temp; k = (int)v[++j])
        {
            // holds the exponent of k in prime
            // factorization of i
            int count = 0;

            // repeatedly divide temp by k till it is
            // divisible and accordingly increase count
            while (temp%k == 0)
            {
                count++;
                temp = temp/k;
            }

            // using the formula no.of divisors =
            // (e1+1)*(e2+1)....
            total = total*(count+1);

        }

        // if temp is not equal to 1 then there is
        // prime number in prime factorization of i
        // greater than sqrt(i)
        if (temp != 1)
            total = total*2;

        // if i is a ndivisor number increase result
        if (total == n)
            result++;
    }
    return result;
}

// Returns count of numbers in [a..b] having
// n divisors.
static int countNDivisors(int a, int b, int n)
{
    int x = (int)Math.Sqrt(b) + 1;

    // primes[i] = true if i is a prime number
    bool[] primes=new bool[x+1];

    // initialising each number as prime
    sieve(primes, x);

    return nDivisors(primes, x, a, b, n);
}

// driver code
public static void Main()
{
    int a = 1, b = 7, n = 2;
    Console.WriteLine(countNDivisors(a, b, n));

}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers with n divisors

// applying sieve of eratosthenes
function sieve(&$primes, $x)
{
    $primes[1] = false;

    // if a number is prime mark all
    // its multiples as non prime
    for ($i = 2; $i * $i <= $x; $i++)
    {
        if ($primes[$i] == true)
        {
            for ($j = 2; $j * $i <= $x; $j++)
                $primes[$i * $j] = false;
        }
    }
}

// function that returns numbers of number
// that have n divisors in range from a to
// b. x is sqrt(b) + 1.
function nDivisors($primes, $x, $a, $b, $n)
{
    // result holds number of numbers
    // having n divisors
    $result = 0;

    // vector to hold all the prime numbers
    // between 1 ans sqrt(b)
    $v = array();
    for ($i = 2; $i <= $x; $i++)
        if ($primes[$i] == true)
            array_push($v, $i);

    // Traversing all numbers in given range
    for ($i = $a; $i <= $b; $i++)
    {
        // initialising temp as i
        $temp = $i;

        // total holds the number of
        // divisors of i
        $total = 1;
        $j = 0;

        // we need to use that prime numbers that
        // are less than equal to sqrt(temp)
        for ($k = $v[$j];
             $k * $k <= $temp; $k = $v[++$j])
        {
            // holds the exponent of k in
            // prime factorization of i
            $count = 0;

            // repeatedly divide temp by k till
            // it is divisible and accordingly
            // increase count
            while ($temp % $k == 0)
            {
                $count++;
                $temp = (int)($temp / $k);
            }

            // using the formula no.of divisors =
            // (e1+1)*(e2+1)....
            $total = $total * ($count + 1);
        }

        // if temp is not equal to 1 then there is
        // prime number in prime factorization of i
        // greater than sqrt(i)
        if ($temp != 1)
            $total = $total * 2;

        // if i is a n divisor number increase result
        if ($total == $n)
            $result++;
    }
    return $result;
}

// Returns count of numbers in [a..b]
// having n divisors.
function countNDivisors($a, $b, $n)
{
    $x = (int)(sqrt($b) + 1);

    // primes[i] = true if i is a prime number
    // initialising each number as prime
    $primes = array_fill(0, $x + 1, true);
    sieve($primes, $x);

    return nDivisors($primes, $x, $a, $b, $n);
}

// Driver code
$a = 1;
$b = 7;
$n = 2;
print(countNDivisors($a, $b, $n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to count numbers with n divisors

// applying sieve of eratosthenes
function sieve(primes, x)
{
    primes[1] = true;

    // if a number is prime mark all its multiples
    // as non prime
    for (var i=2; i*i <= x; i++)
    {
        if (primes[i] == false)
        {
            for (var j=2; j*i <= x; j++)
                primes[i*j] = true;
        }
    }
}

// function that returns numbers of number that have
// n divisors in range from a to b. x is sqrt(b) + 1.
function nDivisors(primes, x,  a, b, n)
{
    // result holds number of numbers having n divisors
    var result = 0;

    // vector to hold all the prime numbers between 1
    // ans sqrt(b)
    var v = [];
    for (var i = 2; i <= x; i++)
        if (primes[i] == false)
            v.push(i);

    // Traversing all numbers in given range
    for (var i=a; i<=b; i++)
    {
        // initialising temp as i
        var temp = i;

        // total holds the number of divisors of i
        var total = 1;
        var j = 0;

        // we need to use that prime numbers that
        // are less than equal to sqrt(temp)
        for (var k = v[j]; k*k <= temp; k = v[++j])
        {
            // holds the exponent of k in prime
            // factorization of i
            var count = 0;

            // repeatedly divide temp by k till it is
            // divisible and accordingly increase count
            while (temp%k == 0)
            {
                count++;
                temp = parseInt(temp/k);
            }

            // using the formula no.of divisors =
            // (e1+1)*(e2+1)....
            total = total*(count+1);

        }

        // if temp is not equal to 1 then there is
        // prime number in prime factorization of i
        // greater than sqrt(i)
        if (temp != 1)
            total = total*2;

        // if i is a ndivisor number increase result
        if (total == n)
            result++;
    }
    return result;
}

// Returns count of numbers in [a..b] having
// n divisors.
function countNDivisors(a, b, n)
{
    var x = parseInt(Math.sqrt(b)) + 1;

    // primes[i] = true if i is a prime number
    var primes = Array(x+1).fill(false);

    // initialising each number as prime
    sieve(primes, x);

    return nDivisors(primes, x, a, b, n);
}

// driver code
var a = 1, b = 7, n = 2;
document.write(countNDivisors(a, b, n));

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
4
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。