# 在反向排序数组中搜索元素

> 原文:[https://www . geeksforgeeks . org/search-反向排序数组中的元素/](https://www.geeksforgeeks.org/search-an-element-in-a-reverse-sorted-array/)

给定一个按降序排列的[数组 **arr[]** ，以及一个整数 **X** ，任务是](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)[检查给定数组中是否存在**X**](https://www.geeksforgeeks.org/check-if-a-value-is-present-in-an-array-in-java/)。如果阵列中存在 **X** ，则打印其索引(*基于 0 的索引*)。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = {5，4，3，2，1}，X = 4
> **输出:** 1
> **说明:**元素 X (= 4)出现在索引 1 处。
> 因此，要求的输出为 1。
> 
> **输入:** arr[] = {10，8，2，-9}，X = 5
> **输出:** -1
> **说明:**数组中不存在元素 X (= 5)。
> 因此，要求的输出为-1。

**天真法:**解决问题最简单的方法就是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，检查是否等于 **X** 。如果发现任何元素满足该条件，则打印该元素的索引。否则打印 **-1** 。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效方法:**要解决这个问题，思路是基于文章[中讨论的方法使用](https://www.geeksforgeeks.org/binary-search/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在排序数组中搜索元素。按照以下步骤解决问题:

1.  将 **X** 与中间元素进行比较。
2.  如果 **X** 与中间元素( **arr【中】**匹配，返回索引**中**。
3.  如果发现 **X** 大于 **arr【中】**，那么 **X** 只能位于子阵**【中+ 1，结束】**中。所以在子阵列**中搜索**X**{ arr[mid+1]，..，arr[end]}** 。
4.  否则，搜索子阵列 **{arr[start]，…。，arr[mid]}**

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to search if element X
// is present in reverse sorted array
int binarySearch(int arr[], int N, int X)
{
    // Store the first index of the
    // subarray in which X lies
    int start = 0;

    // Store the last index of the
    // subarray in which X lies
    int end = N;

    while (start <= end) {

        // Store the middle index
        // of the subarray
        int mid = start
                  + (end - start) / 2;

        // Check if value at middle index
        // of the subarray equal to X
        if (X == arr[mid]) {

            // Element is found
            return mid;
        }

        // If X is smaller than the value
        // at middle index of the subarray
        else if (X < arr[mid]) {

            // Search in right
            // half of subarray
            start = mid + 1;
        }
        else {

            // Search in left
            // half of subarray
            end = mid - 1;
        }
    }

    // If X not found
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int X = 4;

    int res =  binarySearch(arr, N, X);
    printf(" %d " , res);
    return 0;
}
//This code is contributed by Pradeep Mondal P
```

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to search if element X
// is present in reverse sorted array
int binarySearch(int arr[], int N, int X)
{
    // Store the first index of the
    // subarray in which X lies
    int start = 0;

    // Store the last index of the
    // subarray in which X lies
    int end = N;

    while (start <= end) {

        // Store the middle index
        // of the subarray
        int mid = start
                  + (end - start) / 2;

        // Check if value at middle index
        // of the subarray equal to X
        if (X == arr[mid]) {

            // Element is found
            return mid;
        }

        // If X is smaller than the value
        // at middle index of the subarray
        else if (X < arr[mid]) {

            // Search in right
            // half of subarray
            start = mid + 1;
        }
        else {

            // Search in left
            // half of subarray
            end = mid - 1;
        }
    }

    // If X not found
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 3, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int X = 5;
    cout << binarySearch(arr, N, X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Function to search if element X
    // is present in reverse sorted array
    static int binarySearch(int arr[],
                            int N, int X)
    {
        // Store the first index of the
        // subarray in which X lies
        int start = 0;

        // Store the last index of the
        // subarray in which X lies
        int end = N;
        while (start <= end) {

            // Store the middle index
            // of the subarray
            int mid = start
                      + (end - start) / 2;

            // Check if value at middle index
            // of the subarray equal to X
            if (X == arr[mid]) {

                // Element is found
                return mid;
            }

            // If X is smaller than the value
            // at middle index of the subarray
            else if (X < arr[mid]) {

                // Search in right
                // half of subarray
                start = mid + 1;
            }
            else {

                // Search in left
                // half of subarray
                end = mid - 1;
            }
        }

        // If X not found
        return -1;
    }
    public static void main(String[] args)
    {
        int arr[] = { 5, 4, 3, 2, 1 };
        int N = arr.length;
        int X = 5;
        System.out.println(
            binarySearch(arr, N, X));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to search if element X
# is present in reverse sorted array
def binarySearch(arr, N, X):

    # Store the first index of the
    # subarray in which X lies
    start = 0

    # Store the last index of the
    # subarray in which X lies
    end = N

    while (start <= end):

        # Store the middle index
        # of the subarray
        mid = start + (end - start) // 2

        # Check if value at middle index
        # of the subarray equal to X
        if (X == arr[mid]):

            # Element is found
            return mid

        # If X is smaller than the value
        # at middle index of the subarray
        elif (X < arr[mid]):

            # Search in right
            # half of subarray
            start = mid + 1
        else:

            # Search in left
            # half of subarray
            end = mid - 1

    # If X not found
    return -1

# Driver Code
if __name__ == '__main__':

    arr = [ 5, 4, 3, 2, 1 ]
    N = len(arr)
    X = 5

    print(binarySearch(arr, N, X))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to search if element X
// is present in reverse sorted array
static int binarySearch(int []arr,
                        int N, int X)
{
  // Store the first index of the
  // subarray in which X lies
  int start = 0;

  // Store the last index of the
  // subarray in which X lies
  int end = N;
  while (start <= end)
  {
    // Store the middle index
    // of the subarray
    int mid = start +
              (end - start) / 2;

    // Check if value at middle index
    // of the subarray equal to X
    if (X == arr[mid])
    {
      // Element is found
      return mid;
    }

    // If X is smaller than the value
    // at middle index of the subarray
    else if (X < arr[mid])
    {
      // Search in right
      // half of subarray
      start = mid + 1;
    }
    else
    {
      // Search in left
      // half of subarray
      end = mid - 1;
    }
  }

  // If X not found
  return -1;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {5, 4, 3, 2, 1};
  int N = arr.Length;
  int X = 5;
  Console.WriteLine(binarySearch(arr, N, X));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to search if element X
// is present in reverse sorted array
function binarySearch(arr, N, X)
{
    // Store the first index of the
    // subarray in which X lies
    let start = 0;

    // Store the last index of the
    // subarray in which X lies
    let end = N;

    while (start <= end) {

        // Store the middle index
        // of the subarray
        let mid = Math.floor(start
                + (end - start) / 2);

        // Check if value at middle index
        // of the subarray equal to X
        if (X == arr[mid]) {

            // Element is found
            return mid;
        }

        // If X is smaller than the value
        // at middle index of the subarray
        else if (X < arr[mid]) {

            // Search in right
            // half of subarray
            start = mid + 1;
        }
        else {

            // Search in left
            // half of subarray
            end = mid - 1;
        }
    }

    // If X not found
    return -1;
}

// Driver Code
    let arr = [ 5, 4, 3, 2, 1 ];
    let N = arr.length;
    let X = 5;
    document.write(binarySearch(arr, N, X));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(log<sub>2</sub>N)*
*T8】辅助空间: O(1)*