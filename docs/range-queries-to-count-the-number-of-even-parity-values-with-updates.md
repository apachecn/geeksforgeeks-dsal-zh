# 范围查询，通过更新计算偶校验值的数量

> 原文:[https://www . geesforgeks . org/range-query-to-count-number-of-even-奇偶校验-values-with-updates/](https://www.geeksforgeeks.org/range-queries-to-count-the-number-of-even-parity-values-with-updates/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是执行以下两个查询:

*   **查询(L，R)** :打印从 L 到 R 的子阵中偶数奇偶数的个数
*   **更新(I，x)** :通过索引 **i** 更新数组元素引用到 x。

**示例:**

> **输入:** arr[] = {18，15，8，9，14，5}
> 查询 1:查询(L = 0，R = 4)
> 查询 2:更新(i = 3，x = 11)
> 查询 3:查询(L = 0，R = 4)
> **输出:**
> 3
> 2
> **解释:**
> **查询 1:** 斯巴莱是{ 10 奇偶性= 2
> 15 = > 1111，奇偶性= 4
> 8 = > 1000，奇偶性= 1
> 9 = > 1001，奇偶性= 2
> 14 = > 1110，奇偶性= 3
> 子阵列[0-4]具有偶奇偶性的 **3** 元素。
> **查询 2:** 更新 arr[3] = 11
> 更新数组，{18，15，8，11，14，5}
> **查询 3:** 子数组是{18，15，8，11，14}
> 这些元素的二进制表示–
> 18 =>10010，奇偶性= 2
> 15 = > 111，奇偶性= 1

**方法:**思路是用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)查询数组范围内偶校验元素的个数，同时更新。
我们可以通过迭代数字的二进制表示的每一位并计算设置位的数量来找到当前值的奇偶校验。然后检查奇偶校验是否为偶数。如果它具有偶数奇偶校验，则将它设置为 1 或 0。

**构建段树:**

*   段树的叶节点表示为 0(如果是奇数奇偶数)或 1(如果是偶数奇偶数)。
*   段树的内部节点等于其子节点的总和，因此一个节点代表从 L 到 R 范围内的偶数总数，范围[L，R]落在该节点及其下的子树下。

**处理查询:**

*   **查询(L，R):** 每当我们从开始到结束收到一个查询时，我们可以在段树中查询从开始到结束的范围内的节点的总和，这又表示从开始到结束的范围内的偶数奇偶数的数量。
*   **更新(I，x):** 要执行更新查询以将索引 I 处的值更新为 x，我们检查以下情况:
    *   **情况 1:** 如果前一个值和新值都是偶校验数
        子阵列中偶校验数的计数不变，所以我们只更新数组，不修改段树
    *   **情况 2:** 如果前一个值和新值都不是偶校验数
        子阵中偶校验数的计数不变，所以我们只更新数组，不修改段树
    *   **情况 3:** 如果前一个值是偶校验数，但新值不是偶校验数
        子阵列中偶校验数的计数减少，因此我们更新数组并在每个范围内加-1。要更新的索引 I 是段树中的一部分
    *   **情况 4:** 如果前一个值不是偶校验数，但新值是偶校验数
        子阵列中偶校验数的计数增加，因此我们更新数组并在每个范围内增加 1。要更新的索引 I 是段树中的一部分

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// number of Even Parity numbers
// in a subarray and performing updates

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000

// Function that returns true if count
// of set bits in x is even
bool isEvenParity(int x)
{
    // parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// A utility function to get
// the middle index
int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to get the number
// of Even Parity numbers in a given range
int queryEvenParityUtil(
    int* segmentTree, int segmentStart,
    int segmentEnd, int queryStart,
    int queryEnd, int index)
{
    // If segment of this node is a part
    // of given range, then return
    // the number of Even Parity numbers
    // in the segment
    if (queryStart <= segmentStart
        && queryEnd >= segmentEnd)
        return segmentTree[index];

    // If segment of this node
    // is outside the given range
    if (segmentEnd < queryStart
        || segmentStart > queryEnd)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(segmentStart, segmentEnd);
    return queryEvenParityUtil(
               segmentTree, segmentStart, mid,
               queryStart, queryEnd, 2 * index + 1)
           + queryEvenParityUtil(
                 segmentTree, mid + 1, segmentEnd,
                 queryStart, queryEnd, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range
void updateValueUtil(
    int* segmentTree, int segmentStart,
    int segmentEnd, int i, int diff, int si)
{
    // Base Case:
    if (i < segmentStart || i > segmentEnd)
        return;

    // If the input index is in range
    // of this node, then update the value
    // of the node and its children
    segmentTree[si] = segmentTree[si] + diff;
    if (segmentEnd != segmentStart) {

        int mid = getMid(
            segmentStart, segmentEnd);
        updateValueUtil(
            segmentTree, segmentStart,
            mid, i, diff, 2 * si + 1);
        updateValueUtil(
            segmentTree, mid + 1, segmentEnd,
            i, diff, 2 * si + 2);
    }
}

// Function to update a value in the
// input array and segment tree
void updateValue(int arr[], int* segmentTree,
                 int n, int i, int new_val)
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
    // both are Even Parity numbers
    if (isEvenParity(oldValue)
        && isEvenParity(new_val))
        return;

    // Case 2: Old and new values
    // both not Even Parity numbers
    if (!isEvenParity(oldValue)
        && !isEvenParity(new_val))
        return;

    // Case 3: Old value was Even Parity,
    // new value is non Even Parity
    if (isEvenParity(oldValue)
        && !isEvenParity(new_val)) {
        diff = -1;
    }

    // Case 4: Old value was non Even Parity,
    // new_val is Even Parity
    if (!isEvenParity(oldValue)
        && !isEvenParity(new_val)) {
        diff = 1;
    }

    // Update the values of
    // nodes in segment tree
    updateValueUtil(segmentTree, 0,
                    n - 1, i, diff, 0);
}

// Return number of Even Parity numbers
void queryEvenParity(int* segmentTree,
                     int n, int queryStart,
                     int queryEnd)
{
    int EvenParityInRange
        = queryEvenParityUtil(
            segmentTree, 0, n - 1,
            queryStart, queryEnd, 0);

    cout << EvenParityInRange << "\n";
}

// Recursive function that constructs
// Segment Tree for the given array
int constructSTUtil(int arr[],
                    int segmentStart,
                    int segmentEnd,
                    int* segmentTree,
                    int si)
{
    // If there is one element in array,
    // check if it is Even Parity number
    // then store 1 in the segment tree
    // else store 0 and return
    if (segmentStart == segmentEnd) {

        // if arr[segmentStart] is
        // Even Parity number
        if (isEvenParity(arr[segmentStart]))
            segmentTree[si] = 1;
        else
            segmentTree[si] = 0;

        return segmentTree[si];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the
    // two values in this node
    int mid = getMid(segmentStart,
                     segmentEnd);
    segmentTree[si]
        = constructSTUtil(
              arr, segmentStart, mid,
              segmentTree, si * 2 + 1)
          + constructSTUtil(
                arr, mid + 1, segmentEnd,
                segmentTree, si * 2 + 2);
    return segmentTree[si];
}

// Function to construct a segment
// tree from given array
int* constructST(int arr[], int n)
{
    // Height of segment tree
    int x = (int)(ceil(log2(n)));

    // Maximum size of segment tree
    int max_size = 2 * (int)pow(2, x) - 1;

    int* segmentTree = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1,
                    segmentTree, 0);

    // Return the constructed segment tree
    return segmentTree;
}

// Driver Code
int main()
{

    int arr[] = { 18, 15, 8, 9, 14, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    int* segmentTree = constructST(arr, n);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryEvenParity(segmentTree, n, start, end);

    // Query 2: Update(i = 3, x = 11),
    // i.e Update a[i] to x
    int i = 3;
    int x = 11;
    updateValue(arr, segmentTree, n, i, x);

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryEvenParity(
        segmentTree, n, start, end);

    return 0;
}
```

## C#

```
// C# implementation to find
// number of Even Parity numbers
// in a subarray and performing updates
using System;

class GFG{

public static int MAX = 1000;

// Function that returns true if count
// of set bits in x is even
static bool isEvenParity(int x)
{

    // parity will store the
    // count of set bits
    int parity = 0;

    while (x != 0)
    {
        if ((x & 1) != 0)
            parity++;

        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// A utility function to get
// the middle index
static int getMid(int s, int e)
{
    return s + (e - s) / 2;
}

// Recursive function to get the number
// of Even Parity numbers in a given range
static int queryEvenParityUtil(int[] segmentTree,
                               int segmentStart,
                               int segmentEnd,
                               int queryStart,
                               int queryEnd, int index)
{

    // If segment of this node is a part
    // of given range, then return
    // the number of Even Parity numbers
    // in the segment
    if (queryStart <= segmentStart &&
        queryEnd >= segmentEnd)
        return segmentTree[index];

    // If segment of this node
    // is outside the given range
    if (segmentEnd < queryStart ||
        segmentStart > queryEnd)
        return 0;

    // If a part of this segment
    // overlaps with the given range
    int mid = getMid(segmentStart, segmentEnd);
    return queryEvenParityUtil(segmentTree, segmentStart,
                               mid, queryStart, queryEnd,
                               2 * index + 1) +
           queryEvenParityUtil(segmentTree, mid + 1,
                               segmentEnd, queryStart,
                               queryEnd, 2 * index + 2);
}

// Recursive function to update
// the nodes which have the given
// index in their range
static void updateValueUtil(int[] segmentTree,
                            int segmentStart,
                            int segmentEnd, int i,
                            int diff, int si)
{

    // Base Case:
    if (i < segmentStart || i > segmentEnd)
        return;

    // If the input index is in range
    // of this node, then update the value
    // of the node and its children
    segmentTree[si] = segmentTree[si] + diff;

    if (segmentEnd != segmentStart)
    {
        int mid = getMid(segmentStart, segmentEnd);
        updateValueUtil(segmentTree, segmentStart, mid,
                        i, diff, 2 * si + 1);
        updateValueUtil(segmentTree, mid + 1,
                        segmentEnd, i, diff,
                        2 * si + 2);
    }
}

// Function to update a value in the
// input array and segment tree
static void updateValue(int[] arr, int[] segmentTree,
                        int n, int i, int new_val)
{

    // Check for erroneous input index
    if (i < 0 || i > n - 1)
    {
        Console.WriteLine("Invalid Input");
        return;
    }

    int diff = 0, oldValue = 0;

    oldValue = arr[i];

    // Update the value in array
    arr[i] = new_val;

    // Case 1: Old and new values
    // both are Even Parity numbers
    if (isEvenParity(oldValue) &&
        isEvenParity(new_val))
        return;

    // Case 2: Old and new values
    // both not Even Parity numbers
    if (!isEvenParity(oldValue) &&
        !isEvenParity(new_val))
        return;

    // Case 3: Old value was Even Parity,
    // new value is non Even Parity
    if (isEvenParity(oldValue) &&
       !isEvenParity(new_val))
    {
        diff = -1;
    }

    // Case 4: Old value was non Even Parity,
    // new_val is Even Parity
    if (!isEvenParity(oldValue) &&
        !isEvenParity(new_val))
    {
        diff = 1;
    }

    // Update the values of
    // nodes in segment tree
    updateValueUtil(segmentTree, 0, n - 1, i, diff, 0);
}

// Return number of Even Parity numbers
static void queryEvenParity(int[] segmentTree, int n,
                            int queryStart,
                            int queryEnd)
{
    int EvenParityInRange = queryEvenParityUtil(
        segmentTree, 0, n - 1, queryStart, queryEnd, 0);

    Console.WriteLine(EvenParityInRange);
}

// Recursive function that constructs
// Segment Tree for the given array
static int constructSTUtil(int[] arr, int segmentStart,
                           int segmentEnd,
                           int[] segmentTree, int si)
{

    // If there is one element in array,
    // check if it is Even Parity number
    // then store 1 in the segment tree
    // else store 0 and return
    if (segmentStart == segmentEnd)
    {

        // if arr[segmentStart] is
        // Even Parity number
        if (isEvenParity(arr[segmentStart]))
            segmentTree[si] = 1;
        else
            segmentTree[si] = 0;

        return segmentTree[si];
    }

    // If there are more than one elements,
    // then recur for left and right subtrees
    // and store the sum of the
    // two values in this node
    int mid = getMid(segmentStart, segmentEnd);
    segmentTree[si] = constructSTUtil(arr, segmentStart, mid,
                                      segmentTree, si * 2 + 1) +
                      constructSTUtil(arr, mid + 1, segmentEnd,
                                      segmentTree, si * 2 + 2);
    return segmentTree[si];
}

// Function to construct a segment
// tree from given array
static int[] constructST(int[] arr, int n)
{

    // Height of segment tree
    int x = (int)(Math.Ceiling(Math.Log(n, 2)));

    // Maximum size of segment tree
    int max_size = 2 * (int)Math.Pow(2, x) - 1;

    int[] segmentTree = new int[max_size];

    // Fill the allocated memory st
    constructSTUtil(arr, 0, n - 1, segmentTree, 0);

    // Return the constructed segment tree
    return segmentTree;
}

// Driver Code
public static void Main()
{
    int[] arr = { 18, 15, 8, 9, 14, 5 };
    int n = arr.Length;

    // Build segment tree from given array
    int[] segmentTree = constructST(arr, n);

    // Query 1: Query(start = 0, end = 4)
    int start = 0;
    int end = 4;
    queryEvenParity(segmentTree, n, start, end);

    // Query 2: Update(i = 3, x = 11),
    // i.e Update a[i] to x
    int i = 3;
    int x = 11;
    updateValue(arr, segmentTree, n, i, x);

    // Query 3: Query(start = 0, end = 4)
    start = 0;
    end = 4;
    queryEvenParity(segmentTree, n, start, end);
}
}

// This code is contributed by ukasp
```

**Output:** 

```
3
2
```