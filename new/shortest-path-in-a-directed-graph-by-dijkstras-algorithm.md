# Dijkstra 算法

在有向图中的最短路径

> 原文： [https://www.geeksforgeeks.org/shortest-path-in-a-directed-graph-by-dijkstras-algorithm/](https://www.geeksforgeeks.org/shortest-path-in-a-directed-graph-by-dijkstras-algorithm/)

给定图中的[有向图](https://www.geeksforgeeks.org/euler-circuit-directed-graph/)和**源顶点**，任务是在给定图中对边缘加权的非给定图中找到从源顶点到目标顶点的最短距离和路径。 否定），并从父顶点定向到源顶点。

**方法**：

*   将所有顶点标记为不可见。 创建一组所有未访问的顶点。
*   将零距离值分配给源顶点，将无限距离值分配给所有其他顶点。
*   将源顶点设置为当前顶点
*   对于当前顶点，请考虑其所有未访问的子代，并计算它们到当前的暂定距离。 （当前距离+相应边的权重）将新计算的距离与当前分配的值（对于某些顶点可以为无穷大）进行比较，并分配较小的一个。
*   在考虑了当前顶点的所有未访问子元素之后，将*当前*标记为已访问，并将其从未访问集合中移除。
*   同样，继续所有顶点，直到访问了所有节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the 
// shortest path in a directed 
// graph from source vertex to 
// the destination vertex 

#include <bits/stdc++.h> 
#define infi 1000000000 
using namespace std; 

// Class of the node 
class Node { 
public: 
    int vertexNumber; 

    // Adjacency list that shows the 
    // vertexNumber of child vertex 
    // and the weight of the edge 
    vector<pair<int, int> > children; 
    Node(int vertexNumber) 
    { 
        this->vertexNumber = vertexNumber; 
    } 

    // Function to add the child for 
    // the given node 
    void add_child(int vNumber, int length) 
    { 
        pair<int, int> p; 
        p.first = vNumber; 
        p.second = length; 
        children.push_back(p); 
    } 
}; 

// Function to find the distance of 
// the node from the given source 
// vertex to the destination vertex 
vector<int> dijkstraDist( 
    vector<Node*> g, 
    int s, vector<int>& path) 
{ 
    // Stores distance of each 
    // vertex from source vertex 
    vector<int> dist(g.size()); 

    // Boolean array that shows 
    // whether the vertex 'i' 
    // is visited or not 
    bool visited[g.size()]; 
    for (int i = 0; i < g.size(); i++) { 
        visited[i] = false; 
        path[i] = -1; 
        dist[i] = infi; 
    } 
    dist[s] = 0; 
    path[s] = -1; 
    int current = s; 

    // Set of vertices that has 
    // a parent (one or more) 
    // marked as visited 
    unordered_set<int> sett; 
    while (true) { 

        // Mark current as visited 
        visited[current] = true; 
        for (int i = 0; 
             i < g[current]->children.size(); 
             i++) { 
            int v = g[current]->children[i].first; 
            if (visited[v]) 
                continue; 

            // Inserting into the 
            // visited vertex 
            sett.insert(v); 
            int alt 
                = dist[current] 
                  + g[current]->children[i].second; 

            // Condition to check the distance 
            // is correct and update it 
            // if it is minimum from the previous 
            // computed distance 
            if (alt < dist[v]) { 
                dist[v] = alt; 
                path[v] = current; 
            } 
        } 
        sett.erase(current); 
        if (sett.empty()) 
            break; 

        // The new current 
        int minDist = infi; 
        int index = 0; 

        // Loop to update the distance 
        // of the vertices of the graph 
        for (int a: sett) { 
            if (dist[a] < minDist) { 
                minDist = dist[a]; 
                index = a; 
            } 
        } 
        current = index; 
    } 
    return dist; 
} 

// Function to print the path 
// from the source vertex to 
// the destination vertex 
void printPath(vector<int> path, 
               int i, int s) 
{ 
    if (i != s) { 

        // Condition to check if 
        // there is no path between 
        // the vertices 
        if (path[i] == -1) { 
            cout << "Path not found!!"; 
            return; 
        } 
        printPath(path, path[i], s); 
        cout << path[i] << " "; 
    } 
} 

// Driver Code 
int main() 
{ 
    vector<Node*> v; 
    int n = 4, s = 0, e = 5; 

    // Loop to create the nodes 
    for (int i = 0; i < n; i++) { 
        Node* a = new Node(i); 
        v.push_back(a); 
    } 

    // Creating directed 
    // weighted edges 
    v[0]->add_child(1, 1); 
    v[0]->add_child(2, 4); 
    v[1]->add_child(2, 2); 
    v[1]->add_child(3, 6); 
    v[2]->add_child(3, 3); 

    vector<int> path(v.size()); 
    vector<int> dist 
        = dijkstraDist(v, s, path); 

    // Loop to print the distance of 
    // every node from source vertex 
    for (int i = 0; i < dist.size(); i++) { 
        if (dist[i] == infi) { 
            cout << i << " and " << s 
                 << " are not connected"
                 << endl; 
            continue; 
        } 
        cout << "Distance of " << i 
             << "th vertex from source vertex "
             << s << " is: "
             << dist[i] << endl; 
    } 
    return 0; 
} 

```

**Output:**

> 第 0 个顶点到源顶点 0 的距离为：0
> 第 1 个顶点到源顶点 0 的距离为：1
> 第 2 个顶点到源顶点 0 的距离为：3
> 第 3 个顶点到源顶点 0 的距离 是：6

**时间复杂度**：![{\displaystyle \Theta ((|V|^{2})\log |V|)}](img/72fce0050b803ab4d702aea619568a1a.png "Rendered by QuickLaTeX.com")

**相关文章**：我们已经在本文中讨论了使用拓扑排序的有向图中的最短路径； [有向无环图](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)中的最短路径

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。