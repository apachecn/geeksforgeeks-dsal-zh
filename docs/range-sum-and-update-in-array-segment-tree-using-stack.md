# 数组中的范围求和和更新:使用堆栈分割树

> 原文:[https://www . geesforgeks . org/range-sum-and-update-in-array-segment-tree-use-stack/](https://www.geeksforgeeks.org/range-sum-and-update-in-array-segment-tree-using-stack/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是做以下操作:

1.  将数值 **X** 添加到从索引 **A** 到 **B** 的所有元素中，其中 **0 ≤ A ≤ B ≤ N-1** 。
2.  求上图数组更新前后从索引 **L** 到 **R** 的元素之和，其中 **0 ≤ L ≤ R ≤ N-1** 。

**例:**

> **输入:** arr[] = {1，3，5，7，9，11}，L = 1，R = 3，A = 1，B = 5，X = 10
> **输出:**
> 给定范围内的值之和= 15
> 给定范围内的更新值之和= 45
> **说明:**
> 范围内的值之和 **1 至 3** 为 3 + 5 + 7 = 15。
> 从索引 **1 到 5** 加上 **10** 后的 arr[]为 arr[] = {1，13，15，17，19，21}
> 更新后 **1 到 3** 范围内的值之和为 13 + 15 + 17 = 45。
> **输入:** arr[] = { 11，32，5，7，19，11，8}，L = 2，R = 6，A = 1，B = 5，X = 16
> **输出:**
> 给定范围内的值之和= 50
> 给定范围内的更新值之和= 114
> **解释:**
> 给定范围内的值之和 **2 至 6【t38
> 从索引 **1 到 5** 加上 **16** 后的 arr[]为 arr[] = {11，48，21，23，35，27，8}
> 更新后 **2 到 6** 范围内的值之和为 21 + 23 + 35 + 27 + 8 = 114。**

**方法:**
针对给定问题使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的递归方法在本文中讨论。在这篇文章中，我们将讨论一种使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)来避免[递归](https://www.geeksforgeeks.org/recursion/)的方法。
以下是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)实现[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)的步骤:

1.  其思想是使用元组来存储[栈](https://www.geeksforgeeks.org/stack-data-structure/)中有节点号和范围索引的状态。
2.  **<u>为建筑段树</u> :**
    *   将根节点作为元组推送到[栈【T1:](https://www.geeksforgeeks.org/stack-data-structure/) 

```
Stack S;
start = 0, end = arr_size - 1
S.emplace(1, start, end)
```

*   从[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)弹出元素，并执行以下操作，直到[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)变为空:
    1.  如果起始索引等于结束索引，那么我们到达叶节点，并将[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)数组中的值更新为给定数组中当前索引处的值。
    2.  否则，插入当前节点为**的标志元组，放置(current_node，INF，INF)** 以反转求值顺序，并插入左右子节点值为:
        的元组

> mid =(开始+结束)/ 2
> 第一个炮台(curr_node * 2，开始，中间)
> 第一个炮台(curr_node * 2 + 1，中间+ 1，结束)

2.  如果开始索引和结束索引与 **INF** 相同，那么将当前索引处的[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)值更新为:

> 当前索引处的值更新为左右子级的值:
> 树[curr_node] =树[2*curr_node] +树[2*curr_node + 1]

2.  **<u>更新树</u> :**
    *   将根节点推至[栈](https://www.geeksforgeeks.org/stack-data-structure/)，如同构建[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)一样。
    *   从[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)中弹出元素，并执行以下操作，直到堆栈变空:
        1.  如果当前节点有任何挂起的更新，则首先更新到当前节点。
        2.  如果当前节点范围完全位于更新查询范围内，则使用该值更新当前节点。
        3.  如果当前节点范围与更新查询范围重叠，则按照上述方法，在[栈](https://www.geeksforgeeks.org/stack-data-structure/)中推左、右子元组。
        4.  使用上面的左右子查询的结果更新查询。
3.  **<u>更新查询</u> :**
    *   将根节点推至[栈](https://www.geeksforgeeks.org/stack-data-structure/)，如同构建[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)一样。
    *   从堆栈中弹出元素，并执行以下操作，直到[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)变为空:
        1.  如果当前节点范围位于给定查询之外，则继续下一个迭代。
        2.  如果当前节点范围完全位于更新查询范围内，则使用当前节点值更新结果。
        3.  如果当前节点范围与更新查询范围重叠，则按照上述方法，在[栈](https://www.geeksforgeeks.org/stack-data-structure/)中推左、右子元组。
        4.  使用从左右子节点获得的值更新结果。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include"bits/stdc++.h"
using namespace std;

constexpr static int MAXSIZE = 1000;
constexpr static int INF
    = numeric_limits<int>::max();

// Segment Tree array
int64_t tree[MAXSIZE];

// Lazy Update array
int64_t lazy[MAXSIZE];

// This tuple will hold tree state
// the stacks
using QueryAdaptor
    = tuple<int64_t,
            int64_t,
            int64_t>;

// Build our segment tree
void build_tree(int64_t* arr,
                int64_t arr_size)
{

    // Stack will use to update
    // the tree value
    stack<QueryAdaptor> st;

    // Emplace the root of the tree
    st.emplace(1, 0, arr_size - 1);

    // Repeat until empty
    while (!st.empty()) {

        // Take the indexes at the
        // top of the stack
        int64_t currnode, curra, currb;

        // value at the top of the
        // stack
        tie(currnode, curra, currb) = st.top();

        // Pop the value from the
        // stack
        st.pop();

        // Flag with INF ranges are merged
        if (curra == INF && currb == INF) {
            tree[currnode] = tree[currnode * 2]
                             + tree[currnode * 2 + 1];
        }

        // Leaf node
        else if (curra == currb) {
            tree[currnode] = arr[curra];
        }

        else {

            // Insert flag node inverse
            // order of evaluation
            st.emplace(currnode, INF, INF);
            int64_t mid = (curra + currb) / 2;

            // Push children
            st.emplace(currnode * 2,
                       curra, mid);
            st.emplace(currnode * 2 + 1,
                       mid + 1, currb);
        }
    }
}

// A utility function that propagates
// updates lazily down the tree
inline void push_down(int64_t node,
                      int64_t a,
                      int64_t b)
{
    if (lazy[node] != 0) {
        tree[node] += lazy[node] * (b - a + 1);

        if (a != b) {
            lazy[2 * node] += lazy[node];
            lazy[2 * node + 1] += lazy[node];
        }

        lazy[node] = 0;
    }
}

// Iterative Range_Update function to
// add val to all elements in the
// range i-j (inclusive)
void update_tree(int64_t arr_size,
                 int64_t i,
                 int64_t j,
                 int64_t val)
{

    // Initialize the stack
    stack<QueryAdaptor> st;

    // Emplace the root of the tree
    st.emplace(1, 0, arr_size - 1);

    // Work until empty
    while (!st.empty()) {

        // Take the indexes at the
        // top of the stack
        int64_t currnode, curra, currb;
        tie(currnode, curra, currb) = st.top();
        st.pop();

        // Flag with INF ranges are merged
        if (curra == INF && currb == INF) {
            tree[currnode] = tree[currnode * 2]
                             + tree[currnode * 2 + 1];
        }

        // Traverse the previous updates
        // down the tree
        else {
            push_down(currnode, curra, currb);

            // No overlap condition
            if (curra > currb || curra > j
                || currb < i) {
                continue;
            }

            // Total overlap condition
            else if (curra >= i && currb <= j)
            {

                // Update lazy array
                tree[currnode] += val * (currb - curra + 1);

                if (curra != currb) {
                    lazy[currnode * 2] += val;
                    lazy[currnode * 2 + 1] += val;
                }
            }

            // Partial Overlap
            else
            {

                // Insert flag node inverse
                // order of evaluation
                st.emplace(currnode, INF, INF);

                int64_t mid = (curra + currb) / 2;

                // Push children
                st.emplace(currnode * 2,
                           curra, mid);
                st.emplace(currnode * 2 + 1,
                           mid + 1, currb);
            }
        }
    }
}

// A function that find the sum of
// all elements in the range i-j
int64_t query(int64_t arr_size,
              int64_t i,
              int64_t j)
{

    // Initialize stack
    stack<QueryAdaptor> st;

    // Emplace root of the tree
    st.emplace(1, 0, arr_size - 1);

    int64_t result = 0;

    while (!st.empty())
    {

        // Take the indexes at the
        // top of the stack
        int64_t currnode, curra, currb;
        tie(currnode, curra, currb) = st.top();
        st.pop();

        // Traverse the previous updates
        // down the tree
        push_down(currnode, curra, currb);

        // No overlap
        if (curra > currb || curra > j
            || currb < i) {
            continue;
        }

        // Total Overlap
        else if (curra >= i && currb <= j) {
            result += tree[currnode];
        }

        // Partial Overlap
        else {
            std::int64_t mid = (curra + currb) / 2;

            // Push children
            st.emplace(currnode * 2,
                       curra, mid);
            st.emplace(currnode * 2 + 1,
                       mid + 1, currb);
        }
    }

    return result;
}

// Driver Code
int main()
{

    // Initialize our trees with 0
    memset(tree, 0, sizeof(int64_t) * MAXSIZE);
    memset(lazy, 0, sizeof(int64_t) * MAXSIZE);

    int64_t arr[] = { 1, 3, 5, 7, 9, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Build segment tree from given array
    build_tree(arr, n);

    // Print sum of values in array
    // from index 1 to 3
    cout << "Sum of values in given range = "
         << query(n, 1, 3)
         << endl;

    // Add 10 to all nodes at indexes
    // from 1 to 5
    update_tree(n, 1, 5, 10);

    // Find sum after the value is updated
    cout << "Updated sum of values in given range = "
         << query(n, 1, 3)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.util.List;
import java.util.Stack;
class GFG
{

    static final int MAXSIZE = 1000;
    static final int INF = (int) Double.POSITIVE_INFINITY;

    // Segment Tree array
    static int[] tree = new int[MAXSIZE];

    // Lazy Update array
    static int[] lazy = new int[MAXSIZE];

    // Build our segment tree
    static void build_tree(int[] arr, int arr_size)
    {

        // Stack will use to update
        // the tree value
        Stack<List<Integer>> st = new Stack<>();

        // push the root of the tree
        st.push(Arrays.asList(1, 0, arr_size - 1));

        // Repeat until empty
        while (!st.isEmpty())
        {

            // Take the indexes at the
            // top of the stack
            int currnode, curra, currb;

            // value at the top of the
            // stack
            List<Integer> temp = st.peek();
            currnode = temp.get(0);
            curra = temp.get(1);
            currb = temp.get(2);

            // Pop the value from the
            // stack
            st.pop();

            // Flag with INF ranges are merged
            if (curra == INF && currb == INF)
            {
                tree[currnode] = tree[currnode * 2] +
                  tree[currnode * 2 + 1];
            }

            // Leaf node
            else if (curra == currb)
            {
                tree[currnode] = arr[curra];
            }

            else {

                // Insert flag node inverse
                // order of evaluation
                st.push(Arrays.asList(currnode, INF, INF));

                int mid = (curra + currb) / 2;

                // Push children
                st.push(Arrays.asList(currnode * 2, curra, mid));
                st.push(Arrays.asList(currnode * 2 + 1, mid + 1, currb));
            }
        }
    }

    // A utility function that propagates
    // updates lazily down the tree
    static void push_down(int node, int a, int b)
    {
        if (lazy[node] != 0)
        {
            tree[node] += lazy[node] * (b - a + 1);

            if (a != b)
            {
                lazy[2 * node] += lazy[node];
                lazy[2 * node + 1] += lazy[node];
            }

            lazy[node] = 0;
        }
    }

    // Iterative Range_Update function to
    // add val to all elements in the
    // range i-j (inclusive)
    static void update_tree(int arr_size, int i,
                            int j, int val)
    {

        // Initialize the stack
        Stack<List<Integer>> st = new Stack<>();

        // push the root of the tree
        st.push(Arrays.asList(1, 0, arr_size - 1));

        // Work until empty
        while (!st.isEmpty())
        {

            // Take the indexes at the
            // top of the stack
            int currnode, curra, currb;
            List<Integer> temp = st.peek();
            currnode = temp.get(0);
            curra = temp.get(1);
            currb = temp.get(2);
            st.pop();

            // Flag with INF ranges are merged
            if (curra == INF && currb == INF)
            {
                tree[currnode] = tree[currnode * 2] +
                  tree[currnode * 2 + 1];
            }

            // Traverse the previous updates
            // down the tree
            else
            {
                push_down(currnode, curra, currb);

                // No overlap condition
                if (curra > currb || curra > j || currb < i)
                {
                    continue;
                }

                // Total overlap condition
                else if (curra >= i && currb <= j)
                {

                    // Update lazy array
                    tree[currnode] += val * (currb - curra + 1);

                    if (curra != currb)
                    {
                        lazy[currnode * 2] += val;
                        lazy[currnode * 2 + 1] += val;
                    }
                }

                // Partial Overlap
                else
                {

                    // Insert flag node inverse
                    // order of evaluation
                    st.push(Arrays.asList(currnode, INF, INF));

                    int mid = (curra + currb) / 2;

                    // Push children
                    st.push(Arrays.asList(currnode * 2, curra, mid));
                    st.push(Arrays.asList(currnode * 2 + 1,
                                          mid + 1, currb));
                }
            }
        }
    }

    // A function that find the sum of
    // all elements in the range i-j
    static int query(int arr_size, int i, int j)
    {

        // Initialize stack
        Stack<List<Integer>> st = new Stack<>();

        // push root of the tree
        st.push(Arrays.asList(1, 0, arr_size - 1));

        int result = 0;

        while (!st.isEmpty())
        {

            // Take the indexes at the
            // top of the stack
            int currnode, curra, currb;
            List<Integer> temp = st.peek();
            currnode = temp.get(0);
            curra = temp.get(1);
            currb = temp.get(2);
            st.pop();

            // Traverse the previous updates
            // down the tree
            push_down(currnode, curra, currb);

            // No overlap
            if (curra > currb || curra > j || currb < i)
            {
                continue;
            }

            // Total Overlap
            else if (curra >= i && currb <= j)
            {
                result += tree[currnode];
            }

            // Partial Overlap
            else
            {
                int mid = (curra + currb) / 2;

                // Push children
                st.push(Arrays.asList(currnode * 2, curra, mid));
                st.push(Arrays.asList(currnode * 2 + 1, mid + 1, currb));
            }
        }

        return result;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Initialize our trees with 0
        Arrays.fill(tree, 0);
        Arrays.fill(lazy, 0);

        int arr[] = { 1, 3, 5, 7, 9, 11 };
        int n = arr.length;

        // Build segment tree from given array
        build_tree(arr, n);

        // Print sum of values in array
        // from index 1 to 3
        System.out.printf("Sum of values in given range = %d\n", query(n, 1, 3));

        // Add 10 to all nodes at indexes
        // from 1 to 5
        update_tree(n, 1, 5, 10);

        // Find sum after the value is updated
        System.out.printf("Updated sum of values in given range = %d\n", query(n, 1, 3));
    }
}

// This code is contributed by sanjeev2552
```

**Output:** 

```
Sum of values in given range = 15
Updated sum of values in given range = 45
```

**时间复杂度:**

*   **<u>对于树构造</u> :** O(N)，树中有(2n-1)个节点，每个节点的值计算一次。
*   **<u>对于查询</u> :** O(log N)，要查询一个和，我们在每个级别处理四个节点，级别数为 log N
*   **<u>对于更新</u> :** O(log N)，用惰性传播更新树是 O(log N)，因为我们更新树的根，然后只更新树的范围在每个级别重叠的那部分。