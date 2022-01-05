# 可被数组所有元素整除的最小完美立方体

> 原文:[https://www . geeksforgeeks . org/最小完美立方体-可被数组所有元素整除/](https://www.geeksforgeeks.org/smallest-perfect-cube-divisible-by-all-elements-of-an-array/)

给定一个数组**arr【】**，任务是找到能被给定数组的所有元素整除的最小完美立方体。
**例:**

> **输入:** arr[] = {20，4，128，7}
> **输出:** 21952000
> **输入:** arr[] = {10，125，14，42，100}
> **输出:** 9261000

**天真方法:**从 1 开始逐个检查所有完美立方体，选择能被数组所有元素整除的立方体。
**有效方法:**找到数组中所有元素的[最小公倍数](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/)，并将其存储在变量 **lcm** 中。找到找到的 LCM 的所有质因数。
现在对于每个质因数**事实**，其**除以 lcm 'x '的次数**，其中 **x % 3！= 0** :

*   如果 **x % 3 = 2** 则更新 **lcm = lcm *事实**。
*   如果 **x % 3 = 1** 则更新 **lcm = lcm *事实 <sup>2</sup> 。**

最后打印**更新后的 LCM** 。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long int

// Function to return the gcd of two numbers
ll gcd(ll a, ll b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to return the lcm of
// all the elements of the array
ll lcmOfArray(int arr[], int n)
{
    if (n < 1)
        return 0;

    ll lcm = arr[0];

    // To calculate lcm of two numbers
    // multiply them and divide the result
    // by gcd of both the numbers
    for (int i = 1; i < n; i++)
        lcm = (lcm * arr[i]) / gcd(lcm, arr[i]);

    // Return the LCM of the array elements
    return lcm;
}

// Function to return the smallest perfect cube
// divisible by all the elements of arr[]
int minPerfectCube(int arr[], int n)
{
    ll minPerfectCube;

    // LCM of all the elements of arr[]
    ll lcm = lcmOfArray(arr, n);
    minPerfectCube = (long long)lcm;

    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0) {
        cnt++;
        lcm /= 2;
    }

    // If 2 divides lcm cnt number of times
    if (cnt % 3 == 2)
        minPerfectCube *= 2;
    else if (cnt % 3 == 1)
        minPerfectCube *= 4;

    int i = 3;

    // Check all the numbers that divide lcm
    while (lcm > 1) {
        cnt = 0;
        while (lcm % i == 0) {
            cnt++;
            lcm /= i;
        }

        if (cnt % 3 == 1)
            minPerfectCube *= i * i;
        else if (cnt % 3 == 2)
            minPerfectCube *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectCube;
}

// Driver code
int main()
{
    int arr[] = { 10, 125, 14, 42, 100 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minPerfectCube(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to return the lcm of
// aint the elements of the array
static int lcmOfArray(int arr[], int n)
{
    if (n < 1)
        return 0;

    int lcm = arr[0];

    // To calculate lcm of two numbers
    // multiply them and divide the result
    // by gcd of both the numbers
    for (int i = 1; i < n; i++)
        lcm = (lcm * arr[i]) / gcd(lcm, arr[i]);

    // Return the LCM of the array elements
    return lcm;
}

// Function to return the smaintest perfect cube
// divisible by aint the elements of arr[]
static int minPerfectCube(int arr[], int n)
{
    int minPerfectCube;

    // LCM of all the elements of arr[]
    int lcm = lcmOfArray(arr, n);
    minPerfectCube = lcm;

    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0)
    {
        cnt++;
        lcm /= 2;
    }

    // If 2 divides lcm cnt number of times
    if (cnt % 3 == 2)
        minPerfectCube *= 2;
    else if (cnt % 3 == 1)
        minPerfectCube *= 4;

    int i = 3;

    // Check aint the numbers that divide lcm
    while (lcm > 1)
    {
        cnt = 0;
        while (lcm % i == 0)
        {
            cnt++;
            lcm /= i;
        }

        if (cnt % 3 == 1)
            minPerfectCube *= i * i;
        else if (cnt % 3 == 2)
            minPerfectCube *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectCube;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 10, 125, 14, 42, 100 };
    int n = arr.length;
    System.out.println(minPerfectCube(arr, n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the gcd of two numbers
def gcd(a, b) :

    if (b == 0) :
        return a
    else :
        return gcd(b, a % b)

# Function to return the lcm of
# all the elements of the array
def lcmOfArray(arr, n) :

    if (n < 1) :
        return 0

    lcm = arr[0]

    # To calculate lcm of two numbers
    # multiply them and divide the result
    # by gcd of both the numbers
    for i in range(n) :
        lcm = (lcm * arr[i]) // gcd(lcm, arr[i]);

    # Return the LCM of the array elements
    return lcm

# Function to return the smallest perfect cube
# divisible by all the elements of arr[]
def minPerfectCube(arr, n) :

    # LCM of all the elements of arr[]
    lcm = lcmOfArray(arr, n)
    minPerfectCube = lcm

    cnt = 0
    while (lcm > 1 and lcm % 2 == 0) :
        cnt += 1
        lcm //= 2

    # If 2 divides lcm cnt number of times
    if (cnt % 3 == 2) :
        minPerfectCube *= 2

    elif (cnt % 3 == 1) :
        minPerfectCube *= 4

    i = 3

    # Check all the numbers that divide lcm
    while (lcm > 1) :
        cnt = 0

        while (lcm % i == 0) :
            cnt += 1
            lcm //= i

        if (cnt % 3 == 1) :
            minPerfectCube *= i * i

        elif (cnt % 3 == 2) :
            minPerfectCube *= i

        i += 2

    # Return the answer
    return minPerfectCube

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 125, 14, 42, 100 ]

    n = len(arr)
    print(minPerfectCube(arr, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to return the lcm of
// aint the elements of the array
static int lcmOfArray(int []arr, int n)
{
    if (n < 1)
        return 0;

    int lcm = arr[0];

    // To calculate lcm of two numbers
    // multiply them and divide the result
    // by gcd of both the numbers
    for (int i = 1; i < n; i++)
        lcm = (lcm * arr[i]) / gcd(lcm, arr[i]);

    // Return the LCM of the array elements
    return lcm;
}

// Function to return the smaintest perfect cube
// divisible by aint the elements of arr[]
static int minPerfectCube(int []arr, int n)
{
    int minPerfectCube;

    // LCM of all the elements of arr[]
    int lcm = lcmOfArray(arr, n);
    minPerfectCube = lcm;

    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0)
    {
        cnt++;
        lcm /= 2;
    }

    // If 2 divides lcm cnt number of times
    if (cnt % 3 == 2)
        minPerfectCube *= 2;
    else if (cnt % 3 == 1)
        minPerfectCube *= 4;

    int i = 3;

    // Check aint the numbers that divide lcm
    while (lcm > 1)
    {
        cnt = 0;
        while (lcm % i == 0)
        {
            cnt++;
            lcm /= i;
        }

        if (cnt % 3 == 1)
            minPerfectCube *= i * i;
        else if (cnt % 3 == 2)
            minPerfectCube *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectCube;
}

// Driver code
public static void Main()
{
    int []arr = { 10, 125, 14, 42, 100 };
    int n = arr.Length;
    Console.WriteLine(minPerfectCube(arr, n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the gcd of two numbers
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    else
        return gcd($b, $a % $b);
}

// Function to return the lcm of
// all the elements of the array
function lcmOfArray(&$arr, $n)
{
    if ($n < 1)
        return 0;

    $lcm = $arr[0];

    // To calculate lcm of two numbers
    // multiply them and divide the result
    // by gcd of both the numbers
    for ($i = 1; $i < $n; $i++)
        $lcm = ($lcm * $arr[$i]) /
            gcd($lcm, $arr[$i]);

    // Return the LCM of the array elements
    return $lcm;
}

// Function to return the smallest perfect cube
// divisible by all the elements of arr[]
function minPerfectCube(&$arr, $n)
{

    // LCM of all the elements of arr[]
    $lcm = lcmOfArray($arr, $n);
    $minPerfectCube = $lcm;

    $cnt = 0;
    while ($lcm > 1 && $lcm % 2 == 0)
    {
        $cnt++;
        $lcm /= 2;
    }

    // If 2 divides lcm cnt number of times
    if ($cnt % 3 == 2)
        $minPerfectCube *= 2;
    else if ($cnt % 3 == 1)
        $minPerfectCube *= 4;

    $i = 3;

    // Check all the numbers that divide lcm
    while ($lcm > 1)
    {
        $cnt = 0;
        while ($lcm % $i == 0)
        {
            $cnt++;
            $lcm /= $i;
        }

        if ($cnt % 3 == 1)
            $minPerfectCube *= $i * $i;
        else if ($cnt % 3 == 2)
            $minPerfectCube *= $i;

        $i += 2;
    }

    // Return the answer
    return $minPerfectCube;
}

// Driver code
$arr = array(10, 125, 14, 42, 100 );
$n = sizeof($arr);
echo(minPerfectCube($arr, $n));

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the gcd of two numbers
function gcd(a, b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to return the lcm of
// all the elements of the array
function lcmOfArray(arr, n)
{
    if (n < 1)
        return 0;

    let lcm = arr[0];

    // To calculate lcm of two numbers
    // multiply them and divide the result
    // by gcd of both the numbers
    for (let i = 1; i < n; i++)
        lcm = parseInt((lcm * arr[i]) / gcd(lcm, arr[i]));

    // Return the LCM of the array elements
    return lcm;
}

// Function to return the smallest perfect cube
// divisible by all the elements of arr[]
function minPerfectCube(arr, n)
{
    let minPerfectCube;

    // LCM of all the elements of arr[]
    let lcm = lcmOfArray(arr, n);
    minPerfectCube = lcm;

    let cnt = 0;
    while (lcm > 1 && lcm % 2 == 0) {
        cnt++;
        lcm = parseInt(lcm/2);
    }

    // If 2 divides lcm cnt number of times
    if (cnt % 3 == 2)
        minPerfectCube *= 2;
    else if (cnt % 3 == 1)
        minPerfectCube *= 4;

    let i = 3;

    // Check all the numbers that divide lcm
    while (lcm > 1) {
        cnt = 0;
        while (lcm % i == 0) {
            cnt++;
            lcm = parseInt(lcm/i);
        }

        if (cnt % 3 == 1)
            minPerfectCube *= i * i;
        else if (cnt % 3 == 2)
            minPerfectCube *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectCube;
}

// Driver code
let arr = [ 10, 125, 14, 42, 100 ];
let n = arr.length;
document.write(minPerfectCube(arr, n));

</script>
```

**Output:** 

```
9261000
```

***时间复杂度:** O(n * log(arr[i])*

***辅助空间:** O(1)*