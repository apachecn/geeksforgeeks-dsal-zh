# 分数(或有理数)数组的 HCF

> 原文:[https://www . geeksforgeeks . org/hcf 分数或有理数数组/](https://www.geeksforgeeks.org/hcf-of-array-of-fractions-or-rational-numbers/)

给定一个分数序列。求给定分数系列的高频系数。
**例:**

```
Input : [{2, 5}, {8, 9}, {16, 81}, {10, 27}]
Output :  2, 405 
Explanation : 2/405 is the largest number that
divides all 2/5, 8/9, 16/81 and 10/27.

Input : [{9, 10}, {12, 25}, {18, 35}, {21, 40}]
Output : 3, 1400
```

**进场:**

> 找到记数器的高频。
> 求分母的 L.C.M。
> 计算高频/低频交流电的分数
> 将分数降低至最低分数。

## C++

```
// CPP program to find HCF of array of
// rational numbers (fractions).
#include <iostream>
using namespace std;

// hcf of two number
int gcd(int a, int b)
{
    if (a % b == 0)
        return b;
    else
        return (gcd(b, a % b));
}

// find hcf of numerator series
int findHcf(int** arr, int size)
{
    int ans = arr[0][0];   
    for (int i = 1; i < size; i++)   
        ans = gcd(ans, arr[i][0]);

    // return hcf of numerator
    return (ans);
}

// find lcm of denominator series
int findLcm(int** arr, int size)
{
    // ans contains LCM of arr[0][1], ..arr[i][1]
    int ans = arr[0][1];
    for (int i = 1; i < size; i++)
        ans = (((arr[i][1] * ans)) /
               (gcd(arr[i][1], ans)));

    // return lcm of denominator
    return (ans);
}

// Core Function
int* hcfOfFraction(int** arr, int size)
{
    // found hcf of numerator
    int hcf_of_num = findHcf(arr, size);

    // found lcm of denominator
    int lcm_of_deno = findLcm(arr, size);

    int* result = new int[2];
    result[0] = hcf_of_num;
    result[1] = lcm_of_deno;

    for (int i = result[0] / 2; i > 1; i--)
    {
        if ((result[1] % i == 0) && (result[0] % i == 0))
        {
            result[1] /= i;
            result[0] /= i;
        }
    }

    // return result
    return (result);
}

// Main function
int main()
{
    int size = 4;
    int** arr = new int*[size];

    // Initialize the every row
    // with size 2 (1 for numerator
    // and 2 for denominator)
    for (int i = 0; i < size; i++)
        arr[i] = new int[2];

    arr[0][0] = 9;
    arr[0][1] = 10;
    arr[1][0] = 12;
    arr[1][1] = 25;
    arr[2][0] = 18;
    arr[2][1] = 35;
    arr[3][0] = 21;
    arr[3][1] = 40;

    // function for calculate the result
    int* result = hcfOfFraction(arr, size);

    // print the result
    cout << result[0] << ", " << result[1] << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find HCF of array of
// rational numbers (fractions).
class GFG
{

// hcf of two number
static int gcd(int a, int b)
{
    if (a % b == 0)
        return b;
    else
        return (gcd(b, a % b));
}

// find hcf of numerator series
static int findHcf(int [][]arr, int size)
{
    int ans = arr[0][0];
    for (int i = 1; i < size; i++)
        ans = gcd(ans, arr[i][0]);

    // return hcf of numerator
    return (ans);
}

// find lcm of denominator series
static int findLcm(int[][] arr, int size)
{
    // ans contains LCM of arr[0][1], ..arr[i][1]
    int ans = arr[0][1];
    for (int i = 1; i < size; i++)
        ans = (((arr[i][1] * ans)) /
            (gcd(arr[i][1], ans)));

    // return lcm of denominator
    return (ans);
}

// Core Function
static int[] hcfOfFraction(int[][] arr, int size)
{
    // found hcf of numerator
    int hcf_of_num = findHcf(arr, size);

    // found lcm of denominator
    int lcm_of_deno = findLcm(arr, size);

    int[] result = new int[2];
    result[0] = hcf_of_num;
    result[1] = lcm_of_deno;

    for (int i = result[0] / 2; i > 1; i--)
    {
        if ((result[1] % i == 0) && (result[0] % i == 0))
        {
            result[1] /= i;
            result[0] /= i;
        }
    }

    // return result
    return (result);
}

// Driver code
public static void main(String[] args)
{
    int size = 4;
    int[][] arr = new int[size][size];

    // Initialize the every row
    // with size 2 (1 for numerator
    // and 2 for denominator)
    for (int i = 0; i < size; i++)
        arr[i] = new int[2];

    arr[0][0] = 9;
    arr[0][1] = 10;
    arr[1][0] = 12;
    arr[1][1] = 25;
    arr[2][0] = 18;
    arr[2][1] = 35;
    arr[3][0] = 21;
    arr[3][1] = 40;

    // function for calculate the result
    int[] result = hcfOfFraction(arr, size);

    // print the result
    System.out.println(result[0] + ", " + result[1]);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 program to find HCF of array of
from math import gcd

# find hcf of numerator series
def findHcf(arr, size):
    ans = arr[0][0]
    for i in range(1, size, 1):
        ans = gcd(ans, arr[i][0])

    # return hcf of numerator
    return (ans)

# find lcm of denominator series
def findLcm(arr, size):

    # ans contains LCM of arr[0][1], ..arr[i][1]
    ans = arr[0][1]
    for i in range(1, size, 1):
        ans = int((((arr[i][1] * ans)) /
                (gcd(arr[i][1], ans))))

    # return lcm of denominator
    return (ans)

# Core Function
def hcfOfFraction(arr, size):

    # found hcf of numerator
    hcf_of_num = findHcf(arr, size)

    # found lcm of denominator
    lcm_of_deno = findLcm(arr, size)

    result = [0 for i in range(2)]
    result[0] = hcf_of_num
    result[1] = lcm_of_deno

    i = int(result[0] / 2)
    while(i > 1):
        if ((result[1] % i == 0) and
            (result[0] % i == 0)):
            result[1] = int(result[1] / i)
            result[0] = (result[0] / i)

    # return result
    return (result)

# Driver Code
if __name__ == '__main__':
    size = 4
    arr = [0 for i in range(size)]

    # Initialize the every row
    # with size 2 (1 for numerator
    # and 2 for denominator)
    for i in range(size):
        arr[i] = [0 for i in range(2)]

    arr[0][0] = 9
    arr[0][1] = 10
    arr[1][0] = 12
    arr[1][1] = 25
    arr[2][0] = 18
    arr[2][1] = 35
    arr[3][0] = 21
    arr[3][1] = 40

    # function for calculate the result
    result = hcfOfFraction(arr, size)

    # print the result
    print(result[0], ",", result[1])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find HCF of array of
// rational numbers (fractions).
using System;

class GFG
{

// hcf of two number
static int gcd(int a, int b)
{
    if (a % b == 0)
        return b;
    else
        return (gcd(b, a % b));
}

// find hcf of numerator series
static int findHcf(int [,]arr, int size)
{
    int ans = arr[0, 0];
    for (int i = 1; i < size; i++)
        ans = gcd(ans, arr[i, 0]);

    // return hcf of numerator
    return (ans);
}

// find lcm of denominator series
static int findLcm(int[,] arr, int size)
{
    // ans contains LCM of arr[0,1], ..arr[i,1]
    int ans = arr[0,1];
    for (int i = 1; i < size; i++)
        ans = (((arr[i, 1] * ans)) /
            (gcd(arr[i, 1], ans)));

    // return lcm of denominator
    return (ans);
}

// Core Function
static int[] hcfOfFraction(int[,] arr, int size)
{
    // found hcf of numerator
    int hcf_of_num = findHcf(arr, size);

    // found lcm of denominator
    int lcm_of_deno = findLcm(arr, size);

    int[] result = new int[2];
    result[0] = hcf_of_num;
    result[1] = lcm_of_deno;

    for (int i = result[0] / 2; i > 1; i--)
    {
        if ((result[1] % i == 0) && (result[0] % i == 0))
        {
            result[1] /= i;
            result[0] /= i;
        }
    }

    // return result
    return (result);
}

// Driver code
public static void Main(String[] args)
{
    int size = 4;
    int[,] arr = new int[size, size];

    // Initialize the every row
    // with size 2 (1 for numerator
    // and 2 for denominator)

    arr[0, 0] = 9;
    arr[0, 1] = 10;
    arr[1, 0] = 12;
    arr[1, 1] = 25;
    arr[2, 0] = 18;
    arr[2, 1] = 35;
    arr[3, 0] = 21;
    arr[3, 1] = 40;

    // function for calculate the result
    int[] result = hcfOfFraction(arr, size);

    // print the result
    Console.WriteLine(result[0] + ", " + result[1]);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find HCF of array of
// rational numbers (fractions).

// hcf of two number
function gcd(a,b)
{
    if (a % b == 0)
        return b;
    else
        return (gcd(b, a % b));
}

// find hcf of numerator series
function findHcf(arr,size)
{
    let ans = arr[0][0];
    for (let i = 1; i < size; i++)
        ans = gcd(ans, arr[i][0]);

    // return hcf of numerator
    return (ans);
}

// find lcm of denominator series
function findLcm(arr,size)
{
    // ans contains LCM of arr[0][1], ..arr[i][1]
    let ans = arr[0][1];
    for (let i = 1; i < size; i++)
        ans = Math.floor(((arr[i][1] * ans)) /
            (gcd(arr[i][1], ans)));

    // return lcm of denominator
    return (ans);
}

// Core Function
function hcfOfFraction(arr,size)
{
    // found hcf of numerator
    let hcf_of_num = findHcf(arr, size);

    // found lcm of denominator
    let lcm_of_deno = findLcm(arr, size);

    let result = new Array(2);
    result[0] = hcf_of_num;
    result[1] = lcm_of_deno;

    for (let i = result[0] / 2; i > 1; i--)
    {
        if ((result[1] % i == 0) && (result[0] % i == 0))
        {
            result[1] /= i;
            result[0] /= i;
        }
    }

    // return result
    return (result);
}

// Driver code
let size = 4;
let arr = new Array(size);

// Initialize the every row
// with size 2 (1 for numerator
// and 2 for denominator)
for (let i = 0; i < size; i++)
    arr[i] = new Array(2);

arr[0][0] = 9;
arr[0][1] = 10;
arr[1][0] = 12;
arr[1][1] = 25;
arr[2][0] = 18;
arr[2][1] = 35;
arr[3][0] = 21;
arr[3][1] = 40;

// function for calculate the result
let result = hcfOfFraction(arr, size);

// print the result
document.write(result[0] + ", " + result[1]+"<br>");

// This code is contributed by rag2127
</script>
```

**输出:**

```
3, 1400
```