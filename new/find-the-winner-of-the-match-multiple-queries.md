# 查找比赛的获胜者| 多个查询

> 原文： [https://www.geeksforgeeks.org/find-the-winner-of-the-match-multiple-queries/](https://www.geeksforgeeks.org/find-the-winner-of-the-match-multiple-queries/)

给定大小为`N`的对 **arr** 对的数组，表示第一位玩家对第二位玩家获胜的游戏情况。 给定多个查询，每个查询包含两个数字，任务是确定如果彼此竞争，哪个将获胜。

**注意**：

*   如果`A`胜过`B`和`B`胜过`C`，那么`A`将永远胜过`C`。

*   如果`A`胜过`B`和`A`胜过`C`，则如果与`B`和`C`，如果我们无法确定获胜者，则数字较小的玩家获胜

**示例**：

> **输入**：arr [] = {{0，1}，{0，2}，{0，3}，{1，5}，{2，5}，{3，4}，{ 4，5}，{6，0}}
> 查询[] = {{3，5}，{1，2}}
> **输出**：5
> 1
> **说明**：4 胜 3 胜 5 胜 4 胜。所以，第一场比赛的赢家是 5。
> 我们无法确定 1 到 2 之间的获胜者。因此，数字较小的玩家是获胜者，即 1
> 
> **输入**：arr [] = {{0，1}，{0，2}，{0，3}，{1，5}，{2，5}，{3，4}，{ 4，5}，{6，0}}
> 查询[] = {{0，5}，{0，6}}
> **输出**：5
> 0

**先决条件**：[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)

**方法**：

假设所有输入均有效。 现在建立一个图形。 如果玩家 X 赢得玩家 Y，那么我们将玩家 X 的优势添加到玩家 Y。 构建图后，进行拓扑排序。 对于形式（x，y）的每个查询，我们检查拓扑顺序中先于 x 或 y 的数字，然后打印答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find winner of the match 
#include <bits/stdc++.h> 
using namespace std; 

// Function to add edge between two nodes 
void add(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
} 

// Function returns topological order of given graph 
vector<int> topo(vector<int> adj[], int n) 
{ 
    // Indeg vector will store 
    // indegrees of all vertices 
    vector<int> indeg(n, 0); 
    for (int i = 0; i < n; i++) { 
        for (auto x : adj[i]) 
            indeg[x]++; 
    } 
    // Answer vector will have our 
    // final topological order 
    vector<int> answer; 

    // Visited will be true if that 
    // vertex has been visited 
    vector<bool> visited(n, false); 

    // q will store the vertices 
    // that have indegree equal to zero 
    queue<int> q; 
    for (int i = 0; i < n; i++) { 
        if (indeg[i] == 0) { 
            q.push(i); 
            visited[i] = true; 
        } 
    } 

    // Iterate till queue is not empty 
    while (!q.empty()) { 
        int u = q.front(); 
        // Push the front of queue to answer 
        answer.push_back(u); 
        q.pop(); 

        // For all neighbours of u, decrement 
        // their indegree value 
        for (auto x : adj[u]) { 
            indeg[x]--; 

            // If indegree of any vertex becomes zero and 
            // it is not marked then push it to queue 
            if (indeg[x] == 0 && !visited[x]) { 
                q.push(x); 
                // Mark this vertex as visited 
                visited[x] = true; 
            } 
        } 
    } 

    // Return the resultant topological order 
    return answer; 
} 
// Function to return the winner between u and v 
int who_wins(vector<int> topotable, int u, int v) 
{ 
    // Player who comes first wins 
    for (auto x : topotable) { 
        if (x == u) 
            return u; 
        if (x == v) 
            return v; 
    } 
} 

// Driver code 
int main() 
{ 
    vector<int> adj[10]; 

    // Total number of players 
    int n = 7; 

    // Build the graph 
    // add(adj, x, y) means x wins over y 
    add(adj, 0, 1); 
    add(adj, 0, 2); 
    add(adj, 0, 3); 
    add(adj, 1, 5); 
    add(adj, 2, 5); 
    add(adj, 3, 4); 
    add(adj, 4, 5); 
    add(adj, 6, 0); 

    // Resultant topological order in topotable 
    vector<int> topotable = topo(adj, n); 

    // Queries 
    cout << who_wins(topotable, 3, 5) << endl; 
    cout << who_wins(topotable, 1, 2) << endl; 

    return 0; 
} 

```