# 从给定的依赖项中找到任务的顺序

> 原文： [https://www.geeksforgeeks.org/find-the-ordering-of-tasks-from-given-dependencies/](https://www.geeksforgeeks.org/find-the-ordering-of-tasks-from-given-dependencies/)

您必须选择总共 n 个任务，标记为 0 到 n-1。 有些任务可能具有先决条件任务，例如选择任务 0，您必须首先完成任务 1，将其表示为一对：[0，1]

给定任务总数和先决条件对列表，请返回您应选择的任务顺序以完成所有任务。

可能有多个正确的订单，您只需要返回其中之一即可。 如果不可能完成所有任务，则返回一个空数组。

例子：

> 输入：2，[[[1，0]]
> 输出：[0，1]
> 说明：共有 2 个任务可供选择。 要选择任务 1，您应该已经完成​​任务 0。因此正确的任务顺序是[0，1]。
> 
> 输入：4，[[1，0]，[2，0]，[3，1]，[3，2]]
> 输出：[0，1，2，3]或[0，2，1 ，3]
> 说明：共有 4 个任务可供选择。 要选择任务 3，您应该同时完成任务 1 和 2。应该在完成任务 0 之后选择任务 1 和 2。因此，正确的任务顺序是[0，1，2，3]。 另一个正确的顺序是[0，2，1，3]。

**询问**：Google，Twitter，亚马逊和更多公司。

**解决方案**：我们可以将此问题视为一个图形问题（与[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)相关）。 所有任务都是图的节点，如果任务 u 是任务 v 的先决条件，我们将添加从节点 u 到节点 v 的有向边。现在，此问题等效于找到节点/任务的拓扑顺序（使用拓扑排序） ）在先决条件表示的图中。 如果图中有一个循环，则不可能完成所有任务（因为在这种情况下，没有任何任务的拓扑顺序）。 BFS 和 DFS 均可用于[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)来解决它。

由于 pair 对实现图算法不方便，因此我们首先将其转换为图。 如果任务 u 是任务 v 的先决条件，我们将添加从节点 u 到节点 v 的有向边。

**使用 BFS 的拓扑排序**

在这里，我们使用 [Kahn 的算法对拓扑进行排序](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)。 BFS 使用每个节点的度数。 我们将首先尝试查找度数为 0 的节点。 如果我们不这样做，则图中必须有一个循环，并且返回 false。 否则，我们找到了一个。 我们将其度数设置为-1，以防止再次访问它，并将其所有邻居的度数减少 1。此过程将重复 n（节点数）次。

```

// CPP program to find order to process tasks 
// so that all tasks can be finished. This program 
// mainly uses Kahn's algorithm. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns adjacency list representation of graph from 
// given set of pairs. 
vector<unordered_set<int> > make_graph(int numTasks, 
             vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph(numTasks); 
    for (auto pre : prerequisites) 
        graph[pre.second].insert(pre.first); 
    return graph; 
} 

// Computes in-degree of every vertex 
vector<int> compute_indegree(vector<unordered_set<int> >& graph) 
{ 
    vector<int> degrees(graph.size(), 0); 
    for (auto neighbors : graph) 
        for (int neigh : neighbors) 
            degrees[neigh]++; 
    return degrees; 
} 

// main function for topological sorting 
vector<int> findOrder(int numTasks, 
        vector<pair<int, int> >& prerequisites) 
{ 
    // Create an adjacency list 
    vector<unordered_set<int> > graph = 
            make_graph(numTasks, prerequisites); 

    // Find vertices of zero degree 
    vector<int> degrees = compute_indegree(graph); 
    queue<int> zeros; 
    for (int i = 0; i < numTasks; i++) 
        if (!degrees[i]) 
            zeros.push(i); 

    // Find vertices in topological order 
    // starting with vertices of 0 degree 
    // and reducing degrees of adjacent. 
    vector<int> toposort; 
    for (int i = 0; i < numTasks; i++) { 
        if (zeros.empty()) 
            return {}; 
        int zero = zeros.front(); 
        zeros.pop(); 
        toposort.push_back(zero); 
        for (int neigh : graph[zero]) { 
            if (!--degrees[neigh]) 
                zeros.push(neigh); 
        } 
    } 
    return toposort; 
} 

// Driver code 
int main() 
{ 
    int numTasks = 4; 
    vector<pair<int, int> > prerequisites; 

    // for prerequisites: [[1, 0], [2, 1], [3, 2]] 

    prerequisites.push_back(make_pair(1, 0)); 
    prerequisites.push_back(make_pair(2, 1)); 
    prerequisites.push_back(make_pair(3, 2)); 
    vector<int> v = findOrder(numTasks, prerequisites); 

    for (int i = 0; i < v.size(); i++) { 
        cout << v[i] << " "; 
    } 

    return 0; 
} 

```

**Output:**

```
0 1 2 3

```

**使用 DFS 进行拓扑排序**：

在此实现中，我们使用[基于 DFS 的算法进行拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。

```

// CPP program to find Topological sorting using 
// DFS 
#include <bits/stdc++.h> 
using namespace std; 

// Returns adjacency list representation of graph from 
// given set of pairs. 
vector<unordered_set<int> > make_graph(int numTasks, 
             vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph(numTasks); 
    for (auto pre : prerequisites) 
        graph[pre.second].insert(pre.first); 
    return graph; 
} 

// Does DFS and adds nodes to Topological Sort 
bool dfs(vector<unordered_set<int> >& graph, int node,  
           vector<bool>& onpath, vector<bool>& visited,  
                                vector<int>& toposort) 
{ 
    if (visited[node]) 
        return false; 
    onpath[node] = visited[node] = true; 
    for (int neigh : graph[node]) 
        if (onpath[neigh] || dfs(graph, neigh, onpath, visited, toposort)) 
            return true; 
    toposort.push_back(node); 
    return onpath[node] = false; 
} 

// Returns an order of tasks so that all tasks can be 
// finished. 
vector<int> findOrder(int numTasks, vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph = make_graph(numTasks, prerequisites); 
    vector<int> toposort; 
    vector<bool> onpath(numTasks, false), visited(numTasks, false); 
    for (int i = 0; i < numTasks; i++) 
        if (!visited[i] && dfs(graph, i, onpath, visited, toposort)) 
            return {}; 
    reverse(toposort.begin(), toposort.end()); 
    return toposort; 
} 

int main() 
{ 
    int numTasks = 4; 
    vector<pair<int, int> > prerequisites; 

    // for prerequisites: [[1, 0], [2, 1], [3, 2]] 
    prerequisites.push_back(make_pair(1, 0)); 
    prerequisites.push_back(make_pair(2, 1)); 
    prerequisites.push_back(make_pair(3, 2)); 
    vector<int> v = findOrder(numTasks, prerequisites); 

    for (int i = 0; i < v.size(); i++) { 
        cout << v[i] << " "; 
    } 

    return 0; 
} 

```

**Output:**

```
0 1 2 3

```

**参考**：https://leetcode.com/problems/course-schedule-ii/



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。