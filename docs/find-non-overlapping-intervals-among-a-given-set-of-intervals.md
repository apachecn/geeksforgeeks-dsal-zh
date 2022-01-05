# 在给定的一组间隔中找到不重叠的间隔

> 原文:[https://www . geeksforgeeks . org/find-给定间隔集中的非重叠间隔/](https://www.geeksforgeeks.org/find-non-overlapping-intervals-among-a-given-set-of-intervals/)

给定 **N** 组时间间隔，任务是找到与给定的间隔组不重叠的间隔。
**例:**

> **输入:**区间 arr[] = { {1，3}、{2，4}、{3，5}、{7，9} }
> **输出:**
> 【5，7】
> **解释:**
> 唯一不与其他区间重叠的区间是【5，7】。
> **输入:**区间 arr[] = { {1，3}、{9，12}、{2，4}、{6，8} }
> **输出:**
> 【4，6】
> 【8，9】
> **说明:**
> 有两个区间与其他区间不重叠的区间是【4，6】、【8，9】。

**方法:**思路是按照开始时间对给定的时间间隔进行排序，如果连续的间隔没有重叠，那么它们之间的差就是自由间隔。
以下是步骤:

1.  根据开始时间对给定的一组间隔进行排序。
2.  遍历所有的区间组，[检查连续区间是否重叠](https://www.geeksforgeeks.org/check-if-any-two-intervals-overlap-among-a-given-set-of-intervals/)。
3.  如果区间(比如**区间 a** & **区间 b** )没有重叠，那么由**【a . end，b . start】**形成的成对集合就是不重叠的区间。
4.  如果间隔重叠，则检查下一个连续的间隔。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// interval with start time & end time
struct interval {
    int start, end;
};

// Comparator function to sort the given
// interval according to time
bool compareinterval(interval i1, interval i2)
{
    return (i1.start < i2.start);
}

// Function that find the free interval
void findFreeinterval(interval arr[], int N)
{

    // If there are no set of interval
    if (N <= 0) {
        return;
    }

    // To store the set of free interval
    vector<pair<int, int> > P;

    // Sort the given interval according
    // starting time
    sort(arr, arr + N, compareinterval);

    // Iterate over all the interval
    for (int i = 1; i < N; i++) {

        // Previous interval end
        int prevEnd = arr[i - 1].end;

        // Current interval start
        int currStart = arr[i].start;

        // If ending index of previous
        // is less than starting index
        // of current, then it is free
        // interval
        if (prevEnd < currStart) {
            P.push_back({ prevEnd,
                          currStart });
        }
    }

    // Print the free interval
    for (auto& it : P) {
        cout << "[" << it.first << ", "
             << it.second << "]" << endl;
    }
}

// Driver Code
int main()
{

    // Given set of interval
    interval arr[] = { { 1, 3 },
                       { 2, 4 },
                       { 3, 5 },
                       { 7, 9 } };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findFreeinterval(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

// Interval with start time & end time
static class Interval
{
    int start, end;

    Interval(int start, int end)
    {
        this.start = start;
        this.end = end;
    }
}

// Function that find the free interval
static void findFreeinterval(int[][] arr, int N)
{
    // If there are no set of interval
    if (N <= 0)
    {
        return;
    }

    // To store the set of free interval
    ArrayList<Interval> p = new ArrayList<>();

    // Sort the given interval according
    // starting time
    Arrays.sort(arr, new Comparator<int[]>()
    {
        public int compare(int[] a, int[] b)
        {
            return a[0] - b[0];
        }
    });

    // Iterate over all the interval
    for (int i = 1; i < N; i++)
    {

        // Previous interval end
        int prevEnd = arr[i - 1][1];

        // Current interval start
        int currStart = arr[i][0];

        // If ending index of previous
        // is less than starting index
        // of current, then it is free
        // interval
        if (prevEnd < currStart)
        {
            Interval interval = new Interval(prevEnd,
                                              currStart);
            p.add(interval);
        }
    }

    // Print the free interval
    for (int i = 0; i < p.size(); i++)
    {
        System.out.println("[" + p.get(i).start +
                          ", " + p.get(i).end + "]");
    }
}

// Driver code
public static void main(String[] args)
{

    // Given set of interval
    int[][] arr = { { 1, 3 },
                    { 2, 4 },
                    { 3, 5 },
                    { 7, 9 } };

    int N = arr.length;

    // Function Call
    findFreeinterval(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach
def findFreeinterval(arr, N):

    # If there are no set of interval
    if N < 1:
        return

    # To store the set of free interval
    P = []

    # Sort the given interval according
    # Starting time
    arr.sort(key = lambda a:a[0])

    # Iterate over all the interval
    for i in range(1, N):

        # Previous interval end
        prevEnd = arr[i - 1][1]

        # Current interval start
        currStart = arr[i][0]

        # If Previous Interval is less
        # than current Interval then we
        # store that answer
        if prevEnd < currStart:
            P.append([prevEnd, currStart])

    # Print the intervals
    for i in P:
        print(i)

# Driver code
if __name__ == "__main__":

    # Given List of intervals
    arr = [ [ 1, 3 ], [ 2, 4 ],
            [ 3, 5 ], [ 7, 9 ] ]

    N = len(arr)

    # Function call
    findFreeinterval(arr, N)

# This code is contributed by Tokir Manva
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that find the free interval
function findFreeinterval(arr, N)
{

    // If there are no set of interval
    if (N <= 0) {
        return;
    }

    // To store the set of free interval
    var P = [];

    // Sort the given interval according
    // starting time
    arr.sort((a,b) => a[0]-b[0])

    // Iterate over all the interval
    for (var i = 1; i < N; i++) {

        // Previous interval end
        var prevEnd = arr[i - 1][1];

        // Current interval start
        var currStart = arr[i][0];

        // If ending index of previous
        // is less than starting index
        // of current, then it is free
        // interval
        if (prevEnd < currStart) {
            P.push([prevEnd,
                          currStart]);
        }
    }

    // Print the free interval
    P.forEach(it => {

        document.write( "[" + it[0] + ", "
             + it[1] + "]");
    });
}

// Driver Code

// Given set of interval
var arr = [ [ 1, 3 ],
                   [ 2, 4 ],
                   [ 3, 5 ],
                   [ 7, 9 ] ];
var N = arr.length;

// Function Call
findFreeinterval(arr, N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
[5, 7]
```

***时间复杂度:** O(N*log N)* ，其中 N 为区间集的个数。

**辅助空间:** O(N)