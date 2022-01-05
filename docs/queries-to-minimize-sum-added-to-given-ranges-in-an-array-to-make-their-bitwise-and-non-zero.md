# 最小化添加到数组中给定范围的和的查询，以使它们的按位与非零

> 原文:[https://www . geeksforgeeks . org/查询-最小化数组中给定范围的相加和-使其按位非零/](https://www.geeksforgeeks.org/queries-to-minimize-sum-added-to-given-ranges-in-an-array-to-make-their-bitwise-and-non-zero/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，一个由 **{l，r}** 个查询组成的数组 **Q[][]** 。对于每个查询 **{l，r}** ，任务是确定必须添加到该范围内每个数组元素的所有值的最小和，以便该范围内所有数字的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)超过 **0** 。
**注:**给定范围内不同的整数可以加不同的值。

**示例:**

> **输入:** arr[] = {1，2，4，8}，Q[][] = {{1，4}，{2，3}，{1，3}}
> **输出:**3 2 2
> T6】解释:数组元素的二进制表示如下:
> 1–0001
> 2–0010
> 4–0100
> 8–1000
> 对于第一个查询{1，T0 因此，按位 AND = (1 & 3 & 5 & 9) = 1，相加元素的最小和= 3。
> 对于第二个查询{2，3}，添加 2 到第三个元素。因此，按位 AND = (2 & 6) = 2，相加元素的最小和= 2。
> 对于第三个查询{1，3}，添加 1 到第二个和第三个元素。因此，按位 AND = (1 & 3 & 5) = 1，相加元素的最小和= 2。
> 
> **输入:** arr[] = {4，6，5，3}，Q[][] = {{1，4}}
> **输出:** 1
> **解释:**使按位 AND 非零的最佳方式是在最后一个元素上加 1。因此，按位 AND = (4 & 6 & 5 & 4) = 4，相加元素的最小和= 1。

**方法:**首先观察范围内所有整数的**位与****【l，r】**只能是**非零**如果为该范围内的每个整数设置了特定索引的位。
按照以下步骤解决问题:

1.  初始化一个 [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/) pre，其中**pre【I】【j】**存储从索引 **0** 到索引 **i** 的所有整数相加的最小整数和，使得对于它们中的每一个，它们的 **j <sup>第</sup>** 位被设置。
2.  对于索引 **i** 处的每个元素，检查其从 **j = 0 到 31** 的每个位。
3.  用 **0** 初始化变量**和**。
4.  如果设置了**j**位，则将 **pre[i][j]** 更新为 **pre[i][j]=pre[i-1][j]** ，并将总和增加 **2 <sup>j</sup>** 。否则，更新**pre[I][j]= pre[I-1][j]+2<sup>j</sup>–sum**，其中 **(2 <sup>j</sup> -sum)** 是设置**arr【I】**的 **j <sup>第</sup>** 位必须加上的值。
5.  现在，对于每个查询 **{l，r}** ，在给定范围内设置所有元素的 **j <sup>第</sup>T5】位所需的最小和是**pre[r][j]–pre[l-1][j]**。**
6.  对于每个查询 **{l，r}** ，从 **j = 0 到 31** 找到每个位的答案，并打印其中的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the min sum required
// to set the jth bit of all integer
void processing(vector<int> v,
                vector<vector<long long int> >& pre)
{

    // Number of elements
    int N = v.size();

    // Traverse all elements
    for (int i = 0; i < N; i++) {

        // Binary representation
        bitset<32> b(v[i]);

        long long int sum = 0;

        // Take previous values
        if (i != 0) {

            pre[i] = pre[i - 1];
        }

        // Processing each bit and
        // store it in 2d vector
        for (int j = 0; j < 32; j++) {

            if (b[j] == 1) {

                sum += 1ll << j;
            }
            else {

                pre[i][j]
                    += (1ll << j) - sum;
            }
        }
    }
}

// Function to print the minimum
// sum for each query
long long int
process_query(vector<vector<int> > Q,
              vector<vector<long long int> >& pre)
{

    // Stores the sum for each query
    vector<int> ans;

    for (int i = 0; i < Q.size(); i++) {

        // Update wrt 0-based index
        --Q[i][0], --Q[i][1];

        // Initizlize answer
        long long int min1 = INT_MAX;

        // Find minimum sum for each bit
        if (Q[i][0] == 0) {

            for (int j = 0; j < 32; j++) {

                min1 = min(pre[Q[i][1]][j], min1);
            }
        }
        else {

            for (int j = 0; j < 32; j++) {

                min1 = min(pre[Q[i][1]][j]
                               - pre[Q[i][0] - 1][j],
                           min1);
            }
        }

        // Store the answer for
        // each query
        ans.push_back(min1);
    }

    // Print the answer vector
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 1, 2, 4, 8 };

    // Given Queries
    vector<vector<int> > Q
        = { { 1, 4 }, { 2, 3 }, { 1, 3 } };

    // 2d Prefix vector
    vector<vector<long long int> > pre(
        100001, vector<long long int>(32, 0));

    // Preprocessing
    processing(arr, pre);

    // Function call for queries
    process_query(Q, pre);

    return 0;
}
```

**Output:** 

```
3 2 2
```

***时间复杂度:**O(N * 32+sizeof(Q)* 32)*
***辅助空间:** O(N*32)*