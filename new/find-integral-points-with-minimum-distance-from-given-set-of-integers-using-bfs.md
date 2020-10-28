# 使用 BFS 查找与给定整数集之间最小距离的积分点

给定长度为 **N** 的整数数组 **A []** 和整数 **K** 。 任务是找到给定数组中不存在的 **K** 个不同积分点，以使它们与 **A []** 中最近点的距离之和最小。

> **积分点**被定义为两个坐标均为整数的点。 另外，在 x 轴上，我们不需要考虑 y 坐标，因为所有点的 y 坐标都等于零。

**示例**：

> **输入**：A [] = {-1，4，6}，K = 3
> **输出**：-2，0，3
> **说明**：
> A []中-2 的最近点是-1->距离= 1
> A []中 0 的最近点是-1->距离= 1
> 最近点 对于 3 in A []为 4->距离= 1
> 总距离= 1 +1 + 1 = 3，这是最小的可能距离。
> 在相同的最小距离下，其他结果也是可能的。
> **输入**：A [] = {0，1，3，4}，K = 5
> **输出**：-1，2，5，-2，6
> **解释**：
> A []中-1 的最近点是 0->距离= 1
> A []中 2 的最近点是 3->距离 = 1
> A []中 5 的最近点是 4->距离= 1
> A []中-2 的最近点是 0->距离= 2
> 6 的最近点 在 A []中为 4->距离= 2
> 总距离= 2 +1 + 1 +1 + 2 = 7，这是最小可能距离。

**方法**：我们将使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)的概念来解决此问题。

1.  我们首先将给定的整数集作为根元素，并将其推送到[队列](http://www.geeksforgeeks.org/queue-data-structure/)和[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)中。

2.  然后对于任何说 X 的元素，我们将仅使用哈希图检查是否遇到（X-1）或（X + 1）。 如果到目前为止还没有遇到任何问题，那么我们将该元素推送到答案数组中，并同时进行队列和哈希处理。

3.  重复此过程，直到遇到 K 个新元素。

下面是上述方法的实现。

## C++

```cpp

// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find points at
// minimum distance
void minDistancePoints(int A[],
                      int K,
                      int n)
{

    // Hash to store points
    // that are encountered
    map<int, int> m;

    // Queue to store initial
    // set of points
    queue<int> q;

    for (int i = 0; i < n; ++i) {
        m[A[i]] = 1;
        q.push(A[i]);
    }

    // Vector to store integral
    // points
    vector<int> ans;

    // Using bfs to visit nearest
    // points from already
    // visited points
    while (K > 0) {

        // Get first element from
        // queue
        int x = q.front();
        q.pop();

        // Check if (x-1) is not
        // encountered so far
        if (!m[x - 1] && K > 0) {
            // Update hash with
            // this new element
            m[x - 1] = 1;

            // Insert (x-1) into
            // queue
            q.push(x - 1);

            // Push (x-1) as
            // new element
            ans.push_back(x - 1);

            // Decrement counter
            // by 1
            K--;
        }

        // Check if (x+1) is not
        // encountered so far
        if (!m[x + 1] && K > 0) {
            // Update hash with
            // this new element
            m[x + 1] = 1;

            // Insert (x+1) into
            // queue
            q.push(x + 1);

            // Push (x+1) as
            // new element
            ans.push_back(x + 1);

            // Decrement counter
            // by 1
            K--;
        }
    }

    // Print result array
    for (auto i : ans)
        cout << i << " ";
}

// Driver code
int main()
{

    int A[] = { -1, 4, 6 };
    int K = 3;
    int n = sizeof(A) / sizeof(A[0]);

    minDistancePoints(A, K, n);

    return 0;
}

```

## Java

```java

// Java implementation of above approach
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Map;
import java.util.Queue;

class Geeks{

// Function to find points at
// minimum distance
static void minDistancePoints(int A[], 
                              int K, int n)
{

    // Hash to store points
    // that are encountered
    Map<Integer, 
        Boolean> m = new HashMap<Integer, 
                                 Boolean>();

    // Queue to store initial
    // set of points
    Queue<Integer> q = new LinkedList<Integer>();

    for(int i = 0; i < n; ++i)
    {
        m.put(A[i], true);
        q.add(A[i]);
    }

    // List to store integral
    // points
    LinkedList<Integer> ans = new LinkedList<Integer>();

    // Using bfs to visit nearest
    // points from already
    // visited points
    while (K > 0)
    {

        // Get first element from
        // queue
        int x = q.poll();

        // Check if (x-1) is not
        // encountered so far
        if (!m.containsKey(x - 1) && K > 0) 
        {

            // Update hash with
            // this new element
            m.put(x - 1, true);

            // Insert (x-1) into
            // queue
            q.add(x - 1);

            // Push (x-1) as
            // new element
            ans.add(x - 1);

            // Decrement counter
            // by 1
            K--;
        }

        // Check if (x+1) is not
        // encountered so far
        if (!m.containsKey(x + 1) && K > 0)
        {

            // Update hash with
            // this new element
            m.put(x + 1, true);

            // Insert (x+1) into
            // queue
            q.add(x + 1);

            // Push (x+1) as
            // new element
            ans.add(x + 1);

            // Decrement counter
            // by 1
            K--;
        }
    }

    // Print result array
    for(Integer i : ans)
        System.out.print(i + " ");
}

// Driver code
public static void main(String[] args)
{
    int A[] = new int[] { -1, 4, 6 };
    int K = 3;
    int n = A.length;

    minDistancePoints(A, K, n);
}
}

// This code is contributed by Rajnis09

```

## Python3

```py

# Python 3 implementation
# of above approach

# Function to find points 
# at minimum distance
def minDistancePoints(A, K, n):

    # Hash to store points
    # that are encountered
    m = {}

    # Queue to store initial
    # set of points
    q = []

    for i in range(n):
        m[A[i]] = 1
        q.append(A[i])

    # Vector to store 
    # integral points
    ans = []

    # Using bfs to visit nearest
    # points from already
    # visited points
    while (K > 0):

        # Get first element from
        # queue
        x = q[0]
        q = q[1::]

        # Check if (x-1) is not
        # encountered so far
        if ((x - 1) not in m and
             K > 0):

            # Update hash with
            # this new element
            m[x - 1] = m.get(x - 1, 0) + 1

            # Insert (x-1) into
            # queue
            q.append(x - 1)

            # Push (x-1) as
            # new element
            ans.append(x - 1)

            # Decrement counter
            # by 1
            K -= 1

        # Check if (x+1) is not
        # encountered so far
        if ((x + 1) not in m and
             K > 0):
            # Update hash with
            # this new element
            m[x + 1] = m.get(x + 1, 0) + 1

            # Insert (x+1) into
            # queue
            q.append(x + 1)

            # Push (x+1) as
            # new element
            ans.append(x + 1)
            # Decrement counter
            # by 1
            K -= 1

    # Print result array
    for i in ans:
        print(i, end = " ")

# Driver code
if __name__ == '__main__':

    A =  [-1, 4, 6]
    K = 3
    n =  len(A)
    minDistancePoints(A, K, n)

# This code is contributed by bgangwar59

```

## C#

```cs

// C# implementation of above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find points at
// minimum distance
static void minDistancePoints(int []A, 
                              int K, int n)
{

    // Hash to store points
    // that are encountered
    Dictionary<int, 
               Boolean> m = new Dictionary<int, 
                                           Boolean>();

    // Queue to store initial
    // set of points
    Queue<int> q = new Queue<int>();

    for(int i = 0; i < n; ++i)
    {
        m.Add(A[i], true);
        q.Enqueue(A[i]);
    }

    // List to store integral
    // points
    List<int> ans = new List<int>();

    // Using bfs to visit nearest
    // points from already
    // visited points
    while (K > 0)
    {

        // Get first element from
        // queue
        int x = q.Dequeue();

        // Check if (x-1) is not
        // encountered so far
        if (!m.ContainsKey(x - 1) && K > 0) 
        {

            // Update hash with
            // this new element
            m.Add(x - 1, true);

            // Insert (x-1) into
            // queue
            q.Enqueue(x - 1);

            // Push (x-1) as
            // new element
            ans.Add(x - 1);

            // Decrement counter
            // by 1
            K--;
        }

        // Check if (x+1) is not
        // encountered so far
        if (!m.ContainsKey(x + 1) && K > 0)
        {

            // Update hash with
            // this new element
            m.Add(x + 1, true);

            // Insert (x+1) into
            // queue
            q.Enqueue(x + 1);

            // Push (x+1) as
            // new element
            ans.Add(x + 1);

            // Decrement counter
            // by 1
            K--;
        }
    }

    // Print result array
    foreach(int i in ans)
        Console.Write(i + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []A = new int[] { -1, 4, 6 };
    int K = 3;
    int n = A.Length;

    minDistancePoints(A, K, n);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
-2 0 3

```

***时间复杂度**：O（M * log（M））*，其中 M = N +K。



* * *

* * *



