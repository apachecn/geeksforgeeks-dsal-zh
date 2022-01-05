# 找到比赛的获胜者|多次查询

> 原文:[https://www . geesforgeks . org/find-the-winner-match-multi-query/](https://www.geeksforgeeks.org/find-the-winner-of-the-match-multiple-queries/)

给定一组大小为 **N** 的对子 **arr** ，表示第一个玩家赢第二个玩家的游戏情况。给定多个查询，每个查询包含两个数字，任务是确定如果它们相互竞争，哪一个会赢。
**注:**

*   如果 **A** 战胜**B****B**战胜 **C** ，那么 **A** 将永远战胜 **C** 。
*   如果 **A** 战胜 **B** 和 **A** 战胜 **C** ，如果与 **B** 和 **C** 有一场比赛，如果我们不能确定获胜者，那么人数较少的玩家获胜

**例:**

> **输入:** arr[] = {{0，1}、{0，2}、{0，3}、{1，5}、{2，5}、{3，4}、{4，5}、{6，0}}
> 查询[] = {{3，5}、{1，2}}
> **输出:** 3
> 1
> **说明:** 3 胜 4，4 胜 5。所以，3 是第一场比赛的赢家。
> 我们无法在 1 和 2 之间确定胜者。所以，数字较小的玩家就是赢家即 1
> **输入:** arr[] = {{0，1}，{0，2}，{0，3}，{1，5}，{2，5}，{3，4}，{4，5}，{6，0}}
> 查询[] = {{0，5}，{0，6}}
> **输出:** 0
> 6

**先决条件:** [拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)
**方法:**
我们假设所有输入都有效。现在建立一个图表。如果 playerX 赢了 playerY，那么我们从 playerX 到 playerY 增加了一个优势。建立图后做拓扑排序。对于形式(x，y)的每个查询，我们检查拓扑排序中 x 或 y 在哪个数字之前，并打印答案。
以下是上述方法的实施:

## C++

```
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

## 蟒蛇 3

```
# Python3 program to find winner of the match

# Function to add edge between two nodes
def add(adj, u, v):
    adj[u].append(v)

# Function returns topological order of given graph
def topo(adj, n):

    # Indeg vector will store
    # indegrees of all vertices
    indeg = [0 for i in range(n)]
    for i in range(n):
        for x in adj[i]:
            indeg[x] += 1

    # Answer vector will have our
    # final topological order
    answer = []

    # Visited will be true if that
    # vertex has been visited
    visited = [False for i in range(n)]

    # q will store the vertices
    # that have indegree equal to zero
    q = []
    for i in range(n):
        if (indeg[i] == 0):
            q.append(i)
            visited[i] = True

    # Iterate till queue is not empty
    while (len(q) != 0):
        u = q[0]

        # Push the front of queue to answer
        answer.append(u)
        q.remove(q[0])

        # For all neighbours of u, decrement
        # their indegree value
        for x in adj[u]:
            indeg[x] -= 1

            # If indegree of any vertex becomes zero and
            # it is not marked then push it to queue
            if (indeg[x] == 0 and visited[x] == False):
                q.append(x)

                # Mark this vertex as visited
                visited[x] = True

    # Return the resultant topological order
    return answer

# Function to return the winner between u and v
def who_wins(topotable, u, v):
    # Player who comes first wins
    for x in topotable:
        if (x == u):
            return u
        if (x == v):
            return v

# Driver code
if __name__ == '__main__':
    adj = [[] for i in range(10)]

    # Total number of players
    n = 7

    # Build the graph
    # add(adj, x, y) means x wins over y
    add(adj, 0, 1)
    add(adj, 0, 2)
    add(adj, 0, 3)
    add(adj, 1, 5)
    add(adj, 2, 5)
    add(adj, 3, 4)
    add(adj, 4, 5)
    add(adj, 6, 0)

    # Resultant topological order in topotable
    topotable = topo(adj, n)

    # Queries
    print(who_wins(topotable, 3, 5))
    print(who_wins(topotable, 1, 2))

# This code is contributed by Surendra_Gangwar
```

**Output:** 

```
3
1
```