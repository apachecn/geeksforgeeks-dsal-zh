# 检查与所有其他元素同素的数组元素

> 原文:[https://www . geesforgeks . org/check-for-a-array-element-the-co-prime-with-all-others/](https://www.geeksforgeeks.org/check-for-an-array-element-that-is-co-prime-with-all-others/)

给定正整数数组 **arr[]** ，其中**2≤arr[I]≤10<sup>6</sup>T5，所有可能的值为 **i** 。任务是检查给定数组中是否至少有一个元素与该数组的所有其他元素形成同素对。如果不存在这样的元素，则打印**否**否则打印**是**。**

**示例:**

> **输入:** arr[] = {2，8，4，10，6，7}
> **输出:**是
> 7 与数组的所有其他元素同素
> 
> **输入:** arr[] = {3，6，9，12}
> 输出:否

**天真方法:**一个简单的解决方法是检查每个元素与所有其他元素的 gcd 是否等于 1。本方案时间复杂度为 **O(n <sup>2</sup> )** 。

**高效方法:**高效的解决方案是生成给定数组中整数的所有素因子。使用 hash，存储每个元素的计数，它是数组中任何数字的质因数。如果元素与其他元素不包含任何公共素因子，它总是与其他元素形成共素对。
要生成素因子，请阅读文章[使用 O(log n)中的筛进行素因子分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAXN 1000001

// Stores smallest prime factor for every number
int spf[MAXN];

// Hash to store prime factors count
int hash1[MAXN] = { 0 };

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)

        // Marking smallest prime factor for every
        // number to be itself
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    // Checking if i is prime
    for (int i = 3; i * i < MAXN; i++) {

        // Marking SPF for all numbers divisible by i
        if (spf[i] == i) {
            for (int j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to store the prime factors after dividing
// by the smallest prime factor at every step
void getFactorization(int x)
{
    int temp;
    while (x != 1) {
        temp = spf[x];
        if (x % temp == 0) {

            // Storing the count of
            // prime factors in hash
            hash1[spf[x]]++;
            x = x / spf[x];
        }
        while (x % temp == 0)
            x = x / temp;
    }
}

// Function that returns true if there are
// no common prime factors between x
// and other numbers of the array
bool check(int x)
{
    int temp;
    while (x != 1) {
        temp = spf[x];

        // Checking whether it common
        // prime factor with other numbers
        if (x % temp == 0 && hash1[temp] > 1)
            return false;
        while (x % temp == 0)
            x = x / temp;
    }
    return true;
}

// Function that returns true if there is
// an element in the array which is coprime
// with all the other elements of the array
bool hasValidNum(int arr[], int n)
{

    // Using sieve for generating prime factors
    sieve();

    for (int i = 0; i < n; i++)
        getFactorization(arr[i]);

    // Checking the common prime factors
    // with other numbers
    for (int i = 0; i < n; i++)
        if (check(arr[i]))
            return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 2, 8, 4, 10, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (hasValidNum(arr, n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAXN = 1000001;

// Stores smallest prime factor for every number
static int[] spf = new int[MAXN];

// Hash to store prime factors count
static int[] hash1 = new int[MAXN];

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
static void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)

        // Marking smallest prime factor for every
        // number to be itself
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    // Checking if i is prime
    for (int i = 3; i * i < MAXN; i++)
    {

        // Marking SPF for all numbers divisible by i
        if (spf[i] == i)
        {
            for (int j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to store the prime factors after dividing
// by the smallest prime factor at every step
static void getFactorization(int x)
{
    int temp;
    while (x != 1)
    {
        temp = spf[x];
        if (x % temp == 0)
        {

            // Storing the count of
            // prime factors in hash
            hash1[spf[x]]++;
            x = x / spf[x];
        }
        while (x % temp == 0)
            x = x / temp;
    }
}

// Function that returns true if there are
// no common prime factors between x
// and other numbers of the array
static boolean check(int x)
{
    int temp;
    while (x != 1)
    {
        temp = spf[x];

        // Checking whether it common
        // prime factor with other numbers
        if (x % temp == 0 && hash1[temp] > 1)
            return false;
        while (x % temp == 0)
            x = x / temp;
    }
    return true;
}

// Function that returns true if there is
// an element in the array which is coprime
// with all the other elements of the array
static boolean hasValidNum(int []arr, int n)
{

    // Using sieve for generating prime factors
    sieve();

    for (int i = 0; i < n; i++)
        getFactorization(arr[i]);

    // Checking the common prime factors
    // with other numbers
    for (int i = 0; i < n; i++)
        if (check(arr[i]))
            return true;

    return false;
}

// Driver code
public static void main (String[] args)
{

    int []arr = { 2, 8, 4, 10, 6, 7 };
    int n = arr.length;

    if (hasValidNum(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAXN = 1000001

# Stores smallest prime factor for
# every number
spf = [i for i in range(MAXN)]

# Hash to store prime factors count
hash1 = [0 for i in range(MAXN)]

# Function to calculate SPF (Smallest
# Prime Factor) for every number till MAXN
def sieve():

    # Separately marking spf for
    # every even number as 2
    for i in range(4, MAXN, 2):
        spf[i] = 2

    # Checking if i is prime
    for i in range(3, MAXN):

        if i * i >= MAXN:
            break

        # Marking SPF for all numbers
        # divisible by i
        if (spf[i] == i):
            for j in range(i * i, MAXN, i):

                # Marking spf[j] if it is not
                # previously marked
                if (spf[j] == j):
                    spf[j] = i

# Function to store the prime factors
# after dividing by the smallest prime
# factor at every step
def getFactorization(x):

    while (x != 1):
        temp = spf[x]
        if (x % temp == 0):

            # Storing the count of
            # prime factors in hash
            hash1[spf[x]] += 1
            x = x // spf[x]

        while (x % temp == 0):
            x = x // temp

# Function that returns true if there
# are no common prime factors between x
# and other numbers of the array
def check(x):

    while (x != 1):
        temp = spf[x]

        # Checking whether it common
        # prime factor with other numbers
        if (x % temp == 0 and hash1[temp] > 1):
            return False
        while (x % temp == 0):
            x = x //temp

    return True

# Function that returns true if there is
# an element in the array which is coprime
# with all the other elements of the array
def hasValidNum(arr, n):

    # Using sieve for generating
    # prime factors
    sieve()

    for i in range(n):
        getFactorization(arr[i])

    # Checking the common prime factors
    # with other numbers
    for i in range(n):
        if (check(arr[i])):
            return True

    return False

# Driver code
arr = [2, 8, 4, 10, 6, 7]
n = len(arr)

if (hasValidNum(arr, n)):
    print("Yes")
else:
    print("No")

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAXN=1000001;

// Stores smallest prime factor for every number
static int[] spf = new int[MAXN];

// Hash to store prime factors count
static int[] hash1 = new int[MAXN];

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
static void sieve()
{
    spf[1] = 1;
    for (int i = 2; i < MAXN; i++)

        // Marking smallest prime factor for every
        // number to be itself
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for (int i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    // Checking if i is prime
    for (int i = 3; i * i < MAXN; i++)
    {

        // Marking SPF for all numbers divisible by i
        if (spf[i] == i)
        {
            for (int j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to store the prime factors after dividing
// by the smallest prime factor at every step
static void getFactorization(int x)
{
    int temp;
    while (x != 1)
    {
        temp = spf[x];
        if (x % temp == 0)
        {

            // Storing the count of
            // prime factors in hash
            hash1[spf[x]]++;
            x = x / spf[x];
        }
        while (x % temp == 0)
            x = x / temp;
    }
}

// Function that returns true if there are
// no common prime factors between x
// and other numbers of the array
static bool check(int x)
{
    int temp;
    while (x != 1)
    {
        temp = spf[x];

        // Checking whether it common
        // prime factor with other numbers
        if (x % temp == 0 && hash1[temp] > 1)
            return false;
        while (x % temp == 0)
            x = x / temp;
    }
    return true;
}

// Function that returns true if there is
// an element in the array which is coprime
// with all the other elements of the array
static bool hasValidNum(int []arr, int n)
{

    // Using sieve for generating prime factors
    sieve();

    for (int i = 0; i < n; i++)
        getFactorization(arr[i]);

    // Checking the common prime factors
    // with other numbers
    for (int i = 0; i < n; i++)
        if (check(arr[i]))
            return true;

    return false;
}

// Driver code
static void Main()
{
    int []arr = { 2, 8, 4, 10, 6, 7 };
    int n = arr.Length;

    if (hasValidNum(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MAXN = 10001;

// Stores smallest prime factor for every number
$spf = array_fill(0, $MAXN, 0);

// Hash to store prime factors count
$hash1 = array_fill(0, $MAXN, 0);

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
function sieve()
{
    global $spf, $MAXN, $hash1;
    $spf[1] = 1;
    for ($i = 2; $i < $MAXN; $i++)

        // Marking smallest prime factor for every
        // number to be itself
        $spf[$i] = $i;

    // Separately marking spf for every even
    // number as 2
    for ($i = 4; $i < $MAXN; $i += 2)
        $spf[$i] = 2;

    // Checking if i is prime
    for ($i = 3; $i * $i < $MAXN; $i++)
    {

        // Marking SPF for all numbers divisible by i
        if ($spf[$i] == $i)
        {
            for ($j = $i * $i; $j < $MAXN; $j += $i)

                // Marking spf[j] if it is not
                // previously marked
                if ($spf[$j] == $j)
                    $spf[$j] = $i;
        }
    }
}

// Function to store the prime factors after dividing
// by the smallest prime factor at every step
function getFactorization($x)
{
    global $spf,$MAXN,$hash1;
    while ($x != 1)
    {
        $temp = $spf[$x];
        if ($x % $temp == 0)
        {

            // Storing the count of
            // prime factors in hash
            $hash1[$spf[$x]]++;
            $x = (int)($x / $spf[$x]);
        }
        while ($x % $temp == 0)
            $x = (int)($x / $temp);
    }
}

// Function that returns true if there are
// no common prime factors between x
// and other numbers of the array
function check($x)
{
    global $spf,$MAXN,$hash1;
    while ($x != 1)
    {
        $temp = $spf[$x];

        // Checking whether it common
        // prime factor with other numbers
        if ($x % $temp == 0 && $hash1[$temp] > 1)
            return false;
        while ($x % $temp == 0)
            $x = (int)($x / $temp);
    }
    return true;
}

// Function that returns true if there is
// an element in the array which is coprime
// with all the other elements of the array
function hasValidNum($arr, $n)
{
    global $spf,$MAXN,$hash1;

    // Using sieve for generating prime factors
    sieve();

    for ($i = 0; $i < $n; $i++)
        getFactorization($arr[$i]);

    // Checking the common prime factors
    // with other numbers
    for ($i = 0; $i < $n; $i++)
        if (check($arr[$i]))
            return true;

    return false;
}

// Driver code
    $arr = array( 2, 8, 4, 10, 6, 7 );
    $n = count($arr);

    if (hasValidNum($arr, $n))
        echo "Yes";
    else
        echo "No";

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let MAXN = 1000001;

// Stores smallest prime factor for every number
let spf = new Array(MAXN);

// Hash to store prime factors count
let hash1 = new Array(MAXN);

// Function to calculate SPF (Smallest Prime Factor)
// for every number till MAXN
function sieve()
{
    spf[1] = 1;
    for(let i = 2; i < MAXN; i++)

        // Marking smallest prime factor for
        // every number to be itself
        spf[i] = i;

    // Separately marking spf for every even
    // number as 2
    for(let i = 4; i < MAXN; i += 2)
        spf[i] = 2;

    // Checking if i is prime
    for(let i = 3; i * i < MAXN; i++)
    {

        // Marking SPF for all numbers divisible by i
        if (spf[i] == i)
        {
            for(let j = i * i; j < MAXN; j += i)

                // Marking spf[j] if it is not
                // previously marked
                if (spf[j] == j)
                    spf[j] = i;
        }
    }
}

// Function to store the prime factors
// after dividing by the smallest prime
// factor at every step
function getFactorization(x)
{
    let temp;
    while (x != 1)
    {
        temp = spf[x];
        if (x % temp == 0)
        {

            // Storing the count of
            // prime factors in hash
            hash1[spf[x]]++;
            x = x / spf[x];
        }
        while (x % temp == 0)
            x = x / temp;
    }
}

// Function that returns true if there are
// no common prime factors between x
// and other numbers of the array
function check(x)
{
    let temp;
    while (x != 1)
    {
        temp = spf[x];

        // Checking whether it common
        // prime factor with other numbers
        if (x % temp == 0 && hash1[temp] > 1)
            return false;

        while (x % temp == 0)
            x = x / temp;
    }
    return true;
}

// Function that returns true if there is
// an element in the array which is coprime
// with all the other elements of the array
function hasValidNum(arr, n)
{

    // Using sieve for generating prime factors
    sieve();

    for(let i = 0; i < n; i++)
        getFactorization(arr[i]);

    // Checking the common prime factors
    // with other numbers
    for(let i = 0; i < n; i++)
        if (check(arr[i]))
            return true;

    return false;
}

// Driver code
let arr = [ 2, 8, 4, 10, 6, 7 ];
let n = arr.length;

if (hasValidNum(arr, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Yes
```