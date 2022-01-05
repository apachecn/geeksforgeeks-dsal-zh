# 每个人成为朋友的最早时刻

> 原文:[https://www . geesforgeks . org/人人成为朋友的最早时刻/](https://www.geeksforgeeks.org/the-earliest-moment-when-everyone-become-friends/)

给定一组 **N** 人，每个人具有从 **0** 到**(N–1)**的唯一 ID 值，以及形式 **{U，V，time}** 的 **M** 元素的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr】**，表示人 **U** 将在给定的**时间**认识人 **V** 。假设人 **U** 与人 **V** 相识，如果 **U** 与 **V** 是朋友，或者 **U** 是与 **V** 相识的人的朋友。任务是找到每个人互相认识的最早时间。

**示例:**

> **输入:** N = 4，arr[] = {{0，1，2}，{1，2，3}，{2，3，4}}
> **输出:** 4
> **说明:**最初人数为 4 人，即{0}、{1}、{2}、{3}。
> 
> *   在时间= 2 时，{0}和{1}成为了朋友。因此，认识的人组成了{0，1}，{2}，{3}。
> *   在时间= 3 时，{1}和{2}成为了朋友。因此，认识的人变成了{0，1，2}，{3}。
> *   在时间= 4 时，{2}和{3}成为了朋友。因此，认识的人变成了{0，1，2，3}。
> 
> 因此，在时间= 4 时，每个人都互相认识了。
> 
> **输入:** N = 6，arr[] = {{0，1，4}，{3，4，5}，{2，3，14}，{1，5，24}，{2，4，12}，{0，3，42}，{1，2，41}，{4，5，11}}
> **输出:** 24

**方法:**给定的问题可以使用[不相交集合并数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)来解决。这个想法是按照时间价值递增的顺序执行人与人之间的联合操作。要求的答案将是所有人属于同一个集合的时间。按照以下步骤解决给定的问题:

*   根据这里讨论的算法，用**联合**和**查找集**功能实现[不相交集联合数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)。
*   初始化一个变量 **time** ，存储 DSU 当前时间戳的值。
*   [按照时间的递增顺序对给定的数组](https://www.geeksforgeeks.org/sort-c-stl/) **arr[]** 进行排序。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，在 **(U <sub>i</sub> 、V <sub>i</sub> )** 之间执行并集操作，如果 **U <sub>i</sub>** 和 **V <sub>i</sub>** 所属，则将当前时间戳更新为**时间<sub>I</sub>**
*   如果完全遍历数组**arr【】**后的集合总数为 **1** ，则返回变量**时间**的值，否则返回 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Implementation of DSU
class UnionFind {

    vector<int> parent, rank;

    // Stores the current timestamp
    int time;

    // Stores the count of current sets
    int count;

public:
    // Constructor to create and
    // initialize sets of N items
    UnionFind(int N)
        : parent(N), rank(N), count(N)
    {
        time = 0;

        // Creates N single item sets
        for (int i = 0; i < N; i++) {
            parent[i] = i;
            rank[i] = 1;
        }
    }

    // Function to find the set of
    // given item node
    int find(int node)
    {
        if (node == parent[node])
            return node;
        return parent[node]
               = find(parent[node]);
    }

    // Function to perform the union of
    // two sets represented by u and v,
    // and update the value of time
    void performUnion(int u, int v,
                      int updatedTime)
    {

        if (count == 1)
            return;

        // Find current sets of u and v
        int rootX = find(u);
        int rootY = find(v);

        if (rootX != rootY) {

            // Put smaller ranked item under
            // bigger ranked item if ranks
            // are different
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            }
            else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            }
            else {
                parent[rootX] = rootY;
                rank[rootY] += 1;
            }

            // Update the value of the
            // current timestamp
            time = updatedTime;

            // Update the value of
            // set count
            count--;
        }
    }

    // Function to return current
    // set count
    int getCount() { return count; }

    // Function to return current
    // time stamp
    int getTime() { return time; }
};

// Comparator function to sort the array
// in increasing order of 3rd element
bool cmp(vector<int>& A, vector<int>& B)
{
    return A[2] <= B[2];
}

// Function to find the earliest time when
// everyone became friends to each other
int earliestTime(vector<vector<int> >& arr,
                 int N)
{
    // Sort array arr[] in increasing order
    sort(arr.begin(), arr.end(), cmp);

    // Initialize a DSU with N elements
    UnionFind unionFind(N);

    // Iterate over array arr[] perform
    // union operation for each element
    for (auto& it : arr) {

        // Perfoem union operation on
        // it[0] and it[1] and update
        // timestamp to it[2]
        unionFind.performUnion(
            it[0], it[1], it[2]);
    }

    // Return Answer
    if (unionFind.getCount() == 1) {
        return unionFind.getTime();
    }
    else {
        return -1;
    }
}

// Driver Code
int main()
{
    int N = 6;
    vector<vector<int> > arr
        = { { 0, 1, 4 }, { 3, 4, 5 },
            { 2, 3, 14 }, { 1, 5, 24 },
            { 2, 4, 12 }, { 0, 3, 42 },
            { 1, 2, 41 }, { 4, 5, 11 } };

    cout << earliestTime(arr, N);

    return 0;
}
```

**Output:** 

```
24
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)