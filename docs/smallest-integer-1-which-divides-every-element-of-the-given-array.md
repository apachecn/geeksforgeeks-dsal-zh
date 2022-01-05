# 最小整数> 1，用于划分给定数组的每个元素

> 原文:[https://www . geeksforgeeks . org/最小整数 1 除以给定数组的每个元素/](https://www.geeksforgeeks.org/smallest-integer-1-which-divides-every-element-of-the-given-array/)

给定一个数组 **arr[]** ，任务是找到一个最小的整数(除了 1)来划分给定数组的每个元素。

**示例:**

> **输入:** arr[] = { 2，4，8 }
> **输出:** 2
> 2 是分割整个数组的最小可能数。
> 
> **输入:** arr[] = { 4，7，5 }
> **输出:** -1
> 除了 1，没有整数可以分割整个数组。

**方法:**我们知道整个数组的 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 将会是**最大整数**来划分数组的每个元素。如果 **GCD = 1** ，那么没有整数可以分割整个数组。然而，如果 **GCD > 1** 则存在整数，该整数完全划分数组。例如，

> 如果 **GCD = 36** ，那么
> 36 将整个数组进行划分。
> 18 分整阵。
> 十二分全阵。
> 9 除全阵。
> ……
> 1 分割整个阵列。
> 这样，我们看到 36 的所有因子也划分数组。36 的**最小质因数**即 2 是划分整个数组的最小可能整数。因此，我们需要找到 [**GCD**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 的 [**最小质因数**](https://www.geeksforgeeks.org/smallest-prime-divisor-of-a-number/) **作为所需答案。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest divisor
int smallestDivisor(int x)
{
    // if divisible by 2
    if (x % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3; i * i <= x; i += 2) {
        if (x % i == 0)
            return i;
    }

    return x;
}

// Function to return smallest possible integer
// which divides the whole array
int smallestInteger(int* arr, int n)
{
    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return smallestDivisor(gcd);
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << smallestInteger(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to find the smallest divisor
static int smallestDivisor(int x)
{
    // if divisible by 2
    if (x % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3; i * i <= x; i += 2)
    {
        if (x % i == 0)
            return i;
    }

    return x;
}

// Function to return smallest possible integer
// which divides the whole array
static int smallestInteger(int []arr, int n)
{
    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return smallestDivisor(gcd);
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 2, 4, 8 };
    int n = arr.length;
    System.out.println(smallestInteger(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt, gcd

# Function to find the smallest divisor
def smallestDivisor(x) :

    # if divisible by 2
    if (x % 2 == 0) :
        return 2;

    # iterate from 3 to sqrt(n)
    for i in range(3, int(sqrt(x)) + 1, 2) :
        if (x % i == 0) :
            return i;

    return x

# Function to return smallest possible
# integer which divides the whole array
def smallestInteger(arr, n) :

    # To store the GCD of all the
    # array elements
    __gcd = 0;
    for i in range(n) :
        __gcd = gcd(__gcd, arr[i]);

    # Return the smallest prime factor
    # of the gcd calculated
    return smallestDivisor(__gcd);

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 4, 8 ];
    n = len(arr);

    print(smallestInteger(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to find the smallest divisor
static int smallestDivisor(int x)
{
    // if divisible by 2
    if (x % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for (int i = 3; i * i <= x; i += 2)
    {
        if (x % i == 0)
            return i;
    }

    return x;
}

// Function to return smallest possible integer
// which divides the whole array
static int smallestInteger(int []arr, int n)
{
    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return smallestDivisor(gcd);
}

// Driver code
static void Main()
{
    int []arr = { 2, 4, 8 };
    int n = arr.Length;
    Console.WriteLine(smallestInteger(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
function gcd($a, $b)
{
    // Everything divides 0
    if($b == 0)
        return $a;

    return gcd($b , $a % $b);
}

// Function to find the smallest divisor
function smallestDivisor($x)
{
    // if divisible by 2
    if ($x % 2 == 0)
        return 2;

    // iterate from 3 to sqrt(n)
    for ($i = 3; $i < sqrt($x) + 1; $i += 2)
    {
        if ($x % $i == 0)
            return $i;
    }
    return $x;
}

// Function to return smallest possible
// integer which divides the whole array
function smallestInteger($arr, $n)
{

    // To store the GCD of all the
    // array elements
    $__gcd = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $__gcd = gcd($__gcd, $arr[$i]);
    }

    // Return the smallest prime factor
    // of the gcd calculated
    return smallestDivisor($__gcd);
}

// Driver code
$arr = array(2, 4, 8);
$n = count($arr);

echo smallestInteger($arr, $n);

// This code is contributed by Srathore
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach
    function __gcd(a, b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);

    }

    // Function to find the smallest divisor
    function smallestDivisor(x)
    {
        // if divisible by 2
        if (x % 2 == 0)
            return 2;

        // iterate from 3 to sqrt(n)
        for (let i = 3; i * i <= x; i += 2)
        {
            if (x % i == 0)
                return i;
        }

        return x;
    }

    // Function to return smallest possible integer
    // which divides the whole array
    function smallestInteger(arr, n)
    {

        // To store the GCD of all the array elements
        let gcd = 0;
        for (let i = 0; i < n; i++)
            gcd = __gcd(gcd, arr[i]);

        // Return the smallest prime factor
        // of the gcd calculated
        return smallestDivisor(gcd);
    }

    let arr = [ 2, 4, 8 ];
    let n = arr.length;
    document.write(smallestInteger(arr, n));

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```

对于多个查询，我们可以使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)将数字的最小质因数预计算到最大值。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100005;

// To store the smallest prime factor
int spf[MAX];

// Function to store spf of integers
void sieve()
{
    memset(spf, 0, sizeof(spf));
    spf[0] = 1;

    // When gcd is 1 then the answer is -1
    spf[1] = -1;
    for (int i = 2; i * i < MAX; i++) {
        if (spf[i] == 0) {
            for (int j = i * 2; j < MAX; j += i) {
                if (spf[j] == 0) {
                    spf[j] = i;
                }
            }
        }
    }
    for (int i = 2; i < MAX; i++) {
        if (!spf[i])
            spf[i] = i;
    }
}

// Function to return smallest possible integer
// which divides the whole array
int smallestInteger(int* arr, int n)
{

    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return spf[gcd];
}

// Driver code
int main()
{
    sieve();
    int arr[] = { 2, 4, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << smallestInteger(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int MAX = 100005;

// To store the smallest prime factor
static int spf[] = new int[MAX];

// Function to store spf of integers
static void sieve()
{
    spf[0] = 1;

    // When gcd is 1 then the answer is -1
    spf[1] = -1;
    for (int i = 2; i * i < MAX; i++)
    {
        if (spf[i] == 0)
        {
            for (int j = i * 2; j < MAX; j += i)
            {
                if (spf[j] == 0)
                {
                    spf[j] = i;
                }
            }
        }
    }
    for (int i = 2; i < MAX; i++)
    {
        if (spf[i] != 1)
            spf[i] = i;
    }
}

// Function to return smallest possible integer
// which divides the whole array
static int smallestInteger(int[] arr, int n)
{

    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return spf[gcd];
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver code
public static void main(String[] args)
{
    sieve();
    int arr[] = { 2, 4, 8 };
    int n = arr.length;
    System.out.println(smallestInteger(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 10005;

# To store the smallest prime factor
spf = [0] * MAX;

# Function to store spf of integers
def sieve():

    spf[0] = 1;

    # When gcd is 1 then the answer is -1
    spf[1] = -1;
    i = 2;
    while (i * i < MAX):
        if (spf[i] == 0):
            for j in range(i * 2, MAX, i):
                if (spf[j] == 0):
                    spf[j] = i;
        i += 1;

    for i in range(2, MAX):
        if (spf[i] == 0):
            spf[i] = i;

# find gcd of two no
def __gcd(a, b):
    if (b == 0):
        return a;
    return __gcd(b, a % b);

# Function to return smallest possible integer
# which divides the whole array
def smallestInteger(arr, n):

    # To store the GCD of all the array elements
    gcd = 0;
    for i in range(n):
        gcd = __gcd(gcd, arr[i]);

    # Return the smallest prime factor
    # of the gcd calculated
    return spf[gcd];

# Driver code
sieve();
arr = [ 2, 4, 8 ];
n = len(arr);
print(smallestInteger(arr, n));

# This code is contributed by mits
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

static int MAX = 100005;

// To store the smallest prime factor
static int []spf = new int[MAX];

// Function to store spf of integers
static void sieve()
{
    spf[0] = 1;

    // When gcd is 1 then the answer is -1
    spf[1] = -1;
    for (int i = 2; i * i < MAX; i++)
    {
        if (spf[i] == 0)
        {
            for (int j = i * 2; j < MAX; j += i)
            {
                if (spf[j] == 0)
                {
                    spf[j] = i;
                }
            }
        }
    }
    for (int i = 2; i < MAX; i++)
    {
        if (spf[i] != 1)
            spf[i] = i;
    }
}

// Function to return smallest possible integer
// which divides the whole array
static int smallestInteger(int[] arr, int n)
{

    // To store the GCD of all the array elements
    int gcd = 0;
    for (int i = 0; i < n; i++)
        gcd = __gcd(gcd, arr[i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return spf[gcd];
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver code
public static void Main(String[] args)
{
    sieve();
    int []arr = { 2, 4, 8 };
    int n = arr.Length;
    Console.WriteLine(smallestInteger(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MAX = 10005;

// To store the smallest prime factor
$spf = array_fill(0, $MAX, 0);

// Function to store spf of integers
function sieve()
{
    global $spf, $MAX;
    $spf[0] = 1;

    // When gcd is 1 then the answer is -1
    $spf[1] = -1;
    for ($i = 2; $i * $i < $MAX; $i++)
    {
        if ($spf[$i] == 0)
        {
            for ($j = $i * 2; $j < $MAX; $j += $i)
            {
                if ($spf[$j] == 0)
                {
                    $spf[$j] = $i;
                }
            }
        }
    }
    for ($i = 2; $i < $MAX; $i++)
    {
        if (!$spf[$i])
            $spf[$i] = $i;
    }
}

// find gcd of two no
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);

}

// Function to return smallest possible integer
// which divides the whole array
function smallestInteger($arr, $n)
{
    global $spf, $MAX;

    // To store the GCD of all the array elements
    $gcd = 0;
    for ($i = 0; $i < $n; $i++)
        $gcd = __gcd($gcd, $arr[$i]);

    // Return the smallest prime factor
    // of the gcd calculated
    return $spf[$gcd];
}

// Driver code
sieve();
$arr = array( 2, 4, 8 );
$n = count($arr);
echo smallestInteger($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    let MAX = 100005;

    // To store the smallest prime factor
    let spf = new Array(MAX);

    // Function to store spf of integers
    function sieve()
    {
        spf[0] = 1;

        // When gcd is 1 then the answer is -1
        spf[1] = -1;
        for (let i = 2; i * i < MAX; i++)
        {
            if (spf[i] == 0)
            {
                for (let j = i * 2; j < MAX; j += i)
                {
                    if (spf[j] == 0)
                    {
                        spf[j] = i;
                    }
                }
            }
        }
        for (let i = 2; i < MAX; i++)
        {
            if (spf[i] != 1)
                spf[i] = i;
        }
    }

    // Function to return smallest possible integer
    // which divides the whole array
    function smallestInteger(arr, n)
    {

        // To store the GCD of all the array elements
        let gcd = 0;
        for (let i = 0; i < n; i++)
            gcd = __gcd(gcd, arr[i]);

        // Return the smallest prime factor
        // of the gcd calculated
        return spf[gcd];
    }

    function __gcd(a, b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);   
    }

    sieve();
    let arr = [ 2, 4, 8 ];
    let n = arr.length;
    document.write(smallestInteger(arr, n));

</script>
```

**Output:** 

```
2
```