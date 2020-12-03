# 森林中树木的数量

> 原文： [https://www.geeksforgeeks.org/count-number-trees-forest/](https://www.geeksforgeeks.org/count-number-trees-forest/)

给定一个森林的 n 个节点（树木的集合），找到森林中的树木数量。

**示例**：

```
Input :  edges[] = {0, 1}, {0, 2}, {3, 4}
Output : 2
Explanation : There are 2 trees
                   0       3
                  / \       \
                 1   2       4

```

**方法**：

1.在每个节点上应用 DFS。

2.如果从一个源访问每个连接的节点，则递增 1。

3.如果某些节点尚未访问，请再次执行 DFS 遍历。

4.计数将给出森林中的树木数量。

## C++

```cpp

// CPP program to count number of trees in 
// a forest. 
#include<bits/stdc++.h> 
using namespace std; 

// A utility function to add an edge in an 
// undirected graph. 
void addEdge(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// A utility function to do DFS of graph 
// recursively from a given vertex u. 
void DFSUtil(int u, vector<int> adj[], 
                    vector<bool> &visited) 
{ 
    visited[u] = true; 
    for (int i=0; i<adj[u].size(); i++) 
        if (visited[adj[u][i]] == false) 
            DFSUtil(adj[u][i], adj, visited); 
} 

// Returns count of tree is the forest 
// given as adjacency list. 
int countTrees(vector<int> adj[], int V) 
{ 
    vector<bool> visited(V, false); 
    int res = 0; 
    for (int u=0; u<V; u++) 
    { 
        if (visited[u] == false) 
        { 
            DFSUtil(u, adj, visited); 
            res++; 
        } 
    } 
    return res; 
} 

// Driver code 
int main() 
{ 
    int V = 5; 
    vector<int> adj[V]; 
    addEdge(adj, 0, 1); 
    addEdge(adj, 0, 2); 
    addEdge(adj, 3, 4); 
    cout << countTrees(adj, V); 
    return 0; 
} 

```

## Java

```java

// Java program to count number of trees in a forest. 
import java.io.*;  
import java.util.*;  

// This class represents a directed graph using adjacency list  
// representation  
class Graph  
{  
    private int V; // No. of vertices  

    // Array of lists for Adjacency List Representation  
    private LinkedList<Integer> adj[];  

    // Constructor  
    Graph(int v)  
    {  
        V = v;  
        adj = new LinkedList[v];  
        for (int i = 0; i <  v; ++i)  
            adj[i] = new LinkedList();  
    }  

    //Function to add an edge into the graph  
    void addEdge(int v, int w)  
    {  
        adj[v].add(w); // Add w to v's list.  
    }  

    // A function used by DFS  
    void DFSUtil(int v,boolean visited[])  
    {  
        // Mark the current node as visited and print it  
        visited[v] = true;  

        // Recur for all the vertices adjacent to this vertex  
        Iterator<Integer> i = adj[v].listIterator();  
        while (i.hasNext())  
        {  
            int n = i.next();  
            if (!visited[n]) 
            { 
                DFSUtil(n,visited);  
            } 
        } 
    }  

    // The function to do DFS traversal. It uses recursive DFSUtil()  
    int countTrees() 
    {  
        // Mark all the vertices as not visited(set as  
        // false by default in java)  
        boolean visited[] = new boolean[V];  
        int res = 0; 

        // Call the recursive helper function to print DFS traversal  
        // starting from all vertices one by one  
        for (int i = 0; i < V; ++i)  
        { 
            if (visited[i] == false) 
            {  
                DFSUtil(i, visited);  
                res ++; 
            } 
        } 
        return res; 
    }  

    // Driver code 
    public static void main(String args[])  
    {  
        Graph g = new Graph(5);  

        g.addEdge(0, 1);  
        g.addEdge(0, 2);  
        g.addEdge(3, 4);  

        System.out.println(g.countTrees());  
    }  
}  

// This code is contributed by mayankbansal2 

```

## Python

```py

# Python3 program to count number   
# of trees in a forest. 

# A utility function to add an  
# edge in an undirected graph.  
def addEdge(adj, u, v): 
    adj[u].append(v)  
    adj[v].append(u) 

# A utility function to do DFS of graph  
# recursively from a given vertex u.  
def DFSUtil(u, adj, visited): 
    visited[u] = True
    for i in range(len(adj[u])): 
        if (visited[adj[u][i]] == False): 
            DFSUtil(adj[u][i], adj, visited) 

# Returns count of tree is the  
# forest given as adjacency list.  
def countTrees(adj, V): 
    visited = [False] * V  
    res = 0
    for u in range(V): 
        if (visited[u] == False): 
            DFSUtil(u, adj, visited)  
            res += 1
    return res 

# Driver code  
if __name__ == '__main__': 

    V = 5
    adj = [[] for i in range(V)]  
    addEdge(adj, 0, 1)  
    addEdge(adj, 0, 2)  
    addEdge(adj, 3, 4)  
    print(countTrees(adj, V)) 

# This code is contributed by PranchalK 

```

## C#

```cs

// C# program to count number of trees in a forest. 
using System; 
using System.Collections.Generic; 

// This class represents a directed graph  
// using adjacency list representation  
class Graph  
{  
    private int V; // No. of vertices  

    // Array of lists for  
    // Adjacency List Representation  
    private List<int> []adj;  

    // Constructor  
    Graph(int v)  
    {  
        V = v;  
        adj = new List<int>[v];  
        for (int i = 0; i < v; ++i)  
            adj[i] = new List<int>();  
    }  

    // Function to add an edge into the graph  
    void addEdge(int v, int w)  
    {  
        adj[v].Add(w); // Add w to v's list.  
    }  

    // A function used by DFS  
    void DFSUtil(int v, bool []visited)  
    {  
        // Mark the current node as  
        // visited and print it  
        visited[v] = true;  

        // Recur for all the vertices  
        // adjacent to this vertex  
        foreach(int i in adj[v])  
        {  
            int n = i;  
            if (!visited[n]) 
            { 
                DFSUtil(n, visited);  
            } 
        } 
    }  

    // The function to do DFS traversal. 
    // It uses recursive DFSUtil()  
    int countTrees() 
    {  
        // Mark all the vertices as not visited 
        // (set as false by default in java)  
        bool []visited = new bool[V];  
        int res = 0; 

        // Call the recursive helper function  
        // to print DFS traversal starting from  
        // all vertices one by one  
        for (int i = 0; i < V; ++i)  
        { 
            if (visited[i] == false) 
            {  
                DFSUtil(i, visited);  
                res ++; 
            } 
        } 
        return res; 
    }  

    // Driver code 
    public static void Main(String []args)  
    {  
        Graph g = new Graph(5);  

        g.addEdge(0, 1);  
        g.addEdge(0, 2);  
        g.addEdge(3, 4);  

        Console.WriteLine(g.countTrees());  
    }  
}  

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
2

```

**时间复杂度**：O（V + E）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。