# 通过多次交换元素对有一个放错位置的数组进行排序

> 原文:[https://www . geeksforgeeks . org/通过任意次数交换元素来排序有一个放错位置的数组/](https://www.geeksforgeeks.org/sort-the-array-having-one-misplaced-number-by-swapping-elements-any-number-of-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，该数组除了一个元素外都是**排序的**。给出了错位元素的位置 **pos** ，任务是让通过 [**排序的完整数组任意多次交换**](https://www.geeksforgeeks.org/python-program-to-swap-two-elements-in-a-list/) 任意两个元素。

**示例:**

> **输入** : N = 7，pos = 6，arr = {1，2，3，4，9，15，0}
> **输出:** 0 1 2 3 4 9 15
> **解释:**
> 应用以下互换 arr 可以排序:
> 
> 1.交换元素 0 和 1，现在 arr 是{0，2，3，4，9，15，1}
> 2。交换元素 1 和 2，现在 arr 是{0，1，3，4，9，15，2}
> 3。交换元素 2 和 3，现在 arr 是{0，1，2，4，9，15，3}
> 4。交换元素 3 和 4，现在 arr 是{0，1，2，3，9，15，4}
> 5。交换元素 4 和 9，现在 arr 是{0，1，2，3，4，15，9}
> 6。交换元素 9 和 15，现在 arr 是{0，1，2，3，4，9，15}
> 
> 我们现在可以看到，arr[ ]数组已经排序。
> 
> **输入:** N = 4，pos = 2，arr = {2，3，1，4，}
> T3】输出: 1 2 3 4

**进场:**这个问题可以用 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。由于最终数组要排序，放错位置的元素左侧的**元素必须更小，右侧的元素必须更大**。按照下面给出的步骤解决问题:

*   遍历数组 **arr[ ]** ，如果左边元素从**位置 arr[i]** 开始，大于 **arr[pos]** ，**交换 arr[i]和 arr[pos]** 。
*   如果从**位置[j]** 开始的右侧元素小于**位置**，**交换位置[j]和位置**。
*   打印 **arr[ ]** 将是最后一步。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>

using namespace std;

// Function to print sorted array
void PrintSortedArr(int n, int pos, int arr[])
{

    // Traversing element of array.
    for (int i = 0; i < n; ++i) {

        // For the element on left of pos
        if (i < pos) {
            if (arr[pos] < arr[i]) {
                swap(arr[pos], arr[i]);
            }
        }

        // For the element on right of pos
        else if (i > pos) {
            if (arr[pos] > arr[i]) {
                swap(arr[pos], arr[i]);
                pos = i;
            }
        }
    }

    // Printing the sorted array
    cout << "Sorted Array: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{

    // Given Input
    int N = 7, pos = 6;
    int arr[] = { 1, 2, 3, 4, 9, 15, 0 };

    // Function Call
    PrintSortedArr(N, pos, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to print sorted array
static void PrintSortedArr(int n, int pos, int arr[])
{

    // Traversing element of array.
    for (int i = 0; i < n; ++i) {

        // For the element on left of pos
        if (i < pos) {
            if (arr[pos] < arr[i]) {
                int t = arr[pos];
                arr[pos] = arr[i];
                arr[i] = t;
            }
        }

        // For the element on right of pos
        else if (i > pos) {
            if (arr[pos] > arr[i]) {
                int t = arr[pos];
                arr[pos] = arr[i];
                arr[i] = t;
                pos = i;
            }
        }
    }

    // Printing the sorted array
    System.out.print("Sorted Array: ");
    for (int i = 0; i < n; ++i) {
        System.out.print( arr[i] + " ");
    }
}

// Driver code
public static void main(String args[])
{
    // Given Input
    int N = 7, pos = 6;
    int arr[] = { 1, 2, 3, 4, 9, 15, 0 };

    // Function Call
    PrintSortedArr(N, pos, arr);

}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python 3 program for the above approach.

# Function to print sorted array
def PrintSortedArr(n, pos, arr):
    # Traversing element of array.
    for i in range(n):
        # For the element on left of pos
        if (i < pos):
            if (arr[pos] < arr[i]):
                temp = arr[pos]
                arr[pos] = arr[i]
                arr[i] = temp

        # For the element on right of pos
        elif (i > pos):
            if (arr[pos] > arr[i]):
                temp = arr[pos]
                arr[pos] = arr[i]
                arr[i] = temp
                pos = i

    # Printing the sorted array
    print("Sorted Array: ",end="")
    for i in range(n):
        print(arr[i],end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 7
    pos = 6
    arr = [1, 2, 3, 4, 9, 15, 0]

    # Function Call
    PrintSortedArr(N, pos, arr)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print sorted array
static void PrintSortedArr(int n, int pos, int []arr)
{

    // Traversing element of array.
    for (int i = 0; i < n; ++i) {

        // For the element on left of pos
        if (i < pos) {
            if (arr[pos] < arr[i]) {
                int t = arr[pos];
                arr[pos] = arr[i];
                arr[i] = t;
            }
        }

        // For the element on right of pos
        else if (i > pos) {
            if (arr[pos] > arr[i]) {
                int t = arr[pos];
                arr[pos] = arr[i];
                arr[i] = t;
                pos = i;
            }
        }
    }

    // Printing the sorted array
    Console.Write("Sorted Array: ");
    for (int i = 0; i < n; ++i) {
        Console.Write( arr[i] + " ");
    }
}

// Driver code
public static void Main(String []args)
{
    // Given Input
    int N = 7, pos = 6;
    int []arr = { 1, 2, 3, 4, 9, 15, 0 };

    // Function Call
    PrintSortedArr(N, pos, arr);

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to print sorted array
        function PrintSortedArr(n, pos, arr) {

            // Traversing element of array.
            for (let i = 0; i < n; ++i) {

                // For the element on left of pos
                if (i < pos) {
                    if (arr[pos] < arr[i]) {
                        let temp = arr[pos];
                        arr[pos] = arr[i];
                        arr[i] = temp;
                    }
                }

                // For the element on right of pos
                else if (i > pos) {
                    if (arr[pos] > arr[i]) {
                        let temp = arr[pos];
                        arr[pos] = arr[i];
                        arr[i] = temp;
                        pos = i;
                    }
                }
            }

            // Printing the sorted array
            document.write("Sorted Array: ");
            for (let i = 0; i < n; ++i) {
                document.write(arr[i] + " ");
            }
        }

        // Driver Code

        // Given Input
        let N = 7, pos = 6;
        let arr = [1, 2, 3, 4, 9, 15, 0];

        // Function Call
        PrintSortedArr(N, pos, arr);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
Sorted Array: 0 1 2 3 4 9 15 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)