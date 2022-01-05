# 更新前后[L，R]数组中元素的和与最大值

> 原文:[https://www . geeksforgeeks . org/更新前后数组中元素的总和和最大值/](https://www.geeksforgeeks.org/sum-and-maximum-of-elements-in-array-from-l-r-before-and-after-updates/)

**先决条件:** [段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)[在段树](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/)中偷懒繁殖。
给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是执行以下操作:

1.  将值 **arr[i]** 更改为 **min(arr[i]，X)** ，其中 X 是给定范围内的整数**【L，R】**。
2.  找到从索引 **L 到 R** 的最大值，其中 **0 ≤ L ≤ R ≤ N-1** 在上图数组更新前后。
3.  求从索引 **L 到 R** 的元素之和，其中 **0 ≤ L ≤ R ≤ N-1** 在上图数组更新前后。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，L = 2，R = 4，X = 3
> **输出:**
> 更新前范围【2，4】最大值:5
> 更新前范围【2，4】之和:12
> 更新后范围【2，4】最大值:3
> 更新后范围【2，4】之和:9
> **说明:**
> **更新前**
> 
> **更新后:**
> arr[] = {1，2，3，3，3}
> 距离[L，R]的最大值为 3
> 范围内的和[L，R]为 3 + 3 + 3 = 9
> 
> **输入:** arr[] = {1，4，19，0，7，22，7}，L = 1，R = 5，X = 14
> **输出:**
> 更新前范围【1，5】最大值:22
> 更新前范围【1，5】之和:52
> 更新后范围【1，5】最大值:22
> 更新后范围【1，5】之和:39
> **说明:【t1t 7}
> 距离【L，R】的最大值为 22
> 范围【L，R】的和为 4 + 19 + 0 + 7 + 22 = 52**
> 
> **更新后:**
> arr[] = {1，4，14，0，7，14，7}
> 从[L，R]开始的最大值是 14
> 范围内的和[L，R]是 4 + 14 + 0 + 7 + 14 = 39

**方法:**
**<u>[懒惰传播](https://www.geeksforgeeks.org/lazy-propagation-in-segment-tree/) :</u>** 的几个术语

1.  **下推():**将惰性标记应用于当前节点，然后将其下推至其子节点。
2.  **tag_condition:** 是设置惰性节点需要满足的条件。在正常的惰性树中，通常节点覆盖的范围完全位于更新范围内。
3.  [线段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)中的一个节点代表数组的一个范围。现在，该范围内的所有元素都将具有不同的值，并且在更新过程中它们将改变不同的量。因此，我们需要关于不同值及其在该范围内的计数的信息。因此，这变成了最差情况下的 0**(N)**操作，因为在一个范围内的最大 **N** 个不同节点。
4.  以下是在[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)中解决这些限制的方法。段树中的每个节点将具有以下值:
    *   **值**:一个范围的值，这里是该范围内所有元素的总和
    *   **最大值**:该范围内的最大值
    *   **秒最大值**:该范围内严格的第二个最大值
    *   **cnt_max** :该范围内最大值的计数
    *   **cnt_secondmax** :该范围内的最大秒数

以下是步骤:

1.  为给定的数组元素形成一个[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，每个节点都具有上述属性。
2.  对于**更新查询()**调用，请执行以下操作:
    *   如果 **max_value** 小于更新值(比如说 **X** ，那么没有值会改变，因为 **min(arr[i]，X)** 在这种情况下本身就是 arr[i]。
    *   如果**秒最大值≤ X ≤最大值**，则更新该节点的值，**新值**的计算公式为:

        ```
        new_sum = sum - f*maxvalue + f*X, 
        where f is the frequency of maxvalue

        ```

3.  查询查找**【L，R】**范围内的最大数值:
    *   如果范围**【L，R】**完全位于范围之外，则返回 **0** 。
    *   如果范围**【L，R】**完全位于该范围内，则当前范围的最大值为**树【位置】. mx1** 。
    *   否则递归地检查左和右子树的上述条件。
    *   上述所有递归调用的最大值给出了范围**【L，R】**内的最大值。
4.  查询查找**【L，R】**范围内的和:
    *   如果范围**【L，R】**完全位于范围之外，则返回 0。
    *   如果范围**【L，R】**完全位于该范围内，则当前范围的总和为**树【位置】。求和**。
    *   否则递归地检查左和右子树的上述条件。
    *   上述递归调用的所有值的和给出了范围**【L，R】**内的和。

下面是上述方法的实现:

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node for each Segment Tree
typedef struct node {

    int sum;
    int mx1;
    int mx2;
    int cnt_mx1;
    int cnt_mx2;

    // Constructor
    node()
    {
        sum = mx1 = mx2 = 0;
        cnt_mx1 = cnt_mx2 = 0;
    }

} node;

const int N = 1e5 + 5;

// Segment Tree Node
node tree[N];

// For Lazy Propagation
int lazy[N];

// Function to merge 2 nodes of Segment
// Tree
void combine(int pos)
{

    // Map to store the count of
    // maximum1 and maximum2 for every
    // node segment tree
    map<int, int> x;

    // Update the count for left and
    // right subtree
    x[tree[2 * pos + 1].mx1] += tree[2 * pos + 1].cnt_mx1;
    x[tree[2 * pos + 1].mx2] += tree[2 * pos + 1].cnt_mx2;
    x[tree[2 * pos + 2].mx1] += tree[2 * pos + 2].cnt_mx1;
    x[tree[2 * pos + 2].mx2] += tree[2 * pos + 2].cnt_mx2;

    // Vector pair to store mx1 & mx2
    vector<pair<int, int> > v;

    // Traverse the v
    for (auto it = x.begin(); it != x.end(); it++) {
        v.push_back({ it->first, it->second });
    }

    int n = v.size();

    // Update the mx1 and mx2 after
    // combined node
    tree[pos].mx1 = v[n - 1].first;
    tree[pos].cnt_mx1 = v[n - 1].second;

    // If only one node
    if (n == 1) {
        tree[pos].mx2 = tree[pos].cnt_mx2 = 0;
    }

    // ELse Update mx2 and cnt_mx2
    else {
        tree[pos].mx2 = v[n - 2].first;
        tree[pos].cnt_mx2 = v[n - 2].second;
    }

    // Update the sum
    tree[pos].sum = tree[2 * pos + 1].sum
                    + tree[2 * pos + 2].sum;
}

// Function that returns true if tag
// condition is satisfied, and we can
// do lazy update
bool tag_condition(int pos, int x)
{
    if (tree[pos].mx1 > x
        && tree[pos].mx2 <= x) {
        return true;
    }
    return false;
}

// Function that pushes down the lazy
// value of the current node to its children
void pushdown(int beg, int end, int pos)
{
    // If tag condition satisfies
    if (tag_condition(pos, lazy[pos])) {

        int initsum = tree[pos].mx1 * tree[pos].cnt_mx1;
        int finsum = lazy[pos] * tree[pos].cnt_mx1;
        tree[pos].sum += finsum - initsum;

        // If only one node, then update the
        // maximum value to current position
        if (beg == end)
            tree[pos].mx1 = lazy[pos];

        // If lazy[pos] > maximum value
        else {

            // Update mx1 to current
            // lazy[pos]
            if (lazy[pos] > tree[pos].mx2)
                tree[pos].mx1 = lazy[pos];

            // Else update the count
            else {

                tree[pos].mx1 = lazy[pos];
                tree[pos].cnt_mx1 += tree[pos].cnt_mx2;
                tree[pos].mx2 = tree[pos].cnt_mx2 = 0;

                // map to store the cnt
                // of maximum1 and maximum2
                // for every node in segment
                // tree
                map<int, int> x;
                x[tree[2 * pos + 1].mx1] += tree[2 * pos + 1].cnt_mx1;
                x[tree[2 * pos + 1].mx2] += tree[2 * pos + 1].cnt_mx2;
                x[tree[2 * pos + 2].mx1] += tree[2 * pos + 2].cnt_mx1;
                x[tree[2 * pos + 2].mx2] += tree[2 * pos + 2].cnt_mx2;

                // Traverse the map
                for (auto it = x.begin(); it != x.end(); it++) {

                    // Update the maximum
                    // count
                    if (it->first != tree[pos].mx1
                        && it->first > tree[pos].mx2) {
                        tree[pos].mx2 = it->first;
                        tree[pos].cnt_mx2 = it->second;
                    }
                }
            }

            // Update the value for
            // lazy left and right
            // subtree
            lazy[2 * pos + 1] = min(lazy[2 * pos + 1],
                                    lazy[pos]);
            lazy[2 * pos + 2] = min(lazy[2 * pos + 2],
                                    lazy[pos]);
        }
    }

    lazy[pos] = INT_MAX;
}

// Function that Lazy update in segment
// tree i.e., arr[i] = min(arr[i], val)
void update(int beg, int end, int l, int r,
            int pos, int val)
{

    // Push the current node value to
    // left and right subtree
    if (lazy[pos] < INT_MAX)
        pushdown(beg, end, pos);

    // If inside the range, then update
    // the value as per the conditions
    if (l <= beg and r >= end
        && tag_condition(pos, val)) {
        lazy[pos] = min(lazy[pos], val);
        pushdown(beg, end, pos);
        return;
    }

    // Outside the range
    else if (l > end || r < beg
             || beg > end
             || tree[pos].mx1 <= val) {
        return;
    }

    // Check for left and right subtree
    else {

        int mid = (beg + end) / 2;
        update(beg, mid, l, r,
               2 * pos + 1, val);
        update(mid + 1, end, l, r,
               2 * pos + 2, val);
        combine(pos);
    }
}

// Function that returns the maximum
// value in range [L, R]
int query1(int beg, int end, int l,
           int r, int pos)
{

    // Push the current node value in
    // the left and right subtree
    if (lazy[pos] < INT_MAX) {
        pushdown(beg, end, pos);
    }

    // If inside the range, then return
    // the maximum value
    if (l <= beg && r >= end) {
        return tree[pos].mx1;
    }

    // Outside the range
    else if (l > end || r < beg
             || beg > end) {
        return 0;
    }

    // Check for left and right subtree
    else {
        int mid = (beg + end) / 2;
        return max(query1(beg, mid, l, r,
                          2 * pos + 1),
                   query1(mid + 1, end, l,
                          r, 2 * pos + 2));
    }
}

// Function to find the sum in the
// range [L, R]
int query2(int beg, int end, int l,
           int r, int pos)
{
    // Push the current node value
    if (lazy[pos] < INT_MAX)
        pushdown(beg, end, pos);

    // If in the range, return the
    // sum
    if (l <= beg and r >= end)
        return tree[pos].sum;
    else if (l > end || r < beg
             || beg > end) {
        return 0;
    }

    // Check for left and right subtree
    else {
        int mid = (beg + end) / 2;

        return query2(beg, mid, l, r,
                      2 * pos + 1)
               + query1(mid + 1, end, l,
                        r, 2 * pos + 2);
    }
}

// Construct Segment Tree
void constr(int arr[], int beg,
            int end, int pos)
{
    // If only a single node
    if (beg == end) {
        int x = arr[beg];
        tree[pos].sum = x;
        tree[pos].mx1 = x;

        tree[pos].cnt_mx1 = 1;
        tree[pos].mx2 = 0;
        tree[pos].cnt_mx2 = 0;

        return;
    }

    // Recursively update for
    // left and right subtree
    else {

        int mid = (beg + end) / 2;

        // For Left subtree
        constr(arr, beg, mid, 2 * pos + 1);

        // For right subtree
        constr(arr, mid + 1, end, 2 * pos + 2);

        // Combine the two left and
        // right subtree
        combine(pos);
    }
}

// A utility function to construct
// the segment tree
void construct(int arr[], int n)
{
    for (int i = 0; i < N; i++) {
        lazy[i] = INT_MAX;
    }

    // Function call to Construct
    // segment tree
    constr(arr, 0, n - 1, 0);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };

    // Construct segment tree
    construct(arr, 5);

    cout << "Maximum in [2, 4] before update: ";
    // Query for maximum in range [0, 4]
    cout << query1(0, 4, 2, 4, 0) << endl;

    cout << "Sum in [2, 4] before update: ";
    // Query for sum in range [0, 4]
    cout << query2(0, 4, 2, 4, 0) << endl;

    // Update Query
    update(0, 4, 2, 5, 0, 3);

    cout << endl;
    cout << "Updated array elements between "
         << "[2, 4] as min(arr[i], 3)" << endl;
    cout << endl;

    cout << "Maximum in [2, 4] after update: ";
    // Query for maximum in range [0, 4]
    cout << query1(0, 4, 2, 4, 0) << endl;

    cout << "Sum in [2, 4] after update: ";
    // Query for maximum in range [0, 4]
    cout << query2(0, 4, 2, 4, 0) << endl;

    return 0;
}
```

**Output:**

```
Maximum in [2, 4] before update: 5
Sum in [2, 4] before update: 8

Updated array elements between [2, 4] as min(arr[i], 3)

Maximum in [2, 4] after update: 3
Sum in [2, 4] after update: 6

```

**时间复杂度:** O(N*log N)