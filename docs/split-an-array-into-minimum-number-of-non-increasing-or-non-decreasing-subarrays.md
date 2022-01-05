# 将一个阵列分成最小数量的不增加或不减少的子阵列

> 原文:[https://www . geeksforgeeks . org/将数组拆分为最小数量的不增加或不减少的子数组/](https://www.geeksforgeeks.org/split-an-array-into-minimum-number-of-non-increasing-or-non-decreasing-subarrays/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是将给定的阵列分割成最小数量的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得每个子阵列的元素不是按照非递增顺序就是按照非递减顺序。

**示例:**

> **输入:** arr[] = {2，3，9，5，4，6，8}
> **输出:** 3
> **解释:**将阵列分成 3 个子阵列，如下三个子阵列:
> 
> 1.  {2，3，9}(非递减)
> 2.  {5，4}(不增加)
> 3.  {6，8}(非递减)
> 
> **输入:** arr[] = {2，5，3，3，4，5，0，2，1，0}
> **输出:** 4
> **解释:**将阵列拆分为以下 4 个子阵列:
> 
> 1.  {2，5}(非递减)
> 2.  {3，3，4，5}(非递减)
> 3.  {0，2}(非递减)
> 4.  {1，0}(非递增)

**方法:**为了最小化子阵列的数量，每个子阵列的大小应该最大化。这可以通过贪婪地将元素放置在子阵列中来实现。

按照以下步骤解决问题:

*   初始化一个变量，说 **ans** ，用 **1** 存储需要的结果，用 **N** 存储**电流**跟踪电流序列的顺序，是不递减 **(I)** 、不递增 **(D)** ，还是无 **(N)** 。
*   现在，[迭代范围为**【1，N–1】**的数组](https://www.geeksforgeeks.org/iterating-arrays-java/):
    *   如果**电流**等于 **N** ，执行以下操作:
        *   如果**arr【I】<arr【I-1】**则更新**当前**为 **D** 。
        *   否则，如果 **arr[i] > arr[i-1]** ，则更新**当前**为 **I** 。
        *   否则，将**当前**更新为 **N** 。
    *   如果****电流**等于 **I** ，执行以下操作:

        *   如果 **arr[i]≥arr[i-1]** ，则更新**当前**为 **I** 。
        *   否则，将**当前**更新为 **N** ，并将 **ans** 增加 **1** 。** 
    *   **否则，请执行以下操作:

        *   如果 **arr[i] ≤ arr[i-1]** ，则更新**当前**为 **D** 。
        *   否则，将**当前**更新为 **N** ，并将 **ans** 增加 **1** 。** 
*   **完成上述步骤后，打印**和**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
#include <bits/stdc++.h>
using namespace std;

// Function to split the array into minimum count
// of subarrays such that each subarray is either
// non-increasing or non-decreasing
void minimumSubarrays(int arr[], int n)
{

  // Initialize variable to keep
  // track of current sequence
  char current = 'N';

  // Stores the required result
  int answer = 1;

  // Traverse the array, arr[]
  for (int i = 1; i < n; i++) {

    // If current sequence is neither
    // non-increasing nor non-decreasing
    if (current == 'N') {

      // If previous element is greater
      if (arr[i] < arr[i - 1]) {

        // Update current
        current = 'D';
      }

      // If previous element is equal
      // to the current element
      else if (arr[i] == arr[i - 1]) {

        // Update current
        current = 'N';
      }

      // Otherwise
      else {

        // Update current
        current = 'I';
      }
    }

    // If current sequence
    // is in non-decreasing
    else if (current == 'I') {

      // If previous element is
      // less than or equal to
      // the current element
      if (arr[i] >= arr[i - 1]) {
        current = 'I';
      }

      // Otherwise
      else {

        // Update current as N and
        // increment answer by 1
        current = 'N';
        answer += 1;
      }
    }

    // If current sequence
    // is Non-Increasing
    else {

      // If previous element is
      // greater or equal to
      // the current element
      if (arr[i] <= arr[i - 1]) {
        current = 'D';
      }

      // Otherwise
      else {

        // Update current as N and
        // increment answer by 1
        current = 'N';
        answer += 1;
      }
    }
  }

  // Print the answer
  cout<<answer;
}

// Driver Code
int main() {

  // Given array
  int arr[] = { 2, 3, 9, 5, 4, 6, 8 };

  // Given size of array
  int n = sizeof(arr) / sizeof(arr[0]);

  minimumSubarrays(arr, n);
  return 0;
}

// This code is contributed by shikhasingrajput
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to split the array into minimum count
    // of subarrays such that each subarray is either
    // non-increasing or non-decreasing
    static void minimumSubarrays(int[] arr, int n)
    {

        // Initialize variable to keep
        // track of current sequence
        char current = 'N';

        // Stores the required result
        int answer = 1;

        // Traverse the array, arr[]
        for (int i = 1; i < n; i++) {

            // If current sequence is neither
            // non-increasing nor non-decreasing
            if (current == 'N') {

                // If previous element is greater
                if (arr[i] < arr[i - 1]) {

                    // Update current
                    current = 'D';
                }

                // If previous element is equal
                // to the current element
                else if (arr[i] == arr[i - 1]) {

                    // Update current
                    current = 'N';
                }

                // Otherwise
                else {

                    // Update current
                    current = 'I';
                }
            }

            // If current sequence
            // is in non-decreasing
            else if (current == 'I') {

                // If previous element is
                // less than or equal to
                // the current element
                if (arr[i] >= arr[i - 1]) {
                    current = 'I';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }

            // If current sequence
            // is Non-Increasing
            else {

                // If previous element is
                // greater or equal to
                // the current element
                if (arr[i] <= arr[i - 1]) {
                    current = 'D';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }
        }

        // Print the answer
        System.out.print(answer);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array
        int arr[] = { 2, 3, 9, 5, 4, 6, 8 };

        // Given size of array
        int n = arr.length;

        minimumSubarrays(arr, n);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to split the array into minimum count
# of subarrays such that each subarray is either
# non-increasing or non-decreasing
def minimumSubarrays(arr, n):

    # Initialize variable to keep
    # track of current sequence
    current = 'N'

    # Stores the required result
    answer = 1

    # Traverse the array, arr[]
    for i in range(1, n):

        # If current sequence is neither
        # non-increasing nor non-decreasing
        if (current == 'N'):

            # If previous element is greater
            if (arr[i] < arr[i - 1]):

                # Update current
                current = 'D'

            # If previous element is equal
            # to the current element
            elif (arr[i] == arr[i - 1]):

                # Update current
                current = 'N'

            # Otherwise
            else:

                # Update current
                current = 'I'

        # If current sequence
        # is in non-decreasing
        elif (current == 'I'):

            #I f previous element is
            # less than or equal to
            # the current element
            if (arr[i] >= arr[i - 1]):
                current = 'I'

            # Otherwise
            else:

                # Update current as N and
                # increment answer by 1
                current = 'N'
                answer += 1

        # If current sequence
        # is Non-Increasing
        else:

            # If previous element is
            # greater or equal to
            # the current element
            if (arr[i] <= arr[i - 1]):
                current = 'D'

            # Otherwise
            else:

                # Update current as N and
                # increment answer by 1
                current = 'N'
                answer += 1

    # Print the answer
    print(answer)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 3, 9, 5, 4, 6, 8 ]

    # Given size of array
    n = len(arr)

    minimumSubarrays(arr, n)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to split the array into minimum count
    // of subarrays such that each subarray is either
    // non-increasing or non-decreasing
    static void minimumSubarrays(int[] arr, int n)
    {

        // Initialize variable to keep
        // track of current sequence
        char current = 'N';

        // Stores the required result
        int answer = 1;

        // Traverse the array, []arr
        for (int i = 1; i < n; i++) {

            // If current sequence is neither
            // non-increasing nor non-decreasing
            if (current == 'N') {

                // If previous element is greater
                if (arr[i] < arr[i - 1]) {

                    // Update current
                    current = 'D';
                }

                // If previous element is equal
                // to the current element
                else if (arr[i] == arr[i - 1]) {

                    // Update current
                    current = 'N';
                }

                // Otherwise
                else {

                    // Update current
                    current = 'I';
                }
            }

            // If current sequence
            // is in non-decreasing
            else if (current == 'I') {

                // If previous element is
                // less than or equal to
                // the current element
                if (arr[i] >= arr[i - 1]) {
                    current = 'I';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }

            // If current sequence
            // is Non-Increasing
            else {

                // If previous element is
                // greater or equal to
                // the current element
                if (arr[i] <= arr[i - 1]) {
                    current = 'D';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }
        }

        // Print the answer
        Console.Write(answer);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given array
        int []arr = { 2, 3, 9, 5, 4, 6, 8 };

        // Given size of array
        int n = arr.Length;

        minimumSubarrays(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
// Java script program for the above approach

    // Function to split the array into minimum count
    // of subarrays such that each subarray is either
    // non-increasing or non-decreasing
    function minimumSubarrays(arr,n)
    {

        // Initialize variable to keep
        // track of current sequence
        let current = 'N';

        // Stores the required result
        let answer = 1;

        // Traverse the array, arr[]
        for (let i = 1; i < n; i++) {

            // If current sequence is neither
            // non-increasing nor non-decreasing
            if (current == 'N') {

                // If previous element is greater
                if (arr[i] < arr[i - 1]) {

                    // Update current
                    current = 'D';
                }

                // If previous element is equal
                // to the current element
                else if (arr[i] == arr[i - 1]) {

                    // Update current
                    current = 'N';
                }

                // Otherwise
                else {

                    // Update current
                    current = 'I';
                }
            }

            // If current sequence
            // is in non-decreasing
            else if (current == 'I') {

                // If previous element is
                // less than or equal to
                // the current element
                if (arr[i] >= arr[i - 1]) {
                    current = 'I';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }

            // If current sequence
            // is Non-Increasing
            else {

                // If previous element is
                // greater or equal to
                // the current element
                if (arr[i] <= arr[i - 1]) {
                    current = 'D';
                }

                // Otherwise
                else {

                    // Update current as N and
                    // increment answer by 1
                    current = 'N';
                    answer += 1;
                }
            }
        }

        // Print the answer
        document.write(answer);
    }

    // Driver Code

        // Given array
        let arr = [ 2, 3, 9, 5, 4, 6, 8 ];

        // Given size of array
        let n = arr.length;

        minimumSubarrays(arr, n);

// contributed by sravan kumar
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**