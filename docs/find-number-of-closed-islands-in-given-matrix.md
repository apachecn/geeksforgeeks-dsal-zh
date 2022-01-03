# 在给定的矩阵

中查找封闭孤岛的数量

> 原文： [https://www.geeksforgeeks.org/find-number-of-closed-islands-in-given-matrix/](https://www.geeksforgeeks.org/find-number-of-closed-islands-in-given-matrix/)

给定[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/) **mat [] []** 的尺寸为 **NxM** ，使得 1 表示岛屿，`0`表示水。 任务是在给定的矩阵中找到闭合岛的数量。

> 一个封闭的岛称为 **1s** 的组，在所有四个侧面（对角线除外）仅被 **0s** 包围。 如果任何 1 位于给定矩阵的边，则不会被所有`0`包围，因此不将其视为连接岛的一部分。

**示例**：

> **输入**：N = 5，M = 8，
> mat [] [] =
> {{0，0，0，0，0，0，0，1}，
> {0，1，1，1，1，0，0，1}，
> {0，1，0，1，0，0，0，1}，
> {0，1，1，1 ，1，0，1，0}，
> {0，0，0，0，0，0，0，1}}}
> **输出**：2
> **说明 **：
> mat [] [] =
> {{0，0，0，0，0，0，0，1}，
> {0， **1，1，1， 1，** 0，0，1}，
> {0，`1`，0，`1`，0，0，0，1}，
> {0 ， **1，1，1，1，** 0，`1`，0}，
> {0，0，0，0，0，0，0，1}}} [
> 有 2 个封闭的岛屿。
> 黑暗中的岛屿被封闭，因为它们完全被
> 0s（水）包围。
> 矩阵的最后一列还有另外两个岛，但它们并未完全被 0 包围。
> 因此，它们不是封闭的岛屿。
> **输入**：N = 3，M = 3，矩阵[] [] =
> {{1，0，0}，
> {0，1，0}，
> {0，0，1}}
> **输出**：1

**方法 1 –使用** [**DFS 遍历**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) ****：的想法是使用 **DFS 遍历**来计算孤岛数 被水包围。 但是我们必须在给定矩阵的拐角处跟踪岛，因为它们不会计入结果岛中。 步骤如下：

1.  初始化 2D 访问的矩阵（例如**相对于[] []** ），以在给定的矩阵中保持遍历单元格的轨迹。

2.  在给定矩阵的所有角上执行 **DFS 遍历**，如果任何元素的值均为 1，则将所有值为 1 的单元格标记为已访问，因为无法将其计入结果计数中。

3.  对所有剩余的未访问单元执行 **DFS 遍历**，如果遇到的值是 1，则将该单元标记为已访问，将该岛计数为结果计数，然后针对所有 4 个方向（即，左，右， 顶部和底部，使所有 **1 和**都连接到当前单元。

4.  重复上述步骤，直到没有访问所有值为 1 的单元格。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// DFS Traversal to find the count of
// island surrounded by water
void dfs(vector<vector<int> >& matrix,
         vector<vector<bool> >& visited, int x, int y,
         int n, int m)
{
    // If the land is already visited
    // or there is no land or the
    // coordinates gone out of matrix
    // break function as there
    // will be no islands
    if (x < 0 || y < 0 || x >= n || y >= m
        || visited[x][y] == true || matrix[x][y] == 0)
        return;

    // Mark land as visited
    visited[x][y] = true;

    // Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m);
    dfs(matrix, visited, x, y + 1, n, m);
    dfs(matrix, visited, x - 1, y, n, m);
    dfs(matrix, visited, x, y - 1, n, m);
}

// Function that counts the closed island
int countClosedIsland(vector<vector<int> >& matrix, int n,
                      int m)
{

    // Create boolean 2D visited matrix
    // to keep track of visited cell

    // Initially all elements are
    // unvisited.
    vector<vector<bool> > visited(n,
                                  vector<bool>(m, false));

    // Mark visited all lands
    // that are reachable from edge
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {

            // Traverse corners
            if ((i * j == 0 || i == n - 1 || j == m - 1)
                and matrix[i][j] == 1
                and visited[i][j] == false)
                dfs(matrix, visited, i, j, n, m);
        }
    }

    // To stores number of closed islands
    int result = 0;

    for (int i = 0; i < n; ++i) {

        for (int j = 0; j < m; ++j) {

            // If the land not visited
            // then there will be atleast
            // one closed island
            if (visited[i][j] == false
                and matrix[i][j] == 1) {

                result++;

                // Mark all lands associated
                // with island visited.
                dfs(matrix, visited, i, j, n, m);
            }
        }
    }

    // Return the final count
    return result;
}

// Driver Code
int main()
{
    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    vector<vector<int> > matrix
        = { { 0, 0, 0, 0, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 0, 1 },
            { 0, 1, 0, 1, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 1, 0 },
            { 0, 0, 0, 0, 0, 0, 0, 1 } };

    // Function Call
    cout << countClosedIsland(matrix, N, M);
    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
class GFG {

    // DFS Traversal to find the count of
    // island surrounded by water
    static void dfs(int[][] matrix, boolean[][] visited,
                    int x, int y, int n, int m)
    {
        // If the land is already visited
        // or there is no land or the
        // coordinates gone out of matrix
        // break function as there
        // will be no islands
        if (x < 0 || y < 0 || x >= n || y >= m
            || visited[x][y] == true || matrix[x][y] == 0)
            return;

        // Mark land as visited
        visited[x][y] = true;

        // Traverse to all adjacent elements
        dfs(matrix, visited, x + 1, y, n, m);
        dfs(matrix, visited, x, y + 1, n, m);
        dfs(matrix, visited, x - 1, y, n, m);
        dfs(matrix, visited, x, y - 1, n, m);
    }

    // Function that counts the closed island
    static int countClosedIsland(int[][] matrix, int n,
                                 int m)
    {

        // Create boolean 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        boolean[][] visited = new boolean[n][m];

        // Mark visited all lands
        // that are reachable from edge
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {

                // Traverse corners
                if ((i * j == 0 || i == n - 1 || j == m - 1)
                    && matrix[i][j] == 1
                    && visited[i][j] == false)
                    dfs(matrix, visited, i, j, n, m);
            }
        }

        // To stores number of closed islands
        int result = 0;

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {

                // If the land not visited
                // then there will be atleast
                // one closed island
                if (visited[i][j] == false
                    && matrix[i][j] == 1) {
                    result++;

                    // Mark all lands associated
                    // with island visited.
                    dfs(matrix, visited, i, j, n, m);
                }
            }
        }

        // Return the final count
        return result;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given size of Matrix
        int N = 5, M = 8;

        // Given Matrix
        int[][] matrix = { { 0, 0, 0, 0, 0, 0, 0, 1 },
                           { 0, 1, 1, 1, 1, 0, 0, 1 },
                           { 0, 1, 0, 1, 0, 0, 0, 1 },
                           { 0, 1, 1, 1, 1, 0, 1, 0 },
                           { 0, 0, 0, 0, 0, 0, 0, 1 } };

        // Function Call
        System.out.print(countClosedIsland(matrix, N, M));
    }
}

// This code is contributed by Rohit_ranjan

```

## C#

```cs

// C# program for the above approach
using System;

class GFG {

    // DFS Traversal to find the count of
    // island surrounded by water
    static void dfs(int[, ] matrix, bool[, ] visited, int x,
                    int y, int n, int m)
    {

        // If the land is already visited
        // or there is no land or the
        // coordinates gone out of matrix
        // break function as there
        // will be no islands
        if (x < 0 || y < 0 || x >= n || y >= m
            || visited[x, y] == true || matrix[x, y] == 0)
            return;

        // Mark land as visited
        visited[x, y] = true;

        // Traverse to all adjacent elements
        dfs(matrix, visited, x + 1, y, n, m);
        dfs(matrix, visited, x, y + 1, n, m);
        dfs(matrix, visited, x - 1, y, n, m);
        dfs(matrix, visited, x, y - 1, n, m);
    }

    // Function that counts the closed island
    static int countClosedIsland(int[, ] matrix, int n,
                                 int m)
    {

        // Create bool 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        bool[, ] visited = new bool[n, m];

        // Mark visited all lands
        // that are reachable from edge
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {

                // Traverse corners
                if ((i * j == 0 || i == n - 1 || j == m - 1)
                    && matrix[i, j] == 1
                    && visited[i, j] == false)
                    dfs(matrix, visited, i, j, n, m);
            }
        }

        // To stores number of closed islands
        int result = 0;

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {

                // If the land not visited
                // then there will be atleast
                // one closed island
                if (visited[i, j] == false
                    && matrix[i, j] == 1) {
                    result++;

                    // Mark all lands associated
                    // with island visited.
                    dfs(matrix, visited, i, j, n, m);
                }
            }
        }

        // Return the readonly count
        return result;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given size of Matrix
        int N = 5, M = 8;

        // Given Matrix
        int[, ] matrix = { { 0, 0, 0, 0, 0, 0, 0, 1 },
                           { 0, 1, 1, 1, 1, 0, 0, 1 },
                           { 0, 1, 0, 1, 0, 0, 0, 1 },
                           { 0, 1, 1, 1, 1, 0, 1, 0 },
                           { 0, 0, 0, 0, 0, 0, 0, 1 } };

        // Function call
        Console.Write(countClosedIsland(matrix, N, M));
    }
}

// This code is contributed by amal kumar choubey

```

输出：

```
2

```

**时间复杂度**：`O(N * M)`

**辅助空间**：`O(N * M)`

**<u>方法：单个 DFS 遍历</u>**

**对方法 1 的改进**：在上述方法 1 中，我们看到两次调用 DFS 遍历（一次是在拐角单元格为“ 1”时，然后是在不在拐角处的单元格为“ 1”） '并且不会被访问）。 我们仅使用 1 次 DFS 遍历即可解决此问题。 想法是为不在拐角处的值为'1'的单元格调用 DFS，这样做时，如果我们在拐角处找到了值为'1'的单元格，则意味着不应将其视为孤岛 。 代码如下所示：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// DFS Traversal to find the count of
// island surrounded by water
void dfs(vector<vector<int> >& matrix,
         vector<vector<bool> >& visited, int x, int y,
         int n, int m, bool &hasCornerCell)
{
    // If the land is already visited
    // or there is no land or the
    // coordinates gone out of matrix
    // break function as there
    // will be no islands
    if (x < 0 || y < 0 || x >= n || y >= m
        || visited[x][y] == true || matrix[x][y] == 0)
        return;

      // Check for the corner cell
    if(x == 0 || y == 0 || x == n-1 || y == m-1)
    {
      if(matrix[x][y] == 1)
        hasCornerCell = true;
    }

    // Mark land as visited
    visited[x][y] = true;

    // Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m, hasCornerCell);
    dfs(matrix, visited, x, y + 1, n, m, hasCornerCell);
    dfs(matrix, visited, x - 1, y, n, m, hasCornerCell);
    dfs(matrix, visited, x, y - 1, n, m, hasCornerCell);
}

// Function that counts the closed island
int countClosedIsland(vector<vector<int> >& matrix, int n,
                      int m)
{

    // Create boolean 2D visited matrix
    // to keep track of visited cell

    // Initially all elements are
    // unvisited.
    vector<vector<bool>> visited(n,vector<bool>(m, false));

    // Store the count of islands
    int result = 0;  

    // Call DFS on the cells which 
    // are not on corners with value '1'
    for (int i = 0; i < n; ++i) 
    {
        for (int j = 0; j < m; ++j) 
        {

            if ((i != 0 && j != 0 && i != n - 1 && j != m - 1)
                and matrix[i][j] == 1
                and visited[i][j] == false) 
            {

                // Determine if the island is closed
                  bool hasCornerCell = false; 

                /* hasCornerCell will be 
                 updated to true while DFS traversal 
                if there is a cell with value 
                 '1' on the corner */
                dfs(matrix, visited, i, j, n, 
                              m, hasCornerCell);

                /* If the island is closed*/
                  if(!hasCornerCell) 
                  result = result + 1;
            }
        }
    }

    // Return the final count
    return result;
}

// Driver Code
int main()
{
    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    vector<vector<int> > matrix
        = { { 0, 0, 0, 0, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 0, 1 },
            { 0, 1, 0, 1, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 1, 0 },
            { 0, 0, 0, 0, 0, 0, 0, 1 } };

    // Function Call
    cout << countClosedIsland(matrix, N, M);
    return 0;
}

```

输出：

```
2

```

**方法 2 –使用** [**BFS 遍历**](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) ****：的想法是，使用 BFS 遍历拐角处值为 1 的每个单元格，然后遍历 给定的矩阵，如果遇到任何未访问的值为 1 的像元，则增加该岛的计数，并使所有与之相连的 1 都被访问。 步骤如下：

1.  初始化 2D 访问的矩阵（例如**相对于[] []** ），以在给定的矩阵中保持遍历单元格的轨迹。

2.  在给定矩阵的所有角上执行 **BFS 遍历**，如果任何元素的值均为 1，则将所有值为 1 的单元格标记为已访问，因为无法将其计入结果计数中。

3.  对所有剩余的未访问单元执行 **BFS 遍历**，如果遇到的值为 1，则将该单元标记为已访问，将该岛计数为结果计数，并在所有 4 个方向（即，左，右， 顶部和底部，使所有 **1 和**连接到当前单元。

4.  重复上述步骤，直到没有访问所有值为 1 的单元格。

5.  完成上述步骤后，打印岛数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dx[] = { -1, 0, 1, 0 };
int dy[] = { 0, 1, 0, -1 };

// DFS Traversal to find the count of
// island surrounded by water
void bfs(vector<vector<int> >& matrix,
         vector<vector<bool> >& visited,
         int x, int y, int n, int m)
{
    // To store the popped cell
    pair<int, int> temp;

    // To store the cell of BFS
    queue<pair<int, int> > Q;

    // Push the current cell
    Q.push({ x, y });

    // Until Q is not empty
    while (!Q.empty()) 
    {

        temp = Q.front();
        Q.pop();

        // Mark current cell
        // as visited
        visited[temp.first]
               [temp.second]
            = true;

        // Iterate in all four directions
        for (int i = 0; i < 4; i++) 
        {
            int x = temp.first + dx[i];
            int y = temp.second + dy[i];

            // Cell out of the matrix
            if (x < 0 || y < 0
                || x >= n || y >= m
                || visited[x][y] == true
                || matrix[x][y] == 0) 
            {
                continue;
            }

            // Check is adjacent cell is
            // 1 and not visited
            if (visited[x][y] == false
                && matrix[x][y] == 1) 
            {
                Q.push({ x, y });
            }
        }
    }
}

// Function that counts the closed island
int countClosedIsland(vector<vector<int> >& matrix,
                      int n, int m)
{

    // Create boolean 2D visited matrix
    // to keep track of visited cell

    // Initially all elements are
    // unvisited.
    vector<vector<bool> > visited(
        n, vector<bool>(m, false));

    // Mark visited all lands
    // that are reachable from edge
    for (int i = 0; i < n; ++i) 
    {
        for (int j = 0; j < m; ++j) 
        {

            // Traverse corners
            if ((i * j == 0
                 || i == n - 1
                 || j == m - 1)
                and matrix[i][j] == 1
                and visited[i][j] == false) 
            {
                bfs(matrix, visited,
                    i, j, n, m);
            }
        }
    }

    // To stores number of closed islands
    int result = 0;

    for (int i = 0; i < n; ++i) 
    {

        for (int j = 0; j < m; ++j) 
        {

            // If the land not visited
            // then there will be atleast
            // one closed island
            if (visited[i][j] == false
                and matrix[i][j] == 1) 
            {

                result++;

                // Mark all lands associated
                // with island visited
                bfs(matrix, visited, i, j, n, m);
            }
        }
    }

    // Return the final count
    return result;
}

// Driver Code
int main()
{
    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    vector<vector<int> > matrix
        = { { 0, 0, 0, 0, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 0, 1 },
            { 0, 1, 0, 1, 0, 0, 0, 1 },
            { 0, 1, 1, 1, 1, 0, 1, 0 },
            { 0, 0, 0, 0, 0, 0, 0, 1 } };

    // Function Call
    cout << countClosedIsland(matrix, N, M);
    return 0;
}

```

输出：

```
2

```

**时间复杂度**：`O(N * M)`

**辅助空间**：`O(N * M)`

**方法 3 –使用** [**不交集（联合查找）**](https://www.geeksforgeeks.org/union-find/) ****：

1.  遍历给定的矩阵，并将所有 **1s** 更改，并将在矩阵角处连接的 **0s** 。

2.  现在再次遍历矩阵，并为所有连接的 **1s** 创建一条连接所有 1s 的边。

3.  查找使用“不相交集方法”存储的所有边的连通组件。

4.  完成上述步骤后，打印组件数。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that implements the Find
int Find(vector<int>& hashSet, int val)
{

    // Get the val
    int parent = val;

    // Until parent is not found
    while (parent != hashSet[parent]) {
        parent = hashSet[parent];
    }

    // Return the parent
    return parent;
}

// Function that implements the Union
void Union(vector<int>& hashSet,
           int first, int second)
{

    // Find the first father
    int first_father = Find(hashSet, first);

    // Find the second father
    int second_father = Find(hashSet, second);

    // If both are unequals then update
    // first father as ssecond_father
    if (first_father != second_father)
        hashSet[first_father] = second_father;
}

// Recursive Function that change all
// the corners connected 1s to 0s
void change(vector<vector<char> >& matrix,
            int x, int y, int n, int m)
{

    // If already zero then return
    if (x < 0 || y < 0 || x > m - 1
        || y > n - 1 || matrix[x][y] == '0')
        return;

    // Change the current cell to '0'
    matrix[x][y] = '0';

    // Recursive Call for all the
    // four corners
    change(matrix, x + 1, y, n, m);
    change(matrix, x, y + 1, n, m);
    change(matrix, x - 1, y, n, m);
    change(matrix, x, y - 1, n, m);
}

// Function that changes all the
// connected 1s to 0s at the corners
void changeCorner(vector<vector<char> >& matrix)
{
    // Dimensions of matrix
    int m = matrix.size();
    int n = matrix[0].size();

    // Traverse the matrix
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {

            // If corner cell
            if (i * j == 0 || i == m - 1
                || j == n - 1) {

                // If value is 1s, then
                // recursively change to 0
                if (matrix[i][j] == '1') {
                    change(matrix, i, j, n, m);
                }
            }
        }
    }
}

// Function that counts the number
// of island in the given matrix
int numIslands(vector<vector<char> >& matrix)
{

    if (matrix.size() == 0)
        return 0;

    // Dimensions of the matrix
    int m = matrix.size();
    int n = matrix[0].size();

    // Make all the corners connecting
    // 1s to zero
    changeCorner(matrix);

    // First convert to 1 dimension
    // position and convert all the
    // connections to edges
    vector<pair<int, int> > edges;

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {

            // If the cell value is 1
            if (matrix[i][j] == '1') {
                int id = i * n + j;

                // Move right
                if (j + 1 < n) {

                    // If right cell is
                    // 1 then make it as
                    // an edge
                    if (matrix[i][j + 1] == '1') {

                        int right = i * n + j + 1;

                        // Push in edge vector
                        edges.push_back(make_pair(id, right));
                    }
                }
                // Move down
                if (i + 1 < m) {

                    // If right cell is
                    // 1 then make it as
                    // an edge
                    if (matrix[i + 1][j] == '1') {
                        int down = (i + 1) * n + j;

                        // Push in edge vector
                        edges.push_back(make_pair(id, down));
                    }
                }
            }
        }
    }

    // Construct the Union Find structure
    vector<int> hashSet(m * n, 0);
    for (int i = 0; i < m * n; i++) {
        hashSet[i] = i;
    }

    // Next apply Union Find for all
    // the edges stored
    for (auto edge : edges) {
        Union(hashSet, edge.first, edge.second);
    }

    // To count the number of connected
    // islands
    int numComponents = 0;

    // Traverse to find the islands
    for (int i = 0; i < m * n; i++) {
        if (matrix[i / n][i % n] == '1'
            && hashSet[i] == i)
            numComponents++;
    }

    // Return the count of the island
    return numComponents;
}

// Driver Code
int main()
{
    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    vector<vector<char> > matrix
        = { { '0', '0', '0', '0', '0', '0', '0', '1' },
            { '0', '1', '1', '1', '1', '0', '0', '1' },
            { '0', '1', '0', '1', '0', '0', '0', '1' },
            { '0', '1', '1', '1', '1', '0', '1', '0' },
            { '0', '0', '0', '0', '0', '0', '0', '1' } };

    // Function Call
    cout << numIslands(matrix);
    return 0;
}

```

输出：

```
2

```

**时间复杂度**：`O(N * M)`

**辅助空间**：`O(N * M)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。