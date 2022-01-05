# 检查数组是否可以通过交换 GCD 等于数组中最小元素的对来排序

> 原文:[https://www . geeksforgeeks . org/check-if-array-可以通过交换-pairs-having-gcd-等于数组中最小的元素来排序/](https://www.geeksforgeeks.org/check-if-array-can-be-sorted-by-swapping-pairs-having-gcd-equal-to-the-smallest-element-in-the-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过只交换 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) (最大公约数)等于数组最小元素的元素来检查数组是否可以排序。如果可以对数组进行排序，请打印“是”。否则，打印“否”。

**示例:**

> **输入:** arr[] = {4，3，6，6，2，9}
> **输出:**是
> **解释:**
> 数组中最小的元素= 2
> 交换 arr[0]和 arr[2]，因为它们的 gcd 等于 2。因此，arr[] = {6，3，4，6，2，9}
> 交换 arr[0]和 arr[4]，因为它们的 gcd 等于 2。因此，arr[] = {2，3，4，6，6，9}
> **输入:** arr[] = {2，6，2，4，5}
> **输出:**否

**方法:**思路是[从数组](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)中找到最小的元素，检查是否有可能[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序。以下是步骤:

1.  找到数组中最小的元素，并将其存储在一个变量中，比如 **mn** 。
2.  将数组存储在临时数组中，比如 **B[]** 。
3.  [排序原阵](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
4.  现在，[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，如果有一个元素不能被 **mn** 整除，排序后位置改变，则打印“否”。否则，通过与其他元素交换来重新排列可被 **mn** 整除的元素。
5.  如果所有不能被 **mn** 整除的元素的位置保持不变，则打印“是”。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is
// possible to sort array or not
void isPossible(int arr[], int N)
{

    // Store the smallest element
    int mn = INT_MAX;

    // Copy the original array
    int B[N];

    // Iterate over the given array
    for (int i = 0; i < N; i++) {

        // Update smallest element
        mn = min(mn, arr[i]);

        // Copy elements of arr[]
        // to array B[]
        B[i] = arr[i];
    }

    // Sort original array
    sort(arr, arr + N);

    // Iterate over the given array
    for (int i = 0; i < N; i++) {

        // If the i-th element is not
        // in its sorted place
        if (arr[i] != B[i]) {

            // Not possible to swap
            if (B[i] % mn != 0) {
                cout << "No";
                return;
            }
        }
    }

    cout << "Yes";
    return;
}

// Driver Code
int main()
{
    // Given array
    int N = 6;
    int arr[] = { 4, 3, 6, 6, 2, 9 };

    // Function Call
    isPossible(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to check if it is
// possible to sort array or not
static void isPossible(int arr[],
                       int N)
{
  // Store the smallest element
  int mn = Integer.MAX_VALUE;

  // Copy the original array
  int []B = new int[N];

  // Iterate over the given array
  for (int i = 0; i < N; i++)
  {
    // Update smallest element
    mn = Math.min(mn, arr[i]);

    // Copy elements of arr[]
    // to array B[]
    B[i] = arr[i];
  }

  // Sort original array
  Arrays.sort(arr);

  // Iterate over the given array
  for (int i = 0; i < N; i++)
  {
    // If the i-th element is not
    // in its sorted place
    if (arr[i] != B[i])
    {
      // Not possible to swap
      if (B[i] % mn != 0)
      {
        System.out.print("No");
        return;
      }
    }
  }
  System.out.print("Yes");
  return;
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int N = 6;
  int arr[] = {4, 3, 6, 6, 2, 9};

  // Function Call
  isPossible(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
import sys

# Function to check if it is
# possible to sort array or not
def isPossible(arr, N):

    # Store the smallest element
    mn = sys.maxsize;

    # Copy the original array
    B = [0] * N;

    # Iterate over the given array
    for i in range(N):

        # Update smallest element
        mn = min(mn, arr[i]);

        # Copy elements of arr
        # to array B
        B[i] = arr[i];

    # Sort original array
    arr.sort();

    # Iterate over the given array
    for i in range(N):

        # If the i-th element is not
        # in its sorted place
        if (arr[i] != B[i]):

            # Not possible to swap
            if (B[i] % mn != 0):
                print("No");
                return;

    print("Yes");
    return;

# Driver Code
if __name__ == '__main__':

    # Given array
    N = 6;
    arr = [4, 3, 6, 6, 2, 9];

    # Function Call
    isPossible(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to check if it is
// possible to sort array or not
static void isPossible(int []arr,
                       int N)
{
  // Store the smallest element
  int mn = int.MaxValue;

  // Copy the original array
  int []B = new int[N];

  // Iterate over the given array
  for (int i = 0; i < N; i++)
  {
    // Update smallest element
    mn = Math.Min(mn, arr[i]);

    // Copy elements of []arr
    // to array []B
    B[i] = arr[i];
  }

  // Sort original array
  Array.Sort(arr);

  // Iterate over the given array
  for (int i = 0; i < N; i++)
  {
    // If the i-th element is not
    // in its sorted place
    if (arr[i] != B[i])
    {
      // Not possible to swap
      if (B[i] % mn != 0)
      {
        Console.Write("No");
        return;
      }
    }
  }
  Console.Write("Yes");
  return;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int N = 6;
  int []arr = {4, 3, 6, 6, 2, 9};

  // Function Call
  isPossible(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for
// the above approach

// Function to check if it is
// possible to sort array or not
function isPossible(arr,
                       N)
{
  // Store the smallest element
  let mn = Number.MAX_VALUE;

  // Copy the original array
  let B = [];

  // Iterate over the given array
  for (let i = 0; i < N; i++)
  {
    // Update smallest element
    mn = Math.min(mn, arr[i]);

    // Copy elements of arr[]
    // to array B[]
    B[i] = arr[i];
  }

  // Sort original array
  arr.sort();

  // Iterate over the given array
  for (let i = 0; i < N; i++)
  {
    // If the i-th element is not
    // in its sorted place
    if (arr[i] != B[i])
    {
      // Not possible to swap
      if (B[i] % mn != 0)
      {
        document.write("No");
        return;
      }
    }
  }
  document.write("Yes");
  return;
}

// Driver code

  // Given array
  let N = 6;
  let arr = [4, 3, 6, 6, 2, 9];

  // Function Call
  isPossible(arr, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*