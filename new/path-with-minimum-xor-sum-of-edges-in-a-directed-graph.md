# 有向图

中边的最小 XOR 总和的路径

> 原文： [https://www.geeksforgeeks.org/path-with-minimum-xor-sum-of-edges-in-a-directed-graph/](https://www.geeksforgeeks.org/path-with-minimum-xor-sum-of-edges-in-a-directed-graph/)

给定一个有`N`个节点和`E`边的有向图，一个源`S`和一个目标`D`节点。 任务是找到从`S`到`D`具有最小边沿 XOR 之和的路径。 如果没有从`S`到`D`的路径，则打印`-1`。

**示例**：

> **输入**：N = 3，E = 3，边线= {{{{1，2}，5}，{{1，3}，9}，{{2，3}，1}}， S = 1，D = 3
> **输出**：4
> 边权重的最小 XOR 的路径为 1- > 2- > 3
> ，XOR 和为 如 5 ^ 1 = 4。
> 
> **输入**：N = 3，E = 3，边线= {{{{3，2}，5}，{{3，3}，9}，{{3，3}，1}}， S = 1，D = 3
> **输出**：-1

**方法**：这个想法是使用 [Dijkstra 的最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)并稍有变化。 下面是解决问题的分步方法：

*   **基本情况**：如果源节点等于目的地，则返回`0`。

*   使用源节点及其权重为`0`和访问的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)初始化[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。

*   当优先级队列不为空时：

    1.  从优先级队列中弹出最上面的元素。 我们称其为当前节点。

    2.  在被访问数组的帮助下检查当前节点是否已被访问，如果是，则继续。

    3.  如果当前节点是目标节点，则返回当前节点与源节点的 XOR 总和距离。

    4.  迭代与当前节点相邻的所有节点，并推入优先级队列，并将它们的距离作为 XOR 与当前距离和边权重之和。

*   否则，没有从源到目标的路径。 因此，返回-1

下面是上述方法的实现：

## C++

```cpp

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

## Python

```py

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

**Output:**

```
4

```

***时间复杂度**：O（（E + V）logV）*

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。