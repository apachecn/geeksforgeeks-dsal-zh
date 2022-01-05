# 从给定的依赖关系中找出是否有可能完成所有任务

> 原文:[https://www . geesforgeks . org/find-是否有可能从给定的依赖关系中完成所有任务/](https://www.geeksforgeeks.org/find-whether-it-is-possible-to-finish-all-tasks-or-not-from-given-dependencies/)

总共有 n 个任务你必须选择，标记从 0 到 n-1。有些任务可能有先决条件，比如要挑任务 0 就要先挑任务 1，表示成对:[0，1]
给定任务总数和先决条件对列表，你有可能完成所有任务吗？
示例:

> 输入:2，[[1，0]]
> 输出:真
> 说明:一共有 2 个任务要挑。若要选取任务 1，您应该已经完成任务 0。所以是有可能的。
> 输入:2，[[1，0]，[0，1]]
> 输出:假
> 说明:一共有 2 个任务要挑。若要选取任务 1，您应该已经完成任务 0，若要选取任务 0，您也应该已经完成任务 1。所以是不可能的。
> 输入:3、[[1，0]、[2，1]、[3，2]]
> 输出:真
> 说明:一共有 3 个任务要挑。要选择任务 1，您应该已经完成任务 0；要选择任务 2，您应该已经完成任务 1；要选择任务 3，您应该已经完成任务 2。所以是有可能的。

**问于:**谷歌、推特、亚马逊等众多公司。

**解法:**我们可以把这个问题看成一个图(与[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)有关)的问题。所有的任务都是图的节点，如果任务 u 是任务 v 的先决条件，我们将在节点 u 到节点 v 之间添加一条有向边，现在，这个问题相当于检测由先决条件表示的图中的一个循环。如果图中有一个循环，那么不可能完成所有的任务(因为在这种情况下没有任何任务的拓扑顺序)。BFS 和 DFS 都可以用来解决这个问题。
由于 pair 不便于图算法的实现，我们首先将其转化为图。如果任务 u 是任务 v 的先决条件，我们将从节点 u 到节点 v 添加一条有向边
先决条件:[检测有向图中的循环](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)
**使用** [**DFS**](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 对于 DFS，它将首先访问一个节点，然后访问它的一个邻居，然后访问这个邻居的一个邻居……以此类推。如果遇到当前 DFS 访问过程中被访问的节点，检测到一个周期，我们将返回 false。否则，它将从另一个未访问的节点开始，重复这个过程，直到所有节点都被访问。请注意，您应该做两个记录:一个是记录所有被访问的节点，另一个是记录当前 DFS 访问中被访问的节点。
代码如下。我们使用一个被访问的向量来记录所有被访问的节点，另一个路径上的向量来记录当前 DFS 访问的被访问节点。一旦当前访问完成，我们将开始节点的 onpath 值重置为 false。

## 卡片打印处理机（Card Print Processor 的缩写）

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether we can finish all
// tasks or not from given dependencies.
import java.util.*;

public class GFG{

    // class to store dependencies as a pair
    static class pair{
        int first, second;

        pair(int first, int second){
            this.first = first;
            this.second = second;
        }
    }

    // Returns adjacency list representation from a list
    // of pairs.
    static ArrayList<ArrayList<Integer>> make_graph(int numTasks,
                Vector<pair> prerequisites)
    {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>(numTasks);

        for(int i=0; i<numTasks; i++){
            graph.add(new ArrayList<Integer>());
        }

        for (pair pre : prerequisites)
            graph.get(pre.second).add(pre.first);

        return graph;
    }

    // A DFS based function to check if there is a cycle
    // in the directed graph.
    static boolean dfs_cycle(ArrayList<ArrayList<Integer>> graph, int node,
                boolean onpath[], boolean visited[])
    {
        if (visited[node])
            return false;
        onpath[node] = visited[node] = true;

        for (int neigh : graph.get(node))
            if (onpath[neigh] || dfs_cycle(graph, neigh, onpath, visited))
                return true;

        return onpath[node] = false;
    }

    // Main function to check whether possible to finish all tasks or not
    static boolean canFinish(int numTasks, Vector<pair> prerequisites)
    {
        ArrayList<ArrayList<Integer>> graph = make_graph(numTasks, prerequisites);

        boolean onpath[] = new boolean[numTasks];
        boolean visited[] = new boolean[numTasks];

        for (int i = 0; i < numTasks; i++)
            if (!visited[i] && dfs_cycle(graph, i, onpath, visited))
                return false;

        return true;
    }

    public static void main(String args[])
    {
        int numTasks = 4;

        Vector<pair> prerequisites = new Vector<pair>();;

        // for prerequisites: [[1, 0], [2, 1], [3, 2]]

        prerequisites.add(new pair(1, 0));
        prerequisites.add(new pair(2, 1));
        prerequisites.add(new pair(3, 2));

        if (canFinish(numTasks, prerequisites)) {
            System.out.println("Possible to finish all tasks");
        }
        else {
            System.out.println("Impossible to finish all tasks");
        }
    }
}

// This code is contributed by adityapande88.
```

**Output:** 

```
Possible to finish all tasks
```

**使用** [**BFS**](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)
BFS 可以用拓扑排序的思想来求解它。如果拓扑排序是可能的，就意味着没有循环，有可能完成所有的任务。
BFS 使用每个节点的索引。我们将首先尝试找到一个索引为 0 的节点。如果我们做不到这一点，图表中一定有一个循环，我们返回 false。否则我们已经找到了。我们将它的索引设置为-1，以防止再次访问它，并将其所有邻居的索引减少 1。这个过程将重复 n 次(节点数)。如果我们没有返回假，我们将返回真。

## 卡片打印处理机（Card Print Processor 的缩写）

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A BFS based solution to check if we can finish
// all tasks or not. This solution is mainly based
// on Kahn's algorithm.
import java.util.*;

public class GFG{

    // class to store dependencies as a pair
    static class pair{
        int first, second;

        pair(int first, int second){
            this.first = first;
            this.second = second;
        }
    }

    // Returns adjacency list representation from a list
    // of pairs.
    static ArrayList<ArrayList<Integer>> make_graph(int numTasks,
                Vector<pair> prerequisites)
    {
        ArrayList<ArrayList<Integer>> graph = new ArrayList<ArrayList<Integer>>(numTasks);

        for(int i=0; i<numTasks; i++){
            graph.add(new ArrayList<Integer>());
        }

        for (pair pre : prerequisites)
            graph.get(pre.second).add(pre.first);

        return graph;
    }

    // Finds in-degree of every vertex
    static int[] compute_indegree(ArrayList<ArrayList<Integer>> graph)
    {
        int degrees[] = new int[graph.size()];

        for (ArrayList<Integer> neighbors : graph)
            for (int neigh : neighbors)
                degrees[neigh]++;

        return degrees;
    }

    // Main function to check whether possible to finish all tasks or not
    static boolean canFinish(int numTasks, Vector<pair> prerequisites)
    {
        ArrayList<ArrayList<Integer>> graph = make_graph(numTasks, prerequisites);
        int degrees[] = compute_indegree(graph);

        for (int i = 0; i < numTasks; i++) {
            int j = 0;
            for (; j < numTasks; j++)
                if (degrees[j] == 0)
                    break;

            if (j == numTasks)
                return false;

            degrees[j] = -1;
            for (int neigh : graph.get(j))
                degrees[neigh]--;
        }

        return true;
    }

    public static void main(String args[])
    {
        int numTasks = 4;
        Vector<pair> prerequisites = new Vector<pair>();

        prerequisites.add(new pair(1, 0));
        prerequisites.add(new pair(2, 1));
        prerequisites.add(new pair(3, 2));

        if (canFinish(numTasks, prerequisites)) {
            System.out.println("Possible to finish all tasks");
        }
        else {
            System.out.println("Impossible to finish all tasks");
        }

    }
}

// This code is contributed by adityapande88.
```

**Output:** 

```
Possible to finish all tasks
```

**参考:**T2】https://leetcode.com/problems/course-schedule/