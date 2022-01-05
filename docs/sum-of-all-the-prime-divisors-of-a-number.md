# 一个数的所有质因数之和

> 原文:[https://www . geeksforgeeks . org/所有素数除数之和/](https://www.geeksforgeeks.org/sum-of-all-the-prime-divisors-of-a-number/)

给定一个数 n，任务是求 n 的所有质因数之和

**示例:**

```
Input: 60
Output: 10
2, 3, 5 are prime divisors of 60

Input: 39
Output: 16
3, 13 are prime divisors of 39
```

一种**天真的方法**是对所有的数字进行迭代，直到 N，并检查该数字是否除以 N。如果该数字除以 N，则检查该数字是否为质数。把所有质数加起来，直到 N 除以 N

下面是上述方法的实现:

## C++

```
// CPP program to find sum of
// prime divisors of N
#include <bits/stdc++.h>
using namespace std;
#define N 1000005

// Function to check if the
// number is prime or not.
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// function to find sum of prime
// divisors of N
int SumOfPrimeDivisors(int n)
{
    int sum = 0;
    for (int i = 1; i <= n; i++) {
        if (n % i == 0) {
            if (isPrime(i))
                sum += i;
        }
    }
    return sum;
}
// Driver code
int main()
{
    int n = 60;
    cout << "Sum of prime divisors of 60 is " << SumOfPrimeDivisors(n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum
// of prime divisors of N
import java.io.*;
import java.util.*;

class GFG
{
// Function to check if the
// number is prime or not.
static boolean isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

// function to find
// sum of prime
// divisors of N
static int SumOfPrimeDivisors(int n)
{
    int sum = 0;
    for (int i = 1;
             i <= n; i++)
    {
        if (n % i == 0)
        {
            if (isPrime(i))
                sum += i;
        }
    }
    return sum;
}

// Driver code
public static void main(String args[])
{
    int n = 60;
    System.out.print("Sum of prime divisors of 60 is " +
                          SumOfPrimeDivisors(n) + "\n");
}
}
```

## C#

```
// C# program to find sum
// of prime divisors of N
using System;
class GFG
{

// Function to check if the
// number is prime or not.
static bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

// function to find
// sum of prime
// divisors of N
static int SumOfPrimeDivisors(int n)
{
    int sum = 0;
    for (int i = 1;
            i <= n; i++)
    {
        if (n % i == 0)
        {
            if (isPrime(i))
                sum += i;
        }
    }
    return sum;
}

// Driver code
public static void Main()
{
    int n = 60;
    Console.WriteLine("Sum of prime divisors of 60 is " +
                        SumOfPrimeDivisors(n) + "\n");
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python 3 program to find
# sum of prime divisors of N
N = 1000005

# Function to check if the
# number is prime or not.
def isPrime(n):

    # Corner cases
    if n <= 1:
        return False
    if n <= 3:
        return True

    # This is checked so that 
    # we can skip middle five
    # numbers in below loop
    if n % 2 == 0 or n % 3 == 0:
        return False

    i = 5
    while i * i <= n:
        if (n % i == 0 or
            n % (i + 2) == 0):
            return False
        i = i + 6

    return True

# function to find sum
# of prime divisors of N
def SumOfPrimeDivisors(n):
    sum = 0
    for i in range(1, n + 1) :
        if n % i == 0 :
            if isPrime(i):
                sum += i

    return sum

# Driver code
n = 60
print("Sum of prime divisors of 60 is " +
              str(SumOfPrimeDivisors(n)))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of prime divisors of N
$N = 1000005;

// Function to check if the
// number is prime or not.
function isPrime($n)
{
    global $N;
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n;
                 $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
            return false;

    return true;
}

// function to find sum
// of prime divisors of N
function SumOfPrimeDivisors($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            if (isPrime($i))
                $sum += $i;
        }
    }
    return $sum;
}

// Driver code
$n = 60;
echo "Sum of prime divisors of 60 is " .
                 SumOfPrimeDivisors($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to find sum of
// prime divisors of N
    let N = 1000005;

    // Function to check if the
    // number is prime or not.
    function isPrime(n)
    {
        // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
    }

    // function to find sum of prime
    // divisors of N
    function SumOfPrimeDivisors(n)
    {
        let sum = 0;
    for (let i = 1; i <= n; i++) {
        if (n % i == 0) {
            if (isPrime(i))
                sum += i;
        }
    }
    return sum;
    }

    // Driver code
    let n = 60;
    document.write("Sum of prime divisors of 60 is "+SumOfPrimeDivisors(n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Sum of prime divisors of 60 is 10
```

**时间复杂度:** O(N * sqrt(N))

**高效方法:**通过使用厄拉多塞的[筛，经过一些修改，可以降低复杂度。修改如下:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   取一个大小为 N 的数组，在所有的索引中替换零(首先考虑所有的数字都是质数)。
*   迭代索引为零的所有数字(即质数)。
*   把这个数加起来，它是小于 N 的倍数
*   返回存储了总和的数组[N]值。

下面是上述方法的实现。

## C++

```
// CPP program to find prime divisors of
// all numbers from 1 to n
#include <bits/stdc++.h>
using namespace std;

// function to find prime divisors of
// all numbers from 1 to n
int Sum(int N)
{
    int SumOfPrimeDivisors[N+1] = { 0 };

    for (int i = 2; i <= N; ++i) {

        // if the number is prime
        if (!SumOfPrimeDivisors[i]) {

            // add this prime to all it's multiples
            for (int j = i; j <= N; j += i) {

                SumOfPrimeDivisors[j] += i;
            }
        }
    }
    return SumOfPrimeDivisors[N];
}

// Driver code
int main()
{
    int N = 60;
    cout << "Sum of prime divisors of 60 is "
         << Sum(N) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// prime divisors of
// all numbers from 1 to n
import java.io.*;
import java.util.*;

class GFG
{

// function to find prime
// divisors of all numbers
// from 1 to n
static int Sum(int N)
{
    int SumOfPrimeDivisors[] = new int[N + 1];

    for (int i = 2; i <= N; ++i)
    {

        // if the number is prime
        if (SumOfPrimeDivisors[i] == 0)
        {

            // add this prime to
            // all it's multiples
            for (int j = i; j <= N; j += i)
            {

                SumOfPrimeDivisors[j] += i;
            }
        }
    }
    return SumOfPrimeDivisors[N];
}

// Driver code
public static void main(String args[])
{
    int N = 60;
    System.out.print("Sum of prime " +
                "divisors of 60 is " +
                       Sum(N) + "\n");
}
}
```

## 蟒蛇 3

```
# Python 3 program to find
# prime divisors of
# all numbers from 1 to n

# function to find prime
# divisors of all numbers
# from 1 to n
def Sum(N):

    SumOfPrimeDivisors = [0] * (N + 1)

    for i in range(2, N + 1) :

        # if the number is prime
        if (SumOfPrimeDivisors[i] == 0) :

            # add this prime to
            # all it's multiples
            for j in range(i, N + 1, i) :

                SumOfPrimeDivisors[j] += i

    return SumOfPrimeDivisors[N]

# Driver code
N = 60
print("Sum of prime" ,
      "divisors of 60 is",
                  Sum(N));

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find
// prime divisors of
// all numbers from 1 to n
using System;

class GFG
{

// function to find prime
// divisors of all numbers
// from 1 to n
static int Sum(int N)
{
    int []SumOfPrimeDivisors = new int[N + 1];

    for (int i = 2; i <= N; ++i)
    {

        // if the number is prime
        if (SumOfPrimeDivisors[i] == 0)
        {

            // add this prime to
            // all it's multiples
            for (int j = i;
                     j <= N; j += i)
            {

                SumOfPrimeDivisors[j] += i;
            }
        }
    }

    return SumOfPrimeDivisors[N];
}

// Driver code
public static void Main()
{
    int N = 60;
    Console.Write("Sum of prime " +
                    "divisors of 60 is " +
                         Sum(N) + "\n");
}
}

// This code is contributed
// by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find prime
// divisors of all numbers
// from 1 to n

// function to find prime
// divisors of all numbers
// from 1 to n
function Sum($N)
{
    for($i = 0; $i <= $N; $i++)
        $SumOfPrimeDivisors[$i] = 0;

    for ($i = 2; $i <= $N; ++$i)
    {

        // if the number is prime
        if (!$SumOfPrimeDivisors[$i])
        {

            // add this prime to
            // all it's multiples
            for ($j = $i; $j <= $N; $j += $i)
            {

                $SumOfPrimeDivisors[$j] += $i;
            }
        }
    }
    return $SumOfPrimeDivisors[$N];
}

// Driver code
$N = 60;
echo "Sum of prime divisors of 60 is " . Sum($N);

// This code is contributed by Mahadev99
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// prime divisors of
// all numbers from 1 to n

    // function to find prime
    // divisors of all numbers
    // from 1 to n
    function Sum(N)
    {
        let SumOfPrimeDivisors = new Array(N+1);
        for(let i=0;i<SumOfPrimeDivisors.length;i++)
        {
            SumOfPrimeDivisors[i]=0;
        }
        for (let i = 2; i <= N; ++i)
        {

            // if the number is prime
            if (SumOfPrimeDivisors[i] == 0)
            {

                // add this prime to
                // all it's multiples
                for (let j = i; j <= N; j += i)
                {

                    SumOfPrimeDivisors[j] += i;
                }
            }
        }
        return SumOfPrimeDivisors[N];
    }

    // Driver code
    let N = 60;
    document.write("Sum of prime " +
                "divisors of 60 is " +
                       Sum(N) + "<br>");

    // This code is contributed by rag2127

</script>
```

**Output**

```
Sum of prime divisors of 60 is 10
```

**时间复杂度:** O(N * log N)

#### 高效方法:

通过有效地找到所有因素，可以降低时间复杂度。

下面的方法描述了如何有效地找到所有的因素。

如果我们仔细看，所有的除数都是成对出现的。例如，如果 n = 100，那么各种除数对是:(1，100)，(2，50)，(4，25)，(5，20)，(10，10)

利用这个事实，我们可以大大加快我们的程序。

然而，如果像(10，10)那样有两个相等的除数，我们就要小心了。在这种情况下，我们只拿其中一个。

下面是上述方法的实现。

## C++

```
// C++ program to find sum of
// prime divisors of N
#include <bits/stdc++.h>
using namespace std;

// Function to check if the
// number is prime or not.
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// function to find sum of prime
// divisors of N
int SumOfPrimeDivisors(int n)
{
    int sum = 0;
    // return type of sqrt function
    // if float
    int root_n = (int)sqrt(n);
    for (int i = 1; i <= root_n; i++) {
        if (n % i == 0) {
            // both factors are same
            if (i == n / i && isPrime(i)) {
                sum += i;
            }
            else {
                // both factors are
                // not same ( i and n/i )
                if (isPrime(i)) {
                    sum += i;
                }
                if (isPrime(n / i)) {
                    sum += (n / i);
                }
            }
        }
    }
    return sum;
}
// Driver code
int main()
{
    int n = 60;
    cout << "Sum of prime divisors of 60 is "
         << SumOfPrimeDivisors(n) << endl;
}
// This code is contributed by hemantraj712
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of
// prime divisors of N
class GFG{

// Function to check if the
// number is prime or not.
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to find sum of prime
// divisors of N
static int SumOfPrimeDivisors(int n)
{
    int sum = 0;

    // Return type of sqrt function
    // if float
    int root_n = (int)Math.sqrt(n);
    for(int i = 1; i <= root_n; i++)
    {
        if (n % i == 0)
        {

            // Both factors are same
            if (i == n / i && isPrime(i))
            {
                sum += i;
            }
            else
            {

                // Both factors are
                // not same ( i and n/i )
                if (isPrime(i))
                {
                    sum += i;
                }
                if (isPrime(n / i))
                {
                    sum += (n / i);
                }
            }
        }
    }
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 60;
    System.out.println("Sum of prime divisors of 60 is " +
                       SumOfPrimeDivisors(n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find sum of
# prime divisors of N
import math

# Function to check if the
# number is prime or not.
def isPrime(n) :

    # Corner cases
    if (n <= 1) :
        return False
    if (n <= 3) :
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0) :
        return False

    i = 5
    while i * i <= n :
        if (n % i == 0 or n % (i + 2) == 0) :
            return False
        i = i + 6

    return True

# function to find sum of prime
# divisors of N
def SumOfPrimeDivisors(n) :

    Sum = 0

    # return type of sqrt function
    # if float
    root_n = (int)(math.sqrt(n))
    for i in range(1, root_n + 1) :
        if (n % i == 0) :

            # both factors are same
            if (i == (int)(n / i) and isPrime(i)) :
                Sum += i

            else :
                # both factors are
                # not same ( i and n/i )
                if (isPrime(i)) :
                    Sum += i

                if (isPrime((int)(n / i))) :
                    Sum += (int)(n / i)

    return Sum

n = 60
print("Sum of prime divisors of 60 is", SumOfPrimeDivisors(n))

# This code is contributed by rameshtravel07
```

## C#

```
// C# program to find sum of
// prime divisors of N
using System;
class GFG {

    // Function to check if the
    // number is prime or not.
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // function to find sum of prime
    // divisors of N
    static int SumOfPrimeDivisors(int n)
    {
        int sum = 0;
        // return type of sqrt function
        // if float
        int root_n = (int)Math.Sqrt(n);
        for (int i = 1; i <= root_n; i++) {
            if (n % i == 0) {
                // both factors are same
                if (i == n / i && isPrime(i)) {
                    sum += i;
                }
                else {
                    // both factors are
                    // not same ( i and n/i )
                    if (isPrime(i)) {
                        sum += i;
                    }
                    if (isPrime(n / i)) {
                        sum += (n / i);
                    }
                }
            }
        }
        return sum;
    }

  static void Main() {
    int n = 60;
    Console.WriteLine("Sum of prime divisors of 60 is " + SumOfPrimeDivisors(n));
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
    // Javascript program to find sum of
    // prime divisors of N

    // Function to check if the
    // number is prime or not.
    function isPrime(n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // function to find sum of prime
    // divisors of N
    function SumOfPrimeDivisors(n)
    {
        let sum = 0;
        // return type of sqrt function
        // if float
        let root_n = parseInt(Math.sqrt(n), 10);
        for (let i = 1; i <= root_n; i++) {
            if (n % i == 0) {
                // both factors are same
                if (i == parseInt(n / i, 10) && isPrime(i)) {
                    sum += i;
                }
                else {
                    // both factors are
                    // not same ( i and n/i )
                    if (isPrime(i)) {
                        sum += i;
                    }
                    if (isPrime(parseInt(n / i, 10))) {
                        sum += (parseInt(n / i, 10));
                    }
                }
            }
        }
        return sum;
    }

    let n = 60;
    document.write("Sum of prime divisors of 60 is "
         + SumOfPrimeDivisors(n) + "</br>");

 // This code is contributed by muksh07.
</script>
```

**Output**

```
Sum of prime divisors of 60 is 10
```

**时间复杂度** : O(sqrt(N) * sqrt(N))