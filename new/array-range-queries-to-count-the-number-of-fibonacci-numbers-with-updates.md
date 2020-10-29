# 数组范围查询，用于统计具有更新的斐波纳契数的数量

> 原文：[https://www.geeksforgeeks.org/array-range-queries-to-count-the-number-of-fibonacci-numbers-with-updates/](https://www.geeksforgeeks.org/array-range-queries-to-count-the-number-of-fibonacci-numbers-with-updates/)

给定 **N** 个整数的数组 **arr []** ，任务是执行以下两个查询：

*   **查询（开始，结束）**：从头到尾打印子数组中的斐波那契数

*   **update（i，x）**：将 x 添加到数组索引 **i** 引用的数组元素中，即：arr [i] = x

**示例**：

> **输入**：arr = {1，2，3，4，8，9}
> 查询 1：查询（开始= 0，结束= 4）
> 查询 2：更新（i = 3 ，x = 5）
> 查询 3：查询（开始= 0，结束= 4）
> **输出**：4
> 5
> **说明**
> 在**查询 1** 中，子数组[0…4]具有 **4** 斐波那契数即。 {1、2、3、8}
> 在**查询 2** 中，索引 3 的值更新为 5，数组 arr 现在为{1、2、3、5、8、9 }
> 在**查询 3** 中，子数组[0…4]具有 **5** 斐波那契数。 {1,2,3,5,8}

**方法**：为了处理点更新和范围查询，为此目的，[段树](http://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)是最佳的。

为了检查[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，我们可以使用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)来构建[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于最大值 arr [ <sub>i</sub> 。 我们可以采用 MAX 来测试 O（1）时间复杂度的数字。

**构建细分树**：

*   现在，使用段树问题将问题简化为[子数组总和。](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)

*   现在，我们可以构建分段树，其中叶节点表示为 0（如果不是素数）或 1（如果是斐波那契数）。

*   段树的内部节点等于其子节点的总和，因此，一个节点表示从 L 到 R 的范围内的总斐波那契数，范围[L，R]落在该节点下面，并且在其下面是子树。

**处理查询和积分更新**：

*   每当我们收到从头到尾的查询时，我们都可以在段树中查询从头到尾的范围内的节点总数，这又表示从头到尾的范围内的斐波那契数。

*   To perform a point update and to update the value at index i to x, we check for the following cases:

    假设 arr <sub>i</sub> 的旧值为 y，新值为 x。

    1.  **情况 1：斐波那契：如果 x 和 y 都是斐波那契数**

        子数组中斐波那契数的数量不变，因此我们只更新数组而不修改段树

    2.  **情况 2：如果 x 和 y 都不是斐波那契数**

        子数组中斐波那契数的计数不变，因此我们只更新数组而不修改段树

    3.  **情况 3：如果 y 是斐波那契数而不是 x**

        子数组中斐波那契数的计数减少，因此我们更新数组并将-1 添加到每个范围。 要更新的索引 i 是分段树的一部分

    4.  **情况 4：如果 y 不是斐波那契数，而 x 是斐波那契数**

        子数组中斐波那契数的计数增加，因此我们更新数组并将其添加到每个范围。 要更新的索引 i 是分段树的一部分

下面是上述方法的实现：

```
// C++ program to find number of fibonacci numbers
// in a subarray and performing updates
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000
// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
int maxElement)
{
int prev = 0, curr = 1;
hash.insert(prev);
hash.insert(curr);
while (curr <= maxElement) {
int temp = curr + prev;
hash.insert(temp);
prev = curr;
curr = temp;
}
}
// A utility function to get the middle
// index from corner indexes.
int getMid(int s, int e)
{
return s + (e - s) / 2;
}
// Recursive function to get the number
// of Fibonacci numbers in a given range
/* where
st    --> Pointer to segment tree
index --> Index of current node in the
segment tree. Initially 0 is passed
as root is always at index 0
ss & se  --> Starting and ending indexes of
the segment represented by current
node, i.e., st[index]
qs & qe  --> Starting and ending indexes
of query range
*/
int queryFibonacciUtil(int* st, int ss,
int se, int qs,
int qe, int index)
{
// If segment of this node is a part
// of given range, then return
// the number of Fibonacci numbers
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
return queryFibonacciUtil(st, ss, mid, qs,
qe, 2 * index + 1)
+ queryFibonacciUtil(st, mid + 1, se,
qs, qe, 2 * index + 2);
}
// Recursive function to update
// the nodes which have the given
// index in their range.
/* where
st, si, ss and se are same as getSumUtil()
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
int new_val,
set<int> hash)
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
// both are Fibonacci numbers
if (hash.find(oldValue) != hash.end()
&& hash.find(new_val) != hash.end())
return;
// Case 2: Old and new values
// both not Fibonacci numbers
if (hash.find(oldValue) == hash.end()
&& hash.find(new_val) == hash.end())
return;
// Case 3: Old value was Fibonacci,
// new value is non Fibonacci
if (hash.find(oldValue) != hash.end()
&& hash.find(new_val) == hash.end()) {
diff = -1;
}
// Case 4: Old value was non Fibonacci,
// new_val is Fibonacci
if (hash.find(oldValue) == hash.end()
&& hash.find(new_val) != hash.end()) {
diff = 1;
}
// Update the values of nodes in segment tree
updateValueUtil(st, 0, n - 1, i, diff, 0);
}
// Return number of Fibonacci numbers
// in range from index qs (query start)
// to qe (query end).
// It mainly uses queryFibonacciUtil()
void queryFibonacci(int* st, int n,
int qs, int qe)
{
int FibonacciInRange
= queryFibonacciUtil(st, 0, n - 1,
qs, qe, 0);
cout << "Number of Fibonacci numbers "
<< "in subarray from "
<< qs << " to "
<< qe << " = "
<< FibonacciInRange << "\n";
}
// Recursive function that constructs
// Segment Tree for array[ss..se].
// si is index of current node
// in segment tree st
int constructSTUtil(int arr[], int ss,
int se, int* st,
int si, set<int> hash)
{
// If there is one element in array,
// check if it is Fibonacci number
// then store 1 in the segment tree
// else store 0 and return
if (ss == se) {
// if arr[ss] is fibonacci number
if (hash.find(arr[ss]) != hash.end())
st[si] = 1;
else
st[si] = 0;
return st[si];
}
// If there are more than one elements,
// then recur for left and right subtrees
// and store the sum of the
// two values in this node
int mid = getMid(ss, se);
st[si] = constructSTUtil(arr, ss, mid, st,
si * 2 + 1, hash)
+ constructSTUtil(arr, mid + 1, se, st,
si * 2 + 2, hash);
return st[si];
}
// Function to construct a segment tree from given array.
// This function allocates memory for segment tree and
// calls constructSTUtil() to fill the allocated memory
int* constructST(int arr[], int n, set<int> hash)
{
// Allocate memory for segment tree
// Height of segment tree
int x = (int)(ceil(log2(n)));
// Maximum size of segment tree
int max_size = 2 * (int)pow(2, x) - 1;
int* st = new int[max_size];
// Fill the allocated memory st
constructSTUtil(arr, 0, n - 1, st, 0, hash);
// Return the constructed segment tree
return st;
}
// Driver Code
int main()
{
int arr[] = { 1, 2, 3, 4, 8, 9 };
int n = sizeof(arr) / sizeof(arr[0]);
// find the largest node value in the array
int maxEle = *max_element(arr, arr + n);
// Creating a set containing all Fibonacci numbers
// upto the maximum data value in the array
set<int> hash;
createHash(hash, maxEle);
// Build segment tree from given array
int* st = constructST(arr, n, hash);
// Query 1: Query(start = 0, end = 4)
int start = 0;
int end = 4;
queryFibonacci(st, n, start, end);
// Query 2: Update(i = 3, x = 5),
// i.e Update a[i] to x
int i = 3;
int x = 5;
updateValue(arr, st, n, i, x, hash);
// uncomment to see array after update
// for(int i = 0; i < n; i++)
// cout << arr[i] << " ";
// Query 3: Query(start = 0, end = 4)
start = 0;
end = 4;
queryFibonacci(st, n, start, end);
return 0;
}
```

**Output:**

```
Number of Fibonacci numbers in subarray from 0 to 4 = 4
Number of Fibonacci numbers in subarray from 0 to 4 = 5

```

**时间复杂度**：每个查询和更新的时间复杂度为 **O（log n）**，构建段树的时间复杂度为 **`O(n)`**

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



