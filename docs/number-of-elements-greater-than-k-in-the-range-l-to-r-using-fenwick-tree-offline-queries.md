# 使用分威克树(离线查询)计算 L 到 R 范围内大于 K 的元素数量

> 原文:[https://www . geeksforgeeks . org/elements-大于-k-in-range-l-to-r-use-fenwick-tree-offline-query/](https://www.geeksforgeeks.org/number-of-elements-greater-than-k-in-the-range-l-to-r-using-fenwick-tree-offline-queries/)

**先决条件:** [芬威克树(二进制索引树)](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)
给定一个 N 个数字的数组，以及多个查询，其中每个查询将包含三个数字(l、r 和 k)。任务是计算子阵[L，R]中大于 K 的阵元个数。
**例:**

```
Input:  n=6                                           
         q=2                                           
         arr[ ] = { 7, 3, 9, 13, 5, 4 }  
         Query1: l=1, r=4, k=6
         Query2: l=2, r=6, k=8

Output: 3
         2

For the first query, [7, 3, 9, 13] represents the 
subarray from index 1 till 4, in which there are 
3 numbers which are greater than k=6 that are {7, 9, 13}.

For the second query, there are only 
two numbers in the query range which
are greater than k.
```

**天真的方法**是通过简单地遍历数组从索引 l 到 r 来找到每个查询的答案，每当数组元素大于 k 时，就不断地给计数加 1。
**时间复杂度:** O(n*q)
A **更好的方法**是使用合并排序树。在这种方法中，构建一个分段树，在每个节点有一个向量，包含子范围中所有元素的排序顺序。使用段树回答每个查询，其中二分搜索法可用于计算子范围位于查询范围内的每个节点中存在多少大于 k 的数字。
**时间复杂度:** O(q * log(n) * log(n))
一种**高效方法**是使用离线查询和[分支树来解决问题。](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)以下是步骤:

*   首先将所有数组元素和查询存储在同一个数组中。为此，我们可以创建一个自结构或类。
*   然后按降序对结构数组进行排序(如果发生冲突，查询将首先出现，然后是数组元素)。
*   再次处理整个数组结构，但在此之前创建另一个位数组(二进制索引树)，其查询(I)函数将返回数组中所有元素的计数，直到第 I 个索引。
*   最初，用 0 填充整个数组。
*   创建一个答案数组，其中存储了每个查询的答案。
*   处理结构数组。
*   如果它是一个数组元素，那么用该元素索引中的+1 更新位数组。
*   如果是查询，则减去*查询(r)–查询(l-1)* ，这将是该查询的答案，该答案将存储在对应于查询号的索引处的答案数组中。
*   最后输出答案数组。

这里的关键观察是，由于结构的数组已经按降序排序。每当我们遇到任何查询时，只有大于“k”的元素才构成位数组中的计数，这就是所需要的答案。
以下是程序中使用的结构说明:

> **Pos:** 存储查询顺序。在数组元素的情况下，它保持为 0。
> **L:** 存储查询的子阵列的起始索引。如果是数组元素，它也是 0。
> **R:** 存储查询的子数组的结束索引。在数组元素的情况下，它用于存储元素在数组中的位置。
> **Val:** 存储查询的‘k’和所有数组元素。

以下是上述方法的实现:

## C++

```
// C++ program to print the number of elements
// greater than k in a subarray of range L-R.
#include <bits/stdc++.h>
using namespace std;

// Structure which will store both
// array elements and queries.
struct node {
    int pos;
    int l;
    int r;
    int val;
};

// Boolean comparator that will be used
// for sorting the structural array.
bool comp(node a, node b)
{
    // If 2 values are equal the query will
    // occur first then array element
    if (a.val == b.val)
        return a.l > b.l;

    // Otherwise sorted in descending order.
    return a.val > b.val;
}

// Updates the node of BIT array by adding
// 1 to it and its ancestors.
void update(int* BIT, int n, int idx)
{
    while (idx <= n) {
        BIT[idx]++;
        idx += idx & (-idx);
    }
}
// Returns the count of numbers of elements
// present from starting till idx.
int query(int* BIT, int idx)
{
    int ans = 0;
    while (idx) {
        ans += BIT[idx];

        idx -= idx & (-idx);
    }
    return ans;
}

// Function to solve the queries offline
void solveQuery(int arr[], int n, int QueryL[],
                int QueryR[], int QueryK[], int q)
{
    // create node to store the elements
    // and the queries
    node a[n + q + 1];
    // 1-based indexing.

    // traverse for all array numbers
    for (int i = 1; i <= n; ++i) {
        a[i].val = arr[i - 1];
        a[i].pos = 0;
        a[i].l = 0;
        a[i].r = i;
    }

    // iterate for all queries
    for (int i = n + 1; i <= n + q; ++i) {
        a[i].pos = i - n;
        a[i].val = QueryK[i - n - 1];
        a[i].l = QueryL[i - n - 1];
        a[i].r = QueryR[i - n - 1];
    }

    // In-built sort function used to
    // sort node array using comp function.
    sort(a + 1, a + n + q + 1, comp);

    // Binary Indexed tree with
    // initially 0 at all places.
    int BIT[n + 1];

    // initially 0
    memset(BIT, 0, sizeof(BIT));

    // For storing answers for each query( 1-based indexing ).
    int ans[q + 1];

    // traverse for numbers and query
    for (int i = 1; i <= n + q; ++i) {
        if (a[i].pos != 0) {

            // call function to returns answer for each query
            int cnt = query(BIT, a[i].r) - query(BIT, a[i].l - 1);

            // This will ensure that answer of each query
            // are stored in order it was initially asked.
            ans[a[i].pos] = cnt;
        }
        else {
            // a[i].r contains the position of the
            // element in the original array.
            update(BIT, n, a[i].r);
        }
    }
    // Output the answer array
    for (int i = 1; i <= q; ++i) {
        cout << ans[i] << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 7, 3, 9, 13, 5, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // 1-based indexing
    int QueryL[] = { 1, 2 };
    int QueryR[] = { 4, 6 };

    // k for each query
    int QueryK[] = { 6, 8 };

    // number of queries
    int q = sizeof(QueryL) / sizeof(QueryL[0]);

    // Function call to get
    solveQuery(arr, n, QueryL, QueryR, QueryK, q);

    return 0;
}
```

## 蟒蛇 3

```
# Python program to print the number of elements
# greater than k in a subarray of range L-R.

# Structure which will store both
# array elements and queries.
class node:
    def __init__(self):
        self.pos = 0
        self.l = 0
        self.r = 0
        self.val = 0

# Updates the node of BIT array by adding
# 1 to it and its ancestors.
def update(BIT: list, n: int, idx: int):
    while idx <= n:
        BIT[idx] += 1
        idx += idx & -idx

# Returns the count of numbers of elements
# present from starting till idx.
def query(BIT: list, idx: int) -> int:
    ans = 0
    while idx:
        ans += BIT[idx]
        idx -= idx & -idx
    return ans

# Function to solve the queries offline
def solveQuery(arr: list, n: int, QueryL: list,
                QueryR: list, QueryK: list, q: int):

    # create node to store the elements
    # and the queries
    a = [0] * (n + q + 1)
    for i in range(n + q + 1):
        a[i] = node()

    # 1-based indexing

    # traverse for all array numbers
    for i in range(1, n + 1):
        a[i].val = arr[i - 1]
        a[i].pos = 0
        a[i].l = 0
        a[i].r = i

    # iterate for all queries
    for i in range(n + 1, n + q + 1):
        a[i].pos = i - n
        a[i].val = QueryK[i - n - 1]
        a[i].l = QueryL[i - n - 1]
        a[i].r = QueryR[i - n - 1]

    # In-built sorted function used to
    # sort node array using comp function.
    a = [a[0]] + sorted(a[1:],
        key = lambda k: (k.val, k.l),
        reverse = True)

    # Binary Indexed tree with
    # initially 0 at all places.
    BIT = [0] * (n + 1)

    # For storing answers for
    # each query( 1-based indexing ).
    ans = [0] * (q + 1)

    # traverse for numbers and query
    for i in range(1, n + q + 1):
        if a[i].pos != 0:

            # call function to returns answer for each query
            cnt = query(BIT, a[i].r) - query(BIT, a[i].l - 1)

            # This will ensure that answer of each query
            # are stored in order it was initially asked.
            ans[a[i].pos] = cnt
        else:

            # a[i].r contains the position of the
            # element in the original array.
            update(BIT, n, a[i].r)

    # Output the answer array
    for i in range(1, q + 1):
        print(ans[i])

# Driver Code
if __name__ == "__main__":

    arr = [7, 3, 9, 13, 5, 4]
    n = len(arr)

    # 1-based indexing
    QueryL = [1, 2]
    QueryR = [4, 6]

    # k for each query
    QueryK = [6, 8]

    # number of queries
    q = len(QueryL)

    # Function call to get
    solveQuery(arr, n, QueryL, QueryR, QueryK, q)

# This code is contributed by
# sanjeev2552
```

**Output:** 

```
3
2
```

**时间复杂度:** O(N * log N)其中 N =(N+q)
T3】什么是离线查询？
在一些问题中，很难以任何随机的顺序回答查询。因此，与其单独回答每个查询，不如存储所有查询，然后对它们进行相应的排序，以便有效地为它们计算答案。存储所有答案，然后按照最初给出的顺序输出。
该技术称为*离线查询*。
**注意:**也可以使用段树代替分支树，其中段树的每个节点将存储插入的元素数量，直到该迭代。更新和查询功能将会改变，其余的实现将保持不变。
**离线查询的必要条件:**只有当一个查询的答案不依赖于前一个查询的答案时，才能使用该技术，因为排序后查询的顺序可能会改变。