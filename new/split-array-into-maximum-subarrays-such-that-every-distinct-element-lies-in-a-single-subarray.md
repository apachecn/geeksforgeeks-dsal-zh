# 将数组拆分为最大子数组，以便每个不同的元素都位于单个子数组中

> 原文：[https://www.geeksforgeeks.org/split-array-into-maximum-subarrays-such-that-every-distinct-element-lies-in-a-single-subarray/](https://www.geeksforgeeks.org/split-array-into-maximum-subarrays-such-that-every-distinct-element-lies-in-a-single-subarray/)

给定[数组](https://www.geeksforgeeks.org/array-data-structure/)，`arr[]`的大小为`N`，任务是[将数组](https://www.geeksforgeeks.org/split-array-two-equal-sum-subarrays/)拆分为最大数量 [子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，这样[的第一个和最后一个出现的](https://www.geeksforgeeks.org/print-distinct-elements-given-integer-array/)，所有不同的数组元素都位于单个子数组中。

**示例**：

> **输入**：`arr[] = {1, 1, 2, 2}`
>
> **输出**：2
>
> **说明**：
>
> 拆分数组为子数组`{1, 1}`和`{2, 2}`。
>
> 因此，所需的输出为 2。
> 
> **输入**：`arr[] = {1, 2, 4, 1, 4, 7, 7, 8}`
>
> **输出**：3
>
> **说明**：
>
> 将数组拆分为子数组`{1, 2, 4, 1, 4}`, `{7, 7}`和`{8}`。
>
> 因此，所需的输出为 3。

**方法**：想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)存储每个数组元素最后一次出现的索引。 请按照以下步骤解决问题：

1.  初始化一个数组，例如`hash[]`来[存储每个数组元素的最后一次出现的索引](https://www.geeksforgeeks.org/print-the-last-occurrence-of-elements-in-array-in-relative-order/)。

2.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查当前子数组的所有先前元素的最后一次出现的最大索引是否小于或等于当前索引，然后将`count`加 1 。

3.  最后，打印`count`的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize the
// count of subarrays
int maxCtSubarrays(int arr[], int N)
{
    // Store the last index of
    // every array element
    int hash[1000001] = { 0 };

    for (int i = 0; i < N; i++) {
        hash[arr[i]] = i;
    }

    // Store the maximum index of the
    // last occurrence of all elements
    int maxIndex = -1;

    // Store the count of subarrays
    int res = 0;

    for (int i = 0; i < N; i++) {
        maxIndex = max(maxIndex,
                       hash[arr[i]]);

        // If maximum of last indices
        // previous elements is equal
        // to the current index
        if (maxIndex == i) {
            res++;
        }
    }

    // Return the count
    // of subarrays
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 1,
                  4, 7, 7, 8 };
    int N = sizeof(arr)
            / sizeof(arr[0]);

    cout << maxCtSubarrays(arr, N);
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;
class GFG {

// Function to maximize the
// count of subarrays
static int maxCtSubarrays(int arr[], 
                          int N)
{
  // Store the last index of
  // every array element
  int hash[] = new int[1000001];

  for (int i = 0; i < N; i++) 
  {
    hash[arr[i]] = i;
  }

  // Store the maximum index of the
  // last occurrence of all elements
  int maxIndex = -1;

  // Store the count of subarrays
  int res = 0;

  for (int i = 0; i < N; i++) 
  {
    maxIndex = Math.max(maxIndex, 
                        hash[arr[i]]);

    // If maximum of last indices
    // previous elements is equal
    // to the current index
    if (maxIndex == i) 
    {
      res++;
    }
  }

  // Return the count
  // of subarrays
  return res;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {1, 2, 4, 1, 
               4, 7, 7, 8};
  int N = arr.length;
  System.out.print(maxCtSubarrays(arr, N));
}
}

// This code is contributed by Chitranayal

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to maximize the
# count of subarrays
def maxCtSubarrays(arr, N):

    # Store the last index of
    # every array element
    hash = [0] * (1000001)

    for i in range(N):
        hash[arr[i]] = i

    # Store the maximum index of the
    # last occurrence of all elements
    maxIndex = -1

    # Store the count of subarrays
    res = 0

    for i in range(N):
        maxIndex = max(maxIndex,
                       hash[arr[i]])

        # If maximum of last indices
        # previous elements is equal
        # to the current index
        if (maxIndex == i):
            res += 1

    # Return the count
    # of subarrays
    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 4, 1,
            4, 7, 7, 8 ]
    N = len(arr)

    print(maxCtSubarrays(arr, N))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement
// the above approach
using System;
class GFG {

// Function to maximize the
// count of subarrays
static int maxCtSubarrays(int []arr, 
                          int N)
{
  // Store the last index of
  // every array element
  int []hash = new int[1000001];

  for (int i = 0; i < N; i++) 
  {
    hash[arr[i]] = i;
  }

  // Store the maximum index of the
  // last occurrence of all elements
  int maxIndex = -1;

  // Store the count of subarrays
  int res = 0;

  for (int i = 0; i < N; i++) 
  {
    maxIndex = Math.Max(maxIndex, 
                        hash[arr[i]]);

    // If maximum of last indices
    // previous elements is equal
    // to the current index
    if (maxIndex == i) 
    {
      res++;
    }
  }

  // Return the count
  // of subarrays
  return res;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 2, 4, 1, 
               4, 7, 7, 8};
  int N = arr.Length;
  Console.Write(maxCtSubarrays(arr, N));
}
}

// This code is contributed by Princi Singh

```

**输出**：

```
3
```

**时间复杂度**：`O(n)`

**辅助空间**：`O(X)`其中`X`是给定数组中的最大元素。



* * *

* * *



