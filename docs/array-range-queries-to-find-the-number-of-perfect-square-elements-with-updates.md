# 数组范围查询，通过更新找到完美正方形元素的数量

> 原文:[https://www . geesforgeks . org/array-range-query-to-find-number-of-perfect-square-elements-with-updates/](https://www.geeksforgeeks.org/array-range-queries-to-find-the-number-of-perfect-square-elements-with-updates/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是执行以下两个查询:

*   **查询(开始、结束)**:从开始到结束打印子数组中完美平方数的个数
*   **更新(I，x)** :将 x 添加到数组索引 **i** 引用的数组元素中，即:arr[i] = x

**注意:**在下面的示例中遵循基于 0 的索引。

**示例:**

> **输入:** arr = [ 16，15，8，9，14，25]；
> 查询 1:查询(start = 0，end = 4)
> 查询 2:更新(i = 3，x = 11)即 arr[3]=11
> 查询 3:查询(start = 0，end = 4)
> **输出:** 2 1
> **说明:**
> 在**查询 1** 中，子数组【0…4】有 **2** 个完美的正方形数字 16 和 9【16，15，8，9，14】
> 在**查询 2** 中，索引 3 处的值更新为 11，
> 数组 arr 现在为【16，15，8，11，14，25】
> 在**查询 3** 中，子数组【0…4】具有 **1** 完美平方数 16，即。【16、15、8、11、14】

**进场:**

为了处理点更新和范围查询，一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)最适合这个目的。
为了检查完美平方数，首先要计算这个数的平方根，如果平方根是整数，那么当前元素就是完美平方，否则就不是。如果当前元素是一个完美的正方形，则将它设置为 1，否则设置为 0。

**构建段树:**

*   这个问题现在被简化为[子阵和使用分段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的问题。
*   现在，我们可以构建段树，其中叶节点表示为 0(如果它不是一个完美的平方数)或 1(如果它是一个完美的平方数)。
*   段树的内部节点等于其子节点的总和，因此一个节点代表从 L 到 R 范围内的全部完美平方数，范围[L，R]位于该节点及其下的子树之下。

**处理查询和点更新:**

*   每当我们从头到尾收到一个查询时，我们可以在段树中查询从开始到结束范围内的节点的总和，这又表示从开始到结束范围内的完美平方数的数量。
*   为了执行点更新并将索引 I 处的值更新为 x，我们检查以下情况:
    让 arr[i]的旧值为 y，新值为 x。
    1.  **情况 1:如果 x 和 y 都是完美平方数**
        子阵中完美平方数的个数不变，所以我们只更新数组，不修改段树
    2.  **情况 2:如果 x 和 y 都不是完美平方数**
        子阵中完美平方数的计数不变，所以我们只更新数组，不修改段树
    3.  **情况 3:如果 y 是一个完美的平方数但是 x 不是**
        子阵中完美平方数的计数减少，所以我们更新数组并在每个范围内加-1。要更新的索引 I 是段树中的一部分
    4.  **情况 4:如果 y 不是一个完美的平方数，但是 x 是一个完美的平方数**
        子阵中完美平方数的计数增加，所以我们更新数组，每个范围加 1。要更新的索引 I 是段树中的一部分

下面是上述方法的实现:

## C++

```
// C++ program to find number of
// perfect square numbers in a
// subarray and performing updates

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

// Function to check if a number is
// a perfect square or not
bool isPerfectSquare(long long int x)
{
    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0)
               ? true
               : false;
}

// A utility function to get the middle
// index from corner indexes.
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to get the number
// of perfect square numbers in a given
// range
/* where
  st    --> Pointer to segment tree
  index --> Index of current node in the
            segment tree. Initially 0 is
            passed as root is always
            at index 0
  ss & se  --> Starting and ending indexes
              of the segment represented by
              current node i.e. st[index]
  qs & qe  --> Starting and ending indexes
               of query range   */
int queryUtil(int* st, int ss,
              int se, int qs,
              int qe, int index)
{
    // If segment of this node is a part
    // of given range, then return
    // the number of perfect square numbers
    // in the segment
    if (qs <= ss && qe >= se)
        return st[index];

    // If segment of this node
    // is outside the given range
    if (se < qs || ss > qe)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(ss, se);
    return queryUtil(st, ss, mid, qs,
                     qe, 2 * index + 1)
           + queryUtil(st, mid + 1, se,
                       qs, qe, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
   st, si, ss & se are same as getSumUtil()
   i --> index of the element to be updated.
         This index is in input array.
   diff --> Value to be added to all nodes
          which have i in range
*/
void updateValueUtil(int* st, int ss,
                     int se, int i,
                     int diff, int si)
{
    // Base Case:
    // If the input index lies outside
    // the range of this segment
    if (i < ss || i > se)
        return;

    // If the input index is in range
    // of this node, then update the value
    // of the node and its children
    st[si] = st[si] + diff;
    if (se != ss) {

        int mid = getMid(ss, se);
        updateValueUtil(st, ss, mid, i,
                        diff, 2 * si + 1);
        updateValueUtil(st, mid + 1, se,
                        i, diff, 2 * si + 2);
    }
}

// Function to update a value in the
// input array and segment tree.
// It uses updateValueUtil() to update
// the value in segment tree
void updateValue(int arr[], int* st,
                 int n, int i,
                 int new_val)
{
    // Check for erroneous input index
    if (i < 0 || i > n - 1) {
        printf("Invalid Input");
        return;
    }

    int diff, oldValue;

    oldValue = arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Case 1: Old and new values
    // both are perfect square numbers
    if (isPerfectSquare(oldValue)
        && isPerfectSquare(new_val))
        return;

    // Case 2: Old and new values
    // both not perfect square numbers
    if (!isPerfectSquare(oldValue)
        && !isPerfectSquare(new_val))
        return;

    // Case 3: Old value was perfect square,
    // new value is not a perfect square
    if (isPerfectSquare(oldValue)
        && !isPerfectSquare(new_val)) {
        diff = -1;
    }

    // Case 4: Old value was
    // non-perfect square,
    // new_val is perfect square
    if (!isPerfectSquare(oldValue)
        && !isPerfectSquare(new_val)) {
        diff = 1;
    }

    // Update values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0);
}

// Return no. of perfect square numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryUtil()
void query(int* st, int n,
           int qs, int qe)
{

    int perfectSquareInRange
        = queryUtil(
            st, 0, n - 1, qs, qe, 0);

    cout << perfectSquareInRange << "\n";
}

// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
int constructSTUtil(int arr[], int ss,
                    int se, int* st,
                    int si)
{
    // If there is one element in array,
    // check if it is perfect square number
    // then store 1 in the segment tree
    // else store 0 and return
    if (ss == se) {

        // if arr[ss] is a perfect
        // square number
        if (isPerfectSquare(arr[ss]))
            st[si] = 1;
        else
            st[si] = 0;

        return st[si];
    }

    // If there are more than one
    // elements, then recur for
    // left and right subtrees
    // and store the sum of the
    // two values in this node
    int mid = getMid(ss, se);
    st[si]
        = constructSTUtil(arr, ss,
                          mid, st, si * 2 + 1)
          + constructSTUtil(arr, mid + 1,
                            se, st, si * 2 + 2);
    return st[si];
}

// Function to construct a segment
// tree from given array. This
// function allocates memory for
// segment tree and calls
// constructSTUtil() to fill
// the allocated memory
int* constructST(int arr[], int n)
{

    // Allocate memory for segment tree
    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    int* st = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Driver Code
int main()
{
    int arr[] = { 16, 15, 8, 9, 14, 25 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    int* st = constructST(arr, n);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    query(st, n, start, end);

    // Query 2: Update(i = 3, x = 11),
    // i.e Update a[i] to x
    int i = 3;
    int x = 11;
    updateValue(arr, st, n, i, x);

    // uncomment to see array after update
    // for(int i = 0; i < n; i++)
    // cout << arr[i] << " ";

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    query(st, n, start, end);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of
// perfect square numbers in a
// subarray and performing updates
import java.util.*;
class GFG{

static final int MAX = 1000;

// Function to check if a number is
// a perfect square or not
static boolean isPerfectSquare(int x)
{
  // Find floating point value of
  // square root of x.
  double sr = Math.sqrt(x);

  // If square root is an integer
  return ((sr - Math.floor(sr)) == 0) ?
           true : false;
}

// A utility function to get
// the middle index from
// corner indexes.
static int getMid(int s,
                  int e)
{
  return s + (e - s) / 2;
}

// Recursive function to get the number
// of perfect square numbers in a given
// range
/* where
  st    -. Pointer to segment tree
  index -. Index of current node in the
            segment tree. Initially 0 is
            passed as root is always
            at index 0
  ss & se  -. Starting and ending indexes
              of the segment represented by
              current node i.e. st[index]
  qs & qe  -. Starting and ending indexes
               of query range   */
static int queryUtil(int []st, int ss,
                     int se, int qs,
                     int qe, int index)
{
  // If segment of this node is a part
  // of given range, then return
  // the number of perfect square numbers
  // in the segment
  if (qs <= ss && qe >= se)
    return st[index];

  // If segment of this node
  // is outside the given range
  if (se < qs || ss > qe)
    return 0;

  // If a part of this segment
  // overlaps with the given range
  int mid = getMid(ss, se);
  return queryUtil(st, ss, mid, qs,
                   qe, 2 * index + 1) +
         queryUtil(st, mid + 1, se,
                   qs, qe, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
   st, si, ss & se are same as getSumUtil()
   i -. index of the element to be updated.
         This index is in input array.
   diff -. Value to be added to all nodes
          which have i in range
*/
static void updateValueUtil(int []st, int ss,
                            int se, int i,
                            int diff, int si)
{
  // Base Case:
  // If the input index lies outside
  // the range of this segment
  if (i < ss || i > se)
    return;

  // If the input index is in range
  // of this node, then update the value
  // of the node and its children
  st[si] = st[si] + diff;
  if (se != ss)
  {
    int mid = getMid(ss, se);
    updateValueUtil(st, ss, mid, i,
                    diff, 2 * si + 1);
    updateValueUtil(st, mid + 1, se,
                    i, diff, 2 * si + 2);
  }
}

// Function to update a value in the
// input array and segment tree.
// It uses updateValueUtil() to update
// the value in segment tree
static void updateValue(int arr[], int[] st,
                        int n, int i,
                        int new_val)
{
  // Check for erroneous
  // input index
  if (i < 0 || i > n - 1)
  {
    System.out.printf("Invalid Input");
    return;
  }

  int diff = 0, oldValue;
  oldValue = arr[i];

  // Update the value in array
  arr[i] = new_val;

  // Case 1: Old and new values
  // both are perfect square numbers
  if (isPerfectSquare(oldValue) &&
      isPerfectSquare(new_val))
    return;

  // Case 2: Old and new values
  // both not perfect square numbers
  if (!isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
    return;

  // Case 3: Old value was perfect square,
  // new value is not a perfect square
  if (isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
  {
    diff = -1;
  }

  // Case 4: Old value was
  // non-perfect square,
  // new_val is perfect square
  if (!isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
  {
    diff = 1;
  }

  // Update values of nodes
  // in segment tree
  updateValueUtil(st, 0, n - 1,
                  i, diff, 0);
}

// Return no. of perfect square numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryUtil()
static void query(int[] st, int n,
                  int qs, int qe)
{
  int perfectSquareInRange = queryUtil(st, 0,
                                       n - 1,
                                       qs, qe, 0);
  System.out.print(perfectSquareInRange + "\n");
}

// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
static int constructSTUtil(int arr[], int ss,
                           int se, int []st, int si)
{
  // If there is one element
  // in array, check if it is
  // perfect square number
  // then store 1 in the
  //segment tree else
  // store 0 and return
  if (ss == se)
  {
    // if arr[ss] is a perfect
    // square number
    if (isPerfectSquare(arr[ss]))
      st[si] = 1;
    else
      st[si] = 0;

    return st[si];
  }

  // If there are more than one
  // elements, then recur for
  // left and right subtrees
  // and store the sum of the
  // two values in this node
  int mid = getMid(ss, se);
  st[si] = constructSTUtil(arr, ss,
                           mid, st,
                           si * 2 + 1) +
            constructSTUtil(arr, mid + 1,
                            se, st, si * 2 + 2);
  return st[si];
}

// Function to cona segment
// tree from given array. This
// function allocates memory for
// segment tree and calls
// constructSTUtil() to fill
// the allocated memory
static int[] constructST(int arr[],
                         int n)
{
  // Allocate memory for segment tree
  // Height of segment tree
  int x = (int)(Math.ceil(Math.log(n)));

  // Maximum size of segment tree
  int max_size = 4 * (int)Math.pow(2, x) + 1;

  int []st = new int[max_size];

  // Fill the allocated memory st
  constructSTUtil(arr, 0, n - 1, st, 0);

  // Return the constructed segment tree
  return st;
}

// Driver Code
public static void main(String[] args)
{
  int arr[] = {16, 15, 8, 9, 14, 25};
  int n = arr.length;

  // Build segment tree from
  // given array
  int []st = constructST(arr, n);

  // Query 1: Query
  // (start = 0, end = 4)
  int start = 0;
  int end = 4;
  query(st, n, start, end);

  // Query 2: Update(i = 3, x = 11),
  // i.e Update a[i] to x
  int i = 3;
  int x = 11;
  updateValue(arr, st, n, i, x);

  // uncomment to see array after
  // update for(int i = 0; i < n; i++)
  // System.out.print(arr[i]+ " ");

  // Query 3: Query(start = 0, end = 4)
  start = 0;
  end = 4;
  query(st, n, start, end);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python program to find number of
# perfect square numbers in a
# subarray and performing updates
from math import sqrt, floor, ceil, log2
from typing import List
MAX = 1000

# Function to check if a number is
# a perfect square or not
def isPerfectSquare(x: int) -> bool:

    # Find floating point value of
    # square root of x.
    sr = sqrt(x)

    # If square root is an integer
    return True if ((sr - floor(sr)) == 0) else False

# A utility function to get the middle
# index from corner indexes.
def getMid(s: int, e: int) -> int:
    return s + (e - s) // 2

# Recursive function to get the number
# of perfect square numbers in a given
# range
''' where
  st    --> Pointer to segment tree
  index --> Index of current node in the
            segment tree. Initially 0 is
            passed as root is always
            at index 0
  ss & se  --> Starting and ending indexes
              of the segment represented by
              current node i.e. st[index]
  qs & qe  --> Starting and ending indexes
               of query range   '''
def queryUtil(st: List[int], ss: int, se: int,
              qs: int, qe: int,
              index: int) -> int:

    # If segment of this node is a part
    # of given range, then return
    # the number of perfect square numbers
    # in the segment
    if (qs <= ss and qe >= se):
        return st[index]

    # If segment of this node
    # is outside the given range
    if (se < qs or ss > qe):
        return 0

    # If a part of this segment
    # overlaps with the given range
    mid = getMid(ss, se)
    return queryUtil(st, ss, mid, qs, qe, 2 * index + 1) + queryUtil(
        st, mid + 1, se, qs, qe, 2 * index + 2)

# Recursive function to update
# the nodes which have the given
# index in their range.
''' where
   st, si, ss & se are same as getSumUtil()
   i --> index of the element to be updated.
         This index is in input array.
   diff --> Value to be added to all nodes
          which have i in range
'''
def updateValueUtil(st: List[int], ss: int, se: int,
                    i: int, diff: int,
                    si: int) -> None:

    # Base Case:
    # If the input index lies outside
    # the range of this segment
    if (i < ss or i > se):
        return

    # If the input index is in range
    # of this node, then update the value
    # of the node and its children
    st[si] = st[si] + diff
    if (se != ss):

        mid = getMid(ss, se)
        updateValueUtil(st, ss, mid, i,
                        diff, 2 * si + 1)
        updateValueUtil(st, mid + 1, se, i,
                        diff, 2 * si + 2)

# Function to update a value in the
# input array and segment tree.
# It uses updateValueUtil() to update
# the value in segment tree
def updateValue(arr: List[int], st: List[int],
                n: int, i: int,
                new_val: int) -> None:

    # Check for erroneous input index
    if (i < 0 or i > n - 1):
        print("Invalid Input")
        return

    diff = 0
    oldValue = 0

    oldValue = arr[i]

    # Update the value in array
    arr[i] = new_val

    # Case 1: Old and new values
    # both are perfect square numbers
    if (isPerfectSquare(oldValue) and isPerfectSquare(new_val)):
        return

    # Case 2: Old and new values
    # both not perfect square numbers
    if (not isPerfectSquare(oldValue) and not isPerfectSquare(new_val)):
        return

    # Case 3: Old value was perfect square,
    # new value is not a perfect square
    if (isPerfectSquare(oldValue) and not isPerfectSquare(new_val)):
        diff = -1

    # Case 4: Old value was
    # non-perfect square,
    # new_val is perfect square
    if (not isPerfectSquare(oldValue) and not isPerfectSquare(new_val)):
        diff = 1

    # Update values of nodes in segment tree
    updateValueUtil(st, 0, n - 1, i, diff, 0)

# Return no. of perfect square numbers
# in range from index qs (query start)
# to qe (query end).
# It mainly uses queryUtil()
def query(st: List[int], n: int, qs: int, qe: int) -> None:

    perfectSquareInRange = queryUtil(st, 0, n - 1, qs, qe, 0)

    print(perfectSquareInRange)

# Recursive function that constructs
# Segment Tree for array[ss..se].
# si is index of current node
# in segment tree st
def constructSTUtil(arr: List[int], ss: int, se: int, st: List[int],
                    si: int) -> int:

    # If there is one element in array,
    # check if it is perfect square number
    # then store 1 in the segment tree
    # else store 0 and return
    if (ss == se):

        # if arr[ss] is a perfect
        # square number
        if (isPerfectSquare(arr[ss])):
            st[si] = 1
        else:
            st[si] = 0

        return st[si]

    # If there are more than one
    # elements, then recur for
    # left and right subtrees
    # and store the sum of the
    # two values in this node
    mid = getMid(ss, se)
    st[si] = constructSTUtil(arr, ss, mid, st, si * 2 + 1) + constructSTUtil(
        arr, mid + 1, se, st, si * 2 + 2)
    return st[si]

# Function to construct a segment
# tree from given array. This
# function allocates memory for
# segment tree and calls
# constructSTUtil() to fill
# the allocated memory
def constructST(arr: List[int], n: int) -> List[int]:

    # Allocate memory for segment tree
    # Height of segment tree
    x = (ceil(log2(n)))

    # Maximum size of segment tree
    max_size = 2 * pow(2, x) - 1

    st = [0 for _ in range(max_size)]

    # Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, st, 0)

    # Return the constructed segment tree
    return st

# Driver Code
if __name__ == "__main__":

    arr = [16, 15, 8, 9, 14, 25]
    n = len(arr)

    # Build segment tree from given array
    st = constructST(arr, n)

    # Query 1: Query(start = 0, end = 4)
    start = 0
    end = 4
    query(st, n, start, end)

    # Query 2: Update(i = 3, x = 11),
    # i.e Update a[i] to x
    i = 3
    x = 11
    updateValue(arr, st, n, i, x)

    # uncomment to see array after update
    # for(int i = 0; i < n; i++)
    # cout << arr[i] << " ";

    # Query 3: Query(start = 0, end = 4)
    start = 0
    end = 4
    query(st, n, start, end)

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to find number of
// perfect square numbers in a
// subarray and performing updates
using System;
class GFG{

static readonly int MAX = 1000;

// Function to check if a number
// is a perfect square or not
static bool isPerfectSquare(int x)
{
  // Find floating point value of
  // square root of x.
  double sr = Math.Sqrt(x);

  // If square root is an integer
  return ((sr - Math.Floor(sr)) == 0) ?
           true : false;
}

// A utility function to get
// the middle index from
// corner indexes.
static int getMid(int s,
                  int e)
{
  return s + (e - s) / 2;
}

// Recursive function to get the number
// of perfect square numbers in a given
// range
/* where
st -. Pointer to segment tree
index -. Index of current node in the
            segment tree. Initially 0 is
            passed as root is always
            at index 0
ss & se -. Starting and ending indexes
            of the segment represented by
            current node i.e. st[index]
qs & qe -. Starting and ending indexes
            of query range */
static int queryUtil(int []st, int ss,
                     int se, int qs,
                     int qe, int index)
{
  // If segment of this node is a part
  // of given range, then return the
  // number of perfect square numbers
  // in the segment
  if (qs <= ss && qe >= se)
    return st[index];

  // If segment of this node
  // is outside the given range
  if (se < qs || ss > qe)
    return 0;

  // If a part of this segment
  // overlaps with the given range
  int mid = getMid(ss, se);
  return queryUtil(st, ss, mid, qs,
                   qe, 2 * index + 1) +
         queryUtil(st, mid + 1, se,
                   qs, qe, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
st, si, ss & se are same as getSumUtil()
i -. index of the element to be updated.
        This index is in input array.
diff -. Value to be added to all nodes
        which have i in range
*/
static void updateValueUtil(int []st, int ss,
                            int se, int i,
                            int diff, int si)
{
  // Base Case:
  // If the input index lies outside
  // the range of this segment
  if (i < ss || i > se)
    return;

  // If the input index is in range
  // of this node, then update the value
  // of the node and its children
  st[si] = st[si] + diff;

  if (se != ss)
  {
    int mid = getMid(ss, se);
    updateValueUtil(st, ss, mid, i,
                    diff, 2 * si + 1);
    updateValueUtil(st, mid + 1, se,
                    i, diff, 2 * si + 2);
  }
}

// Function to update a value in the
// input array and segment tree.
// It uses updateValueUtil() to update
// the value in segment tree
static void updateValue(int []arr, int[] st,
                        int n, int i,
                        int new_val)
{
  // Check for erroneous
  // input index
  if (i < 0 || i > n - 1)
  {
    Console.Write("Invalid Input");
    return;
  }

  int diff = 0, oldValue;
  oldValue = arr[i];

  // Update the value in array
  arr[i] = new_val;

  // Case 1: Old and new values
  // both are perfect square numbers
  if (isPerfectSquare(oldValue) &&
      isPerfectSquare(new_val))
    return;

  // Case 2: Old and new values
  // both not perfect square numbers
  if (!isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
    return;

  // Case 3: Old value was perfect
  // square, new value is not a
  // perfect square
  if (isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
  {
    diff = -1;
  }

  // Case 4: Old value was
  // non-perfect square,
  // new_val is perfect square
  if (!isPerfectSquare(oldValue) &&
      !isPerfectSquare(new_val))
  {
    diff = 1;
  }

  // Update values of nodes
  // in segment tree
  updateValueUtil(st, 0, n - 1,
                  i, diff, 0);
}

// Return no. of perfect square numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryUtil()
static void query(int[] st, int n,
                  int qs, int qe)
{
int perfectSquareInRange = queryUtil(st, 0,
                                     n - 1,
                                     qs, qe, 0);
Console.Write(perfectSquareInRange + "\n");
}

// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
static int constructSTUtil(int []arr, int ss,
                           int se, int []st, int si)
{
  // If there is one element
  // in array, check if it is
  // perfect square number
  // then store 1 in the
  //segment tree else
  // store 0 and return
  if (ss == se)
  {
    // if arr[ss] is a perfect
    // square number
    if (isPerfectSquare(arr[ss]))
      st[si] = 1;
    else
      st[si] = 0;

    return st[si];
  }

  // If there are more than one
  // elements, then recur for
  // left and right subtrees
  // and store the sum of the
  // two values in this node
  int mid = getMid(ss, se);
  st[si] = constructSTUtil(arr, ss,
                           mid, st,
                           si * 2 + 1) +
    constructSTUtil(arr, mid + 1,
                    se, st, si * 2 + 2);
  return st[si];
}

// Function to cona segment
// tree from given array. This
// function allocates memory for
// segment tree and calls
// constructSTUtil() to fill
// the allocated memory
static int[] constructST(int []arr,
                         int n)
{
// Allocate memory for segment tree
// Height of segment tree
int x = (int)(Math.Ceiling(Math.Log(n)));

// Maximum size of segment tree
int max_size = 4 * (int)Math.Pow(2,
                                 x) + 1;

int []st = new int[max_size];

// Fill the allocated
// memory st
constructSTUtil(arr, 0,
                n - 1,
                st, 0);

// Return the constructed
// segment tree
return st;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {16, 15, 8, 9, 14, 25};
  int n = arr.Length;

  // Build segment tree
  // from given array
  int []st = constructST(arr, n);

  // Query 1: Query
  // (start = 0, end = 4)
  int start = 0;
  int end = 4;
  query(st, n, start, end);

  // Query 2: Update(i = 3,
  // x = 11), i.e Update a[i] to x
  int i = 3;
  int x = 11;
  updateValue(arr, st, n, i, x);

  // uncomment to see array after
  // update for(int i = 0; i < n; i++)
  // Console.Write(arr[i]+ " ");

  // Query 3: Query(start = 0,
  // end = 4)
  start = 0;
  end = 4;
  query(st, n, start, end);
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
2
1
```

***时间复杂度:**每次查询更新的时间复杂度为 **O(log N)** ，构建段树的时间复杂度为 **O(N)***