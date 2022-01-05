# 重新排列数组以最大化小于其相邻元素的元素

> 原文:[https://www . geeksforgeeks . org/重排数组以最大化比相邻元素都小的元素/](https://www.geeksforgeeks.org/rearrange-the-array-to-maximize-the-elements-which-is-smaller-than-both-its-adjacent-elements/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是[重新排列数组元素](https://www.geeksforgeeks.org/array-data-structure/array-rearrangement/)，使得小于其相邻元素的元素的[计数最大。](https://www.geeksforgeeks.org/count-of-array-elements-which-is-smaller-than-both-its-adjacent-elements/)

**注:**索引 **0** 左边和索引 **N-1** 右边的元素被认为是 **-INF。**

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 2 1 3 4
> **解释:**
> 一种可能的重新排列方式为{2，1，3，4}。
> 
> 1.  对于 arr[0](= 2)，大于其两侧的元素。
> 2.  对于 arr[1](= 1)，小于它两边的元素。
> 3.  对于 arr[2](= 3)，小于其右边的元素，大于其左边的元素。
> 4.  对于 arr[4](= 1)，大于它两边的元素。
> 
> 因此，在上述布置中，总共有 1 个阵列元件满足条件。这是最大的可能。
> 
> **输入:** arr[] = {2，7 }
> T3】输出: 2 7

**方法:**给定的问题可以基于以下观察来解决:

> 1.  The maximum number of indicators satisfying the conditions is **x** .
> 2.  Then, at least **(x+1)** larger elements are needed to realize it, because each element needs 2 larger elements.
> 3.  Therefore, the maximum number of neighboring elements less than it is given by **(n–1)/2** .

按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说大小为 **N** 的 **temp[]** ，存储重新排列的数组。
*   [按照递增顺序](https://www.geeksforgeeks.org/sort-c-stl/)对给定数组 **arr[]** 进行排序。
*   从数组**arr【】**中选择第一个**(N–1)/2**元素，并将它们放在数组**temp【】**的奇数索引处。
*   从数组**arr【】**中选择剩余的 **(N + 1)/2** 元素，并将其放置在数组**temp【】**中剩余的索引中。
*   最后，完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **temp[]** 作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange array such that
// count of element that are smaller than
// their adjacent elements is maximum
void maximumIndices(int arr[], int N)
{
    // Stores the rearranged array
    int temp[N] = { 0 };

    // Stores the maximum count of
    // elements
    int maxIndices = (N - 1) / 2;

    // Sort the given array
    sort(arr, arr + N);

    // Place the smallest (N - 1)/2
    // elements at odd indices
    for (int i = 0; i < maxIndices; i++) {
        temp[2 * i + 1] = arr[i];
    }

    // Placing the rest of the elements
    // at remaining indices
    int j = 0;

    for (int i = maxIndices; i < N;) {

        // If no element of the array
        // has been placed here
        if (temp[j] == 0) {
            temp[j] = arr[i];
            i++;
        }
        j++;
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        cout << temp[i] << " ";
    }
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    maximumIndices(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to rearrange array such that
    // count of element that are smaller than
    // their adjacent elements is maximum
    public static void maximumIndices(int arr[], int N)
    {
        // Stores the rearranged array
        int[] temp = new int[N];

        // Stores the maximum count of
        // elements
        int maxIndices = (N - 1) / 2;

        // Sort the given array
        Arrays.sort(arr);

        // Place the smallest (N - 1)/2
        // elements at odd indices
        for (int i = 0; i < maxIndices; i++) {
            temp[2 * i + 1] = arr[i];
        }

        // Placing the rest of the elements
        // at remaining indices
        int j = 0;

        for (int i = maxIndices; i < N;) {

            // If no element of the array
            // has been placed here
            if (temp[j] == 0) {
                temp[j] = arr[i];
                i++;
            }
            j++;
        }

        // Print the resultant array
        for (int i = 0; i < N; i++) {
            System.out.print(temp[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 1, 2, 3, 4 };
        int N = 4;

        // Function call
        maximumIndices(arr, N);
    }
}

// This code is contributed by RohitOberoi.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to rearrange array such that
# count of element that are smaller than
# their adjacent elements is maximum
def maximumIndices(arr, N):
    # Stores the rearranged array
    temp = [0] * N

    # Stores the maximum count of
    # elements
    maxIndices = (N - 1) // 2

    # Sort the given array
    arr.sort()

    # Place the smallest (N - 1)/2
    # elements at odd indices
    for i in range(maxIndices):
        temp[2 * i + 1] = arr[i]

    # Placing the rest of the elements
    # at remaining indices
    j = 0
    i = maxIndices

    while(i < N):

        # If no element of the array
        # has been placed here
        if (temp[j] == 0):
            temp[j] = arr[i]
            i += 1

        j += 1

    # Print the resultant array
    for i in range(N):
        print(temp[i], end=" ")

# Driver Code

# Input
arr = [1, 2, 3, 4]
N = len(arr)

# Function call
maximumIndices(arr, N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to rearrange array such that
// count of element that are smaller than
// their adjacent elements is maximum
public static void maximumIndices(int []arr, int N)
{

    // Stores the rearranged array
    int[] temp = new int[N];

    // Stores the maximum count of
    // elements
    int maxIndices = (N - 1) / 2;

    // Sort the given array
    Array.Sort(arr);

    // Place the smallest (N - 1)/2
    // elements at odd indices
    for(int i = 0; i < maxIndices; i++)
    {
        temp[2 * i + 1] = arr[i];
    }

    // Placing the rest of the elements
    // at remaining indices
    int j = 0;

    for(int i = maxIndices; i < N;)
    {

        // If no element of the array
        // has been placed here
        if (temp[j] == 0)
        {
            temp[j] = arr[i];
            i++;
        }
        j++;
    }

    // Print the resultant array
    for(int i = 0; i < N; i++)
    {
        Console.Write(temp[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    int []arr = { 1, 2, 3, 4 };
    int N = 4;

    // Function call
    maximumIndices(arr, N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

     // JavaScript program for the above approach

     // Function to rearrange array such that
     // count of element that are smaller than
     // their adjacent elements is maximum
     function maximumIndices(arr, N) {
         // Stores the rearranged array
         let temp = new Array(N).fill(0);

         // Stores the maximum count of
         // elements
         let maxIndices = parseInt((N - 1) / 2);

         // Sort the given array
         arr.sort(function (a, b) { return a - b; })

         // Place the smallest (N - 1)/2
         // elements at odd indices
         for (let i = 0; i < maxIndices; i++) {
             temp[2 * i + 1] = arr[i];
         }

         // Placing the rest of the elements
         // at remaining indices
         let j = 0;

         for (let i = maxIndices; i < N;) {

             // If no element of the array
             // has been placed here
             if (temp[j] == 0) {
                 temp[j] = arr[i];
                 i++;
             }
             j++;
         }

         // Print the resultant array
         for (let i = 0; i < N; i++) {
             document.write(temp[i] + " ");
         }
     }

     // Driver Code

     // Input
     let arr = [1, 2, 3, 4];
     let N = arr.length;

     // Function call
     maximumIndices(arr, N);

 // This code is contributed by Potta Lokesh

 </script>
```

**Output**

```
2 1 3 4 
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*