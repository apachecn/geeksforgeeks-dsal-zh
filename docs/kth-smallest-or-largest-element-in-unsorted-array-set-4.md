# 未排序数组中第 k 个最小或最大的元素|集合 4

> 原文:[https://www . geeksforgeeks . org/kth-最小或最大元素未排序数组集-4/](https://www.geeksforgeeks.org/kth-smallest-or-largest-element-in-unsorted-array-set-4/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数字 **K** ，其中 **K** 小于数组的大小，我们需要找到给定数组中的 **Kth 最小元素**。假设数组元素可以重复(不限于不同的)。

**示例:**

> **输入:** arr[] = {7，10，4，3，20，15}，K = 3
> **输出:** 7
> 
> **输入:** arr[] = {7，1，5，4，20，15，8}，K = 5
> **输出:** 8

我们还用其他方法讨论了这篇文章:

*   [未排序数组中第 K 个最小/最大元素|集合 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)
*   [未排序数组中第 K 个最小/最大元素|集合 2(预期线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)
*   [未排序数组中第 K 个最小/最大元素|集合 3(最坏情况线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)

**方法:**思路是使用[计数排序](https://www.geeksforgeeks.org/counting-sort/)的概念。以下是步骤:

1.  找到数组中的最大元素(比如说 **maxE** )并创建一个长度为 **maxE + 1** 的数组(比如说 **freq[]** )，并将其初始化为零。
2.  循环遍历给定数组中的所有元素，并将元素的频率存储在 **freq[]** 中。
3.  迭代数组 **freq[]** 直到我们到达 **Kth** 元素。
4.  打印上一步中到达的 **Kth** 元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the Kth smallest
// element in Unsorted Array
int findKthSmallest(int arr[], int n, int k)
{

    // Initialize the max Element as 0
    int max = 0;

    // Iterate arr[] and find the maximum
    // element in it
    for (int i = 0; i < n; i++)
    {
        if (arr[i] > max)
            max = arr[i];
    }

    // Frequency array to store
    // the frequencies
    int counter[max + 1] = { 0 };

    // Counter variable
    int smallest = 0;

    // Counting the frequencies
    for (int i = 0; i < n; i++)
    {
        counter[arr[i]]++;
    }

    // Iterate through the freq[]
    for (int num = 1; num <= max; num++)
    {
        // Check if num is present
        // in the array
        if (counter[num] > 0) {

            // Increment the counter
            // with the frequency
            // of num
            smallest += counter[num];
        }

        // Checking if we have reached
        // the Kth smallest element
        if (smallest >= k)
        {
            // Return the Kth
            // smallest element
            return num;
        }
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 7, 1, 4, 4, 20, 15, 8 };

    int N = sizeof(arr) / sizeof(arr[0]);

    int K = 5;

    // Function Call
    cout << findKthSmallest(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Function to find the Kth smallest
    // element in Unsorted Array
    static int findKthSmallest(int[] arr, int n, int k)
    {

        // Initialize the max Element as 0
        int max = 0;

        // Iterate arr[] and find the maximum
        // element in it
        for (int i = 0; i < n; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }

        // Frequency array to store
        // the frequencies
        int[] counter = new int[max + 1];

        // Counter variable
        int smallest = 0;

        // Counting the frequencies
        for (int i = 0; i < n; i++)
        {
            counter[arr[i]]++;
        }

        // Iterate through the freq[]
        for (int num = 1; num <= max; num++)
        {
            // Check if num is present
            // in the array
            if (counter[num] > 0)
            {
                // Increment the counter
                // with the frequency
                // of num
                smallest += counter[num];
            }

            // Checking if we have reached
            // the Kth smallest element
            if (smallest >= k)
            {
                // Return the Kth
                // smallest element
                return num;
            }
        }
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 7, 1, 4, 4, 20, 15, 8 };

        int N = arr.length;

        int K = 5;

        // Function call
        System.out.print(findKthSmallest(arr, N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the Kth
# smallest element in Unsorted
# Array
def findKthSmallest(arr, n, k):

    # Initialize the max
    # Element as 0
    max = 0

    # Iterate arr[] and find
    # the maximum element in it
    for i in range(n):
        if (arr[i] > max):
            max = arr[i]

    # Frequency array to
    # store the frequencies
    counter = [0] * (max + 1)

    # Counter variable
    smallest = 0

    # Counting the frequencies
    for i in range(n):
        counter[arr[i]] += 1

    # Iterate through the freq[]
    for num in range(1, max + 1):

        # Check if num is present
        # in the array
        if (counter[num] > 0):

            # Increment the counter
            # with the frequency
            # of num
            smallest += counter[num]

        # Checking if we have reached
        # the Kth smallest element
        if (smallest >= k):

            # Return the Kth
            # smallest element
            return num

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [7, 1, 4, 4,
           20, 15, 8]

    N = len(arr)
    K = 5

    # Function Call
    print(findKthSmallest(arr, N, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the Kth smallest
// element in Unsorted Array
static int findKthSmallest(int[] arr,
                           int n, int k)
{
  // Initialize the max
  // Element as 0
  int max = 0;

  // Iterate []arr and find
  // the maximum element in it
  for (int i = 0; i < n; i++)
  {
    if (arr[i] > max)
      max = arr[i];
  }

  // Frequency array to store
  // the frequencies
  int[] counter = new int[max + 1];

  // Counter variable
  int smallest = 0;

  // Counting the frequencies
  for (int i = 0; i < n; i++)
  {
    counter[arr[i]]++;
  }

  // Iterate through the []freq
  for (int num = 1;
           num <= max; num++)
  {
    // Check if num is present
    // in the array
    if (counter[num] > 0)
    {
      // Increment the counter
      // with the frequency
      // of num
      smallest += counter[num];
    }

    // Checking if we have reached
    // the Kth smallest element
    if (smallest >= k)
    {
      // Return the Kth
      // smallest element
      return num;
    }
  }
  return -1;
}

// Driver code
public static void Main(String[] args)
{
  // Given array
  int[] arr = {7, 1, 4, 4,
               20, 15, 8};
  int N = arr.Length;
  int K = 5;

  // Function call
  Console.Write(findKthSmallest(arr,
                                N, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to find the Kth smallest
    // element in Unsorted Array
    function findKthSmallest(arr, n, k)
    {

        // Initialize the max Element as 0
        let max = 0;

        // Iterate arr[] and find the maximum
        // element in it
        for (let i = 0; i < n; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }

        // Frequency array to store
        // the frequencies
        let counter = Array.from({length: max + 1}, (_, i) => 0);

        // Counter variable
        let smallest = 0;

        // Counting the frequencies
        for (let i = 0; i < n; i++)
        {
            counter[arr[i]]++;
        }

        // Iterate through the freq[]
        for (let num = 1; num <= max; num++)
        {
            // Check if num is present
            // in the array
            if (counter[num] > 0)
            {
                // Increment the counter
                // with the frequency
                // of num
                smallest += counter[num];
            }

            // Checking if we have reached
            // the Kth smallest element
            if (smallest >= k)
            {
                // Return the Kth
                // smallest element
                return num;
            }
        }
        return -1;
    }

// Driver Code

    // Given array
        let arr = [ 7, 1, 4, 4, 20, 15, 8 ];

        let N = arr.length;

        let K = 5;

        // Function call
        document.write(findKthSmallest(arr, N, K));

 // This code is contributed by sanjoy_62.
</script>
```

**Output**

```
8
```

**时间复杂度:** *O(N+MaxElement)* 其中 N 是给定数组中的元素个数，MaxElement 是数组中的最大个数。伪线性时间复杂度。
**辅助空间:** *O(M)* 其中 M 是给定数组中的最大元素。