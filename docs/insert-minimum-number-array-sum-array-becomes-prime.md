# 在数组中插入最小数，使数组的和成为质数

> 原文:[https://www . geesforgeks . org/insert-minimum-number-array-sum-array-变成-prime/](https://www.geeksforgeeks.org/insert-minimum-number-array-sum-array-becomes-prime/)

给定 n 个整数的数组。找到要插入数组中的最小数，这样数组中所有元素的和就成了质数。如果和已经是质数，那么返回 0。
**例:**

```
Input : arr[] = { 2, 4, 6, 8, 12 }
Output : 5

Input : arr[] = { 3, 5, 7 }
Output : 0
```

**天真法:**解决这个问题最简单的方法就是先求数组元素的和。然后检查这个和是否是质数，如果和是质数，返回零，否则找到大于这个和的质数。我们可以通过从(和+1)开始检查一个数是否是素数，直到找到一个素数，来找到大于和的素数。一旦找到一个大于和的素数，就返回和与这个素数的差。
以下是上述想法的实现:

## C++

```
// C++ program to find minimum number to
// insert in array so their sum is prime
#include <bits/stdc++.h>
using namespace std;

// function to check if a
// number is prime or not
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n - 1
    for (int i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Find prime number
// greater than a number
int findPrime(int n)
{
    int num = n + 1;

    // find prime greater than n
    while (num)
    {
        // check if num is prime
        if (isPrime(num))
            return num;

        // increment num
        num = num + 1;
    }

    return 0;
}

// To find number to be added
// so sum of array is prime
int minNumber(int arr[], int n)
{
    int sum = 0;

    // To find sum of array elements
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // if sum is already prime
    // return 0
    if (isPrime(sum))
        return 0;

    // To find prime number
    // greater than sum
    int num = findPrime(sum);

    // Return difference of
    // sum and num
    return num - sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6, 8, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minNumber(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number to
// insert in array so their sum is prime

class GFG
{
    // function to check if a
    // number is prime or not
    static boolean isPrime(int n)
        {
            // Corner case
            if (n <= 1)
                return false;

            // Check from 2 to n - 1
            for (int i = 2; i < n; i++)
                if (n % i == 0)
                    return false;

            return true;
        }

    // Find prime number
    // greater than a number
    static int findPrime(int n)
        {
            int num = n + 1;

            // find prime greater than n
            while (num > 0)
                {

                    // check if num is prime
                    if (isPrime(num))
                        return num;

                    // increment num
                    num = num + 1;
                }
            return 0;
        }

    // To find number to be added
    // so sum of array is prime
    static int minNumber(int arr[], int n)
        {
            int sum = 0;

            // To find sum of array elements
            for (int i = 0; i < n; i++)
                sum += arr[i];

            // if sum is already prime
            // return 0
            if (isPrime(sum))
                return 0;

            // To find prime number
            // greater than sum
            int num = findPrime(sum);

            // Return difference of
            // sum and num
            return num - sum;
        }

    // Driver Code
    public static void main(String[]args)
        {
            int arr[] = { 2, 4, 6, 8, 12 };
            int n = arr.length;
            System.out.println(minNumber(arr, n));
        }
}

// This code is contributed by Azkia Anam.
```

## 蟒蛇 3

```
# Python3 program to find minimum number to
# insert in array so their sum is prime

# function to check if a
# number is prime or not
def isPrime(n):

    # Corner case
    if n <= 1:
        return False

    # Check from 2 to n - 1
    for i in range(2, n):
        if n % i == 0:
            return False

    return True

# Find prime number
# greater than a number
def findPrime(n):
    num = n + 1

    # find prime greater than n
    while (num):

        # check if num is prime
        if isPrime(num):
            return num

        # Increment num
        num += 1

    return 0

# To find number to be added
# so sum of array is prime
def minNumber(arr):
    s = 0

    # To find sum of array elements
    for i in range(0, len(arr)):
        s += arr[i]

    # If sum is already prime
    # return 0
    if isPrime(s) :
        return 0

    # To find prime number
    # greater than sum
    num = findPrime(s)

    # Return difference of sum and num
    return num - s

# Driver code
arr = [ 2, 4, 6, 8, 12 ]
print (minNumber(arr))

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find minimum number to
// insert in array so their sum is prime
using System;

class GFG
{
    // function to check if a
    // number is prime or not
    static bool isPrime(int n)
        {
            // Corner case
            if (n <= 1)
                return false;

            // Check from 2 to n - 1
            for (int i = 2; i < n; i++)
                if (n % i == 0)
                    return false;

            return true;
        }

    // Find prime number
    // greater than a number
    static int findPrime(int n)
        {
            int num = n + 1;

            // find prime greater than n
            while (num > 0)
                {

                    // check if num is prime
                    if (isPrime(num))
                        return num;

                    // increment num
                    num = num + 1;
                }
            return 0;
        }

    // To find number to be added
    // so sum of array is prime
    static int minNumber(int []arr, int n)
        {
            int sum = 0;

            // To find sum of array elements
            for (int i = 0; i < n; i++)
                sum += arr[i];

            // if sum is already prime
            // return 0
            if (isPrime(sum))
                return 0;

            // To find prime number
            // greater than sum
            int num = findPrime(sum);

            // Return difference of sum and num
            return num - sum;
        }

    // Driver Code
    public static void Main()
        {
            int []arr = { 2, 4, 6, 8, 12 };
            int n = arr.Length;
            Console.Write(minNumber(arr, n));
        }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number to
// insert in array so their sum is prime

// function to check if a
// number is prime or not
function isPrime($n)
{

    // Corner case
    if ($n <= 1)
        return false;

    // Check from 2 to n - 1
    for ($i = 2; $i < $n; $i++)
        if ($n % $i == 0)
            return false;

    return true;
}

// Find prime number
// greater than a number
function findPrime($n)
{
    $num = $n + 1;

    // find prime greater than n
    while ($num)
    {
        // check if num is prime
        if (isPrime($num))
            return $num;

        // increment num
        $num = $num + 1;
    }

    return 0;
}

// To find number to be added
// so sum of array is prime
function minNumber($arr, $n)
{
    $sum = 0;

    // To find sum of array elements
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // if sum is already prime
    // return 0
    if (isPrime($sum))
        return 0;

    // To find prime number
    // greater than sum
    $num = findPrime($sum);

    // Return difference of
    // sum and num
    return $num - $sum;
}

    // Driver Code
    $arr = array(2, 4, 6, 8, 12);
    $n = sizeof($arr);
    echo minNumber($arr, $n);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number to
// insert in array so their sum is prime

    // function to check if a
    // number is prime or not
    function isPrime(n)
    {
        // Corner case
            if (n <= 1)
                return false;

            // Check from 2 to n - 1
            for (let i = 2; i < n; i++)
                if (n % i == 0)
                    return false;

            return true;
    }

    // Find prime number
    // greater than a number
    function findPrime(n)
    {
        let num = n + 1;

            // find prime greater than n
            while (num > 0)
                {

                    // check if num is prime
                    if (isPrime(num))
                        return num;

                    // increment num
                    num = num + 1;
                }
            return 0;
    }

    // To find number to be added
    // so sum of array is prime
    function minNumber(arr,n)
    {
        let sum = 0;

            // To find sum of array elements
            for (let i = 0; i < n; i++)
                sum += arr[i];

            // if sum is already prime
            // return 0
            if (isPrime(sum))
                return 0;

            // To find prime number
            // greater than sum
            let num = findPrime(sum);

            // Return difference of
            // sum and num
            return num - sum;
    }

     // Driver Code
    let arr=[2, 4, 6, 8, 12 ];
    let n = arr.length;
    document.write(minNumber(arr, n));

    //This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
5
```

**时间复杂度:** O( N <sup>2</sup> )
**高效方法:**我们可以通过使用埃拉托斯特尼的[筛高效地预先计算一个大型布尔数组来检查一个数是否是素数，从而优化上述方法。一旦所有质数都产生了，就找出刚好大于和的质数，并返回它们之间的差。
以下是本办法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to find minimum number to
// insert in array so their sum is prime
#include <bits/stdc++.h>
using namespace std;

#define MAX 100005

// Array to store primes
bool isPrime[MAX];

// function to calculate primes
// using sieve of eratosthenes
void sieveOfEratostheneses()
{
    memset(isPrime, true, sizeof(isPrime));
    isPrime[1] = false;
    for (int i = 2; i * i < MAX; i++)
    {
        if (isPrime[i])
        {
            for (int j = 2 * i; j < MAX; j += i)
                isPrime[j] = false;
        }
    }
}

// Find prime number
// greater than a number
int findPrime(int n)
{
    int num = n + 1;

    // To return prime number
    // greater than n
    while (num)
    {
        // check if num is prime
        if (isPrime[num])
            return num;

        // increment num
        num = num + 1;
    }
    return 0;
}

// To find number to be added
// so sum of array is prime
int minNumber(int arr[], int n)
{
    // call sieveOfEratostheneses
    // to calculate primes
    sieveOfEratostheneses();

    int sum = 0;

    // To find sum of array elements
    for (int i = 0; i < n; i++)
        sum += arr[i];

    if (isPrime[sum])
        return 0;

    // To find prime number
    // greater then sum
    int num = findPrime(sum);

    // Return difference of
    // sum and num
    return num - sum;
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 6, 8, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minNumber(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number to
// insert in array so their sum is prime

class GFG
{
static int MAX = 100005;

// Array to store primes
static boolean[] isPrime = new boolean[MAX];

// function to calculate primes
// using sieve of eratosthenes
static void sieveOfEratostheneses()
{
    isPrime[1] = true;
    for (int i = 2; i * i < MAX; i++)
    {
        if (!isPrime[i])
        {
            for (int j = 2 * i; j < MAX; j += i)
                isPrime[j] = true;
        }
    }
}

// Find prime number greater
// than a number
static int findPrime(int n)
{
    int num = n + 1;

    // To return prime number
    // greater than n
    while (num > 0)
    {
        // check if num is prime
        if (!isPrime[num])
            return num;

        // increment num
        num = num + 1;
    }
    return 0;
}

// To find number to be added
// so sum of array is prime
static int minNumber(int arr[], int n)
{
    // call sieveOfEratostheneses
    // to calculate primes
    sieveOfEratostheneses();

    int sum = 0;

    // To find sum of array elements
    for (int i = 0; i < n; i++)
        sum += arr[i];

    if (!isPrime[sum])
        return 0;

    // To find prime number
    // greater then sum
    int num = findPrime(sum);

    // Return difference of
    // sum and num
    return num - sum;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 6, 8, 12 };
    int n = arr.length;

    System.out.println(minNumber(arr, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find minimum number to
# insert in array so their sum is prime

isPrime = [1] * 100005

# function to calculate prime
# using sieve of eratosthenes
def sieveOfEratostheneses():
    isPrime[1] = False
    i = 2
    while i * i < 100005:
        if(isPrime[i]):
            j = 2 * i
            while j < 100005:
                isPrime[j] = False
                j += i
        i += 1
    return

# Find prime number
# greater than a number
def findPrime(n):
    num = n + 1

    # find prime greater than n
    while(num):

        # check if num is prime
        if isPrime[num]:
            return num

        # Increment num
        num += 1

    return 0

# To find number to be added
# so sum of array is prime
def minNumber(arr):

    # call sieveOfEratostheneses to
    # calculate primes
    sieveOfEratostheneses()

    s = 0

    # To find sum of array elements
    for i in range(0, len(arr)):
        s += arr[i]

    # If sum is already prime
    # return 0
    if isPrime[s] == True:
        return 0

    # To find prime number
    # greater than sum
    num = findPrime(s)

    # Return difference of
    # sum and num
    return num - s

# Driver code
arr = [ 2, 4, 6, 8, 12 ]
print (minNumber(arr))

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find minimum number to
// insert in array so their sum is prime

class GFG
{
static int MAX = 100005;

// Array to store primes
static bool[] isPrime = new bool[MAX];

// function to calculate primes
// using sieve of eratosthenes
static void sieveOfEratostheneses()
{
    isPrime[1] = true;
    for (int i = 2; i * i < MAX; i++)
    {
        if (!isPrime[i])
        {
            for (int j = 2 * i; j < MAX; j += i)
                isPrime[j] = true;
        }
    }
}

// Find prime number greater
// than a number
static int findPrime(int n)
{
    int num = n + 1;

    // To return prime number
    // greater than n
    while (num > 0)
    {
        // check if num is prime
        if (!isPrime[num])
            return num;

        // increment num
        num = num + 1;
    }
    return 0;
}

// To find number to be added
// so sum of array is prime
static int minNumber(int[] arr, int n)
{
    // call sieveOfEratostheneses
    // to calculate primes
    sieveOfEratostheneses();

    int sum = 0;

    // To find sum of array elements
    for (int i = 0; i < n; i++)
        sum += arr[i];

    if (!isPrime[sum])
        return 0;

    // To find prime number
    // greater then sum
    int num = findPrime(sum);

    // Return difference of
    // sum and num
    return num - sum;
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 4, 6, 8, 12 };
    int n = arr.Length;

    System.Console.WriteLine(minNumber(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to find minimum number to
// insert in array so their sum is prime

$MAX =100005;

// function to calculate primes 
// using sieve of eratosthenes
function sieveOfEratostheneses()
{
    $isPrime = array_fill(true,$MAX, NULL);
    $isPrime[1] = false;
    for ($i = 2; $i * $i < $MAX; $i++) 
    {
        if ($isPrime[$i]) 
        {
            for ($j = 2 * $i; $j < $MAX; $j += $i)
                $isPrime[$j] = false;
        }
    }
}

// Find prime number 
// greater than a number
function findPrime($n)
{
    $num = $n + 1;

    // To return prime number
    // greater than n
    while ($num) 
    {
        // check if num is prime
        if ($isPrime[$num])
            return $num;

        // increment num
        $num = $num + 1;
    }
    return 0;
}

// To find number to be added 
// so sum of array is prime
function minNumber(&$arr, $n)
{
    // call sieveOfEratostheneses
    // to calculate primes
    sieveOfEratostheneses();

    $sum = 0;

    // To find sum of array elements
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    if ($isPrime[$sum])
        return 0;

    // To find prime number
    // greater then sum
    $num = findPrime($sum);

    // Return difference of 
    // sum and num
    return $num - $sum;
}

// Driver Code

    $arr = array ( 2, 4, 6, 8, 12 );
    $n = sizeof($arr) / sizeof($arr[0]);

    echo minNumber($arr, $n);

    return 0;
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number to
// insert in array so their sum is prime

let MAX = 100005;

// Array to store primes
let isPrime = new Array(MAX).fill(0);

// function to calculate primes
// using sieve of eratosthenes
function sieveOfEratostheneses()
{
    isPrime[1] = true;
    for (let i = 2; i * i < MAX; i++)
    {
        if (!isPrime[i])
        {
            for (let j = 2 * i; j < MAX; j += i)
                isPrime[j] = true;
        }
    }
}

// Find prime number greater
// than a number
function findPrime(n)
{
    let num = n + 1;

    // To return prime number
    // greater than n
    while (num > 0)
    {
        // check if num is prime
        if (!isPrime[num])
            return num;

        // increment num
        num = num + 1;
    }
    return 0;
}

// To find number to be added
// so sum of array is prime
function minNumber(arr, n)
{
    // call sieveOfEratostheneses
    // to calculate primes
    sieveOfEratostheneses();

    let sum = 0;

    // To find sum of array elements
    for (let i = 0; i < n; i++)
        sum += arr[i];

    if (!isPrime[sum])
        return 0;

    // To find prime number
    // greater then sum
    let num = findPrime(sum);

    // Return difference of
    // sum and num
    return num - sum;
}

// driver program

    let arr = [ 2, 4, 6, 8, 12 ];
    let n = arr.length;

    document.write(minNumber(arr, n));

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
5
```

**时间复杂度:** O(N log(log N))
本文由**核素**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。