# 快速排序算法是否自适应

> 原文:[https://www . geesforgeks . org/is-quick-sort-algorithm-adaptive-or-not/](https://www.geeksforgeeks.org/is-quick-sort-algorithm-adaptive-or-not/)

先决条件:[快速排序算法](https://www.geeksforgeeks.org/quick-sort/)

**适应性[快速排序算法](https://www.geeksforgeeks.org/quick-sort/)中的**是指如果给我们一个已经[排序](http://www.geeksforgeeks.org/search-an-element-in-a-sorted-and-pivoted-array/)的[数组](https://www.geeksforgeeks.org/array-data-structure/)，那么应该执行还是不执行操作，即**如果在排序数组上执行的操作数不等于在未排序数组上执行的操作数，那么该算法称为自适应。**

在本文中，我们将看到 **<u>快速排序算法是否自适应</u>** 。

**举个例子:**

> int arr[] = {1，2，3，4，5 }；

所以在上面的例子中，我们可以看到[数组是经过排序的](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。但是当数组是**未排序的**时，那么就应该执行操作，我们知道在最坏的情况下快速排序的时间复杂度是 **O(N^2)** 。因此，如果数组未排序，那么要排序的[数组的时间复杂度为](https://www.geeksforgeeks.org/sorting-algorithms/)o(n^2)，

**原因**:因为要排序数组 **N-1** 传球应该做 **N-i-1** 互换。

**快速排序算法不自适应**，

**<u>我们能让快速排序算法自适应吗？</u>T3】**

是的，我们可以很容易地使它自适应。

**例如:**

在下面的代码中，我们创建了一个 ***void*** 函数***AdaptiveBubbleSort***，它接受参数**“arr[]，n”**，这是一个数组，其大小为 **n** 。

我们已经创建了 **isSorted** 整数变量，该变量用 **0** 初始化，如果它被排序为 **IsSorted = 1** ，则内部 for 循环将不执行，但如果它不执行，则执行内部 for 循环，此外，如果我们发现元素 **j+1** 比当前元素 **j** 少，则在交换它们之后交换它们，直到它被排序。

最后，调用**导出的**变量并返回。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the array
void Print(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Function for adaptive sort algorithm
// to sort the array if the array is not
// sorted otherwise return in one-pass.
void AdaptiveBubbleSort(int arr[], int n)
{

    int temp;

    // Stores the status of the array of
    // sorted or not.
    int isSorted = 0;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Initialize it with 1
        isSorted = 1;

        // Compare the adjacent elements
        for (int j = 0; j < n - i - 1; j++) {

            // Violates the condition that the
            // array is not sorted
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                isSorted = 0;
            }
        }

        // If the array is sorted, then return
        // the array and no need to compare elements
        if (isSorted) {
            return;
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = 5;
    cout << "Array before sorting : ";
    Print(arr, n);
    AdaptiveBubbleSort(arr, n);
    cout << "Array after sorting : ";
    Print(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the array
static void Print(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        System.out.print(arr[i]+ " ");
    }
    System.out.println();
}

// Function for adaptive sort algorithm
// to sort the array if the array is not
// sorted otherwise return in one-pass.
static void AdaptiveBubbleSort(int arr[], int n)
{

    int temp;

    // Stores the status of the array of
    // sorted or not.
    int isSorted = 0;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Initialize it with 1
        isSorted = 1;

        // Compare the adjacent elements
        for (int j = 0; j < n - i - 1; j++) {

            // Violates the condition that the
            // array is not sorted
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                isSorted = 0;
            }
        }

        // If the array is sorted, then return
        // the array and no need to compare elements
        if (isSorted!=0) {
            return;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = 5;
    System.out.print("Array before sorting : ");
    Print(arr, n);
    AdaptiveBubbleSort(arr, n);
    System.out.print("Array after sorting : ");
    Print(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print the array
def Print(arr, n):
    for i in range(n):
        print(arr[i], end=" ")
    print("")

# Function for adaptive sort algorithm
# to sort the array if the array is not
# sorted otherwise return in one-pass.
def AdaptiveBubbleSort(arr, n):

    # Stores the status of the array of
    # sorted or not.
    isSorted = 0

    # Traverse the array
    for i in range(n - 1):

        # Initialize it with 1
        isSorted = 1

        # Compare the adjacent elements
        for j in range(n - i - 1):

            # Violates the condition that the
            # array is not sorted
            if (arr[j] > arr[j + 1]):
                temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
                isSorted = 0

        # If the array is sorted, then return
        # the array and no need to compare elements
        if (isSorted):
            return

# Driver Code
arr = [1, 2, 3, 4, 5]
n = 5
print("Array before sorting : ")
Print(arr, n)
AdaptiveBubbleSort(arr, n)
print("Array after sorting : ")
Print(arr, n)

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the array
static void Print(int[] arr, int n)
{
    for (int i = 0; i < n; i++) {
        Console.Write(arr[i]+ " ");
    }
    Console.WriteLine();
}

// Function for adaptive sort algorithm
// to sort the array if the array is not
// sorted otherwise return in one-pass.
static void AdaptiveBubbleSort(int[] arr, int n)
{

    int temp;

    // Stores the status of the array of
    // sorted or not.
    int isSorted = 0;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Initialize it with 1
        isSorted = 1;

        // Compare the adjacent elements
        for (int j = 0; j < n - i - 1; j++) {

            // Violates the condition that the
            // array is not sorted
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                isSorted = 0;
            }
        }

        // If the array is sorted, then return
        // the array and no need to compare elements
        if (isSorted != 0) {
            return;
        }
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int n = 5;
    Console.Write("Array before sorting : ");
    Print(arr, n);
    AdaptiveBubbleSort(arr, n);
    Console.Write("Array after sorting : ");
    Print(arr, n);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to print the array
    const Print = (arr, n) => {
        for (let i = 0; i < n; i++) {
            document.write(`${arr[i]} `);
        }
        document.write("<br/>");
    }

    // Function for adaptive sort algorithm
    // to sort the array if the array is not
    // sorted otherwise return in one-pass.
    const AdaptiveBubbleSort = (arr, n) => {

        let temp;

        // Stores the status of the array of
        // sorted or not.
        let isSorted = 0;

        // Traverse the array
        for (let i = 0; i < n - 1; i++) {

            // Initialize it with 1
            isSorted = 1;

            // Compare the adjacent elements
            for (let j = 0; j < n - i - 1; j++) {

                // Violates the condition that the
                // array is not sorted
                if (arr[j] > arr[j + 1]) {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    isSorted = 0;
                }
            }

            // If the array is sorted, then return
            // the array and no need to compare elements
            if (isSorted) {
                return;
            }
        }
    }

    // Driver Code
    let arr = [1, 2, 3, 4, 5];
    let n = 5;
    document.write("Array before sorting : ");
    Print(arr, n);
    AdaptiveBubbleSort(arr, n);
    document.write("Array after sorting : ");
    Print(arr, n);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
Array before sorting : 1 2 3 4 5 
Array after sorting : 1 2 3 4 5 
```

因此，如果数组已经排序，那么每个元素几乎都会遍历一次。因此，时间复杂度变为 **O(N)** ，否则取 **O(N*log(N))。**
在所有情况下**辅助空间**将为 **O(1)。**