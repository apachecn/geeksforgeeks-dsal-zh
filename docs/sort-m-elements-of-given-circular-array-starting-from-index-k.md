# 从索引 K 开始对给定圆形数组的 M 个元素进行排序

> 原文:[https://www . geeksforgeeks . org/sort-m-给定循环数组的元素-从索引开始-k/](https://www.geeksforgeeks.org/sort-m-elements-of-given-circular-array-starting-from-index-k/)

给定一个大小为 **N** 的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**和两个整数 **K** 和 **M** ，任务是从索引 **K** 开始排序 **M** 数组元素。

**示例:**

> **输入:** arr[] = {4，1，6，5，3}，K = 2，M = 3
> **输出:** 4 1 3 5 6
> **解释:**从索引 2 开始对 3 个数组元素进行排序后，将 arr[]修改为{4，1，3，5，6}。
> 
> **输入:** arr[] = {67，2，9，7，1}，K = 4，M = 3
> **输出:** 2 67 9 7 1
> **解释:**从索引 4 开始对 3 个数组元素进行排序后，将 arr[]修改为{2，67，9，7，1}。

**方法:**想法是[交换圆形数组中相邻的元素](https://www.geeksforgeeks.org/minimum-swaps-required-sort-binary-array/)，如果它们的元素顺序不正确。按照以下步骤解决给定的问题:

*   [使用变量 **i** 在范围**【0，M–1】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 。
    *   使用变量 **j** 在范围**【K，K+M–1】**内再次遍历数组 **arr[]** ，如果 **arr[j%n]** 大于 **arr[(j + 1)%n]** ，则[交换当前相邻的值对](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)。
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the circular array
void printCircularArray(int arr[], int n)
{
    // Print the array
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to sort m elements of diven
// circular array starting from index k
void sortCircularArray(int arr[], int n,
                       int k, int m)
{
    // Traverse M elements
    for (int i = 0; i < m; i++) {

        // Iterate from index k to k + m - 1
        for (int j = k; j < k + m - 1; j++) {

            // Check if the next element
            // in the circular array is
            // less than the current element
            if (arr[j % n]
                > arr[(j + 1) % n]) {

                // Swap current element
                // with the next element
                swap(arr[j % n], arr[(j + 1) % n]);
            }
        }
    }

    // Print the circular array
    printCircularArray(arr, n);
}

// Driver Code
int main()
{
    int arr[] = { 4, 1, 6, 5, 3 };
    int K = 2, M = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    sortCircularArray(arr, N, K, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to print the circular array
static void printCircularArray(int arr[], int n)
{
    // Print the array
    for (int i = 0; i < n; i++) {
        System.out.print(arr[i] + " ");
    }
}

// Function to sort m elements of diven
// circular array starting from index k
static void sortCircularArray(int arr[], int n,
                       int k, int m)
{
    // Traverse M elements
    for (int i = 0; i < m; i++) {

        // Iterate from index k to k + m - 1
        for (int j = k; j < k + m - 1; j++) {

            // Check if the next element
            // in the circular array is
            // less than the current element
            if (arr[j % n]
                > arr[(j + 1) % n]) {

                // Swap current element
                // with the next element
                int t = arr[j % n];
                arr[j % n] = arr[(j + 1) % n];
                arr[(j + 1) % n] = t;
            }
        }
    }

    // Print the circular array
    printCircularArray(arr, n);
}

// Driver Code
public static void main (String[] args)
{  
    int[] arr = { 4, 1, 6, 5, 3 };
    int K = 2, M = 3;
    int N = arr.length;

    // Function Call
    sortCircularArray(arr, N, K, M);
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the circular array
def printCircularArray(arr, n):

    # Print the array
    for i in range(n):
        print(arr[i], end = " ")

# Function to sort m elements of diven
# circular array starting from index k
def sortCircularArray(arr, n, k, m):

    # Traverse M elements
    for i in range(m):

        # Iterate from index k to k + m - 1
        for j in range(k, k + m - 1):

            # Check if the next element
            # in the circular array is
            # less than the current element
            if (arr[j % n] > arr[(j + 1) % n]):

                # Swap current element
                # with the next element
                arr[j % n], arr[(j + 1) % n] = (arr[(j + 1) % n],
                                                arr[j % n])

    # Print the circular array
    printCircularArray(arr, n)

# Driver Code
if __name__ == "__main__" :

    arr = [ 4, 1, 6, 5, 3 ]
    K = 2
    M = 3
    N = len(arr)

    # Function Call
    sortCircularArray(arr, N, K, M)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to print the circular array
    static void printCircularArray(int []arr, int n)
    {
        // Print the array
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }

    // Function to sort m elements of diven
    // circular array starting from index k
    static void sortCircularArray(int []arr, int n,
                           int k, int m)
    {

        // Traverse M elements
        for (int i = 0; i < m; i++)
        {

            // Iterate from index k to k + m - 1
            for (int j = k; j < k + m - 1; j++)
            {

                // Check if the next element
                // in the circular array is
                // less than the current element
                if (arr[j % n]
                    > arr[(j + 1) % n]) {

                    // Swap current element
                    // with the next element
                    int t = arr[j % n];
                    arr[j % n] = arr[(j + 1) % n];
                    arr[(j + 1) % n] = t;
                }
            }
        }

        // Print the circular array
        printCircularArray(arr, n);
    }

    // Driver Code
    public static void Main (string[] args)
    {  
        int[] arr = { 4, 1, 6, 5, 3 };
        int K = 2, M = 3;
        int N = arr.Length;

        // Function Call
        sortCircularArray(arr, N, K, M);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the circular array
function printCircularArray(arr, n)
{
    // Print the array
    for (let i = 0; i < n; i++) {
        document.write(arr[i] + " ");
    }
}

// Function to sort m elements of diven
// circular array starting from index k
function sortCircularArray(arr, n, k, m)
{
    // Traverse M elements
    for (let i = 0; i < m; i++) {

        // Iterate from index k to k + m - 1
        for (let j = k; j < k + m - 1; j++) {

            // Check if the next element
            // in the circular array is
            // less than the current element
            if (arr[j % n]
                > arr[(j + 1) % n]) {

                // Swap current element
                // with the next element
                let t = arr[j % n];
                arr[j % n] = arr[(j + 1) % n];
                arr[(j + 1) % n] = t;
            }
        }
    }

    // Print the circular array
    printCircularArray(arr, n);
}

// Driver Code
    let arr = [ 4, 1, 6, 5, 3 ];
    let K = 2, M = 3;
    let N = arr.length;

    // Function Call
    sortCircularArray(arr, N, K, M);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
4 1 3 5 6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*