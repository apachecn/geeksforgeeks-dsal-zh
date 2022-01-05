# 数组中最大的完美立方数

> 原文:[https://www . geeksforgeeks . org/最大完美立方体数组中的数字/](https://www.geeksforgeeks.org/largest-perfect-cube-number-in-an-array/)

给定一组 **N 个**整数。任务是找出最大的数，也就是一个完美的立方体。如果没有完美立方体的数字，打印-1。
**示例** :

```
Input : arr[] = {16, 8, 25, 2, 3, 10} 
Output : 25
Explanation: 25 is the largest number 
that is a perfect cube. 

Input : arr[] = {36, 64, 10, 16, 29, 25| 
Output : 64
```

一个**简单的解决方案**是对元素进行排序，并对 **N** 个数字进行排序，然后使用 cbrt()函数从后面开始检查一个完美的立方数。最后的第一个数字是一个完美的立方数，这就是我们的答案。排序的复杂度为 O(n log n)，cbrt()函数的复杂度为 log n，所以最坏的情况下复杂度为 O(n log n)。
一个**高效解**就是对 O(n)中的所有元素进行迭代，每次与最大元素进行比较，存储所有完美立方体的最大值。
以下是上述方法的实施:

## C++

```
// CPP program to find the largest perfect
// cube number among n numbers

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is perfect cube number or not
bool checkPerfectcube(int n)
{
    // takes the sqrt of the number
    int d = cbrt(n);

    // checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to find the largest perfect
// cube number in the array
int largestPerfectcubeNumber(int a[], int n)
{
    // stores the maximum of all
    // perfect cube numbers
    int maxi = -1;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i]))
            maxi = max(a[i], maxi);
    }

    return maxi;
}

// Driver Code
int main()
{
    int a[] = { 16, 64, 25, 2, 3, 10 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << largestPerfectcubeNumber(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest perfect
// cube number among n numbers
class Solution
{

// Function to check if a number
// is perfect cube number or not
static boolean checkPerfectcube(int n)
{
    // takes the sqrt of the number
    int d =(int) Math.cbrt(n);

    // checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to find the largest perfect
// cube number in the array
static int largestPerfectcubeNumber(int a[], int n)
{
    // stores the maximum of all
    // perfect cube numbers
    int maxi = -1;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i]))
            maxi = Math.max(a[i], maxi);
    }

    return maxi;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 16, 64, 25, 2, 3, 10 };

    int n =a.length;

    System.out.print(largestPerfectcubeNumber(a, n));

}
}

//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find the largest
# perfect cube number among n numbers
import math

# Function to check if a number
# is perfect cube number or not
def checkPerfectcube(n):

    # checks if it is a perfect
    # cube number
    cube_root = n**(1./3.)
    if round(cube_root) ** 3 == n:
        return True

    else:
        return False

# Function to find the largest perfect
# cube number in the array
def largestPerfectcubeNumber(a, n):

    # stores the maximum of all
    # perfect cube numbers
    maxi = -1

    # Traverse all elements in the array
    for i in range(0, n, 1):

        # store the maximum if current
        # element is a perfect cube
        if (checkPerfectcube(a[i])):
            maxi = max(a[i], maxi)

    return maxi;

# Driver Code
if __name__ == '__main__':
    a = [16, 64, 25, 2, 3, 10]

    n = len(a)

    print(largestPerfectcubeNumber(a, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
//C# program to find the largest perfect
// cube number among n numbers
using System;

public class Solution
{

    // Function to check if a number
    // is perfect cube number or not
    static bool checkPerfectcube(int n)
    {
        // takes the sqrt of the number
        int d = (int)Math.Ceiling(Math.Pow(n, (double)1 / 3));
        // checks if it is a perfect
        // cube number
        if (d * d * d == n)
            return true;

        return false;
    }

    // Function to find the largest perfect
    // cube number in the array
    static int largestPerfectcubeNumber(int []a, int n)
    {
        // stores the maximum of all
        // perfect cube numbers
        int maxi = -1;

        // Traverse all elements in the array
        for (int i = 0; i < n; i++) {

            // store the maximum if current
            // element is a perfect cube
            if (checkPerfectcube(a[i]))
                maxi = Math.Max(a[i], maxi);
        }

        return maxi;
    }

    // Driver Code
    public static void Main()
    {
        int []a = { 16, 64, 25, 2, 3, 10 };

        int n =a.Length;

        Console.WriteLine(largestPerfectcubeNumber(a, n));

    }
}

/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the largest perfect
// cube number among n numbers

// Function to check if a number
// is perfect cube number or not
function checkPerfectcube($n)
{
    // takes the sqrt of the number
    $d = pow($n, (1 / 3));
    $d = round($d);

    // checks if it is a perfect
    // cube number
    if ($d * $d * $d == $n)
        return true;

    return false;
}

// Function to find the largest perfect
// cube number in the array
function largestPerfectcubeNumber(&$a, $n)
{
    // stores the maximum of all
    // perfect cube numbers
    $maxi = -1;

    // Traverse all elements in the array
    for ($i = 0; $i < $n; $i++)
    {

        // store the maximum if current
        // element is a perfect cube
        if (checkPerfectcube($a[$i]))
            $maxi = max($a[$i], $maxi);
    }

    return $maxi;
}

// Driver Code
$a = array( 16, 64, 25, 2, 3, 10 );
$n = sizeof($a);
echo largestPerfectcubeNumber($a, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find the largest perfect
// cube number among n numbers

// Function to check if a number
// is perfect cube number or not
function checkPerfectcube(n)
{
    // takes the sqrt of the number
    let d = parseInt(Math.cbrt(n));

    // checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to find the largest perfect
// cube number in the array
function largestPerfectcubeNumber(a, n)
{
    // stores the maximum of all
    // perfect cube numbers
    let maxi = -1;

    // Traverse all elements in the array
    for (let i = 0; i < n; i++) {

        // store the maximum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i]))
            maxi = Math.max(a[i], maxi);
    }

    return maxi;
}

// Driver Code
let a = [ 16, 64, 25, 2, 3, 10 ];

let n = a.length;

document.write(largestPerfectcubeNumber(a, n));

</script>
```

**Output:** 

```
64
```