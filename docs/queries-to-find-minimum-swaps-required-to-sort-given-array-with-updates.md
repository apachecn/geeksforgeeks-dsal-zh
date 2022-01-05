# 查询以找到用更新对给定数组进行排序所需的最小交换量

> 原文:[https://www . geesforgeks . org/query-to-find-minimum-swaps-required-to-sort-给定数组-带更新/](https://www.geeksforgeeks.org/queries-to-find-minimum-swaps-required-to-sort-given-array-with-updates/)

给定大小为 **N** 的排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和具有形式为 **{x，y}** 的查询的数组 **Q[][]** 。在每个查询 **{x，y}** 中，通过将值**arr【x】**增加 **y** 来更新给定数组。任务是找到[排序数组](https://www.geeksforgeeks.org/sorting-algorithms/)所需的最小交换次数，该数组是在给定数组中单独执行每个查询后获得的。

**示例:**

> **输入:** arr[] = {2，3，4，5，6}，Q[][] = {{2，8}，{3，1}}
> **输出:** 2 0
> **解释:**
> 以下是每个查询所需的交换次数:
> **查询 1:** 将 arr[2]增加 8。因此，arr[] = {2，3，12，5，6}。
> 要使该数组排序，将 12 向右移动 2 个位置。
> 现在 arr[] = {2，3，5，6，12}。因此，它需要 2 次互换。
> **查询 2:** 将 arr[3]增加 1。因此，arr[] = {2，3，4，6，6}。
> 数组仍然排序。因此，它需要 0 次交换。
> 
> **输入:** arr[] = {2，3，4，5，6}，Q[][] = {{0，-1}，{4，-11 } }；
> **输出:** 0 4
> **说明:**
> 以下是每个查询所需的交换次数:
> **查询 1:** 将 arr[0]增加-1。因此，arr[] = {1，3，4，5，6}。
> 数组仍然排序。因此，它需要 0 次交换。
> **查询 2:** 将 arr[4]增加-11。因此，arr[] = {2，3，4，5，-5}。
> 要使这个数组排序，将 shift -5 向左移动 4 个位置。
> 现在 arr[] = {-5，2，3，4，5}。因此，它需要 4 次互换。

**简单方法:**最简单的方法是为每个查询 **{x，y}** 将值**arr【x】**递增 **y** 来更新给定的数组。之后，遍历更新后的数组，当 **arr[x]** 大于 **arr[x+1]** 时，向右交换 **arr[x]** ，每次递增 **x** ，然后向左交换 **arr[x]** ，而 **arr[x]** 小于 **arr[x-1]** ，每次递减 **x** 打印 **x** 的初始值和最终值的绝对差值。

***时间复杂度:** O(Q*N <sup>2</sup> ，其中 N 是给定数组的长度，Q 是查询的总数。*
***辅助空间:** O(N)*

**高效方法:**想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来找到在每次查询后对给定的[数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)所需的最小交换次数。按照以下步骤解决问题:

1.  对于每个查询 **{x，y}** ，将值**arr【x】+y**存储在变量**新元素**中。
2.  使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，找到给定数组中的值的索引，该值刚好小于或等于值**新元素**。
3.  如果找不到这样的值，打印 **x** ，否则将该值放在索引 **j** 处。
4.  打印索引 **i** 和索引 **j** 之间的绝对差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the position of
// the given value using binary search
int computePos(int arr[], int n,
               int value)
{
    // Return 0 if every value is
    // greater than the given value
    if (value < arr[0])
        return 0;

    // Return N-1 if every value is
    // smaller than the given value
    if (value > arr[n - 1])
        return n - 1;

    // Perform Binary Search
    int start = 0;
    int end = n - 1;

    // Iterate till start < end
    while (start < end) {

        // Find the mid
        int mid = (start + end + 1) / 2;

        // Update start and end
        if (arr[mid] >= value)
            end = mid - 1;
        else
            start = mid;
    }

    // Return the position of
    // the given value
    return start;
}

// Function to return the number of
// make the array sorted
void countShift(int arr[], int n,
                vector<vector<int> >& queries)
{
    for (auto q : queries) {

        // Index x to update
        int index = q[0];

        // Increment value by y
        int update = q[1];

        // Set newElement equals
        // to x + y
        int newElement = arr[index]
                         + update;

        // Compute the new index
        int newIndex = computePos(
            arr, n, newElement);

        // Print the minimum number
        // of swaps
        cout << abs(newIndex - index)
             << " ";
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 3, 4, 5, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Given Queries
    vector<vector<int> > queries
        = { { 0, -1 }, { 4, -11 } };

    // Function Call
    countShift(arr, N, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to return the position of
// the given value using binary search
static int computePos(int arr[],
                      int n, int value)
{
  // Return 0 if every value is
  // greater than the given value
  if (value < arr[0])
    return 0;

  // Return N-1 if every value is
  // smaller than the given value
  if (value > arr[n - 1])
    return n - 1;

  // Perform Binary Search
  int start = 0;
  int end = n - 1;

  // Iterate till start < end
  while (start < end)
  {
    // Find the mid
    int mid = (start +
               end + 1) / 2;

    // Update start and end
    if (arr[mid] >= value)
      end = mid - 1;
    else
      start = mid;
  }

  // Return the position of
  // the given value
  return start;
}

// Function to return the number of
// make the array sorted
static void countShift(int arr[], int n,
                       Vector<Vector<Integer> > queries)
{
  for (Vector<Integer> q : queries)
  {
    // Index x to update
    int index = q.get(0);

    // Increment value by y
    int update = q.get(1);

    // Set newElement equals
    // to x + y
    int newElement = arr[index] + update;

    // Compute the new index
    int newIndex = computePos(arr, n,
                              newElement);

    // Print the minimum number
    // of swaps
    System.out.print(Math.abs(newIndex -
                              index) + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {2, 3, 4, 5, 6};

  int N = arr.length;

  // Given Queries
  Vector<Vector<Integer> > queries =
                new Vector<>();
  Vector<Integer> v =
         new Vector<>();
  Vector<Integer> v1 =
         new Vector<>();

  v.add(0);
  v.add(-1);
  queries.add(v);
  v1.add(4);
  v1.add(-11);
  queries.add(v1);

  // Function Call
  countShift(arr, N, queries);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the position of
# the given value using binary search
def computePos(arr, n, value):

    # Return 0 if every value is
    # greater than the given value
    if (value < arr[0]):
        return 0

    # Return N-1 if every value is
    # smaller than the given value
    if (value > arr[n - 1]):
        return n - 1

    # Perform Binary Search
    start = 0
    end = n - 1

    # Iterate till start < end
    while (start < end):

        # Find the mid
        mid = (start + end + 1) // 2

        # Update start and end
        if (arr[mid] >= value):
            end = mid - 1
        else:
            start = mid

    # Return the position of
    # the given value
    return start

# Function to return the number of
# make the array sorted
def countShift(arr, n, queries):

    for q in queries:

        # Index x to update
        index = q[0]

        # Increment value by y
        update = q[1]

        # Set newElement equals
        # to x + y
        newElement = arr[index] + update

        # Compute the new index
        newIndex = computePos(arr, n, newElement)

        # Print the minimum number
        # of swaps
        print(abs(newIndex - index), end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 3, 4, 5, 6 ]

    N = len(arr)

    # Given Queries
    queries = [ [ 0, -1 ], [4, -11 ] ]

    # Function Call
    countShift(arr, N, queries)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the position of
// the given value using binary search
static int computePos(int []arr,
                      int n, int value)
{
  // Return 0 if every value is
  // greater than the given value
  if (value < arr[0])
    return 0;

  // Return N-1 if every value is
  // smaller than the given value
  if (value > arr[n - 1])
    return n - 1;

  // Perform Binary Search
  int start = 0;
  int end = n - 1;

  // Iterate till start
  // < end
  while (start < end)
  {
    // Find the mid
    int mid = (start +
               end + 1) / 2;

    // Update start and end
    if (arr[mid] >= value)
      end = mid - 1;
    else
      start = mid;
  }

  // Return the position of
  // the given value
  return start;
}

// Function to return the number of
// make the array sorted
static void countShift(int []arr, int n,
                       List<List<int> >
                       queries)
{
  foreach (List<int> q in queries)
  {
    // Index x to update
    int index = q[0];

    // Increment value by y
    int update = q[1];

    // Set newElement equals
    // to x + y
    int newElement = arr[index] +
                     update;

    // Compute the new index
    int newIndex = computePos(arr, n,
                              newElement);

    // Print the minimum number
    // of swaps
    Console.Write(Math.Abs(newIndex -
                           index) + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {2, 3, 4, 5, 6};

  int N = arr.Length;

  // Given Queries
  List<List<int> > queries =
            new List<List<int>>();
  List<int> v =
       new List<int>();
  List<int> v1 =
       new List<int>();

  v.Add(0);
  v.Add(-1);
  queries.Add(v);
  v1.Add(4);
  v1.Add(-11);
  queries.Add(v1);

  // Function Call
  countShift(arr, N, queries);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the position of
// the given value using binary search
function computePos(arr, n, value)
{
    // Return 0 if every value is
    // greater than the given value
    if (value < arr[0])
        return 0;

    // Return N-1 if every value is
    // smaller than the given value
    if (value > arr[n - 1])
        return n - 1;

    // Perform Binary Search
    var start = 0;
    var end = n - 1;

    // Iterate till start < end
    while (start < end) {

        // Find the mid
        var mid = parseInt((start + end + 1) / 2);

        // Update start and end
        if (arr[mid] >= value)
            end = mid - 1;
        else
            start = mid;
    }

    // Return the position of
    // the given value
    return start;
}

// Function to return the number of
// make the array sorted
function countShift(arr, n, queries)
{
    for(var i =0; i< queries.length; i++)
    {
        // Index x to update
        var index = queries[i][0];

        // Increment value by y
        var update = queries[i][1];

        // Set newElement equals
        // to x + y
        var newElement = arr[index]
                         + update;

        // Compute the new index
        var newIndex = computePos(
            arr, n, newElement);

        // Print the minimum number
        // of swaps
        document.write( Math.abs(newIndex - index)
             + " ");
    }
}

// Driver Code
// Given array arr[]
var arr = [ 2, 3, 4, 5, 6 ];
var N = arr.length;

// Given Queries
var queries = [[ 0, -1 ], [ 4, -11 ]];

// Function Call
countShift(arr, N, queries);

</script>
```

**Output:** 

```
0 4
```

***时间复杂度:**O(Q * N * log N)*
T5**辅助空间:** O(N)