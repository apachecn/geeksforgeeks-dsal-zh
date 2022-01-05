# 求 k 个排序数组中的第 m 个最小值

> 原文:[https://www . geeksforgeeks . org/find-m-th-k 中最小值排序数组/](https://www.geeksforgeeks.org/find-m-th-smallest-value-in-k-sorted-arrays/)

给定 k 个可能大小不同的排序数组，在合并后的数组中找到第 m 个最小值。
示例:

```
Input: m = 5     
      arr[][] = { {1, 3},
                  {2, 4, 6},
                  {0, 9, 10, 11}} ;
Output: 4
Explanation The merged array would
be {0 1 2 3 4 6 9 10 11}.  The 5-th 
smallest element in this merged
array is 4.

Input: m = 2
      arr[][] = { {1, 3, 20},
                  {2, 4, 6}} ;
Explanation The merged array would
be {1 2 3 4 6 20}. The 2nd smallest element would be 2\. 
Output: 2
```

一个**简单的解决方案**是创建一个输出数组，然后一个接一个地将所有数组复制到其中。最后，使用对输出数组进行排序。这种方法需要 O(N ^ Logn ^ N)个时间，其中 N 是所有元素的计数。
一个**高效的解决方案**是使用堆数据结构。基于堆的解决方案的时间复杂度为 O(m ^ Log k)。
1。创建一个 k 大小的最小堆，并将所有数组中的第一个元素插入到堆中
2。重复以下步骤 m 次
…..a)从堆中移除最小元素(最小值总是在根)，并将其存储在输出数组中。
…..b)从提取元素的数组中插入下一个元素。如果数组没有更多的元素，那么什么也不要做。
3。打印最后删除的项目。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find m-th smallest element
// in the merged arrays.
#include <bits/stdc++.h>
using namespace std;

// A pair of pairs, first element is going to
// store value, second element index of array
// and third element index in the array.
typedef pair<int, pair<int, int> > ppi;

// This function takes an array of arrays as an
// argument and all arrays are assumed to be
// sorted. It returns m-th smallest element in
// the array obtained after merging the given
// arrays.
int mThLargest(vector<vector<int> > arr, int m)
{
    // Create a min heap with k heap nodes. Every
    // heap node has first element of an array
    priority_queue<ppi, vector<ppi>, greater<ppi> > pq;

    for (int i = 0; i < arr.size(); i++)
        pq.push({ arr[i][0], { i, 0 } });

    // Now one by one get the minimum element
    // from min heap and replace it with next
    // element of its array
    int count = 0;
    int i = 0, j = 0;
    while (count < m && pq.empty() == false) {
        ppi curr = pq.top();
        pq.pop();

        // i ==> Array Number
        // j ==> Index in the array number
        i = curr.second.first;
        j = curr.second.second;

        // The next element belongs to same array as
        // current.
        if (j + 1 < arr[i].size())
            pq.push({ arr[i][j + 1], { i, j + 1 } });

        count++;
    }

    return arr[i][j];
}

// Driver program to test above functions
int main()
{
    vector<vector<int> > arr{ { 2, 6, 12 },
                              { 1, 9 },
                              { 23, 34, 90, 2000 } };

    int m = 4;
    cout << mThLargest(arr, m);

    return 0;
}
```

**Output:** 

```
9
```