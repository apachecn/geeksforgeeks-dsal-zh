# 从给定索引开始计算子阵列中最大数组元素出现次数的查询

> 原文:[https://www . geeksforgeeks . org/查询-计数-子数组中最大数组元素出现次数-从给定索引开始/](https://www.geeksforgeeks.org/queries-to-count-occurrences-of-maximum-array-element-in-subarrays-starting-from-given-indices/)

给定两个由 **N** 整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和 **q[]** ，每个查询 **q[i]** 的任务是确定[最大数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)出现在[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)**【q[I]，arr[N–1]】**中的次数。

**示例:**

> **输入:** arr[] = {5，4，5，3，2}，q[] = {1，2，3，4，5}
> **输出:** 2 1 1 1 1
> **解释:**
> 对于第一个查询索引从 1 开始。子阵列是[5，4，5，3，2]，最大值是 5，它在子阵列中的出现次数是 2。
> 对于第二个查询索引从 2 开始。子阵列是[4，5，3，2]，最大值是 5，它在子阵列中的出现次数是 1。
> 对于第三个查询索引从 3 开始。子阵列是[5，3，2]，最大值是 5，它在子阵列中的出现次数是 1。
> 对于第四个查询索引从 4 开始。子阵列是[3，2]，最大值是 3，它在子阵列中的出现次数是 1。
> 对于第五个查询索引从 5 开始。子阵列为[2]，最大值为 2，它在子阵列中的出现次数为 1。
> 
> **输入:** arr[] = {2，1，2}，q[] = {1，2，3}
> **输出:** 2 1 1

**天真法:**最简单的方法是[遍历阵](https://www.geeksforgeeks.org/iterating-arrays-java/)[找到最大阵元](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)。现在，对于每个查询 q[i]，遍历子阵列**【q[I]，arr[N–1]]**，并打印子阵列中[最大元素](https://www.geeksforgeeks.org/max_element-in-cpp/)的出现次数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。以下是步骤:

*   创建一个数组 **maxFreqVec[]** 来存储从给定索引 **q[i]** 到 **N** 的 max 元素的出现。
*   [从右侧遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，跟踪数组中的[最大元素，并用该最大元素的出现更新该索引处的数组 **maxFreqVec[]** 。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
*   完成上述步骤后，遍历数组 **q[]** 并打印值**maxFreqVec[q[I]–1]**作为每个查询的每个子数组中的最大元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find occurrence of
// max element in given subarray
void FreqOfMaxElement(vector<int> arr,
                      vector<int> q)
{

    // Store the frequency of maximum
    // element
    vector<int> maxFreqVec(arr.size());

    int maxSoFar = INT_MIN;
    int maxFreq = 0;

    // Traverse over the array arr[]
    // from right to left
    for(int i = arr.size() - 1; i >= 0; i--)
    {

        // If curr element is greater
        // than maxSofar
        if (arr[i] > maxSoFar)
        {

            // Reset maxSofar and maxFreq
            maxSoFar = arr[i];
            maxFreq = 1;
        }

        // If curr is equal to maxSofar
        else if (arr[i] == maxSoFar)
        {

            // Increment the maxFreq
            maxFreq++;
        }

        // Update maxFreqVec[i]
        maxFreqVec[i] = maxFreq;
    }

    // Print occurrence of maximum
    // element for each query
    for(int k : q)
    {
        cout << maxFreqVec[k - 1] << " ";
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 5, 4, 5, 3, 2 };
    vector<int> q = { 1, 2, 3, 4, 5 };

    // Function Call
    FreqOfMaxElement(arr, q);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to find occurrence of
    // max element in given subarray
    static void FreqOfMaxElement(
        int[] arr, int[] q)
    {

        // Store the frequency of maximum
        // element
        int[] maxFreqVec
            = new int[arr.length];

        int maxSoFar = Integer.MIN_VALUE;
        int maxFreq = 0;

        // Traverse over the array arr[]
        // from right to left
        for (int i = arr.length - 1;
             i >= 0; i--) {

            // If curr element is greater
            // than maxSofar
            if (arr[i] > maxSoFar) {

                // Reset maxSofar and maxFreq
                maxSoFar = arr[i];
                maxFreq = 1;
            }

            // If curr is equal to maxSofar
            else if (arr[i] == maxSoFar) {

                // Increment the maxFreq
                maxFreq++;
            }

            // Update maxFreqVec[i]
            maxFreqVec[i] = maxFreq;
        }

        // Print occurrence of maximum
        // element for each query
        for (int k : q) {
            System.out.print(
                maxFreqVec[k - 1] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 5, 4, 5, 3, 2 };
        int[] q = { 1, 2, 3, 4, 5 };

        // Function Call
        FreqOfMaxElement(arr, q);
    }
}
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
import sys;

# Function to find occurrence
# of max element in given
# subarray
def FreqOfMaxElement(arr, q):

    # Store the frequency of
    # maximum element
    maxFreqVec = [0] * (len(arr));

    maxSoFar = -sys.maxsize;
    maxFreq = 0;

    # Traverse over the array
    # arr from right to left
    for i in range(len(arr)-1,
                   -1, -1):

        # If curr element is
        # greater than maxSofar
        if (arr[i] > maxSoFar):

            # Reset maxSofar
            # and maxFreq
            maxSoFar = arr[i];
            maxFreq = 1;

        # If curr is equal to
        # maxSofar
        elif (arr[i] == maxSoFar):

            # Increment the
            # maxFreq
            maxFreq += 1;

        # Update maxFreqVec[i]
        maxFreqVec[i] = maxFreq;

    # Proccurrence of maximum
    # element for each query
    for i in range(0, len(q)):
        print(maxFreqVec[q[i] - 1],
              end = " ");

# Driver Code
if __name__ == '__main__':

    arr = [5, 4, 5, 3, 2];
    q = [1, 2, 3, 4, 5];

    # Function Call
    FreqOfMaxElement(arr, q);

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find occurrence of
// max element in given subarray
static void FreqOfMaxElement(int[] arr,
                             int[] q)
{
  // Store the frequency of
  // maximum element
  int[] maxFreqVec = new int[arr.Length];

  int maxSoFar = Int32.MinValue;
  int maxFreq = 0;

  // Traverse over the array arr[]
  // from right to left
  for (int i = arr.Length - 1;
           i >= 0; i--)
  {
    // If curr element is greater
    // than maxSofar
    if (arr[i] > maxSoFar)
    {
      // Reset maxSofar and maxFreq
      maxSoFar = arr[i];
      maxFreq = 1;
    }

    // If curr is equal to maxSofar
    else if (arr[i] == maxSoFar)
    {
      // Increment the maxFreq
      maxFreq++;
    }

    // Update maxFreqVec[i]
    maxFreqVec[i] = maxFreq;
  }

  // Print occurrence of maximum
  // element for each query
  foreach (int k in q)
  {
    Console.Write(maxFreqVec[k - 1] +
                  " ");
  }
}

// Driver code
static void Main()
{
  int[] arr = {5, 4, 5, 3, 2};
  int[] q = {1, 2, 3, 4, 5};

  // Function Call
  FreqOfMaxElement(arr, q);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find occurrence of
// max element in given subarray
function FreqOfMaxElement(arr, q)
{

    // Store the frequency of maximum
    // element
    var maxFreqVec = new Array(arr.length);
    var maxSoFar = -1000000000;
    var maxFreq = 0;

    // Traverse over the array arr[]
    // from right to left
    for(var i = arr.length - 1; i >= 0; i--)
    {

        // If curr element is greater
        // than maxSofar
        if (arr[i] > maxSoFar)
        {

            // Reset maxSofar and maxFreq
            maxSoFar = arr[i];
            maxFreq = 1;
        }

        // If curr is equal to maxSofar
        else if (arr[i] == maxSoFar)
        {

            // Increment the maxFreq
            maxFreq++;
        }

        // Update maxFreqVec[i]
        maxFreqVec[i] = maxFreq;
    }

    // Print occurrence of maximum
    // element for each query
    q.forEach(k => {
        document.write( maxFreqVec[k - 1] + " ");
    });
}

// Driver Code
var arr = [ 5, 4, 5, 3, 2 ];
var q = [ 1, 2, 3, 4, 5 ];

// Function Call
FreqOfMaxElement(arr, q);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
2 1 1 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)