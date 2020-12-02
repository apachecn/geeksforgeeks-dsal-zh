# 使用广度优先搜索解决供水问题

> 原文： [https://www.geeksforgeeks.org/implementing-water-supply-problem-using-breadth-first-search/](https://www.geeksforgeeks.org/implementing-water-supply-problem-using-breadth-first-search/)

给定使用 **N-1** 条道路连接的 **N 个**城市。 在城市 **[i，i + 1]** 之间，从[1]到 N-1 的所有`i`都有一条边。
该任务是建立供水连接。 将供水设置在一个城市中，然后使用公路运输将水从该城市输送到其他城市。 某些城市被封锁，这意味着水无法通过该特定城市。 确定可以供水的最大城市数。
**输入格式**：

*   第一行包含一个整数> strong> N，表示城市数。
*   接下来的 N-1 行包含两个以空格分隔的整数 **u v** ，表示在
    城市 u 和 v 之间的道路。
*   下一行包含 N 个以空格分隔的整数，如果第个城市的**被阻止，则为 1，否则为 0。**

**示例**：

> **输入**：
> 4
> 1 2
> 2 3
> 3 4
> 0 1 1 0
> **输出**：
> 2
> **说明**：如果选择了城市 1，则从
> 城市 1 到 2 供水。如果选择了城市 4，则从城市 4 到 3 供水
> ，因此最大为 2。 可以给城市供水。
> **输入**：
> 7
> 1 2
> 2 3
> 3 4
> 4 5
> 5 6
> 6 7
> 0 1 1 0 0 0 0
> **输出**：
> 5
> **说明**：如果选择城市 1，则从
> 城市 1 到 2 供应水，或者 选择了城市 4，从城市 4 向
> 3、5、6 和 7 供应水，因此最多 5 个城市被供水。

**方法**：
在本文中，将讨论基于 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 的解决方案。
我们在每个城市上进行广度优先搜索，并检查以下两项内容：该城市未被阻止且该城市未被访问。 如果这两个条件都返回 true，则我们从该城市进行广度优先搜索，并计算可以供水的城市数量。
也可以使用深度优先搜索来实现此解决方案。
以下是上述方法的实现：

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

**输出**：

```
2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。