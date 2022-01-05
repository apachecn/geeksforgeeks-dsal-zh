# 通过给每个递增/递减的连续对分配该顺序的值来最小化可能的总和

> 原文:[https://www . geeksforgeeks . org/通过按顺序分配每个递增递减连续值对来最小化可能总和/](https://www.geeksforgeeks.org/minimum-sum-possible-by-assigning-every-increasing-decreasing-consecutive-pair-with-values-in-that-order/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到可以分配给每个数组元素 **arr[i]** 的正整数的最小和，这样如果 **arr[i] > arr[i+1]** 或**arr[I–1]**，那么分配给 **arr[i]** 的正整数必须超过分配给 **arr 的整数**

**示例:**

> **输入:** arr[] = {1，0，2}
> **输出:** 5
> **解释:**分配正整数的一种可能方式是 ans[] = {2，1，2}，从而满足以下条件:
> 
> *   arr[0] > arr[1]和 ans[0] > ans[1]
> *   arr[1] < arr[2]和 ans[1] < ans[2]
> 
> 因此，最小可能和= 2 + 1 + 2 = 5。
> 
> **输入:** arr[] = {1，2，2}
> **输出:** 4
> **解释:**分配正整数的一种可能方式是 ans[] = {1，2，1}。因此，最小可能和= 1 + 2 + 1 = 4。

**方法:**想法是[从左到右和从右到左遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)以更新每个元素的答案 **arr[i]** 使得 **arr[i]** 的答案大于 **arr[i+1]** 和**arr[I–1]**的答案，如果 **arr[i]** 大于**arr[I+1]**按照以下步骤解决问题:

*   初始化一个大小为 **N** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **和**，该向量存储可以分配给每个元素的最小正整数。
*   用 **1** 初始化向量**和**，因为每个元素必须被分配一个正整数。
*   [使用变量 **i** 从左到右遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，如果 **arr[i]** 大于**arr[I–1]**，则将 **ans[i]** 更新为**ans[I]= ans[I–1]+1**。
*   现在，使用变量 **i** 从右向左遍历数组，如果 **arr[i]** 大于 **arr[i+1]** ，则更新 **ans[i]** 为 **ans[i] = max(ans[i]，ans[i + 1] + 1)** 。
*   现在，找出向量**和**中存在的正整数之和，并将其打印为最小可能和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum sum
// of values assigned to each element
// of the array as per given conditions
void minSum(int* arr, int n)
{
    // Initialize vectors with value 1
    vector<int> ans(n, 1);

    // Traverse from left to right
    for (int i = 1; i < n; i++) {

        // Update if ans[i] > ans[i-1]
        if (arr[i] > arr[i - 1]) {
            ans[i] = max(ans[i],
                         ans[i - 1] + 1);
        }
    }

    // Traverse from right to left
    for (int i = n - 2; i >= 0; i--) {

        // Update as ans[i] > ans[i+1]
        // if arr[i]> arr[i+1]
        if (arr[i] > arr[i + 1]) {
            ans[i] = max(ans[i],
                         ans[i + 1] + 1);
        }
    }

    // Find the minimum sum
    int s = 0;
    for (auto x : ans) {
        s = s + x;
    }

    // Print the sum
    cout << s << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    minSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to print the
// minimum sum of values
// assigned to each element
// of the array as per given
// conditions
static void minSum(int[] arr,
                   int n)
{
  // Initialize vectors
  // with value 1
  int[] ans = new int[n];
  Arrays.fill(ans, 1);

  // Traverse from left
  // to right
  for (int i = 1; i < n; i++)
  {
    // Update if ans[i] > ans[i-1]
    if (arr[i] > arr[i - 1])
    {
      ans[i] = Math.max(ans[i],
                        ans[i - 1] + 1);
    }
  }

  // Traverse from right to left
  for (int i = n - 2; i >= 0; i--)
  {
    // Update as ans[i] > ans[i+1]
    // if arr[i]> arr[i+1]
    if (arr[i] > arr[i + 1])
    {
      ans[i] = Math.max(ans[i],
                        ans[i + 1] + 1);
    }
  }

  // Find the minimum sum
  int s = 0;
  for (int x : ans)
  {
    s = s + x;
  }

  // Print the sum
  System.out.print(s + "\n");
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {1, 2, 2};

  int N = arr.length;

  // Function Call
  minSum(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to print the minimum
# sum of values assigned to each
# element of the array as per
# given conditions
def minSum(arr, n):

    # Initialize vectors with
    # value 1
    ans = [1] * (n)

    # Traverse from left to
    # right
    for i in range(1, n):

        # Update if ans[i] >
        # ans[i-1]
        if (arr[i] > arr[i - 1]):
            ans[i] = max(ans[i],
                         ans[i - 1] + 1)

    # Traverse from right
    # to left
    for i in range(n - 2,
                   -1, -1):

        # Update as ans[i] >
        # ans[i+1] if arr[i] >
        # arr[i+1]
        if (arr[i] > arr[i + 1]):
            ans[i] = max(ans[i],
                         ans[i + 1] + 1)

    # Find the minimum sum
    s = 0
    for x in ans:
        s = s + x

    # Print the sum
    print(s)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 2, 2]

    N = len(arr)

    # Function Call
    minSum(arr, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to print the
// minimum sum of values
// assigned to each element
// of the array as per given
// conditions
static void minSum(int[] arr,
                   int n)
{
  // Initialize vectors
  // with value 1
  int[] ans = new int[n];

  for(int i = 0; i < n; i++)
    ans[i] = 1;

  // Traverse from left
  // to right
  for (int i = 1; i < n; i++)
  {
    // Update if ans[i] > ans[i-1]
    if (arr[i] > arr[i - 1])
    {
      ans[i] = Math.Max(ans[i],
                        ans[i - 1] + 1);
    }
  }

  // Traverse from right to left
  for (int i = n - 2; i >= 0; i--)
  {
    // Update as ans[i] > ans[i+1]
    // if arr[i]> arr[i+1]
    if (arr[i] > arr[i + 1])
    {
      ans[i] = Math.Max(ans[i],
                        ans[i + 1] + 1);
    }
  }

  // Find the minimum sum
  int s = 0;
  foreach (int x in ans)
  {
    s = s + x;
  }

  // Print the sum
  Console.Write(s + "\n");
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 2, 2};

  int N = arr.Length;

  // Function Call
  minSum(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to print the
// minimum sum of values
// assigned to each element
// of the array as per given
// conditions
function minSum(arr, n)
{
  // Initialize vectors
  // with value 1
  let ans = new Array(n).fill(1);

  // Traverse from left
  // to right
  for (let i = 1; i < n; i++)
  {
    // Update if ans[i] > ans[i-1]
    if (arr[i] > arr[i - 1])
    {
      ans[i] = Math.max(ans[i],
                        ans[i - 1] + 1);
    }
  }

  // Traverse from right to left
  for (let i = n - 2; i >= 0; i--)
  {
    // Update as ans[i] > ans[i+1]
    // if arr[i]> arr[i+1]
    if (arr[i] > arr[i + 1])
    {
      ans[i] = Math.max(ans[i],
                        ans[i + 1] + 1);
    }
  }

  // Find the minimum sum
  let s = 0;
  for (let x in ans)
  {
    s = s + ans[x];
  }

  // Print the sum
  document.write(s + "\n");
}

// Driver Code

    // Given array arr[]
  let arr = [1, 2, 2];

  let N = arr.length;

  // Function Call
  minSum(arr, N);

</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)