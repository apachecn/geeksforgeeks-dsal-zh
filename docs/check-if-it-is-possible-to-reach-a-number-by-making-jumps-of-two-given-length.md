# 通过两次给定长度的跳跃来检查是否有可能到达一个数

> 原文:[https://www . geeksforgeeks . org/check-如果有可能通过两个给定长度的跳跃来达到一个数字/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-reach-a-number-by-making-jumps-of-two-given-length/)

给定起始位置“k”和两个跳跃大小“d1”和“d2”，我们的任务是找到达到“x”所需的最小跳跃次数(如果可能的话)。
在任何位置 P，我们都可以跳到位置:

*   **P + d1** 和**P–D1**
*   **P + d2** 和**P–D2**

**例:**

```
Input : k = 10, d1 = 4, d2 = 6 and x = 8 
Output : 2
1st step 10 + d1 = 14
2nd step 14 - d2 = 8

Input : k = 10, d1 = 4, d2 = 6 and x = 9
Output : -1
-1 indicates it is not possible to reach x.
```

在[上一篇文章](https://www.geeksforgeeks.org/reach-the-numbers-by-making-jumps-of-two-given-lengths/)中，我们讨论了一种策略，通过跳转两个给定的长度来检查 K 是否可以到达一个数字列表。
在这里，我们得到的不是一个数字列表，而是一个整数 **x** ，如果可以从 **k** 到达，那么任务就是找到所需的最小步数或跳数。
我们将使用**广度优先搜索** :
**方法** :
来解决这个问题

*   检查从 **k** 是否可以到达“x”。如果数字 **x** 满足**(x–k)% gcd(D1，d2) = 0** ，则可以从 k 到达。
*   如果 x 是可达的:
    1.  维护一个散列表来存储已经访问过的位置。
    2.  从 k 位置开始应用 bfs 算法。
    3.  如果您在“stp”步骤中到达 P 位置，您可以在“stp+1”步骤中到达 p+d1 位置。
    4.  如果位置 P 是要求的位置‘x’，那么达到 P 所采取的步骤就是答案

下图描述了算法如何在 k = 10、d1 = 4 和 d2 = 6 的情况下找到达到 x = 8 所需的步数。

![Algo Example](https://docs.google.com/drawings/d/e/2PACX-1vQNc-ChldajMUiKj_gyuUb4IrdhU7cCl-CLDSnA_slb_nU47DBOWqvE-ME35jMpaU6-vF4Jj1abOrrH/pub?w=1440&h=1080)

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to perform BFS traversal to
// find minimum number of step needed
// to reach x from K
int minStepsNeeded(int k, int d1, int d2, int x)
{
    // Calculate GCD of d1 and d2
    int gcd = __gcd(d1, d2);

    // If position is not reachable
    // return -1
    if ((k - x) % gcd != 0)
        return -1;

    // Queue for BFS
    queue<pair<int, int> > q;

    // Hash Table for marking
    // visited positions
    unordered_set<int> visited;

    // we need 0 steps to reach K
    q.push({ k, 0 });

    // Mark starting position
    // as visited
    visited.insert(k);

    while (!q.empty()) {

        int s = q.front().first;

        // stp is the number of steps
        // to reach position s
        int stp = q.front().second;

        if (s == x)
            return stp;

        q.pop();

        if (visited.find(s + d1) == visited.end()) {

            // if position not visited
            // add to queue and mark visited
            q.push({ s + d1, stp + 1 });

            visited.insert(s + d1);
        }

        if (visited.find(s + d2) == visited.end()) {
            q.push({ s + d2, stp + 1 });
            visited.insert(s + d2);
        }

        if (visited.find(s - d1) == visited.end()) {
            q.push({ s - d1, stp + 1 });
            visited.insert(s - d1);
        }
        if (visited.find(s - d2) == visited.end()) {
            q.push({ s - d2, stp + 1 });
            visited.insert(s - d2);
        }
    }
}

// Driver Code
int main()
{
    int k = 10, d1 = 4, d2 = 6, x = 8;

    cout << minStepsNeeded(k, d1, d2, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}
// Function to perform BFS traversal to
// find minimum number of step needed
// to reach x from K
static int minStepsNeeded(int k, int d1,
                          int d2, int x)
{
    // Calculate GCD of d1 and d2
    int gcd = __gcd(d1, d2);

    // If position is not reachable
    // return -1
    if ((k - x) % gcd != 0)
        return -1;

    // Queue for BFS
    Queue<pair> q = new LinkedList<>();

    // Hash Table for marking
    // visited positions
    HashSet<Integer> visited = new HashSet<>();

    // we need 0 steps to reach K
    q.add(new pair(k, 0 ));

    // Mark starting position
    // as visited
    visited.add(k);

    while (!q.isEmpty())
    {
        int s = q.peek().first;

        // stp is the number of steps
        // to reach position s
        int stp = q.peek().second;

        if (s == x)
            return stp;

        q.remove();

        if (!visited.contains(s + d1))
        {

            // if position not visited
            // add to queue and mark visited
            q.add(new pair(s + d1, stp + 1));

            visited.add(s + d1);
        }

        if (visited.contains(s + d2))
        {
            q.add(new pair(s + d2, stp + 1));
            visited.add(s + d2);
        }

        if (!visited.contains(s - d1))
        {
            q.add(new pair(s - d1, stp + 1));
            visited.add(s - d1);
        }
        if (!visited.contains(s - d2))
        {
            q.add(new pair(s - d2, stp + 1));
            visited.add(s - d2);
        }
    }
    return Integer.MIN_VALUE;
}

// Driver Code
public static void main(String[] args)
{
    int k = 10, d1 = 4, d2 = 6, x = 8;

    System.out.println(minStepsNeeded(k, d1, d2, x));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd
from collections import deque as queue

# Function to perform BFS traversal to
# find minimum number of step needed
# to reach x from K
def minStepsNeeded(k, d1, d2, x):

    # Calculate GCD of d1 and d2
    gcd = __gcd(d1, d2)

    # If position is not reachable
    # return -1
    if ((k - x) % gcd != 0):
        return -1

    # Queue for BFS
    q = queue()

    # Hash Table for marking
    # visited positions
    visited = dict()

    # we need 0 steps to reach K
    q.appendleft([k, 0])

    # Mark starting position
    # as visited
    visited[k] = 1

    while (len(q) > 0):

        sr = q.pop()
        s, stp = sr[0], sr[1]

        # stp is the number of steps
        # to reach position s
        if (s == x):
            return stp

        if (s + d1 not in visited):

            # if position not visited
            # add to queue and mark visited
            q.appendleft([(s + d1), stp + 1])

            visited[(s + d1)] = 1

        if (s + d2 not in visited):
            q.appendleft([(s + d2), stp + 1])
            visited[(s + d2)] = 1

        if (s - d1 not in visited):
            q.appendleft([(s - d1), stp + 1])
            visited[(s - d1)] = 1

        if (s - d2 not in visited):
            q.appendleft([(s - d2), stp + 1])
            visited[(s - d2)] = 1

# Driver Code
k = 10
d1 = 4
d2 = 6
x = 8

print(minStepsNeeded(k, d1, d2, x))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to perform BFS traversal to
// find minimum number of step needed
// to reach x from K
static int minStepsNeeded(int k, int d1,
                          int d2, int x)
{
    // Calculate GCD of d1 and d2
    int gcd = __gcd(d1, d2);

    // If position is not reachable
    // return -1
    if ((k - x) % gcd != 0)
        return -1;

    // Queue for BFS
    Queue<pair> q = new Queue<pair>();

    // Hash Table for marking
    // visited positions
    HashSet<int> visited = new HashSet<int>();

    // we need 0 steps to reach K
    q.Enqueue(new pair(k, 0));

    // Mark starting position
    // as visited
    visited.Add(k);

    while (q.Count != 0)
    {
        int s = q.Peek().first;

        // stp is the number of steps
        // to reach position s
        int stp = q.Peek().second;

        if (s == x)
            return stp;

        q.Dequeue();

        if (!visited.Contains(s + d1))
        {

            // if position not visited
            // add to queue and mark visited
            q.Enqueue(new pair(s + d1, stp + 1));

            visited.Add(s + d1);
        }

        if (!visited.Contains(s + d2))
        {
            q.Enqueue(new pair(s + d2, stp + 1));
            visited.Add(s + d2);
        }

        if (!visited.Contains(s - d1))
        {
            q.Enqueue(new pair(s - d1, stp + 1));
            visited.Add(s - d1);
        }
        if (!visited.Contains(s - d2))
        {
            q.Enqueue(new pair(s - d2, stp + 1));
            visited.Add(s - d2);
        }
    }
    return int.MinValue;
}

// Driver Code
public static void Main(String[] args)
{
    int k = 10, d1 = 4, d2 = 6, x = 8;

    Console.WriteLine(minStepsNeeded(k, d1, d2, x));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

function __gcd(a,b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to perform BFS traversal to
// find minimum number of step needed
// to reach x from K
function minStepsNeeded(k,d1,d2,x)
{
    // Calculate GCD of d1 and d2
    let gcd = __gcd(d1, d2);

    // If position is not reachable
    // return -1
    if ((k - x) % gcd != 0)
        return -1;

    // Queue for BFS
    let q = [];

    // Hash Table for marking
    // visited positions
    let visited = new Set();

    // we need 0 steps to reach K
    q.push([k, 0 ]);

    // Mark starting position
    // as visited
    visited.add(k);

    while (q.length!=0)
    {
        let s = q[0][0];

        // stp is the number of steps
        // to reach position s
        let stp = q[0][1];

        if (s == x)
            return stp;

        q.shift();

        if (!visited.has(s + d1))
        {

            // if position not visited
            // add to queue and mark visited
            q.push([s + d1, stp + 1]);

            visited.add(s + d1);
        }

        if (!visited.has(s + d2))
        {
            q.push([s + d2, stp + 1]);
            visited.add(s + d2);
        }

        if (!visited.has(s - d1))
        {
            q.push([s - d1, stp + 1]);
            visited.add(s - d1);
        }
        if (!visited.has(s - d2))
        {
            q.push([s - d2, stp + 1]);
            visited.add(s - d2);
        }
    }
    return Number.MIN_VALUE;
}

// Driver Code
let k = 10, d1 = 4, d2 = 6, x = 8;
document.write(minStepsNeeded(k, d1, d2, x));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(|k-x|)

**辅助空间:** O(|k-x|)