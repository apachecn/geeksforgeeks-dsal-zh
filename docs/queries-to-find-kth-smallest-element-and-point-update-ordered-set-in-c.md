# 查找第 kth 个最小元素和点更新的查询:C++中的有序集

> 原文:[https://www . geesforgeks . org/query-to-find-kth-最小元素和点-更新-有序集-in-c/](https://www.geeksforgeeks.org/queries-to-find-kth-smallest-element-and-point-update-ordered-set-in-c/)

给定大小为 N 的数组 arr[]和包含 M 个查询的集合 Q[][]，任务是在给定的数组上执行查询，这样可以有两种类型的查询:

*   **类型 1:**【I，x】–将 i <sup>第</sup>索引处的元素更新为 x。
*   **类型 2:**【k】–找到数组中第 k 个<sup>最小元素</sup>。

**示例:**

> **输入:** arr[] = {4，3，6，2}，Q[][] = {{1，2，5}，{2，3}，{1，1，7}，{2，1}}
> **输出:** 5 2
> **解释:**
> 对于 1 <sup>st</sup> 查询:arr[] = {4，5，6，2}
> 对于 2 <sup>nd</sup> 查询:3【T10
> 对于 3 <sup>rd</sup> 查询:arr[] = {7，5，6，2}
> 对于 4<sup>rd</sup>查询:1 <sup>st</sup> 最小元素为 2。
> 
> **输入:** arr[] = {1，0，4，2，0}，Q[][] = {{1，2，1}，{2，2}，{1，4，5}，{1，3，7}，{2，1}，{2，5}}
> **输出:** 1 0 7

**天真方法:**这个问题的天真方法是在恒定时间内更新数组中的第 i <sup>个</sup>元素，并使用排序来[找到第 K <sup>个</sup>个最小元素](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)。

**时间复杂度:** O(M * (N * log(N)))，其中 M 为查询数，N 为数组大小。

**高效方法:**想法是使用类似于[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)的[基于策略的数据结构](https://www.geeksforgeeks.org/policy-based-data-structures-g/)。

这里，基于[树的容器](https://gcc.gnu.org/onlinedocs/libstdc++/ext/pb_ds/tree_based_containers.html)用于以排序树的形式存储数组，使得左侧的所有节点都小于根，右侧的所有节点都大于根。以下是数据结构的属性:

*   它是通过保持节点不变来索引的，其中每个节点在其子树中都包含一个节点计数。
*   每次我们插入一个新节点或者删除一个节点，我们都可以通过冒泡到根来保持 O(logN)时间上的不变量。
*   因此，其左子树中节点的计数给出了排序顺序中该节点的**索引**，因为左子树的每个节点的值都小于父节点。

因此，我们的想法是对每个查询遵循以下方法:

1.  **类型 1:** 对于这个查询，我们更新数组的第 i <sup>个</sup>元素。因此，我们需要更新数组和数据结构中的元素。为了更新树容器中的值，在树中找到 arr[i]值，将其从树中删除，并将更新后的值插回到树中。
2.  **类型 2:** 为了找到第 K <sup>个</sup>最小的元素，在树上使用 find _ by _ order(K–1)，因为数据是已排序的数据。这类似于排序数组上的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)操作。

下面是上述方法的实现:

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace std;
using namespace __gnu_pbds;

// Defining the policy based Data Structure
typedef tree<pair<int, int>,
             null_type,
             less<pair<int, int> >,
             rb_tree_tag,
             tree_order_statistics_node_update>
    indexed_set;

// Elements in the array are not unique,
// so a pair is used to give uniqueness
// by incrementing cnt and assigning
// with array elements to insert in mySet
int cnt = 0;

// Variable to store the data in the
// policy based Data Structure
indexed_set mySet;

// Function to insert the elements
// of the array in mySet
void insert(int n, int arr[])
{
    for (int i = 0; i < n; i++) {
        mySet.insert({ arr[i], cnt });
        cnt++;
    }
}

// Function to update the value in
// the data structure
void update(int x, int y)
{
    // Get the pointer of the element
    // in mySet which has to be updated
    auto it = mySet.lower_bound({ y, 0 });

    // Delete from mySet
    mySet.erase(it);

    // Insert the updated value in mySet
    mySet.insert({ x, cnt });
    cnt++;
}

// Function to find the K-th smallest
// element in the set
int get(int k)
{
    // Find the pointer to the kth smallest element
    auto it = mySet.find_by_order(k - 1);
    return (it->first);
}

// Function to perform the queries on the set
void operations(int arr[], int n,
                vector<vector<int> > query, int m)
{
    // To insert the element in mySet
    insert(n, arr);

    // Iterating through the queries
    for (int i = 0; i < m; i++) {

        // Checking if the query is of type 1
        // or type 2
        if (query[i][0] == 1) {

            // The array is 0-indexed
            int j = query[i][1] - 1;
            int x = query[i][2];

            // Update the element in mySet
            update(x, arr[j]);

            // Update the element in the array
            arr[j] = x;
        }
        else {
            int K = query[i][1];

            // Print Kth smallest element
            cout << get(K) << endl;
        }
    }
}

// Driver code
int main()
{
    int n = 5, m = 6, arr[] = { 1, 0, 4, 2, 0 };

    vector<vector<int> > query = { { 1, 2, 1 },
                                   { 2, 2 },
                                   { 1, 4, 5 },
                                   { 1, 3, 7 },
                                   { 2, 1 },
                                   { 2, 5 } };

    operations(arr, n, query, m);

    return 0;
}
```

**Output:**

```
1
0
7

```

**时间复杂度:**由于每个操作需要 O(Log(N))个时间，并且有 M 个查询，所以整体时间复杂度为 **O(M * Log(N))** 。