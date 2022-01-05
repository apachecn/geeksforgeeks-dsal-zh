# 不是完美立方体的数组中最大的数字

> 原文:[https://www . geeksforgeeks . org/阵列中最大数量的非完美立方体/](https://www.geeksforgeeks.org/largest-number-in-an-array-that-is-not-a-perfect-cube/)

给定 n 个整数的数组。任务是找出不是完美立方体的最大数字。如果没有完美立方体的数字，打印-1。
**例**:

```
Input: arr[] = {16, 8, 25, 2, 3, 10} 
Output: 25
25 is the largest number that is not a perfect cube. 

Input: arr[] = {36, 64, 10, 16, 29, 25}
Output: 36
```

一个**简单的解决方案**是对元素进行排序，然后对数字进行排序，并使用 cbrt()函数从后面开始检查非完美立方数。最后的第一个不是完美立方数的数就是我们的答案。排序的复杂度为 O(n log n)，cbrt()函数的复杂度为 log n，所以最坏的情况下，复杂度为 O(n log n)。
一个**高效的解决方案**是对 O(n)中的所有元素进行迭代，每次与最大元素进行比较，存储所有非完美立方体的最大值。
以下是上述方法的实施:

## C++

```
// CPP program to find the largest non-perfect
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

// Function to find the largest non perfect
// cube number in the array
int largestNonPerfectcubeNumber(int a[], int n)
{
    // stores the maximum of all
    // perfect cube numbers
    int maxi = -1;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if current
        // element is a non perfect cube
        if (!checkPerfectcube(a[i]))
            maxi = max(a[i], maxi);
    }

    return maxi;
}

// Driver Code
int main()
{
    int a[] = { 16, 64, 25, 2, 3, 10 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << largestNonPerfectcubeNumber(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest non-perfect
// cube number among n numbers

import java.io.*;

class GFG {

// Function to check if a number
// is perfect cube number or not
static boolean checkPerfectcube(int n)
{
    // takes the sqrt of the number
    int d = (int)Math.cbrt(n);

    // checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to find the largest non perfect
// cube number in the array
static int largestNonPerfectcubeNumber(int []a, int n)
{
    // stores the maximum of all
    // perfect cube numbers
    int maxi = -1;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if current
        // element is a non perfect cube
        if (!checkPerfectcube(a[i]))
            maxi = Math.max(a[i], maxi);
    }

    return maxi;
}

// Driver Code

    public static void main (String[] args) {
    int a[] = { 16, 64, 25, 2, 3, 10 };

    int n = a.length;

    System.out.print( largestNonPerfectcubeNumber(a, n));
    }
}
// This code is contributed
// by inder_verma
```

## 蟒蛇 3

```
# Python 3 program to find the largest
# non-perfect cube number among n numbers
import math

# Function to check if a number
# is perfect cube number or not
def checkPerfectcube(n):

    # takes the sqrt of the number
    cube_root = n ** (1./3.)
    if round(cube_root) ** 3 == n:
        return True
    else:
        return False

# Function to find the largest non
# perfect cube number in the array
def largestNonPerfectcubeNumber(a, n):

    # stores the maximum of all
    # perfect cube numbers
    maxi = -1

    # Traverse all elements in the array
    for i in range(0, n, 1):

        # store the maximum if current
        # element is a non perfect cube
        if (checkPerfectcube(a[i]) == False):
            maxi = max(a[i], maxi)

    return maxi

# Driver Code
if __name__ == '__main__':
    a = [16, 64, 25, 2, 3, 10]

    n = len(a)

    print(largestNonPerfectcubeNumber(a, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the largest non-perfect
// cube number among n numbers
using System;
public class GFG {

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

    // Function to find the largest non perfect
    // cube number in the array
    static int largestNonPerfectcubeNumber(int []a, int n)
    {
        // stores the maximum of all
        // perfect cube numbers
        int maxi = -1;

        // Traverse all elements in the array
        for (int i = 0; i < n; i++) {

            // store the maximum if current
            // element is a non perfect cube
            if (checkPerfectcube(a[i])==false)
                maxi = Math.Max(a[i], maxi);
        }

        return maxi;
    }

    // Driver Code

        public static void Main () {
        int []a = { 16, 64, 25, 2, 3, 10 };

        int n = a.Length;

        Console.WriteLine( largestNonPerfectcubeNumber(a, n));
        }
}
/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the largest non-perfect
// cube number among n numbers

// Function to check if a number
// is perfect cube number or not
function checkPerfectcube($n)
{
    // takes the sqrt of the number
    $d = (int)round(pow($n, 1/3));
    // checks if it is a perfect
    // cube number
    if ($d * $d * $d == $n)
        return true;

    return false;
}

// Function to find the largest non perfect
// cube number in the array
function largestNonPerfectcubeNumber($a, $n)
{
    // stores the maximum of all
    // perfect cube numbers
    $maxi = -1;

    // Traverse all elements in the array
    for ($i = 0; $i < $n; $i++) {

        // store the maximum if current
        // element is a non perfect cube
        if (!checkPerfectcube($a[$i]))
            $maxi = max($a[$i], $maxi);
    }

    return $maxi;
}

// Driver Code

    $a = array( 16, 64, 25, 2, 3, 10 );

    $n = count($a);

    echo largestNonPerfectcubeNumber($a, $n);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the largest non-perfect
// cube number among n numbers

// Function to check if a number
// is perfect cube number or not
function checkPerfectcube(n)
{

    // takes the sqrt of the number
    let d = Math.cbrt(n);

    // checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to find the largest non perfect
// cube number in the array
function largestNonPerfectcubeNumber(a, n)
{
    // stores the maximum of all
    // perfect cube numbers
    let maxi = -1;

    // Traverse all elements in the array
    for (let i = 0; i < n; i++) {

        // store the maximum if current
        // element is a non perfect cube
        if (!checkPerfectcube(a[i]))
            maxi = Math.max(a[i], maxi);
    }

    return maxi;
}

// Driver Code
let a = [ 16, 64, 25, 2, 3, 10 ];
let n = a.length;
document.write(largestNonPerfectcubeNumber(a, n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
25
```

**时间复杂度:** O(n)

**辅助空间:** O(1)