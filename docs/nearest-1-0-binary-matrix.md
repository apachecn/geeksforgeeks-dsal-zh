# 二进制矩阵中最接近的 1

> 原文:[https://www.geeksforgeeks.org/nearest-1-0-binary-matrix/](https://www.geeksforgeeks.org/nearest-1-0-binary-matrix/)

给定一个 m*n 阶的二进制矩阵，任务是为矩阵中的每个 0 找到最近的 1 的距离，并打印最终的距离矩阵。从任何细胞(I，j)，我们只能在四个方向上移动，向上，向下，向左和向右。
<u>注意:</u>从一个单元格到紧邻的另一个单元格的距离总是增加 1。
**示例:**

```
Input : m = 3, n = 4
        mat[m][n] = {{0, 0, 0, 1},
                     {0, 0, 1, 1},
                     {0, 1, 1, 0}}
Output: 3 2 1 0
        2 1 0 0
        1 0 0 1
```

这个问题的一个简单的解决方案是对矩阵中的每个 0 递归地检查矩阵中最近的 1。
一个**高效的解决方案**解决这个问题的办法就是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。下面是解决这个问题的算法:

*   取距离矩阵 dist[m][n]，用 INT_MAX 初始化。
*   现在遍历矩阵，对值为“1”的单元格(I，j)的索引进行 make_pair(i，j)，并将该对推入队列，并更新 dist[i][j] = 0，因为“1”与自身的距离将始终为 0。
*   现在从队列中逐个弹出元素，直到它变空，并在上面调用 **BFS** 。
*   在这里，我们需要找到最近的一个的距离，对于具有“1”的单元格，我们称之为 **BFS** ，因此每当我们从队列中取出 popped 元素的相邻元素时，我们都试图通过放置 if(dist[I][j]+1)<dist[ADci][ADCj]来最小化距离。然后我们更新距离矩阵中相邻元素的距离，并将这个相邻元素推送到队列中，完成 **BFS** 的遍历并填充完整的距离矩阵。
*   完成 **BFS** 遍历后，距离矩阵的每个单元格将包含最近的距离‘1’。

## C++

```
// C++ program to find the minimum distance from a
// "1" in binary matrix.
#include<bits/stdc++.h>
using namespace std;
const int MAX = 1000;

// distance matrix which stores the distance of
// nearest '1'
int dist[MAX][MAX];

// Function to find the nearest '1'
void nearestOne(int mat[][MAX], int m, int n)
{
    // two array when respective values of newx and
    // newy are added to (i,j) it gives up, down,
    // left or right adjacent of (i,j) cell
    int newx[] = {-1, 0, 1, 0};
    int newy[] = {0, -1, 0, 1};

    // queue of pairs to store nodes for bfs
    queue< pair<int,int> > q;

    // traverse matrix and make pair of indices of
    // cell (i,j) having value '1' and push them
    // in queue
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n; j++)
        {
            dist[i][j] = INT_MAX;

            if (mat[i][j] == 1)
            {
                // distance of '1' from itself is always 0
                dist[i][j] = 0;

                // make pair and push it in queue
                q.push(make_pair(i, j));
            }
        }
    }

    // now do bfs traversal
    // pop element from queue one by one until it gets empty
    // pair element to hold the currently popped element
    pair<int ,int> poped;
    while (!q.empty())
    {
        poped = q.front();
        q.pop();

        // coordinate of currently popped node
        int x = poped.first;
        int y = poped.second;

        // now check for all adjancent of popped element
        for (int i=0; i<4; i++)
        {
            int adjx = x + newx[i];
            int adjy = y + newy[i];

            // if new coordinates are within boundary and
            // we can minimize the distance of adjacent
            // then update the distance of adjacent in
            // distance matrix and push this adjacent
            // element in queue for further bfs
            if (adjx>=0 && adjx<m && adjy>=0 && adjy<n &&
                    dist[adjx][adjy] > dist[x][y] + 1)
            {
                // update distance
                dist[adjx][adjy] = dist[x][y] + 1;
                q.push(make_pair(adjx,adjy));
            }
        }
    }
}

// Driver program to run the case
int main()
{
    int m = 3, n = 4;
    int mat[][MAX] = {{0, 0, 0, 1},
        {0, 0, 1, 1},
        {0, 1, 1, 0}
    };

    // Fills values in dist[][]
    nearestOne(mat, m, n);

    // print distance matrix
    for (int i=0; i<m; i++)
    {
        for (int j=0; j<n; j++)
            cout << dist[i][j] << " ";
        cout << endl;
    }
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum distance from a
# "1" in binary matrix.
MAX = 1000
INT_MAX = (2**32)

# distance matrix which stores the distance of
# nearest '1'
dist = [[0 for i in range(MAX)] for j in range(MAX)]

# Function to find the nearest '1'
def nearestOne(mat, m, n):

    # two array when respective values of newx and
    # newy are added to (i,j) it gives up, down,
    # left or right adjacent of (i,j) cell
    newx = [-1, 0, 1, 0]
    newy = [0, -1, 0, 1]

    # queue of pairs to store nodes for bfs
    q = []

    # traverse matrix and make pair of indices of
    # cell (i,j) having value '1' and push them
    # in queue
    for i in range(m):
        for j in range(n):
            dist[i][j] = INT_MAX
            if (mat[i][j] == 1):

                # distance of '1' from itself is always 0
                dist[i][j] = 0

                # make pair and push it in queue
                q.append([i, j])

    # now do bfs traversal
    # pop element from queue one by one until it gets empty
    # pair element to hold the currently popped element
    poped = []
    while (len(q)):
        poped = q[0]
        q.pop(0)

        # coordinate of currently popped node
        x = poped[0]
        y = poped[1]

        # now check for all adjancent of popped element
        for i in range(4):

            adjx = x + newx[i]
            adjy = y + newy[i]

            # if new coordinates are within boundary and
            # we can minimize the distance of adjacent
            # then update the distance of adjacent in
            # distance matrix and push this adjacent
            # element in queue for further bfs
            if (adjx >= 0 and adjx < m and adjy >= 0 and
                adjy < n and dist[adjx][adjy] > dist[x][y] + 1):

                # update distance
                dist[adjx][adjy] = dist[x][y] + 1
                q.append([adjx, adjy])

# Driver code
m = 3
n = 4
mat= [[0, 0, 0, 1], [0, 0, 1, 1], [0, 1, 1, 0]]

# Fills values in dist[][]
nearestOne(mat, m, n)

# prdistance matrix
for i in range(m):
    for j in range(n):
        print(dist[i][j], end=" ")
    print()

# This code is contributed by shubhamsingh10
```

**输出:**

```
3 2 1 0
2 1 0 0
1 0 0 1
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。