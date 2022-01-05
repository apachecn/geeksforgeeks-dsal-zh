# 使用位集

在一个范围内进行子集和查询

> 原文:[https://www . geesforgeks . org/subset-sum-query-in-range-use-bit set/](https://www.geeksforgeeks.org/subset-sum-queries-in-a-range-using-bitset/)

给定一个由 **N** 个正整数和 **M** 个查询组成的数组[]。每个查询由两个整数组成 **L** 和 **R** 用一个范围表示。对于每个查询，找出位于给定范围内的数字的计数，该计数可以表示为给定数组的任何子集的和。

**先决条件:** [使用位集](https://www.geeksforgeeks.org/subset-sum-queries-using-bitset/)
的子集和查询**示例:**

> **输入:** arr[] = { 1，2，2，3，5 }，M = 4
> L = 1，R = 2
> L = 1，R = 5
> L = 3，R = 6
> L = 9，R = 30
> **输出:**T9】2
> 5
> 4
> 5
> **解释:**对于第一个查询，在范围【1，2】内所有数字 I。对于第二个查询，在范围[1，5]中，所有数字，即 1，2，3，4 和 5，可以表示为子集和，1 表示为 1，2 表示为 2，3 表示为 3，4 表示为 2 + 2 或 1 + 3，5 表示为 5。对于第三个查询，在范围[3，6]中，所有数字，即 3，4，5 和 6，都可以表示为子集和。对于最后一个查询，只有数字 9、10、11、12、13 可以表示为子集和，9 表示为 5 + 2 + 2，10 表示为 5 + 2 + 2 + 1，11 表示为 5 + 3 + 2 + 1，12 表示为 5 + 3 + 2 + 2，13 表示为 5 + 3 + 2 + 2 + 1。

**方法:**想法是使用一个位集并迭代数组来表示所有可能的子集和。位集的当前状态是通过将位集的先前状态左移 X 次来对其进行“或”来定义的，其中 X 是数组中当前处理的元素。为了在 O(1)时间内回答查询，我们可以预计算到每个数字的数字计数，对于一个范围[L，R]，答案将是**pre[R]–pre[L–1]**，其中 pre[]是预计算的数组。

下面是上述方法的实现。

```
// CPP Program to answer subset
// sum queries in a given range
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1001;
bitset<MAX> bit;

// precomputation array
int pre[MAX];

// structure to represent query
struct que {
    int L, R;
};

void answerQueries(int Q, que Queries[], int N,
                   int arr[])
{
    // Setting bit at 0th position as 1
    bit[0] = 1;
    for (int i = 0; i < N; i++)
        bit |= (bit << arr[i]);

    // Precompute the array
    for (int i = 1; i < MAX; i++)
        pre[i] = pre[i - 1] + bit[i];

    // Answer Queries
    for (int i = 0; i < Q; i++) {
        int l = Queries[i].L;
        int r = Queries[i].R;
        cout << pre[r] - pre[l - 1] << endl;
    }
}

// Driver Code to test above function
int main()
{
    int arr[] = { 1, 2, 2, 3, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 4;
    que Queries[M];
    Queries[0].L = 1, Queries[0].R = 2;
    Queries[1].L = 1, Queries[1].R = 5;
    Queries[2].L = 3, Queries[2].R = 6;
    Queries[3].L = 9, Queries[3].R = 30;
    answerQueries(M, Queries, N, arr);
    return 0;
}
```

**Output:**

```
2
5
4
5

```

**时间复杂度:**每个查询都可以在 O(1)时间内回答，预计算需要 O(MAX)时间。