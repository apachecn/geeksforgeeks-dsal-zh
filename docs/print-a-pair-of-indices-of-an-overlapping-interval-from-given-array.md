# 打印给定数组中重叠区间的一对索引

> 原文:[https://www . geeksforgeeks . org/print-一对来自给定数组的重叠区间索引/](https://www.geeksforgeeks.org/print-a-pair-of-indices-of-an-overlapping-interval-from-given-array/)

给定一个大小为 **N** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】【】**，每行代表表格 **{X，Y}** ( *基于 1 的索引*)的区间，任务是找到一对重叠区间的索引。如果不存在这样的配对，则打印 **-1 -1** 。

**示例:**

> **输入:** N = 5，arr[][] = {{1，5}，{2，10}，{3，10}，{2，2}，{2，15}}
> **输出:** 4 1
> **解释:**位置 4 即(2，2)的范围位于位置 1 即(1，5)的范围内。
> 
> **输入:** N = 4，arr[][] = {{2，10}，{1，9}，{1，8}，{1，7}}
> **输出:** -1 -1

**天真的方法:**最简单的方法是检查每对间隔中是否有一个位于另一个的内部。如果没有找到这样的间隔，打印 **-1 -1** ，否则，打印找到的间隔的索引。
***时间复杂度:** O(N <sup>2</sup> )其中 N 为给定整数。*
***辅助空间:** O(N)*

**有效方法:**思路是[根据每个区间的左边部分给定区间集合](https://www.geeksforgeeks.org/sorting-algorithms/)排序。按照以下步骤解决问题:

1.  首先，[通过存储每个区间的索引，按左边框对段](https://www.geeksforgeeks.org/sorting-algorithms/)进行递增排序。
2.  然后，初始化变量 **curr** 和 **currPos** ，分别用排序数组中第一个区间的左边部分及其索引。
3.  现在，遍历从 **i = 0 到 N–1**的[排序的](https://www.geeksforgeeks.org/sorting-algorithms/)间隔。
4.  如果任意两个相邻间隔的左边部分相等，那么打印它们的索引，因为其中一个位于另一个的内部。
5.  如果当前区间的右边部分大于 **curr** ，则将 **curr** 设置为等于该右边部分，将 **currPos** 设置为等于原始数组中该区间的索引。否则，打印当前间隔的索引和存储在 **currPos** 变量中的索引。
6.  遍历后，如果没有找到这样的间隔，打印 **-1 -1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Pair of two integers
// of the form {X, Y}
typedef pair<int, int> ii;

// Pair of pairs and integers
typedef pair<ii, int> iii;

// FUnction to find a pair of indices of
// the overlapping interval in the array
ii segment_overlapping(int N,
                       vector<vector<int> > arr)
{

    // Store intervals {X, Y} along
    // with their indices
    vector<iii> tup;

    // Traverse the given intervals
    for (int i = 0; i < N; i++) {

        int x, y;
        x = arr[i][0];
        y = arr[i][1];

        // Store intervals and their indices
        tup.push_back(iii(ii(x, y), i + 1));
    }

    // Sort the intervals
    sort(tup.begin(), tup.end());

    // Stores Y of the first interval
    int curr = tup[0].first.second;

    // Stores index of first interval
    int currPos = tup[0].second;

    // Traverse the sorted intervals
    for (int i = 1; i < N; i++) {

        // Stores X value of previous interval
        int Q = tup[i - 1].first.first;

        // Stores X value of current interval
        int R = tup[i].first.first;

        // If Q and R equal
        if (Q == R) {

            // If Y value of immediate previous
            // interval is less than Y value of
            // current interval
            if (tup[i - 1].first.second
                < tup[i].first.second) {

                // Stores index of immediate
                // previous interval
                int X = tup[i - 1].second;

                // Stores index of current
                // interval
                int Y = tup[i].second;

                return { X, Y };
            }

            else {

                // Stores index of current
                // interval
                int X = tup[i].second;

                // Stores index of immediate
                // previous interval
                int Y = tup[i - 1].second;

                return { X, Y };
            }
        }

        // Stores Y value of current interval
        int T = tup[i].first.second;

        // T is less than or equal to curr
        if (T <= curr)
            return { tup[i].second, currPos };

        else {

            // Update curr
            curr = T;

            // Update currPos
            currPos = tup[i].second;
        }
    }

    // No answer exists
    return { -1, -1 };
}

// Driver Code
int main()

{

    // Given intervals
    vector<vector<int> > arr = { { 1, 5 }, { 2, 10 },
                                 { 3, 10 }, { 2, 2 },
                                 { 2, 15 } };

    // Size of intervals
    int N = arr.size();

    // Find answer
    ii ans = segment_overlapping(N, arr);

    // Print answer
    cout << ans.first << " " << ans.second;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;

// Pair of two integers
// of the form {X, Y}
class pair1
{
  int first, second;
  pair1(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}

// Pair of pairs and integers
class pair2
{
  int first, second, index;
  pair2(int first, int second, int index)
  {
    this.first = first;
    this.second = second;
    this.index = index;
  }
}
class GFG
{

  // Function to find a pair of indices of
  // the overlapping interval in the array
  static pair1 segment_overlapping(int N,
                                   int[][] arr)
  {

    // Store intervals {X, Y} along
    // with their indices
    ArrayList<pair2> tup=new ArrayList<>();

    // Traverse the given intervals
    for (int i = 0; i < N; i++)
    {

      int x, y;
      x = arr[i][0];
      y = arr[i][1];

      // Store intervals and their indices
      tup.add(new pair2(x, y, i + 1));
    }

    // Sort the intervals
    Collections.sort(tup, (a, b)->(a.first != b.first) ?
                     a.first - b.first:a.second - b.second);

    // Stores Y of the first interval
    int curr = tup.get(0).second;

    // Stores index of first interval
    int currPos = tup.get(0).index;

    // Traverse the sorted intervals
    for (int i = 1; i < N; i++)
    {

      // Stores X value of previous interval
      int Q = tup.get(i - 1).first;

      // Stores X value of current interval
      int R = tup.get(i).first;

      // If Q and R equal
      if (Q == R)
      {

        // If Y value of immediate previous
        // interval is less than Y value of
        // current interval
        if (tup.get(i - 1).second
            < tup.get(i).second)
        {

          // Stores index of immediate
          // previous interval
          int X = tup.get(i - 1).index;

          // Stores index of current
          // interval
          int Y = tup.get(i).index;

          return new pair1( X, Y );
        }

        else {

          // Stores index of current
          // interval
          int X = tup.get(i).index;

          // Stores index of immediate
          // previous interval
          int Y = tup.get(i - 1).index;

          return new pair1( X, Y );
        }
      }

      // Stores Y value of current interval
      int T = tup.get(i).second;

      // T is less than or equal to curr
      if (T <= curr)
        return new pair1( tup.get(i).index, currPos );

      else
      {

        // Update curr
        curr = T;

        // Update currPos
        currPos = tup.get(i).index;
      }
    }

    // No answer exists
    return new pair1(-1, -1 );
  }
  // Driver function
  public static void main (String[] args)
  {

    // Given intervals
    int[][] arr = { { 1, 5 }, { 2, 10 },
                   { 3, 10 }, { 2, 2 },
                   { 2, 15 } };

    // Size of intervals
    int N = arr.length;

    // Find answer
    pair1 ans = segment_overlapping(N, arr);

    // Print answer
    System.out.print(ans.first+" "+ans.second);
  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# FUnction to find a pair of indices of
# the overlapping interval in the array
def segment_overlapping(N, arr):

    # Store intervals {X, Y} along
    # with their indices
    tup = []

    # Traverse the given intervals
    for i in range(N):
        x = arr[i][0]
        y = arr[i][1]

        # Store intervals and their indices
        tup.append([x, y, i + 1])

    # Sort the intervals
    tup = sorted(tup)

    # Stores Y of the first interval
    curr = tup[0][1]

    # Stores index of first interval
    currPos = tup[0][2]

    # Traverse the sorted intervals
    for i in range(1, N):

        # Stores X value of previous interval
        Q = tup[i - 1][0]

        # Stores X value of current interval
        R = tup[i][0]

        # If Q and R equal
        if (Q == R):

            # If Y value of immediate previous
            # interval is less than Y value of
            # current interval
            if (tup[i - 1][1] < tup[i][1]):

                # Stores index of immediate
                # previous interval
                X = tup[i - 1][2]

                # Stores index of current
                # interval
                Y = tup[i][2]
                return [X, Y]
            else:

                # Stores index of current
                # interval
                X = tup[i][2]

                # Stores index of immediate
                # previous interval
                Y = tup[i - 1][2]
                return { X, Y }

        # Stores Y value of current interval
        T = tup[i][1]

        # T is less than or equal to curr
        if (T <= curr):
            return [tup[i][2], currPos]

        else:

            # Update curr
            curr = T

            # Update currPos
            currPos = tup[i][2]

    # No answer exists
    return [ -1, -1 ]

# Driver Code
if __name__ == '__main__':

    # Given intervals
    arr = [ [ 1, 5 ], [ 2, 10 ], [ 3, 10 ], [ 2, 2 ], [2, 15 ] ]

    # Size of intervals
    N = len(arr)

    # Find answer
    ans = segment_overlapping(N, arr)

    # Pranswer
    print(ans[0], ans[1])

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find a pair of indices of
// the overlapping interval in the array
static void segment_overlapping(int N, int[,] arr)
{

    // Store intervals {X, Y} along
    // with their indices
    List<Tuple<Tuple<int, int>,
                     int>> tup = new List<Tuple<Tuple<int, int>,
                                                      int>>();

    // Traverse the given intervals
    for(int i = 0; i < N; i++)
    {

        int x, y;
        x = arr[i, 0];
        y = arr[i, 1];

        // Store intervals and their indices
        tup.Add(new Tuple<Tuple<int, int>, int>(
                      new Tuple<int, int>(x, y), i + 1));
    }

    // Sort the intervals
    tup.Sort();

    // Stores Y of the first interval
    int curr = tup[0].Item1.Item2;

    // Stores index of first interval
    int currPos = tup[0].Item2;

    // Traverse the sorted intervals
    for(int i = 1; i < N; i++)
    {

        // Stores X value of previous interval
        int Q = tup[i - 1].Item1.Item1;

        // Stores X value of current interval
        int R = tup[i].Item1.Item1;

        // If Q and R equal
        if (Q == R)
        {

            // If Y value of immediate previous
            // interval is less than Y value of
            // current interval
            if (tup[i - 1].Item1.Item2 <
                tup[i].Item1.Item2)
            {

                // Stores index of immediate
                // previous interval
                int X = tup[i - 1].Item2;

                // Stores index of current
                // interval
                int Y = tup[i].Item2;

                Console.WriteLine(X + " " + Y);

                return;
            }

            else
            {

                // Stores index of current
                // interval
                int X = tup[i].Item2;

                // Stores index of immediate
                // previous interval
                int Y = tup[i - 1].Item2;

                Console.WriteLine(X + " " + Y);

                return;
            }
        }

        // Stores Y value of current interval
        int T = tup[i].Item1.Item2;

        // T is less than or equal to curr
        if (T <= curr)
        {
            Console.Write(tup[i].Item2 + " " + currPos);
            return;
        }
        else
        {

            // Update curr
            curr = T;

            // Update currPos
            currPos = tup[i].Item2;
        }
    }

    // No answer exists
    Console.Write("-1 -1");
}

// Driver code
static public void Main()
{

    // Given intervals
    int[,] arr = { { 1, 5 }, { 2, 10 },
                   { 3, 10 }, { 2, 2 },
                   { 2, 15 } };

    // Size of intervals
    int N = arr.Length / 2;

    segment_overlapping(N, arr);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// FUnction to find a pair of indices of
// the overlapping interval in the array
function segment_overlapping(N, arr)
{

    // Store intervals {X, Y} along
    // with their indices
    var tup = [];

    // Traverse the given intervals
    for (var i = 0; i < N; i++) {

        var x, y;
        x = arr[i][0];
        y = arr[i][1];

        // Store intervals and their indices
        tup.push([[x, y], i + 1]);
    }

    // Sort the intervals
    tup.sort((a,b) =>
    {
       if(a[0][0] == b[0][0])
       {
           return a[0][1] - b[0][1];
       }

       var tmp = (a[0][0] - b[0][0]);
       console.log(tmp);

       return (a[0][0] - b[0][0])
    });

    // Stores Y of the first interval
    var curr = tup[0][0][1];

    // Stores index of first interval
    var currPos = tup[0][1];

    // Traverse the sorted intervals
    for (var i = 1; i < N; i++) {

        // Stores X value of previous interval
        var Q = tup[i - 1][0][0];

        // Stores X value of current interval
        var R = tup[i][0][0];

        // If Q and R equal
        if (Q == R) {

            // If Y value of immediate previous
            // interval is less than Y value of
            // current interval
            if (tup[i - 1][0][1]
                < tup[i][0][1]) {

                // Stores index of immediate
                // previous interval
                var X = tup[i - 1][1];

                // Stores index of current
                // interval
                var Y = tup[i][1];

                return [X, Y];
            }

            else {

                // Stores index of current
                // interval
                var X = tup[i][1];

                // Stores index of immediate
                // previous interval
                var Y = tup[i - 1][1];

                return [X, Y];
            }
        }

        // Stores Y value of current interval
        var T = tup[i][0][1];

        // T is less than or equal to curr
        if (T <= curr)
            return [tup[i][1], currPos];

        else {

            // Update curr
            curr = T;

            // Update currPos
            currPos = tup[i][1];
        }
    }

    // No answer exists
    return [-1, -1];
}

// Driver Code
// Given intervals
var arr = [ [ 1, 5 ], [ 2, 10 ],
                             [ 3, 10 ], [ 2, 2 ],
                             [ 2, 15 ] ];
// Size of intervals
var N = arr.length;

// Find answer
var ans = segment_overlapping(N, arr);

// Print answer
document.write( ans[0] + " " + ans[1]);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
4 1
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*