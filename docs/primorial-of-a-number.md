# 一个数字的原始值

> 原文:[https://www.geeksforgeeks.org/primorial-of-a-number/](https://www.geeksforgeeks.org/primorial-of-a-number/)

给定一个数字 n，任务是计算它的原始值。素数(表示为 P <sub>n</sub> #)是前 n 个素数的乘积。[一个数的素数](https://en.wikipedia.org/wiki/Primorial)类似于一个数的阶乘。在素数运算中，不是所有的自然数都相乘，只有素数相乘才能计算出一个数的素数。用 P#表示。
**例:**

```
Input: n = 3
Output: 30 
Priomorial = 2 * 3 * 5 = 30
As a side note, factorial is 2 * 3 * 4 * 5

Input: n = 5
Output: 2310
Primorial = 2 * 3 * 5 * 7 * 11 
```

一种**天真的方法**是逐一检查从 1 到 n 的所有数字是否是素数，如果是，则将乘法结果存储在结果中，类似地将素数的乘法结果存储到 n。
一种**高效的**方法是使用 Sundaram 的[筛](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)找到直到 n 的所有素数，然后通过将它们全部相乘来计算素数。

## C++

```
// C++ program to find Primorial of given numbers
#include<bits/stdc++.h>
using namespace std;
const int MAX = 1000000;

// vector to store all prime less than and equal to 10^6
vector <int> primes;

// Function for sieve of sundaram. This function stores all
// prime numbers less than MAX in primes
void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool marked[MAX/2 + 1] = {0};

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (sqrt(MAX)-1)/2 ; i++)
        for (int j = (i*(i+1))<<1 ; j <= MAX/2 ; j += 2*i +1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=MAX/2; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// Function to calculate primorial of n
int calculatePrimorial(int n)
{
    // Multiply first n primes
    int result = 1; 
    for (int i=0; i<n; i++)
       result = result * primes[i];
    return result;
}

// Driver code
int main()
{
    int n = 5;
    sieveSundaram();
    for (int i = 1 ; i<= n; i++)
        cout << "Primorial(P#) of " << i << " is "
            << calculatePrimorial(i) <<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Primorial of given numbers
import java.util.*;

class GFG{

public static int MAX = 1000000;

// vector to store all prime less than and equal to 10^6
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Function for sieve of sundaram. This function stores all
// prime numbers less than MAX in primes
static void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    boolean[] marked = new boolean[MAX];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (Math.sqrt(MAX) - 1) / 2 ; i++)
    {
        for (int j = (i * (i + 1)) << 1 ; j <= MAX / 2 ; j += 2 * i + 1)
        {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
    {
        if (marked[i] == false)
        {
            primes.add(2 * i + 1);
        }
    }
}

// Function to calculate primorial of n
static int calculatePrimorial(int n)
{
    // Multiply first n primes
    int result = 1;
    for (int i = 0; i < n; i++)
    {
    result = result * primes.get(i);
    }
    return result;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    sieveSundaram();
    for (int i = 1 ; i <= n; i++)
    {
        System.out.println("Primorial(P#) of "+i+" is "+calculatePrimorial(i));
    }
}
}
// This Code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find Primorial of given numbers
import math
MAX = 1000000;

# vector to store all prime less than and equal to 10^6
primes=[];

# Function for sieve of sundaram. This function stores all
# prime numbers less than MAX in primes
def sieveSundaram():

    # In general Sieve of Sundaram, produces primes smaller
    # than (2*x + 2) for a number given number x. Since
    # we want primes smaller than MAX, we reduce MAX to half
    # This array is used to separate numbers of the form
    # i+j+2ij from others where 1 <= i <= j
    marked=[False]*(int(MAX/2)+1);

    # Main logic of Sundaram. Mark all numbers which
    # do not generate prime number by doing 2*i+1
    for i in range(1,int((math.sqrt(MAX)-1)/2)+1):
        for j in range(((i*(i+1))<<1),(int(MAX/2)+1),(2*i+1)):
            marked[j] = True;

    # Since 2 is a prime number
    primes.append(2);

    # Print other primes. Remaining primes are of the
    # form 2*i + 1 such that marked[i] is false.
    for i in range(1,int(MAX/2)):
        if (marked[i] == False):
            primes.append(2*i + 1);

# Function to calculate primorial of n
def calculatePrimorial(n):
    # Multiply first n primes
    result = 1;
    for i in range(n):
        result = result * primes[i];
    return result;

# Driver code
n = 5;
sieveSundaram();
for i in range(1,n+1):
    print("Primorial(P#) of",i,"is",calculatePrimorial(i));

# This code is contributed by mits
```

## C#

```
// C# program to find Primorial of given numbers
using System;
using System.Collections;

class GFG{

public static int MAX = 1000000;

// vector to store all prime less than and equal to 10^6
static ArrayList primes = new ArrayList();

// Function for sieve of sundaram. This function stores all
// prime numbers less than MAX in primes
static void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    bool[] marked = new bool[MAX];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (Math.Sqrt(MAX) - 1) / 2 ; i++)
    {
        for (int j = (i * (i + 1)) << 1 ; j <= MAX / 2 ; j += 2 * i + 1)
        {
            marked[j] = true;
        }
    }

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
    {
        if (marked[i] == false)
        {
            primes.Add(2 * i + 1);
        }
    }
}

// Function to calculate primorial of n
static int calculatePrimorial(int n)
{
    // Multiply first n primes
    int result = 1;
    for (int i = 0; i < n; i++)
    {
    result = result * (int)primes[i];
    }
    return result;
}

// Driver code
public static void Main()
{
    int n = 5;
    sieveSundaram();
    for (int i = 1 ; i <= n; i++)
    {
        System.Console.WriteLine("Primorial(P#) of "+i+" is "+calculatePrimorial(i));
    }
}
}
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Primorial
// of given numbers
$MAX = 100000;

// vector to store all prime less
// than and equal to 10^6
$primes = array();

// Function for sieve of sundaram.
// This function stores all prime
// numbers less than MAX in primes
function sieveSundaram()
{
    global $MAX, $primes;

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than MAX, we reduce MAX
    // to half. This array is used to
    // separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    $marked = array_fill(0, $MAX / 2 + 1, 0);

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for ($i = 1; $i <= (sqrt($MAX) - 1) / 2 ; $i++)
        for ($j = ($i * ($i + 1)) << 1 ;
             $j <= $MAX / 2 ; $j += 2 * $i + 1)
            $marked[$j] = true;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Print other primes. Remaining primes
    // are of the form 2*i + 1 such that
    // marked[i] is false.
    for ($i = 1; $i <= $MAX / 2; $i++)
        if ($marked[$i] == false)
            array_push($primes, (2 * $i + 1));
}

// Function to calculate primorial of n
function calculatePrimorial($n)
{
    global $primes;

    // Multiply first n primes
    $result = 1;
    for ($i = 0; $i < $n; $i++)
    $result = $result * $primes[$i];
    return $result;
}

// Driver code
$n = 5;
sieveSundaram();
for ($i = 1 ; $i<= $n; $i++)
    echo "Primorial(P#) of " . $i .
         " is " . calculatePrimorial($i) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find Primorial
// of given numbers
let MAX = 100000;

// vector to store all prime less
// than and equal to 10^6
let primes = new Array();

// Function for sieve of sundaram.
// This function stores all prime
// numbers less than MAX in primes
function sieveSundaram()
{

    // In general Sieve of Sundaram,
    // produces primes smaller than
    // (2*x + 2) for a number given
    // number x. Since we want primes
    // smaller than MAX, we reduce MAX
    // to half. This array is used to
    // separate numbers of the form
    // i+j+2ij from others where 1 <= i <= j
    let marked = new Array(MAX / 2 + 1).fill(0);

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (let i = 1; i <= (Math.sqrt(MAX) - 1) / 2 ; i++)
        for (let j = (i * (i + 1)) << 1 ;
            j <= MAX / 2 ; j += 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push(2);

    // Print other primes. Remaining primes
    // are of the form 2*i + 1 such that
    // marked[i] is false.
    for (let i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push(2 * i + 1);
}

// Function to calculate primorial of n
function calculatePrimorial(n)
{   
    // Multiply first n primes
    let result = 1;
    for (let i = 0; i < n; i++)
    result = result * primes[i];
    return result;
}

// Driver code
let n = 5;
sieveSundaram();
for (let i = 1 ; i<= n; i++)
    document.write("Primorial(P#) of " + i + " is " +
    calculatePrimorial(i) + "<br>");

// This code is contributed by gfgking

</script>
```

**输出:**

```
Primorial(P#) of 1 is 2
Primorial(P#) of 2 is 6
Primorial(P#) of 3 is 30
Primorial(P#) of 4 is 210
Primorial(P#) of 5 is 2310
```

本文由[**Sahil Chhabra(KILLER)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。