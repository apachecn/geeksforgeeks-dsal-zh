# 从中心开始以螺旋方式对给定数组进行排序

> 原文:[https://www . geeksforgeeks . org/排序-以螺旋方式给定数组-从中心开始/](https://www.geeksforgeeks.org/sort-the-given-array-in-spiral-manner-starting-from-the-center/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是[从数组的中间开始按降序](https://www.geeksforgeeks.org/sort-c-stl/)对数组进行排序，在中间元素的右边有下一个最大的元素，在中间元素的左边有下一个最大的元素，以此类推。

**示例:**

> **输入:** arr[] = {4，9，3，5，7}
> **输出:** 3 5 9 7 4
> **解释:**
> 数组中最大的元素是 9 在索引= 2 时保持在数组中间。
> 下一个最大的元素是 7，放在索引= 3 的中间元素的右边。
> 第三大元素是 5，位于索引= 1 的中间元素的左侧。
> 第四大元素是 4，放在索引= 4 的元素 7 的右边。
> 最小的元素是 3，放在索引= 0 的元素是 5 的左边。
> 
> **输入:** arr[] = {4，5，3，7，6，9，7}
> **输出:** 3 5 7 9 7 6 4
> **解释:**
> 数组中最大的元素是 9 在索引= 3 时保持在数组中间。
> 下一个最大的元素是 7，放在索引= 3 的中间元素的右边。
> 第三大元素是 7，位于索引= 2 的中间元素的左侧。
> 第四大元素是 6，位于索引= 5 的元素 7 的右侧。
> 第五大元素是 5，位于索引= 1 的元素 7 的左侧。
> 第六大元素是 4，位于索引= 6 的元素 6 的右侧。
> 最小的元素是 3，放在索引= 0 的元素 5 的左边。

**方法:**想法是使用[冒泡排序](https://www.geeksforgeeks.org/bubble-sort/)并从最小的元素开始排序数组。首先，将最小的元素放在最左边的索引中，然后将下一个最小的元素放在最右边的索引中。以下是步骤:

*   初始化变量，比如**左= 0** 、**右= N–1**和 **i = 1** 。
*   从左侧位置开始，即从**左侧= 0** 开始，然后在数组的剩余部分执行冒泡排序，找到最小的元素并将其放置在最左侧位置，直到 **i ==右侧**。
*   增加 **1** 左边的值，因为它的元素已经放置好了，不需要改变。
*   从右侧位置开始，再次执行反向遍历的冒泡排序，找到最小的元素并将其放置在右侧位置，直到 **i ==左侧**。
*   右减 **1** 的值，因为它的元素已经被放置，不需要改变。
*   如果 **N** 为偶数，最小的元素应该出现在数组的最右端，但是在我们的方法中，最小的元素被放置在最左端。因此，为了实现所需的模式，请反转数组的前半部分。
*   打印修改后的排序数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort the array
// according to the given pattern
void centerSpiralSort(int arr[], int N)
{
    // Initializing the variables
    int left = 0;
    int right = N - 1;
    int i = 1;

    while (left < right) {

        // Performing bubble sort
        for (i = left + 1; i <= right;
             i++) {
            if (arr[left] > arr[i]) {

                // Swapping if
                // arr[left] > arr[i]
                swap(arr[left], arr[i]);
            }
        }

        // Increment left by 1
        left++;

        // Performing bubble sort
        for (i = right - 1; i >= left;
             i--) {
            if (arr[right] > arr[i]) {

                // Swapping if
                // arr[right] > arr[i]
                swap(arr[right], arr[i]);
            }
        }

        // Decrement right by 1
        right--;
    }

    // If N is an even number
    // Reversing the array from 0 to N/2-1
    if (N % 2 == 0) {

        // Reversing the half array
        for (int i = 0; i < N / 2; i++) {
            swap(arr[i], arr[N - 1 - i]);
        }
    }

    // Print the elements of the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 4, 9, 3, 5, 7 };

    // Size of the array
    int N = sizeof arr / sizeof arr[0];

    // Function Call
    centerSpiralSort(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to sort the array
    // according to the given pattern
    static void centerSpiralSort(int arr[], int N)
    {

        // Initializing the variables
        int left = 0;
        int right = N - 1;
        int i = 1;
        int temp;

        while (left < right) {

            // Performing bubble sort
            for (i = left + 1; i <= right; i++) {
                if (arr[left] > arr[i]) {

                    // Swapping if
                    // arr[left] > arr[i]
                    temp = arr[left];
                    arr[left] = arr[i];
                    arr[i] = temp;
                }
            }

            // Increment left by 1
            left++;

            // Performing bubble sort
            for (i = right - 1; i >= left; i--) {
                if (arr[right] > arr[i]) {

                    // Swapping if
                    // arr[right] > arr[i]
                    temp = arr[right];
                    arr[right] = arr[i];
                    arr[i] = temp;
                }
            }

            // Decrement right by 1
            right--;
        }

        // If N is an even number
        // Reversing the array from 0 to N/2-1
        if (N % 2 == 0) {

            // Reversing the half array
            for (i = 0; i < N / 2; i++) {
                temp = arr[i];
                arr[i] = arr[N - 1 - i];
                arr[N - 1 - i] = temp;
            }
        }

        // Print the elements of the array
        for (i = 0; i < N; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int arr[] = { 4, 9, 3, 5, 7 };

        // Size of the array
        int N = arr.length;

        // Function Call
        centerSpiralSort(arr, N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to sort the array
# according to the given pattern
def centerSpiralSort(arr, N):

    # Initializing the variables
    left = 0
    right = N - 1
    i = 1

    while (left < right):

        # Performing bubble sort
        for i in range(left + 1, right + 1, 1):
            if (arr[left] > arr[i]):

                # Swapping if
                # arr[left] > arr[i]
                temp = arr[left]
                arr[left] = arr[i]
                arr[i] = temp

        # Increment left by 1
        left += 1

        # Performing bubble sort
        i = right - 1

        while(i >= left):
            if (arr[right] > arr[i]):

                # Swapping if
                # arr[right] > arr[i]
                temp = arr[right]
                arr[right] = arr[i]
                arr[i] = temp

            i -= 1

        # Decrement right by 1
        right -= 1

    # If N is an even number
    # Reversing the array from 0 to N/2-1
    if (N % 2 == 0):

        # Reversing the half array
        for i in range(N / 2):
            temp = arr[i]
            arr[i] = arr[N - 1 - i]
            arr[N - 1 - i] = temp

    # Print the elements of the array
    for i in range(N):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 4, 9, 3, 5, 7 ]

    # Size of the array
    N = len(arr)

    # Function Call
    centerSpiralSort(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to sort the array
// according to the given pattern
static void centerSpiralSort(int []arr, int N)
{

    // Initializing the variables
    int left = 0;
    int right = N - 1;
    int i = 1;
    int temp;

    while (left < right)
    {

        // Performing bubble sort
        for(i = left + 1; i <= right; i++)
        {
            if (arr[left] > arr[i])
            {

                // Swapping if
                // arr[left] > arr[i]
                temp = arr[left];
                arr[left] = arr[i];
                arr[i] = temp;
            }
        }

        // Increment left by 1
        left++;

        // Performing bubble sort
        for(i = right - 1; i >= left; i--)
        {
            if (arr[right] > arr[i])
            {

                // Swapping if
                // arr[right] > arr[i]
                temp = arr[right];
                arr[right] = arr[i];
                arr[i] = temp;
            }
        }

        // Decrement right by 1
        right--;
    }

    // If N is an even number
    // Reversing the array from 0 to N/2-1
    if (N % 2 == 0)
    {

        // Reversing the half array
        for(i = 0; i < N / 2; i++)
        {
            temp = arr[i];
            arr[i] = arr[N - 1 - i];
            arr[N - 1 - i] = temp;
        }
    }

    // Print the elements of the array
    for(i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 4, 9, 3, 5, 7 };

    // Size of the array
    int N = arr.Length;

    // Function Call
    centerSpiralSort(arr, N);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to sort the array
// according to the given pattern
function centerSpiralSort(arr, N) {
  // Initializing the variables
  let left = 0;
  let right = N - 1;
  let i = 1;

  while (left < right) {
    // Performing bubble sort
    for (i = left + 1; i <= right; i++) {
      if (arr[left] > arr[i]) {
        // Swapping if
        // arr[left] > arr[i]
        let temp = arr[left];
        arr[left] = arr[i];
        arr[i] = temp;
      }
    }

    // Increment left by 1
    left++;

    // Performing bubble sort
    for (i = right - 1; i >= left; i--) {
      if (arr[right] > arr[i]) {
        // Swapping if
        // arr[right] > arr[i]
        let temp = arr[right];
        arr[right] = arr[i];
        arr[i] = temp;
      }
    }

    // Decrement right by 1
    right--;
  }

  // If N is an even number
  // Reversing the array from 0 to N/2-1
  if (N % 2 == 0) {
    // Reversing the half array
    for (let i = 0; i < N / 2; i++) {
      let temp = arr[N - 1 - i];
      arr[N - 1 - i] = arr[i];
      arr[i] = temp;
    }
  }

  // Print the elements of the array
  for (let i = 0; i < N; i++) {
    document.write(arr[i] + " ");
  }
}

// Driver Code

// Given array
let arr = [4, 9, 3, 5, 7];

// Size of the array
let N = arr.length;

// Function Call
centerSpiralSort(arr, N);

</script>
```

**Output**

```
3 5 9 7 4 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*