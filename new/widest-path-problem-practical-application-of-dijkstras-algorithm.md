# 最宽路径问题| Dijkstra 算法

的实际应用

> 原文： [https://www.geeksforgeeks.org/widest-path-problem-practical-application-of-dijkstras-algorithm/](https://www.geeksforgeeks.org/widest-path-problem-practical-application-of-dijkstras-algorithm/)

强烈建议先使用优先级队列阅读 [Dijkstra 的算法。](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)

最宽路径问题是在图**的两个顶点之间找到路径的问题，该路径最大化了路径**中最小权重边缘的权重。 请参见下图以了解问题所在：

![Graph](img/67bc793c40c778ab962b64e8a0200c3d.png)

**实际应用示例：**
这个问题是 Dijkstra 算法的著名变种。 在实际应用中，此问题可以看作是带有路由器的图形，因为其顶点和边表示两个顶点之间的带宽。 现在，如果我们要查找 Internet 连接中两个位置之间的最大带宽路径，则可以通过此算法解决此问题。

**如何解决这个问题？**
我们将通过使用 Dijkstra 算法的优先级队列（（| E | + | V |）log | V |）实现来解决此问题，并稍作更改。

我们只需用以下方法替换 Dijkstra 算法中的松弛条件即可解决此问题：

> max（min（widest_dist [u]，weight（u，v）），widest_dist [v]）

其中 u 是 v 的源顶点。v 是当前正在检查条件的顶点。

该算法针对有向图和无向图均运行。

请参阅以下图像系列，以获取有关问题和算法的想法：

边缘上的值表示有向边缘的权重。
![DAG](img/1bf09efb6453d84484bdb10d6322d013.png)

我们将从源顶点开始，然后遍历所有与其相连的顶点，并根据松弛条件添加优先级队列。
![](img/d2270bf13cce586b42df9154beec790c.png)

![](img/20c9cdb531fc9819f7d6090ce7bca6f6.png)

现在（2，1）将弹出，而 2 将是当前源顶点。

![](img/da518a500ed544c1c429c5c8bcc2a906.png)

现在（3，1）从队列中弹出。 但是由于 3 没有通过有向边连接的顶点，因此不会发生任何事情。 因此（4，2）接下来将弹出。

![](img/4adeddb9cead19a5da4efabfd717f9bc.png)

最后，算法停止，因为优先级队列中没有更多元素。
![](img/5cce6dd21367b9ee1e4d0e5c7856ae8b.png)

最大距离最远的路径是 1-4-3，最大瓶颈值是 2。因此，最终我们得到的最大距离是 2，到达目标顶点 3。

下面是上述方法的实现：

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print the required path 
void printpath(vector<int>& parent, int vertex, int target) 
{ 
    if (vertex == 0) { 
        return; 
    } 

    printpath(parent, parent[vertex], target); 

    cout << vertex << (vertex == target ? "\n" : "--"); 
} 

// Function to return the maximum weight 
// in the widest path of the given graph 
int widest_path_problem(vector<vector<pair<int, int> > >& Graph, 
                        int src, int target) 
{ 
    // To keep track of widest distance 
    vector<int> widest(Graph.size(), INT_MIN); 

    // To get the path at the end of the algorithm 
    vector<int> parent(Graph.size(), 0); 

    // Use of Minimum Priority Queue to keep track minimum 
    // widest distance vertex so far in the algorithm 
    priority_queue<pair<int, int>, vector<pair<int, int> >, 
                   greater<pair<int, int> > > 
        container; 

    container.push(make_pair(0, src)); 

    widest[src] = INT_MAX; 

    while (container.empty() == false) { 
        pair<int, int> temp = container.top(); 

        int current_src = temp.second; 

        container.pop(); 

        for (auto vertex : Graph[current_src]) { 

            // Finding the widest distance to the vertex 
            // using current_source vertex's widest distance 
            // and its widest distance so far 
            int distance = max(widest[vertex.second], 
                               min(widest[current_src], vertex.first)); 

            // Relaxation of edge and adding into Priority Queue 
            if (distance > widest[vertex.second]) { 

                // Updating bottle-neck distance 
                widest[vertex.second] = distance; 

                // To keep track of parent 
                parent[vertex.second] = current_src; 

                // Adding the relaxed edge in the prority queue 
                container.push(make_pair(distance, vertex.second)); 
            } 
        } 
    } 

    printpath(parent, target, target); 

    return widest[target]; 
} 

// Driver code 
int main() 
{ 

    // Graph representation 
    vector<vector<pair<int, int> > > graph; 

    int no_vertices = 4; 

    graph.assign(no_vertices + 1, vector<pair<int, int> >()); 

    // Adding edges to graph 

    // Resulting graph 
    // 1--2 
    // |  | 
    // 4--3 

    // Note that order in pair is (distance, vertex) 
    graph[1].push_back(make_pair(1, 2)); 
    graph[1].push_back(make_pair(2, 4)); 
    graph[2].push_back(make_pair(3, 3)); 
    graph[4].push_back(make_pair(5, 3)); 

    cout << widest_path_problem(graph, 1, 3); 

    return 0; 
} 

```

**Output:**

```
1--4--3
2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。