# 从给定的依赖关系中找到任务的顺序

> 原文:[https://www . geeksforgeeks . org/从给定的依赖项中找到任务的顺序/](https://www.geeksforgeeks.org/find-the-ordering-of-tasks-from-given-dependencies/)

总共有 n 个任务你必须选择，标记从 0 到 n-1。有些任务可能有先决条件任务，例如要选择任务 0，您必须先完成任务 1，任务 1 表示为一对:[0，1]

给定任务总数和先决条件对列表，返回您应该选择完成所有任务的任务顺序。

可能有多个正确的订单，你只需要退回其中一个即可。如果不可能完成所有任务，返回一个空数组。

示例:

> 输入:2、[[1，0]]
> 输出:【0，1]
> 说明:一共有 2 个任务可以挑。若要选取任务 1，您应该已经完成任务 0。所以正确的任务顺序是[0，1]。
> 
> 输入:4、[[1，0]，[2，0]，[3，1]，[3，2]]
> 输出:[0，1，2，3]或[0，2，1，3]
> 说明:共 4 个任务可挑。要选择任务 3，您应该已经完成了任务 1 和任务 2。任务 1 和 2 都应该在您完成任务 0 后选取。所以一个正确的任务顺序是[0，1，2，3]。另一个正确的排序是[0，2，1，3]。

**问于:**谷歌、推特、亚马逊等众多公司。

**解法:**我们可以把这个问题看成一个图(与[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)有关)的问题。所有的任务都是图的节点，如果任务 u 是任务 v 的先决条件，我们将从节点 u 到节点 v 增加一条有向边，现在，这个问题等价于在先决条件表示的图中寻找节点/任务的拓扑排序(使用拓扑排序)。如果图中有一个循环，那么不可能完成所有的任务(因为在这种情况下没有任何任务的拓扑顺序)。BFS 和 DFS 都可用于[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)求解。

由于 pair 不便于图算法的实现，我们首先将其转换为图。如果任务 u 是任务 v 的先决条件，我们将从节点 u 到节点 v 添加一条有向边。

**使用 BFS**
进行拓扑排序这里我们使用[卡恩的算法进行拓扑排序](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)。BFS 使用每个节点的索引。我们将首先尝试找到一个索引为 0 的节点。如果我们做不到这一点，图表中一定有一个循环，我们返回 false。否则我们已经找到了。我们将它的索引设置为-1，以防止再次访问它，并将其所有邻居的索引减少 1。这个过程将重复 n 次(节点数)。

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

**使用 DFS 的拓扑排序:**
在这个实现中，我们使用[基于 DFS 的算法进行拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。

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

**参考:**https://leetcode.com/problems/course-schedule-ii/