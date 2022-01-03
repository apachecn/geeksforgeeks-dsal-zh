# 在给定条件下遍历整个矩阵的最小初始顶点

> 原文： [https://www.geeksforgeeks.org/minimum-initial-vertices-traverse-whole-matrix-given-conditions/](https://www.geeksforgeeks.org/minimum-initial-vertices-traverse-whole-matrix-given-conditions/)

我们为每个矩阵提供了一个包含不同值的矩阵。 我们的目标是找到矩阵中的最小位置集，以便可以从集合中的位置开始遍历整个矩阵。

我们可以在以下条件下遍历矩阵：

*   我们只能移动到其值小于或等于当前单元格值的邻居。 单元的邻居定义为与给定单元共享一侧的单元。

**示例**：

```
Input : 1 2 3
        2 3 1
        1 1 1
Output : 1 1
         0 2
If we start from 1, 1 we can cover 6 
vertices in the order (1, 1) -> (1, 0) -> (2, 0) 
-> (2, 1) -> (2, 2) -> (1, 2). We cannot cover
the entire matrix with this vertex. Remaining 
vertices can be covered (0, 2) -> (0, 1) -> (0, 0). 

Input : 3 3
        1 1
Output : 0 1
If we start from 0, 1, we can traverse 
the entire matrix from this single vertex 
in this order (0, 0) -> (0, 1) -> (1, 1) -> (1, 0). 
Traversing the matrix in this order 
satisfies all the conditions stated above.
```

从以上示例中，我们可以轻松地识别出，为了使用最小数量的职位，我们必须从具有最高像元值的职位开始。 因此，我们选择矩阵中包含最高值的位置。 我们将具有最高值的顶点放在单独的数组中。 从

最大值开始，我们在每个顶点上执行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。 如果在 dfs 中遇到任何未访问的顶点，则必须将此顶点包含在集合中。 处理完所有单元后，该集合将包含所需的顶点。

**这是如何工作的？**

我们需要访问所有顶点并达到最大值，我们必须从它们开始。 如果两个最大值不相邻，则必须同时选择两个。 如果两个最大值相邻，则可以选择其中任意一个，因为允许移动到等值邻居。

## C++

```cpp

// C++ program to find minimum initial
// vertices to reach whole matrix.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// (n, m) is current source cell from which
// we need to do DFS. N and M are total no.
// of rows and columns.
void dfs(int n, int m, bool visit[][MAX],
         int adj[][MAX], int N, int M)
{
    // Marking the vertex as visited
    visit[n][m] = 1;

    // If below neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n + 1 < N &&
        adj[n][m] >= adj[n + 1][m] &&
        !visit[n + 1][m])
        dfs(n + 1, m, visit, adj, N, M);

    // If right neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m + 1 < M &&
        adj[n][m] >= adj[n][m + 1] &&
        !visit[n][m + 1])
        dfs(n, m + 1, visit, adj, N, M);

    // If above neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (n - 1 >= 0 &&
        adj[n][m] >= adj[n - 1][m] &&
        !visit[n - 1][m])
        dfs(n - 1, m, visit, adj, N, M);

    // If left neighbor is valid and has
    // value less than or equal to current
    // cell's value
    if (m - 1 >= 0 &&
        adj[n][m] >= adj[n][m - 1] &&
        !visit[n][m - 1])
        dfs(n, m - 1, visit, adj, N, M);
}

void printMinSources(int adj[][MAX], int N, int M)
{
    // Storing the cell value and cell indices
    // in a vector.
    vector<pair<long int, pair<int, int> > > x;
    for (int i = 0; i < N; i++)
        for (int j = 0; j < M; j++)
            x.push_back(make_pair(adj[i][j],
                        make_pair(i, j)));

    // Sorting the newly created array according
    // to cell values
    sort(x.begin(), x.end());

    // Create a visited array for DFS and
    // initialize it as false.
    bool visit[N][MAX];
    memset(visit, false, sizeof(visit));

    // Applying dfs for each vertex with
    // highest value
    for (int i = x.size()-1; i >=0 ; i--)
    {
        // If the given vertex is not visited
        // then include it in the set
        if (!visit[x[i].second.first][x[i].second.second])
        {
            cout << x[i].second.first << " "
                 << x[i].second.second << endl;
            dfs(x[i].second.first, x[i].second.second,
               visit, adj, N, M);
        }
    }
}

// Driver code
int main()
{
    int N = 2, M = 2;

    int adj[N][MAX] = {{3, 3},
                       {1, 1}};
    printMinSources(adj, N, M);
    return 0;
}

```

## Python

```py

# Python3 program to find minimum initial
# vertices to reach whole matrix
MAX = 100

# (n, m) is current source cell from which
# we need to do DFS. N and M are total no.
# of rows and columns.
def dfs(n, m, visit, adj, N, M):

    # Marking the vertex as visited
    visit[n][m] = 1

    # If below neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (n + 1 < N and
        adj[n][m] >= adj[n + 1][m] and
        not visit[n + 1][m]):
        dfs(n + 1, m, visit, adj, N, M)

    # If right neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (m + 1 < M and
        adj[n][m] >= adj[n][m + 1] and
        not visit[n][m + 1]):
        dfs(n, m + 1, visit, adj, N, M)

    # If above neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (n - 1 >= 0 and
        adj[n][m] >= adj[n - 1][m] and
        not visit[n - 1][m]):
        dfs(n - 1, m, visit, adj, N, M)

    # If left neighbor is valid and has
    # value less than or equal to current
    # cell's value
    if (m - 1 >= 0 and
        adj[n][m] >= adj[n][m - 1] and
        not visit[n][m - 1]):
        dfs(n, m - 1, visit, adj, N, M)

def printMinSources(adj, N, M):

    # Storing the cell value and cell 
    # indices in a vector.
    x = []

    for i in range(N):
        for j in range(M):
            x.append([adj[i][j], [i, j]])

    # Sorting the newly created array according
    # to cell values
    x.sort()

    # Create a visited array for DFS and
    # initialize it as false.
    visit = [[False for i in range(MAX)]
                    for i in range(N)]

    # Applying dfs for each vertex with
    # highest value
    for i in range(len(x) - 1, -1, -1):

        # If the given vertex is not visited
        # then include it in the set
        if (not visit[x[i][1][0]][x[i][1][1]]):
            print('{} {}'.format(x[i][1][0],
                                 x[i][1][1]))

            dfs(x[i][1][0], 
                x[i][1][1],
                visit, adj, N, M)

# Driver code
if __name__=='__main__':

    N = 2
    M = 2

    adj = [ [ 3, 3 ], [ 1, 1 ] ]

    printMinSources(adj, N, M)

# This code is contributed by rutvik_56

```

**输出**：

```
0 1
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。