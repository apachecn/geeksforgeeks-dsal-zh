# 两个范围的交点数量

> 原文:[https://www . geeksforgeeks . org/两个范围之间的交叉数/](https://www.geeksforgeeks.org/number-of-intersections-between-two-ranges/)

给定类型 <sub>1</sub> 范围的 **N** 范围和类型 <sub>2</sub> 的 **M** 范围。任务是找出所有可能的类型 <sub>1</sub> 和类型 <sub>2</sub> 范围对之间的交集总数。给出了 <sub>1</sub> 型和 <sub>2</sub> 型范围的所有起点和终点。
**举例:**

> **输入:** N = 2，M = 2
> type1[ ] = { { 1，3}，{5，9 } }
> type2[ ] = { { 2，8}，{9，12 } }
> T5】输出: 3
> 范围{ 2，8 }与 type <sub>1</sub> 范围{ 1，3 }相交，而{5，9}
> 范围{ 9，12 }仅与{ 5，9 }相交。
> 所以路口总数为 3 个。
> **输入:** N = 3，M = 1
> type1[ ] = { { 1，8 }，{ 5，10 }，{ 14，28 }
> type2[ ] = { { 2，8 } }
> **输出:** 2

**进场:**

*   思路是用包含-排除法确定路口总数。
*   可能的交叉总数为 **n * m** 。现在减去那些与第一<sup>型</sup>型 <sub>2</sub> 范围不相交的 <sub>1</sub> 范围的计数。
*   那些类型 <sub>1</sub> 范围将不与 i <sup>第</sup>类型 <sub>2</sub> 范围相交，该范围在 i <sup>第</sup>类型 <sub>2</sub> 范围开始之前结束，在 i <sup>第</sup>类型 <sub>2</sub> 范围结束之后开始。
*   这个计数可以通过使用二分搜索法来确定。C++内置函数**上限**可以直接使用。

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return total
// number of intersections
int FindIntersection(pair<int, int> type1[], int n,
                     pair<int, int> type2[], int m)
{

    // Maximum possible number
    // of intersections
    int ans = n * m;

    vector<int> start, end;
    for (int i = 0; i < n; i++) {

        // Store all starting
        // points of type1 ranges
        start.push_back(type1[i].first);

        // Store all endpoints
        // of type1 ranges
        end.push_back(type1[i].second);
    }

    sort(start.begin(), start.end());
    sort(end.begin(), end.end());

    for (int i = 0; i < m; i++) {

        // Starting point of type2 ranges
        int L = type2[i].first;

        // Ending point of type2 ranges
        int R = type2[i].second;

        // Subtract those ranges which
        // are starting after R
        ans -= (start.end() -
        upper_bound(start.begin(), start.end(), R));

        // Subtract those ranges which
        // are ending before L
        ans -=
        (upper_bound(end.begin(), end.end(), L - 1)
        - end.begin());
    }

    return ans;
}

// Driver Code
int main()
{

    pair<int, int> type1[] =
    { { 1, 2 }, { 2, 3 }, { 4, 5 }, { 6, 7 } };

    pair<int, int> type2[] =
    { { 1, 5 }, { 2, 3 }, { 4, 7 }, { 5, 7 } };

    int n = sizeof(type1) / (sizeof(type1[0]));
    int m = sizeof(type2) / sizeof(type2[0]);

    cout << FindIntersection(type1, n, type2, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;
import java.util.*;
class GFG
{
    static int upperBound(ArrayList<Integer> a, int low,
                          int high, int element)
    {
    while (low < high)
    {
        int middle = low + (high - low) / 2;
        if (a.get(middle) > element)
        {
            high = middle;
        }
      else
      {
            low = middle + 1;
        }
    }
    return low;
    }

    // Function to return total
    // number of intersections
    static int FindIntersection(ArrayList<ArrayList<Integer>> type1,
                                int n, ArrayList<ArrayList<Integer>> type2, int m )
    {

        // Maximum possible number
        // of intersections
        int ans = n * m;
        ArrayList<Integer> start = new ArrayList<Integer>();
        ArrayList<Integer> end = new ArrayList<Integer>();
        for (int i = 0; i < n; i++)
        {

            // Store all starting
            // points of type1 ranges
            start.add(type1.get(i).get(0));

            // Store all endpoints
            // of type1 ranges
            end.add(type1.get(i).get(1));

        }
        Collections.sort(start);
        Collections.sort(end);

        for (int i = 0; i < m; i++)
        {

            // Starting point of type2 ranges
            int L = type2.get(i).get(0);

            // Ending point of type2 ranges
            int R = type2.get(i).get(1);

            // Subtract those ranges which
            // are starting after R
            ans -= start.size() - upperBound(start, 0, start.size(), R);

            // Subtract those ranges which
            // are ending before L
            ans -= upperBound(end, 0, end.size() , L - 1);

        }
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        ArrayList<ArrayList<Integer>> type1 = new ArrayList<ArrayList<Integer>>();
        type1.add(new ArrayList<Integer>(Arrays.asList(1,2)));
        type1.add(new ArrayList<Integer>(Arrays.asList(2,3)));
        type1.add(new ArrayList<Integer>(Arrays.asList(4,5)));
        type1.add(new ArrayList<Integer>(Arrays.asList(6,7)));

        ArrayList<ArrayList<Integer>> type2 = new ArrayList<ArrayList<Integer>>();
        type2.add(new ArrayList<Integer>(Arrays.asList(1,5)));
        type2.add(new ArrayList<Integer>(Arrays.asList(2,3)));
        type2.add(new ArrayList<Integer>(Arrays.asList(4,7)));
        type2.add(new ArrayList<Integer>(Arrays.asList(5,7)));

        int n = type1.size();
        int m = type2.size();

        System.out.println(FindIntersection(type1, n, type2, m));
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of above approach
from bisect import bisect as upper_bound

# Function to return total
# number of intersections
def FindIntersection(type1, n, type2, m):

    # Maximum possible number
    # of intersections
    ans = n * m

    start = []
    end = []
    for i in range(n):

        # Store all starting
        # points of type1 ranges
        start.append(type1[i][0])

        # Store all endpoints
        # of type1 ranges
        end.append(type1[i][1])

    start = sorted(start)
    start = sorted(end)

    for i in range(m):

        # Starting point of type2 ranges
        L = type2[i][0]

        # Ending point of type2 ranges
        R = type2[i][1]

        # Subtract those ranges which
        # are starting after R
        ans -= (len(start)- upper_bound(start, R))

        # Subtract those ranges which
        # are ending before L
        ans -= (upper_bound(end, L - 1))

    return ans

# Driver Code
type1 = [ [ 1, 2 ], [ 2, 3 ],
          [ 4, 5 ], [ 6, 7 ] ]

type2 = [ [ 1, 5 ], [ 2, 3 ],
          [ 4, 7 ], [ 5, 7 ] ]

n = len(type1)
m = len(type2)

print(FindIntersection(type1, n, type2, m))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;
class GFG
{
  static int upperBound(List<int> a, int low,
                        int high, int element)
  {
    while (low < high)
    {
      int middle = low + (high - low) / 2;
      if (a[middle] > element)
      {
        high = middle;
      }
      else
      {
        low = middle + 1;
      }
    }
    return low;
  }

  // Function to return total
  // number of intersections
  static int FindIntersection(List<List<int>> type1, int n,
                              List<List<int>> type2, int m)
  {

    // Maximum possible number
    // of intersections
    int ans = n * m;
    List<int> start = new List<int>();
    List<int> end = new List<int>();
    for (int i = 0; i < n; i++)
    {

      // Store all starting
      // points of type1 ranges
      start.Add(type1[i][0]);

      // Store all endpoints
      // of type1 ranges
      end.Add(type1[i][1]);
    }
    start.Sort();
    end.Sort();

    for (int i = 0; i < m; i++)
    {

      // Starting point of type2 ranges
      int L = type2[i][0];

      // Ending point of type2 ranges
      int R = type2[i][1];

      // Subtract those ranges which
      // are starting after R
      ans -= start.Count - upperBound(start, 0, start.Count, R);

      // Subtract those ranges which
      // are ending before L
      ans -= upperBound(end, 0, end.Count , L - 1);
    }
    return ans;
  }

  // Driver Code
  static public void Main ()
  {
    List<List<int>> type1 = new List<List<int>>();
    type1.Add(new List<int>(){1,2});
    type1.Add(new List<int>(){2,3});
    type1.Add(new List<int>(){4,5});
    type1.Add(new List<int>(){6,7});

    List<List<int>> type2 = new List<List<int>>();
    type2.Add(new List<int>(){1,5});
    type2.Add(new List<int>(){2,3});
    type2.Add(new List<int>(){4,7});
    type2.Add(new List<int>(){5,7});       
    int n = type1.Count;
    int m = type2.Count;
    Console.WriteLine(FindIntersection(type1, n, type2, m));       
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

function upperBound(a,low,high,element)
{
    while (low < high)
    {
        let middle = low + Math.floor((high - low) / 2);
        if (a[middle] > element)
        {
            high = middle;
        }
      else
      {
            low = middle + 1;
        }
    }
    return low;
}

// Function to return total
    // number of intersections
function FindIntersection(type1,n,type2,m)
{
    // Maximum possible number
        // of intersections
        let ans = n * m;
        let start = [];
        let end = [];
        for (let i = 0; i < n; i++)
        {

            // Store all starting
            // points of type1 ranges
            start.push(type1[i][0]);

            // Store all endpoints
            // of type1 ranges
            end.push(type1[i][1]);

        }
        start.sort(function(a,b){return a-b;});
        end.sort(function(a,b){return a-b;});

        for (let i = 0; i < m; i++)
        {

            // Starting point of type2 ranges
            let L = type2[i][0];

            // Ending point of type2 ranges
            let R = type2[i][1];

            // Subtract those ranges which
            // are starting after R
            ans -= start.length - upperBound(start, 0, start.length, R);

            // Subtract those ranges which
            // are ending before L
            ans -= upperBound(end, 0, end.length , L - 1);

        }
        return ans;
}

 // Driver Code
let type1 = [ [ 1, 2 ], [ 2, 3 ],
          [ 4, 5 ], [ 6, 7 ] ];

let type2 = [ [ 1, 5 ], [ 2, 3 ],
          [ 4, 7 ], [ 5, 7 ] ];

let n = type1.length;
let m = type2.length;

document.write(FindIntersection(type1, n, type2, m));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
9
```

**时间复杂度:** O(M*log(N))