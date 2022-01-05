# 查找给定查询中每个元素所属的数组以及元素计数

> 原文:[https://www . geeksforgeeks . org/find-给定查询中每个元素所属的数组以及元素计数/](https://www.geeksforgeeks.org/find-the-array-to-which-each-element-in-given-queries-belong-along-with-count-of-elements/)

给定长度为 **N** 的成对**arr【】【】**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，以及长度为 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **查询【】**，以及整数 **R** ，其中每个**查询**包含从 **1** 到 **R** 的整数，每个**查询【I】**的任务是查找

> **注:**最初从 **1** 到 **R** 的每个整数都属于不同的集合。

**示例:**

> **输入:** R = 5，arr[] = {{1，2}，{2，3}，{4，5}}，查询[] = {2，4，1，3}
> T3】输出:3 2 3
> T6】解释:T8】从 arr[]对制作集合后，{1，2，3}，{4，5}
> 对于第一个查询:2 属于集合{1，2，3 }，元素总数为 3
> 对于第二个查询:4 属于集合{4，5}，元素总数为 2。
> 对于第三个查询:1 属于集合{1，2，3}，元素总数为 3。
> 对于第四个查询:3 属于集合{1，2，3}，元素总数为 3。
> 
> **输入:** R = 6，arr[] = {{1，3}，{2，4}}，查询[] = {2，5，6，1}
> **输出:** 2 1 1 2

**方法:**给定的问题可以使用[不相交集合并](https://www.geeksforgeeks.org/union-find/)来解决。最初，所有元素都在不同的集合中，处理 **arr[]** 并对给定的对执行[联合操作](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)，在联合更新中，父元素的 **total[]** 值。对于每个查询执行[查找操作](https://www.geeksforgeeks.org/union-find/)，对于返回的父元素，查找当前集合的大小作为**总【父】**的值。按照以下步骤解决问题:

*   [初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **父级(R + 1)** 、**秩(R + 1，0)** 、**总计(R + 1，1)** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，R+1】**，并将**父项【I】**的值设置为 **I** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**，并执行联合操作为**联合(父级，等级，总计，arr[I]。首先，逮捕[我]。第二)**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，M–1】**，并执行以下步骤:
    *   调用[函数](https://www.geeksforgeeks.org/functions-in-c/)查找当前元素的父元素**查询【我】**为**查找(父元素，查询【我】)**。
    *   将**总计【I】**的值打印为当前集的大小。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the find operation
// of disjoint set union
int Find(vector<int>& parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(parent, parent[a]));
}

// Function to find the Union operation
// of disjoint set union
void Union(vector<int>& parent,
           vector<int>& rank,
           vector<int>& total,
           int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Update the parent for node b
    parent[b] = a;

    // Update the total number of
    // elements of a
    total[a] += total[b];
}

// Function to find the total element
// of the set which belongs to the
// element queries[i]
void findTotNumOfSet(vector<pair<int, int> >& arr,
                     vector<int>& queries,
                     int R, int N, int M)
{

    // Stores the parent elements
    // of the sets
    vector<int> parent(R + 1);

    // Stores the rank of the sets
    vector<int> rank(R + 1, 0);

    // Stores the total number of
    // elements of the sets
    vector<int> total(R + 1, 1);

    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add the arr[i].first and
        // arr[i].second elements to
        // the same set
        Union(parent, rank, total,
              arr[i].first,
              arr[i].second);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the total elements of
        // the set which belongs to P
        cout << total[P] << " ";
    }
}

// Driver Code
int main()
{
    int R = 5;
    vector<pair<int, int> > arr{ { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    vector<int> queries{ 2, 4, 1, 3 };
    int N = arr.size();
    int M = queries.size();

    findTotNumOfSet(arr, queries, R, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to perform the find operation
// of disjoint set union
static int Find(int [] parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(parent, parent[a]));
}

// Function to find the Union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] total,
           int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Update the parent for node b
    parent[b] = a;

    // Update the total number of
    // elements of a
    total[a] += total[b];
}

// Function to find the total element
// of the set which belongs to the
// element queries[i]
static void findTotNumOfSet(int[][] arr,
                     int [] queries,
                     int R, int N, int M)
{

    // Stores the parent elements
    // of the sets
    int [] parent = new int[R + 1];

    // Stores the rank of the sets
    int [] rank = new int[R + 1];

    // Stores the total number of
    // elements of the sets
    int [] total = new int[R + 1];
    for (int i = 0; i < total.length; i++) {
        total[i] = 1;
    }
    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add the arr[i][0] and
        // arr[i][1] elements to
        // the same set
        Union(parent, rank, total,
              arr[i][0],
              arr[i][1]);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the total elements of
        // the set which belongs to P
        System.out.print(total[P]+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int R = 5;
    int[][]  arr = { { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    int [] queries = { 2, 4, 1, 3 };
    int N = arr.length;
    int M = queries.length;

    findTotNumOfSet(arr, queries, R, N, M);

}
}

// This code is contributed by 29AjayKumar.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to perform the find operation
# of disjoint set union
def Find(parent, a):
    if (parent[a] == a):
        return a
    else:
        return Find(parent, parent[a])

# Function to find the Union operation
# of disjoint set union
def Union(parent, rank, total, a, b):

    # Find the parent of a and b
    a = Find(parent, a)
    b = Find(parent, b)
    if(a == b):
        return

    # If the rank are the same
    if(rank[a] == rank[b]):
        rank[a] += 1
    if(rank[a] < rank[b]):
        temp = a
        a = b
        b = temp

    # Update the parent for node b
    parent[b] = a

    # Update the total number of
    # elements of a
    total[a] += total[b]

# Function to find the total element
# of the set which belongs to the
# element queries[i]
def findTotNumOfSet(arr, queries, R, N, M):

    # Stores the parent elements
    # of the sets
    parent = [None]*(R+1)

    # Stores the rank of the sets
    rank = [0]*(R+1)

    # Stores the total number of
    # elements of the sets
    total = [1]*(R + 1)
    for i in range(1, R + 1):

        # Add the arr[i].first and
        # arr[i].second elements to
        # the same set
        parent[i] = i
    for i in range(N):
        Union(parent, rank, total, arr[i][0], arr[i][1])
    for i in range(M):

        # Find the parent element of
        # the element queries[i]
        P = Find(parent, queries[i])

        # Print the total elements of
        # the set which belongs to P
        print(total[P], end=" ")

# Driver code
R = 5
arr = [[1, 2], [2, 3], [4, 5]]
queries = [2, 4, 1, 3]
N = len(arr)
M = len(queries)
findTotNumOfSet(arr, queries, R, N, M)

# This code is contributed by parthmanchanda81
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to perform the find operation
// of disjoint set union
static int Find(int [] parent, int a)
{
    return parent[a]
           = (parent[a] == a)
                 ? a
                 : (Find(parent, parent[a]));
}

// Function to find the Union operation
// of disjoint set union
static void Union(int [] parent,
           int [] rank,
           int [] total,
           int a, int b)
{
    // Find the parent of a and b
    a = Find(parent, a);
    b = Find(parent, b);

    if (a == b)
        return;

    // If the rank are the same
    if (rank[a] == rank[b]) {
        rank[a]++;
    }

    if (rank[a] < rank[b]) {
        int temp = a;
        a = b;
        b = temp;
    }

    // Update the parent for node b
    parent[b] = a;

    // Update the total number of
    // elements of a
    total[a] += total[b];
}

// Function to find the total element
// of the set which belongs to the
// element queries[i]
static void findTotNumOfSet(int[,] arr,
                     int [] queries,
                     int R, int N, int M)
{

    // Stores the parent elements
    // of the sets
    int [] parent = new int[R + 1];

    // Stores the rank of the sets
    int [] rank = new int[R + 1];

    // Stores the total number of
    // elements of the sets
    int [] total = new int[R + 1];
    for (int i = 0; i < total.Length; i++) {
        total[i] = 1;
    }
    for (int i = 1; i < R + 1; i++) {

        // Update parent[i] to i
        parent[i] = i;
    }

    for (int i = 0; i < N; i++) {

        // Add the arr[i,0] and
        // arr[i,1] elements to
        // the same set
        Union(parent, rank, total,
              arr[i,0],
              arr[i,1]);
    }

    for (int i = 0; i < M; i++) {

        // Find the parent element of
        // the element queries[i]
        int P = Find(parent, queries[i]);

        // Print the total elements of
        // the set which belongs to P
        Console.Write(total[P]+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int R = 5;
    int[,]  arr = { { 1, 2 },
                                 { 2, 3 },
                                 { 4, 5 } };
    int [] queries = { 2, 4, 1, 3 };
    int N = arr.GetLength(0);
    int M = queries.GetLength(0);

    findTotNumOfSet(arr, queries, R, N, M);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to perform the find operation
// of disjoint set union
function Find(parent, a)
{
  return (parent[a] = parent[a] == a ? a : Find(parent, parent[a]));
}

// Function to find the Union operation
// of disjoint set union
function Union(parent, rank, total, a, b)
{

  // Find the parent of a and b
  a = Find(parent, a);
  b = Find(parent, b);

  if (a == b) return;

  // If the rank are the same
  if (rank[a] == rank[b]) {
    rank[a]++;
  }

  if (rank[a] < rank[b]) {
    let temp = a;
    a = b;
    b = temp;
  }

  // Update the parent for node b
  parent[b] = a;

  // Update the total number of
  // elements of a
  total[a] += total[b];
}

// Function to find the total element
// of the set which belongs to the
// element queries[i]
function findTotNumOfSet(arr, queries, R, N, M)
{

  // Stores the parent elements
  // of the sets
  let parent = new Array(R + 1);

  // Stores the rank of the sets
  let rank = new Array(R + 1).fill(0);

  // Stores the total number of
  // elements of the sets
  let total = new Array(R + 1).fill(1);

  for (let i = 1; i < R + 1; i++)
  {

    // Update parent[i] to i
    parent[i] = i;
  }

  for (let i = 0; i < N; i++)
  {

    // Add the arr[i].first and
    // arr[i].second elements to
    // the same set
    Union(parent, rank, total, arr[i][0], arr[i][1]);
  }

  for (let i = 0; i < M; i++)
  {

    // Find the parent element of
    // the element queries[i]
    let P = Find(parent, queries[i]);

    // Print the total elements of
    // the set which belongs to P
    document.write(total[P] + " ");
  }
}

// Driver Code
let R = 5;
let arr = [
  [1, 2],
  [2, 3],
  [4, 5],
];
let queries = [2, 4, 1, 3];
let N = arr.length;
let M = queries.length;

findTotNumOfSet(arr, queries, R, N, M);

// This code is ontributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
3 2 3 3
```

***时间复杂度:**O(M * log R)*
T5**辅助空间:** O(R)