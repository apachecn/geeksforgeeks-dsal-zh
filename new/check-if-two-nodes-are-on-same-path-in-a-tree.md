# 检查树中两个节点是否在同一路径上

> 原文： [https://www.geeksforgeeks.org/check-if-two-nodes-are-on-same-path-in-a-tree/](https://www.geeksforgeeks.org/check-if-two-nodes-are-on-same-path-in-a-tree/)

给定一棵树（不一定是二叉树）和许多查询，以便每个查询都将树的两个节点作为参数。 对于每个查询对，查找两个节点是否在从根到底部的同一路径上。

例如，考虑下面的树，如果给定的查询是（1、5），（1、6）和（2、6），则答案分别应为 true，true 和 false。

![Check if two nodes are on same path in a tree](img/ca517b7d3ca64bafc40f46b794f4e05f.png)

请注意，1 和 5 位于同一根到叶路径上，而 1 和 6 不在同一根到叶路径上。

显然，深度优先搜索技术将用于解决上述问题，主要问题是如何快速响应多个查询。 在这里，我们的图是一棵树，可以有任何数量的子代。 现在，如果从根节点开始，树中的 DFS 以深度搜索的方式进行，即假设根有三个孩子，而那些孩子只有一个孩子，那么如果 DFS 启动，则它首先访问根节点的第一个孩子，然后将 深入到该节点的子节点。 带有小树的情况可以显示如下：

访问节点的顺序为– 1 2 5 3 6 4 7。
因此，稍后再访问其他子节点，直到成功成功访问一个子节点为止。 为简化起见，如果我们假设手中有一只手表，那么我们将以 DFS 方式从根部开始行走。

Intime –首次访问该节点
Outtime-如果稍后再访问该节点，但是没有未访问的子节点，我们将其称为 Outtime，

*注意：它的子树中的任何节点将始终具有其子节点（或子节点的子节点）intime <，因为它总是在子节点之前（由于 DFS）首先被访问，并且在所有子节点中都将超时> 它的子树，因为在注意超时之前，它会等待所有子项都标记为已访问。*

对于任意两个节点 u，v，如果它们位于同一路径中，

```
Intime[v] < Intime[u] and Outtime[v] > Outtime[u]
                 OR
Intime[u] < Intime[v] and Outtime[u ]> Outtime[v]

```

*   如果给定的一对节点遵循两个条件中的任何一个，则它们在叶路径的同一根上。
*   否则不在同一路径上（如果两个节点在不同的路径上，则意味着彼此之间的子树中没有一个）。

**伪代码**

我们使用全局变量时间，该时间将随着节点开始时的 dfs 而增加，并在之后增加

```
DFS(v)
    increment timer
    Intime[v] = timer
    mark v as visited
    for all u that are children of v
              DFS(u)
    increment timer
    Outtime[v] = timer
end

```

时间复杂度–预处理为 O（n），每个查询为 O（1）。

**实现**：
下面是上述伪代码的实现。

## C ++

```

// C++ program to check if given pairs lie on same 
// path or not. 
#include<bits/stdc++.h> 
using namespace std; 
const int MAX = 100001; 

// To keep track of visited vertices in DFS 
bool visit[MAX] = {0}; 

// To store start and end time of all vertices 
// during DFS. 
int intime[MAX]; 
int outtime[MAX]; 

// initially timer is zero 
int timer = 0; 

// Does DFS of given graph and fills arrays 
// intime[] and outtime[]. These arrays are used 
// to answer given queries. 
void dfs(vector<int> graph[], int v) 
{ 
    visit[v] = true; 

    // Increment the timer as you enter 
    // the recursion for v 
    ++timer; 

    // Upgrade the in time for the vertex 
    intime[v] = timer; 

    vector<int>::iterator it = graph[v].begin(); 
    while (it != graph[v].end()) 
    { 
        if (visit[*it]==false) 
            dfs(graph, *it); 
        it++; 
    } 

    // increment the timer as you exit the 
    // recursion for v 
    ++timer; 

    // upgrade the outtime for that node 
    outtime[v] = timer; 
} 

// Returns true if 'u' and 'v' lie on same root to leaf path 
// else false. 
bool query(int u, int v) 
{ 
    return ( (intime[u]<intime[v] && outtime[u]>outtime[v]) || 
             (intime[v]<intime[u] && outtime[v]>outtime[u]) ); 
} 

// Driver code 
int main() 
{ 
    // Let us create above shown tree 
    int n = 9; // total number of nodes 
    vector<int> graph[n+1]; 
    graph[1].push_back(2); 
    graph[1].push_back(3); 
    graph[3].push_back(6); 
    graph[2].push_back(4); 
    graph[2].push_back(5); 
    graph[5].push_back(7); 
    graph[5].push_back(8); 
    graph[5].push_back(9); 

    // Start dfs (here root node is 1) 
    dfs(graph, 1); 

    // below are calls for few pairs of nodes 
    query(1, 5)? cout << "Yes\n" : cout << "No\n"; 
    query(2, 9)? cout << "Yes\n" : cout << "No\n"; 
    query(2, 6)? cout << "Yes\n" : cout << "No\n"; 

    return 0; 
} 

```

## 爪哇

```

// Java program to check if given  
// pairs lie on same path or not. 
import java.util.*; 

class GFG{ 

static int MAX = 100001; 

// To keep track of visited vertices in DFS 
static boolean []visit = new boolean[MAX]; 

// To store start and end time of all vertices 
// during DFS. 
static int []intime = new int[MAX]; 
static int []outtime = new int[MAX]; 

// Initially timer is zero 
static int timer = 0; 

// Does DFS of given graph and fills arrays 
// intime[] and outtime[]. These arrays are used 
// to answer given queries. 
static void dfs(Vector<Integer> graph[], int v) 
{ 
    visit[v] = true; 

    // Increment the timer as you enter 
    // the recursion for v 
    ++timer; 

    // Upgrade the in time for the vertex 
    intime[v] = timer; 

    for(int it : graph[v]) 
    { 
        if (visit[it] == false) 
            dfs(graph, it); 

        it++; 
    } 

    // Increment the timer as you exit the 
    // recursion for v 
    ++timer; 

    // Upgrade the outtime for that node 
    outtime[v] = timer; 
} 

// Returns true if 'u' and 'v' lie on  
// same root to leaf path else false. 
static boolean query(int u, int v) 
{ 
    return ((intime[u] < intime[v] &&  
            outtime[u] > outtime[v]) || 
            (intime[v] < intime[u] &&  
            outtime[v] > outtime[u])); 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // Let us create above shown tree 
    int n = 9; // total number of nodes 

    @SuppressWarnings("unchecked") 
    Vector<Integer> []graph = new Vector[n + 1]; 
    for(int i = 0; i < graph.length; i++) 
        graph[i] = new Vector<Integer>(); 

    graph[1].add(2); 
    graph[1].add(3); 
    graph[3].add(6); 
    graph[2].add(4); 
    graph[2].add(5); 
    graph[5].add(7); 
    graph[5].add(8); 
    graph[5].add(9); 

    // Start dfs (here root node is 1) 
    dfs(graph, 1); 

    // Below are calls for few pairs of nodes 
    if (query(1, 5)) 
        System.out.print("Yes\n" ); 
    else
        System.out.print("No\n"); 

    if (query(2, 9)) 
        System.out.print("Yes\n"); 
    else
        System.out.print("No\n"); 

    if (query(2, 6)) 
        System.out.print("Yes\n" ); 
    else
        System.out.print("No\n"); 
} 
} 

// This code is contributed by Princi Singh

```

## Python3

```

# Python3 program to check if given  
# pairs lie on same path or not. 

# Does DFS of given graph and fills  
# arrays intime[] and outtime[].  
# These arrays are used to answer  
# given queries.  
def dfs(graph, v): 
    global intime, outtime, visit, MAX, timer 
    visit[v] = True

    # Increment the timer as you enter  
    # the recursion for v  
    timer += 1

    # Upgrade the in time for the vertex  
    intime[v] = timer  
    it = 0
    while it < len(graph[v]): 
        if (visit[graph[v][it]] == False):  
            dfs(graph, graph[v][it])  
        it += 1

    # increment the timer as you  
    # exit the recursion for v  
    timer += 1

    # upgrade the outtime for that node  
    outtime[v] = timer 

# Returns true if 'u' and 'v' lie on  
# same root to leaf path else false.  
def query(u, v): 
    global intime, outtime, visit, MAX, timer 
    return ((intime[u] < intime[v] and 
             outtime[u] > outtime[v]) or 
            (intime[v] < intime[u] and 
             outtime[v] > outtime[u]) ) 

# Driver code  
MAX = 100001

# To keep track of visited vertices in DFS  
visit = [0] * MAX

# To store start and end time of  
# all vertices during DFS.  
intime = [0] * MAX
outtime = [0] * MAX

# initially timer is zero  
timer = 0

# Let us create above shown tree  
n = 9 # total number of nodes  
graph = [[] for i in range(n+1)] 
graph[1].append(2)  
graph[1].append(3)  
graph[3].append(6)  
graph[2].append(4)  
graph[2].append(5)  
graph[5].append(7)  
graph[5].append(8)  
graph[5].append(9)  

# Start dfs (here root node is 1)  
dfs(graph, 1)  

# below are calls for few pairs of nodes  
print("Yes") if query(1, 5) else print("No") 
print("Yes") if query(2, 9) else print("No") 
print("Yes") if query(2, 6) else print("No") 

# This code is contributed by PranchalK 

```

## C＃

```

// C# program to check if given  
// pairs lie on same path or not. 
using System; 
using System.Collections.Generic; 
class GFG{ 

static int MAX = 100001; 

// To keep track of visited  
// vertices in DFS 
static bool []visit =  
       new bool[MAX]; 

// To store start and end  
// time of all vertices  
// during DFS. 
static int []intime =  
       new int[MAX]; 
static int []outtime =  
       new int[MAX]; 

// Initially timer is zero 
static int timer = 0; 

// Does DFS of given graph  
// and fills arrays intime[]  
// and outtime[]. These arrays  
// are used to answer given queries. 
static void dfs(List<int> []graph,  
                int v) 
{ 
  visit[v] = true; 

  // Increment the timer as  
  // you enter the recursion  
  // for v 
  ++timer; 

  // Upgrade the in time  
  // for the vertex 
  intime[v] = timer; 

  foreach(int it in graph[v]) 
  { 
    if (visit[it] == false) 
      dfs(graph, it); 
  } 

  // Increment the timer as  
  // you exit the recursion for v 
  ++timer; 

  // Upgrade the outtime for  
  // that node 
  outtime[v] = timer; 
} 

// Returns true if 'u' and  
// 'v' lie on same root to  
// leaf path else false. 
static bool query(int u,  
                  int v) 
{ 
  return ((intime[u] < intime[v] &&  
           outtime[u] > outtime[v]) || 
          (intime[v] < intime[u] &&  
           outtime[v] > outtime[u])); 
} 

// Driver code 
public static void Main(String[] args) 
{     
  // Let us create above shown tree 
  // total number of nodes 
  int n = 9;  

  List<int> []graph = 
       new List<int>[n + 1]; 

  for(int i = 0;  
          i < graph.Length; i++) 
    graph[i] = new List<int>(); 

  graph[1].Add(2); 
  graph[1].Add(3); 
  graph[3].Add(6); 
  graph[2].Add(4); 
  graph[2].Add(5); 
  graph[5].Add(7); 
  graph[5].Add(8); 
  graph[5].Add(9); 

  // Start dfs (here root  
  // node is 1) 
  dfs(graph, 1); 

  // Below are calls for few  
  // pairs of nodes 
  if (query(1, 5)) 
    Console.Write("Yes\n" ); 
  else
    Console.Write("No\n"); 

  if (query(2, 9)) 
    Console.Write("Yes\n"); 
  else
    Console.Write("No\n"); 

  if (query(2, 6)) 
    Console.Write("Yes\n" ); 
  else
    Console.Write("No\n"); 
} 
} 

// This code is contributed by Amit Katiyar

```

**输出**：

```
Yes
Yes
No

```

**插图**：
从下面的图中了解更多，我们可以举一些例子。 上面修改的 DFS 算法将导致树的顶点在此处标记为以下时间和超时。 现在我们将考虑所有情况。

![Check if two nodes are on same path in a tree1](img/afc556932679d430eed7a9320729d155.png)

情况 1：节点 2 和 4：节点 2 的 intime 小于节点 4，但是由于 4 在其子树中，因此它的退出时间将比 4 大。 因此，条件是有效的，并且两者都在同一条路径上。
情况 2：节点 7 和 6：节点 7 的有效时间少于节点 6，但是由于两个节点都不在彼此的子树中，因此它们的退出时间不符合要求的条件。

本文由 **Saurabh Joshi 提供。** 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以撰写文章，并将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

