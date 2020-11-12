# 检查给定的排列是否为图的有效 DFS

> 原文：[https://www.geeksforgeeks.org/check-given-permutation-valid-dfs-graph/](https://www.geeksforgeeks.org/check-given-permutation-valid-dfs-graph/)

给定一个图，该图具有从 1 到`N`的`N`个节点和`M`个边的数字，以及从 1 到`N`的数字数组。请检查是否有可能通过在给定图上应用 DFS（深度优先遍历）来获得数组的任何排列。

**先决条件**：[DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) | CPP 中的[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)

**示例**：

```
Input: N = 3, M = 2
        Edges are:
        1) 1-2
        2) 2-3
        P = {1, 2, 3}
Output: YES
Explanation: 
Since there are edges between 
1-2 and 2-3, therefore we can 
have DFS in the order 1-2-3

Input: N = 3, M = 2
        Edges are:
        1) 1-2
        2) 2-3
        P = {1, 3, 2}
Output: NO
Explanation: 
Since there is no edge between 1 and 3,
the DFS traversal is not possible 
in the order of given permutation.

```

**方法**：我们假设输入图表示为[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)。 想法是首先根据输入顺序对所有邻接表排序，然后从给定排列的第一个节点开始遍历给定图。 如果我们以相同顺序访问所有顶点，则给定的排列是有效的 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。

1.  将每个数字的索引存储在哈希映射中的给定排列中。

2.  由于需要维护顺序，因此根据排列索引对每个邻接表排序。

3.  使用源节点作为给定排列的第一个数字执行深度优先遍历搜索。

4.  保留一个计数器变量，并在每次递归调用时，检查计数器是否已达到节点数（即`N`），并将标志设置为 1。如果在完成 DFS 后标志为 0，则回答为`No`，否则为`Yes`。

**以下是上述方法的实现**：

```
ter_none
edit
play_arrow

brightness_4
// C++ program to check if given 
// permutation can be obtained 
// upon DFS traversal on given graph 
#include <bits/stdc++.h> 
using namespace std; 
  
// To track of DFS is valid or not. 
bool flag = false; 
  
// HashMap to store the indexes 
// of given permutation 
map<int, int> mp; 
  
// Comparator function for sort 
bool cmp(int a, int b) 
{ 
    // Sort according ascending 
    // order of indexes 
    return mp[a] < mp[b]; 
} 
  
// Graph class represents an undirected 
// using adjacency list representation 
class Graph { 
    int V; // No. of vertices 
    int counter; // Counter variable 
  
public: 
    // Pointer to an array containing 
    // adjacency lists 
    list<int>* adj; 
  
    Graph(int V); // Constructor 
  
    // function to add an edge to graph 
    void addEdge(int u, int v); 
  
    // DFS traversal of the vertices 
    // reachable from v 
    void DFS(int v, int Perm[]); 
}; 
  
Graph::Graph(int V) 
{ 
    this->V = V; 
    this->counter = 0; 
    adj = new list<int>[V + 1]; 
} 
  
void Graph::addEdge(int u, int v) 
{ 
  
    // Add v to u's list. 
    adj[u].push_back(v); 
  
    // Add u to v's list 
    adj[v].push_back(u); 
} 
  
// DFS traversal of the 
// vertices reachable from v. 
void Graph::DFS(int v, int Perm[]) 
{ 
    // Increment counter for 
    // every node being traversed 
    counter++; 
  
    // Check if counter has 
    // reached number of vertices 
    if (counter == V) { 
  
        // Set flag to 1 
        flag = 1; 
        return; 
    } 
  
    // Recur for all vertices adjacent 
    // to this vertices only if it 
    // lies in the given permutation 
    list<int>::iterator i; 
    for (i = adj[v].begin(); 
         i != adj[v].end(); i++) { 
  
        // if the current node equals to 
        // current element of permutation 
        if (*i == Perm[counter]) 
            DFS(*i, Perm); 
    } 
} 
  
// Returns true if P[] is a valid DFS of given 
// graph. In other words P[] can be obtained by 
// doing a DFS of the graph. 
bool checkPermutation( 
    int N, int M, 
    vector<pair<int, int> > V, 
    int P[]) 
{ 
  
    // Create the required graph with 
    // N vertices and M edges 
    Graph G(N); 
  
    // Add Edges to Graph G 
    for (int i = 0; i < M; i++) 
        G.addEdge(V[i].first, 
                  V[i].second); 
  
    for (int i = 0; i < N; i++) 
        mp[P[i]] = i; 
  
    // Sort every adjacency 
    // list according to HashMap 
    for (int i = 1; i <= N; i++) 
        G.adj[i].sort(cmp); 
  
    // Call DFS with source node as P[0] 
    G.DFS(P[0], P); 
  
    // If Flag has been set to 1, means 
    // given permutation is obtained 
    // by DFS on given graph 
    return flag; 
} 
  
// Driver code 
int main() 
{ 
    // Number of vertices 
    // and number of edges 
    int N = 3, M = 2; 
  
    // Vector of pair to store edges 
    vector<pair<int, int> > V; 
  
    V.push_back(make_pair(1, 2)); 
    V.push_back(make_pair(2, 3)); 
  
    int P[] = { 1, 2, 3 }; 
  
    // Return the answer 
    if (checkPermutation(N, M, V, P)) 
        cout << "YES" << endl; 
    else
        cout << "NO" << endl; 
  
    return 0; 
} 
```

**输出**：

```
YES

```



* * *

* * *



