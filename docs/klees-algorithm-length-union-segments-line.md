# 克莱算法(线段并集长度)

> 原文:[https://www . geesforgeks . org/klees-算法-长度-并集-线段-直线/](https://www.geeksforgeeks.org/klees-algorithm-length-union-segments-line/)

给定一条线上线段的开始和结束位置，任务是取所有给定线段的并集，并找出这些线段所覆盖的长度。
**例:**

```
Input : segments[] = {{2, 5}, {4, 8}, {9, 12}}
Output : 9 
Explanation:
segment 1 = {2, 5}
segment 2 = {4, 8}
segment 3 = {9, 12}
If we take the union of all the line segments,
we cover distances [2, 8] and [9, 12]. Sum of 
these two distances is 9 (6 + 3)
```

**进场:**

该算法是由 Klee 在 1977 年提出的。算法的时间复杂度为 O(N ^ log N)。已经证明该算法是最快的(渐近的)，并且该问题不能以更好的复杂度来解决。

**描述:**
1)将所有线段的所有坐标放入一个辅助数组点[]。
2)根据坐标值排序。
3)排序的附加条件——如果有相等的坐标，插入任一线段的左坐标，而不是右坐标。
4)现在遍历整个数组，计数器“计数”重叠的段。
5)如果计数大于零，则结果加到点[I]–点[i-1]之间的差值上。
6)如果当前元素属于左端，我们增加“计数”，否则减少。
**图解:**

```
Lets take the example :
segment 1 : (2,5)
segment 2 : (4,8)
segment 3 : (9,12)

Counter = result = 0;
n = number of segments = 3;

for i=0,  points[0] = {2, false}
          points[1] = {5, true}
for i=1,  points[2] = {4, false}
          points[3] = {8, true}
for i=2,  points[4] = {9, false}
          points[5] = {12, true}

Therefore :
points = {2, 5, 4, 8, 9, 12}
         {f, t, f, t, f, t}

after applying sorting :
points = {2, 4, 5, 8, 9, 12}
         {f, f, t, t, f, t}

Now,
for i=0, result = 0;
         Counter = 1;

for i=1, result = 2;
         Counter = 2;

for i=2, result = 3;
         Counter = 1;

for i=3, result = 6;
         Counter = 0;

for i=4, result = 6;
         Counter = 1;

for i=5, result = 9;
         Counter = 0;

Final answer = 9;
```

## C++

```
// C++ program to implement Klee's algorithm
#include<bits/stdc++.h>
using namespace std;

// Returns sum of lengths covered by union of given
// segments
int segmentUnionLength(const vector<
                          pair <int,int> > &seg)
{
    int n = seg.size();

    // Create a vector to store starting and ending
    // points
    vector <pair <int, bool> > points(n * 2);
    for (int i = 0; i < n; i++)
    {
        points[i*2]     = make_pair(seg[i].first, false);
        points[i*2 + 1] = make_pair(seg[i].second, true);
    }

    // Sorting all points by point value
    sort(points.begin(), points.end());

    int result = 0; // Initialize result

    // To keep track of counts of
    // current open segments
    // (Starting point is processed,
    // but ending point
    // is not)
    int Counter = 0;

    // Traverse through all points
    for (unsigned i=0; i<n*2; i++)
    {
        // If there are open points, then we add the
        // difference between previous and current point.
        // This is interesting as we don't check whether
        // current point is opening or closing,
        if (Counter)
            result += (points[i].first -
                        points[i-1].first);

        // If this is an ending point, reduce, count of
        // open points.
        (points[i].second)? Counter-- : Counter++;
    }
    return result;
}

// Driver program for the above code
int main()
{
    vector< pair <int,int> > segments;
    segments.push_back(make_pair(2, 5));
    segments.push_back(make_pair(4, 8));
    segments.push_back(make_pair(9, 12));
    cout << segmentUnionLength(segments) << endl;
    return 0;
}
```

## 计算机编程语言

```
# Python program for the above approach

def segmentUnionLength(segments):

    # Size of given segments list
    n = len(segments)

    # Initialize empty points container
    points = [None] * (n * 2)

    # Create a vector to store starting
    # and ending points
    for i in range(n):
        points[i * 2] = (segments[i][0], False)
        points[i * 2 + 1] = (segments[i][1], True)

    # Sorting all points by point value
    points = sorted(points, key=lambda x: x[0])

    # Initialize result as 0
    result = 0

    # To keep track of counts of current open segments
    # (Starting point is processed, but ending point
    # is not)
    Counter = 0

    # Traverse through all points
    for i in range(0, n * 2):

        # If there are open points, then we add the
        # difference between previous and current point.
        if (i > 0) & (points[i][0] > points[i - 1][0]) &  (Counter > 0):
            result += (points[i][0] - points[i - 1][0])

        # If this is an ending point, reduce, count of
        # open points.
        if points[i][1]:
            Counter -= 1
        else:
            Counter += 1
    return result

# Driver code
if __name__ == '__main__':
    segments = [(2, 5), (4, 8), (9, 12)]
    print(segmentUnionLength(segments))
```

**Output**

```
9
```

**时间复杂度:** O(n * log n)
本文由 [**阿比南丹米塔尔**](https://in.linkedin.com/in/abhinandanm) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。