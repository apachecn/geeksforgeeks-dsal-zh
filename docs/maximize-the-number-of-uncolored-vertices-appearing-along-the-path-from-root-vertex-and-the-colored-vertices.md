# 最大化从根顶点到有色顶点的路径中出现的无色顶点的数量

> 原文： [https://www.geeksforgeeks.org/maximize-the-number-of-uncolored-vertices-appearing-along-the-path-from-root-vertex-and-the-colored-vertices/](https://www.geeksforgeeks.org/maximize-the-number-of-uncolored-vertices-appearing-along-the-path-from-root-vertex-and-the-colored-vertices/)

给定一棵具有 **N 个**顶点的树，顶点 **1 作为根**顶点， **N – 1** 边。 我们必须精确着色`k`的顶点数，**计数根顶点与每个着色顶点之间的无色顶点**的数量。 如果未着色，则必须在计数中包括根顶点。 最大化从根顶点到着色顶点的路径之间出现的未着色顶点数量的任务。

**示例**：

```
Input :

           1
         / |  \
       /   |    \
     2     3      4
          / \      \
         /   \      \
        5     6      7

k = 4 
Output : 7
Explanation:
If we color vertex 2, 5, 6 and 7, 
the number of uncolored vertices between the path
from root to colored vertices is maximum which is 7.

Input :

          1
         / \
        /   \
       2     3
      /
     /
    4

k = 1
Output : 2

```

**方法**：

为了解决上述问题，我们观察到，如果选择一个顶点不着色，则必须选择其父对象不着色。 然后，我们可以计算出如果选择一条通往着色顶点的路径，我们将获得多少个未着色顶点。 只需计算每个顶点的根之间的顶点数量与当前顶点之下的顶点数量之间的差即可。 取所有差异中最大的 k 并计算总和。 使用 nth_element stl 获得`O(N)`解。

下面是上述方法的实现：

```

// C++ program to Maximize the number 
// of uncolored vertices occurring between 
// the path from root vertex and the colored vertices 
#include <bits/stdc++.h> 
using namespace std; 

// Comparator function 
bool cmp(int a, int b) 
{ 
    return a > b; 
} 

class graph { 
    vector<vector<int> > g; 
    vector<int> depth; 
    vector<int> subtree; 
    int* diff; 

public: 
    // Constructor 
    graph(int n) 
    { 
        g = vector<vector<int> >(n + 1); 

        depth = vector<int>(n + 1); 

        subtree = vector<int>(n + 1); 

        diff = new int[n + 1]; 
    } 

    // Function to push edges 
    void push(int a, int b) 
    { 
        g[a].push_back(b); 

        g[b].push_back(a); 
    } 

    // function for dfs traversal 
    int dfs(int v, int p) 
    { 

        // Store depth of vertices 
        depth[v] = depth[p] + 1; 

        subtree[v] = 1; 

        for (auto i : g[v]) { 
            if (i == p) 
                continue; 

            // Calculate number of vertices 
            // in subtree of all vertices 
            subtree[v] += dfs(i, v); 
        } 

        // Computing the difference 
        diff[v] = depth[v] - subtree[v]; 

        return subtree[v]; 
    } 

    // Function that print maximum number of 
    // uncolored vertices occur between root vertex 
    // and all colored vertices 
    void solution(int n, int k) 
    { 

        // Computing first k largest difference 
        nth_element(diff + 1, diff + k, diff + n + 1, cmp); 

        int sum = 0; 

        for (int i = 1; i <= k; i++) { 
            sum += diff[i]; 
        } 

        // Print the result 
        cout << sum << "\n"; 
    } 
}; 

// Driver Code 
int main() 
{ 

    int N = 7; 
    int k = 4; 

    // initialise graph 
    graph g(N); 

    g.push(1, 2); 
    g.push(1, 3); 
    g.push(1, 4); 
    g.push(3, 5); 
    g.push(3, 6); 
    g.push(4, 7); 

    g.dfs(1, 0); 

    g.solution(N, k); 

    return 0; 
} 

```

**Output:**

```
7

```

**时间复杂度**：`O(N)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。