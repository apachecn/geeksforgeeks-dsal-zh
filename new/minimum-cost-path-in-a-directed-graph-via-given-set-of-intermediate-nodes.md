# 通过给定的中间节点集在有向图中的最小成本路径

> 原文： [https://www.geeksforgeeks.org/minimum-cost-path-in-a-directed-graph-via-given-set-of-intermediate-nodes/](https://www.geeksforgeeks.org/minimum-cost-path-in-a-directed-graph-via-given-set-of-intermediate-nodes/)

给定一个加权有向图`G`，它是由顶点组成的数组 V []，任务是找到经过 **V 集的所有顶点的[最小成本路径](https://www.geeksforgeeks.org/min-cost-path-dp-6/) 从给定源`S`到目的地`D`的**。

**示例**：

> **输入**：V = {7}，S = 0，D = 6
> 
> ![](img/46c12a05cb450814a6507dc6c8ed8cce.png)
> 
> **输出**：11
> **说明**：
> 最小路径 0- > 7- > 5- >6。
> 因此， 路径= 3 + 6 + 2 = 11
> 
> **输入**：V = {7，4}，S = 0，D = 6
> 
> ![](img/46c12a05cb450814a6507dc6c8ed8cce.png)
> 
> **输出**：12
> **说明**：
> 最小路径 0- > 7- > 4- > 6\.
> 因此， 路径= 3 + 5 + 4 = 12

**方法**：
要解决此问题，其想法是使用[广度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历。 **BFS** 通常用于在图形中查找[最短路径，并且所有节点到源，中间节点和目标的最小距离可以通过](https://www.geeksforgeeks.org/shortest-path-unweighted-graph/) [BFS 计算[](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 。

请按照以下步骤解决问题：

*   将 **minSum** 初始化为 **INT_MAX** 。
*   使用 **BFS** 从源节点`S`遍历图形。
*   将源的每个相邻节点标记为新源，然后从该节点执行 **BFS** 。
*   一旦遇到目标节点`D`，则检查是否访问了所有中间节点。
*   如果访问了所有中间节点，则更新 **minSum** 并返回最小值。
*   如果未访问所有中间节点，则返回 **minSum** 。
*   将来源标记为未访问。
*   打印获得的 **minSum** 的最终值。

下面是上述方法的实现：

## C ++

```

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Stores minimum-cost of path from source
int minSum = INT_MAX;

// Function to Perform BFS on graph g
// starting from vertex v
void getMinPathSum(unordered_map<int,
                                 vector<pair<int,
                                             int> > >& graph,
                   vector<bool>& visited,
                   vector<int> necessary,
                   int source, int dest, int currSum)
{
    // If destination is reached
    if (source == dest) {
        // Set flag to true
        bool flag = true;

        // Visit all the intermediate nodes
        for (int i : necessary) {

            // If any intermediate node
            // is not visited
            if (!visited[i]) {
                flag = false;
                break;
            }
        }

        // If all intermediate
        // nodes are visited
        if (flag)

            // Update the minSum
            minSum = min(minSum, currSum);
        return;
    }
    else {

        // Mark the current node
        // visited
        visited = true;

        // Traverse adjacent nodes
        for (auto node : graph) {
            if (!visited[node.first]) {

                // Mark the neighbour visited
                visited[node.first] = true;

                // Find minimum cost path
                // considering the neighbour
                // as the source
                getMinPathSum(graph, visited,
                              necessary, node.first,
                              dest, currSum + node.second);

                // Mark the neighbour unvisited
                visited[node.first] = false;
            }
        }

        // Mark the source unvisited
        visited = false;
    }
}

// Driver Code
int main()
{
    // Stores the graph
    unordered_map<int, vector<pair<int,
                                   int> > >
        graph;
    graph[0] = { { 1, 2 }, { 2, 3 }, { 3, 2 } };
    graph[1] = { { 4, 4 }, { 0, 1 } };
    graph[2] = { { 4, 5 }, { 5, 6 } };
    graph[3] = { { 5, 7 }, { 0, 1 } };
    graph[4] = { { 6, 4 } };
    graph[5] = { { 6, 2 } };
    graph[6] = { { 7, 11 } };

    // Number of nodes
    int n = 7;

    // Source
    int source = 0;

    // Destination
    int dest = 6;

    // Keeps a check on visited
    // and unvisited nodes
    vector<bool> visited(n, false);

    // Stores intemediate nodes
    vector<int> necessary{ 2, 4 };

    getMinPathSum(graph, visited, necessary,
                  source, dest, 0);

    // If no path is found
    if (minSum == INT_MAX)
        cout << "-1\n";
    else
        cout << minSum << '\n';
    return 0;
}

```

## 爪哇

```

// Java program to implement 
// the above approach 
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    pair(int f, int s)
    {
        this.first = f;
        this.second = s;
    }
}

// Stores minimum-cost of path from source
static int minSum = Integer.MAX_VALUE;

// Function to Perform BFS on graph g
// starting from vertex v
static void getMinPathSum(Map<Integer, ArrayList<pair>> graph,
                          boolean[] visited,
                          ArrayList<Integer> necessary,
                          int source, int dest, int currSum)
{

    // If destination is reached
    if (source == dest)
    {

        // Set flag to true
        boolean flag = true;

        // Visit all the intermediate nodes
        for(int i : necessary)
        {

            // If any intermediate node
            // is not visited
            if (!visited[i])
            {
                flag = false;
                break;
            }
        }

        // If all intermediate
        // nodes are visited
        if (flag)

            // Update the minSum
            minSum = Math.min(minSum, currSum);

        return;
    }
    else
    {

        // Mark the current node
        // visited
        visited = true;

        // Traverse adjacent nodes
        for(pair node : graph.get(source))
        {
            if (!visited[node.first]) 
            {

                // Mark the neighbour visited
                visited[node.first] = true;

                // Find minimum cost path
                // considering the neighbour
                // as the source
                getMinPathSum(graph, visited,
                              necessary, node.first,
                              dest, currSum + node.second);

                // Mark the neighbour unvisited
                visited[node.first] = false;
            }
        }

        // Mark the source unvisited
        visited = false;
    }
}

// Driver code
public static void main(String[] args)
{

    // Stores the graph
    Map<Integer, ArrayList<pair>> graph = new HashMap<>();

    for(int i = 0; i <= 6; i++)
        graph.put(i, new ArrayList<pair>());

    graph.get(0).add(new pair(1, 2));
    graph.get(0).add(new pair(2, 3));
    graph.get(0).add(new pair(3, 2));
    graph.get(1).add(new pair(4, 4));
    graph.get(1).add(new pair(0, 1));
    graph.get(2).add(new pair(4, 5));
    graph.get(2).add(new pair(5, 6));
    graph.get(3).add(new pair(5, 7));
    graph.get(3).add(new pair(0, 1));
    graph.get(4).add(new pair(6, 4));
    graph.get(5).add(new pair(4, 2));
    graph.get(6).add(new pair(7, 11));

    // Number of nodes
    int n = 7;

    // Source
    int source = 0;

    // Destination
    int dest = 6;

    // Keeps a check on visited
    // and unvisited nodes
    boolean[] visited = new boolean[n];

    // Stores intemediate nodes
    ArrayList<Integer> necessary = new ArrayList<>(
                                   Arrays.asList(2, 4));

    getMinPathSum(graph, visited, necessary,
                  source, dest, 0);

    // If no path is found
    if (minSum == Integer.MAX_VALUE)
        System.out.println(-1);
    else
        System.out.println(minSum);
}
}

// This code is contributed by offbeat

```

**Output:** 

```
12

```

***时间复杂度**：O（N + M）*
***辅助空间**：O（N + M）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。