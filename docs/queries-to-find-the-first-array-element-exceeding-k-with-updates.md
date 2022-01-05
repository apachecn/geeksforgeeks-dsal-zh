# 查询找到第一个超过 K 的数组元素并更新

> 原文:[https://www . geeksforgeeks . org/query-to-find-first-array-element-over-k-with-updates/](https://www.geeksforgeeks.org/queries-to-find-the-first-array-element-exceeding-k-with-updates/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和由以下两种类型的查询组成的 [2D 数组](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) **Q[][]** :

*   **1 X Y:** 用 **Y.** 更新索引 **X** 处的数组元素
*   **2 K:** 打印大于等于 **K** 的第一个数组元素的位置。如果没有这样的索引，那么打印 **-1** 。

**示例:**

> **输入** : arr[] = { 1，3，2，4，6 }，Q[][] = {{2，5}，{ 1，3，5}，{2，4}，{2，8}}
> **输出** : 5 3 -1
> **解释:**
> 查询 1:自 arr[4] > 5 开始，arr[4]的位置为 5。
> 查询 2:用 5 更新 arr[2]将 arr[]修改为{1，3，5，4，6}
> 查询 3:由于 arr[2] > 4，arr[4]的位置为 5。
> 查询 4:没有大于 8 的数组元素。
> 
> **输入** : arr[] = {1，2，3}，N = 3，Q[][] = {{2，2}，{1，3，5}，{2，10}}
> 输出 : 2 -1

**天真方法:**解决这个问题最简单的方法如下:

*   对于类型为 **1** 的查询，则更新**arr【X–1】**为 **Y** 。
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，打印第一个数组元素大于等于 **K** 的位置。

***时间复杂度:**O(N * | Q |)*
T5**辅助空间:** O(1)

**高效途径:**上述途径可以通过[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)进行优化。想法是使用[范围最大查询和节点更新](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)的概念来构建和更新树。按照以下步骤解决问题:

*   [建立一个段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，每个节点由它的[子树的最大值组成。](https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/)
*   可以使用[范围最大查询和节点更新](https://www.geeksforgeeks.org/segment-tree-set-2-range-maximum-query-node-update/)的概念进行更新操作
*   大于或等于 **K** 的第一个数组元素的位置可以通过递归检查以下条件来找到:
    *   检查左子树的根是否大于或等于 **K** 。如果发现是真的，那么从左边的子树中找到位置。如果在左子树中没有找到这样的数组元素，那么递归地找到右子树中的位置。
    *   否则，递归查找右子树中的位置。
*   最后，打印大于等于 **K** 的数组元素的位置。

**以下是上述方法**的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the mid
// of start and end
int getMid(int s, int e) { return s + (e - s) / 2; }

// Function to update nodes at position index
void updateValue(int arr[], int* st, int ss, int se,
                 int index, int value, int node)
{

    // If index is out of range
    if (index < ss || index > se) {
        cout << "Invalid Input" << endl;
        return;
    }

    // If a leaf node is found
    if (ss == se) {

        // update value in array
        arr[index] = value;

        // Update value in
        // the segment tree
        st[node] = value;
    }
    else {

        // Stores mid of ss and se
        int mid = getMid(ss, se);

        // If index is less than or
        // equal to mid
        if (index >= ss && index <= mid) {

            // Recursively call for left subtree
            updateValue(arr, st, ss, mid, index, value,
                        2 * node + 1);
        }
        else {

            // Recursively call for right subtree
            updateValue(arr, st, mid + 1, se, index, value,
                        2 * node + 2);
        }

        // Update st[node]
        st[node] = max(st[2 * node + 1], st[2 * node + 2]);
    }
    return;
}

// Function to find the position of first element
// which is greater than or equal to X
int findMinimumIndex(int* st, int ss, int se, int K, int si)
{

    // If no such element found in current
    // subtree which is greater than or
    // equal to K
    if (st[si] < K)
        return 1e9;

    // If current node is leaf node
    if (ss == se) {

        // If value of current node
        // is greater than or equal to X
        if (st[si] >= K) {

            return ss;
        }

        return 1e9;
    }

    // Stores mid of ss and se
    int mid = getMid(ss, se);

    int l = 1e9;

    // If root of left subtree is
    // greater than or equal to K
    if (st[2 * si + 1] >= K)
        l = min(l, findMinimumIndex(st, ss, mid, K,
                                    2 * si + 1));

    // If no such array element is
    // found in the left subtree
    if (l == 1e9 && st[2 * si + 2] >= K)
        l = min(l, findMinimumIndex(st, mid + 1, se, K,
                                    2 * si + 2));

    return l;
}

// Function to build a segment tree
int Build(int arr[], int ss, int se, int* st, int si)
{

    // If current node is leaf node
    if (ss == se) {
        st[si] = arr[ss];
        return arr[ss];
    }

    // store mid of ss and se
    int mid = getMid(ss, se);

    // Stores maximum of left subtree and rightsubtree
    st[si] = max(Build(arr, ss, mid, st, si * 2 + 1),
                 Build(arr, mid + 1, se, st, si * 2 + 2));

    return st[si];
}

// Function to initialize a segment tree
// for the given array
int* constructST(int arr[], int n)
{

    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    // Allocate memory
    int* st = new int[max_size];

    // Fill the allocated memory st
    Build(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

// Function to perform the queries of
// the given type
void PerformQueries(int arr[], int N,
                    vector<vector<int> > Q)
{

    // Build segment tree for the given array
    int* st = constructST(arr, N);

    // Traverse the query array
    for (int i = 0; i < Q.size(); i++) {

        // If query of type 1 found
        if (Q[i][0] == 1)

            updateValue(arr, st, 0, N - 1, Q[i][1] - 1, 5,
                        0);
        else {

            // Stores index of first array element
            // which is greater than or equal
            // to Q[i][1]
            int f = findMinimumIndex(st, 0, N - 1, Q[i][1],
                                     0);
            if (f < N)
                cout << f + 1 << " ";
            else
                cout << -1 << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 2, 4, 6 };

    vector<vector<int> > Q{
        { 2, 5 }, { 1, 3, 5 }, { 2, 4 }, { 2, 8 }
    };
    int N = sizeof(arr) / sizeof(arr[0]);

    PerformQueries(arr, N, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
class GFG
{

  // Function to find the mid
  // of start and end
  static int getMid(int s, int e)
  {
    return s + (e - s) / 2;
  }
  static void updateValue(int arr[], int[] st, int ss,
                          int se, int index, int value,
                          int node)
  {

    // If index is out of range
    if (index < ss || index > se)
    {
      System.out.println("Invalid Input");
      return;
    }

    // If a leaf node is found
    if (ss == se)
    {

      // update value in array
      arr[index] = value;

      // Update value in
      // the segment tree
      st[node] = value;
    }
    else
    {

      // Stores mid of ss and se
      int mid = getMid(ss, se);

      // If index is less than or
      // equal to mid
      if (index >= ss && index <= mid)
      {

        // Recursively call for left subtree
        updateValue(arr, st, ss, mid, index, value,
                    2 * node + 1);
      }
      else
      {

        // Recursively call for right subtree
        updateValue(arr, st, mid + 1, se, index,
                    value, 2 * node + 2);
      }

      // Update st[node]
      st[node] = Math.max(st[2 * node + 1],
                          st[2 * node + 2]);
    }
  }

  // Function to find the position of first element
  // which is greater than or equal to X
  static int findMinimumIndex(int[] st, int ss, int se,
                              int K, int si)
  {

    // If no such element found in current
    // subtree which is greater than or
    // equal to K
    if (st[si] < K)
      return 1000000000;

    // If current node is leaf node
    if (ss == se)
    {

      // If value of current node
      // is greater than or equal to X
      if (st[si] >= K)
      {
        return ss;
      }
      return 1000000000;
    }

    // Stores mid of ss and se
    int mid = getMid(ss, se);

    int l = 1000000000;

    // If root of left subtree is
    // greater than or equal to K
    if (st[2 * si + 1] >= K)
      l = Math.min(l, findMinimumIndex(st, ss, mid, K,
                                       2 * si + 1));

    // If no such array element is
    // found in the left subtree
    if (l == 1e9 && st[2 * si + 2] >= K)
      l = Math.min(l,
                   findMinimumIndex(st, mid + 1, se,
                                    K, 2 * si + 2));

    return l;
  }

  // Function to build a segment tree
  static int Build(int arr[], int ss, int se, int[] st,
                   int si)
  {

    // If current node is leaf node
    if (ss == se)
    {
      st[si] = arr[ss];
      return arr[ss];
    }

    // store mid of ss and se
    int mid = getMid(ss, se);

    // Stores maximum of left subtree and rightsubtree
    st[si] = Math.max(
      Build(arr, ss, mid, st, si * 2 + 1),
      Build(arr, mid + 1, se, st, si * 2 + 2));

    return st[si];
  }

  // Function to initialize a segment tree
  // for the given array
  static int[] constructST(int arr[], int n)
  {

    // Height of segment tree
    int x = (int)Math.ceil(Math.log(n) / Math.log(2));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.pow(2, x) - 1;

    // Allocate memory
    int[] st = new int[max_size];

    // Fill the allocated memory st
    Build(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
  }
  static void PerformQueries(int arr[], int N, int[][] Q)
  {

    // Build segment tree for the given array
    int[] st = constructST(arr, N);

    // Traverse the query array
    for (int i = 0; i < Q.length; i++)
    {

      // If query of type 1 found
      if (Q[i][0] == 1)
        updateValue(arr, st, 0, N - 1, Q[i][1] - 1,
                    5, 0);
      else {

        // Stores index of first array element
        // which is greater than or equal
        // to Q[i][1]
        int f = findMinimumIndex(st, 0, N - 1,
                                 Q[i][1], 0);
        if (f < N)
          System.out.print(f + 1 + " ");
        else
          System.out.print(-1 + " ");
      }
    }
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { 1, 3, 2, 4, 6 };

    int[][] Q
      = { { 2, 5 }, { 1, 3, 5 }, { 2, 4 }, { 2, 8 } };
    int N = arr.length;
    PerformQueries(arr, N, Q);
  }
}

// This code is contributed by hemanthsawarna1506
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to find the mid
# of start and end
def getMid(s,e):
    return s + math.floor((e - s) / 2)

def updateValue(arr,st,ss,se,index,value,node):
    # If index is out of range
    if (index < ss or index > se):
      print("Invalid Input")
      return

    # If a leaf node is found
    if (ss == se):
      # update value in array
      arr[index] = value

      # Update value in
      # the segment tree
      st[node] = value
    else:
      # Stores mid of ss and se
      mid = getMid(ss, se)

      # If index is less than or
      # equal to mid
      if (index >= ss and index <= mid):

        # Recursively call for left subtree
        updateValue(arr, st, ss, mid, index, value, 2 * node + 1)
      else:

        # Recursively call for right subtree
        updateValue(arr, st, mid + 1, se, index, value, 2 * node + 2)

      # Update st[node]
      st[node] = max(st[2 * node + 1], st[2 * node + 2])

# Function to find the position of first element
# which is greater than or equal to X
def findMinimumIndex(st, ss, se, K, si):
    # If no such element found in current
    # subtree which is greater than or
    # equal to K
    if (st[si] < K):
      return 1000000000

    # If current node is leaf node
    if (ss == se):
      # If value of current node
      # is greater than or equal to X
      if (st[si] >= K):
        return ss
      return 1000000000

    # Stores mid of ss and se
    mid = getMid(ss, se)

    l = 1000000000

    # If root of left subtree is
    # greater than or equal to K
    if (st[2 * si + 1] >= K):
      l = min(l, findMinimumIndex(st, ss, mid, K, 2 * si + 1))

    # If no such array element is
    # found in the left subtree
    if (l == 1e9 and st[2 * si + 2] >= K):
      l = min(l, findMinimumIndex(st, mid + 1, se, K, 2 * si + 2))

    return l

# Function to build a segment tree
def Build(arr, ss, se, st, si):

    # If current node is leaf node
    if (ss == se):
      st[si] = arr[ss]
      return arr[ss]

    # store mid of ss and se
    mid = getMid(ss, se)

    # Stores maximum of left subtree and rightsubtree
    st[si] = max(Build(arr, ss, mid, st, si * 2 + 1), Build(arr, mid + 1, se, st, si * 2 + 2))

    return st[si]

# Function to initialize a segment tree
# for the given array
def constructST(arr,n):

    # Height of segment tree
    x = math.ceil(math.log(n) / math.log(2))

    # Maximum size of segment tree
    max_size = 2 * pow(2, x) - 1

    # Allocate memory
    st = [0]*(max_size)

    # Fill the allocated memory st
    Build(arr, 0, n - 1, st, 0)

    # Return the constructed segment tree
    return st

def PerformQueries(arr, N, Q):

    # Build segment tree for the given array
    st = constructST(arr, N)

    # Traverse the query array
    for i in range(len(Q)):

      # If query of type 1 found
      if (Q[i][0] == 1):
        updateValue(arr, st, 0, N - 1, Q[i][1] - 1, 5, 0)
      else:
        # Stores index of first array element
        # which is greater than or equal
        # to Q[i][1]
        f = findMinimumIndex(st, 0, N - 1, Q[i][1], 0)
        if (f < N):
          print((f + 1 ), end = " ")
        else:
          print(-1, end = " ")

# Driver code
arr = [1, 3, 2, 4, 6 ]
Q= [[ 2, 5 ], [ 1, 3, 5 ], [2, 4 ], [ 2, 8 ]]
N = len(arr)

PerformQueries(arr, N, Q)

# This code is contributed by decode2207.
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the mid
// of start and end
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

static void updateValue(int[] arr, int[] st, int ss,
                        int se, int index, int value,
                        int node)
{

    // If index is out of range
    if (index < ss || index > se)
    {
        Console.WriteLine("Invalid Input");
        return;
    }

    // If a leaf node is found
    if (ss == se)
    {

        // Update value in array
        arr[index] = value;

        // Update value in
        // the segment tree
        st[node] = value;
    }
    else
    {

        // Stores mid of ss and se
        int mid = getMid(ss, se);

        // If index is less than or
        // equal to mid
        if (index >= ss && index <= mid)
        {

            // Recursively call for left subtree
            updateValue(arr, st, ss, mid, index, value,
                        2 * node + 1);
        }
        else
        {

            // Recursively call for right subtree
            updateValue(arr, st, mid + 1, se, index,
                        value, 2 * node + 2);
        }

        // Update st[node]
        st[node] = Math.Max(st[2 * node + 1],
                            st[2 * node + 2]);
    }
}

// Function to find the position of first element
// which is greater than or equal to X
static int findMinimumIndex(int[] st, int ss, int se,
                            int K, int si)
{

    // If no such element found in current
    // subtree which is greater than or
    // equal to K
    if (st[si] < K)
        return 1000000000;

    // If current node is leaf node
    if (ss == se)
    {

        // If value of current node
        // is greater than or equal to X
        if (st[si] >= K)
        {
            return ss;
        }
        return 1000000000;
    }

    // Stores mid of ss and se
    int mid = getMid(ss, se);

    int l = 1000000000;

    // If root of left subtree is
    // greater than or equal to K
    if (st[2 * si + 1] >= K)
        l = Math.Min(l, findMinimumIndex(st, ss, mid, K,
                                         2 * si + 1));

    // If no such array element is
    // found in the left subtree
    if (l == 1e9 && st[2 * si + 2] >= K)
        l = Math.Min(l,
                     findMinimumIndex(st, mid + 1, se,
                                    K, 2 * si + 2));

    return l;
}

// Function to build a segment tree
static int Build(int[] arr, int ss, int se,
                 int[] st, int si)
{

    // If current node is leaf node
    if (ss == se)
    {
        st[si] = arr[ss];
        return arr[ss];
    }

    // Store mid of ss and se
    int mid = getMid(ss, se);

    // Stores maximum of left subtree and rightsubtree
    st[si] = Math.Max(
        Build(arr, ss, mid, st, si * 2 + 1),
        Build(arr, mid + 1, se, st, si * 2 + 2));

    return st[si];
}

// Function to initialize a segment tree
// for the given array
static int[] constructST(int[] arr, int n)
{

    // Height of segment tree
    int x = (int)Math.Ceiling(Math.Log(n) /
                              Math.Log(2));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.Pow(2, x) - 1;

    // Allocate memory
    int[] st = new int[max_size];

    // Fill the allocated memory st
    Build(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

static void PerformQueries(int[] arr, int N, int[][] Q)
{

    // Build segment tree for the given array
    int[] st = constructST(arr, N);

    // Traverse the query array
    for(int i = 0; i < Q.Length; i++)
    {

        // If query of type 1 found
        if (Q[i][0] == 1)
            updateValue(arr, st, 0, N - 1,
                        Q[i][1] - 1, 5, 0);
        else
        {

            // Stores index of first array element
            // which is greater than or equal
            // to Q[i][1]
            int f = findMinimumIndex(st, 0, N - 1,
                                     Q[i][1], 0);
            if (f < N)
                Console.Write(f + 1 + " ");
            else
                Console.Write(-1 + " ");
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 3, 2, 4, 6 };
    int[][] Q = new int[4][];

    // Initialize the elements
    Q[0] = new int[] { 2, 5 };
    Q[1] = new int[] { 1, 3, 5 };
    Q[2] = new int[] { 2, 4 };
    Q[3] = new int[] { 2, 8 };

    int N = arr.Length;
    PerformQueries(arr, N, Q);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the mid
// of start and end
function getMid(s,e)
{
    return s + Math.floor((e - s) / 2);
}

function updateValue(arr,st,ss,se,index,value,node)
{
    // If index is out of range
    if (index < ss || index > se)
    {
      document.write("Invalid Input<br>");
      return;
    }

    // If a leaf node is found
    if (ss == se)
    {

      // update value in array
      arr[index] = value;

      // Update value in
      // the segment tree
      st[node] = value;
    }
    else
    {

      // Stores mid of ss and se
      let mid = getMid(ss, se);

      // If index is less than or
      // equal to mid
      if (index >= ss && index <= mid)
      {

        // Recursively call for left subtree
        updateValue(arr, st, ss, mid, index, value,
                    2 * node + 1);
      }
      else
      {

        // Recursively call for right subtree
        updateValue(arr, st, mid + 1, se, index,
                    value, 2 * node + 2);
      }

      // Update st[node]
      st[node] = Math.max(st[2 * node + 1],
                          st[2 * node + 2]);
    }
}

// Function to find the position of first element
// which is greater than or equal to X
function findMinimumIndex(st,ss,se,K,si)
{
    // If no such element found in current
    // subtree which is greater than or
    // equal to K
    if (st[si] < K)
      return 1000000000;

    // If current node is leaf node
    if (ss == se)
    {

      // If value of current node
      // is greater than or equal to X
      if (st[si] >= K)
      {
        return ss;
      }
      return 1000000000;
    }

    // Stores mid of ss and se
    let mid = getMid(ss, se);

    let l = 1000000000;

    // If root of left subtree is
    // greater than or equal to K
    if (st[2 * si + 1] >= K)
      l = Math.min(l, findMinimumIndex(st, ss, mid, K,
                                       2 * si + 1));

    // If no such array element is
    // found in the left subtree
    if (l == 1e9 && st[2 * si + 2] >= K)
      l = Math.min(l,
                   findMinimumIndex(st, mid + 1, se,
                                    K, 2 * si + 2));

    return l;
}

// Function to build a segment tree
function Build(arr,ss,se,st,si)
{
    // If current node is leaf node
    if (ss == se)
    {
      st[si] = arr[ss];
      return arr[ss];
    }

    // store mid of ss and se
    let mid = getMid(ss, se);

    // Stores maximum of left subtree and rightsubtree
    st[si] = Math.max(
      Build(arr, ss, mid, st, si * 2 + 1),
      Build(arr, mid + 1, se, st, si * 2 + 2));

    return st[si];
}

// Function to initialize a segment tree
  // for the given array
function constructST(arr,n)
{
    // Height of segment tree
    let x = Math.ceil(Math.log(n) / Math.log(2));

    // Maximum size of segment tree
    let max_size = 2 * Math.pow(2, x) - 1;

    // Allocate memory
    let st = new Array(max_size);

    // Fill the allocated memory st
    Build(arr, 0, n - 1, st, 0);

    // Return the constructed segment tree
    return st;
}

function PerformQueries(arr,N,Q)
{
    // Build segment tree for the given array
    let st = constructST(arr, N);

    // Traverse the query array
    for (let i = 0; i < Q.length; i++)
    {

      // If query of type 1 found
      if (Q[i][0] == 1)
        updateValue(arr, st, 0, N - 1, Q[i][1] - 1,
                    5, 0);
      else {

        // Stores index of first array element
        // which is greater than or equal
        // to Q[i][1]
        let f = findMinimumIndex(st, 0, N - 1,
                                 Q[i][1], 0);
        if (f < N)
          document.write((f + 1 )+ " ");
        else
          document.write(-1 + " ");
      }
    }
}

// Driver Code
let arr=[1, 3, 2, 4, 6 ];
let Q= [[ 2, 5 ], [ 1, 3, 5 ], [2, 4 ], [ 2, 8 ]];
let N = arr.length;
PerformQueries(arr, N, Q);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
5 3 -1 
```