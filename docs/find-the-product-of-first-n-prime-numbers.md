# 求前 N 个素数的乘积

> 原文:[https://www . geesforgeks . org/find-第一个 n 素数的乘积/](https://www.geeksforgeeks.org/find-the-product-of-first-n-prime-numbers/)

给定一个正整数 N，计算前 N 个素数的乘积。

**示例:**

```
Input : N = 3
Output : 30
Explanation : First 3 prime numbers are 2, 3, 5.

Input : N = 5
Output : 2310 
```

**进场:**

*   创建一个筛子，它将帮助我们识别这个数字在 O(1)时间内是否是质数。
*   运行一个从 1 开始的循环，直到并且除非我们找到 n 个质数。
*   把所有质数相乘，忽略那些不是质数的。
*   然后，显示前 N 个素数的乘积。

**时间复杂度**–O(Nlog(logN))

下面是上述方法的实现:

## C++

```
// C++ implementation of above solution
#include "cstring"
#include <iostream>
using namespace std;
#define MAX 10000

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the product of 1st N prime numbers
int solve(int n)
{
    // count of prime numbers
    int count = 0, num = 1;

    // product of prime numbers
    long long int prod = 1;

    while (count < n) {

        // if the number is prime add it
        if (prime[num]) {
            prod *= num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return prod;
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    int n = 5;

    // find the value of 1st n prime numbers
    cout << solve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above solution

class GFG
{
    static int MAX=10000;

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    static boolean[] prime=new boolean[MAX + 1];

static void SieveOfEratosthenes()
{

    prime[1] = true;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == false) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = true;
        }
    }
}

// find the product of 1st N prime numbers
static int solve(int n)
{
    // count of prime numbers
    int count = 0, num = 1;

    // product of prime numbers
    int prod = 1;

    while (count < n) {

        // if the number is prime add it
        if (!prime[num]) {
            prod *= num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return prod;
}

// Driver code
public static void main(String[] args)
{
    // create the sieve
    SieveOfEratosthenes();

    int n = 5;

    // find the value of 1st n prime numbers
    System.out.println(solve(n));

}
}
// This code is contributed by mits
```

## C#

```
// C# implementation of above solution

class GFG
{
    static int MAX=10000;

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    static bool[] prime=new bool[MAX + 1];

static void SieveOfEratosthenes()
{

    prime[1] = true;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == false) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = true;
        }
    }
}

// find the product of 1st N prime numbers
static int solve(int n)
{
    // count of prime numbers
    int count = 0, num = 1;

    // product of prime numbers
    int prod = 1;

    while (count < n) {

        // if the number is prime add it
        if (!prime[num]) {
            prod *= num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return prod;
}

// Driver code
public static void Main()
{
    // create the sieve
    SieveOfEratosthenes();

    int n = 5;

    // find the value of 1st n prime numbers
    System.Console.WriteLine(solve(n));

}
}
// This code is contributed by mits
```

## 计算机编程语言

```
'''
python3 implementation of above solution'''
import math as mt

MAX=10000

'''
Create a boolean array "prime[0..n]" and initialize
all entries it as true. A value in prime[i] will
finally be false if i is Not a prime, else true.'''

prime=[True for i in range(MAX+1)]

def SieveOfErastosthenes():

    prime[1]=False

    for p in range(2,mt.ceil(mt.sqrt(MAX))):
        #if prime[p] is not changes, then it is a prime

        if prime[p]:
            #set all multiples of p to non-prime
            for i in range(2*p,MAX+1,p):
                prime[i]=False

#find the product of 1st N prime numbers

def solve(n):
    #count of prime numbers
    count,num=0,1

    #product of prime numbers

    prod=1
    while count<n:
        #if the number is prime add it

        if prime[num]:
            prod*=num
            #increase the count

            count+=1
        num+=1
    return prod

#Driver code

#create the sieve
SieveOfErastosthenes()

n=5

#find the value of 1st n prime numbers
print(solve(n))

#this code is contributed by Mohit Kumar 29

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above solution
$MAX = 10000;

// Create a boolean array "$prime[0..$n]" and
// initialize all entries it as true. A value
// in $prime[i] will finally be false if i is
// Not a $prime, else true.
$prime = array_fill(0, $MAX + 1, true);

function SieveOfEratosthenes()
{
    global $MAX;
    global $prime;
    $prime = array_fill(0, $MAX + 1, true);
    $prime[1] = false;

    for ($p = 2; $p * $p <= $MAX; $p++)
    {

        // If $prime[$p] is not changed,
        // then it is a $prime
        if ($prime[$p] == true)
        {

            // Set all multiples of $p to non-$prime
            for ($i = $p * 2; $i <= $MAX; $i += $p)
                $prime[$i] = false;
        }
    }
}

// find the product of 1st N $prime numbers
function solve($n)
{
    global $prime;

    // $count of $prime numbers
    $count = 0;
    $num = 1;

    // product of $prime numbers
    $prod = 1;

    while ($count < $n)
    {

        // if the number is $prime add it
        if ($prime[$num]== true)
        {
            $prod *= $num;

            // increase the $count
            $count++;
        }

        // get to next number
        $num++;
    }
    return $prod;
}

// Driver code

// create the sieve
SieveOfEratosthenes();

$n = 5;

// find the value of 1st $n $prime numbers
echo solve($n);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript implementation of above solution
let MAX = 10000;

// Create a boolean array "prime[0..n]" and
// initialize all entries it as true. A value
// in prime[i] will finally be false if i is
// Not a prime, else true.
let prime = new Array(MAX + 1).fill(true);

function SieveOfEratosthenes()
{
    prime[1] = false;

    for (let p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Set all multiples of p to non-prime
            for (let i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the product of 1st N prime numbers
function solve(n)
{   
    // count of prime numbers
    let count = 0;
    let num = 1;

    // product of prime numbers
    let prod = 1;

    while (count < n)
    {

        // if the number is prime add it
        if (prime[num]== true)
        {
            prod *= num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return prod;
}

// Driver code

// create the sieve
SieveOfEratosthenes();

let n = 5;

// find the value of 1st n prime numbers
document.write(solve(n));

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
2310
```

**注:**对于较大的 N 值，乘积可能给出整数溢出误差。
同样对于多个查询，可以使用前缀数组技术，该技术将在首先制作前缀数组之后给出 O(1)中每个查询的输出，这将花费 O(N)时间。