# 数组中最小的完美立方体

> 原文:[https://www . geeksforgeeks . org/最小完美阵列立方体/](https://www.geeksforgeeks.org/smallest-perfect-cube-in-an-array/)

给定一个由 **n** 个整数组成的数组 **arr[]** 。任务是从数组中找到最小的完美立方体。如果数组中没有完美立方体，打印 **-1** 。
**举例:**

> **输入:** arr[] = {16，8，25，2，3，10}
> **输出:** 8
> 8 是数组中唯一的完美立方体
> **输入:** arr[] = {27，8，1，64}
> **输出:** 1
> 所有元素都是完美立方体但 1 是所有元素中的最小值。

一个**简单的解决方案**是对元素进行排序，然后对数字进行排序，并使用 [cbrt()](https://www.geeksforgeeks.org/stdcbrt-in-c/) 函数从头开始检查一个完美的立方数。我们的答案是从一开始的第一个数字，它是一个完美的立方数。排序的复杂度为 **O(n log n)** ，cbrt()函数的复杂度为 **log n** ，所以最坏的情况下复杂度为 **O(n log n)** 。
一个**高效的解决方案**是对 O(n)中的所有元素进行迭代，每次与最小元素进行比较，存储所有完美立方体的最小值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if n is a perfect cube
bool checkPerfectcube(int n)
{
    // Takes the sqrt of the number
    int d = cbrt(n);

    // Checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to return the smallest perfect
// cube from the array
int smallestPerfectCube(int a[], int n)
{

    // Stores the minimum of all the
    // perfect cubes from the array
    int mini = INT_MAX;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++) {

        // Store the minimum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i])) {
            mini = min(a[i], mini);
        }
    }

    return mini;
}

// Driver code
int main()
{
    int a[] = { 16, 8, 25, 2, 3, 10 };

    int n = sizeof(a) / sizeof(a[0]);

    cout << smallestPerfectCube(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns true
// if n is a perfect cube
static boolean checkPerfectcube(int n)
{
    // Takes the sqrt of the number
    int d = (int)Math.cbrt(n);

    // Checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to return the smallest perfect
// cube from the array
static int smallestPerfectCube(int a[], int n)
{

    // Stores the minimum of all the
    // perfect cubes from the array
    int mini = Integer.MAX_VALUE;

    // Traverse all elements in the array
    for (int i = 0; i < n; i++)
    {

        // Store the minimum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i]))
        {
            mini = Math.min(a[i], mini);
        }
    }

    return mini;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 16, 8, 25, 2, 3, 10 };

    int n = a.length;

    System.out.print(smallestPerfectCube(a, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import sys

# Function that returns true
# if n is a perfect cube
def checkPerfectcube(n) :

    # Takes the sqrt of the number
    d = int(n**(1/3));

    # Checks if it is a perfect
    # cube number
    if (d * d * d == n) :
        return True;

    return False;

# Function to return the smallest perfect
# cube from the array
def smallestPerfectCube(a, n) :

    # Stores the minimum of all the
    # perfect cubes from the array
    mini = sys.maxsize;

    # Traverse all elements in the array
    for i in range(n) :

        # Store the minimum if current
        # element is a perfect cube
        if (checkPerfectcube(a[i])) :
            mini = min(a[i], mini);

    return mini;

# Driver code
if __name__ == "__main__" :

    a = [ 16, 8, 25, 2, 3, 10 ];

    n = len(a);

    print(smallestPerfectCube(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if n is a perfect cube
    static bool checkPerfectcube(int n)
    {
        // Takes the sqrt of the number
        int d = (int)Math.Sqrt(n);

        // Checks if it is a perfect
        // cube number
        if (d * d * d == n)
            return true;

        return false;
    }

    // Function to return the smallest perfect
    // cube from the array
    static int smallestPerfectCube(int []a, int n)
    {

        // Stores the minimum of all the
        // perfect cubes from the array
        int mini = int.MaxValue;

        // Traverse all elements in the array
        for (int i = 0; i < n; i++)
        {

            // Store the minimum if current
            // element is a perfect cube
            if (checkPerfectcube(a[i]))
            {
                mini = Math.Min(a[i], mini);
            }
        }

        return mini;
    }

    // Driver code
    static public void Main ()
    {
        int []a = { 16, 8, 25, 2, 3, 10 };

        int n = a.Length;
        Console.Write(smallestPerfectCube(a, n));
    }
}

// This code is contributed by ajit..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if n is a perfect cube
function checkPerfectcube(n)
{
    // Takes the sqrt of the number
    let d = parseInt(Math.cbrt(n));

    // Checks if it is a perfect
    // cube number
    if (d * d * d == n)
        return true;

    return false;
}

// Function to return the smallest perfect
// cube from the array
function smallestPerfectCube(a, n)
{

    // Stores the minimum of all the
    // perfect cubes from the array
    let mini = Number.MAX_VALUE;

    // Traverse all elements in the array
    for (let i = 0; i < n; i++) {

        // Store the minimum if current
        // element is a perfect cube
        if (checkPerfectcube(a[i])) {
            mini = Math.min(a[i], mini);
        }
    }

    return mini;
}

// Driver code
let a = [ 16, 8, 25, 2, 3, 10 ];

let n = a.length;

document.write(smallestPerfectCube(a, n));

</script>
```

**Output:** 

```
8
```