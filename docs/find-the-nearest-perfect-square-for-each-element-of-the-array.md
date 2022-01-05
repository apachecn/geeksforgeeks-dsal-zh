# 为数组的每个元素找到最近的完美正方形

> 原文:[https://www . geeksforgeeks . org/查找数组中每个元素的最近完美平方/](https://www.geeksforgeeks.org/find-the-nearest-perfect-square-for-each-element-of-the-array/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为每个数组元素打印[最近的完美正方形](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)。

**示例:**

> **输入:** arr[] = {5，2，7，13}
> **输出:** 4 1 9 16
> **解释:**
> arr[0](= 5)最近的完美平方是 4。
> arr[1](= 2)的最近完美平方是 1。
> arr[2](= 7)的最近完美平方是 9。
> arr[3](= 13)的最近完美平方是 16。
> 
> **输入:** arr[] = {31，18，64}
> **输出:** 36 16 64

**方法:**按照以下步骤解决问题:

*   [从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   对于每个数组元素，找到[最近的完美正方形](https://www.geeksforgeeks.org/closest-perfect-square-and-its-distance/)
    *   如果 **N** 是**完美正方形**那么打印 N
    *   否则，找到第一个 [<u>完美方块</u>](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/) 编号 **> N** 并注意其与 **N** 的区别。
    *   然后，找到第一个完美平方数 **< N** ，并注意其与 **N** 的区别。
    *   并打印完美的正方形，得到这两个差值的最小

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest perfect square
// for every element in the given array
void nearestPerfectSquare(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Calculate square root of
        // current  element
        int sr = sqrt(arr[i]);

        // Calculate perfect square
        int a = sr * sr;
        int b = (sr + 1) * (sr + 1);

        // Find the nearest
        if ((arr[i] - a) < (b - arr[i]))
            cout << a << " ";
        else
            cout << b << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, 2, 7, 13 };
    int N = sizeof(arr) / sizeof(arr[0]);
    nearestPerfectSquare(arr, N);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the nearest perfect square
// for every element in the given array
static void nearestPerfectSquare(int[] arr, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Calculate square root of
        // current  element
        int sr = (int)Math.sqrt(arr[i]);

        // Calculate perfect square
        int a = sr * sr;
        int b = (sr + 1) * (sr + 1);

        // Find the nearest
        if ((arr[i] - a) < (b - arr[i]))
            System.out.print(a + " ");
        else
            System.out.print(b + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 5, 2, 7, 13 };
    int N = arr.length;

    nearestPerfectSquare(arr, N);
}
}

// This code is contributed by souravmahato348
```

## **蟒蛇 3**

```
# Python program for the above approach
# Function to find the nearest perfect square
# for every element in the given array
# import the math module
import math
def nearestPerfectSquare(arr,N):

    # Traverse the array
    for i in range(0,N):

        # Calculate square root of
        # current  element
        sr = math.floor(math.sqrt(arr[i]))

        # Calculate perfect square
        a = sr * sr
        b = (sr + 1) * (sr + 1)

        # Find the nearest
        if ((arr[i] - a) < (b - arr[i])):
           print(a ,end=" ")
        else :
           print(b ,end=" ")

# Driver Code
arr =  [5, 2, 7, 13]
N = len(arr)
nearestPerfectSquare(arr, N)

# This code is contributed by shivanisinghss2110
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the nearest perfect square
    // for every element in the given array
    static void nearestPerfectSquare(int[] arr, int N)
    {

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Calculate square root of
            // current  element
            int sr = (int)Math.Sqrt(arr[i]);

            // Calculate perfect square
            int a = sr * sr;
            int b = (sr + 1) * (sr + 1);

            // Find the nearest
            if ((arr[i] - a) < (b - arr[i]))
                Console.Write(a + " ");
            else
                Console.Write(b + " ");
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 5, 2, 7, 13 };
        int N = arr.Length;

        nearestPerfectSquare(arr, N);
    }
}

// This code is contributed by souravmahato348
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find the nearest perfect square
// for every element in the given array
function nearestPerfectSquare(arr, N)
{

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Calculate square root of
        // current  element
        let sr = parseInt(Math.sqrt(arr[i]));

        // Calculate perfect square
        let a = sr * sr;
        let b = (sr + 1) * (sr + 1);

        // Find the nearest
        if ((arr[i] - a) < (b - arr[i]))
            document.write(a + " ");
        else
            document.write(b + " ");
    }
}

// Driver Code
    let arr = [ 5, 2, 7, 13 ];
    let N = arr.length;
    nearestPerfectSquare(arr, N);

</script>
```

****Output:** 

```
4 1 9 16
```** 

*****时间复杂度:**O(N * sqrt(arr[I])***

*****辅助空间:** O(1)***