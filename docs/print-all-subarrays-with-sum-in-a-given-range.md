# 打印给定范围内总和的所有子阵列

> 原文:[https://www . geeksforgeeks . org/print-给定范围内的所有子阵列总和/](https://www.geeksforgeeks.org/print-all-subarrays-with-sum-in-a-given-range/)

给定正整数数组 **arr[]** 和两个整数 **L** 和 **R** 定义范围**【L，R】**。任务是打印总和在 **L** 到 **R** 范围内的子阵列。

**示例:**

> **输入:** arr[] = {1，4，6}，L = 3，R = 8
> **输出:** {1，4}，{4}，{6}。
> **说明:**所有可能的子阵如下
> {1】和为 1。
> {1，4}与总和 5。
> {1，4，6}与 sum 11。
> {4}与 sum 4。
> {4，6}加和 10。
> {6}与 sum 6。
> 因此，子阵列{1，4}、{4}、{6}的和在范围[3，8]内。
> 
> **输入:** arr[] = {2，3，5，8}，L = 4，R = 13
> **输出:** {2，3}，{2，3，5}，{3，5}，{5}，{5，8}，{8}。

**方法:**这个问题可以通过使用两个循环进行蛮力和检查每个可能的子阵列来解决。下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find subarrays in given range
void subArraySum(int arr[], int n,
                 int leftsum, int rightsum)
{
    int curr_sum, i, j, res = 0;

    // Pick a starting point
    for (i = 0; i < n; i++) {
        curr_sum = arr[i];

        // Try all subarrays starting with 'i'
        for (j = i + 1; j <= n; j++) {
            if (curr_sum > leftsum
                && curr_sum < rightsum) {
                cout << "{ ";

                for (int k = i; k < j; k++)
                    cout << arr[k] << " ";

                cout << "}\n";
            }
            if (curr_sum > rightsum || j == n)
                break;
            curr_sum = curr_sum + arr[j];
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int L = 10, R = 23;

    subArraySum(arr, N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG
{

    // Function to find subarrays in given range
    static void subArraySum(int arr[], int n, int leftsum,
                            int rightsum)
    {
        int curr_sum, i, j, res = 0;

        // Pick a starting point
        for (i = 0; i < n; i++) {
            curr_sum = arr[i];

            // Try all subarrays starting with 'i'
            for (j = i + 1; j <= n; j++) {
                if (curr_sum > leftsum
                    && curr_sum < rightsum) {
                    System.out.print("{ ");

                    for (int k = i; k < j; k++)
                        System.out.print(arr[k] + " ");

                    System.out.println("}");
                }
                if (curr_sum > rightsum || j == n)
                    break;
                curr_sum = curr_sum + arr[j];
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 15, 2, 4, 8, 9, 5, 10, 23 };
        int N = arr.length;

        int L = 10, R = 23;

        subArraySum(arr, N, L, R);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for above approach

# Function to find subarrays in given range
def subArraySum (arr, n, leftsum, rightsum):
    res = 0

    # Pick a starting point
    for i in range(n):
        curr_sum = arr[i]

        # Try all subarrays starting with 'i'
        for j in range(i + 1, n + 1):
            if (curr_sum > leftsum
                and curr_sum < rightsum):
                print("{ ", end="")

                for k in range(i, j):
                    print(arr[k], end=" ")

                print("}")
            if (curr_sum > rightsum or j == n):
                break
            curr_sum = curr_sum + arr[j]

# Driver Code
arr = [15, 2, 4, 8, 9, 5, 10, 23]
N = len(arr)
L = 10
R = 23
subArraySum(arr, N, L, R)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

    // Function to find subarrays in given range
    static void subArraySum(int []arr, int n, int leftsum,
                            int rightsum)
    {
        int curr_sum, i, j, res = 0;

        // Pick a starting point
        for (i = 0; i < n; i++) {
            curr_sum = arr[i];

            // Try all subarrays starting with 'i'
            for (j = i + 1; j <= n; j++) {
                if (curr_sum > leftsum
                    && curr_sum < rightsum) {
                    Console.Write("{ ");

                    for (int k = i; k < j; k++)
                        Console.Write(arr[k] + " ");

                    Console.WriteLine("}");
                }
                if (curr_sum > rightsum || j == n)
                    break;
                curr_sum = curr_sum + arr[j];
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 15, 2, 4, 8, 9, 5, 10, 23 };
        int N = arr.Length;

        int L = 10, R = 23;

        subArraySum(arr, N, L, R);
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript program for above approach

    // Function to find subarrays in given range
    const subArraySum = (arr, n, leftsum, rightsum) => {
        let curr_sum, i, j, res = 0;

        // Pick a starting point
        for (i = 0; i < n; i++) {
            curr_sum = arr[i];

            // Try all subarrays starting with 'i'
            for (j = i + 1; j <= n; j++) {
                if (curr_sum > leftsum
                    && curr_sum < rightsum) {
                    document.write("{ ");

                    for (let k = i; k < j; k++)
                        document.write(`${arr[k]} `);

                    document.write("}<br/>");
                }
                if (curr_sum > rightsum || j == n)
                    break;
                curr_sum = curr_sum + arr[j];
            }
        }
    }

    // Driver Code
    let arr = [15, 2, 4, 8, 9, 5, 10, 23];
    let N = arr.length;
    let L = 10, R = 23;
    subArraySum(arr, N, L, R);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
{ 15 }
{ 15 2 }
{ 15 2 4 }
{ 2 4 8 }
{ 4 8 }
{ 4 8 9 }
{ 8 9 }
{ 8 9 5 }
{ 9 5 }
{ 5 10 }
```

**时间复杂度:** O(N^3)

**辅助空间:** O(1)