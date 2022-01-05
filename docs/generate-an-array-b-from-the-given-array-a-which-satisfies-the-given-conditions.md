# 从满足给定条件的给定数组 A[]生成数组 B[]

> 原文:[https://www . geeksforgeeks . org/从给定数组 a 生成满足给定条件的数组 b/](https://www.geeksforgeeks.org/generate-an-array-b-from-the-given-array-a-which-satisfies-the-given-conditions/)

给定一个由 **N** 个整数组成的数组 **A[]** ，使得**A[0]+A[1]+A[2]+…A[N–1]= 0**。任务是为所有有效的 **i** 和**b[0]+b[1]+b[2]+…+b[n–1]= 0**生成一个数组 **B[]** ，使得 **B[i]** 要么是**⌊a[i/2⌋**要么是**⌈a[i/2⌉**。

**示例:**

> **输入:** A[] = {1，2，-5，3，-1}
> **输出:**0 1-2 1 0
> T6】输入: A[] = {3，-5，-7，9，2，-2}
> **输出:** 1 -2 -4 5 1 -1

**方法:**对于偶数整数，可以安全地假设 **B[i]** 将是 **A[i] / 2** 但是对于奇数整数，为了保持和等于零，取正好一半奇数整数的上限和正好另一半奇数整数的下限。既然奇–奇=偶且偶–偶=偶且 0 也是偶，可以说 **A[]** 将始终包含偶数个奇整数，这样和就可以是 **0** 。所以对于有效的输入，总会有答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the array elements
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to generate and print
// the required array
void generateArr(int arr[], int n)
{

    // To switch the ceil and floor
    // function alternatively
    bool flip = true;

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // If the number is odd then print the ceil
        // or floor value after division by 2
        if (arr[i] & 1) {

            // Use the ceil and floor alternatively
            if (flip ^= true)
                cout << ceil((float)(arr[i]) / 2.0) << " ";
            else
                cout << floor((float)(arr[i]) / 2.0) << " ";
        }

        // If arr[i] is even then it will
        // be completely divisible by 2
        else {
            cout << arr[i] / 2 << " ";
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 3, -5, -7, 9, 2, -2 };
    int n = sizeof(arr) / sizeof(int);

    generateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
// Utility function to print
// the array elements
import java.util.*;
import java.lang.*;

class GFG
{

static void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to generate and print
// the required array
static void generateArr(int arr[], int n)
{

    // To switch the ceil and floor
    // function alternatively
    boolean flip = true;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // If the number is odd then print the ceil
        // or floor value after division by 2
        if ((arr[i] & 1) != 0)
        {

            // Use the ceil and floor alternatively
            if (flip ^= true)
                System.out.print((int)(Math.ceil(arr[i] /
                                            2.0)) + " ");
            else
                System.out.print((int)(Math.floor(arr[i] /
                                            2.0)) + " ");
        }

        // If arr[i] is even then it will
        // be completely divisible by 2
        else
        {
            System.out.print(arr[i] / 2 +" ");
        }
    }
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 3, -5, -7, 9, 2, -2 };
    int n = arr.length;

    generateArr(arr, n);
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil, floor

# Utility function to print
# the array elements
def printArr(arr, n):
    for i in range(n):
        print(arr[i], end = " ")

# Function to generate and print
# the required array
def generateArr(arr, n):

    # To switch the ceil and floor
    # function alternatively
    flip = True

    # For every element of the array
    for i in range(n):

        # If the number is odd then print the ceil
        # or floor value after division by 2
        if (arr[i] & 1):

            # Use the ceil and floor alternatively
            flip ^= True
            if (flip):
                print(int(ceil((arr[i]) / 2)),
                                   end = " ")
            else:
                print(int(floor((arr[i]) / 2)),
                                    end = " ")

        # If arr[i] is even then it will
        # be completely divisible by 2
        else:
            print(int(arr[i] / 2), end = " ")

# Driver code
arr = [3, -5, -7, 9, 2, -2]
n = len(arr)

generateArr(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
// Utility function to print
// the array elements
using System;
using System.Collections.Generic;

class GFG
{

static void printArr(int []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to generate and print
// the required array
static void generateArr(int []arr, int n)
{

    // To switch the ceil and floor
    // function alternatively
    bool flip = true;

    // For every element of the array
    for (int i = 0; i < n; i++)
    {

        // If the number is odd then print the ceil
        // or floor value after division by 2
        if ((arr[i] & 1) != 0)
        {

            // Use the ceil and floor alternatively
            if (flip ^= true)
                Console.Write((int)(Math.Ceiling(arr[i] /
                                            2.0)) + " ");
            else
                Console.Write((int)(Math.Floor(arr[i] /
                                            2.0)) + " ");
        }

        // If arr[i] is even then it will
        // be completely divisible by 2
        else
        {
            Console.Write(arr[i] / 2 +" ");
        }
    }
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, -5, -7, 9, 2, -2 };
    int n = arr.Length;

    generateArr(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript implementation of the approach
// Utility function to print
// the array elements   
function printArr(arr , n) {
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Function to generate and print
    // the required array
    function generateArr(arr , n) {

        // To switch the ceil and floor
        // function alternatively
        var flip = true;

        // For every element of the array
        for (i = 0; i < n; i++) {

            // If the number is odd then print the ceil
            // or floor value after division by 2
            if ((arr[i] & 1) != 0) {

                // Use the ceil and floor alternatively
                if (flip ^= true)
                    document.write(parseInt( (Math.ceil(arr[i] / 2.0))) + " ");
                else
                    document.write(parseInt( (Math.floor(arr[i] / 2.0))) + " ");
            }

            // If arr[i] is even then it will
            // be completely divisible by 2
            else {
                document.write(arr[i] / 2 + " ");
            }
        }
    }

    // Driver code

        var arr = [ 3, -5, -7, 9, 2, -2 ];
        var n = arr.length;

        generateArr(arr, n);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
1 -2 -4 5 1 -1
```