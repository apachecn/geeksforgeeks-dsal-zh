# 右旋转 K 次后打印数组|设置 2

> 原文:[https://www . geesforgeks . org/print-array-it-right-rotated-k-times-set-2/](https://www.geeksforgeeks.org/print-array-after-it-is-right-rotated-k-times-set-2/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-class-c/)**arr【】**和一个值 **K，**任务是[打印向右旋转 **K** 次的数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/)。

**示例:**

> **输入:** arr = {1，3，5，7，9}，K = 2
> **输出:** 7 9 1 3 5
> 
> **输入:** arr = {1，2，3，4，5}，K = 4
> T3】输出: 2 3 4 5 1

**算法:**给定的问题可以通过[反转子阵](https://www.geeksforgeeks.org/check-if-two-arrays-can-be-made-equal-by-reversing-any-subarray-once/)来解决。可以遵循以下步骤来解决问题:

*   将所有数组元素从 **1** 反转到 **N -1**
*   将数组元素从 **1** 反转到**K–1**
*   将数组元素从 **K** 反转到 **N -1**

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rotate the array
// to the right, K times
void RightRotate(int Array[], int N, int K)
{

    // Reverse all the array elements
    reverse(Array, Array + N);

    // Reverse the first k elements
    reverse(Array, Array + K);

    // Reverse the elements from K
    // till the end of the array
    reverse(Array + K, Array + N);

    // Print the array after rotation
    for (int i = 0; i < N; i++) {

        cout << Array[i] << " ";
    }

    cout << endl;
}

// Driver code
int main()
{

    // Initialize the array
    int Array[] = { 1, 2, 3, 4, 5 };

    // Find the size of the array
    int N = sizeof(Array) / sizeof(Array[0]);

    // Initialize K
    int K = 4;

    // Call the function and
    // print the answer
    RightRotate(Array, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
class GFG
{

    // Function to rotate the array
    // to the right, K times
    static void RightRotate(int[] Array, int N, int K)
    {

        // Reverse all the array elements
        for (int i = 0; i < N / 2; i++) {
            int temp = Array[i];
            Array[i] = Array[N - i - 1];
            Array[N - i - 1] = temp;
        }

        // Reverse the first k elements
        for (int i = 0; i < K / 2; i++) {
            int temp = Array[i];
            Array[i] = Array[K - i - 1];
            Array[K - i - 1] = temp;
        }

        // Reverse the elements from K
        // till the end of the array
        for (int i = 0; i < (K + N) / 2; i++) {
            int temp = Array[(i + K) % N];
            Array[(i + K) % N] = Array[(N - i + K - 1) % N];
            Array[(N - i + K - 1) % N] = temp;
        }

        // Print the array after rotation
        for (int i = 0; i < N; i++) {

            System.out.print(Array[i] + " ");
        }

        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int Array[] = { 1, 2, 3, 4, 5 };

        // Find the size of the array
        int N = Array.length;

        // Initialize K
        int K = 4;

        // Call the function and
        // print the answer
        RightRotate(Array, N, K);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to rotate the array
# to the right, K times
def RightRotate(Array, N, K):

    # Reverse all the array elements
    for i in range(math.ceil(N / 2)):
        temp = Array[i]
        Array[i] = Array[N - i - 1]
        Array[N - i - 1] = temp

    # Reverse the first k elements
    for i in range(math.ceil(K / 2)):
        temp = Array[i]
        Array[i] = Array[K - i - 1]
        Array[K - i - 1] = temp

    # Reverse the elements from K
    # till the end of the array
    for i in range(math.ceil((K + N) / 2)):
        temp = Array[(i + K) % N]
        Array[(i + K) % N] = Array[(N - i + K - 1) % N]
        Array[(N - i + K - 1) % N] = temp

    # Print the array after rotation
    for i in range(N):
        print(Array[i], end=" ")

# Driver Code
arr = [1, 2, 3, 4, 5]
N = len(arr)
K = 4

# Call the function and
# print the answer
RightRotate(arr, N, K)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
    // Function to rotate the array
    // to the right, K times
    static void RightRotate(int []Array, int N, int K)
    {

        // Reverse all the array elements
        for (int i = 0; i < N / 2; i++) {
            int temp = Array[i];
            Array[i] = Array[N - i - 1];
            Array[N - i - 1] = temp;
        }

        // Reverse the first k elements
        for (int i = 0; i < K / 2; i++) {
            int temp = Array[i];
            Array[i] = Array[K - i - 1];
            Array[K - i - 1] = temp;
        }

        // Reverse the elements from K
        // till the end of the array
        for (int i = 0; i < (K + N) / 2; i++) {
            int temp = Array[(i + K) % N];
            Array[(i + K) % N] = Array[(N - i + K - 1) % N];
            Array[(N - i + K - 1) % N] = temp;
        }

        // Print the array after rotation
        for (int i = 0; i < N; i++) {

            Console.Write(Array[i] + " ");
        }
    }

    // Driver code
    public static void Main()
    {

        // Initialize the array
        int []Array = { 1, 2, 3, 4, 5 };

        // Find the size of the array
        int N = Array.Length;

        // Initialize K
        int K = 4;

        // Call the function and
        // print the answer
        RightRotate(Array, N, K);
    }
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to rotate the array
// to the right, K times
function RightRotate(Array, N, K)
{

    // Reverse all the array elements
    for (let i = 0; i < N / 2; i++) {
        let temp = Array[i];
        Array[i] = Array[N - i - 1];
        Array[N - i - 1] = temp;
    }  

    // Reverse the first k elements
    for (let i = 0; i < K / 2; i++) {
        let temp = Array[i];
        Array[i] = Array[K - i - 1];
        Array[K - i - 1] = temp;
    }

    // Reverse the elements from K
    // till the end of the array
    for (let i = 0; i < (K + N) / 2; i++) {
        let temp = Array[(i + K) % N];
        Array[(i + K) % N] = Array[(N - i + K - 1) % N];
        Array[(N - i + K - 1) % N] = temp;
    }

    // Print the array after rotation
    for (let i = 0; i < N; i++) {
        document.write(Array[i] + " ");
    }
}

// Driver Code

let arr = [ 1, 2, 3, 4, 5 ];
let N = arr.length;
let K =4;

// Call the function and
// print the answer
RightRotate(arr, N, K);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2 3 4 5 1 
```

**时间复杂度** : O(N)
**辅助空间** : O(1)