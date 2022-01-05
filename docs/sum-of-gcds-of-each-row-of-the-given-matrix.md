# 给定矩阵每行的 gcd 之和

> 原文:[https://www . geeksforgeeks . org/给定矩阵每行 gcds 之和/](https://www.geeksforgeeks.org/sum-of-gcds-of-each-row-of-the-given-matrix/)

给定一个大小为 **N * N** 的矩阵 **mat[][]** ，任务是求给定矩阵所有行的 gcd 之和。
**例:**

> **输入:** arr[][] = {
> {2，4，6，8}，
> {3，6，9，12}，
> {4，8，12，16}，
> {5，10，15，20 } }；
> **输出:** 14
> gcd(2，4，6，8) = 2
> gcd(3，6，9，12) = 3
> gcd(4，8，12，16) = 4
> gcd(5，10，15，20) = 5
> 2 + 3 + 4 + 5 = 14
> **输入:** arr[][] = {
> {1，2
> T22】输出: 10

**逼近:**求矩阵每行的 [GCD](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 并加到总和中。总和将是所有行的 GCD 总和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to return the sum of gcd
// of each row of the given matrix
int sumGcd(int arr[][4], int n)
{

    // To store the required sum
    int sum = 0;

    for (int i = 0; i < n; i++) {

        // To store the gcd of the current row
        int gcdRow = arr[i][0];
        for (int j = 1; j < n; j++)
            gcdRow = gcd(arr[i][j], gcdRow);

        // Add gcd of the current row to the sum
        sum += gcdRow;
    }

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int arr[][4] = { { 2, 4, 6, 8 },
                     { 3, 6, 9, 12 },
                     { 4, 8, 12, 16 },
                     { 5, 10, 15, 20 } };
    int size = sizeof(arr) / sizeof(arr[0]);

    cout << sumGcd(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the sum of gcd
    // of each row of the given matrix
    static int sumGcd(int arr[][], int n)
    {

        // To store the required sum
        int sum = 0;

        for (int i = 0; i < n; i++)
        {

            // To store the gcd of the current row
            int gcdRow = arr[i][0];
            for (int j = 1; j < n; j++)
                gcdRow = gcd(arr[i][j], gcdRow);

            // Add gcd of the current row to the sum
            sum += gcdRow;
        }

        // Return the required sum
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[][] = { { 2, 4, 6, 8 },
                        { 3, 6, 9, 12 },
                        { 4, 8, 12, 16 },
                        { 5, 10, 15, 20 } };

        int size = arr.length ;

        System.out.println(sumGcd(arr, size));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return gcd of a and b
def gcd(a, b):
    if (a == 0):
        return b
    return gcd(b % a, a)

# Function to return the Sum of gcd
# of each row of the given matrix
def SumGcd(arr, n):

    # To store the required Sum
    Sum = 0

    for i in range(n):

        # To store the gcd of the current row
        gcdRow = arr[i][0]

        for j in range(1,n):
            gcdRow = gcd(arr[i][j], gcdRow)

        # Add gcd of the current row to the Sum
        Sum += gcdRow

    # Return the required Sum
    return Sum

# Driver code

arr= [ [ 2, 4, 6, 8 ],
    [ 3, 6, 9, 12 ],
    [ 4, 8, 12, 16 ],
    [ 5, 10, 15, 20 ] ]

size = len(arr)

print(SumGcd(arr, size))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the sum of gcd
    // of each row of the given matrix
    static int sumGcd(int [ , ]arr, int n)
    {

        // To store the required sum
        int sum = 0;

        for (int i = 0; i < n; i++)
        {

            // To store the gcd of the current row
            int gcdRow = arr[i, 0];
            for (int j = 1; j < n; j++)
                gcdRow = gcd(arr[i, j], gcdRow);

            // Add gcd of the current row to the sum
            sum += gcdRow;
        }

        // Return the required sum
        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int [ , ] arr = new int[ 4, 4 ]{{ 2, 4, 6, 8 },
                                        { 3, 6, 9, 12 },
                                        { 4, 8, 12, 16 },
                                        { 5, 10, 15, 20 }};

        int size = 4;
        Console.WriteLine(sumGcd(arr, size));
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the approach

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to return the sum of gcd
// of each row of the given matrix
function sumGcd(&$arr, $n)
{

    // To store the required sum
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // To store the gcd of the current row
        $gcdRow = $arr[$i][0];
        for ($j = 1; $j < $n; $j++)
            $gcdRow = gcd($arr[$i][$j], $gcdRow);

        // Add gcd of the current row to the sum
        $sum += $gcdRow;
    }

    // Return the required sum
    return $sum;
}

// Driver code

    $arr = array(array( 2, 4, 6, 8 ),
                array( 3, 6, 9, 12 ),
                array(4, 8, 12, 16 ),
                array( 5, 10, 15, 20));
    $size = sizeof($arr);

    echo sumGcd($arr, $size);

    return 0;

// This code is contributed by ChitraNayal   
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return gcd of a and b
    function gcd(a,b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to return the sum of gcd
    // of each row of the given matrix
    function sumGcd(arr,n)
    {
        // To store the required sum
        let sum = 0;

        for (let i = 0; i < n; i++)
        {

            // To store the gcd of the current row
            let gcdRow = arr[i][0];
            for (let j = 1; j < n; j++)
                gcdRow = gcd(arr[i][j], gcdRow);

            // Add gcd of the current row to the sum
            sum += gcdRow;
        }

        // Return the required sum
        return sum;
    }

    // Driver code
    let arr= [ [ 2, 4, 6, 8 ],
    [ 3, 6, 9, 12 ],
    [ 4, 8, 12, 16 ],
    [ 5, 10, 15, 20 ] ];

    let size = arr.length ;
    document.write(sumGcd(arr, size));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
14
```