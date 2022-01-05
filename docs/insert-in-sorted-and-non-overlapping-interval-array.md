# 插入已排序且不重叠的区间数组

> 原文:[https://www . geesforgeks . org/insert-in-sorted-and-non-overlap-interval-array/](https://www.geeksforgeeks.org/insert-in-sorted-and-non-overlapping-interval-array/)

给定一组不重叠的间隔和一个新的间隔，在正确的位置插入间隔。如果插入导致间隔重叠，则合并重叠的间隔。假设根据开始时间对非重叠间隔集进行排序，以找到正确的插入位置。

先决条件:[合并间隔](https://www.geeksforgeeks.org/merging-intervals/)

**示例:**

```
Input: Set : [1, 3], [6, 9]
        New Interval : [2, 5] 
Output: [1, 5], [6, 9]
The correct position to insert new interval 
[2, 5] is between the two given intervals. 
The resulting set would have been 
[1, 3], [2, 5], [6, 9], but the intervals 
[1, 3], [2, 5] are overlapping. So, they are 
merged together in one interval [1, 5]. 

Input: Set : [1, 2], [3, 5], [6, 7], [8, 10], [12, 16]
        New Interval : [4, 9]
Output: [1, 2], [3, 10], [12, 16]
First the interval is inserted between intervals 
[3, 5] and [6, 7]. Then overlapping intervals are 
merged together in one interval.
```

[Recommended : Please try your approach first on IDE and then look at the solution](https://ide.geeksforgeeks.org/)

**进场:**
让待插入的新区间为:【a，b】
**情况 1 :** b <(集合中第一个区间的起始时间)
在这种情况下只需在集合的开头插入新区间即可。
**情况 2 :** (集合中最后一个区间的结束值)< a
在这种情况下，只需在集合末尾插入新的区间即可。
**病例 3 :** a？(第一个区间的起始值)和 b？(最后一个间隔的结束值)
在这种情况下，新间隔与所有间隔重叠，即它包含所有间隔。所以最终的答案是新的音程本身。
**情况 4 :** 新的间隔不与集合中的任何间隔重叠，并且落在集合中的任何两个间隔之间
在这种情况下，只需将间隔插入集合中的正确位置。这方面的一个示例测试案例是:

```
Input: Set : [1, 2], [6, 9]
        New interval : [3, 5]
Output: [1, 2], [3, 5], [6, 9]
```

**情况 5 :** 新间隔与集合的间隔重叠。
在这种情况下，只需将新间隔与重叠间隔合并即可。为了更好的理解如何合并重叠区间，参考这篇文章:[合并重叠区间](https://www.geeksforgeeks.org/merging-intervals/)

上面的示例测试用例示例 2 涵盖了这种情况。

## C++

```
// C++ Code to insert a new interval in set of sorted
// intervals and merge overlapping intervals that are
// formed as a result of insertion.
#include <bits/stdc++.h>

using namespace std;

// Define the structure of interval
struct Interval
{
    int start;
    int end;
    Interval()
        : start(0), end(0)
    {
    }
    Interval(int s, int e)
        : start(s), end(e)
    {
    }
};

// A subroutine to check if intervals overlap or not.
bool doesOverlap(Interval a, Interval b)
{
    return (min(a.end, b.end) >= max(a.start, b.start));
}

// Function to insert new interval and
// merge overlapping intervals
vector<Interval> insertNewInterval
(vector<Interval>& Intervals, Interval newInterval)
{
    vector<Interval> ans;
    int n = Intervals.size();

    // If set is empty then simply insert
    // newInterval and return.
    if (n == 0)
    {
        ans.push_back(newInterval);
        return ans;
    }

    // Case 1 and Case 2 (new interval to be
    // inserted at corners)
    if (newInterval.end < Intervals[0].start ||
            newInterval.start > Intervals[n - 1].end)
    {
        if (newInterval.end < Intervals[0].start)
            ans.push_back(newInterval);

        for (int i = 0; i < n; i++)
            ans.push_back(Intervals[i]);

        if (newInterval.start > Intervals[n - 1].end)
            ans.push_back(newInterval);

        return ans;
    }

    // Case 3 (New interval covers all existing)
    if (newInterval.start <= Intervals[0].start &&
        newInterval.end >= Intervals[n - 1].end)
    {
        ans.push_back(newInterval);
        return ans;
    }

    // Case 4 and Case 5
    // These two cases need to check whether
    // intervals overlap or not. For this we
    // can use a subroutine that will perform
    // this function.
    bool overlap = true;
    for (int i = 0; i < n; i++)
    {
        overlap = doesOverlap(Intervals[i], newInterval);
        if (!overlap)
        {
            ans.push_back(Intervals[i]);

            // Case 4 : To check if given interval
            // lies between two intervals.
            if (i < n &&
                newInterval.start > Intervals[i].end &&
                newInterval.end < Intervals[i + 1].start)
                ans.push_back(newInterval);

            continue;
        }

        // Case 5 : Merge Overlapping Intervals.
        // Starting time of new merged interval is
        // minimum of starting time of both
        // overlapping intervals.
        Interval temp;
        temp.start = min(newInterval.start,
                         Intervals[i].start);

        // Traverse the set until intervals are
        // overlapping
        while (i < n && overlap)
        {

            // Ending time of new merged interval
            // is maximum of ending time both
            // overlapping intervals.
            temp.end = max(newInterval.end,
                           Intervals[i].end);
            if (i == n - 1)
                overlap = false;
            else
                overlap = doesOverlap(Intervals[i + 1],
                                          newInterval);
            i++;
        }

        i--;
        ans.push_back(temp);
    }

    return ans;
}

// Driver code
int main()
{
    vector<Interval> Intervals;
    Interval newInterval;

    newInterval.start = 1;
    newInterval.end = 2;
    Intervals.push_back(newInterval);
    newInterval.start = 3;
    newInterval.end = 5;
    Intervals.push_back(newInterval);
    newInterval.start = 6;
    newInterval.end = 7;
    Intervals.push_back(newInterval);
    newInterval.start = 8;
    newInterval.end = 10;
    Intervals.push_back(newInterval);
    newInterval.start = 12;
    newInterval.end = 16;
    Intervals.push_back(newInterval);
    newInterval.start = 4;
    newInterval.end = 9;

    vector<Interval> ans =
          insertNewInterval(Intervals, newInterval);

    for (int i = 0; i < ans.size(); i++)
        cout << ans[i].start << ", "
             << ans[i].end << "\n";

    return 0;
}
```

**Output**

```
1, 2
3, 10
12, 16
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

**使用堆栈的另一种方法:**

我们将在堆栈中推进对，直到它与间隔合并或找到合适的位置来安装它。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <iostream>
#include <stack>
using namespace std;

// Program to merge interval
void mergeInterval2(pair<int, int> arr[],
                    int n, pair<int,
                               int> newPair)
{ 

    // Create stack of type
    // pair<int, int>
    stack< pair<int, int> > stk;

    // Pushing first pair
    stk.push(arr[0]);

    // Storing the top element
    pair<int, int> top = stk.top();

    // Checking is newPair.first
    // is less than top.second
    if (newPair.first < top.second)
    {

        // Pop the top element
        // as it will merge with the
        // previous range
        stk.pop();

        // Re-assigning top.first
        top.first = min(top.first,
                          newPair.first);

        // Re-assigning top.second
        top.second = max(top.second,
                          newPair.second);

        // Push the current interval
        stk.push(top);
    }
    else
    {

       // Push the new pair as it does
       // not intersect to first pair
       stk.push(newPair);
    }

    // Iterate i from 1 to n - 1
    for (int i = 1; i < n; i++)
    {

        // Store the top element of
        // the stack stk
        pair<int, int> top = stk.top();

        // Checking is arr[i].first
        // is less than top.second
        if (arr[i].first < top.second)
        {

            // Pop the top element
            // as it will merge with the
            // previous range
            stk.pop();

            // Re-assigning top.first
            top.first = min(top.first,
                            arr[i].first);

            // Re-assigning top.second
            top.second = max(top.second,
                            arr[i].second);

            // Push the current interval
            stk.push(top);
        }

        else
        {

            // Push the new pair as it does
            // not intersect to first pair
            stk.push(arr[i]);
        }
    }

    // Storing the final intervals
    stack< pair<int,int> > finalIntervals;

    // Poping the stack elements
    while (stk.empty() != true)
    {
        pair<int, int> ele =
                       stk.top();
        stk.pop();

        // Push ele in finalIntervals
        finalIntervals.push(ele);  
    }

    // Displaying the final result
    while (finalIntervals.empty() != true)
    {
        pair<int, int> ele =
                       finalIntervals.top();
        finalIntervals.pop();

        cout << ele.first << ", "
             << ele.second << endl;
    }
}

// Driver Code
int main()
{

    pair<int, int> arr2[] = {
        { 1, 2 }, { 3, 5 }, { 6, 7 },
                 { 8, 10 }, { 12, 16 }
    };
    pair<int, int> newPair{ 4, 9 };
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    // Function Call
    mergeInterval2(arr2, n2, newPair);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for above approach

# Program to merge interval
def mergeInterval2(arr, n, newPair) :

    # Create stack of type
    # pair<int, int>
    stk = []

    # Pushing first pair
    stk.append(arr[0])

    # Storing the top element
    top = stk[len(stk) - 1]

    # Checking is newPair.first
    # is less than top.second
    if (newPair[0] < top[1]) :

        # Pop the top element
        # as it will merge with the
        # previous range
        stk.pop()

        # Re-assigning top.first
        top[0] = min(top[0], newPair[0])

        # Re-assigning top.second
        top[1] = max(top[1], newPair[1])

        # Push the current interval
        stk.append(top)

    else :
        # Push the new pair as it does
        # not intersect to first pair
        stk.append(newPair)

    # Iterate i from 1 to n - 1
    for i in range(1, n) :

        # Store the top element of
        # the stack stk
        top = stk[len(stk) - 1]

        # Checking is arr[i].first
        # is less than top.second
        if (arr[i][0] < top[1]) :

            # Pop the top element
            # as it will merge with the
            # previous range
            stk.pop()

            # Re-assigning top.first
            top[0] = min(top[0], arr[i][0])

            # Re-assigning top.second
            top[1] = max(top[1], arr[i][1])

            # Push the current interval
            stk.append(top)

        else :

            # Push the new pair as it does
            # not intersect to first pair
            stk.append(arr[i])

    # Storing the final intervals
    finalIntervals = []

    # Poping the stack elements
    while (len(stk) > 0) :

        ele = stk[len(stk) - 1]
        stk.pop()

        # Push ele in finalIntervals
        finalIntervals.append(ele)

    # Displaying the final result
    while (len(finalIntervals) > 0) :

        ele = finalIntervals[len(finalIntervals) - 1]
        finalIntervals.pop()

        print(ele[0] , end = ", ")
        print(ele[1])

arr2 = [ [ 1, 2 ], [ 3, 5 ], [ 6, 7 ], [ 8, 10 ], [ 12, 16 ] ]

newPair = [ 4, 9 ]
n2 = len(arr2)

# Function Call
mergeInterval2(arr2, n2, newPair)

# This code is contributed by divyesh072019
```

## C#

```
// C# program for above approach
using System;
using System.Collections;

class GFG{

// Function to merge interval
static void mergeInterval2(Tuple<int, int>[] arr,
                    int n, Tuple<int, int> newPair)
{ 

    // Create stack of type
    // pair<int, int>
    Stack stk = new Stack();

    // Pushing first pair
    stk.Push(arr[0]);

    // Storing the top element
    Tuple<int,
          int> top = (Tuple<int,
                            int>)stk.Peek();

    // Checking is newPair.first
    // is less than top.second
    if (newPair.Item1 < top.Item2)
    {

        // Pop the top element
        // as it will merge with the
        // previous range
        stk.Pop();

        // Re-assigning top.first and top.second
        top = new Tuple<int, int>(Math.Min(top.Item1,
                                           newPair.Item1),
                                  Math.Max(top.Item2,
                                           newPair.Item2));

        // Push the current interval
        stk.Push(top);
    }
    else
    {

        // Push the new pair as it does
        // not intersect to first pair
        stk.Push(newPair);
    }

    // Iterate i from 1 to n - 1
    for(int i = 1; i < n; i++)
    {

        // Store the top element of
        // the stack stk
        Tuple<int,
              int> Top = (Tuple<int,
                                int>)stk.Peek();

        // Checking is arr[i].first
        // is less than top.second
        if (arr[i].Item1 < Top.Item2)
        {

            // Pop the top element
            // as it will merge with the
            // previous range
            stk.Pop();

            // Re-assigning top.first and top.second
            Top = new Tuple<int, int>(Math.Min(Top.Item1,
                                               arr[i].Item1),
                                      Math.Max(Top.Item2,
                                               arr[i].Item2));

            // Push the current interval
            stk.Push(Top);
        }
        else
        {

            // Push the new pair as it does
            // not intersect to first pair
            stk.Push(arr[i]);
        }
    }

    // Storing the final intervals
    Stack finalIntervals = new Stack();

    // Poping the stack elements
    while (stk.Count != 0)
    {
        Tuple<int,
              int> ele = (Tuple<int,
                                int>)stk.Peek();
        stk.Pop();

        // Push ele in finalIntervals
        finalIntervals.Push(ele);  
    }

    // Displaying the final result
    while (finalIntervals.Count != 0)
    {
        Tuple<int,
              int> ele = (Tuple<int,
                                int>)finalIntervals.Peek();

        finalIntervals.Pop();

        Console.WriteLine(ele.Item1 + ", " + ele.Item2);
    }
}

// Driver Code
static void Main()
{
    Tuple<int, int>[] arr2 =
    {
        Tuple.Create(1, 2),
        Tuple.Create(3, 5),
        Tuple.Create(6, 7),
        Tuple.Create(8, 10),
        Tuple.Create(12, 16),
    };

    Tuple<int,
          int> newPair = new Tuple<int,
                                   int>(4, 9);
    int n2 = arr2.Length;

    // Function Call
    mergeInterval2(arr2, n2, newPair);
}
}

// This code is contributed by divyeshrabadiya07
```

**Output**

```
1, 2
3, 10
12, 16
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)