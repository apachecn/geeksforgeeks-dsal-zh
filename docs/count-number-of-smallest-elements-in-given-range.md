# 计算给定范围内最小元素的数量

> 原文:[https://www . geesforgeks . org/count-给定范围内最小元素的数量/](https://www.geeksforgeeks.org/count-number-of-smallest-elements-in-given-range/)

给定一个由 N 个数字和 Q 个查询组成的数组，每个查询由 L 和 r 组成。我们需要编写一个程序，打印 L-R 范围内最小元素的出现次数。

示例:

```
Input: a[] = {1, 1, 2, 4, 3, 3}
        Q = 2 
        L = 1 R = 4 
        L = 3 R = 6
Output: 2 
        1 
Explanation: The smallest element in range 1-4 
is 1 which occurs 2 times. The smallest element
in the range 3-6 is 2 which occurs once.  

Input : a[] = {1, 2, 3, 3, 1}
        Q = 2 
        L = 1 R = 5 
        L = 3 R = 4
Output : 2
         2

```

一种正常的方法是从 L-R 迭代，找出范围内最小的元素。在 L-R 范围内再次迭代，并计算最小元素在 L-R 范围内出现的次数。在最坏的情况下，如果 L=1 且 R=N，复杂度将为 O(N)

一个有效的方法是使用[分割树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)来解决上述问题。在段树的每个节点上，存储最小元素和最小元素的计数。在叶节点，数组元素存储在最小值和计数存储 1 中。对于除叶节点之外的所有其他节点，我们按照给定的条件合并右节点和左节点:

> **1。min(left _ subtree)<min(right _ subtree):**
> node . min = min(left _ subtree)，node . count = left _ subtree . count
> **2。min(left _ subtree)>min(right _ subtree):**
> node . min = min(right _ subtree)，node . count = right _ subtree . count
> **3。min(left _ subtree)= min(right_subtree):**
> node . min = min(left _ subtree)或 min(right _ subtree)，node . count = left _ subtree . count+right _ subtree . count

下面给出了上述方法的实现:

```
// CPP program to Count number of occurrence of
// smallest element in range L-R
#include <bits/stdc++.h>
using namespace std;

#define N 100005

// predefines the tree with nodes
// storing min and count
struct node {
    int min;
    int cnt;
} tree[5 * N];

// function to construct the tree
void buildtree(int low, int high, int pos, int a[])
{
    // base condition
    if (low == high) {

        // leaf node has a single element
        tree[pos].min = a[low];
        tree[pos].cnt = 1;
        return;
    }

    int mid = (low + high) >> 1;
    // left-subtree
    buildtree(low, mid, 2 * pos + 1, a);

    // right-subtree
    buildtree(mid + 1, high, 2 * pos + 2, a);

    // left subtree has the minimum element
    if (tree[2 * pos + 1].min < tree[2 * pos + 2].min) {
        tree[pos].min = tree[2 * pos + 1].min;
        tree[pos].cnt = tree[2 * pos + 1].cnt;
    }

    // right subtree has the minimum element
    else if (tree[2 * pos + 1].min > tree[2 * pos + 2].min) {
        tree[pos].min = tree[2 * pos + 2].min;
        tree[pos].cnt = tree[2 * pos + 2].cnt;
    }

    // both subtree has the same minimum element
    else {
        tree[pos].min = tree[2 * pos + 1].min;
        tree[pos].cnt = tree[2 * pos + 1].cnt + tree[2 * pos + 2].cnt;
    }
}

// function that answers every query
node query(int s, int e, int low, int high, int pos)
{
    node dummy;
    // out of range
    if (e < low or s > high) {
        dummy.min = dummy.cnt = INT_MAX;
        return dummy;
    }

    // in range
    if (s >= low and e <= high) {
        return tree[pos];
    }

    int mid = (s + e) >> 1;

    // left-subtree
    node ans1 = query(s, mid, low, high, 2 * pos + 1);

    // right-subtree
    node ans2 = query(mid + 1, e, low, high, 2 * pos + 2);

    node ans;
    ans.min = min(ans1.min, ans2.min);

    // add count when min is same of both subtree
    if (ans1.min == ans2.min)
        ans.cnt = ans2.cnt + ans1.cnt;

    // store the minimal's count
    else if (ans1.min < ans2.min)
        ans.cnt = ans1.cnt;

    else
        ans.cnt = ans2.cnt;

    return ans;
}

// function to answer query in range l-r
int answerQuery(int a[], int n, int l, int r)
{
    // calls the function which returns a node
    // this function returns the count which
    // will be the answer
    return query(0, n - 1, l - 1, r - 1, 0).cnt;
}

// Driver Code
int main()
{
    int a[] = { 1, 1, 2, 4, 3, 3 };

    int n = sizeof(a) / sizeof(a[0]);
    buildtree(0, n - 1, 0, a);
    int l = 1, r = 4;

    // answers 1-st query
    cout << answerQuery(a, n, l, r) << endl;

    l = 2, r = 6;
    // answers 2nd query
    cout << answerQuery(a, n, l, r) << endl;
    return 0;
}
```

输出:

```
2
1

```

**时间复杂度:** **O(n)** 为树的构造。 **O(log n)** 为每个查询。