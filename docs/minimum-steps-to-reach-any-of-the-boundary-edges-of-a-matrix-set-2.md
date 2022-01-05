# 到达矩阵任何边界边的最小步数|集合-2

> 原文:[https://www . geeksforgeeks . org/到达矩阵集边界边缘的最小步骤数-2/](https://www.geeksforgeeks.org/minimum-steps-to-reach-any-of-the-boundary-edges-of-a-matrix-set-2/)

给定一个 N×M 矩阵，其中 a <sub>i，j</sub> = 1 表示单元格不为空，a <sub>i，j</sub> = 0 表示单元格为空，a <sub>i，j</sub> = 2 表示您正站在该单元格处。您可以垂直向上或向下移动，水平向左或向右移动到任何空单元格。任务是找到到达矩阵任何边界边的最小步数。如果无法到达任何边界边缘，打印-1。

**注**:整个矩阵中只会有一个数值为 2 的单元格。

**示例:**

```
Input: matrix[] = {1, 1, 1, 0, 1}
                  {1, 0, 2, 0, 1} 
                  {0, 0, 1, 0, 1}
                  {1, 0, 1, 1, 0} 
Output: 2
Move to the right and then move 
upwards to reach the nearest boundary
edge. 

Input: matrix[] = {1, 1, 1, 1, 1}
                  {1, 0, 2, 0, 1} 
                  {1, 0, 1, 0, 1}
                  {1, 1, 1, 1, 1}
Output: -1 

```

**逼近**:问题已经在[集-1](https://www.geeksforgeeks.org/minimum-steps-to-reach-any-of-the-boundary-edges-of-a-matrix/) 中使用动态规划解决。在本文中，我们将讨论一种使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 的方法。下面给出了解决上述问题的步骤。

*   在矩阵中找到“2”的索引。
*   检查该索引是否是边界边，如果是，则不需要移动。
*   将“2”的索引 x 和索引 y 插入队列，移动为 0。
*   使用二维可见阵列来标记矩阵中的访问位置。
*   迭代直到队列为空或者我们到达任何边界边缘。
*   获取队列中的前面元素(x，y，val = moves)，并将 vis[x][y]标记为已访问。尽可能做所有可能的动作(右、左、上、下)。
*   将所有有效移动的 val+1 及其索引重新插入队列。
*   如果 x 和 y 在任何时候都成为边界边缘，则返回 val。
*   如果所有的移动都完成了，并且队列是空的，那么这是不可能的，因此返回-1。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find Minimum steps
// to reach any of the boundary
// edges of a matrix
#include <bits/stdc++.h>
using namespace std;
#define r 4
#define c 5

// Function to check validity
bool check(int i, int j, int n, int m, int mat[r])
{
    if (i >= 0 && i < n && j >= 0 && j < m) {
        if (mat[i][j] == 0)
            return true;
    }
    return false;
}

// Function to find out minimum steps
int findMinSteps(int mat[r], int n, int m)
{

    int indx, indy;
    indx = indy = -1;

    // Find index of only 2 in matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (mat[i][j] == 2) {
                indx = i, indy = j;
                break;
            }
        }
        if (indx != -1)
            break;
    }

    // Push elements in the queue
    queue<pair<int, pair<int, int> > > q;

    // Push the position 2 with moves as 0
    q.push(make_pair(0, make_pair(indx, indy)));

    // If already at boundary edge
    if (check(indx, indy, n, m, mat))
        return 0;

    // Marks the visit
    bool vis[r];
    memset(vis, 0, sizeof vis);

    // Iterate in the queue
    while (!q.empty()) {
        // Get the front of the queue
        auto it = q.front();

        // Pop the first element from the queue
        q.pop();

        // Get the position
        int x = it.second.first;
        int y = it.second.second;

        // Moves
        int val = it.first;

        // If a boundary edge
        if (x == 0 || x == (n - 1) || y == 0 || y == (m - 1)) {
            return val;
        }

        // Marks the visited array
        vis[x][y] = 1;

        // If a move is possible
        if (check(x - 1, y, n, m, mat)) {

            // If not visited previously
            if (!vis[x - 1][y])
                q.push(make_pair(val + 1, make_pair(x - 1, y)));
        }

        // If a move is possible
        if (check(x + 1, y, n, m, mat)) {

            // If not visited previously
            if (!vis[x + 1][y])
                q.push(make_pair(val + 1, make_pair(x + 1, y)));
        }

        // If a move is possible
        if (check(x, y + 1, n, m, mat)) {

            // If not visited previously
            if (!vis[x][y + 1])
                q.push(make_pair(val + 1, make_pair(x, y + 1)));
        }

        // If a move is possible
        if (check(x, y - 1, n, m, mat)) {

            // If not visited previously
            if (!vis[x][y - 1])
                q.push(make_pair(val + 1, make_pair(x, y - 1)));
        }
    }

    return -1;
}

// Driver Code
int main()
{
    int mat[r] = { { 1, 1, 1, 0, 1 },
                      { 1, 0, 2, 0, 1 },
                      { 0, 0, 1, 0, 1 },
                      { 1, 0, 1, 1, 0 } };

    cout << findMinSteps(mat, r, c);
}
```

## 蟒蛇 3

```
# Python3 program to find Minimum steps
# to reach any of the boundary
# edges of a matrix
from collections import deque
r = 4
c = 5

# Function to check validity
def check(i, j, n, m, mat):

    if (i >= 0 and i < n and j >= 0 and j < m):
        if (mat[i][j] == 0):
            return True

    return False

# Function to find out minimum steps
def findMinSteps(mat, n, m):

    indx = indy = -1;

    # Find index of only 2 in matrix
    for i in range(n):
        for j in range(m):
            if (mat[i][j] == 2):
                indx = i
                indy = j
                break

        if (indx != -1):
            break

    # Push elements in the queue
    q = deque()

    # Push the position 2 with moves as 0
    q.append([0, indx, indy])

    # If already at boundary edge
    if (check(indx, indy, n, m, mat)):
        return 0

    # Marks the visit
    vis=[ [0 for i in range(r)]for i in range(r)]

    # Iterate in the queue
    while len(q) > 0:

        # Get the front of the queue
        it = q.popleft()

        #Pop the first element from the queue

        # Get the position
        x = it[1]
        y = it[2]

        # Moves
        val = it[0]

        # If a boundary edge
        if (x == 0 or x == (n - 1) or y == 0 or y == (m - 1)):
            return val

        # Marks the visited array
        vis[x][y] = 1

        # If a move is possible
        if (check(x - 1, y, n, m, mat)):

            # If not visited previously
            if (not vis[x - 1][y]):
                q.append([val + 1, x - 1, y])

        # If a move is possible
        if (check(x + 1, y, n, m, mat)):

            # If not visited previously
            if (not vis[x + 1][y]):
                q.append([val + 1, x + 1, y])

        # If a move is possible
        if (check(x, y + 1, n, m, mat)):

            # If not visited previously
            if (not vis[x][y + 1]):
                q.append([val + 1, x, y + 1])

        # If a move is possible
        if (check(x, y - 1, n, m, mat)):

            # If not visited previously
            if (not vis[x][y - 1]):
                q.append([val + 1, x, y - 1])

    return -1

# Driver Code
mat = [[1, 1, 1, 0, 1 ],
       [1, 0, 2, 0, 1 ],
       [0, 0, 1, 0, 1 ],
       [1, 0, 1, 1, 0 ] ];

print(findMinSteps(mat, r, c))

# This code is contributed by mohit kumar 29
```

**Output:**

```
2

```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N^2)