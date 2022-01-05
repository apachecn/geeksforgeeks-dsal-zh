# BFS 使用 STL 进行竞争编码

> 原文:[https://www . geesforgeks . org/bfs-using-STL-competitive-coding/](https://www.geeksforgeeks.org/bfs-using-stl-competitive-coding/)

一个基于 STL 的 BFS 的简单实现，在 STL 中使用[队列](https://www.geeksforgeeks.org/queue-cpp-stl/)和[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。邻接表用向量的向量来表示。

```
In BFS, we start with a node.
1) Create a queue and enqueue source into it. 
   Mark source as visited.
2) While queue is not empty, do following
    a) Dequeue a vertex from queue. Let this 
       be f.
    b) Print f
    c) Enqueue all not yet visited adjacent
       of f and mark them visited.
```

下面是从源顶点 1 开始的 BFS 示例。请注意，一个图可以有多个 bfs(甚至从一个特定的顶点)。

![BFS using STL for competitive coding](img/2937b8f5e49cbc777eff03ed060e459e.png)

更多 BFS 详情，请参考[本帖](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph)。
这里的代码经过简化，可以用于竞争性编码。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A Quick implementation of BFS using
// vectors and queue
#include <bits/stdc++.h>
#define pb push_back

using namespace std;

vector<bool> v;
vector<vector<int> > g;

void edge(int a, int b)
{
    g[a].pb(b);

    // for undirected graph add this line
    // g[b].pb(a);
}

void bfs(int u)
{
    queue<int> q;

    q.push(u);
    v[u] = true;

    while (!q.empty()) {

        int f = q.front();
        q.pop();

        cout << f << " ";

        // Enqueue all adjacent of f and mark them visited 
        for (auto i = g[f].begin(); i != g[f].end(); i++) {
            if (!v[*i]) {
                q.push(*i);
                v[*i] = true;
            }
        }
    }
}

// Driver code
int main()
{
    int n, e;
    cin >> n >> e;

    v.assign(n, false);
    g.assign(n, vector<int>());

    int a, b;
    for (int i = 0; i < e; i++) {
        cin >> a >> b;
        edge(a, b);
    }

    for (int i = 0; i < n; i++) {
        if (!v[i])
            bfs(i);
    }

    return 0;
}
```

```
Input:
8 10
0 1
0 2
0 3
0 4
1 5
2 5
3 6
4 6
5 7
6 7

Output:
0 1 2 3 4 5 6 7
```

本文由 [**尼基尔·马亨德兰**](https://auth.geeksforgeeks.org/profile.php?user=Nikhil Mahendran) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。