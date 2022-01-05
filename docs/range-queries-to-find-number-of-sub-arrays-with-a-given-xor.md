# 通过给定的异或运算查找子阵列数量的范围查询

> 原文:[https://www . geesforgeks . org/range-query-to-find-number-of-sub-array-with-给定-xor/](https://www.geeksforgeeks.org/range-queries-to-find-number-of-sub-arrays-with-a-given-xor/)

给定大小为 **n** 和 **q** 查询的数组**arr【】**和整数 **k** 。每个查询由一个索引范围**【l，r】**组成，任务是统计索引对 **i** 和 **j** 的数量，使得 **l ≤ i ≤ j ≤ r** (基于 1 的索引)和元素 **a[i]，a[i + 1]，…，a[j]** 的异或等于 **k** 。

**示例:**

> **输入:** arr[] = {1，1，1，0，2，3}，q[] = {{2，6}}，k = 3
> **输出:** 2
> {1，0，2}和{3}是索引范围【2，6】(基于 1 的索引)内所需的子数组
> 
> **输入:** arr[] = {1，1，1}，q[] = {{1，3}，{1，1}，{1，2}}，k = 1
> **输出:**
> 4
> 1
> 2

**方法:** [**这篇文章**](https://www.geeksforgeeks.org/count-number-subarrays-given-xor/) 讨论了在每个查询中寻找具有给定的 0(n)异或的子数组，因此如果 q 很大，我们的总运行时间复杂度将是 0(n * q)。
既然给我们离线查询，想法就是用莫的算法。我们将数组划分为 sqrt(n)个块，并根据块索引对查询进行排序，首先用较少的 r 值断开连接。
我们将保留一个数组 xorr[]，其中 xorr[i]存储从 0 到 I(基于索引 0)的数组元素前缀的 xor。
我们还将保留另一个数组 cnt[]，其中 cnt[y]存储带有 xorr[i] = k 的前缀数量。
假设，我们在索引 x 处添加一个元素，让 xorr[x] ^ k = y，现在如果 cnt[y]大于 0，则存在带有相同 xor 的前缀，因此我们得到在索引 x 处结束的带有给定 xor k 的 y 子数组。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const long long bsz = 316;
long long res = 0;

// Query structure
struct Query {
    long long l, r, q_idx, block_idx;

    Query() {}
    Query(long long _l, long long _r, long long _q_idx)
    {
        l = _l, r = _r, q_idx = _q_idx, block_idx = _l / bsz;
    }

    // We use operator overloading
    // to sort the queries
    bool operator<(const Query& y) const
    {
        if (block_idx != y.block_idx)
            return block_idx < y.block_idx;
        return r < y.r;
    }
};

Query queries[1000005];
unordered_map<long long, long long> cnt;
long long n, q, k;
long long xorr[1000005];

// Function to add elements while traversing
void add(long long u)
{
    long long y = xorr[u] ^ k;

    // We find the number of prefixes with value y
    // that are contributing to the answer,
    // add them to the answer
    res = res + cnt[y];

    // If we are performing add operation, and suppose
    // we are at index u then count of xorr[u]
    // will increase by 1 as we are adding
    // the answer to the list
    cnt[xorr[u]]++;
}

// Function to delete elements while traversing
void del(long long u)
{
    // If we are performing delete operation and suppose
    // we are at index u then count of xorr[u]
    // will decrease by 1 as we are removing
    // the answer from the list
    cnt[xorr[u]]--;
    long long y = xorr[u] ^ k;

    // We find the number of prefixes with value y
    // that was initially contributing to the answer
    // now we do not need them, hence subtract it from answer
    res = res - cnt[y];
}

// Here we are performing Mo's algorithm
// if you have no idea of it then go through here:
// https:// www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/
void Mo()
{
    // first we sort the queries with block index, and ties are broken by less r value .
    sort(queries + 1, queries + q + 1);
    vector<long long> ans(q + 1);
    long long l = 1, r = 0;
    res = 0;
    cnt[0] = 1;

    // Iterate each query and check whether
    // we have to move the left and right pointer
    // to left or right
    for (long long i = 1; i <= q; ++i) {

        // If current right pointer r is less than
        // the rightmost index of the present query,
        // increment r
        while (r < queries[i].r) {
            ++r;

            // While incrementing we are adding new numbers
            // to our list. Hence, we modify our answer
            // for each r using add() function
            add(r);
        }

        // If current left pointer is greater than the
        // left most index of the present query, decrement l
        while (l > queries[i].l) {
            l--;

            // While decrementing l, we are again adding
            // new numbers to our list, hence we modify
            // our answer using add() function
            add(l - 1);
        }

        // Similarly, if current left pointer is less than
        // the left most index of the present query, increment l
        while (l < queries[i].l) {

            // While incrementing we are deleting elements
            // as we are moving right, hence we modify our answer
            // using del() function
            del(l - 1);
            ++l;
        }

        // If current right pointer is greater than the rightmost
        // index of the present query, decrement it
        while (r > queries[i].r) {

            // While decrementing, modify the answer
            del(r);
            --r;
        }
        ans[queries[i].q_idx] = res;
    }
    for (long long i = 1; i <= q; ++i) {
        cout << ans[i] << endl;
    }
}

// Driver code
int main()
{
    q = 3, k = 3;
    vector<long long> v;
    v.push_back(0);
    v.push_back(1);
    v.push_back(1);
    v.push_back(1);
    v.push_back(0);
    v.push_back(2);
    v.push_back(3);

    // 1-based indexing
    n = v.size() + 1;

    xorr[1] = v[1];
    for (long long i = 2; i <= n; ++i)
        xorr[i] = xorr[i - 1] ^ v[i];

    // Queries
    queries[1] = Query(1, 6, 1);
    queries[2] = Query(2, 4, 2);
    queries[3] = Query(2, 6, 3);

    Mo();

    return 0;
}
```

**Output:**

```
3
0
2

```

**时间复杂度:** O((n + q) * sqrt(n))