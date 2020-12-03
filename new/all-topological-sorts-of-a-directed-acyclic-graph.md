# 有向无环图

的所有拓扑排序

> 原文： [https://www.geeksforgeeks.org/all-topological-sorts-of-a-directed-acyclic-graph/](https://www.geeksforgeeks.org/all-topological-sorts-of-a-directed-acyclic-graph/)

对`D`相连的**的拓扑排序**循环`G`raph（DAG）是顶点的线性排序，使得对于每个有向边 uv，顶点 u 都位于 v in 之前 订购。 如果图形不是 DAG，则无法对图形进行拓扑排序。

给定 DAG，打印图形的所有拓扑类型。

```
For example, consider the below graph.

 ![graph](img/7d0dd3600bc879e60d2864710a2aab68.png) 给定图的所有拓扑排序为：4 5 0 2 3 1 4 5 2 0 3 1 4 5 2 3 0 1 4 5 2 3 1 0 5 2 3 4 0 1 5 2  3 4 1 0 5 2 4 0 3 1 5 2 4 3 0 1 5 2 4 3 1 0 5 4 0 2 3 1 5 4 2 0 3 1 5 4 2 3 0 1 5 4 2 3 1 0
```

在有向无环图中，很多次我们可以得到彼此不相关的顶点，因此可以用多种方式对它们进行排序。 在许多情况下，这些各种拓扑排序很重要，例如，如果顶点之间也有一定的相对权重，这是为了最大程度地减少，那么我们需要注意相对顺序及其相对权重，这就需要检查 所有可能的拓扑顺序。

我们可以通过回溯来进行所有可能的排序，算法步骤如下：

1.  将所有顶点初始化为未访问。

2.  现在选择不可见的顶点，其度数为零，并将所有这些顶点的度数减少 1（对应于删除边），现在将该顶点添加为结果，并再次调用递归函数并回溯。

3.  从访问的功能重置值返回后，将求和结果和不度数枚举为其他可能性。

以下是上述步骤的实现。

## C++

```cpp

// C++ program to print all topological sorts of a graph 
#include <bits/stdc++.h> 
using namespace std; 

class Graph 
{ 
    int V;    // No. of vertices 

    // Pointer to an array containing adjacency list 
    list<int> *adj; 

    // Vector to store indegree of vertices 
    vector<int> indegree; 

    // A function used by alltopologicalSort 
    void alltopologicalSortUtil(vector<int>& res, 
                                bool visited[]); 

public: 
    Graph(int V);   // Constructor 

    // function to add an edge to graph 
    void addEdge(int v, int w); 

    // Prints all Topological Sorts 
    void alltopologicalSort(); 
}; 

//  Constructor of graph 
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 

    // Initialising all indegree with 0 
    for (int i = 0; i < V; i++) 
        indegree.push_back(0); 
} 

//  Utility function to add edge 
void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v's list. 

    // increasing inner degree of w by 1 
    indegree[w]++; 
} 

//  Main recursive function to print all possible 
//  topological sorts 
void Graph::alltopologicalSortUtil(vector<int>& res, 
                                   bool visited[]) 
{ 
    // To indicate whether all topological are found 
    // or not 
    bool flag = false;  

    for (int i = 0; i < V; i++) 
    { 
        //  If indegree is 0 and not yet visited then 
        //  only choose that vertex 
        if (indegree[i] == 0 && !visited[i]) 
        { 
            //  reducing indegree of adjacent vertices 
            list<int>:: iterator j; 
            for (j = adj[i].begin(); j != adj[i].end(); j++) 
                indegree[*j]--; 

            //  including in result 
            res.push_back(i); 
            visited[i] = true; 
            alltopologicalSortUtil(res, visited); 

            // resetting visited, res and indegree for 
            // backtracking 
            visited[i] = false; 
            res.erase(res.end() - 1); 
            for (j = adj[i].begin(); j != adj[i].end(); j++) 
                indegree[*j]++; 

            flag = true; 
        } 
    } 

    //  We reach here if all vertices are visited. 
    //  So we print the solution here 
    if (!flag) 
    { 
        for (int i = 0; i < res.size(); i++) 
            cout << res[i] << " "; 
        cout << endl; 
    } 
} 

//  The function does all Topological Sort. 
//  It uses recursive alltopologicalSortUtil() 
void Graph::alltopologicalSort() 
{ 
    // Mark all the vertices as not visited 
    bool *visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    vector<int> res; 
    alltopologicalSortUtil(res, visited); 
} 

// Driver program to test above functions 
int main() 
{ 
    // Create a graph given in the above diagram 
    Graph g(6); 
    g.addEdge(5, 2); 
    g.addEdge(5, 0); 
    g.addEdge(4, 0); 
    g.addEdge(4, 1); 
    g.addEdge(2, 3); 
    g.addEdge(3, 1); 

    cout << "All Topological sorts\n"; 

    g.alltopologicalSort(); 

    return 0; 
} 

```

## Java

```java

//Java program to print all topolgical sorts of a graph 
import java.util.*; 

class Graph { 
    int V; // No. of vertices 

    List<Integer> adjListArray[]; 

    public Graph(int V) { 

        this.V = V; 

        @SuppressWarnings("unchecked") 
        List<Integer> adjListArray[] = new LinkedList[V]; 

        this.adjListArray = adjListArray; 

        for (int i = 0; i < V; i++) { 
            adjListArray[i] = new LinkedList<>(); 
        } 
    } 
    // Utility function to add edge 
    public void addEdge(int src, int dest) { 

        this.adjListArray[src].add(dest); 

    } 

    // Main recursive function to print all possible 
    // topological sorts 
    private void allTopologicalSortsUtil(boolean[] visited,  
                        int[] indegree, ArrayList<Integer> stack) { 
        // To indicate whether all topological are found 
        // or not 
        boolean flag = false; 

        for (int i = 0; i < this.V; i++) { 
            // If indegree is 0 and not yet visited then 
            // only choose that vertex 
            if (!visited[i] && indegree[i] == 0) { 

                // including in result 
                visited[i] = true; 
                stack.add(i); 
                for (int adjacent : this.adjListArray[i]) { 
                    indegree[adjacent]--; 
                } 
                allTopologicalSortsUtil(visited, indegree, stack); 

                // resetting visited, res and indegree for 
                // backtracking 
                visited[i] = false; 
                stack.remove(stack.size() - 1); 
                for (int adjacent : this.adjListArray[i]) { 
                    indegree[adjacent]++; 
                } 

                flag = true; 
            } 
        } 
        // We reach here if all vertices are visited. 
        // So we print the solution here 
        if (!flag) { 
            stack.forEach(i -> System.out.print(i + " ")); 
            System.out.println(); 
        } 

    } 

    // The function does all Topological Sort. 
    // It uses recursive alltopologicalSortUtil() 
    public void allTopologicalSorts() { 
        // Mark all the vertices as not visited 
        boolean[] visited = new boolean[this.V]; 

        int[] indegree = new int[this.V]; 

        for (int i = 0; i < this.V; i++) { 

            for (int var : this.adjListArray[i]) { 
                indegree[var]++; 
            } 
        } 

        ArrayList<Integer> stack = new ArrayList<>(); 

        allTopologicalSortsUtil(visited, indegree, stack); 
    } 

    // Driver code 
    public static void main(String[] args) { 

        // Create a graph given in the above diagram 
        Graph graph = new Graph(6); 
        graph.addEdge(5, 2); 
        graph.addEdge(5, 0); 
        graph.addEdge(4, 0); 
        graph.addEdge(4, 1); 
        graph.addEdge(2, 3); 
        graph.addEdge(3, 1); 

        System.out.println("All Topological sorts"); 
        graph.allTopologicalSorts(); 
    } 
} 

```

输出：

```
All Topological sorts
4 5 0 2 3 1 
4 5 2 0 3 1 
4 5 2 3 0 1 
4 5 2 3 1 0 
5 2 3 4 0 1 
5 2 3 4 1 0 
5 2 4 0 3 1 
5 2 4 3 0 1 
5 2 4 3 1 0 
5 4 0 2 3 1 
5 4 2 0 3 1 
5 4 2 3 0 1 
5 4 2 3 1 0 

```

本文由 Utkarsh Trivedi 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

