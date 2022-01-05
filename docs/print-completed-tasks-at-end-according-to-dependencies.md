# 根据依赖关系

打印结束时完成的任务

> 原文:[https://www . geesforgeks . org/print-completed-tasks-in-end-根据依赖关系/](https://www.geeksforgeeks.org/print-completed-tasks-at-end-according-to-dependencies/)

给定表单的 **N** 依赖项 **X Y** ，其中 X & Y 代表两个不同的任务。依赖关系 X Y 表示形式的依赖关系 **Y - > X** ，即如果任务 Y 发生，那么任务 X 将发生，换句话说，任务 Y 必须首先完成才能启动任务 X。任务是按照**字典顺序**打印最后要完成的所有任务。**注意**任务只用大写英文字母表示。

> **输入:** dep[][] = {{A，B}，{C，B}，{D，A}，{D，C}，{B，E}}，tasks[] = {B，C}
> **输出:** A B C D
> 任务 A 发生在任务 B 之后，任务 D 只能发生在任务 A 或 C 完成后
> 
> 所以，需要的顺序是 A B C D
> 
> **输入:** dep[][] = {{Q，P}，{S，Q}，{Q，R}}，tasks[]= { R }
> T3】输出: Q R S

**进场:** [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 可以用来解决问题。形式 **X Y (Y - > X)** 的依赖关系可以表示为图中从节点 **Y** 到节点 **X** 的边。从每个 **M** 初始节点启动 DFS，并使用布尔数组将遇到的节点标记为已访问。最后，按照字典顺序打印使用 DFS 覆盖的节点/任务。该方法之所以有效，是因为 DFS 将以顺序方式覆盖从初始节点开始的所有节点。

考虑下面代表上面第一个例子的图表:
![](img/df8b873a593a2cf1e0f6c80f2e28ec2c.png)
该图表用
颜色将初始任务 B 和 C 的 DFS 期间覆盖的边显示为红色。这样访问的节点是 A、B、C 和 d

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <cstring>
#include <iostream>
#include <vector>
using namespace std;

// Graph class represents a directed graph
// using adjacency list representation
class Graph {

    // Number of vertices
    int V;

    // Pointer to an array containing
    // adjacency lists
    vector<int>* adj;

    // Boolean array to mark tasks as visited
    bool visited[26];

    // A recursive function used by DFS
    void DFSUtil(int v);

public:
    // Constructor
    Graph()
    {

        // There are only 26 English
        // upper case letters
        this->V = 26;
        adj = new vector<int>[26];
    }

    // Function to add an edge to the graph
    void addEdge(char v, char w);

    // DFS traversal of the vertices
    // reachable from v
    void DFS(char start[], int M);

    void printTasks();
};

// Function to add an edge to the graph
void Graph::addEdge(char v, char w)
{

    // Add w to v's list
    adj[v - 65].push_back(w - 65);
}

void Graph::DFSUtil(int v)
{

    // Mark the current node as visited and
    // print it
    visited[v] = true;

    // Recur for all the vertices adjacent
    // to this vertex
    vector<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFSUtil(*i);
}

// DFS traversal of the vertices reachable
// from start nodes
// It uses recursive DFSUtil()
void Graph::DFS(char start[], int M)
{
    // Mark all the vertices as not visited
    for (int i = 0; i < V; i++)
        visited[i] = false;

    // Call the recursive helper function
    // to print DFS traversal
    for (int i = 0; i < M; i++)
        DFSUtil(start[i] - 65);
}

// Helper function to print the tasks in
// lexicographical order that are completed
// at the end of the DFS
void Graph::printTasks()
{
    for (int i = 0; i < 26; i++) {
        if (visited[i])
            cout << char(i + 65) << " ";
    }
    cout << endl;
}

// Driver code
int main()
{
    // Create the graph
    Graph g;
    g.addEdge('B', 'A');
    g.addEdge('B', 'C');
    g.addEdge('A', 'D');
    g.addEdge('C', 'D');
    g.addEdge('E', 'B');

    // Initial tasks to be run
    char start[] = { 'B', 'C' };
    int n = sizeof(start) / sizeof(char);

    // Start the dfs
    g.DFS(start, n);

    // Print the tasks that will get finished
    g.printTasks();

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict 

# This class represents a directed graph 
# using adjacency list representation 
class Graph: 

    # Constructor 
    def __init__(self): 

        # Default dictionary to store the graph 
        self.graph = defaultdict(list) 
        self.visited = [False]*26

    # Function to add an edge to the graph 
    def addEdge(self, u, v): 
        self.graph[ord(u)-65].append(ord(v)-65) 

    # A function used by DFS 
    def DFSUtil(self, v): 

        # Mark the current node as visited 
        # and print it 
        self.visited[v]= True

        # Recur for all the vertices adjacent 
        # to this vertex 
        for i in self.graph[v]: 
            if self.visited[i] == False: 
                self.DFSUtil(i) 

    # Function to perform the DFS traversal 
    # It uses recursive DFSUtil() 
    def DFS(self, start, M): 

        # Total vertices 
        V = len(self.graph)

        # Call the recursive helper function 
        # to print the DFS traversal starting 
        # from all vertices one by one 
        for i in range(M):
            self.DFSUtil(ord(start[i])-65) 

    def printOrder(self):
        for i in range(26):
            if self.visited[i] == True:
                print(chr(i + 65), end =" ")
        print("\n")

# Driver code 
g = Graph() 
g.addEdge('B', 'A') 
g.addEdge('B', 'C') 
g.addEdge('A', 'D') 
g.addEdge('C', 'D') 
g.addEdge('E', 'B') 

g.DFS(['B', 'C'], 2) 
g.printOrder()
```

**Output:**

```
A B C D

```

**时间复杂度:** O(V + E)，其中 V 为图中节点数，E 为边数或依赖数。在这种情况下，由于 V 总是 26，所以时间复杂度是 O(26 + E)或者最坏情况下只是 **O(E)** 。
**空间复杂度:** O(V + E)