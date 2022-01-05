# 边与权重乘积最小的路径> = 1

> 原文:[https://www . geeksforgeeks . org/重量最小的边积路径-1/](https://www.geeksforgeeks.org/path-with-smallest-product-of-edges-with-weight-1/)

给定具有 **N** 个节点和 **E** 条边的有向图，其中每条边的权重为 **> 1** ，还给定了源 **S** 和目的地 **D** 。任务是找到从 **S** 到 **D** 边积最小的路径。如果没有从 **S** 到 **D** 的路径，则打印 **-1** 。

**示例:**

> **输入:** N = 3，E = 3，边= {{1，2}，5}，{ { 1，3}，9}，{{2，3}，1}}，S = 1，D = 3
> **输出:** 5
> 边乘积最小的路径将是 1- > 2- > 3
> ，乘积为 5*1 = 5。
> 
> **输入:** N = 3，E = 3，边= {{3，2}，5}，{{3，3}，9}，{ { 3，3}，1}，S = 1，D = 3
> **输出:** -1

**方法:**思路是用[迪克斯特拉的最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)稍加变异。
可以按照以下步骤计算结果:

*   如果源等于目的地，则返回 **0** 。
*   用 **S** 及其权重为 **1** 和访问数组**v[**初始化优先级队列 **pq** 。
*   当 **pq** 不为空时:
    1.  从 **pq** 弹出最上面的元素。我们称之为 **curr** ，它的距离乘积为 **dist** 。
    2.  如果已经访问了 **curr** ，则继续。
    3.  如果 **curr** 等于 **D** ，则返回 **dist** 。
    4.  迭代所有与 **curr** 相邻的节点，推入 **pq** (下一个和 dist + gr[nxt]。重量)
*   返回 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the smallest
// product of edges
double dijkstra(int s, int d,
                vector<vector<pair<int, double> > > gr)
{
    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    set<pair<int, int> > pq;
    pq.insert({ 1, s });

    // Visited array
    bool v[gr.size()] = { 0 };

    // While the priority-queue
    // is not empty
    while (pq.size()) {

        // Current node
        int curr = pq.begin()->second;

        // Current product of distance
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
            pq.insert({ dist * it.second, it.first });
    }

    // If no path exists
    return -1;
}

// Driver code
int main()
{
    int n = 3;

    // Graph as adjacency matrix
    vector<vector<pair<int, double> > > gr(n + 1);

    // Input edges
    gr[1].push_back({ 3, 9 });
    gr[2].push_back({ 3, 1 });
    gr[1].push_back({ 2, 5 });

    // Source and destination
    int s = 1, d = 3;

    // Dijkstra
    cout << dijkstra(s, d, gr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.PriorityQueue;

class Pair implements Comparable<Pair>
{
    int first, second;

    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }

    public int compareTo(Pair o)
    {
        if (this.first == o.first)
        {
            return this.second - o.second;
        }
        return this.first - o.first;
    }
}

class GFG{

// Function to return the smallest
// xor sum of edges
static int dijkstra(int s, int d,
                    ArrayList<ArrayList<Pair>> gr)
{

    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    PriorityQueue<Pair> pq = new PriorityQueue<>();
    pq.add(new Pair(1, s));

    // Visited array
    boolean[] v = new boolean[gr.size()];

    // While the priority-queue
    // is not empty
    while (!pq.isEmpty())
    {

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

    System.out.println(dijkstra(s, d, gr));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the smallest
# product of edges
def dijkstra(s, d, gr) :

    # If the source is equal
    # to the destination
    if (s == d) :
        return 0;

    # Initialise the priority queue
    pq = [];
    pq.append(( 1, s ));

    # Visited array
    v = [0]*(len(gr) + 1);

    # While the priority-queue
    # is not empty
    while (len(pq) != 0) :

        # Current node
        curr = pq[0][1];

        # Current product of distance
        dist = pq[0][0];

        # Popping the top-most element
        pq.pop();

        # If already visited continue
        if (v[curr]) :
            continue;

        # Marking the node as visited
        v[curr] = 1;

        # If it is a destination node
        if (curr == d) :
            return dist;

        # Traversing the current node
        for it in gr[curr] :
            if it not in pq :
                pq.insert(0,( dist * it[1], it[0] ));

    # If no path exists
    return -1;

# Driver code
if __name__ == "__main__" :

    n = 3;

    # Graph as adjacency matrix
    gr = {};

    # Input edges
    gr[1] = [( 3, 9) ];
    gr[2] = [ (3, 1) ];
    gr[1].append(( 2, 5 ));
    gr[3] = [];

    #print(gr);
    # Source and destination
    s = 1; d = 3;

    # Dijkstra
    print(dijkstra(s, d, gr));

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the smallest
// product of edges
function dijkstra(s, d, gr)
{
    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Initialise the priority queue
    var pq = [];
    pq.push([1, s]);

    // Visited array
    var v = Array(gr.length).fill(0);

    // While the priority-queue
    // is not empty
    while (pq.length!=0) {

        // Current node
        var curr = pq[0][1];

        // Current product of distance
        var dist = pq[0][0];

        // Popping the top-most element
        pq.shift();

        // If already visited continue
        if (v[curr])
            continue;

        // Marking the node as visited
        v[curr] = 1;

        // If it is a destination node
        if (curr == d)
            return dist;

        // Traversing the current node
        for (var it of gr[curr])
            pq.push([dist * it[1], it[0] ]);
        pq.sort();
    }

    // If no path exists
    return -1;
}

// Driver code
var n = 3;

// Graph as adjacency matrix
var gr = Array.from(Array(n + 1), ()=> Array());

// Input edges
gr[1].push([3, 9]);
gr[2].push([3, 1]);
gr[1].push([2, 5]);

// Source and destination
var s = 1, d = 3;

// Dijkstra
document.write(dijkstra(s, d, gr));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
5
```

**时间复杂度:**O((E+V)logV)
T3】辅助空间 : O(V)。