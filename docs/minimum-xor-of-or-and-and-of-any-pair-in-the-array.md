# 数组中任意一对“或”与“与”的最小异或

> 原文:[https://www . geesforgeks . org/阵列中任意对的最小异或/](https://www.geeksforgeeks.org/minimum-xor-of-or-and-and-of-any-pair-in-the-array/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]****N**的任务是找到给定数组中任意一对的按位“或”与“与”的按位“异或”的最小值。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1
> **解释:**
> 对于元素 2 & 3:
> 表达式(2 & 3)异或(2|3)的值为 1，这是给定数组中所有对的最小值。
> **输入:** arr[] = {3，6，8，4，5}
> **输出:** 1
> **解释:**
> 对于元素 4 & 5:
> 表达式(4 & 5) xor (4|5)的值为 1，这是给定数组中所有对的最小值。

**方法:**对于任意一对元素，如 **X** 和 **Y** ，表达式 **(X & Y) xor (X|Y)** 的值可以写成:

> = >(x.y)^(x+y)
> =>(x . y)(x+y)'+(x . y)'(x+y)
> =>(x . y)(x)。Y ')+(X '+Y ')(X+Y)
> =>X . X ' . Y . Y '+X '。X+X’。Y+Y’。x+Y’。y
> =>0+0+X’。Y+Y’。X + 0
> = > X^Y

根据以上计算，对于给定数组中的任意对 **(X，Y)** ，表达式 **(X & Y)异或(X|Y)** 简化为 **X 异或 Y** 。因此，给定数组中任意对的按位“或”与“与”的按位“异或”的最小值就是最小值对的“异或”，可以使用本文中讨论的方法来计算。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// value of XOR of AND and OR of
// any pair in the given array
int maxAndXor(int arr[], int n)
{
    int ans = INT_MAX;

    // Sort the array
    sort(arr, arr + n);

    // Traverse the array arr[]
    for (int i = 0; i < n - 1; i++) {

        // Compare and Find the minimum
        // XOR value of an array.
        ans = min(ans, arr[i] ^ arr[i + 1]);
    }

    // Return the final answer
    return ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maxAndXor(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to for above approach
import java.io.*;
import java.util.Arrays;
class GFG {

    // Function to find the minimum
    // value of XOR of AND and OR of
    // any pair in the given array
    static int maxAndXor(int arr[], int n)
    {
        int ans = Integer.MAX_VALUE;

        // Sort the array
        Arrays.sort(arr);

        // Traverse the array arr[]
        for (int i = 0; i < n - 1; i++) {

            // Compare and Find the minimum
            // XOR value of an array.
            ans = Math.min(ans, arr[i] ^ arr[i + 1]);
        }

        // Return the final answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = new int[] { 1, 2, 3, 4, 5 };

        int N = arr.length;

        // Function Call
        System.out.println(maxAndXor(arr, N));
    }
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum
# value of XOR of AND and OR of
# any pair in the given array

def maxAndXor(arr, n):

    ans = float('inf')

    # Sort the array
    arr.sort()

    # Traverse the array arr[]
    for i in range(n - 1):

        # Compare and Find the minimum
        # XOR value of an array.
        ans = min(ans, arr[i] ^ arr[i + 1])

    # Return the final answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 2, 3, 4, 5]
    N = len(arr)

    # Function Call
    print(maxAndXor(arr, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to for above approach
using System;
class GFG {

    // Function to find the minimum
    // value of XOR of AND and OR of
    // any pair in the given array
    static int maxAndXor(int[] arr, int n)
    {
        int ans = 9999999;

        // Sort the array
        Array.Sort(arr);

        // Traverse the array arr[]
        for (int i = 0; i < n - 1; i++) {

            // Compare and Find the minimum
            // XOR value of an array.
            ans = Math.Min(ans, arr[i] ^ arr[i + 1]);
        }

        // Return the final answer
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        // Given array arr[]
        int[] arr = new int[] { 1, 2, 3, 4, 5 };

        int N = arr.Length;

        // Function Call
        Console.Write(maxAndXor(arr, N));
    }
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the minimum
    // value of XOR of AND and OR of
    // any pair in the given array
    function maxAndXor(arr, n)
    {
        let ans = Number.MAX_VALUE;

        // Sort the array
        arr.sort();

        // Traverse the array arr[]
        for (let i = 0; i < n - 1; i++) {

            // Compare and Find the minimum
            // XOR value of an array.
            ans = Math.min(ans, arr[i] ^ arr[i + 1]);
        }

        // Return the final answer
        return ans;
    }

// Driver Code

    // Given array arr[]
        let arr = [ 1, 2, 3, 4, 5 ];

        let N = arr.length;

        // Function Call
        document.write(maxAndXor(arr, N));

 // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*