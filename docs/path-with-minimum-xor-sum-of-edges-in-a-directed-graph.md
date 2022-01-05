# 有向图中边的异或和最小的路径

> 原文:[https://www . geesforgeks . org/有向图中最小异或边和路径/](https://www.geeksforgeeks.org/path-with-minimum-xor-sum-of-edges-in-a-directed-graph/)

给定一个具有 **N** 节点和 **E** 边的有向图，一个源 **S** 和一个目的地 **D** 节点。任务是找到 **S** 到 **D** 边异或和最小的路径。如果 **S** 到 **D** 之间没有路径，则打印 **-1** 。

**示例:**

> **输入:** N = 3，E = 3，边= {{1，2}，5}，{ { 1，3}，9}，{{2，3}，1}}，S = 1，D = 3
> **输出:** 4
> 边权重 XOR 最小的路径将是 1- > 2- > 3
> ，XOR 和为 5^1 = 4。
> 
> **输入:** N = 3，E = 3，边= {{3，2}，5}，{{3，3}，9}，{ { 3，3}，1}，S = 1，D = 3
> **输出:** -1

**方法:**思路是用[迪克斯特拉的最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)稍加变异。以下是解决该问题的分步方法:

*   **基本情况:**如果源节点等于目的节点，则返回 **0** 。
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，源节点及其权重为 **0** 和一个已访问的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)。
*   当优先级队列不为空时:
    1.  从优先级队列中弹出最上面的元素。让我们称它为当前节点。
    2.  检查当前节点是否已经在被访问阵列的帮助下被访问，如果是，则继续。
    3.  如果当前节点是目的节点，则返回当前节点到源节点的异或和距离。
    4.  迭代所有与当前节点相邻的节点，将其推入优先级队列，并将它们的距离与当前距离和边权重进行异或求和。
*   否则，没有从源到目标的路径。因此，返回-1

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest
// xor sum of edges
double minXorSumOfEdges(
    int s, int d,
    vector<vector<pair<int, int> > > gr)
{
    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    set<pair<int, int> > pq;
    pq.insert({ 0, s });

    // Visited array
    bool v[gr.size()] = { 0 };

    // While the priority-queue
    // is not empty
    while (pq.size()) {

        // Current node
        int curr = pq.begin()->second;

        // Current xor sum of distance
        int dist = pq.begin()->first;

        // Popping the top-most element
        pq.erase(pq.begin());

        // If already visited continue
        if (v[curr])
            continue;

        // Marking the node as visited
        v[curr] = 1;

        // If it is a destination node
        if (curr == d)
            return dist;

        // Traversing the current node
        for (auto it : gr[curr])
            pq.insert({ dist ^ it.second,
                        it.first });
    }

    // If no path exists
    return -1;
}

// Driver code
int main()
{
    int n = 3;

    // Graph as adjacency matrix
    vector<vector<pair<int, int> > >
        gr(n + 1);

    // Input edges
    gr[1].push_back({ 3, 9 });
    gr[2].push_back({ 3, 1 });
    gr[1].push_back({ 2, 5 });

    // Source and destination
    int s = 1, d = 3;

    cout << minXorSumOfEdges(s, d, gr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.PriorityQueue;
import java.util.ArrayList;

class Pair implements Comparable<Pair>
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }

    @Override
    public int compareTo(Pair p)
    {
        if (this.first == p.first)
        {
            return this.second - p.second;
        }
        return this.first - p.first;
    }
}

class GFG{

// Function to return the smallest
// xor sum of edges
static int minXorSumOfEdges(int s, int d, 
                            ArrayList<ArrayList<Pair>> gr)
{

    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    PriorityQueue<Pair> pq = new PriorityQueue<>();
    pq.add(new Pair(0, s));

    // Visited array
    boolean[] v = new boolean[gr.size()];

    // While the priority-queue
    // is not empty
    while (!pq.isEmpty())
    {

        // Iterator<Pair> itr = pq.iterator();
        // Current node
        Pair p = pq.poll();
        int curr = p.second;

        // Current xor sum of distance
        int dist = p.first;

        // If already visited continue
        if (v[curr])
            continue;

        // Marking the node as visited
        v[curr] = true;

        // If it is a destination node
        if (curr == d)
            return dist;

        // Traversing the current node
        for(Pair it : gr.get(curr))
            pq.add(new Pair(dist ^ it.second, it.first));
    }

    // If no path exists
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    // Graph as adjacency matrix
    ArrayList<ArrayList<Pair>> gr = new ArrayList<>();
    for(int i = 0; i < n + 1; i++)
    {
        gr.add(new ArrayList<Pair>());
    }

    // Input edges
    gr.get(1).add(new Pair(3, 9));
    gr.get(2).add(new Pair(3, 1));
    gr.get(1).add(new Pair(2, 5));

    // Source and destination
    int s = 1, d = 3;
    System.out.println(minXorSumOfEdges(s, d, gr));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque

# Function to return the smallest
# xor sum of edges
def minXorSumOfEdges(s, d, gr):

    # If the source is equal
    # to the destination
    if (s == d):
        return 0

    # Initialise the priority queue
    pq = []
    pq.append((0, s))

    # Visited array
    v = [0] * len(gr)

    # While the priority-queue
    # is not empty
    while (len(pq) > 0):
        pq = sorted(pq)

        # Current node
        curr = pq[0][1]

        # Current xor sum of distance
        dist = pq[0][0]

        # Popping the top-most element
        del pq[0]

        # If already visited continue
        if (v[curr]):
            continue

        # Marking the node as visited
        v[curr] = 1

        # If it is a destination node
        if (curr == d):
            return dist

        # Traversing the current node
        for it in gr[curr]:
            pq.append((dist ^ it[1],
                              it[0]))
    # If no path exists
    return -1

# Driver code
if __name__ == '__main__':

    n = 3

    # Graph as adjacency matrix
    gr = [[] for i in range(n + 1)]

    # Input edges
    gr[1].append([ 3, 9 ])
    gr[2].append([ 3, 1 ])
    gr[1].append([ 2, 5 ])

    # Source and destination
    s = 1
    d = 3

    print(minXorSumOfEdges(s, d, gr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to return the smallest
  // xor sum of edges
  static int minXorSumOfEdges(int s, int d, List<List<Tuple<int,int>>> gr)
  {

    // If the source is equal
    // to the destination
    if (s == d)
      return 0;

    // Initialise the priority queue
    List<Tuple<int,int>> pq = new List<Tuple<int,int>>();
    pq.Add(new Tuple<int,int>(0, s));

    // Visited array
    int[] v = new int[gr.Count];

    // While the priority-queue
    // is not empty
    while (pq.Count > 0)
    {
      pq.Sort();

      // Current node
      int curr = pq[0].Item2;

      // Current xor sum of distance
      int dist = pq[0].Item1;

      // Popping the top-most element
      pq.RemoveAt(0);

      // If already visited continue
      if(v[curr] != 0)
        continue;

      // Marking the node as visited
      v[curr] = 1;

      // If it is a destination node
      if (curr == d)
        return dist;

      // Traversing the current node
      foreach(Tuple<int,int> it in gr[curr])
      {
        pq.Add(new Tuple<int,int>(dist ^ it.Item2, it.Item1));
      }
    }

    // If no path exists
    return -1;
  }

  // Driver code
  static void Main()
  {
    int n = 3;

    // Graph as adjacency matrix
    List<List<Tuple<int,int>>> gr = new List<List<Tuple<int,int>>>();

    for(int i = 0; i < n + 1; i++)
    {
      gr.Add(new List<Tuple<int,int>>());
    }

    // Input edges
    gr[1].Add(new Tuple<int,int>(3, 9));
    gr[2].Add(new Tuple<int,int>(3, 1));
    gr[1].Add(new Tuple<int,int>(2, 5));

    // Source and destination
    int s = 1;
    int d = 3;

    Console.WriteLine(minXorSumOfEdges(s, d, gr));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest
// xor sum of edges
function minXorSumOfEdges(s, d, gr)
{

    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    let pq = [];
    pq.push([0, s]);

    // Visited array
    let v = new Array(gr.length);

    // While the priority-queue
    // is not empty
    while (pq.length != 0)
    {
        pq.sort(function(a, b){return a[0] - b[0];});

        // Iterator<Pair> itr = pq.iterator();
        // Current node
        let p = pq.shift();
        let curr = p[1];

        // Current xor sum of distance
        let dist = p[0];

        // If already visited continue
        if (v[curr])
            continue;

        // Marking the node as visited
        v[curr] = true;

        // If it is a destination node
        if (curr == d)
            return dist;

        // Traversing the current node
        for(let it = 0; it < gr[curr].length; it++)
            pq.push([dist ^ gr[curr][it][1],
                            gr[curr][it][0]]);
    }

    // If no path exists
    return -1;
}

// Driver code
let n = 3;

// Graph as adjacency matrix
let gr = [];
for(let i = 0; i < n + 1; i++)
{
    gr.push([]);
}

// Input edges
gr[1].push([3, 9]);
gr[2].push([3, 1]);
gr[1].push([2, 5]);

// Source and destination
let s = 1, d = 3;

document.write(minXorSumOfEdges(s, d, gr));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O((E+V)logV)*T4】