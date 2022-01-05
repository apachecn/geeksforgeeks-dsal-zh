# 利用广度优先搜索实现供水问题

> 原文:[https://www . geesforgeks . org/implementing-供水-问题-使用-广度优先-搜索/](https://www.geeksforgeeks.org/implementing-water-supply-problem-using-breadth-first-search/)

给定使用 **N-1** 道路连接的 **N** 个城市。在城市**【I，I+1】**之间，从 1 到 N-1 的所有 **i** 都存在一条边。
任务是建立供水连接。在一个城市设置供水，水通过公路运输从该城市输送到其他城市。某些城市被封锁，这意味着水不能通过那个特定的城市。确定可供水的最大城市数量。
**输入格式:**

*   第一行包含一个表示城市数量的整数。
*   接下来的 N-1 行包含两个用空格分隔的整数 **u v** ，表示
    城市 u 和 v 之间的道路
*   下一行包含 N 个用空格分隔的整数，其中如果第**个第**个城市被
    封锁，则为 1，否则为 0。

**示例:**

> **输入:**
> 4
> 1 2
> 2 3
> 3 4
> 0 1 1 0
> **输出:**
> 2
> **说明:**如果选择城市 1，则从
> 城市 1 至 2 供水。如果选择城市 4，则从城市 4 到 3
> 供水，因此最多可向 2 个城市供水。
> **输入:**
> 7
> 1 2
> 2 3
> 3 4
> 4 5
> 5 6
> 6 7
> 0 1 0 0 0
> **输出:**
> 5
> **解释:**如果选择城市 1，则从
> 城市 1 至 2 供水，或者如果选择城市 4，则从城市 4 至供水

**方法:**
在这篇文章中，讨论了一个基于 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 的解决方案。
我们对每个城市进行广度优先搜索，检查两点:城市没有被封锁，城市没有被访问。如果这两个条件都成立，那么我们从该城市开始进行广度优先搜索，并计算可供水的城市数量。
这个解决方案也可以使用深度优先搜索来实现。
以下是上述方法的实现:

## C++

```
// C++ program to solve water
// supply problem using BFS

#include <iostream>
#include <vector>
#include <queue>
using namespace std;

// Function to perform BFS
int bfsUtil(int v[], bool vis[], vector<int> adj[],
                                            int src)
{
    // Mark current source visited
    vis[src] = true;

    queue<int> q; //Queue for BFS
    q.push(src); // Push src to queue

    int count = 0;
    while (!q.empty()) {

        int p = q.front();

        for (int i = 0; i < adj[p].size(); i++) {

            // When the adjacent city not visited and
            // not blocked, push city in the queue.
            if (!vis[adj[p][i]] && v[adj[p][i]] == 0) {
                count++;
                vis[adj[p][i]] = true;
                q.push(adj[p][i]);
            }

            // when the adjacent city is not visited
            // but blocked so the blocked city is
            // not pushed in queue
            else if (!vis[adj[p][i]] && v[adj[p][i]] == 1) {
                count++;
            }
        }
        q.pop();
    }

    return count + 1;
}

// Utility function to perform BFS
int bfs(int N, int v[], vector<int> adj[])
{
    bool vis[N + 1];
    int max = 1, res;

    // marking visited array false
    for (int i = 1; i <= N; i++)
        vis[i] = false;

    // Check for each and every city
    for (int i = 1; i <= N; i++) {
        // Checks that city is not blocked
        // and not visited.
        if (v[i] == 0 && !vis[i]) {
            res = bfsUtil(v, vis, adj, i);
            if (res > max) {
                max = res;
            }
        }
    }

    return max;
}

// Driver Code
int main()
{
    int N = 4; // Denotes the number of cities
    vector<int> adj[N + 1];
    int v[N + 1];

    // Adjacency list denoting road
    // between city u and v
    adj[1].push_back(2);
    adj[2].push_back(1);
    adj[2].push_back(3);
    adj[3].push_back(2);
    adj[3].push_back(4);
    adj[4].push_back(3);

    // array for storing whether ith
    // city is blocked or not
    v[1] = 0;
    v[2] = 1;
    v[3] = 1;
    v[4] = 0;

    cout<<bfs(N, v, adj);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve water
// supply problem using BFS
import java.util.*;

class GFG{

// Function to perform BFS
static int bfsUtil(int v[], boolean vis[],
                   Vector<Integer> adj[],
                   int src)
{

    // Mark current source visited
    vis[src] = true;

    // Queue for BFS
    Queue<Integer> q = new LinkedList<>();

    // Push src to queue
    q.add(src);

    int count = 0;
    while (!q.isEmpty())
    {
        int p = q.peek();

        for(int i = 0; i < adj[p].size(); i++)
        {

            // When the adjacent city not
            // visited and not blocked, push
            // city in the queue.
            if (!vis[adj[p].get(i)] &&
                   v[adj[p].get(i)] == 0)
            {
                count++;
                vis[adj[p].get(i)] = true;
                q.add(adj[p].get(i));
            }

            // When the adjacent city is not visited
            // but blocked so the blocked city is
            // not pushed in queue
            else if (!vis[adj[p].get(i)] &&
                        v[adj[p].get(i)] == 1)
            {
                count++;
            }
        }
        q.remove();
    }
    return count + 1;
}

// Utility function to perform BFS
static int bfs(int N, int v[],
        Vector<Integer> adj[])
{
    boolean []vis = new boolean[N + 1];
    int max = 1, res;

    // Marking visited array false
    for(int i = 1; i <= N; i++)
        vis[i] = false;

    // Check for each and every city
    for(int i = 1; i <= N; i++)
    {

        // Checks that city is not blocked
        // and not visited.
        if (v[i] == 0 && !vis[i])
        {
            res = bfsUtil(v, vis, adj, i);
            if (res > max)
            {
                max = res;
            }
        }
    }
    return max;
}

// Driver Code
public static void main(String[] args)
{

    // Denotes the number of cities
    int N = 4;

    @SuppressWarnings("unchecked")
    Vector<Integer> []adj = new Vector[N + 1];
    for (int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    int []v = new int[N + 1];

    // Adjacency list denoting road
    // between city u and v
    adj[1].add(2);
    adj[2].add(1);
    adj[2].add(3);
    adj[3].add(2);
    adj[3].add(4);
    adj[4].add(3);

    // Array for storing whether ith
    // city is blocked or not
    v[1] = 0;
    v[2] = 1;
    v[3] = 1;
    v[4] = 0;

    System.out.print(bfs(N, v, adj));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to solve water
# supply problem using BFS

# Function to perform BFS
def bfsUtil(v, vis, adj, src):

    # Mark current source visited
    vis[src] = True

    # Queue for BFS   
    q = []

    # Push src to queue
    q.append(src)

    count = 0
    while (len(q) != 0):
        p = q[0]

        for i in range(len(adj[p])):

            # When the adjacent city not visited and
            # not blocked, push city in the queue.
            if (vis[adj[p][i]] == False and v[adj[p][i]] == 0):
                count += 1
                vis[adj[p][i]] = True
                q.push(adj[p][i])

            # when the adjacent city is not visited
            # but blocked so the blocked city is
            # not pushed in queue
            elif(vis[adj[p][i]] == False and v[adj[p][i]] == 1):
                count += 1
        q.remove(q[0])

    return count + 1

# Utility function to perform BFS
def bfs(N, v, adj):
    vis = [ 0 for i in range(N + 1)]
    mx = 1

    # marking visited array false
    for i in range(1, N + 1, 1):
        vis[i] = False

    # Check for each and every city
    for i in range(1, N + 1, 1):

        # Checks that city is not blocked
        # and not visited.
        if (v[i] == 0 and vis[i] == False):
            res = bfsUtil(v, vis, adj, i)
            if (res > mx):
                mx = res

    return mx

# Driver Code
if __name__ == '__main__':
    N = 4

    # Denotes the number of cities
    adj = [[] for i in range(N + 1)]
    v = [0 for i in range(N + 1)]

    # Adjacency list denoting road
    # between city u and v
    adj[1].append(2)
    adj[2].append(1)
    adj[2].append(3)
    adj[3].append(2)
    adj[3].append(4)
    adj[4].append(3)

    # array for storing whether ith
    # city is blocked or not
    v[1] = 0
    v[2] = 1
    v[3] = 1
    v[4] = 0

    print(bfs(N, v, adj))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to solve water
// supply problem using BFS
using System;
using System.Collections.Generic;
class GFG{

// Function to perform BFS
static int bfsUtil(int []v, bool []vis,
                   List<int> []adj,
                   int src)
{
  // Mark current source visited
  vis[src] = true;

  // Queue for BFS
  Queue<int> q = new Queue<int>();

  // Push src to queue
  q.Enqueue(src);

  int count = 0;
  while (q.Count != 0)
  {
    int p = q.Peek();
    for(int i = 0; i < adj[p].Count; i++)
    {
      // When the adjacent city not
      // visited and not blocked, push
      // city in the queue.
      if (!vis[adj[p][i]] &&
          v[adj[p][i]] == 0)
      {
        count++;
        vis[adj[p][i]] = true;
        q.Enqueue(adj[p][i]);
      }

      // When the adjacent city is not visited
      // but blocked so the blocked city is
      // not pushed in queue
      else if (!vis[adj[p][i]] &&
               v[adj[p][i]] == 1)
      {
        count++;
      }
    }
    q.Dequeue();
  }
  return count + 1;
}

// Utility function to perform BFS
static int bfs(int N, int []v,
               List<int> []adj)
{
  bool []vis = new bool[N + 1];
  int max = 1, res;

  // Marking visited array false
  for(int i = 1; i <= N; i++)
    vis[i] = false;

  // Check for each and every city
  for(int i = 1; i <= N; i++)
  {
    // Checks that city is not blocked
    // and not visited.
    if (v[i] == 0 && !vis[i])
    {
      res = bfsUtil(v, vis, adj, i);
      if (res > max)
      {
        max = res;
      }
    }
  }
  return max;
}

// Driver Code
public static void Main(String[] args)
{
  // Denotes the number of cities
  int N = 4;

  List<int> []adj = new List<int>[N + 1];
  for (int i = 0; i < adj.Length; i++)
    adj[i] = new List<int>();

  int []v = new int[N + 1];

  // Adjacency list denoting road
  // between city u and v
  adj[1].Add(2);
  adj[2].Add(1);
  adj[2].Add(3);
  adj[3].Add(2);
  adj[3].Add(4);
  adj[4].Add(3);

  // Array for storing whether ith
  // city is blocked or not
  v[1] = 0;
  v[2] = 1;
  v[3] = 1;
  v[4] = 0;

  Console.Write(bfs(N, v, adj));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program to solve water
    // supply problem using BFS

    // Function to perform BFS
    function bfsUtil(v, vis, adj, src)
    {

        // Mark current source visited
        vis[src] = true;

        // Queue for BFS
        let q = [];

        // Push src to queue
        q.push(src);

        let count = 0;
        while (q.length > 0)
        {
            let p = q[0];

            for(let i = 0; i < adj[p].length; i++)
            {

                // When the adjacent city not
                // visited and not blocked, push
                // city in the queue.
                if (!vis[adj[p][i]] &&
                       v[adj[p][i]] == 0)
                {
                    count++;
                    vis[adj[p][i]] = true;
                    q.add(adj[p][i]);
                }

                // When the adjacent city is not visited
                // but blocked so the blocked city is
                // not pushed in queue
                else if (!vis[adj[p][i]] &&
                            v[adj[p][i]] == 1)
                {
                    count++;
                }
            }
            q.shift();
        }
        return count + 1;
    }

    // Utility function to perform BFS
    function bfs(N, v, adj)
    {
        let vis = new Array(N + 1);
        let max = 1, res;

        // Marking visited array false
        for(let i = 1; i <= N; i++)
            vis[i] = false;

        // Check for each and every city
        for(let i = 1; i <= N; i++)
        {

            // Checks that city is not blocked
            // and not visited.
            if (v[i] == 0 && !vis[i])
            {
                res = bfsUtil(v, vis, adj, i);
                if (res > max)
                {
                    max = res;
                }
            }
        }
        return max;
    }

    // Denotes the number of cities
    let N = 4;

    let adj = new Array(N + 1);
    for (let i = 0; i < adj.length; i++)
        adj[i] = [];

    let v = new Array(N + 1);

    // Adjacency list denoting road
    // between city u and v
    adj[1].push(2);
    adj[2].push(1);
    adj[2].push(3);
    adj[3].push(2);
    adj[3].push(4);
    adj[4].push(3);

    // Array for storing whether ith
    // city is blocked or not
    v[1] = 0;
    v[2] = 1;
    v[3] = 1;
    v[4] = 0;

    document.write(bfs(N, v, adj));

    // This code is contributed by divyeshrabadiya07.

</script>
```

**输出:**

```
2
```