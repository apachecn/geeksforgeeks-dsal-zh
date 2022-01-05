# 区间数组中的第 k 个最小元素

> 原文:[https://www . geesforgeks . org/kth-区间数组中的最小元素/](https://www.geeksforgeeks.org/kth-smallest-element-from-an-array-of-intervals/)

给定一个间隔为**的[数组](https://www.geeksforgeeks.org/array-data-structure/)，大小为 **N** ，任务是在给定数组的间隔内的所有元素中找到 **K <sup>th</sup>** 最小的元素。**

**示例:**

> **输入:** arr[] = {{5，11}，{10，15}，{12，20}}，K =12
> **输出:** 13
> **说明:**给定区间数组中的元素为:{5，6，7，8，9，10，10，11，11，12，12，13，13，14，15，15，16，17，18
> 因此，K <sup>第</sup> (=12 <sup>第</sup>)个最小元素为 13。
> 
> **输入:** arr[] = {{5，11}，{10，15}，{12，20}}，K = 7
> **输出:** 10

**天真方法:**最简单的方法是从区间数组中生成一个包含所有元素的新数组。[整理新阵](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。最后，返回阵列的第 [K <sup>个</sup>最小元素。](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)

**时间复杂度:** O(X*Log(X))，其中 **X** 为区间内元素总数。
**辅助空间:** O(X*log(X))

**高效途径:**对上述途径进行优化，思路是使用 [MinHeap](https://www.geeksforgeeks.org/binary-heap/) 。按照以下步骤解决问题。

1.  创建一个 [MinHeap](https://www.geeksforgeeks.org/binary-heap/) ，比如 **pq** 来存储给定数组的所有区间，这样它就返回 O(1)中剩余区间的所有元素中的最小元素。
2.  从 **MinHeap** 弹出最小间隔，检查弹出间隔的最小元素是否小于弹出间隔的最大元素。如果发现为真，则插入新的间隔**{弹出间隔的最小元素+ 1，弹出间隔的最大元素}** 。
3.  重复上述步骤**K–1**次。
4.  最后，返回弹出间隔的最小元素。

下面是上述方法的实现:

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the Kth smallest
// element from an array of intervals
int KthSmallestNum(pair<int, int> arr[],
                   int n, int k)
{

    // Store all the intervals so that it
    // returns the minimum element in O(1)
    priority_queue<pair<int, int>,
                   vector<pair<int, int> >,
                   greater<pair<int, int> > >
        pq;

    // Insert all Intervals into the MinHeap
    for (int i = 0; i < n; i++) {
        pq.push({ arr[i].first,
                  arr[i].second });
    }

    // Stores the count of
    // popped elements
    int cnt = 1;

    // Iterate over MinHeap
    while (cnt < k) {

        // Stores minimum element
        // from all remaining intervals
        pair<int, int> interval
            = pq.top();

        // Remove minimum element
        pq.pop();

        // Check if the minimum of the current
        // interval is less than the maximum
        // of the current interval
        if (interval.first < interval.second) {

            // Insert new interval
            pq.push(
                { interval.first + 1,
                  interval.second });
        }

        cnt++;
    }
    return pq.top().first;
}

// Driver Code
int main()
{
    // Intervals given
    pair<int, int> arr[]
        = { { 5, 11 },
            { 10, 15 },
            { 12, 20 } };

    // Size of the arr
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 12;

    cout << KthSmallestNum(arr, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.io.*;

class GFG{

// Function to get the Kth smallest
// element from an array of intervals
public static int KthSmallestNum(int arr[][], int n,
                                 int k)
{

    // Store all the intervals so that it
    // returns the minimum element in O(1)
    PriorityQueue<int[]> pq = new PriorityQueue<>(
                              (a, b) -> a[0] - b[0]);

    // Insert all Intervals into the MinHeap
    for(int i = 0; i < n; i++)
    {
        pq.add(new int[]{arr[i][0],
                         arr[i][1]});
    }

    // Stores the count of
    // popped elements
    int cnt = 1;

    // Iterate over MinHeap
    while (cnt < k)
    {

        // Stores minimum element
        // from all remaining intervals
        int[] interval = pq.poll();

        // Check if the minimum of the current
        // interval is less than the maximum
        // of the current interval
        if (interval[0] < interval[1])
        {

            // Insert new interval
            pq.add(new int[]{interval[0] + 1,
                             interval[1]});
        }
        cnt++;
    }
    return pq.peek()[0];
}

// Driver Code
public static void main(String args[])
{

    // Intervals given
    int arr[][] = { { 5, 11 },
                    { 10, 15 },
                    { 12, 20 } };

    // Size of the arr
    int n = arr.length;

    int k = 12;

    System.out.println(KthSmallestNum(arr, n, k));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get the Kth smallest
# element from an array of intervals
def KthSmallestNum(arr, n, k):

    # Store all the intervals so that it
    # returns the minimum element in O(1)
    pq = []

    # Insert all Intervals into the MinHeap
    for i in range(n):
        pq.append([arr[i][0], arr[i][1]])

    # Stores the count of
    # popped elements
    cnt = 1

    # Iterate over MinHeap
    while (cnt < k):

        # Stores minimum element
        # from all remaining intervals
        pq.sort(reverse = True)
        interval = pq[0]

        # Remove minimum element
        pq.remove(pq[0])

        # Check if the minimum of the current
        # interval is less than the maximum
        # of the current interval
        if (interval[0] < interval[1]):

            # Insert new interval
            pq.append([interval[0] + 1,
                       interval[1]])

        cnt += 1

    pq.sort(reverse = True)
    return pq[0][0] + 1

# Driver Code
if __name__ == '__main__':

    # Intervals given
    arr = [ [ 5, 11 ],
            [ 10, 15 ],
            [ 12, 20 ] ]

    # Size of the arr
    n = len(arr)

    k = 12

    print(KthSmallestNum(arr, n, k))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG {

    // Function to get the Kth smallest
    // element from an array of intervals
    static int KthSmallestNum(int[,] arr, int n, int k)
    {
        // Store all the intervals so that it
        // returns the minimum element in O(1)
        ArrayList pq = new ArrayList();

        // Insert all Intervals into the MinHeap
        for(int i = 0; i < n; i++)
        {
            pq.Add(new Tuple<int,int>(arr[i,0], arr[i,1]));
        }

        // Stores the count of
        // popped elements
        int cnt = 1;

        // Iterate over MinHeap
        while (cnt < k)
        {
            // Stores minimum element
            // from all remaining intervals
            pq.Sort();
            pq.Reverse();
            Tuple<int,int> interval = (Tuple<int,int>)pq[0];

            // Remove minimum element
            pq.RemoveAt(0);

            // Check if the minimum of the current
            // interval is less than the maximum
            // of the current interval
            if (interval.Item1 < interval.Item2)
            {
                // Insert new interval
                pq.Add(new Tuple<int,int>(interval.Item1 + 1, interval.Item2));
            }
            cnt += 1;
        }
        pq.Sort();
        pq.Reverse();
        return ((Tuple<int,int>)pq[0]).Item1 + 1;
    }

  // Driver code
  static void Main()
  {

    // Intervals given
    int[,] arr = { { 5, 11 },
            { 10, 15 },
            { 12, 20 } };

    // Size of the arr
    int n = arr.GetLength(0);
    int k = 12;
    Console.WriteLine(KthSmallestNum(arr, n, k));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to get the Kth smallest
// element from an array of intervals
function KthSmallestNum(arr, n, k)
{
    // Store all the intervals so that it
    // returns the minimum element in O(1)
    var pq = [];

    // Insert all Intervals into the MinHeap
    for(var i = 0; i < n; i++)
    {
        pq.push([arr[i][0], arr[i][1]]);
    }

    // Stores the count of
    // popped elements
    var cnt = 1;

    // Iterate over MinHeap
    while (cnt < k)
    {
        // Stores minimum element
        // from all remaining intervals
        pq.sort((a,b)=>{
        if(a[0]==b[0])
            return a[1]-b[1]
        return a[0]-b[0]
        });
        var interval = pq[0];

        // Remove minimum element
        pq.shift();

        // Check if the minimum of the current
        // interval is less than the maximum
        // of the current interval
        if (interval[0] < interval[1])
        {
            // Insert new interval
            pq.push([interval[0] + 1, interval[1]]);
        }
        cnt += 1;
    }
    pq.sort((a,b) =>
    {
        if(a[0]==b[0])
            return a[1]-b[1]
        return a[0]-b[0]
    });
    return (pq[0])[0];
}

 // Driver code
// Intervals given
var arr = [ [ 5, 11 ],
        [ 10, 15 ],
        [ 12, 20 ] ];

// Size of the arr
var n = arr.length;
var k = 12;
document.write(KthSmallestNum(arr, n, k));

</script>
```

**Output:** 

```
13
```

***时间复杂度:** O(K*logK)*
***辅助空间:** O(N)*