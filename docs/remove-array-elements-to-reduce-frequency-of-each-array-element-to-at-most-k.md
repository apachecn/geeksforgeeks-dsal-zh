# 去掉阵元，将每个阵元的频率降低到最多 K

> 原文:[https://www . geesforgeks . org/remove-array-elements-to-reduce-frequency-of-每个数组元素到最多 k 个/](https://www.geeksforgeeks.org/remove-array-elements-to-reduce-frequency-of-each-array-element-to-at-most-k/)

给定一个大小为 **N** 的[排序数组](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)**arr【】**和一个整数 **K** ，任务是通过移除最小数量的数组元素来打印数组，以使每个元素的频率最多为 **K** 。

**示例:**

> **输入:** arr[] = { 1，1，1，1，2，2，3，4，4，4，4，5 }，K = 3
> **输出:** { 1，1，1，2，2，2，3，4，4，4，5 }
> **解释:**
> 移除 arr[0]，arr[8]将 arr[]修改为{ 1，1，1，2，2，2，3，4，4，5 }。
> 每个不同数组元素的频率最多为 K(=3)。
> 因此，需要的输出是{ 1，1，1，2，2，2，3，4，4，4，5 }。
> 
> **输入:** arr[] = { 1，2，2，3，4，4，5，5 }，K = 2
> **输出:** { 1，2，2，3，4，4，5，5 }

**天真法:**解决这个问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查数组元素的频率是否大于 **K** 。如果发现为真，则从数组中移除当前元素。否则，增加数组元素的频率并打印数组元素。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤解决问题:

*   初始化一个变量，比如说 **j = 0** 通过移除数组元素来存储任意数组元素的索引，这样每个不同元素的频率最多为 **K** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查 **j < K** 或**arr【I】>arr【j–K】**是否为真。如果发现为真，则更新 **arr[j++] = arr[i]** 。
*   最后，通过删除所有索引大于或等于 **j** 的数组元素来打印数组。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to remove array elements
// such that frequency of each distinct
// array element is at most K
vector<int> RemoveElemArr(vector<int>& arr,
                        int n, int k)
{
    // Base Case
    if (n == 0 || n == 1)
        return arr;

    // Stores index of array element by removing
    // the array element such that the frequency
    // of array elements is at most K
    int j = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If j < k or arr[i] > arr[j - k]
        if (j < k || arr[i] > arr[j - k]) {

            // Update arr[j]
            arr[j++] = arr[i];
        }
    }

    // Remove array elements
    while (arr.size() > j) {
        arr.pop_back();
    }

    return arr;
}

// Function to print the array
void printArray(vector<int>& arr)
{

    // Traverse the array
    for (int i = 0; i < arr.size();
        i++) {
        cout << arr[i] << " ";
    }
}

// Utility Function to remove array elements
// such that frequency of each distinct
// array element is at most K
void UtilRemov(vector<int>& arr, int n, int k)
{
    arr = RemoveElemArr(arr, n, k);

    // Print updated array
    printArray(arr);
}

// Driver Code
int main()
{

    vector<int> arr
        = { 1, 2, 2, 3, 4, 4, 4, 5, 5 };

    int k = 2;
    int n = arr.size();

    UtilRemov(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to remove array elements
// such that frequency of each distinct
// array element is at most K
static int [] RemoveElemArr(int []arr,
                        int n, int k)
{

    // Base Case
    if (n == 0 || n == 1)
        return arr;

    // Stores index of array element by removing
    // the array element such that the frequency
    // of array elements is at most K
    int j = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

        // If j < k or arr[i] > arr[j - k]
        if (j < k || arr[i] > arr[j - k])
        {

            // Update arr[j]
            arr[j++] = arr[i];
        }
    }

    // Remove array elements
    while (arr.length > j)
    {
        arr = Arrays.copyOfRange(arr, 0, arr.length-1);
    }

    return arr;
}

// Function to print the array
static void printArray(int [] arr)
{

    // Traverse the array
    for (int i = 0; i < arr.length;
        i++)
    {
        System.out.print(arr[i]+ " ");
    }
}

// Utility Function to remove array elements
// such that frequency of each distinct
// array element is at most K
static void UtilRemov(int []arr, int n, int k)
{
    arr = RemoveElemArr(arr, n, k);

    // Print updated array
    printArray(arr);
}

// Driver Code
public static void main(String[] args)
{

    int []arr
        = { 1, 2, 2, 3, 4, 4, 4, 5, 5 };
    int k = 2;
    int n = arr.length;
    UtilRemov(arr, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to remove array elements
# such that frequency of each distinct
# array element is at most K
def RemoveElemArr(arr, n, k):

    # Base Case
    if (n == 0 or n == 1):
        return arr

    # Stores index of array element by
    # removing the array element such
    # that the frequency of array
    # elements is at most K
    j = 0

    # Traverse the array
    for i in range(n):

        # If j < k or arr[i] > arr[j - k]
        if (j < k or arr[i] > arr[j - k]):

            # Update arr[j]
            arr[j], j = arr[i], j + 1

    # Remove array elements
    while (len(arr) > j):
        del arr[-1]

    return arr

# Function to print the array
def printArray(arr):

    # Traverse the array
    for i in arr:
        print(i, end = " ")

# Utility Function to remove array elements
# such that frequency of each distinct
# array element is at most K
def UtilRemov(arr, n, k):

    arr = RemoveElemArr(arr, n, k)

    # Print updated array
    printArray(arr)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 2, 3, 4, 4, 4, 5, 5 ]

    k = 2
    n = len(arr)

    UtilRemov(arr, n, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;
using System.Linq;

class GFG
{

  // Function to remove array elements
  // such that frequency of each distinct
  // array element is at most K
  static int [] RemoveElemArr(int []arr,
                              int n, int k)
  {

    // Base Case
    if (n == 0 || n == 1)
      return arr;

    // Stores index of array element by removing
    // the array element such that the frequency
    // of array elements is at most K
    int j = 0;

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If j < k or arr[i] > arr[j - k]
      if (j < k || arr[i] > arr[j - k])
      {

        // Update arr[j]
        arr[j++] = arr[i];
      }
    }

    // Remove array elements
    while (arr.Length > j)
    {
      arr = arr.Take(arr.Length - 1).ToArray();
    }

    return arr;
  }

  // Function to print the array
  static void printArray(int [] arr)
  {

    // Traverse the array
    for (int i = 0; i < arr.Length;
         i++)
    {
      Console.Write(arr[i] + " ");
    }
  }

  // Utility Function to remove array elements
  // such that frequency of each distinct
  // array element is at most K
  static void UtilRemov(int []arr, int n, int k)
  {
    arr = RemoveElemArr(arr, n, k);

    // Print updated array
    printArray(arr);
  }

  // Driver code
  public static void Main()
  {
    int []arr
      = { 1, 2, 2, 3, 4, 4, 4, 5, 5 };
    int k = 2;
    int n = arr.Length;
    UtilRemov(arr, n, k);
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to remove array elements
// such that frequency of each distinct
// array element is at most K
function RemoveElemArr(arr, n, k)
{
    // Base Case
    if (n == 0 || n == 1)
        return arr;

    // Stores index of array element by removing
    // the array element such that the frequency
    // of array elements is at most K
    var j = 0;

    // Traverse the array
    for (var i = 0; i < n; i++) {

        // If j < k or arr[i] > arr[j - k]
        if (j < k || arr[i] > arr[j - k]) {

            // Update arr[j]
            arr[j++] = arr[i];
        }
    }

    // Remove array elements
    while (arr.length > j) {
        arr.pop();
    }

    return arr;
}

// Function to print the array
function printArray(arr)
{

    // Traverse the array
    for (var i = 0; i < arr.length;
        i++) {
        document.write(arr[i] + " ");
    }
}

// Utility Function to remove array elements
// such that frequency of each distinct
// array element is at most K
function UtilRemov(arr, n, k)
{
    arr = RemoveElemArr(arr, n, k);

    // Print updated array
    printArray(arr);
}

var arr = [ 1, 2, 2, 3, 4, 4, 4, 5, 5 ];

    var k = 2;
    var n = arr.length;

    UtilRemov(arr, n, k);

    // This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1 2 2 3 4 4 5 5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)