# 使用维护对象的算法查询值在 A 到 B 范围内的元素

> 原文:[https://www . geeksforgeeks . org/查询具有使用 mos 算法的 a 到 b 范围内的值的元素/](https://www.geeksforgeeks.org/queries-for-elements-having-values-within-the-range-a-to-b-using-mos-algorithm/)

**先决条件:** [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)、 [SQRT 分解](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)
给定一个由 **N** 个元素和两个整数 **A** 到 **B** 组成的数组**arr【】**对于每个查询，找到子数组**arr【L】中的元素个数**

**示例:**

> **输入:** arr[] = {3，4，6，2，7，1}，A = 1，B = 6，查询= {0，4}
> **输出:** 4
> **解释:**
> 所有 3，4，6，2 都位于子阵列{3，4，6，2}
> 中的 1 到 6 之间，因此，此类元素的计数为 4。
> 
> **输入:** arr[] = {0，1，2，3，4，5，6，7}，A = 1，B = 5，查询= {3，5}
> **输出:** 3
> **解释:**
> 所有元素 3，4 和 5 都位于子阵列{3，4，5}中的 1 到 5 范围内。
> 因此，此类元素的计数为 3。

**方法:**想法是使用 [MO 的算法](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/)对所有查询进行预处理，以便一个查询的结果可以用于下一个查询。下面是步骤的图示:

1.  将查询分组到多个块中，其中每个块包含起始范围为(0 到√N–1)、(√N 到 2x√N–1)等的值。按照 **R** 的递增顺序对块内的查询进行排序。
2.  逐个处理所有查询，每个查询都使用上一个查询中计算的结果。
3.  当 arr[i]出现在范围[L，R]内时，保持对 arr[I]频率进行计数的频率阵列。

**例如:**

> arr[] = [3，4，6，2，7，1]，L = 0，R = 4 和 A = 1，B = 6
> 最初将频率数组初始化为 0，即 freq[]=[0…0]
> **步骤 1:** 添加 arr[0]，并将其频率增加为 freq[arr[0]]+
> 即 freq[3]++和 freq[]=[0，0，0，1，0，0，0]
> **步骤 2: 0]
> **步骤 3:** 添加 arr[2]并增加 freq[arr[2]]+
> 即 freq[6]++和 freq[]=[0，0，0，1，1，0，1，0]
> **步骤 4:** 添加 arr[3]并增加 freq[arr[3]]+
> 即 freq[2]++和 freq[]=[0，0，1，1，1**

为了在**步骤 7**中计算总和，我们不能进行迭代，因为这会导致每个查询的 **O(N)** 时间复杂度。所以我们将使用 [**平方根分解技术**](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/) 来寻找和，每个查询的时间复杂度为 **O(√N)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// values in the range A to B
// in a subarray of L to R

#include <bits/stdc++.h>
using namespace std;

#define MAX 100001
#define SQRSIZE 400

// Variable to represent block size.
// This is made global so compare()
// of sort can use it.
int query_blk_sz;

// Structure to represent a query range
struct Query {
    int L;
    int R;
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
    if (x.L / query_blk_sz
        != y.L / query_blk_sz)
        return (x.L / query_blk_sz
                < y.L / query_blk_sz);

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
int getans(int A, int B)
{
    int ans = 0;
    int left_blk, right_blk;
    left_blk = getblocknumber(A);
    right_blk = getblocknumber(B);

    // If left block is equal to right block
    // then we can traverse that block
    if (left_blk == right_blk) {
        for (int i = A; i <= B; i++)
            ans += frequency[i];
    }
    else {
        // Traversing first block in
        // range
        for (int i = A;
             i < (left_blk + 1) * blk_sz;
             i++)
            ans += frequency[i];

        // Traversing completely overlapped
        // blocks in range
        for (int i = left_blk + 1;
             i < right_blk; i++)
            ans += blocks[i];

        // Traversing last block in range
        for (int i = right_blk * blk_sz;
             i <= B; i++)
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
                  Query q[], int m,
                  int A, int B)
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

        int L = q[i].L, R = q[i].R;

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
        printf("%d\n", getans(A, B));
    }
}

// Driver code
int main()
{

    int arr[] = { 3, 4, 6, 2, 7, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    int A = 1, B = 6;
    blk_sz = sqrt(N);
    Query Q[] = { { 0, 4 } };

    int M = sizeof(Q) / sizeof(Q[0]);

    // Answer the queries
    queryResults(arr, N, Q, M, A, B);

    return 0;
}
```

**Output:** 

```
4
```

**时间复杂度:**O(Q *√N)
T3】空间复杂度: O(N)