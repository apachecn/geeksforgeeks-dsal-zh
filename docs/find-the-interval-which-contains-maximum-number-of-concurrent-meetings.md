# 找出包含最大并发会议数的时间间隔

> 原文:[https://www . geeksforgeeks . org/find-包含最大并发会议数的时间间隔/](https://www.geeksforgeeks.org/find-the-interval-which-contains-maximum-number-of-concurrent-meetings/)

给定二维数组 **arr[][]** 的维度 **N * 2** ，其中包含给定日期的 **N** 会议的开始和结束时间。任务是打印一个时间段列表，在此期间可以举行大多数并发会议。

**例:**

> **输入:** arr[][] = {{100，300}，{145，215}，{200，230}，{215，300}，{215，400}，{500，600}，{600，700}}
> **输出:**【215，230】
> **解释:**
> 给定的 5 次会议在{215，T3 }重叠
> 
> **输入:** arr[][] = {{100，200}，{50，300}，{300，400}}
> **输出:**【100，200】

**方法:**思路是用一个 [Min-Heap](https://www.geeksforgeeks.org/binary-heap/) 来解决这个问题。以下是步骤:

1.  [根据会议开始时间对数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。
2.  初始化一个**最小堆**。
3.  初始化变量 **max_len** 、 **max_start** 和 **max_end** ，分别存储最小堆的最大大小、并发会议的开始时间和结束时间。
4.  [迭代排序后的数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并不断从 **min_heap** 弹出，直到 *arr[i][0]* 变得小于 **min_heap** 的元素，即弹出所有结束时间小于当前会议开始时间的会议，并将 *arr[i][1]* 推入 **min_heap** 。
5.  如果 min_heap 的大小超过 **max_len** ，则更新 **max_len = size(min_heap)** 、 **max_start = meetings[i][0]** 和 **max_end = min_heap_element。**
6.  返回 **max_start** 和 **max_end** 的值。

以下是上述方法的实现:

## C++14

```
// C++14 implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

bool cmp(vector<int> a,vector<int> b)
{

    if(a[0] != b[0])
        return a[0] < b[0];

    return a[1] - b[1];
}

// Function to find time slot of
// maximum concurrent meeting
void maxConcurrentMeetingSlot(
    vector<vector<int>> meetings)
{

    // Sort array by
    // start time of meeting
    sort(meetings.begin(), meetings.end(), cmp);

    // Declare Minheap
    priority_queue<int, vector<int>,
                       greater<int>> pq;

    // Insert first meeting end time
    pq.push(meetings[0][1]);

    // Initialize max_len,
    // max_start and max_end
    int max_len = 0, max_start = 0;
    int max_end = 0;

    // Traverse over sorted array
    // to find required slot
    for(auto k : meetings)
    {

        // Pop all meetings that end
        // before current meeting
        while (pq.size() > 0 &&
                    k[0] >= pq.top())
            pq.pop();

        // Push current meeting end time
        pq.push(k[1]);

        // Update max_len, max_start
        // and max_end if size of
        // queue is greater than max_len
        if (pq.size() > max_len)
        {
            max_len = pq.size();
            max_start = k[0];
            max_end = pq.top();
        }
    }

    // Print slot of maximum
    // concurrent meeting
    cout << max_start << " " << max_end;
}

// Driver Code
int main()
{

    // Given array of meetings
    vector<vector<int>> meetings = { { 100, 200 },
                                     { 50, 300 },
                                     { 300, 400 } };

    // Function call
    maxConcurrentMeetingSlot(meetings);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find time slot of
    // maximum concurrent meeting
    static void maxConcurrentMeetingSlot(
        int[][] meetings)
    {

        // Sort array by
        // start time of meeting
        Arrays.sort(meetings,
                    (a, b)
                        -> (a[0] != b[0])
                               ? a[0] - b[0]
                               : a[1] - b[1]);

        // Declare Minheap
        PriorityQueue<Integer> pq
            = new PriorityQueue<>();

        // Insert first meeting end time
        pq.add(meetings[0][1]);

        // Initialize max_len,
        // max_start and max_end
        int max_len = 0, max_start = 0;
        int max_end = 0;

        // Traverse over sorted array
        // to find required slot
        for (int[] k : meetings) {

            // Pop all meetings that end
            // before current meeting
            while (!pq.isEmpty()
                   && k[0] >= pq.peek())
                pq.poll();

            // Push current meeting end time
            pq.add(k[1]);

            // Update max_len, max_start
            // and max_end if size of
            // queue is greater than max_len
            if (pq.size() > max_len) {
                max_len = pq.size();
                max_start = k[0];
                max_end = pq.peek();
            }
        }

        // Print slot of maximum
        // concurrent meeting
        System.out.println(
            max_start + " " + max_end);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array of meetings
        int meetings[][]
            = { { 100, 200 },
                { 50, 300 },
                { 300, 400 } };

        // Function Call
        maxConcurrentMeetingSlot(meetings);
    }
}
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to find time slot of
    // maximum concurrent meeting
function maxConcurrentMeetingSlot(meetings)
{
    // Sort array by
        // start time of meeting
        meetings.sort(function(a, b){return (a[0] != b[0])
                               ? a[0] - b[0]
                               : a[1] - b[1]});

        // Declare Minheap
        let pq = [];

        // Insert first meeting end time
        pq.push(meetings[0][1]);
          pq.sort(function(a,b){return a-b;});
        // Initialize max_len,
        // max_start and max_end
        let max_len = 0, max_start = 0;
        let max_end = 0;

        // Traverse over sorted array
        // to find required slot
        for (let k=0;k< meetings.length;k++) {

            // Pop all meetings that end
            // before current meeting
            while (pq.length!=0
                   && meetings[k][0] >= pq[0])
                pq.shift();

            // Push current meeting end time
            pq.push(meetings[k][1]);
              pq.sort(function(a,b){return a-b;});
            // Update max_len, max_start
            // and max_end if size of
            // queue is greater than max_len
            if (pq.length > max_len) {
                max_len = pq.length;
                max_start = meetings[k][0];
                max_end = pq[0];
            }
        }

        // Print slot of maximum
        // concurrent meeting
        document.write(
            max_start + " " + max_end+"<br>");
}

// Driver Code
let meetings
= [[ 100, 200 ],
[ 50, 300 ],
[ 300, 400 ]];

// Function Call
maxConcurrentMeetingSlot(meetings);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
100 200
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(N)*