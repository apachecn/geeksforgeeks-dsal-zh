# 检查一个数组是否可以通过交换另一个数组中由不等元素组成的索引对进行排序

> 原文:[https://www . geeksforgeeks . org/check-if-a-array-可以通过交换-对-从-index-由-不等-元素组成-在另一个数组中进行排序/](https://www.geeksforgeeks.org/check-if-an-array-can-be-sorted-by-swapping-pairs-from-indices-consisting-of-unequal-elements-in-another-array/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和大小为 **N** 的二进制数组 **B[]** ，任务是检查如果 **B[i]** 不等于 **B[j]** 的话，数组 **A[]** 是否可以通过交换对 **(A[i]，A[j])** 转换为排序数组。如果数组 **A[]** 可以排序，则打印“**是**”。否则，打印“**否**”。

**示例:**

> **输入:** A[] = {3，1，2}，B[] = {0，1，1}
> **输出:**是
> **说明:**
> 从 B[1]开始交换 A[]的位置 1 和位置 2 的元素！=B[2]。所以，A[] = {1，3，2}，B[] = {1，0，1}
> 现在，从 B[2]开始交换 A[]的位置 2 和位置 3 的元素！=B[3]。所以，A[] = {1，2，3}。因此，它被排序。
> 
> **输入:** A[] = {5，15，4}，B[] = {0，0，0}
> **输出:**否

**方法:**根据以下观察结果可以解决问题:

> 如果数组 B[]的至少两个元素不同，则可以交换数组 A[]的任意两个元素。

按照以下步骤解决问题:

*   检查给定数组 **A[]** 是否已经按照升序[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。如果发现属实，则打印**“是”**。
*   否则，统计 **B[]** 阵中出现的 **1** 和 **0** 的数量。
    *   如果数组 **B[]** 至少包含一个 **0** 和一个 **1** ，则打印**“是”**。
    *   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if array, A[] can be converted
// into sorted array by swapping (A[i], A[j]) if B[i]
// not equal to B[j]
bool checkifSorted(int A[], int B[], int N)
{

  // Stores if array A[] is sorted
  // in descending order or not
  bool flag = false;

  // Traverse the array A[]
  for (int i = 0; i < N - 1; i++) {

    // If A[i] is greater than A[i + 1]
    if (A[i] > A[i + 1]) {

      // Update flag
      flag = true;
      break;
    }
  }

  // If array is sorted
  // in ascending order
  if (!flag) {
    return true;
  }

  // count = 2: Check if 0s and 1s
  // both present in the B[]
  int count = 0;

  // Traverse the array
  for (int i = 0; i < N; i++) {

    // If current element is 0
    if (B[i] == 0) {

      // Update count
      count++;
      break;
    }
  }

  // Traverse the array B[]
  for (int i = 0; i < N; i++) {

    // If current element is 1
    if (B[i] == 1) {
      count++;
      break;
    }
  }

  // If both 0s and 1s are present
  // in the array
  if (count == 2) {
    return true;
  }
  return false;
}

// Driver Code
int main()
{
  // Input array A[]
  int A[] = { 3, 1, 2 };

  // Input array B[]
  int B[] = { 0, 1, 1 };

  int N = sizeof(A) / sizeof(A[0]);
  // Function call
  bool check = checkifSorted(A, B, N);

  // If true,print YES
  if (check) {
    cout << "YES" <<endl;
  }
  // Else print NO
  else {
    cout << "NO" <<endl;
  }

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.io.*;

class GFG {

    // Function to check if array, A[] can be converted
    // into sorted array by swapping (A[i], A[j]) if B[i]
    // not equal to B[j]
    static boolean checkifSorted(int A[], int B[], int N)
    {

        // Stores if array A[] is sorted
        // in descending order or not
        boolean flag = false;

        // Traverse the array A[]
        for (int i = 0; i < N - 1; i++) {

            // If A[i] is greater than A[i + 1]
            if (A[i] > A[i + 1]) {

                // Update flag
                flag = true;
                break;
            }
        }

        // If array is sorted
        // in ascending order
        if (!flag) {
            return true;
        }

        // count = 2: Check if 0s and 1s
        // both present in the B[]
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If current element is 0
            if (B[i] == 0) {

                // Update count
                count++;
                break;
            }
        }

        // Traverse the array B[]
        for (int i = 0; i < N; i++) {

            // If current element is 1
            if (B[i] == 1) {
                count++;
                break;
            }
        }

        // If both 0s and 1s are present
        // in the array
        if (count == 2) {
            return true;
        }
        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input array A[]
        int A[] = { 3, 1, 2 };

        // Input array B[]
        int B[] = { 0, 1, 1 };

        int N = A.length;
        // Function call
        boolean check = checkifSorted(A, B, N);

        // If true,print YES
        if (check) {
            System.out.println("YES");
        }
        // Else print NO
        else {
            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to check if array, A[] can be converted
# into sorted array by swapping (A[i], A[j]) if B[i]
# not equal to B[j]
def checkifSorted(A, B, N):

  # Stores if array A[] is sorted
  # in descending order or not
  flag = False

  # Traverse the array A[]
  for i in range( N - 1):

    # If A[i] is greater than A[i + 1]
    if (A[i] > A[i + 1]):

      # Update flag
      flag = True
      break

  # If array is sorted
  # in ascending order
  if (not flag):
    return True

  # count = 2: Check if 0s and 1s
  # both present in the B[]
  count = 0

  # Traverse the array
  for i in range(N):

    # If current element is 0
    if (B[i] == 0):

      # Update count
      count += 1
      break

  # Traverse the array B[]
  for i in range(N):

    # If current element is 1
    if B[i]:
      count += 1
      break

  # If both 0s and 1s are present
  # in the array
  if (count == 2):
    return True

  return False

# Driver Code
# Input array A[]
A = [ 3, 1, 2 ]

# Input array B[]
B = [ 0, 1, 1 ]
N = len(A)

# Function call
check = checkifSorted(A, B, N)

# If true,print YES
if (check):
  print("YES")

# Else print NO
else:
  print("NO")

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program of the above approach
using System;
public class GFG
{

    // Function to check if array, A[] can be converted
    // into sorted array by swapping (A[i], A[j]) if B[i]
    // not equal to B[j]
    static bool checkifSorted(int []A, int []B, int N)
    {

        // Stores if array A[] is sorted
        // in descending order or not
        bool flag = false;

        // Traverse the array A[]
        for (int i = 0; i < N - 1; i++) {

            // If A[i] is greater than A[i + 1]
            if (A[i] > A[i + 1]) {

                // Update flag
                flag = true;
                break;
            }
        }

        // If array is sorted
        // in ascending order
        if (!flag) {
            return true;
        }

        // count = 2: Check if 0s and 1s
        // both present in the B[]
        int count = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // If current element is 0
            if (B[i] == 0) {

                // Update count
                count++;
                break;
            }
        }

        // Traverse the array B[]
        for (int i = 0; i < N; i++)
        {

            // If current element is 1
            if (B[i] == 1)
            {
                count++;
                break;
            }
        }

        // If both 0s and 1s are present
        // in the array
        if (count == 2)
        {
            return true;
        }
        return false;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        // Input array A[]
        int []A = { 3, 1, 2 };

        // Input array B[]
        int []B = { 0, 1, 1 };
        int N = A.Length;

        // Function call
        bool check = checkifSorted(A, B, N);

        // If true,print YES
        if (check) {
            Console.WriteLine("YES");
        }
        // Else print NO
        else {
            Console.WriteLine("NO");
        }
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to check if array, A can be converted
    // into sorted array by swapping (A[i], A[j]) if B[i]
    // not equal to B[j]
    function checkifSorted(A , B , N) {

        // Stores if array A is sorted
        // in descending order or not
        var flag = false;

        // Traverse the array A
        for (i = 0; i < N - 1; i++) {

            // If A[i] is greater than A[i + 1]
            if (A[i] > A[i + 1]) {

                // Update flag
                flag = true;
                break;
            }
        }

        // If array is sorted
        // in ascending order
        if (!flag) {
            return true;
        }

        // count = 2: Check if 0s and 1s
        // both present in the B
        var count = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {

            // If current element is 0
            if (B[i] == 0) {

                // Update count
                count++;
                break;
            }
        }

        // Traverse the array B
        for (i = 0; i < N; i++) {

            // If current element is 1
            if (B[i] == 1) {
                count++;
                break;
            }
        }

        // If both 0s and 1s are present
        // in the array
        if (count == 2) {
            return true;
        }
        return false;
    }

    // Driver Code

        // Input array A
        var A = [ 3, 1, 2 ];

        // Input array B
        var B = [ 0, 1, 1 ];

        var N = A.length;
        // Function call
        var check = checkifSorted(A, B, N);

        // If true,print YES
        if (check) {
            document.write("YES");
        }
        // Else print NO
        else {
            document.write("NO");
        }

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)