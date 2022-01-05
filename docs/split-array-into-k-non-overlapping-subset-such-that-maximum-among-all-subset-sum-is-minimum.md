# 将数组拆分成 K 个不重叠子集，使得所有子集和中的最大值最小

> 原文:[https://www . geesforgeks . org/split-array-in-k-non-重叠-subset-so-all-subset-sum-is-minimum/](https://www.geeksforgeeks.org/split-array-into-k-non-overlapping-subset-such-that-maximum-among-all-subset-sum-is-minimum/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是将给定的数组拆分成 **K 个不重叠的子集**，使得所有子集之和的最大值最小。

**示例:**

> **输入:** arr[] = {1，7，9，2，12，3，3}，M = 3
> **输出:** 13
> **解释:**
> 将数组吐为 3 个不重叠子集的一种可能方式是{arr[4]，arr[0]}，{arr[2]，arr[6]}，以及{arr[1]，arr[5]，arr[3]}。
> 每个子集的和分别为 13、12 和 12。现在，所有子集的和中的最大值是 13，这是最小可能的和。
> 
> **输入:** arr[] = {1，2，3，4，5}，M = 2
> T3】输出: 8

**方法:**给定问题可以通过[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)和[排序给定数组](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。按照以下步骤解决问题:

*   使用[优先级队列](https://www.geeksforgeeks.org/implement-min-heap-using-stl/)初始化一个[最小堆](https://www.geeksforgeeks.org/binary-heap/)，比如 **PQ** 来存储每组元素的总和。
*   在**【1，K】**范围内迭代，将 **0** 推入 **PQ** 。
*   [对数组进行排序， **arr[]** 按降序排列](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[i]** ，将元素 **arr[i]** 添加到最小和组，该组将位于优先级队列 **PQ** 的[顶部。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
*   完成上述步骤后，打印优先级队列的最后一个元素 **PQ** ，作为所有可能组中最小化的最大和的结果。

下面是上述方法的实现:

+++++

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the array into M
// groups such that maximum of the sum
// of all elements of all the groups
// is minimized
int findMinimumValue(int arr[], int N,
                     int M)
{
    // Sort the array in decreasing order
    sort(arr, arr + N, greater<int>());

    // Initialize priority queue (Min heap)
    priority_queue<int, vector<int>,
                   greater<int> >
        pq;

    // Push 0 for all the M groups
    for (int i = 1; i <= M; ++i) {
        pq.push(0);
    }

    // Traverse the array, arr[]
    for (int i = 0; i < N; ++i) {

        // Pop the group having the
        // minimum sum
        int val = pq.top();
        pq.pop();

        // Increment val by arr[i]
        val += arr[i];

        // Push the new sum of the
        // group into the pq
        pq.push(val);
    }

    // Iterate while size of the pq
    // is greater than 1
    while (pq.size() > 1) {
        pq.pop();
    }

    // Return result
    return pq.top();
}

// Driver Code
int main()
{
    int arr[] = { 1, 7, 9, 2, 12, 3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;
    cout << findMinimumValue(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to split the array into M
    // groups such that maximum of the sum
    // of all elements of all the groups
    // is minimized
    static int findMinimumValue(Vector<Integer> arr, int N, int M)
    {

        // Sort the array in decreasing order
        Collections.sort(arr);
        Collections.reverse(arr);

        // Initialize priority queue (Min heap)
        Vector<Integer> pq = new Vector<Integer>();

        // Push 0 for all the M groups
        for (int i = 1; i <= M; ++i) {
            pq.add(0);
        }

        Collections.sort(pq);

        // Traverse the array, arr[]
        for (int i = 0; i < N; ++i) {

            // Pop the group having the
            // minimum sum
            int val = pq.get(0);
            pq.remove(0);

            // Increment val by arr[i]
            val += arr.get(i);

            // Push the new sum of the
            // group into the pq
            pq.add(val);
            Collections.sort(pq);
        }

        // Iterate while size of the pq
        // is greater than 1
        while (pq.size() > 1) {
            pq.remove(0);
        }

        // Return result
        return pq.get(0);
    }

    public static void main(String[] args) {
        Integer[] arr = { 1, 7, 9, 2, 12, 3, 3 };
        Vector<Integer> Arr = new Vector<Integer>();
        Collections.addAll(Arr, arr);
        int N = Arr.size();
        int K = 3;
        System.out.println(findMinimumValue(Arr, N, K));
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split the array into M
# groups such that maximum of the sum
# of all elements of all the groups
# is minimized
def findMinimumValue(arr, N, M):

    # Sort the array in decreasing order
    arr.sort()
    arr.reverse()

    # Initialize priority queue (Min heap)
    pq = []

    # Push 0 for all the M groups
    for i in range(1, M + 1):
        pq.append(0)

    pq.sort()

    # Traverse the array, arr[]
    for i in range(N):

        # Pop the group having the
        # minimum sum
        val = pq[0]
        del pq[0]

        # Increment val by arr[i]
        val += arr[i]

        # Push the new sum of the
        # group into the pq
        pq.append(val)
        pq.sort()

    # Iterate while size of the pq
    # is greater than 1
    while (len(pq) > 1) :
        del pq[0]

    # Return result
    return pq[0]

arr = [ 1, 7, 9, 2, 12, 3, 3 ]
N = len(arr)
K = 3
print(findMinimumValue(arr, N, K))

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to split the array into M
    // groups such that maximum of the sum
    // of all elements of all the groups
    // is minimized
    static int findMinimumValue(int[] arr, int N, int M)
    {

        // Sort the array in decreasing order
        Array.Sort(arr);
        Array.Reverse(arr);

        // Initialize priority queue (Min heap)
        List<int> pq = new List<int>();

        // Push 0 for all the M groups
        for (int i = 1; i <= M; ++i) {
            pq.Add(0);
        }

        pq.Sort();

        // Traverse the array, arr[]
        for (int i = 0; i < N; ++i) {

            // Pop the group having the
            // minimum sum
            int val = pq[0];
            pq.RemoveAt(0);

            // Increment val by arr[i]
            val += arr[i];

            // Push the new sum of the
            // group into the pq
            pq.Add(val);
            pq.Sort();
        }

        // Iterate while size of the pq
        // is greater than 1
        while (pq.Count > 1) {
            pq.RemoveAt(0);
        }

        // Return result
        return pq[0];
    }

  static void Main() {
    int[] arr = { 1, 7, 9, 2, 12, 3, 3 };
    int N = arr.Length;
    int K = 3;
    Console.Write(findMinimumValue(arr, N, K));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to split the array into M
    // groups such that maximum of the sum
    // of all elements of all the groups
    // is minimized
    function findMinimumValue(arr, N, M)
    {

        // Sort the array in decreasing order
        arr.sort(function(a, b){return a - b});
        arr.reverse();

        // Initialize priority queue (Min heap)
        let pq = [];

        // Push 0 for all the M groups
        for (let i = 1; i <= M; ++i) {
            pq.push(0);
        }

        pq.sort(function(a, b){return a - b});

        // Traverse the array, arr[]
        for (let i = 0; i < N; ++i) {

            // Pop the group having the
            // minimum sum
            let val = pq[0];
            pq.shift();

            // Increment val by arr[i]
            val += arr[i];

            // Push the new sum of the
            // group into the pq
            pq.push(val);
            pq.sort(function(a, b){return a - b});
        }

        // Iterate while size of the pq
        // is greater than 1
        while (pq.length > 1) {
            pq.shift();
        }

        // Return result
        return pq[0];
    }

    let arr = [ 1, 7, 9, 2, 12, 3, 3 ];
    let N = arr.length;
    let K = 3;
    document.write(findMinimumValue(arr, N, K));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(N*log K)*
***辅助空间:** O(M)*