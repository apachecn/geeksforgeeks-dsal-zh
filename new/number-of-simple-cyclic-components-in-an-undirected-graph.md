# 无向图

中单周期分量的数量

> 原文： [https://www.geeksforgeeks.org/number-of-simple-cyclic-components-in-an-undirected-graph/](https://www.geeksforgeeks.org/number-of-simple-cyclic-components-in-an-undirected-graph/)

给定一个无向简单图形的“ n”个顶点和“ m”个边的集合（没有平行边，也没有自环），找到图中存在的单周期分量的数量。 单循环组件是 n 个节点的图形，其中包含通过组件的所有节点的单个循环。

**示例**：

```
Let us consider the following graph with 15 vertices.

Input: V = 15, E = 14
       1 10  // edge 1
       1 5   // edge 2
       5 10  // edge 3
       2 9   // ..
       9 15  // ..
       2 15  // ..
       2 12  // ..
       12 15 // ..
       13 8  // ..
       6 14  // ..
       14 3  // ..
       3 7   // ..
       7 11  // edge 13
       11 6  // edge 14
Output :2
In the above-mentioned example, the two 
single-cyclic-components are composed of 
vertices (1, 10, 5) and (6, 11, 7, 3, 14) 
respectively.

```

现在我们可以轻松地看到一个单周期组件是一个连接的组件，其中每个顶点的度数均为 2。
因此，为了解决此问题，我们首先确定断开连接图的所有[连接的组件。 为此，我们使用深度优先搜索算法。 为了使 DFS 算法起作用，需要维护一个“找到的”数组，以记述递归函数 DFS 发现的所有顶点。 一旦发现了特定连接组件的所有元素（例如 vertices（9，2，15，12）形成了一个连接图组件），我们将检查该组件中的所有顶点的度数是否等于 2。 如果是，则增加计数器变量“ count”，该变量表示在给定图中找到的单循环组件的数量。 为了说明我们目前正在处理的组件，我们也可以使用向量数组“ curr_graph”。](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

## C++

```cpp

// CPP program to find single cycle components 
// in a graph. 
#include <bits/stdc++.h> 
using namespace std; 

const int N = 100000; 

// degree of all the vertices 
int degree[N]; 

// to keep track of all the vertices covered  
// till now 
bool found[N]; 

// all the vertices in a particular  
// connected component of the graph 
vector<int> curr_graph; 

// adjacency list 
vector<int> adj_list[N]; 

// depth-first traversal to identify all the 
// nodes in a particular connected graph  
// component 
void DFS(int v) 
{ 
    found[v] = true; 
    curr_graph.push_back(v); 
    for (int it : adj_list[v]) 
        if (!found[it]) 
            DFS(it); 
} 

// function to add an edge in the graph 
void addEdge(vector<int> adj_list[N], int src, 
             int dest) 
{ 
    // for index decrement both src and dest. 
    src--, dest--; 
    adj_list[src].push_back(dest); 
    adj_list[dest].push_back(src); 
    degree[src]++; 
    degree[dest]++; 
} 

int countSingleCycles(int n, int m) 
{ 
    // count of cycle graph components 
    int count = 0; 
    for (int i = 0; i < n; ++i) { 
        if (!found[i]) { 
            curr_graph.clear(); 
            DFS(i); 

            // traversing the nodes of the 
            // current graph component 
            int flag = 1; 
            for (int v : curr_graph) { 
                if (degree[v] == 2) 
                    continue; 
                else { 
                    flag = 0; 
                    break; 
                } 
            } 
            if (flag == 1) { 
                count++; 
            } 
        } 
    } 
    return(count); 
} 

int main() 
{ 
    // n->number of vertices 
    // m->number of edges 
    int n = 15, m = 14; 
    addEdge(adj_list, 1, 10); 
    addEdge(adj_list, 1, 5); 
    addEdge(adj_list, 5, 10); 
    addEdge(adj_list, 2, 9); 
    addEdge(adj_list, 9, 15); 
    addEdge(adj_list, 2, 15); 
    addEdge(adj_list, 2, 12); 
    addEdge(adj_list, 12, 15); 
    addEdge(adj_list, 13, 8); 
    addEdge(adj_list, 6, 14); 
    addEdge(adj_list, 14, 3); 
    addEdge(adj_list, 3, 7); 
    addEdge(adj_list, 7, 11); 
    addEdge(adj_list, 11, 6); 

    cout << countSingleCycles(n, m); 

    return 0; 
} 

```

## Java

```java

// Java program to find single cycle components  
// in a graph.  
import java.util.*; 

class GFG 
{ 

static int N = 100000;  

// degree of all the vertices  
static int degree[] = new int[N];  

// to keep track of all the vertices covered  
// till now  
static boolean found[] = new boolean[N];  

// all the vertices in a particular  
// connected component of the graph  
static Vector<Integer> curr_graph = new Vector<Integer>();  

// adjacency list  
static Vector<Vector<Integer>> adj_list = new Vector<Vector<Integer>>();  

// depth-first traversal to identify all the  
// nodes in a particular connected graph  
// component  
static void DFS(int v)  
{  
    found[v] = true;  
    curr_graph.add(v);  
    for (int it = 0 ;it < adj_list.get(v).size(); it++)  
        if (!found[adj_list.get(v).get(it)])  
            DFS(adj_list.get(v).get(it));  
}  

// function to add an edge in the graph  
static void addEdge( int src,int dest)  
{  
    // for index decrement both src and dest.  
    src--; dest--;  
    adj_list.get(src).add(dest);  
    adj_list.get(dest).add(src);  
    degree[src]++;  
    degree[dest]++;  
}  

static int countSingleCycles(int n, int m)  
{  
    // count of cycle graph components  
    int count = 0;  
    for (int i = 0; i < n; ++i)  
    {  

        if (!found[i]) 
        {  
            curr_graph.clear();  

            DFS(i);  

            // traversing the nodes of the  
            // current graph component  
            int flag = 1;  
            for (int v = 0 ; v < curr_graph.size(); v++)  
            {  
                if (degree[curr_graph.get(v)] == 2)  
                    continue;  
                else 
                {  
                    flag = 0;  
                    break;  
                }  
            }  
            if (flag == 1)  
            {  
                count++;  
            }  
        }  
    }  
    return(count);  
}  

// Driver code 
public static void main(String args[]) 
{  

    for(int i = 0; i < N + 1; i++) 
    adj_list.add(new Vector<Integer>()); 

    // n->number of vertices  
    // m->number of edges  
    int n = 15, m = 14;  
    addEdge( 1, 10);  
    addEdge( 1, 5);  
    addEdge( 5, 10);  
    addEdge( 2, 9);  
    addEdge( 9, 15);  
    addEdge( 2, 15);  
    addEdge( 2, 12);  
    addEdge( 12, 15);  
    addEdge( 13, 8);  
    addEdge( 6, 14);  
    addEdge( 14, 3);  
    addEdge( 3, 7);  
    addEdge( 7, 11);  
    addEdge( 11, 6);  

    System.out.println(countSingleCycles(n, m));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python

```py

# Python3 program to find single  
# cycle components in a graph.  
N = 100000

# degree of all the vertices  
degree = [0] * N  

# to keep track of all the  
# vertices covered till now  
found = [None] * N  

# All the vertices in a particular  
# connected component of the graph  
curr_graph = []  

# adjacency list  
adj_list = [[] for i in range(N)]  

# depth-first traversal to identify  
# all the nodes in a particular  
# connected graph component  
def DFS(v):  

    found[v] = True
    curr_graph.append(v) 

    for it in adj_list[v]:  
        if not found[it]:  
            DFS(it)  

# function to add an edge in the graph  
def addEdge(adj_list, src, dest):  

    # for index decrement both src and dest.  
    src, dest = src - 1, dest - 1
    adj_list[src].append(dest)  
    adj_list[dest].append(src)  
    degree[src] += 1
    degree[dest] += 1

def countSingleCycles(n, m):  

    # count of cycle graph components  
    count = 0
    for i in range(0, n):  
        if not found[i]:  
            curr_graph.clear()  
            DFS(i)  

            # traversing the nodes of the  
            # current graph component  
            flag = 1
            for v in curr_graph:  
                if degree[v] == 2:  
                    continue
                else:  
                    flag = 0
                    break

            if flag == 1:  
                count += 1

    return count  

# Driver Code 
if __name__ == "__main__": 

    # n->number of vertices  
    # m->number of edges  
    n, m = 15, 14
    addEdge(adj_list, 1, 10)  
    addEdge(adj_list, 1, 5)  
    addEdge(adj_list, 5, 10)  
    addEdge(adj_list, 2, 9)  
    addEdge(adj_list, 9, 15)  
    addEdge(adj_list, 2, 15)  
    addEdge(adj_list, 2, 12)  
    addEdge(adj_list, 12, 15)  
    addEdge(adj_list, 13, 8)  
    addEdge(adj_list, 6, 14)  
    addEdge(adj_list, 14, 3)  
    addEdge(adj_list, 3, 7)  
    addEdge(adj_list, 7, 11)  
    addEdge(adj_list, 11, 6)  

    print(countSingleCycles(n, m))  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# program to find single cycle components  
// in a graph.  
using System; 
using System.Collections.Generic; 

class GFG 
{ 
static int N = 100000;  

// degree of all the vertices  
static int []degree = new int[N];  

// to keep track of all the vertices covered  
// till now  
static bool []found = new bool[N];  

// all the vertices in a particular  
// connected component of the graph  
static List<int> curr_graph = new List<int>();  

// adjacency list  
static List<List<int>> adj_list = new List<List<int>>();  

// depth-first traversal to identify all the  
// nodes in a particular connected graph  
// component  
static void DFS(int v)  
{  
    found[v] = true;  
    curr_graph.Add(v);  
    for (int it = 0; it < adj_list[v].Count; it++)  
        if (!found[adj_list[v][it]])  
            DFS(adj_list[v][it]);  
}  

// function to add an edge in the graph  
static void addEdge(int src,int dest)  
{  
    // for index decrement both src and dest.  
    src--; dest--;  
    adj_list[src].Add(dest);  
    adj_list[dest].Add(src);  
    degree[src]++;  
    degree[dest]++;  
}  

static int countSingleCycles(int n, int m)  
{  
    // count of cycle graph components  
    int count = 0;  
    for (int i = 0; i < n; ++i)  
    {  
        if (!found[i]) 
        {  
            curr_graph.Clear();  

            DFS(i);  

            // traversing the nodes of the  
            // current graph component  
            int flag = 1;  
            for (int v = 0 ; v < curr_graph.Count; v++)  
            {  
                if (degree[curr_graph[v]] == 2)  
                    continue;  
                else
                {  
                    flag = 0;  
                    break;  
                }  
            }  
            if (flag == 1)  
            {  
                count++;  
            }  
        }  
    }  
    return(count);  
}  

// Driver code 
public static void Main(String []args) 
{  
    for(int i = 0; i < N + 1; i++) 
    adj_list.Add(new List<int>()); 

    // n->number of vertices  
    // m->number of edges  
    int n = 15, m = 14;  
    addEdge(1, 10);  
    addEdge(1, 5);  
    addEdge(5, 10);  
    addEdge(2, 9);  
    addEdge(9, 15);  
    addEdge(2, 15);  
    addEdge(2, 12);  
    addEdge(12, 15);  
    addEdge(13, 8);  
    addEdge(6, 14);  
    addEdge(14, 3);  
    addEdge(3, 7);  
    addEdge(7, 11);  
    addEdge(11, 6);  

    Console.WriteLine(countSingleCycles(n, m));  
} 
}  

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
2

```

因此，找到了循环图分量的总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。