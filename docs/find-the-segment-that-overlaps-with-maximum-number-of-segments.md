# 找到与最大线段数重叠的线段

> 原文:[https://www . geeksforgeeks . org/find-与最大段数重叠的段/](https://www.geeksforgeeks.org/find-the-segment-that-overlaps-with-maximum-number-of-segments/)

给定一个 [2D 阵列](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **线段[][]** ，其中每个线段都是代表 **(X，Y)** 坐标的**【L，R】**形式，任务是找到与最大数量的线段重叠的线段。

**示例:**

> **输入:**段[][] = {{1，4}，{2，3}，{3，6}}
> **输出:** : {3，6}
> **解释:**每个段与所有其他段重叠。因此，打印它们中的任何一个。
> 
> **输入:**分段[[]= { { 1，2}，{3，8}，{4，5}，{6，7}，{9，10}}
> **输出:** {3，8}
> **解释:**分段{3，8}与{4，5}和{6，7}重叠。

**方法:**按照以下步骤解决问题:

*   很明显，在一个片段**【currL，currR】**中，所有小于**【currL】**的剩余片段的**【R】**值和所有大于**【currR】**的剩余片段的**【L】**值都不会被计算到答案中。
*   将所有的**“R”**值存储在一个数组中，并执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来查找所有小于**“currL”**的**“R”**值，并类似地执行此操作来查找所有大于**“currR”**的**“L”**值。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在每次迭代时更新交点最大的线段坐标。
*   打印具有最大交点的线段。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the segment which
// overlaps with maximum number of segments
void maxIntersection(int segments[][2], int N)
{
    // 'L' & 'R' co-ordinates of all
    // segments are stored in lvalues & rvalues
    vector<int> rvalues(N), lvalues(N);

    // Assign co-ordinates
    for (int i = 0; i < N; ++i) {

        lvalues[i] = segments[i][0];
        rvalues[i] = segments[i][1];
    }

    // Co-ordinate compression
    sort(lvalues.begin(), lvalues.end());
    sort(rvalues.begin(), rvalues.end());

    // Stores the required segment
    pair<int, int> answer = { -1, -1 };

    // Stores the current maximum
    // number of intersections
    int numIntersections = 0;

    for (int i = 0; i < N; ++i) {

        // Find number of 'R' coordinates
        // which are less than the 'L'
        // value of the current segment
        int lesser
            = lower_bound(rvalues.begin(), rvalues.end(),
                          segments[i][0])
              - rvalues.begin();

        // Find number of 'L' coordinates
        // which are greater than the 'R'
        // value of the current segment
        int greater = max(
            0, N
                   - (int)(upper_bound(lvalues.begin(),
                                       lvalues.end(),
                                       segments[i][1])
                           - lvalues.begin()));

        // Segments excluding 'lesser' and
        // 'greater' gives the number of
        // intersections
        if ((N - lesser - greater) >= numIntersections) {
            answer = { segments[i][0], segments[i][1] };

            // Update the current maximum
            numIntersections = (N - lesser - greater);
        }
    }

    // Print segment coordinates
    cout << answer.first << " " << answer.second;
}

// Driver Code
int main()
{
    // Given segments
    int segments[][2] = { { 1, 4 }, { 2, 3 }, { 3, 6 } };

    // Size of segments array
    int N = sizeof(segments) / sizeof(segments[0]);

    maxIntersection(segments, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the segment which
// overlaps with maximum number of segments
static void maxIntersection(int segments[][], int N)
{

    // 'L' & 'R' co-ordinates of all
    // segments are stored in lvalues & rvalues
    int []rvalues = new int[N];
    int []lvalues = new int[N];

    // Assign co-ordinates
    for (int i = 0; i < N; ++i)
    {

        lvalues[i] = segments[i][0];
        rvalues[i] = segments[i][1];
    }

    // Co-ordinate compression
    Arrays.sort(lvalues);
    Arrays.sort(rvalues);

    // Stores the required segment
    int []answer = { -1, -1 };

    // Stores the current maximum
    // number of intersections
    int numIntersections = 0;
    for (int i = 0; i < N; ++i)
    {

        // Find number of 'R' coordinates
        // which are less than the 'L'
        // value of the current segment
        int lesser
            = lower_bound(rvalues, 0,
                          segments.length,
                          segments[i][0]);

        // Find number of 'L' coordinates
        // which are greater than the 'R'
        // value of the current segment
        int greater = Math.max(
            0, N-(upper_bound(lvalues, 0,
                              segments.length,
                              segments[i][1])));

        // Segments excluding 'lesser' and
        // 'greater' gives the number of
        // intersections
        if ((N - lesser - greater) >= numIntersections) {
            answer = new int[]{ segments[i][0], segments[i][1] };

            // Update the current maximum
            numIntersections = (N - lesser - greater);
        }
    }

    // Print segment coordinates
    System.out.print(answer[0]+ " " +  answer[1]);
}
static int lower_bound(int[] a, int low, int high, int element){
    while(low < high){
        int middle = low + (high - low)/2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

static int upper_bound(int[] a, int low, int high, int element){
    while(low < high){
        int middle = low + (high - low)/2;
        if(a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}
// Driver Code
public static void main(String[] args)
{
    // Given segments
    int segments[][] = { { 1, 4 }, { 2, 3 }, { 3, 6 } };

    // Size of segments array
    int N = segments.length;

    maxIntersection(segments, N);
}
}
// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the segment which
  // overlaps with maximum number of segments
  static void maxIntersection(int [,]segments, int N)
  {

    // 'L' & 'R' co-ordinates of all
    // segments are stored in lvalues & rvalues
    int []rvalues = new int[N];
    int []lvalues = new int[N];

    // Assign co-ordinates
    for (int i = 0; i < N; ++i)
    {
      lvalues[i] = segments[i,0];
      rvalues[i] = segments[i,1];
    }

    // Co-ordinate compression
    Array.Sort(lvalues);
    Array.Sort(rvalues);

    // Stores the required segment
    int []answer = { -1, -1 };

    // Stores the current maximum
    // number of intersections
    int numIntersections = 0;
    for (int i = 0; i < N; ++i)
    {

      // Find number of 'R' coordinates
      // which are less than the 'L'
      // value of the current segment
      int lesser
        = lower_bound(rvalues, 0,
                      segments.GetLength(0),
                      segments[i,0]);

      // Find number of 'L' coordinates
      // which are greater than the 'R'
      // value of the current segment
      int greater = Math.Max(
        0, N-(upper_bound(lvalues, 0,
                          segments.GetLength(0),
                          segments[i,1])));

      // Segments excluding 'lesser' and
      // 'greater' gives the number of
      // intersections
      if ((N - lesser - greater) >= numIntersections) {
        answer = new int[]{ segments[i,0], segments[i,1] };

        // Update the current maximum
        numIntersections = (N - lesser - greater);
      }
    }

    // Print segment coordinates
    Console.Write(answer[0]+ " " +  answer[1]);
  }
  static int lower_bound(int[] a, int low,
                         int high, int element)
  {
    while(low < high)
    {
      int middle = low + (high - low)/2;
      if(element > a[middle])
        low = middle + 1;
      else
        high = middle;
    }
    return low;
  }

  static int upper_bound(int[] a, int low,
                         int high, int element)
  {
    while(low < high)
    {
      int middle = low + (high - low)/2;
      if(a[middle] > element)
        high = middle;
      else
        low = middle + 1;
    }
    return low;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given segments
    int [,]segments = { { 1, 4 }, { 2, 3 }, { 3, 6 } };

    // Size of segments array
    int N = segments.GetLength(0);
    maxIntersection(segments, N);
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    function lower_bound(a , low , high , element) {
        while (low < high) {
            var middle = low + (high - low) / 2;
            if (element > a[middle])
                low = middle + 1;
            else
                high = middle;
        }
        return low;
    }

    function upper_bound(a , low , high , element) {
        while (low < high) {
            var middle = low + (high - low) / 2;
            if (a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Function to find the segment which
    // overlaps with maximum number of segments
    function maxIntersection(segments , N) {

        // 'L' & 'R' co-ordinates of all
        // segments are stored in lvalues & rvalues
        let rvalues = Array(N).fill(0);
        let lvalues = Array(N).fill(0);

        // Assign co-ordinates
        for (i = 0; i < N; ++i) {

            lvalues[i] = segments[i][0];
            rvalues[i] = segments[i][1];
        }

        // Co-ordinate compression
        lvalues.sort((a,b)=>a-b);
        rvalues.sort((a,b)=>a-b);

        // Stores the required segment
        let answer = [ -1, -1 ];

        // Stores the current maximum
        // number of intersections
        var numIntersections = 0;
        for (var i = 0; i < N; ++i) {

            // Find number of 'R' coordinates
            // which are less than the 'L'
            // value of the current segment
            var lesser = lower_bound(rvalues, 0,
            segments.length, segments[i][0]);

            // Find number of 'L' coordinates
            // which are greater than the 'R'
            // value of the current segment
            var greater = Math.max(0, N - (upper_bound(lvalues,
            0, segments.length, segments[i][1])));

            // Segments excluding 'lesser' and
            // 'greater' gives the number of
            // intersections
            if ((N - lesser - greater) >= numIntersections) {
                answer =   [ segments[i][0], segments[i][1] ];

                // Update the current maximum
                numIntersections = (N - lesser - greater);
            }
        }

        // Print segment coordinates
        document.write(answer[0] + " " + answer[1]);
    }

    // Driver Code

        // Given segments
        var segments = [ [ 1, 4 ], [ 2, 3 ], [ 3, 6 ] ];

        // Size of segments array
        var N = segments.length;

        maxIntersection(segments, N);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
3 6
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*