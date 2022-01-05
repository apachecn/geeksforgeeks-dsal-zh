# 通过用给定范围内最远的同质数替换元素来修改数组

> 原文:[https://www . geeksforgeeks . org/通过用给定范围内最远的同素数替换元素来修改数组/](https://www.geeksforgeeks.org/modify-array-by-replacing-elements-with-their-farthest-co-prime-number-from-a-given-range/)

给定一个由 **N** 个整数和两个正整数 **L** 和 **R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是为每个数组元素找到**【L，R】**范围内最远的同质数。

**示例:**

> **输入:** arr[] = {5，150，120}，L = 2，R = 250
> **输出:** 249 7 247
> **说明:**
> 与 arr[0]同素且离它最远的数是 249。
> 与 arr[1]同素且离它最远的数是 7。
> 与 arr[2]同素且离它最远的数是 247。
> 
> **输入:** arr[] = {60，246，75，103，155，110}，L = 2，R = 250
> **输出:** 60 246 75 103 155 110

**方法:**给定的问题可以通过[对每个数组元素迭代给定的范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【L，R】**并找到与该数组元素具有 [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) **1** 的最远元素来解决。按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   初始化两个变量，说 **d** 为 **0** 和**互素**为 **-1** ，分别用**arr【I】**存储最远距离和互素数。
    *   迭代给定的范围**【L，R】**并执行以下步骤:
        *   将 **d** 的值更新为**arr【I】**和 **j** 的绝对差值。
        *   如果**arr[I]****j**的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)为**1****d**小于**ABS(arr[I]–j)**，则将**互质**的值更新为 **j** 。
    *   将 **arr[i]** 的值更新为**互质**。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/) **arr[]** 作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate GCD
// of the integers a and b
int gcd(int a, int b)
{
    // Base Case
    if (a == 0)
        return b;

    // Recursively find the GCD
    return gcd(b % a, a);
}

// Function to find the farthest
// co-prime number over the range
// [L, R] for each array element
void update(int arr[], int n)
{
    // Traverse the array arr[]
    for (int i = 0; i < n; i++) {

        // Stores the distance
        // between j and arr[i]
        int d = 0;

        // Stores the integer coprime
        // which is coprime is arr[i]
        int coPrime = -1;

        // Traverse the range [2, 250]
        for (int j = 2; j <= 250; j++) {

            // If gcd of arr[i] and j is 1
            if (gcd(arr[i], j) == 1
                && d < abs(arr[i] - j)) {

                // Update the value of d
                d = abs(arr[i] - j);

                // Update the value
                // of coPrime
                coPrime = j;
            }
        }

        // Update the value of arr[i]
        arr[i] = coPrime;
    }

    // Print the array arr[]
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 60, 246, 75, 103, 155, 110 };
    int N = sizeof(arr) / sizeof(arr[0]);
    update(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to calculate GCD
// of the integers a and b
static int gcd(int a, int b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursively find the GCD
    return gcd(b % a, a);
}

// Function to find the farthest
// co-prime number over the range
// [L, R] for each array element
static void update(int arr[], int n)
{

    // Traverse the array arr[]
    for(int i = 0; i < n; i++)
    {

        // Stores the distance
        // between j and arr[i]
        int d = 0;

        // Stores the integer coprime
        // which is coprime is arr[i]
        int coPrime = -1;

        // Traverse the range [2, 250]
        for(int j = 2; j <= 250; j++)
        {

            // If gcd of arr[i] and j is 1
            if (gcd(arr[i], j) == 1 &&
                d < Math.abs(arr[i] - j))
            {

                // Update the value of d
                d = Math.abs(arr[i] - j);

                // Update the value
                // of coPrime
                coPrime = j;
            }
        }

        // Update the value of arr[i]
        arr[i] = coPrime;
    }

    // Print the array arr[]
    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 60, 246, 75, 103, 155, 110 };
    int N = arr.length;

    update(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# python 3 program for the above approach
from math import gcd

# Function to find the farthest
# co-prime number over the range
# [L, R] for each array element
def update(arr, n):

    # Traverse the array arr[]
    for i in range(n):

        # Stores the distance
        # between j and arr[i]
        d = 0

        # Stores the integer coprime
        # which is coprime is arr[i]
        coPrime = -1

        # Traverse the range [2, 250]
        for j in range(2, 251, 1):

            # If gcd of arr[i] and j is 1
            if (gcd(arr[i], j) == 1 and d < abs(arr[i] - j)):

                # Update the value of d
                d = abs(arr[i] - j)

                # Update the value
                # of coPrime
                coPrime = j

        # Update the value of arr[i]
        arr[i] = coPrime

    # Print the array arr[]
    for i in range(n):
        print(arr[i],end =" ")

# Driver Code
if __name__ == '__main__':
    arr = [60, 246, 75, 103, 155, 110]
    N = len(arr)
    update(arr, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to calculate GCD
    // of the integers a and b
    static int gcd(int a, int b)
    {

        // Base Case
        if (a == 0)
            return b;

        // Recursively find the GCD
        return gcd(b % a, a);
    }

    // Function to find the farthest
    // co-prime number over the range
    // [L, R] for each array element
    static void update(int[] arr, int n)
    {

        // Traverse the array arr[]
        for (int i = 0; i < n; i++) {

            // Stores the distance
            // between j and arr[i]
            int d = 0;

            // Stores the integer coprime
            // which is coprime is arr[i]
            int coPrime = -1;

            // Traverse the range [2, 250]
            for (int j = 2; j <= 250; j++) {

                // If gcd of arr[i] and j is 1
                if (gcd(arr[i], j) == 1
                    && d < Math.Abs(arr[i] - j)) {

                    // Update the value of d
                    d = Math.Abs(arr[i] - j);

                    // Update the value
                    // of coPrime
                    coPrime = j;
                }
            }

            // Update the value of arr[i]
            arr[i] = coPrime;
        }

        // Print the array arr[]
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 60, 246, 75, 103, 155, 110 };
        int N = arr.Length;

        update(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to calculate GCD
// of the integers a and b
function gcd(a, b)
{

    // Base Case
    if (a == 0)
        return b;

    // Recursively find the GCD
    return gcd(b % a, a);
}

// Function to find the farthest
// co-prime number over the range
// [L, R] for each array element
function update(arr, n)
{

    // Traverse the array arr[]
    for(let i = 0; i < n; i++)
    {

        // Stores the distance
        // between j and arr[i]
        let d = 0;

        // Stores the integer coprime
        // which is coprime is arr[i]
        let coPrime = -1;

        // Traverse the range [2, 250]
        for(let j = 2; j <= 250; j++)
        {

            // If gcd of arr[i] and j is 1
            if (gcd(arr[i], j) == 1 &&
                d < Math.abs(arr[i] - j))
            {

                // Update the value of d
                d = Math.abs(arr[i] - j);

                // Update the value
                // of coPrime
                coPrime = j;
            }
        }

        // Update the value of arr[i]
        arr[i] = coPrime;
    }

    // Print the array arr[]
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver code

    let arr = [ 60, 246, 75, 103, 155, 110 ];
    let N = arr.length;

    update(arr, N)

</script>
```

**Output:** 

```
247 5 248 250 2 249
```

**时间复杂度:**O((R–L)* N)
T3】辅助空间: O(1)