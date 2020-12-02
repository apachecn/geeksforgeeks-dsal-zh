# 未加权图

中的多源最短路径

> 原文： [https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/)

假设有 n 个城镇通过 m 条双向道路连接。 其中有城镇，设有警察局。 我们想找出每个城镇到最近的警察局的距离。 如果城镇本身只有 1，则距离为 0。

例：

```
Input : 
Number of Vertices = 6
Number of Edges = 9
Towns with Police Station : 1, 5
Edges:
1 2
1 6
2 6
2 3
3 6
5 4
6 5
3 4
5 3

Output :
1 0
2 1
3 1
4 1
5 0
6 1

```

**天真的方法**：我们可以遍历顶点，并从每个顶点运行一个 BFS，以从该顶点找到最近的设有警察局的城镇。 这将需要 O（V.E）。

在每个顶点上使用 BFS 的幼稚方法实现：

```

// cpp program to demonstrate distance to 
// nearest source problem using BFS 
// from each vertex 
#include <bits/stdc++.h> 
using namespace std; 
#define N 100000 + 1 
#define inf 1000000 

// This array stores the distances of the  
// vertices from the nearest source 
int dist[N]; 

// a hash array where source[i] = 1 
// means vertex i is a source 
int source[N]; 

// The BFS Queue 
// The pairs are of the form (vertex, distance  
// from current source) 
deque<pair<int, int> > BFSQueue; 

// visited array for remembering visited vertices 
int visited[N]; 

// The BFS function 
void BFS(vector<int> graph[], int start) 
{ 
    // clearing the queue 
    while (!BFSQueue.empty()) 
        BFSQueue.pop_back(); 

    // push_back starting vertices 
    BFSQueue.push_back({ start, 0 }); 

    while (!BFSQueue.empty()) { 

        int s = BFSQueue.front().first; 
        int d = BFSQueue.front().second; 
        visited[s] = 1; 
        BFSQueue.pop_front(); 

        // stop at the first source we reach during BFS 
        if (source[s] == 1) { 
            dist[start] = d; 
            return; 
        } 

        // Pushing the adjacent unvisited vertices 
        // with distance from current source = this 
        // vertex's distance  + 1 
        for (int i = 0; i < graph[s].size(); i++) 
            if (visited[graph[s][i]] == 0) 
                BFSQueue.push_back({ graph[s][i], d + 1 }); 
    } 
} 

// This function calculates the distance of each  
// vertex from nearest source 
void nearestTown(vector<int> graph[], int n,  
                       int sources[], int S) 
{ 

    // reseting the source hash array 
    for (int i = 1; i <= n; i++) 
        source[i] = 0; 
    for (int i = 0; i <= S - 1; i++) 
        source[sources[i]] = 1; 

    // loop through all the vertices and run 
    // a BFS from each vertex to find the distance 
    // to nearest town from it 
    for (int i = 1; i <= n; i++) { 
        for (int i = 1; i <= n; i++) 
            visited[i] = 0; 
        BFS(graph, i); 
    } 

    // Printing the distances 
    for (int i = 1; i <= n; i++) 
        cout << i << " " << dist[i] << endl; 
} 

void addEdge(vector<int> graph[], int u, int v) 
{ 
    graph[u].push_back(v); 
    graph[v].push_back(u); 
} 

// Driver Code 
int main() 
{    // Number of vertices 
    int n = 6; 

    vector<int> graph[n + 1]; 

    // Edges 
    addEdge(graph, 1, 2); 
    addEdge(graph, 1, 6); 
    addEdge(graph, 2, 6); 
    addEdge(graph, 2, 3); 
    addEdge(graph, 3, 6); 
    addEdge(graph, 5, 4); 
    addEdge(graph, 6, 5); 
    addEdge(graph, 3, 4); 
    addEdge(graph, 5, 3); 

    // Sources 
    int sources[] = { 1, 5 }; 

    int S = sizeof(sources) / sizeof(sources[0]); 

    nearestTown(graph, n, sources, S); 

    return 0; 
} 

```

输出：

```
1 0
2 1
3 1
4 1
5 0
6 1

```

**时间复杂度**：*O（V.E）*

**有效方法**更好的方法是以修改的方式使用 [Djikstra 的算法](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)。 让我们将其中一个来源视为原始来源，将其他来源视为顶点，其原始路径的成本路径为 0。 因此，我们将所有源推入距离= 0 的 Djikstra 队列中，将其余顶点推入距离= infinity 的其余顶点。 现在，使用 Dijkstra 算法计算出的每个顶点到原始来源的最小距离实际上就是到最近来源的距离。
**说明**：C ++实现使用[对](https://www.geeksforgeeks.org/set-in-cpp-stl/)[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)对（到源的距离，顶点）的[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)集。 最初，该集合包含距离= 0 的源和距离= infinity 的所有其他顶点。
在每一步中，我们将到达距源（即，集合本身的第一个元素（距离为 0 的第一步中的源本身））与源的最小距离（d）的顶点。 我们遍历所有相邻顶点，如果任何顶点的距离为> d +1，我们将其在集合中的条目替换为新的距离。 然后我们从集合中删除当前顶点。 我们继续执行此操作，直到集合为空。
这样的想法是，到集合顶部的顶点的路径不能比当前路径短，因为其他任何路径都将是更长路径（> =它的长度）和非负数之和。 路径长度（除非我们考虑负边缘）。
由于所有源的距离都为 0，因此在开始时，相邻的非源顶点的距离将为 1。所有顶点的距离将为距其最近源的距离。

实施有效方法：

```

// cpp program to demonstrate 
// multi-source BFS 
#include <bits/stdc++.h> 
using namespace std; 
#define N 100000 + 1 
#define inf 1000000 

// This array stores the distances of the vertices 
// from the nearest source 
int dist[N]; 

// This Set contains the vertices not yet visited in 
// increasing order of distance from the nearest source 
// calculated till now 
set<pair<int, int> > Q; 

// Util function for Multi-Source BFS 
void multiSourceBFSUtil(vector<int> graph[], int s) 
{ 
    set<pair<int, int> >::iterator it; 
    int i; 
    for (i = 0; i < graph[s].size(); i++) { 
        int v = graph[s][i]; 
        if (dist[s] + 1 < dist[v]) { 

            // If a shorter path to a vertex is 
            // found than the currently stored  
            // distance replace it in the Q 
            it = Q.find({ dist[v], v }); 
            Q.erase(it); 
            dist[v] = dist[s] + 1; 
            Q.insert({ dist[v], v }); 
        } 
    } 

    // Stop when the Q is empty -> All 
    // vertices have been visited. And we only  
    // visit a vertex when we are sure that a  
    // shorter path to that vertex is not  
    // possible 
    if (Q.size() == 0) 
        return; 

    // Go to the first vertex in Q 
    // and remove it from the Q 
    it = Q.begin(); 
    int next = it->second; 
    Q.erase(it); 

    multiSourceBFSUtil(graph, next); 
} 

// This function calculates the distance of  
// each vertex from nearest source 
void multiSourceBFS(vector<int> graph[], int n,  
                          int sources[], int S) 
{ 
    // a hash array where source[i] = 1 
    // means vertex i is a source 
    int source[n + 1]; 

    for (int i = 1; i <= n; i++) 
        source[i] = 0; 
    for (int i = 0; i <= S - 1; i++) 
        source[sources[i]] = 1; 

    for (int i = 1; i <= n; i++) { 
        if (source[i]) { 
            dist[i] = 0; 
            Q.insert({ 0, i }); 
        } 
        else { 
            dist[i] = inf; 
            Q.insert({ inf, i }); 
        } 
    } 

    set<pair<int, int> >::iterator itr; 

    // Get the vertex with lowest distance, 
    itr = Q.begin(); 

    // currently one of the souces with distance = 0 
    int start = itr->second; 

    multiSourceBFSUtil(graph, start); 

    // Printing the distances 
    for (int i = 1; i <= n; i++) 
        cout << i << " " << dist[i] << endl; 
} 

void addEdge(vector<int> graph[], int u, int v) 
{ 
    graph[u].push_back(v); 
    graph[v].push_back(u); 
} 

// Driver Code 
int main() 
{ 
    // Number of vertices 
    int n = 6; 

    vector<int> graph[n + 1]; 

    // Edges 
    addEdge(graph, 1, 2); 
    addEdge(graph, 1, 6); 
    addEdge(graph, 2, 6); 
    addEdge(graph, 2, 3); 
    addEdge(graph, 3, 6); 
    addEdge(graph, 5, 4); 
    addEdge(graph, 6, 5); 
    addEdge(graph, 3, 4); 
    addEdge(graph, 5, 3); 

    // Sources 
    int sources[] = { 1, 5 }; 

    int S = sizeof(sources) / sizeof(sources[0]); 

    multiSourceBFS(graph, n, sources, S); 

    return 0; 
} 

```

输出：

```
1 0
2 1
3 1
4 1
5 0
6 1

```

**时间复杂度**： *O（E.logV）*

**更有效的方法**：一种更好的方法是使用多源 BFS，它是对 BFS 的修改。我们会将所有源顶点放在队列中，而不是将单个顶点放在标准队列中 BFS。这样，多源 BFS 将首先访问所有源顶点。 之后，它将访问与所有源顶点相距 1 的顶点，然后与所有源顶点相距 2 的顶点，依此类推。

下面是上述方法的实现：

```

// CPP program to demonstrate Multi-source BFS 
#include<bits/stdc++.h> 
using namespace std; 
#define N 1000000 

// This array stores the distances of the vertices  
// from the nearest source  
int dist[N]; 

//This boolean array is true if the current vertex  
// is visited otherwise it is false 
bool visited[N]; 

void addEdge(vector<int> graph[], int u, int v)  
{  
    //Function to add 2 edges in an undirected graph 
    graph[u].push_back(v);  
    graph[v].push_back(u);  
}  

// Multisource BFS Function 
void Multisource_BFS(vector<int> graph[],queue<int>q) 
{ 
    while(!q.empty()) 
    { 
        int k = q.front(); 
        q.pop(); 

        for(auto i:graph[k]) 
        { 
            if(!visited[i]) 
            { 

                // Pushing the adjacent unvisited vertices 
                // with distance from current source = this 
                // vertex's distance + 1 
                q.push(i); 
                dist[i] = dist[k] + 1;  
                visited[i] = true; 
            } 
        } 
    } 
} 

// This function calculates the distance of each  
// vertex from nearest source 
void nearestTown(vector<int> graph[],int n,int sources[],int s) 
{ 
    //Create a queue for BFS 
    queue<int> q; 

    //Mark all the source vertices as visited and enqueue it  
    for(int i = 0;i < s; i++) 
    { 
        q.push(sources[i]); 
        visited[sources[i]]=true; 
    } 

    Multisource_BFS(graph,q); 

    //Printing the distances 
    for(int i = 1; i <= n; i++) 
    { 
        cout<< i << " " << dist[i] << endl; 
    } 

} 

// Driver code 
int main() 
{      
    // Number of vertices  
    int n = 6;  

    vector<int> graph[n + 1];  

    // Edges  
    addEdge(graph, 1, 2);  
    addEdge(graph, 1, 6);  
    addEdge(graph, 2, 6);  
    addEdge(graph, 2, 3);  
    addEdge(graph, 3, 6);  
    addEdge(graph, 5, 4);  
    addEdge(graph, 6, 5);  
    addEdge(graph, 3, 4);  
    addEdge(graph, 5, 3);  

    // Sources  
    int sources[] = { 1, 5 };  

    int S = sizeof(sources) / sizeof(sources[0]);  

    nearestTown(graph, n, sources, S); 

    return 0; 
} 

```

输出：

```
1 0
2 1
3 1
4 1
5 0
6 1

```

**时间复杂度**： *O（V + E）*

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。