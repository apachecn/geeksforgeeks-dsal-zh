# 使用 BFS 的水壶问题

> 原文： [https://www.geeksforgeeks.org/water-jug-problem-using-bfs/](https://www.geeksforgeeks.org/water-jug-problem-using-bfs/)

您会得到一公升的水罐和一公升的水罐。 两个水罐最初都是空的。 水壶上没有标记，可以测量较小的数量。 您必须使用水壶来测量 d 小于 n 的 d 升水。

（X，Y）对应于以下状态：X 代表 Jug1 中的水量，Y 代表 Jug2 中的水量。

确定从初始状态（xi，yi）到最终状态（xf， yf），其中（xi，yi）是（0，0），表示两个水罐最初都是空的，而（xf，yf）表示状态可能是（0，d）或（d，0）。

您可以执行的操作是：

1.  清空一个水罐，（X，Y）->（0，Y）清空一个水罐 1

2.  装满水罐，（0，0）->（X，0）装满水罐 1

3.  从一个水罐倒水到另一个水罐，直到其中一个水罐倒空或装满为止，（X，Y）->（X-d，Y + d）

例子：

```
Input : 4 3 2
Output : {(0, 0), (0, 3), (4, 0), (4, 3), 
          (3, 0), (1, 3), (3, 3), (4, 2),
          (0, 2)}

```

我们已经在[两个水壶难题](https://www.geeksforgeeks.org/two-water-jug-puzzle/)中讨论了一种解决方案

在本文中，将讨论基于 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的解决方案。

我们对状态进行广度优先搜索，这些状态将在应用允许的操作后创建，我们还使用成对访问映射来跟踪在搜索中仅应访问一次的状态。也可以使用深度优先实现此解决方案 搜索。

```

#include <bits/stdc++.h> 
#define pii pair<int, int> 
#define mp make_pair 
using namespace std; 

void BFS(int a, int b, int target) 
{ 
    // Map is used to store the states, every 
    // state is hashed to binary value to  
    // indicate either that state is visited  
    // before or not 
    map<pii, int> m; 
    bool isSolvable = false; 
    vector<pii> path; 

    queue<pii> q; // queue to maintain states 
    q.push({ 0, 0 }); // Initialing with initial state 

    while (!q.empty()) { 

        pii u = q.front(); // current state 

        q.pop(); // pop off used state 

        // if this state is already visited 
        if (m[{ u.first, u.second }] == 1) 
            continue; 

        // doesn't met jug constraints 
        if ((u.first > a || u.second > b || 
            u.first < 0 || u.second < 0)) 
            continue; 

        // filling the vector for constructing 
        // the solution path 
        path.push_back({ u.first, u.second }); 

        // marking current state as visited 
        m[{ u.first, u.second }] = 1; 

        // if we reach solution state, put ans=1 
        if (u.first == target || u.second == target) { 
            isSolvable = true; 
            if (u.first == target) { 
                if (u.second != 0) 

                    // fill final state 
                    path.push_back({ u.first, 0 }); 
            } 
            else { 
                if (u.first != 0) 

                    // fill final state 
                    path.push_back({ 0, u.second }); 
            } 

            // print the solution path 
            int sz = path.size(); 
            for (int i = 0; i < sz; i++) 
                cout << "(" << path[i].first 
                    << ", " << path[i].second << ")\n"; 
            break; 
        } 

        // if we have not reached final state  
        // then, start developing intermediate  
        // states to reach solution state 
        q.push({ u.first, b }); // fill Jug2 
        q.push({ a, u.second }); // fill Jug1 

        for (int ap = 0; ap <= max(a, b); ap++) { 

            // pour amount ap from Jug2 to Jug1 
            int c = u.first + ap; 
            int d = u.second - ap; 

            // check if this state is possible or not 
            if (c == a || (d == 0 && d >= 0)) 
                q.push({ c, d }); 

            // Pour amount ap from Jug 1 to Jug2 
            c = u.first - ap; 
            d = u.second + ap; 

            // check if this state is possible or not 
            if ((c == 0 && c >= 0) || d == b) 
                q.push({ c, d }); 
        } 

        q.push({ a, 0 }); // Empty Jug2 
        q.push({ 0, b }); // Empty Jug1 
    } 

    // No, solution exists if ans=0 
    if (!isSolvable) 
        cout << "No solution";  
} 

// Driver code 
int main() 
{ 
    int Jug1 = 4, Jug2 = 3, target = 2; 
    cout << "Path from initial state "
            "to solution state :\n"; 
    BFS(Jug1, Jug2, target); 
    return 0; 
} 

```

输出：

```
Path from initial state to solution state ::
(0, 0)
(0, 3)
(4, 0)
(4, 3)
(3, 0)
(1, 3)
(3, 3)
(4, 2)
(0, 2) 

```

本文由 [**Abhishek rajput**](https://auth.geeksforgeeks.org/profile.php?user=Abhishek rajput) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

