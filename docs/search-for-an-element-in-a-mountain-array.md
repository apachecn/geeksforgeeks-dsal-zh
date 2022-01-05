# 在山阵中搜索元素

> 原文:[https://www . geesforgeks . org/search-for-in-a-element-in-mountain-array/](https://www.geeksforgeeks.org/search-for-an-element-in-a-mountain-array/)

给定一个[山阵](https://www.geeksforgeeks.org/longest-mountain-subarray/)**arr【】**和一个整数 **X** ，任务是找到给定阵中 **X** 的最小索引。如果没有找到这样的索引，打印 **-1** 。

**示例:**

> **输入:** arr = {1，2，3，4，5，3，1}，X = 3
> **输出:** 2
> **说明:**
> 数组中 X(= 3)的最小索引为 2。
> 因此，要求的输出为 2。
> 
> **输入:** arr[] = {0，1，2，4，2，1}，X = 3
> **输出:** -1
> **说明:**由于数组中不存在 3，所以需要的输出为-1。

**天真法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查当前索引中的元素是否等于 **X** 。如果发现是真的，那么打印索引。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**高效途径:**解决这个问题的最佳思路是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。按照以下步骤解决此问题:

*   从山阵中找到[峰指数。](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)
*   基于获得的峰值指数，将数组划分为两部分。它首先使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)搜索左侧，然后搜索右侧。已知峰元素左侧为[按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)，右侧为[按降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   在左边的山阵中搜索。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the index of
// the peak element in the array
int findPeak(vector<int> arr)
{

  // Stores left most index in which
  // the peak element can be found
  int left = 0;

  // Stores right most index in which
  // the peak element can be found
  int right = arr.size() - 1;
  while (left < right)
  {

    // Stores mid of left and right
    int mid = left + (right - left) / 2;

    // If element at mid is less than
    // element at (mid + 1)
    if (arr[mid] < arr[mid + 1])
    {

      // Update left
      left = mid + 1;
    }
    else
    {

      // Update right
      right = mid;
    }
  }
  return left;
}

// Function to perform binary search in an
// a subarray if elements of the subarray
// are in an ascending order
int BS(int X, int left, int right,
       vector<int> arr)
{
  while (left <= right)
  {

    // Stores mid of left and right
    int mid = left + (right - left) / 2;

    // If X found at mid
    if (arr[mid] == X)
    {
      return mid;
    }

    // If X is greater than mid
    else if (X > arr[mid])
    {

      // Update left
      left = mid + 1;
    }

    else
    {

      // Update right
      right = mid - 1;
    }
  }
  return -1;
}

// Function to perform binary search in an
// a subarray if elements of the subarray
// are in an ascending order
int reverseBS(int X, int left, int right, vector<int> arr)
{
  while (left <= right)
  {

    // Stores mid of left and right
    int mid = left + (right - left) / 2;

    // If X found at mid
    if (arr[mid] == X)
    {
      return mid;
    }

    else if (X > arr[mid])
    {

      // Update right
      right = mid - 1;
    }
    else
    {

      // Update left
      left = mid + 1;
    }
  }
  return -1;
}

// Function to find the smallest index of X
void findInMA(int X, vector<int> mountainArr)
{

  // Stores index of peak element in array
  int peakIndex = findPeak(mountainArr);

  // Stores index of X in the array
  int res = -1;

  // If X greater than or equal to first element
  // of array and less than the peak element
  if (X >= mountainArr[0] && X <= mountainArr[peakIndex])
  {

    // Update res
    res = BS(X, 0, peakIndex, mountainArr);
  }

  // If element not found on
  // left side of peak element
  if (res == -1)
  {

    // Update res
    res = reverseBS(X, peakIndex + 1,
                    mountainArr.size() - 1,
                    mountainArr);
  }

  // Print res
  cout<<res<<endl;
}

// Driver Code
int main()
{

  // Given X
  int X = 3;

  // Given array
  vector<int> list{1, 2, 3, 4, 5, 3, 1};

  // Function Call
  findInMA(X, list);
}

// This code is contributed by bgangwar59.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the index of
    // the peak element in the array
    public static int findPeak(
        ArrayList<Integer> arr)
    {

        // Stores left most index in which
        // the peak element can be found
        int left = 0;

        // Stores right most index in which
        // the peak element can be found
        int right = arr.size() - 1;

        while (left < right) {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If element at mid is less than
            // element at (mid + 1)
            if (arr.get(mid) < arr.get(mid + 1)) {

                // Update left
                left = mid + 1;
            }
            else {

                // Update right
                right = mid;
            }
        }

        return left;
    }

    // Function to perform binary search in an
    // a subarray if elements of the subarray
    // are in an ascending order
    static int BS(int X, int left, int right,
                  ArrayList<Integer> arr)
    {

        while (left <= right) {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If X found at mid
            if (arr.get(mid) == X) {
                return mid;
            }

            // If X is greater than mid
            else if (X > arr.get(mid)) {

                // Update left
                left = mid + 1;
            }

            else {

                // Update right
                right = mid - 1;
            }
        }
        return -1;
    }

    // Function to perform binary search in an
    // a subarray if elements of the subarray
    // are in an ascending order
    static int reverseBS(int X, int left, int right,
                         ArrayList<Integer> arr)
    {
        while (left <= right) {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If X found at mid
            if (arr.get(mid) == X) {
                return mid;
            }

            else if (X > arr.get(mid)) {

                // Update right
                right = mid - 1;
            }
            else {

                // Update left
                left = mid + 1;
            }
        }
        return -1;
    }

    // Function to find the smallest index of X
    static void findInMA(int X,
                         ArrayList<Integer> mountainArr)
    {

        // Stores index of peak element in array
        int peakIndex = findPeak(mountainArr);

        // Stores index of X in the array
        int res = -1;

        // If X greater than or equal to first element
        // of array and less than the peak element
        if (X >= mountainArr.get(0)
            && X <= mountainArr.get(peakIndex)) {

            // Update res
            res = BS(X, 0, peakIndex, mountainArr);
        }

        // If element not found on
        // left side of peak element
        if (res == -1) {

            // Update res
            res = reverseBS(X, peakIndex + 1,
                            mountainArr.size() - 1,
                            mountainArr);
        }

        // Print res
        System.out.println(res);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given X
        int X = 3;

        // Given array
        ArrayList<Integer> list = new ArrayList<>(
            Arrays.asList(1, 2, 3, 4, 5, 3, 1));

        // Function Call
        findInMA(X, list);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the index of
# the peak element in the array
def findPeak(arr):

    # Stores left most index in which
    # the peak element can be found
    left = 0

    # Stores right most index in which
    # the peak element can be found
    right = len(arr) - 1

    while (left < right):

        # Stores mid of left and right
        mid = left + (right - left) // 2

        # If element at mid is less than
        # element at(mid + 1)
        if (arr[mid] < arr[(mid + 1)]):

            # Update left
            left = mid + 1

        else:

            # Update right
            right = mid

    return left

# Function to perform binary search in an
# a subarray if elements of the subarray
# are in an ascending order
def BS(X, left, right, arr):

    while (left <= right):

        # Stores mid of left and right
        mid = left + (right - left) // 2

        # If X found at mid
        if (arr[mid] == X):
            return mid

        # If X is greater than mid
        elif (X > arr[mid]):

            # Update left
            left = mid + 1

        else:

            # Update right
            right = mid - 1

    return -1

# Function to perform binary search in an
# a subarray if elements of the subarray
# are in an ascending order
def reverseBS(X, left, right, arr):

    while (left <= right):

        # Stores mid of left and right
        mid = left + (right - left) // 2

        # If X found at mid
        if (arr[mid] == X):
            return mid

        elif (X > arr[mid]):

            # Update right
            right = mid - 1

        else:

            # Update left
            left = mid + 1

    return -1

# Function to find the smallest index of X
def findInMA(X, mountainArr):

    # Stores index of peak element in array
    peakIndex = findPeak(mountainArr)

    # Stores index of X in the array
    res = -1

    # If X greater than or equal to first element
    # of array and less than the peak element
    if (X >= mountainArr[0] and
        X <= mountainArr[peakIndex]):

        # Update res
        res = BS(X, 0, peakIndex, mountainArr)

    # If element not found on
    # left side of peak element
    if (res == -1):

        # Update res
        res = reverseBS(X, peakIndex + 1,
                        mountainArr.size() - 1,
                        mountainArr)

    # Print res
    print(res)

# Driver Code
if __name__ == "__main__":

    # Given X
    X = 3

    # Given array
    arr = [ 1, 2, 3, 4, 5, 3, 1 ]

    # Function Call
    findInMA(X, arr)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq;
class GFG
{

    // Function to find the index of
    // the peak element in the array
    public static int findPeak(List<int> arr)
    {

        // Stores left most index in which
        // the peak element can be found
        int left = 0;

        // Stores right most index in which
        // the peak element can be found
        int right = arr.Count - 1;

        while (left < right)
        {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If element at mid is less than
            // element at (mid + 1)
            if (arr[mid] < arr[(mid + 1)])
            {

                // Update left
                left = mid + 1;
            }
            else
            {

                // Update right
                right = mid;
            }
        }

        return left;
    }

    // Function to perform binary search in an
    // a subarray if elements of the subarray
    // are in an ascending order
    static int BS(int X, int left, int right,
                List<int> arr)
    {

        while (left <= right)
        {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If X found at mid
            if (arr[(mid)] == X)
            {
                return mid;
            }

            // If X is greater than mid
            else if (X > arr[mid])
            {

                // Update left
                left = mid + 1;
            }

            else
            {

                // Update right
                right = mid - 1;
            }
        }
        return -1;
    }

    // Function to perform binary search in an
    // a subarray if elements of the subarray
    // are in an ascending order
    static int reverseBS(int X, int left, int right,
                         List<int> arr)
    {
        while (left <= right)
        {

            // Stores mid of left and right
            int mid = left + (right - left) / 2;

            // If X found at mid
            if (arr[mid] == X)
            {
                return mid;
            }

            else if (X > arr[mid])
            {

                // Update right
                right = mid - 1;
            }
            else
            {

                // Update left
                left = mid + 1;
            }
        }
        return -1;
    }

    // Function to find the smallest index of X
    static void findInMA(int X,
                         List<int> mountainArr)
    {

        // Stores index of peak element in array
        int peakIndex = findPeak(mountainArr);

        // Stores index of X in the array
        int res = -1;

        // If X greater than or equal to first element
        // of array and less than the peak element
        if (X >= mountainArr[0]
            && X <= mountainArr[peakIndex])
        {

            // Update res
            res = BS(X, 0, peakIndex, mountainArr);
        }

        // If element not found on
        // left side of peak element
        if (res == -1)
        {

            // Update res
            res = reverseBS(X, peakIndex + 1,
                            mountainArr.Count - 1,
                            mountainArr);
        }

        // Print res
        Console.WriteLine(res);
    }

    // Driver Code
    public static void Main( )
    {

        // Given X
        int X = 3;

        // Given array
        List<int> list =  new List<int>(){1, 2, 3, 4, 5, 3, 1};

        // Function Call
        findInMA(X, list);
    }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the index of
// the peak element in the array
function findPeak(arr)
{

  // Stores left most index in which
  // the peak element can be found
  var left = 0;

  // Stores right most index in which
  // the peak element can be found
  var right = arr.length - 1;
  while (left < right)
  {

    // Stores mid of left and right
    var mid = left + parseInt((right - left) / 2);

    // If element at mid is less than
    // element at (mid + 1)
    if (arr[mid] < arr[mid + 1])
    {

      // Update left
      left = mid + 1;
    }
    else
    {

      // Update right
      right = mid;
    }
  }
  return left;
}

// Function to perform binary search in an
// a subarray if elements of the subarray
// are in an ascending order
function BS(X, left, right, arr)
{
  while (left <= right)
  {

    // Stores mid of left and right
    var mid = left + parseInt((right - left) / 2);

    // If X found at mid
    if (arr[mid] == X)
    {
      return mid;
    }

    // If X is greater than mid
    else if (X > arr[mid])
    {

      // Update left
      left = mid + 1;
    }

    else
    {

      // Update right
      right = mid - 1;
    }
  }
  return -1;
}

// Function to perform binary search in an
// a subarray if elements of the subarray
// are in an ascending order
function reverseBS(X, left, right, arr)
{
  while (left <= right)
  {

    // Stores mid of left and right
    var mid = left + parseInt((right - left) / 2);

    // If X found at mid
    if (arr[mid] == X)
    {
      return mid;
    }

    else if (X > arr[mid])
    {

      // Update right
      right = mid - 1;
    }
    else
    {

      // Update left
      left = mid + 1;
    }
  }
  return -1;
}

// Function to find the smallest index of X
function findInMA(X, mountainArr)
{

  // Stores index of peak element in array
  var peakIndex = findPeak(mountainArr);

  // Stores index of X in the array
  var res = -1;

  // If X greater than or equal to first element
  // of array and less than the peak element
  if (X >= mountainArr[0] && X <= mountainArr[peakIndex])
  {

    // Update res
    res = BS(X, 0, peakIndex, mountainArr);
  }

  // If element not found on
  // left side of peak element
  if (res == -1)
  {

    // Update res
    res = reverseBS(X, peakIndex + 1,
                    mountainArr.length - 1,
                    mountainArr);
  }

  // Print res
  document.write( res + "<br>");
}

// Driver Code
// Given X
var X = 3;
// Given array
var list = [1, 2, 3, 4, 5, 3, 1];
// Function Call
findInMA(X, list);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(Log(N))*
***辅助空间:** O(1)*