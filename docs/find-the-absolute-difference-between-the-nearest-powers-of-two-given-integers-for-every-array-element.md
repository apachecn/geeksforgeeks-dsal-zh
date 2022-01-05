# 求每个数组元素的两个给定整数的最近幂之间的绝对差

> 原文:[https://www . geeksforgeeks . org/查找每个数组元素的最近二次幂整数之差/](https://www.geeksforgeeks.org/find-the-absolute-difference-between-the-nearest-powers-of-two-given-integers-for-every-array-element/)

给定一个由 **N** 正整数和两个正整数 **A** 和 **B** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是用 **A** 和 **B** 的最近幂的[绝对](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)差替换每个数组元素。如果存在两个最接近的幂，则选择两者中的最大值。

**示例:**

> **输入:** arr[] = {5，12，25}，A = 2，B = 3
> T3】输出:1 7 5
> T6】解释:
> 
> *   对于元素 arr[0](= 5):2 的最近幂是 4，3 的最近幂是 3。因此，4 和 3 的绝对差是 1。
> *   对于 arr[1](= 12):2 的最近幂是 16，3 的最近幂是 9。因此，16 和 9 的绝对差是 7。
> *   对于 arr[2](= 5):2 的最近幂是 32，3 的最近幂是 27。因此，27 和 32 的绝对差是 5。
> 
> 因此，修改后的数组是{1，7，5}。
> 
> **输入:** arr[] = {32，3，7}，a = 2，b = 3
> T3】输出: 0 1 1

**方法:**给定的问题可以通过为每个数组元素找到 **A** 和 **B** 的最近幂并将其更新为获得的两个值的绝对差来解决。
按照步骤解决问题

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   找出 **a** 小于和大于**arr【I】**的[完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)的两个值，并找出两个值中最接近的值。
    *   找出 **b** 小于和大于**arr【I】**的[完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)的两个值，并找出两个值中最接近的值。
    *   找出获得的两个最接近值之间的绝对差值，并用它更新 **arr[i]** 。
*   完成上述步骤后，[打印修改后的数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the array
void printArray(int arr[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Function to modify array elements
// by absolute difference of the
// nearest perfect power of a and b
void nearestPowerDiff(int arr[], int N,
                      int a, int b)
{
    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Find the log a of arr[i]
        int log_a = log(arr[i]) / log(a);

        // Find the power of a less
        // than and greater than a
        int A = pow(a, log_a);
        int B = pow(a, log_a + 1);

        if ((arr[i] - A) < (B - arr[i]))
            log_a = A;
        else
            log_a = B;

        // Find the log b of arr[i]
        int log_b = log(arr[i]) / log(b);

        // Find the power of b less than
        // and greater than b
        A = pow(b, log_b);
        B = pow(b, log_b + 1);

        if ((arr[i] - A) < (B - arr[i]))
            log_b = A;
        else
            log_b = B;

        // Update arr[i] with absolute
        // difference of log_a & log _b
        arr[i] = abs(log_a - log_b);
    }

    // Print the modified array
    printArray(arr, N);
}

// Driver Code
int main()
{
    int arr[] = { 5, 12, 25 };
    int A = 2, B = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    nearestPowerDiff(arr, N, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to print the array
static void printArray(int[] arr, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Function to modify array elements
// by absolute difference of the
// nearest perfect power of a and b
static void nearestPowerDiff(int[] arr, int N,
                             int a, int b)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Find the log a of arr[i]
        int log_a = (int)(Math.log(arr[i]) /
                          Math.log(a));

        // Find the power of a less
        // than and greater than a
        int A = (int)(Math.pow(a, log_a));
        int B = (int)(Math.pow(a, log_a + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_a = A;
        else
            log_a = B;

        // Find the log b of arr[i]
        int log_b = (int)(Math.log(arr[i]) /
                          Math.log(b));

        // Find the power of b less than
        // and greater than b
        A = (int)(Math.pow(b, log_b));
        B = (int)(Math.pow(b, log_b + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_b = A;
        else
            log_b = B;

        // Update arr[i] with absolute
        // difference of log_a & log _b
        arr[i] = Math.abs(log_a - log_b);
    }

    // Print the modified array
    printArray(arr, N);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 5, 12, 25 };
    int A = 2, B = 3;
    int N = arr.length;

    nearestPowerDiff(arr, N, A, B);
}
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to print the array
def printArray(arr, N):

    # Traverse the array
    for i in range(N):
        print(arr[i], end = " ")

# Function to modify array elements
# by absolute difference of the
# nearest perfect power of a and b
def nearestPowerDiff(arr, N, a, b):

    # Traverse the array arr[]
    for i in range(N):

        # Find the log a of arr[i]
        log_a = int(math.log(arr[i]) /
                    math.log(a))

        # Find the power of a less
        # than and greater than a
        A = int(pow(a, log_a))
        B = int(pow(a, log_a + 1))

        if ((arr[i] - A) < (B - arr[i])):
            log_a = A
        else:
            log_a = B

        # Find the log b of arr[i]
        log_b = int(math.log(arr[i]) /
                    math.log(b))

        # Find the power of b less than
        # and greater than b
        A = int(pow(b, log_b))
        B = int(pow(b, log_b + 1))

        if ((arr[i] - A) < (B - arr[i])):
            log_b = A
        else:
            log_b = B

        # Update arr[i] with absolute
        # difference of log_a & log _b
        arr[i] = abs(log_a - log_b)

    # Print the modified array
    printArray(arr, N)

# Driver Code
arr = [ 5, 12, 25 ]
A = 2
B = 3
N = len(arr)

nearestPowerDiff(arr, N, A, B)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to print the array
static void printArray(int[] arr, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to modify array elements
// by absolute difference of the
// nearest perfect power of a and b
static void nearestPowerDiff(int[] arr, int N,
                             int a, int b)
{

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Find the log a of arr[i]
        int log_a = (int)(Math.Log(arr[i]) /
                          Math.Log(a));

        // Find the power of a less
        // than and greater than a
        int A = (int)(Math.Pow(a, log_a));
        int B = (int)(Math.Pow(a, log_a + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_a = A;
        else
            log_a = B;

        // Find the log b of arr[i]
        int log_b = (int)(Math.Log(arr[i]) /
                          Math.Log(b));

        // Find the power of b less than
        // and greater than b
        A = (int)(Math.Pow(b, log_b));
        B = (int)(Math.Pow(b, log_b + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_b = A;
        else
            log_b = B;

        // Update arr[i] with absolute
        // difference of log_a & log _b
        arr[i] = Math.Abs(log_a - log_b);
    }

    // Print the modified array
    printArray(arr, N);
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 5, 12, 25 };
    int A = 2, B = 3;
    int N = arr.Length;

    nearestPowerDiff(arr, N, A, B);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to print the array
function printArray(arr, N)
{

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        document.write(arr[i] + " ");
    }
}

// Function to modify array elements
// by absolute difference of the
// nearest perfect power of a and b
function nearestPowerDiff(arr, N,
                             a, b)
{

    // Traverse the array arr[]
    for(let i = 0; i < N; i++)
    {

        // Find the log a of arr[i]
        let log_a = Math.floor(Math.log(arr[i]) /
                          Math.log(a));

        // Find the power of a less
        // than and greater than a
        let A = Math.floor(Math.pow(a, log_a));
        let B = Math.floor(Math.pow(a, log_a + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_a = A;
        else
            log_a = B;

        // Find the log b of arr[i]
        let log_b = Math.floor(Math.log(arr[i]) /
                          Math.log(b));

        // Find the power of b less than
        // and greater than b
        A = Math.floor(Math.pow(b, log_b));
        B = Math.floor(Math.pow(b, log_b + 1));

        if ((arr[i] - A) < (B - arr[i]))
            log_b = A;
        else
            log_b = B;

        // Update arr[i] with absolute
        // difference of log_a & log _b
        arr[i] = Math.abs(log_a - log_b);
    }

    // Print the modified array
    printArray(arr, N);
}

// Driver code

        let arr = [ 5, 12, 25 ];
    let A = 2, B = 3;
    let N = arr.length;

    nearestPowerDiff(arr, N, A, B);

    // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1 7 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)