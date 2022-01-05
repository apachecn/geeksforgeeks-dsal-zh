# 尺寸大于 K 且总和大于给定值的最小子阵列

> 原文:[https://www . geeksforgeeks . org/尺寸最小的大于 k 的子阵列，其和大于给定值/](https://www.geeksforgeeks.org/smallest-subarray-of-size-greater-than-k-with-sum-greater-than-a-given-value/)

给定一个数组，大小为 **N** 的 **arr[]** ，两个正整数 **K** 和 **S** ，任务是找出大小大于 **K** 的最小[子数组](https://www.geeksforgeeks.org/tag/subarray/)的长度，其和大于 **S** 。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 1，S = 8
> **输出:** 2
> **说明:**
> 和大于 S(=8)的最小子阵为{4，5}
> 因此，所需输出为 2。
> 
> **输入:** arr[] = {1，3，5，1，8，2，4}，K= 2，S= 13
> **输出:** 3

**方法:**使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)可以解决问题。按照以下步骤解决问题:

1.  初始化两个变量，比如 i **= 0** 和 j **= 0** 都指向数组的开始，即索引 0。
2.  初始化一个变量和来存储当前正在处理的子阵列的和。
3.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)、 **arr[]** ，通过递增 j 并添加 **arr[j]**
4.  取窗口长度或当前子阵列的长度，由 **j-i+1** (+1，因为索引从零开始)**给出。**
5.  首先，检查当前子阵列即这里的 winLen 的大小是否大于 **K** 。如果不是这种情况，增加 j 值，**继续循环。**
6.  否则，我们得到当前子阵列的大小大于 **K** ，现在我们必须检查是否满足第二个条件，即当前子阵列的总和大于 s。
7.  如果是这种情况，我们更新 minLength 变量，它存储满足上述条件的子数组的最小长度。
8.  此时，我们检查子阵列的大小是否可以减小(通过增加 **i** ) 使得它仍然大于 K，并且总和也大于 s。我们不断地从总和中移除数组的第 I 个元素，以减小 **While 循环中的子阵列大小**，然后增加 **j** ，使得我们移动到数组中的下一个元素。这
9.  最后，打印得到的满足条件的所需子阵列的最小长度。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// smallest subarray of size > K with
// sum greater than S
int smallestSubarray(int K, int S,
                     int arr[], int N)
{
    // Store the first index of
    // the current subarray
    int start = 0;

    // Store the last index of
    // the the current subarray
    int end = 0;

    // Store the sum of the
    // current subarray
    int currSum = arr[0];

    // Store the length of
    // the smallest subarray
    int res = INT_MAX;

    while (end < N - 1) {

        // If sum of the current subarray <= S
        // or length of current subarray <= K
        if (currSum <= S
            || (end - start + 1) <= K) {
            // Increase the subarray
            // sum and size
            currSum += arr[++end];
        }

        // Otherwise
        else {

            // Update to store the minimum
            // size of subarray obtained
            res = min(res, end - start + 1);

            // Decrement current subarray
            // size by removing first element
            currSum -= arr[start++];
        }
    }

    // Check if it is possible to reduce
    // the length of the current window
    while (start < N) {
        if (currSum > S
            && (end - start + 1) > K)
            res = min(res, (end - start + 1));

        currSum -= arr[start++];
    }
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int K = 1, S = 8;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << smallestSubarray(K, S, arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to find the length of the
// smallest subarray of size > K with
// sum greater than S
public static int smallestSubarray(int k, int s,
                                   int[] array, int N)
{

        int i=0;
        int j=0;
        int minLen = Integer.MAX_VALUE;
        int sum = 0;

        while(j < N)
        {
            sum += array[j];
            int winLen = j-i+1;
            if(winLen <= k)
                j++;
            else{
                if(sum > s)
                {
                    minLen = Math.min(minLen,winLen);
                    while(sum > s)
                    {
                        sum -= array[i];
                        i++;
                    }
                    j++;
                }
            }
        }
        return minLen;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int K = 1, S = 8;
    int N = arr.length;

    System.out.print(smallestSubarray(K, S, arr, N));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the length of the
# smallest subarray of size > K with
# sum greater than S
def smallestSubarray(K, S, arr, N):

  # Store the first index of
  # the current subarray
  start = 0

  # Store the last index of
  # the the current subarray
  end = 0

  # Store the sum of the
  # current subarray
  currSum = arr[0]

  # Store the length of
  # the smallest subarray
  res = sys.maxsize

  while end < N - 1:

      # If sum of the current subarray <= S
      # or length of current subarray <= K
      if ((currSum <= S) or
         ((end - start + 1) <= K)):

          # Increase the subarray
          # sum and size
          end = end + 1;
          currSum += arr[end]

      # Otherwise
      else:

          # Update to store the minimum
          # size of subarray obtained
          res = min(res, end - start + 1)

          # Decrement current subarray
          # size by removing first element
          currSum -= arr[start]
          start = start + 1

  # Check if it is possible to reduce
  # the length of the current window
  while start < N:
      if ((currSum > S) and
         ((end - start + 1) > K)):
          res = min(res, (end - start + 1))

      currSum -= arr[start]
      start = start + 1

  return res;

# Driver Code
if __name__ == "__main__":

  arr = [ 1, 2, 3, 4, 5 ]
  K = 1
  S = 8
  N = len(arr)

  print(smallestSubarray(K, S, arr, N))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the length of the
// smallest subarray of size > K with
// sum greater than S
static int smallestSubarray(int K, int S,
                            int[] arr, int N)
{

    // Store the first index of
    // the current subarray
    int start = 0;

    // Store the last index of
    // the the current subarray
    int end = 0;

    // Store the sum of the
    // current subarray
    int currSum = arr[0];

    // Store the length of
    // the smallest subarray
    int res = int.MaxValue;

    while (end < N - 1)
    {

        // If sum of the current subarray <= S
        // or length of current subarray <= K
        if (currSum <= S ||
           (end - start + 1) <= K)
        {

            // Increase the subarray
            // sum and size
            currSum += arr[++end];
        }

        // Otherwise
        else
        {

            // Update to store the minimum
            // size of subarray obtained
            res = Math.Min(res, end - start + 1);

            // Decrement current subarray
            // size by removing first element
            currSum -= arr[start++];
        }
    }

    // Check if it is possible to reduce
    // the length of the current window
    while (start < N)
    {
        if (currSum > S && (end - start + 1) > K)
            res = Math.Min(res, (end - start + 1));

        currSum -= arr[start++];
    }
    return res;
}

// Driver Code
static public void Main()
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int K = 1, S = 8;
    int N = arr.Length;

    Console.Write(smallestSubarray(K, S, arr, N));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to find the length of the
// smallest subarray of size > K with
// sum greater than S
function smallestSubarray(K, S, arr, N)
{

    // Store the first index of
    // the current subarray
    let start = 0;

    // Store the last index of
    // the the current subarray
    let end = 0;

    // Store the sum of the
    // current subarray
    let currSum = arr[0];

    // Store the length of
    // the smallest subarray
    let res = Number.MAX_SAFE_INTEGER;
    while (end < N - 1)
    {

        // If sum of the current subarray <= S
        // or length of current subarray <= K
        if (currSum <= S
            || (end - start + 1) <= K)
        {

            // Increase the subarray
            // sum and size
            currSum += arr[++end];
        }

        // Otherwise
        else {

            // Update to store the minimum
            // size of subarray obtained
            res = Math.min(res, end - start + 1);

            // Decrement current subarray
            // size by removing first element
            currSum -= arr[start++];
        }
    }

    // Check if it is possible to reduce
    // the length of the current window
    while (start < N)
    {
        if (currSum > S
            && (end - start + 1) > K)
            res = Math.min(res, (end - start + 1));

        currSum -= arr[start++];
    }
    return res;
}

// Driver Code
    let arr = [ 1, 2, 3, 4, 5 ];
    let K = 1, S = 8;
    let N = arr.length;
    document.write(smallestSubarray(K, S, arr, N));

// This code is contributed by Surbhi tyagi.
</script>
```

**Output:** 

```
2
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)