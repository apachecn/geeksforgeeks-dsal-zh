# 可被数组所有元素整除的最小完美正方形

> 原文:[https://www . geeksforgeeks . org/最小完美平方可被数组的所有元素整除/](https://www.geeksforgeeks.org/smallest-perfect-square-divisible-by-all-elements-of-an-array/)

给定一个数组**arr【】**，任务是找到能被给定数组的所有元素整除的最小完美平方。
**例:**

> **输入:** arr[] = {2，3，4，5，7}
> **输出:** 44100
> **输入:** arr[] = {20，25，14，21，100，18，42，16，55}
> **输出:** 21344400

**天真方法:**逐个检查从 1 开始的所有平方数，选择能被数组所有元素整除的一个。
**有效方法:**找到数组中所有元素的[最小公倍数](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/)，并将其存储在变量 **lcm** 中。找到找到的 LCM 的所有质因数。
现在检查是否有**质因数****除以 lcm 奇数次**。如果有这些因素，**将 LCM 乘以这些因素**。最后打印**更新后的 LCM** 。
以下是上述方法的实施:

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

// Function to return the smallest perfect square
// divisible by all the elements of arr[]
int minPerfectSquare(int arr[], int n)
{
    ll minPerfectSq;

    // LCM of all the elements of arr[]
    ll lcm = lcmOfArray(arr, n);
    minPerfectSq = (long long)lcm;

    // Check if 2 divides lcm odd number of times
    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0) {
        cnt++;
        lcm /= 2;
    }
    if (cnt % 2 != 0)
        minPerfectSq *= 2;

    int i = 3;

    // Check all the numbers that divide lcm
    // odd number of times
    while (lcm > 1) {
        cnt = 0;
        while (lcm % i == 0) {
            cnt++;
            lcm /= i;
        }

        // If i divided lcm odd number of times
        // then multiply the lcm with i
        if (cnt % 2 != 0)
            minPerfectSq *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectSq;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minPerfectSquare(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class solution
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
// all the elements of the array
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

// Function to return the smallest perfect square
// divisible by all the elements of arr[]
static int minPerfectSquare(int arr[], int n)
{
    int minPerfectSq;

    // LCM of all the elements of arr[]
    int lcm = lcmOfArray(arr, n);
    minPerfectSq = (int)lcm;

    // Check if 2 divides lcm odd number of times
    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0) {
        cnt++;
        lcm /= 2;
    }
    if (cnt % 2 != 0)
        minPerfectSq *= 2;

    int i = 3;

    // Check all the numbers that divide lcm
    // odd number of times
    while (lcm > 1) {
        cnt = 0;
        while (lcm % i == 0) {
            cnt++;
            lcm /= i;
        }

        // If i divided lcm odd number of times
        // then multiply the lcm with i
        if (cnt % 2 != 0)
            minPerfectSq *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectSq;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 2, 3, 4, 5, 7 };
    int n = arr.length;
    System.out.println(minPerfectSquare(arr, n));

}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import gcd

# Function to return the lcm of
# all the elements of the array
def lcmOfArray(arr, n):
    if (n < 1):
        return 0

    lcm = arr[0]

    # To calculate lcm of two numbers
    # multiply them and divide the result
    # by gcd of both the numbers
    for i in range(1, n, 1):
        lcm = int((lcm * arr[i]) /
               gcd(lcm, arr[i]))

    # Return the LCM of the array elements
    return lcm

# Function to return the smallest perfect
# square divisible by all the elements of arr[]
def minPerfectSquare(arr, n):

    # LCM of all the elements of arr[]
    lcm = lcmOfArray(arr, n)
    minPerfectSq = int(lcm)

    # Check if 2 divides lcm odd
    # number of times
    cnt = 0
    while (lcm > 1 and lcm % 2 == 0):
        cnt += 1
        lcm /= 2

    if (cnt % 2 != 0):
        minPerfectSq *= 2

    i = 3

    # Check all the numbers that divide
    # lcm odd number of times
    while (lcm > 1):
        cnt = 0;
        while (lcm % i == 0):
            cnt += 1
            lcm /= i

        # If i divided lcm odd number of
        # times then multiply the lcm with i
        if (cnt % 2 != 0):
            minPerfectSq *= i

        i += 2

    # Return the answer
    return minPerfectSq

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 4, 5, 7]
    n = len(arr)
    print(minPerfectSquare(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

public class GFG{

// Function to return the gcd of two numbers
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Function to return the lcm of
// all the elements of the array
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

// Function to return the smallest perfect square
// divisible by all the elements of arr[]
static int minPerfectSquare(int []arr, int n)
{
    int minPerfectSq;

    // LCM of all the elements of arr[]
    int lcm = lcmOfArray(arr, n);
    minPerfectSq = (int)lcm;

    // Check if 2 divides lcm odd number of times
    int cnt = 0;
    while (lcm > 1 && lcm % 2 == 0) {
        cnt++;
        lcm /= 2;
    }
    if (cnt % 2 != 0)
        minPerfectSq *= 2;

    int i = 3;

    // Check all the numbers that divide lcm
    // odd number of times
    while (lcm > 1) {
        cnt = 0;
        while (lcm % i == 0) {
            cnt++;
            lcm /= i;
        }

        // If i divided lcm odd number of times
        // then multiply the lcm with i
        if (cnt % 2 != 0)
            minPerfectSq *= i;

        i += 2;
    }

    // Return the answer
    return minPerfectSq;
}

// Driver code
    static public void Main (){

    int []arr = { 2, 3, 4, 5, 7 };
    int n = arr.Length;
    Console.WriteLine(minPerfectSquare(arr, n));

    }
}
//This code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the gcd of
// two numbers
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    else
        return gcd($b, $a % $b);
}

// Function to return the lcm of
// all the elements of the array
function lcmOfArray($arr, $n)
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

// Function to return the smallest perfect
// square divisible by all the elements of arr[]
function minPerfectSquare($arr, $n)
{
    // LCM of all the elements of arr[]
    $lcm = lcmOfArray($arr, $n);
    $minPerfectSq = $lcm;

    // Check if 2 divides lcm odd
    // number of times
    $cnt = 0;
    while ($lcm > 1 && $lcm % 2 == 0)
    {
        $cnt++;
        $lcm = floor($lcm / 2);
    }
    if ($cnt % 2 != 0)
        $minPerfectSq *= 2;

    $i = 3;

    // Check all the numbers that divide
    // lcm odd number of times
    while ($lcm > 1)
    {
        $cnt = 0;
        while ($lcm % $i == 0)
        {
            $cnt++;
            $lcm = $lcm / $i;
        }

        // If i divided lcm odd number of times
        // then multiply the lcm with i
        if ($cnt % 2 != 0)
            $minPerfectSq *= $i;

        $i += 2;
    }

    // Return the answer
    return $minPerfectSq;
}

// Driver code
$arr = array( 2, 3, 4, 5, 7 );
$n = sizeof($arr);
echo minPerfectSquare($arr, $n);

// This code is contributed by Ryuga
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
            lcm = parseInt((lcm * arr[i]) / gcd(lcm, arr[i]), 10);

        // Return the LCM of the array elements
        return lcm;
    }

    // Function to return the smallest perfect square
    // divisible by all the elements of arr[]
    function minPerfectSquare(arr, n)
    {
        let minPerfectSq;

        // LCM of all the elements of arr[]
        let lcm = lcmOfArray(arr, n);
        minPerfectSq = lcm;

        // Check if 2 divides lcm odd number of times
        let cnt = 0;
        while (lcm > 1 && lcm % 2 == 0) {
            cnt++;
            lcm = parseInt(lcm / 2, 10);
        }
        if (cnt % 2 != 0)
            minPerfectSq *= 2;

        let i = 3;

        // Check all the numbers that divide lcm
        // odd number of times
        while (lcm > 1) {
            cnt = 0;
            while (lcm % i == 0) {
                cnt++;
                lcm = parseInt(lcm / i, 10);
            }

            // If i divided lcm odd number of times
            // then multiply the lcm with i
            if (cnt % 2 != 0)
                minPerfectSq *= i;

            i += 2;
        }

        // Return the answer
        return minPerfectSq;
    }

    let arr = [ 2, 3, 4, 5, 7 ];
    let n = arr.length;
    document.write(minPerfectSquare(arr, n));

</script>
```

**Output:** 

```
44100
```