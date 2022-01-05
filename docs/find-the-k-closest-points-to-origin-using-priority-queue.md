# 使用优先级队列

找到离原点最近的 K 个点

> 原文:[https://www . geeksforgeeks . org/find-k-最接近原点-使用优先级-队列/](https://www.geeksforgeeks.org/find-the-k-closest-points-to-origin-using-priority-queue/)

给定 2D 平面上 n 个点的**列表，任务是找到离原点 O(0，0)最近的 K (k < n 个点。
*注:点 P(x，y)与 O(0，0)之间的距离采用标准**欧氏距离**。*
**示例:****

> **输入:** [(1，0)，(2，1)，(3，6)，(-5，2)，(1，-4)]，K = 3
> **输出:**【(1，0)，(2，1)，(1，-4)】
> **说明:**
> 原点距离的平方为
> (1，0) : 1
> (2，1) : 5
> (3，6) : 45
> (-5，2):29【T11
> **输入:** [(1，3)，(-2，2)]，K = 1
> **输出:** [(-2，2)]
> **解释:**
> 点距原点距离的平方是
> (1，3) : 10
> (-2，2) : 8
> 因此对于 K = 1，最近的点是(-2，2)。

**使用基于距离排序的方法:**这种方法在[这篇文章](https://www.geeksforgeeks.org/find-k-closest-points-to-the-origin/)中有解释。
**进场使用** [**优先级队列**](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **进行对比:**解决上述问题的主要思路是**将该点的坐标**存储在一对优先级队列中，根据该点距离原点的距离。为了将最大优先级分配给离原点最远的点，我们使用优先级队列中的[比较器类。然后打印优先级队列的前 K 个元素。
以下是上述方法的实施:](https://www.geeksforgeeks.org/stl-priority-queue-for-structure-or-class/)

## C++

```
// C++ implementation to find the K
// closest points to origin
// using Priority Queue

#include <bits/stdc++.h>
using namespace std;

// Comparator class to assign
// priority to coordinates
class comp {

public:
    bool operator()(pair<int, int> a,
                    pair<int, int> b)
    {
        int x1 = a.first * a.first;
        int y1 = a.second * a.second;
        int x2 = b.first * b.first;
        int y2 = b.second * b.second;

        // return true if distance
        // of point 1 from origin
        // is greater than distance of
        // point 2 from origin
        return (x1 + y1) > (x2 + y2);
    }
};

// Function to find the K closest points
void kClosestPoints(int x[], int y[],
                    int n, int k)
{
    // Create a priority queue
    priority_queue<pair<int, int>,
                   vector<pair<int, int> >,
                   comp>
        pq;

    // Pushing all the points
    // in the queue
    for (int i = 0; i < n; i++) {
        pq.push(make_pair(x[i], y[i]));
    }

    // Print the first K elements
    // of the queue
    for (int i = 0; i < k; i++) {

        // Store the top of the queue
        // in a temporary pair
        pair<int, int> p = pq.top();

        // Print the first (x)
        // and second (y) of pair
        cout << p.first << " "
             << p.second << endl;

        // Remove top element
        // of priority queue
        pq.pop();
    }
}

// Driver code
int main()
{
    // x coordinate of points
    int x[] = { 1, -2 };

    // y coordinate of points
    int y[] = { 3, 2 };
    int K = 1;

    int n = sizeof(x) / sizeof(x[0]);

    kClosestPoints(x, y, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the K
// closest points to origin
// using Priority Queue
import java.util.*;

// Point class to store
// a point
class Pair implements Comparable<Pair>
{
    int first, second;
    Pair(int a, int b)
    {
        first = a;
        second = b;
    }

    public int compareTo(Pair o)
    {
        int x1 = first * first;
        int y1 = second * second;
        int x2 = o.first * o.first;
        int y2 = o.second * o.second;
        return (x1 + y1) - (x2 + y2);
    }
}

class GFG{

// Function to find the K closest points
static void kClosestPoints(int x[], int y[],
                           int n, int k)
{
    // Create a priority queue
    PriorityQueue<Pair> pq = new PriorityQueue<>();

    // Pushing all the points
    // in the queue
    for(int i = 0; i < n; i++)
    {
        pq.add(new Pair(x[i], y[i]));
    }

    // Print the first K elements
    // of the queue
    for(int i = 0; i < k; i++)
    {

        // Remove the top of the queue
        // and store in a temporary pair
        Pair p = pq.poll();

        // Print the first (x)
        // and second (y) of pair
        System.out.println(p.first +
                     " " + p.second);
    }
}

// Driver code
public static void main(String[] args)
{

    // x coordinate of points
    int x[] = { 1, -2 };

    // y coordinate of points
    int y[] = { 3, 2 };
    int K = 1;

    int n = x.length;

    kClosestPoints(x, y, n, K);
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// Javascript implementation to find the K
// closest points to origin
// using Priority Queue

// Function to find the K closest points
function kClosestPoints(x, y, n, k)
{
    // Create a priority queue
    var pq = [];

    // Pushing all the points
    // in the queue
    for (var i = 0; i < n; i++) {
        pq.push([x[i], y[i]]);
    }

    // Print the first K elements
    // of the queue
    for (var i = 0; i < k; i++) {

        // Store the top of the queue
        // in a temporary pair
        var p = pq[pq.length-1];

        // Print the first (x)
        // and second (y) of pair
        document.write( p[0] + " "
              + p[1] + "<br>");

        // Remove top element
        // of priority queue
        pq.pop();
    }
}

// Driver code
// x coordinate of points
var x = [1, -2];

// y coordinate of points
var y = [3, 2];
var K = 1;
var n = x.length;
kClosestPoints(x, y, n, K);

// This code is contributed by rutvik_56.
</script>
```

## 蟒蛇 3

```
# Python3 implementation to find the K
# closest points to origin
# using Priority Queue

import heapq as hq
# Function to find the K closest points
def kClosestPoints(x, y, n, k):
    # Create a priority queue
    pq=[]

    # Pushing all the points
    # in the queue
    for i in range(n):
        hq.heappush(pq, (x[i]*x[i]+y[i]*y[i],x[i],y[i]))

    # Print the first K elements
    # of the queue
    for i in range(k) :

        # Store the top of the queue
        # in a temporary pair
        p = hq.heappop(pq)

        # Print the first (x)
        # and second (y) of pair
        print("{} {}".format(p[1],p[2]))  

# Driver code
if __name__ == '__main__':
    # x coordinate of points
    x = [1, -2]

    # y coordinate of points
    y = [3, 2]
    K = 1

    n=len(x)

    kClosestPoints(x, y, n, K)
```

**Output:** 

```
-2 2
```

**时间复杂度:** O(N + K * log(N))
**辅助空间** : O(N)