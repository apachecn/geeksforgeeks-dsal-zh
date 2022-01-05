# 交换交替边界对

> 原文:[https://www . geesforgeks . org/swap-alternate-boundary-pairs/](https://www.geeksforgeeks.org/swap-alternate-boundary-pairs/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是交换第一个和最后一个元素，然后第三个和第三个最后一个元素，然后第五个和第五个最后一个元素，以此类推。在所有有效操作后打印最终数组。

> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 6 2 4 3 5 1
> 操作 1:交换 1 和 6
> 操作 2:交换 3 和 4
> **输入:** arr[] = {5，54，12，63，45}
> **输出:** 45 54 12 63 5

**方法:**初始化指针 **i = 0** 和**j = N–1**然后交换这些指针处的元素并更新 **i = i + 2** 和**j = j–2**。重复这些步骤，同时 **i < j** 。最后打印更新后的数组。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print
// the contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to update the array
void UpdateArr(int arr[], int n)
{

    // Initialize the pointers
    int i = 0, j = n - 1;

    // While there are elements to swap
    while (i < j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;

        // Update the pointers
        i += 2;
        j -= 2;
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    UpdateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Utility function to print
    // the contents of an array
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to update the array
    static void UpdateArr(int arr[], int n)
    {

        // Initialize the pointers
        int i = 0, j = n - 1;

        // While there are elements to swap
        while (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            // Update the pointers
            i += 2;
            j -= 2;
        }

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int n = arr.length;

        UpdateArr(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# the contents of an array
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = " ");

# Function to update the array
def UpdateArr(arr, n):

    # Initialize the pointers
    i = 0;
    j = n - 1;

    # While there are elements to swap
    while (i < j):
        temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;

        # Update the pointers
        i += 2;
        j -= 2;

    # Print the updated array
    printArr(arr, n);

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6 ];
    n = len(arr);

    UpdateArr(arr, n);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Utility function to print
    // the contents of an array
    static void printArr(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to update the array
    static void UpdateArr(int []arr, int n)
    {

        // Initialize the pointers
        int i = 0, j = n - 1;

        // While there are elements to swap
        while (i < j)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            // Update the pointers
            i += 2;
            j -= 2;
        }

        // Print the updated array
        printArr(arr, n);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 1, 2, 3, 4, 5, 6 };
        int n = arr.Length;

        UpdateArr(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Utility function to print
// the contents of an array
function printArr(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to update the array
function UpdateArr(arr, n)
{

    // Initialize the pointers
    let i = 0, j = n - 1;

    // While there are elements to swap
    while (i < j) {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;

        // Update the pointers
        i += 2;
        j -= 2;
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code

    let arr = [ 1, 2, 3, 4, 5, 6 ];
    let n = arr.length;;

    UpdateArr(arr, n);

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
6 2 4 3 5 1
```