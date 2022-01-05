# 子阵中小于或等于一个数的元素个数:MO 的算法

> 原文:[https://www . geesforgeks . org/元素数量-小于或等于子数组中的一个数字-mos-算法/](https://www.geeksforgeeks.org/number-of-elements-less-than-or-equal-to-a-number-in-a-subarray-mos-algorithm/)

给定一个 L、R 和 X 形式的数组**arr****N**和 **Q** 查询，任务是打印 L 到 R 表示的子数组中小于或等于 X 的元素数量

**先决条件:** [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)[Sqrt 分解](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)

**示例:**

```
Input: 
arr[] = {2, 3, 4, 5}
Q = {{0, 3, 5}, {0, 2, 2}}
Output:
 4
 1
Explanation:
Number of elements less than or equal to 5
in arr[0..3] is 4 (all elements)

Number of elements less than or equal to 2 
in arr[0..2] is 1 (only 2)
```

**方法:**
MO 算法的思想是对所有查询进行预处理，使得一个查询的结果可以用于下一个查询。
让 **arr[0…n-1]** 为输入数组， **Q[0..m-1]** 是查询的数组。

1.  对所有查询进行排序，将从 **0 到√n–1**的 L 值查询放在一起，然后将从 **√n 到 2×√n–1**的所有查询放在一起，依此类推。一个块中的所有查询都按照 R 值的递增顺序进行排序。
2.  逐个处理所有查询，每个查询都使用上一个查询中计算的结果。
3.  我们将保持**频率阵列**，当 arr[i]出现在范围[L，R]中时，该频率阵列将对 arr[I]的频率进行计数。
4.  **例如:** arr[]=[3，4，6，2，7，1]，L=0，R=4，X=5

> 最初，频率数组被初始化为 0，即 freq[]=[0…0]
> **第 1 步**–添加 arr[0]，并将其频率增加为 freq[arr[0]]++即 freq[3]+【T3]和 freq[]=[0，0，0，1，0，0，0，0]
> **第 2 步**–添加 arr[1]，并增加 freq[arr[1]]+，即 freq[4]+
> 和 freq 0]
> **步骤 4**–添加 arr[3]并增加 freq[arr[3]]++即 freq[2]+
> 和 freq[]=[0，0，1，1，1，0，1，0]
> **步骤 5**–添加 arr[4]并增加 freq[arr[4]]++即 freq[7]+
> 和 freq[]=[0，0，1，1，1
> **第 7 步**–答案等于![\sum_{i=0}^{X} freq[i]   ](img/e2ee671453f962c0e227770d20d6c810.png "Rendered by QuickLaTeX.com")
> 为了计算第 7 步中的**和，我们不能进行迭代，因为这样会导致每个查询的时间复杂度为 O(N)，所以我们将使用 **sqrt 分解技术**来寻找每个查询的**时间复杂度为 O(√n)的和**。**

## C++

```
// C++ program to answer queries to
// count number of elements smaller
// than or equal to x.
#include <bits/stdc++.h>
using namespace std;

#define MAX 100001
#define SQRSIZE 400

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
int query_blk_sz;

// Structure to represent a
// query range
struct Query {

    int L;
    int R;
    int x;
};

// Frequency array
// to keep count of elements
int frequency[MAX];

// Array which contains the frequency
// of a particular block
int blocks[SQRSIZE];

// Block size
int blk_sz;

// Function used to sort all queries
// so that all queries of the same
// block are arranged together and
// within a block, queries are sorted
// in increasing order of R values.
bool compare(Query x, Query y)
{
    if (x.L / query_blk_sz !=
        y.L / query_blk_sz)
        return x.L / query_blk_sz <
               y.L / query_blk_sz;

    return x.R < y.R;
}

// Function used to get the block
// number of current a[i] i.e ind
int getblocknumber(int ind)
{
    return (ind) / blk_sz;
}

// Function to get the answer
// of range [0, k] which uses the
// sqrt decomposition technique
int getans(int k)
{
    int ans = 0;
    int left_blk, right_blk;
    left_blk = 0;
    right_blk = getblocknumber(k);

    // If left block is equal to
    // right block then we can traverse
    // that block
    if (left_blk == right_blk) {
        for (int i = 0; i <= k; i++)
            ans += frequency[i];
    }
    else {
        // Traversing first block in
        // range
        for (int i = 0; i <
             (left_blk + 1) * blk_sz; i++)
            ans += frequency[i];

        // Traversing completely overlapped
        // blocks in range
        for (int i = left_blk + 1;
             i < right_blk; i++)
            ans += blocks[i];

        // Traversing last block in range
        for (int i = right_blk * blk_sz;
             i <= k; i++)
            ans += frequency[i];
    }
    return ans;
}

void add(int ind, int a[])
{
    // Increment the frequency of a[ind]
    // in the frequency array
    frequency[a[ind]]++;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]++;
}
void remove(int ind, int a[])
{
    // Decrement the frequency of
    // a[ind] in the frequency array
    frequency[a[ind]]--;

    // Get the block number of a[ind]
    // to update the result in blocks
    int block_num = getblocknumber(a[ind]);

    blocks[block_num]--;
}
void queryResults(int a[], int n,
                  Query q[], int m)
{

    // Initialize the block size
    // for queries
    query_blk_sz = sqrt(m);

    // Sort all queries so that queries
    // of same blocks are arranged
    // together.
    sort(q, q + m, compare);

    // Initialize current L,
    // current R and current result
    int currL = 0, currR = 0;

    for (int i = 0; i < m; i++) {

        // L and R values of the
        // current range

        int L = q[i].L, R = q[i].R,
                x = q[i].x;

        // Add Elements of current
        // range
        while (currR <= R) {
            add(currR, a);
            currR++;
        }
        while (currL > L) {
            add(currL - 1, a);
            currL--;
        }

        // Remove element of previous
        // range
        while (currR > R + 1)

        {
            remove(currR - 1, a);
            currR--;
        }
        while (currL < L) {
            remove(currL, a);
            currL++;
        }
        printf("query[%d, %d, %d] : %d\n",
               L, R, x, getans(x));
    }
}
// Driver code
int main()
{

    int arr[] = { 2, 0, 3, 1, 4, 2, 5, 11 };
    int N = sizeof(arr) / sizeof(arr[0]);

    blk_sz = sqrt(N);
    Query Q[] = { { 0, 2, 2 }, { 0, 3, 5 },
                { 5, 7, 10 } };

    int M = sizeof(Q) / sizeof(Q[0]);

    // Answer the queries
    queryResults(arr, N, Q, M);
    return 0;
}
```

**Output:** 

```
query[0, 2, 2] : 2
query[0, 3, 5] : 4
query[5, 7, 10] : 2
```

**时间复杂度:** **O(Q × √N)** 。
MO 的算法需要 O(Q × √N)时间，sqrt 分解技术需要 O(Q × √N)时间来求解 freq[0]+…。freq[k]，因此总时间复杂度为 O(Q × √N + Q × √N)，也就是 O(Q × √N)。