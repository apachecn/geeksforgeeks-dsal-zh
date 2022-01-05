# 找到包含 Q 查询给定元素的最小范围大小

> 原文:[https://www . geeksforgeeks . org/find-包含给定元素的最小范围大小-用于 q 查询/](https://www.geeksforgeeks.org/find-the-minimum-range-size-that-contains-the-given-element-for-q-queries/)

给定一个由 **N** 对整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **间隔[]** ，其中每对整数表示值范围**【L，R】**。另外，给定一个由 **M** 查询组成的整数[数组](https://www.geeksforgeeks.org/array-data-structure/) **Q[]** 。对于每个查询，任务是找到包含该元素的最小范围的大小。如果不存在有效间隔，返回 **-1** 。

**示例**

> **输入:**区间[] = [[1，4]，[2，3]，[3，6]，[9，25]，[7，15]，[4，4]]
> Q[] = [7，50，2]
> **输出:** [9，-1，2]
> **解释:**元素 7 仅在[7，15]范围内因此，答案将为 15–7+1 = 8。元素 50 不在范围内。因此，答案将是-1。
> 同样，元素 2 在[2，3]和[1，4]的范围内，但最小的范围是[2，3]因此，答案将是 3-2+1 = 2。
> 
> **输入:**间隔[] = [[1，4]，[2，4]，[3，6]]
> Q[] = [2，3]
> **输出:**【3，3】

**天真方法:**解决问题最简单的方法是迭代数组**范围[]** ，并为每个查询找到包含给定元素的最小范围。

***时间复杂度:** O(N×M)*
***辅助空间:** O(M)*

**高效方法:**使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)可以进一步优化上述方法。按照以下步骤解决问题:

*   初始化一个向量向量，说出**查询**，将所有查询连同其索引一起插入到[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **Q** 中。
*   使用向量的默认[排序功能对向量**间隔**和**查询**进行排序。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，说 **pq** ，键为区间大小，值为范围的右边界。
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**结果**，它将存储每个查询的最小范围的大小。
*   初始化一个整数变量，比如说 **i** ，它将保持数组中遍历元素的轨迹**间隔**。
*   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)****【0，M-1】**中迭代，并执行以下步骤:

    *   当**I<interval . size()**和**interval[I][0]<= query[j][0]**时迭代，将**-(interval[I][1]–interval[I][0]+1)、interval[I][1]**作为一对，并将 **i** 的值增加 **1** 。
    *   现在从[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) **pq** 中移除所有元素，右元素小于**查询【j】【0】**。
    *   如果[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) **pq > 0** 的大小，则将**结果【查询[j][1]】**的值修改为**pq . top()【0】**。** 
*   **返回[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【RES】作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the size of minimum
// Interval that contains the given element
vector<int> minInterval(vector<vector<int> >& intervals,
                        vector<int>& q)
{
    // Store all the queries
    // along with their index
    vector<vector<int> > queries;

    for (int i = 0; i < q.size(); i++)
        queries.push_back({ q[i], i });

    // Sort the vector intervals and queries
    sort(intervals.begin(), intervals.end());
    sort(queries.begin(), queries.end());

    // Max priority queue to keep track
    // of intervals size and right value
    priority_queue<vector<int> > pq;

    // Stores the result of all the queries
    vector<int> result(queries.size(), -1);

    // Current position of intervals
    int i = 0;

    for (int j = 0; j < queries.size(); j++) {

        // Stores the current query
        int temp = queries[j][0];

        // Insert all the intervals whose left value
        // is less than or equal to the current query
        while (i < intervals.size()
               && intervals[i][0] <= temp) {

            // Insert the negative of range size and
            // the right bound of the interval
            pq.push(
                { -intervals[i][1] + intervals[i][0] - 1,
                  intervals[i++][1] });
        }

        // Pop all the intervals with right value
        // less than the current query
        while (!pq.empty() && temp > pq.top()[1]) {
            pq.pop();
        }

        // Check if the valid interval exists
        // Update the answer for current query
        // in result array
        if (!pq.empty())
            result[queries[j][1]] = -pq.top()[0];
    }
    // Return the result array
    return result;
}

// Driver Code
int main()
{
    // Given Input
    vector<vector<int> > intervals
        = { { 1, 4 }, { 2, 3 }, { 3, 6 }, { 9, 25 }, { 7, 15 }, { 4, 4 } };
    vector<int> Q = { 7, 50, 2, 3, 4, 9 };

    // Function Call
    vector<int> result = minInterval(intervals, Q);

    // Print the result for each query
    for (int i = 0; i < result.size(); i++)
        cout << result[i] << " ";
    return 0;
}
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to find the size of minimum
// Interval that contains the given element
function minInterval(intervals, q)
{
    // Store all the queries
    // along with their index
    var queries = [];

    for (var i = 0; i < q.length; i++)
        queries.push([q[i], i]);

    // Sort the vector intervals and queries
    intervals.sort((a,b)=> {
            if(a[0] == b[0])
                return a[1] - b[1];
            return a[0] - b[0];
        });
    queries.sort((a,b)=> {
            if(a[0] == b[0])
                return a[1]-b[1];
            return a[0]-b[0];
        });

    // Max priority queue to keep track
    // of intervals size and right value
    var pq = [];

    // Stores the result of all the queries
    var result = Array(queries.length).fill(-1);

    // Current position of intervals
    var i = 0;

    for (var j = 0; j < queries.length; j++) {

        // Stores the current query
        var temp = queries[j][0];

        // Insert all the intervals whose left value
        // is less than or equal to the current query
        while (i < intervals.length
               && intervals[i][0] <= temp) {

            // Insert the negative of range size and
            // the right bound of the interval
            pq.push(
                [ -intervals[i][1] + intervals[i][0] - 1,
                  intervals[i++][1] ]);
        }
        pq.sort((a,b)=> {
            if(a[0] == b[0])
                return a[1]-b[1];
            return a[0]-b[0];
        });

        // Pop all the intervals with right value
        // less than the current query
        while (pq.length != 0 && temp > pq[pq.length-1][1]) {
            pq.pop();
        }

        // Check if the valid interval exists
        // Update the answer for current query
        // in result array
        if (pq.length!=0)
            result[queries[j][1]] = -pq[pq.length-1][0];
    }
    // Return the result array
    return result;
}

// Driver Code
// Given Input
var intervals
    = [ [ 1, 4 ], [ 2, 3 ], [ 3, 6 ], [ 9, 25 ], [ 7, 15 ], [ 4, 4 ] ];
var Q = [ 7, 50, 2, 3, 4, 9 ];

// Function Call
var result = minInterval(intervals, Q);

// Print the result for each query
for (var i = 0; i < result.length; i++)
    document.write(result[i] + " ");

// This code is contributed by rrrtnx.
</script>
```

****Output**

```
9 -1 2 2 1 9 
```** 

*****时间复杂度:**O(NlogN+MlogM)*
T5**辅助空间** : O(N+M)**