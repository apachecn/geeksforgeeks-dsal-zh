# 根据给定的投票系统找出谁赢得了选举

> 原文:[https://www . geeksforgeeks . org/find-谁赢得了选举-基于给定投票系统/](https://www.geeksforgeeks.org/find-who-won-the-election-based-on-given-voting-system/)

给定形式为 **{X，Y}** 的成对 **arr[][]** 的[数组](https://www.geeksforgeeks.org/array-data-structure/),使得每个 **arr[i]** 表示具有候选 ID **Y** 的候选人被投票的时间 **X** ，以及由 **M** 正整数组成的查询**查询[**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，每个查询的任务**Q【I**

**注意:**如果在给定时间内有 2 名候选人获得相同票数 **K** ，那么先打印获得这些票数的候选人。

**示例:**

> **输入:** arr[] = {{1，2}、{2，2}、{4，1}、{5，5}、{7，1}、{11，1}}，查询[] = {2，8，12}
> **输出:**2 2 1
> T6】解释:T8】对于查询[0] = 2，在时间 2，候选人 candidateID = 2 已获得最高票数。
> 对于查询[1] = 8，在时间 8，候选人 ID 为 2 和 1 的候选人获得了最大票数，即 2，但是由于候选人 ID 为 2 的候选人之前获得了这些票数，因此答案是 2。
> 对于查询[2] = 12，在时间 12，候选人 candidateID = 1 获得最大票数，即 3 票。
> 
> **输入:** arr[] = {{1，1}}，查询[]= { 1 }
> T3】输出: 1

**方法:**给定的问题可以通过在数组**arr【】**中的每个即将到来的时间间隔预计算获胜者并将其存储在另一个数组中来解决，以 **{timeInterval，winnerCandidateID}** 的形式说出**Ans【】**，然后对于每个查询**查询【I】**在数组**Ans【】**上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)以在时间**查询【I】获得获胜候选按照以下步骤解决问题:**

*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)，比如 **Ans[]** ，该向量存储每个输入时间间隔的获胜者 **arr[i]。首先**。
*   [初始化一个无序的地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如说**地图【】**，存储候选人的 ID 在每个进入时间间隔的频率。
*   [初始化一对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)，比如说**上一个【】**保持对获胜候选人的跟踪。
*   [推矢量中的第一对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **Ans[]** ，并标记为前一对。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**，并执行以下步骤:
    *   增加当前候选**arr【I】的频率。第二张**由 **1** 中的**地图**组成。
    *   如果当前候选人赢到现在，则更新上一对**。**
    *   **[在向量中插入先前的](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/) **Ans[]** 。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M)** ，并执行以下步骤:

    *   对于每个查询，在成对的 **和**的[向量上执行二分搜索法运算，以找到获胜的候选项。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
    *   对时间即向量对的第一个值**Ans【】**进行二分搜索法运算，找到小于等于**的最大值查询【**I**】**，打印对应的 **candidateID** 。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to perform binary search
// to find the candidate with most votes
// for a particular time
int binarySearch(vector<pair<int, int> >& Ans,
                 int low, int high, int value)
{
    // Base Cases
    if (value <= Ans[low].first)
        return Ans[low].second;
    if (value >= Ans[high].first)
        return Ans[high].second;

    int winningCandidate;

    while (low <= high) {

        // Find the mid
        int mid = low + (high - low) / 2;

        // If the value at mid is the
        // result
        if (Ans[mid].first == value) {
            winningCandidate
                = Ans[mid].second;
            break;
        }

        // Update the ranges
        else if (Ans[mid].first < value) {
            winningCandidate
                = Ans[mid].second;
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }

    return winningCandidate;
}

// Function to find the winner for each query
void findWinner(pair<int, int> arr[],
                int N, int query[],
                int M)
{

    // Map to store the frequency
    unordered_map<int, int> Map;

    // Stores the winning candidate till
    // a particular time
    vector<pair<int, int> > Ans;

    // Starting Reference
    pair<int, int> previous
        = { arr[0].first, arr[0].second };
    Ans.push_back(previous);
    Map[arr[0].second]++;

    // Iterate over the range
    for (int i = 1; i < N; i++) {

        // Increase the frequency
        Map[arr[i].second]++;

        // Update the reference if another
        // candidate gets more votes than
        // the one considered
        if (Map[arr[i].second]
            > Map[previous.second]) {
            previous.second = arr[i].second;
        }

        previous.first = arr[i].first;

        // Push into the vector
        Ans.push_back(previous);
    }

    // Iterate over the range
    for (int i = 0; i < M; i++) {
        cout << binarySearch(
                    Ans, 0, N - 1, query[i])
             << ' ';
    }
}

// Driver Code
int main()
{
    pair<int, int> arr[]
        = { { 1, 2 }, { 2, 2 }, { 4, 1 },
            { 5, 5 }, { 7, 1 }, { 11, 1 } };
    int query[] = { 2, 8, 12 };
    int N = 6;
    int M = 3;

    findWinner(arr, N, query, M);

    return 0;
}
```

****Output:**

```
2 2 1

```** 

*****时间复杂度:** O(max(N，M * log(N))*
***辅助空间:** O(N)***