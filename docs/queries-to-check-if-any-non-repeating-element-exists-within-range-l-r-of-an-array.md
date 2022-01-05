# 查询数组

的范围【L，R】内是否存在任何非重复元素

> 原文:[https://www . geesforgeks . org/query-to-check-if-any-non-repeating-element-exists-in-range-l-r-of-a-array/](https://www.geeksforgeeks.org/queries-to-check-if-any-non-repeating-element-exists-within-range-l-r-of-an-array/)

给定一个由整数和查询组成的 **(L，R)** 形式的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是检查索引**【L，R】***(基于 1 的索引)*中是否存在任何非重复元素。如果至少有一个非重复元素，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** arr[] = {1，2，1，2，3，4}，query[][]= { {1，4}，{1，5}}
> **输出:**否是
> **解释:**
> 对于第一个查询，子阵是{ 1，2，1，2}，我们可以看到两个数都有频率 2。所以答案是 No.
> 对于第二个查询，子阵是{1，2，1，2，3}，我们可以看到 3 有频率 1 所以答案是 Yes。
> 
> **输入:** arr[] = {1，2，3，4，5}，query[][]= { {1，4}}
> **输出:**是
> **解释:**子阵为{ 1，2，3，4}，所有元素为频率 1，所以答案为是。

**天真方法:**
解决这个问题最简单的方法是为每个查询迭代一个给定的子数组，并维护一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储每个元素的频率。迭代地图，检查是否有频率为 1 的元素。

***时间复杂度:** O(Q * N)
**辅助空间复杂度:** O(N)*

**高效方法:**解决方案的关键观察是，对于给定数组中频率为 1 的元素，数组中该数字的**前一次出现**严格小于查询 l，元素的**后一次出现**严格大于某个查询的 r。用这个观察来寻找秩序。以下是使用[合并排序树](https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/)方法解决给定问题的步骤:

1.  将数组中每个带有元素的**的前一次出现和下一次出现存储为[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)。**
2.  构建合并排序树，并根据前一个匹配项合并其中的节点。[合并](https://www.geeksforgeeks.org/merge-operations-using-stl-in-c-merge-includes-set_union-set_intersection-set_difference/)功能用于合并范围。
3.  在合并排序树的每个节点上，在下一次出现时保持前缀最大值，因为我们需要尽可能小的前一次出现和尽可能大的某个元素的下一次出现。
4.  为了回答这个问题，我们需要先前出现次数严格小于 l 的节点。
5.  对于合并排序树中前一次出现次数小于 l 的元素，查找最大下一次出现次数，并检查下一次出现次数是否大于查询的 r，然后在频率为 1 的子数组中存在一个元素。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 9;
const int N = 1e5 + 5;

// Merge sort of pair type for storing
// prev and next occurrences of element
vector<vector<pair<int, int> > > segtree(4 * N);

// Stores the occurrences
vector<pair<int, int> > occurrences(N);

// Finds occurrences
vector<set<int> > pos(N);

int n;

// Function to build merge sort tree
void build(int node = 0, int l = 0,
           int r = n - 1)
{

    // For leaf node, push the prev &
    // next occurrence of the lth node
    if (l == r) {
        segtree[node].push_back(occurrences[l]);
        return;
    }

    int mid = (l + r) / 2;

    // Left recursion call
    build(2 * node + 1, l, mid);

    // Right recursion call
    build(2 * node + 2, mid + 1, r);

    // Merging the left child and right child
    // according to the prev occurrence
    merge(segtree[2 * node + 1].begin(),
          segtree[2 * node + 1].end(),
          segtree[2 * node + 2].begin(),
          segtree[2 * node + 2].end(),
          back_inserter(segtree[node]));

    // Update the next occurrence
    // with prefix maximum
    int mx = 0;

    for (auto& i : segtree[node]) {

        // Update the maximum
        // next occurrence
        mx = max(mx, i.second);

        // Update the next occurrence
        // with prefix max
        i.second = mx;
    }
}

// Function to check whether an
// element is present from x to y
// with frequency 1
bool query(int x, int y, int node = 0,
           int l = 0, int r = n - 1)
{
    // No overlap condition
    if (l > y || r < x || x > y)
        return false;

    // Complete overlap condition
    if (x <= l && r <= y) {

        // Find the first node with
        // prev occurrence >= x
        auto it = lower_bound(segtree[node].begin(),
                              segtree[node].end(),
                              make_pair(x, -1));

        // No element in this range with
        // previous occurrence less than x
        if (it == segtree[node].begin())
            return false;

        else {

            it--;

            // Check if the max next
            // occurrence is greater
            // than y or not
            if (it->second > y)
                return true;
            else
                return false;
        }
    }

    int mid = (l + r) / 2;
    bool a = query(x, y, 2 * node + 1, l, mid);
    bool b = query(x, y, 2 * node + 2, mid + 1, r);

    // Return if any of the
    // children returned true
    return (a | b);
}

// Function do preprocessing that
// is finding the next and previous
// occurrences
void preprocess(int arr[])
{

    // Store the position of
    // every element
    for (int i = 0; i < n; i++) {
        pos[arr[i]].insert(i);
    }

    for (int i = 0; i < n; i++) {

        // Find the previous
        // and next occurrences
        auto it = pos[arr[i]].find(i);
        if (it == pos[arr[i]].begin())
            occurrences[i].first = -INF;

        else
            occurrences[i].first = *prev(it);

        // Check if there is no next occurrence
        if (next(it) == pos[arr[i]].end())

            occurrences[i].second = INF;
        else
            occurrences[i].second = *next(it);
    }

    // Building the merge sort tree
    build();
}

// Function to find whether there is a
// number in the subarray with 1 frequency
void answerQueries(int arr[],
                   vector<pair<int, int> >& queries)
{
    preprocess(arr);

    // Answering the queries
    for (int i = 0; i < queries.size(); i++) {
        int l = queries[i].first - 1;
        int r = queries[i].second - 1;

        bool there = query(l, r);

        if (there == true)
            cout << "Yes\n";

        else
            cout << "No\n";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 2, 3, 4 };
    n = sizeof(arr) / sizeof(arr[0]);

    vector<pair<int, int> > queries = { { 1, 4 }, { 1, 5 } };

    answerQueries(arr, queries);
}
```

**Output:**

```
No
Yes

```

**时间复杂度:***O(N * log(N)+Q * log<sup>2</sup>(N))*
**辅助空间:** *O(N*log(N))*