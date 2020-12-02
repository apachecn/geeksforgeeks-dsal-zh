# 查找是否可以根据给定的依赖项完成所有任务

> 原文： [https://www.geeksforgeeks.org/find-whether-it-is-possible-to-finish-all-tasks-or-not-from-given-dependencies/](https://www.geeksforgeeks.org/find-whether-it-is-possible-to-finish-all-tasks-or-not-from-given-dependencies/)

您必须选择总共 n 个任务，标记为 0 到 n-1。 某些任务可能有先决条件，例如，要选择任务 0，您必须首先选择任务 1（表示为一对）：[0，1]

给定任务总数和先决条件对列表，您是否可以完成所有任务？

例子：

> 输入：2，[[[1，0]]
> 输出：true
> 说明：共有 2 个任务可供选择。 要选择任务 1，您应该已经完成​​任务 0。所以这是可能的。
> 
> 输入：2，[[1，0]，[0，1]]
> 输出：false
> 说明：共有 2 个任务可供选择。 要选择任务 1，您应该已经完成​​了任务 0，要选择任务 0，您还应该已经完成​​了任务 1，因此这是不可能的。
> 
> 输入：3，[[1、0]，[2、1]，[3、2]]
> 输出：true
> 说明：总共有 3 个任务可供选择。 要选择任务 1，您应该已经完成​​了任务 0，要选择任务 2，您应该已经完成​​了任务 1，而要选择任务 3，您应该已经完成​​了任务 2。所以这是可能的。

**询问**：Google，Twitter，亚马逊和更多公司。

**解决方案**：我们可以将此问题视为一个图形问题（与[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)相关）。 所有任务都是图的节点，如果任务 u 是任务 v 的先决条件，我们将添加从节点 u 到节点 v 的有向边。现在，此问题等效于检测先决条件表示的图中的循环。 如果图中有一个循环，则不可能完成所有任务（因为在这种情况下，没有任何任务的拓扑顺序）。 BFS 和 DFS 均可用于解决该问题。

由于 pair 对实现图算法不方便，因此我们首先将其转换为图。 如果任务 u 是任务 v 的先决条件，我们将添加从节点 u 到节点 v 的有向边。

先决条件：[有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)中的检测周期

**使用 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)** 对于 DFS，它将首先访问一个节点，然后访问该节点的一个邻居，然后访问该邻居的一个邻居……等等。 如果它遇到在当前 DFS 访问过程中访问过的节点，则将检测到一个周期，并且我们将返回 false。 否则，它将从另一个未访问的节点开始，并重复此过程，直到访问了所有节点。 请注意，您应该进行两条记录：一条记录​​所有访问的节点，另一条记录当前 DFS 访问中的访问的节点。

代码如下。 我们使用访问的向量来记录所有访问的节点，并使用另一个向量的 onpath 来记录当前 DFS 访问的访问的节点。 当前访问完成后，我们将起始节点的 onpath 值重置为 false。

```

// CPP program to check whether we can finish all 
// tasks or not from given dependencies. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns adjacency list representation from a list 
// of pairs. 
vector<unordered_set<int> > make_graph(int numTasks, 
            vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph(numTasks); 
    for (auto pre : prerequisites) 
        graph[pre.second].insert(pre.first); 
    return graph; 
} 

// A DFS based function to check if there is a cycle 
// in the directed graph. 
bool dfs_cycle(vector<unordered_set<int> >& graph, int node,  
               vector<bool>& onpath, vector<bool>& visited) 
{ 
    if (visited[node]) 
        return false; 
    onpath[node] = visited[node] = true; 
    for (int neigh : graph[node]) 
        if (onpath[neigh] || dfs_cycle(graph, neigh, onpath, visited)) 
            return true; 
    return onpath[node] = false; 
} 

// Main function to check whether possible to finish all tasks or not 
bool canFinish(int numTasks, vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph = make_graph(numTasks, prerequisites); 
    vector<bool> onpath(numTasks, false), visited(numTasks, false); 
    for (int i = 0; i < numTasks; i++) 
        if (!visited[i] && dfs_cycle(graph, i, onpath, visited)) 
            return false; 
    return true; 
} 

int main() 
{ 
    int numTasks = 4; 

    vector<pair<int, int> > prerequisites; 

    // for prerequisites: [[1, 0], [2, 1], [3, 2]] 

    prerequisites.push_back(make_pair(1, 0)); 
    prerequisites.push_back(make_pair(2, 1)); 
    prerequisites.push_back(make_pair(3, 2)); 
    if (canFinish(numTasks, prerequisites)) { 
        cout << "Possible to finish all tasks"; 
    } 
    else { 
        cout << "Impossible to finish all tasks"; 
    } 

    return 0; 
} 

```

**Output:**

```
Possible to finish all tasks

```

**使用 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)**
BFS 可使用拓扑排序的思想来解决它。 如果可以进行拓扑排序，则意味着没有周期，并且可以完成所有任务。

BFS 使用每个节点的度数。 我们将首先尝试查找度数为 0 的节点。 如果我们不这样做，则图中必须有一个循环，并且返回 false。 否则，我们找到了一个。 我们将其度数设置为-1，以防止再次访问它，并将其所有邻居的度数减少 1。此过程将重复 n（节点数）次。 如果没有返回 false，则返回 true。

```

// A BFS based solution to check if we can finish 
// all tasks or not. This solution is mainly based 
// on Kahn's algorithm. 
#include <bits/stdc++.h> 
using namespace std; 

// Returns adjacency list representation from a list 
// of pairs. 
vector<unordered_set<int> > make_graph(int numTasks,  
            vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph(numTasks); 
    for (auto pre : prerequisites) 
        graph[pre.second].insert(pre.first); 
    return graph; 
} 

// Finds in-degree of every vertex 
vector<int> compute_indegree(vector<unordered_set<int> >& graph) 
{ 
    vector<int> degrees(graph.size(), 0); 
    for (auto neighbors : graph) 
        for (int neigh : neighbors) 
            degrees[neigh]++; 
    return degrees; 
} 

// Main function to check whether possible to finish all tasks or not 
bool canFinish(int numTasks, vector<pair<int, int> >& prerequisites) 
{ 
    vector<unordered_set<int> > graph = make_graph(numTasks, prerequisites); 
    vector<int> degrees = compute_indegree(graph); 
    for (int i = 0; i < numTasks; i++) { 
        int j = 0; 
        for (; j < numTasks; j++) 
            if (!degrees[j]) 
                break; 
        if (j == numTasks) 
            return false; 
        degrees[j] = -1; 
        for (int neigh : graph[j]) 
            degrees[neigh]--; 
    } 
    return true; 
} 

int main() 
{ 
    int numTasks = 4; 
    vector<pair<int, int> > prerequisites; 
    prerequisites.push_back(make_pair(1, 0)); 
    prerequisites.push_back(make_pair(2, 1)); 
    prerequisites.push_back(make_pair(3, 2)); 
    if (canFinish(numTasks, prerequisites)) { 
        cout << "Possible to finish all tasks"; 
    } 
    else { 
        cout << "Impossible to finish all tasks"; 
    } 

    return 0; 
} 

```

**Output:**

```
Possible to finish all tasks

```

**参考**：
https://leetcode.com/problems/course-schedule/



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。