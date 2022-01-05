# 一个数的三重除数相乘的和

> 原文:[https://www . geeksforgeeks . org/一个数的三重除数的乘法之和/](https://www.geeksforgeeks.org/sum-of-multiplication-of-triplet-of-divisors-of-a-number/)

给定大小为 **n** 的整数数组 **arr[]** 。对于每一个元素，你必须打印出用这个元素的除数构成的每一个三元组的乘法总和。
**例:**

> **输入:**arr[]= { 4 }
> T3】输出: 8
> 4 有三个除数 1、2 和 4。
> 1 * 2 * 4 = 8
> **输入:** arr[] = {9，5，6}
> **输出:** 27 0 72
> 9 有三个除数 1，3，9。1 * 3 * 9 = 27
> 5 有两个除数 1 和 5。所以，没有形成三元组。
> 同样，6 有 4 个除数 1、2、3 和 6。(1 * 2 * 3)+(1 * 3 * 6)+(2 * 3 * 6)+(1 * 6 * 2)= 72

**天真方法:**存储一个数的所有除数，应用蛮力方法，对于每个三元组，将这三个元素的乘积加到答案中。
**高效方法:**这个方法类似于厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)，我们用它来求一个范围的所有素数。

1.  首先，我们制作一个数组 sum1，它将数 x 的所有除数之和存储在 sum1[x]处。所以首先迭代所有小于 maximum_Element 的数，并将这个数加到这个数的倍数的除数之和。因此，我们将能够在任何数的位置存储该数的所有除数的和。
2.  填充 sum1 数组后，是时候填充第二个数组 sum2 了，它将存储 sum2[x]中每个数 x 对除数的乘积之和。为了填充这个，我们对每个类似于步骤 1 的数字进行运算，并将这个数字与它的较高值相乘。
3.  为了填充 sum3 数组，我们将对所有小于 max_Element 的数字进行类似的处理，并将 j 的除数相乘的和相加，使得 I 是 j 的除数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll max_Element = 1e6 + 5;

// Global array declaration
int sum1[max_Element], sum2[max_Element], sum3[max_Element];

// Function to find the sum of multiplication of
// every triplet in the divisors of a number
void precomputation(int arr[], int n)
{
    // sum1[x] represents the sum of all the divisors of x
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)

            // Adding i to sum1[j] because i
            // is a divisor of j
            sum1[j] += i;

    // sum2[x] represents the sum of all the divisors of x
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)

            // Here i is divisor of j and sum1[j] - i
            // represents sum of all divisors of
            // j which do not include i so we add
            // i * (sum1[j] - i) to sum2[j]
            sum2[j] += (sum1[j] - i) * i;

    // In the above implementation we have considered
    // every pair two times so we have to divide
    // every sum2 array element by 2
    for (int i = 1; i < max_Element; i++)
        sum2[i] /= 2;

    // Here i is the divisor of j and we are trying to
    // add the sum of multiplication of all triplets of
    // divisors of j such that one of the divisors is i
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)
            sum3[j] += i * (sum2[j] - i * (sum1[j] - i));

    // In the above implementation we have considered
    // every triplet three times so we have to divide
    // every sum3 array element by 3
    for (int i = 1; i < max_Element; i++)
        sum3[i] /= 3;

    // Print the results
    for (int i = 0; i < n; i++)
        cout << sum3[arr[i]] << " ";
}

// Driver code
int main()
{

    int arr[] = { 9, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Precomputing
    precomputation(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFGq
{

static int max_Element = (int) (1e6 + 5);

// Global array declaration
static int sum1[] = new int[max_Element], sum2[] =
        new int[max_Element], sum3[] = new int[max_Element];

// Function to find the sum of multiplication of
// every triplet in the divisors of a number
static void precomputation(int arr[], int n)
{
    // sum1[x] represents the sum of all the divisors of x
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)

            // Adding i to sum1[j] because i
            // is a divisor of j
            sum1[j] += i;

    // sum2[x] represents the sum of all the divisors of x
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)

            // Here i is divisor of j and sum1[j] - i
            // represents sum of all divisors of
            // j which do not include i so we add
            // i * (sum1[j] - i) to sum2[j]
            sum2[j] += (sum1[j] - i) * i;

    // In the above implementation we have considered
    // every pair two times so we have to divide
    // every sum2 array element by 2
    for (int i = 1; i < max_Element; i++)
        sum2[i] /= 2;

    // Here i is the divisor of j and we are trying to
    // add the sum of multiplication of all triplets of
    // divisors of j such that one of the divisors is i
    for (int i = 1; i < max_Element; i++)
        for (int j = i; j < max_Element; j += i)
            sum3[j] += i * (sum2[j] - i * (sum1[j] - i));

    // In the above implementation we have considered
    // every triplet three times so we have to divide
    // every sum3 array element by 3
    for (int i = 1; i < max_Element; i++)
        sum3[i] /= 3;

    // Print the results
    for (int i = 0; i < n; i++)
        System.out.print(sum3[arr[i]] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 9, 5, 6 };
    int n = arr.length;

    // Precomputing
    precomputation(arr, n);
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Global array declaration
#global max_Element
max_Element = 100005

sum1 = [0 for i in range(max_Element)]
sum2 = [0 for i in range(max_Element)]
sum3 = [0 for i in range(max_Element)]

# Function to find the sum of multiplication of
# every triplet in the divisors of a number
def precomputation(arr, n):

    # global max_Element
    # sum1[x] represents the sum of
    # all the divisors of x
    for i in range(1, max_Element, 1):
        for j in range(i, max_Element, i):

            # Adding i to sum1[j] because i
            # is a divisor of j
            sum1[j] += i

    # sum2[x] represents the sum of
    # all the divisors of x
    for i in range(1, max_Element, 1):
        for j in range(i, max_Element, i):

            # Here i is divisor of j and sum1[j] - i
            # represents sum of all divisors of
            # j which do not include i so we add
            # i * (sum1[j] - i) to sum2[j]
            sum2[j] += (sum1[j] - i) * i

    # In the above implementation we have considered
    # every pair two times so we have to divide
    # every sum2 array element by 2
    for i in range(1, max_Element, 1):
        sum2[i] = int(sum2[i] / 2)

    # Here i is the divisor of j and we are trying to
    # add the sum of multiplication of all triplets of
    # divisors of j such that one of the divisors is i
    for i in range(1, max_Element, 1):
        for j in range(i, max_Element, i):
            sum3[j] += i * (sum2[j] - i *
                           (sum1[j] - i))

    # In the above implementation we have considered
    # every triplet three times so we have to divide
    # every sum3 array element by 3
    for i in range(1, max_Element, 1):
        sum3[i] = int(sum3[i] / 3)

    # Print the results
    for i in range(n):
        print(sum3[arr[i]], end = " ")

# Driver code
if __name__ == '__main__':
    arr = [9, 5, 6]
    n = len(arr)

    # Precomputing
    precomputation(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int max_Element = (int) (1e6 + 5);

    // Global array declaration
    static int []sum1 = new int[max_Element];
    static int []sum2 = new int[max_Element];
    static int []sum3 = new int[max_Element];

    // Function to find the sum of multiplication of
    // every triplet in the divisors of a number
    static void precomputation(int []arr, int n)
    {
        // sum1[x] represents the sum of all the divisors of x
        for (int i = 1; i < max_Element; i++)
            for (int j = i; j < max_Element; j += i)

                // Adding i to sum1[j] because i
                // is a divisor of j
                sum1[j] += i;

        // sum2[x] represents the sum of all the divisors of x
        for (int i = 1; i < max_Element; i++)
            for (int j = i; j < max_Element; j += i)

                // Here i is divisor of j and sum1[j] - i
                // represents sum of all divisors of
                // j which do not include i so we add
                // i * (sum1[j] - i) to sum2[j]
                sum2[j] += (sum1[j] - i) * i;

        // In the above implementation we have considered
        // every pair two times so we have to divide
        // every sum2 array element by 2
        for (int i = 1; i < max_Element; i++)
            sum2[i] /= 2;

        // Here i is the divisor of j and we are trying to
        // add the sum of multiplication of all triplets of
        // divisors of j such that one of the divisors is i
        for (int i = 1; i < max_Element; i++)
            for (int j = i; j < max_Element; j += i)
                sum3[j] += i * (sum2[j] - i * (sum1[j] - i));

        // In the above implementation we have considered
        // every triplet three times so we have to divide
        // every sum3 array element by 3
        for (int i = 1; i < max_Element; i++)
            sum3[i] /= 3;

        // Print the results
        for (int i = 0; i < n; i++)
            Console.Write(sum3[arr[i]] + " ");
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 9, 5, 6 };
        int n = arr.Length;

        // Precomputing
        precomputation(arr, n);
    }
}

// This code has been contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$max_Element = 1005;

// Global array declaration
$sum1 = array_fill(0, $max_Element, 0);
$sum2 = array_fill(0, $max_Element, 0);
$sum3 = array_fill(0, $max_Element, 0);

// Function to find the sum of multiplication of
// every triplet in the divisors of a number
function precomputation($arr, $n)
{
    global $max_Element, $sum3, $sum2, $sum1;

    // sum1[x] represents the sum of
    // all the divisors of x
    for ($i = 1; $i < $max_Element; $i++)
        for ($j = $i; $j < $max_Element; $j += $i)

            // Adding i to sum1[j] because i
            // is a divisor of j
            $sum1[$j] += $i;

    // sum2[x] represents the sum of
    // all the divisors of x
    for ($i = 1; $i < $max_Element; $i++)
        for ($j = $i; $j < $max_Element; $j += $i)

            // Here i is divisor of j and sum1[j] - i
            // represents sum of all divisors of
            // j which do not include i so we add
            // i * (sum1[j] - i) to sum2[j]
            $sum2[$j] += ($sum1[$j] - $i) * $i;

    // In the above implementation we have considered
    // every pair two times so we have to divide
    // every sum2 array element by 2
    for ($i = 1; $i < $max_Element; $i++)
        $sum2[$i] = (int)($sum2[$i] / 2);

    // Here i is the divisor of j and we are trying to
    // add the sum of multiplication of all triplets of
    // divisors of j such that one of the divisors is i
    for ($i = 1; $i < $max_Element; $i++)
        for ($j = $i; $j < $max_Element; $j += $i)
            $sum3[$j] += $i * ($sum2[$j] - $i *
                              ($sum1[$j] - $i));

    // In the above implementation we have considered
    // every triplet three times so we have to divide
    // every sum3 array element by 3
    for ($i = 1; $i < $max_Element; $i++)
        $sum3[$i] = (int)($sum3[$i] / 3);

    // Print the results
    for ($i = 0; $i < $n; $i++)
        echo $sum3[$arr[$i]] . " ";
}

// Driver code
$arr = array( 9, 5, 6 );
$n = count($arr);

// Precomputing
precomputation($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

var max_Element = 1e6 + 5;

// Global array declaration
var sum1=new Array(max_Element).fill(0);
var sum2=new Array(max_Element).fill(0);
var sum3=new Array(max_Element).fill(0);

// Function to find the sum of multiplication of
// every triplet in the divisors of a number
function precomputation( arr, n)
{
    // sum1[x] represents the sum of all the divisors of x
    for (var i = 1; i < max_Element; i++)
        for (var j = i; j < max_Element; j += i)

            // Adding i to sum1[j] because i
            // is a divisor of j
            sum1[j] += i;

    // sum2[x] represents the sum of all the divisors of x
    for (var i = 1; i < max_Element; i++)
        for (var j = i; j < max_Element; j += i)

            // Here i is divisor of j and sum1[j] - i
            // represents sum of all divisors of
            // j which do not include i so we add
            // i * (sum1[j] - i) to sum2[j]
            sum2[j] += (sum1[j] - i) * i;

    // In the above implementation we have considered
    // every pair two times so we have to divide
    // every sum2 array element by 2
    for (var i = 1; i < max_Element; i++)
        sum2[i] /= 2;

    // Here i is the divisor of j and we are trying to
    // add the sum of multiplication of all triplets of
    // divisors of j such that one of the divisors is i
    for (var i = 1; i < max_Element; i++)
        for (var j = i; j < max_Element; j += i)
            sum3[j] += i * (sum2[j] - i * (sum1[j] - i));

    // In the above implementation we have considered
    // every triplet three times so we have to divide
    // every sum3 array element by 3
    for (var i = 1; i < max_Element; i++)
        sum3[i] /= 3;

    // Print the results
    for (var i = 0; i < n; i++)
        document.write( sum3[arr[i]] + " ");
}

    var arr=[9, 5, 6 ];
    var n =3;

    // Precomputing
    precomputation(arr, n);

</script>
```

**Output:** 

```
27 0 72
```