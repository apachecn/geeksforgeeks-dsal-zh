# 求给定矩阵中封闭岛的个数

> 原文:[https://www . geesforgeks . org/find-给定矩阵中封闭岛屿的数量/](https://www.geeksforgeeks.org/find-number-of-closed-islands-in-given-matrix/)

给定尺寸为 **NxM** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/) **mat[][]** ，使得 1 表示岛， **0** 表示水。任务是找出给定矩阵中封闭岛的数量。

> 一个封闭的岛被称为 **1s** 群，在所有四个边(不包括对角线)上仅被 **0s** 包围。如果任何 1 位于给定矩阵的边缘，则它不被视为连接岛的一部分，因为它没有被所有 **0** 包围。

**示例:**

> **输入:** N = 5，M = 8，
> mat[][] =
> {{0，0，0，0，0，0，0，1}，
> {0，1，1，1，0，0，1}，
> {0，1，0，1，0，0，0，0，1}，
> {0，1，1，1，1，0，1，1，0，1，0}，
> {0，0，0，0，0，0，0，0，0 **1、1、1、1、** 0、0、1}、
> {0、 **1** 、0、 **1** 、0、0、0、1}、
> {0、 **1、1、1、1、** 0、 **1** 、0}、
> {0、0、0、0、0、0、1}}
> 有
> 黑暗中的岛屿是封闭的，因为它们完全被
> 0s(水)包围。
> 矩阵最后一列还有两个岛，但没有被 0 完全包围。
> 因此它们不是封闭的岛屿。
> 
> **输入:** N = 3，M = 3，矩阵[][] =
> {{1，0，0}，
> {0，1，0}，
> {0，0，1}}
> **输出:** 1

**方法 1–使用** [**DFS 遍历**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) **:** 思路是使用 **DFS 遍历**统计被水包围的岛屿数量。但是我们必须在给定矩阵的角上保持岛的轨迹，因为它们不会被计算在合成岛中。以下是步骤:

1.  初始化一个 2D 访问矩阵(比如说 **vis[][]** )来跟踪给定矩阵中遍历的单元。
2.  对给定矩阵的所有角执行 **DFS 遍历**，如果任何元素的值为 1，则将值为 1 的所有单元格标记为已访问，因为它不能计入结果计数。
3.  对所有剩余的未访问单元执行 **DFS 遍历**，如果遇到的值为 1，则将该单元标记为已访问，在结果计数中对该岛进行计数，并递归调用所有 4 个方向的 DFS，即左、右、上和下，以使所有连接到当前单元的 **1s** 都被访问。
4.  重复上述步骤，直到值为 1 的所有单元格都没有被访问。

下面是上述方法的实现:

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS Traversal to find the count of
# island surrounded by water
def dfs(matrix, visited, x, y, n, m):

    # If the land is already visited
    # or there is no land or the
    # coordinates gone out of matrix
    # break function as there
    # will be no islands
    if (x < 0 or y < 0 or
        x >= n or y >= m or
        visited[x][y] == True or
        matrix[x][y] == 0):
        return

    # Mark land as visited
    visited[x][y] = True

    # Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m);
    dfs(matrix, visited, x, y + 1, n, m);
    dfs(matrix, visited, x - 1, y, n, m);
    dfs(matrix, visited, x, y - 1, n, m);

# Function that counts the closed island
def countClosedIsland(matrix, n, m):

    # Create boolean 2D visited matrix
    # to keep track of visited cell

    # Initially all elements are
    # unvisited.
    visited = [[False for i in range(m)]
                      for j in range(n)]

    # Mark visited all lands
    # that are reachable from edge
    for i in range(n):
        for j in range(m):

            # Traverse corners
            if ((i * j == 0 or i == n - 1 or
                 j == m - 1) and matrix[i][j] == 1 and
                 visited[i][j] == False):
                dfs(matrix, visited, i, j, n, m)

    # To stores number of closed islands
    result = 0

    for i in range(n):
        for j in range(m):

            # If the land not visited
            # then there will be atleast
            # one closed island
            if (visited[i][j] == False and
                 matrix[i][j] == 1):
                result += 1

                # Mark all lands associated
                # with island visited.
                dfs(matrix, visited, i, j, n, m)

    # Return the final count
    return result

#  Driver Code

# Given size of Matrix
N = 5
M = 8

# Given Matrix
matrix = [ [ 0, 0, 0, 0, 0, 0, 0, 1 ],
           [ 0, 1, 1, 1, 1, 0, 0, 1 ],
           [ 0, 1, 0, 1, 0, 0, 0, 1 ],
           [ 0, 1, 1, 1, 1, 0, 1, 0 ],
           [ 0, 0, 0, 0, 0, 0, 0, 1 ] ]

# Function Call
print(countClosedIsland(matrix, N, M))

# This code is contributed by rag2127
```

## C#

```
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

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // DFS Traversal to find the count of
    // island surrounded by water
    function dfs(matrix, visited, x, y, n, m)
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
    function countClosedIsland(matrix, n, m)
    {

        // Create boolean 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        let visited = new Array(n);
        for (let i = 0; i < n; ++i)
        {
            visited[i] = new Array(m);
            for (let j = 0; j < m; ++j)
            {
                visited[i][j] = false;
            }
        }

        // Mark visited all lands
        // that are reachable from edge
        for (let i = 0; i < n; ++i) {
            for (let j = 0; j < m; ++j) {

                // Traverse corners
                if ((i * j == 0 || i == n - 1 || j == m - 1)
                    && matrix[i][j] == 1
                    && visited[i][j] == false)
                    dfs(matrix, visited, i, j, n, m);
            }
        }

        // To stores number of closed islands
        let result = 0;

        for (let i = 0; i < n; ++i) {
            for (let j = 0; j < m; ++j) {

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

    // Given size of Matrix
    let N = 5, M = 8;

    // Given Matrix
    let matrix = [ [ 0, 0, 0, 0, 0, 0, 0, 1 ],
      [ 0, 1, 1, 1, 1, 0, 0, 1 ],
      [ 0, 1, 0, 1, 0, 0, 0, 1 ],
      [ 0, 1, 1, 1, 1, 0, 1, 0 ],
      [ 0, 0, 0, 0, 0, 0, 0, 1 ] ];

    // Function Call
    document.write(countClosedIsland(matrix, N, M));

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*

**<u>方法:单 DFS 遍历</u>**

**对方法 1 的改进:**在上面的方法 1 中，我们看到我们调用了两次 DFS 遍历(一次在带有‘1’的角单元上，然后在不在带有‘1’的角上且未被访问的单元上)。我们可以只使用 1 个 DFS 遍历来解决这个问题。这个想法是为不在拐角处的值为“1”的单元格调用 DFS，在这样做的同时，如果我们在拐角处找到一个值为“1”的单元格，那么这意味着它不应该被算作一个岛。代码如下所示:

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// DFS Traversal to find the count of
// island surrounded by water
static void dfs(int[][] matrix, boolean[][] visited,
                int x, int y, int n, int m,
                boolean hasCornerCell)
{

    // If the land is already visited
    // or there is no land or the
    // coordinates gone out of matrix
    // break function as there
    // will be no islands
    if (x < 0 || y < 0 || x >= n || y >= m ||
        visited[x][y] == true || matrix[x][y] == 0)
        return;

    if (x == 0 || y == 0 ||
        x == n - 1 || y == m - 1)
    {
        if (matrix[x][y] == 1)
            hasCornerCell = true;
    }

    // Mark land as visited
    visited[x][y] = true;

    // Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m,
        hasCornerCell);
    dfs(matrix, visited, x, y + 1, n, m,
        hasCornerCell);
    dfs(matrix, visited, x - 1, y, n, m,
        hasCornerCell);
    dfs(matrix, visited, x, y - 1, n, m,
        hasCornerCell);
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
    int result = 0;

    // Mark visited all lands
    // that are reachable from edge
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {
            if ((i != 0 && j != 0 &&
                 i != n - 1 && j != m - 1) &&
                 matrix[i][j] == 1 &&
                 visited[i][j] == false)
            {

                // Determine if the island is closed
                boolean hasCornerCell = false;

                // hasCornerCell will be updated to
                // true while DFS traversal if there
                // is a cell with value '1' on the corner
                dfs(matrix, visited, i, j, n, m,
                    hasCornerCell);

                // If the island is closed
                if (!hasCornerCell)
                    result = result + 1;
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

// This code is contributed by grand_master
```

## 蟒蛇 3

```
# Python3 program for the above approach

# DFS Traversal to find the count of
# island surrounded by water
def dfs(matrix, visited, x, y, n, m, hasCornerCell):

    # If the land is already visited
    # or there is no land or the
    # coordinates gone out of matrix
    # break function as there
    # will be no islands
    if (x < 0 or y < 0 or
        x >= n or y >= m or
        visited[x][y] == True or
         matrix[x][y] == 0):
        return

    if (x == 0 or y == 0 or
        x == n - 1 or y == m - 1):
        if (matrix[x][y] == 1):
            hasCornerCell = True

    # Mark land as visited
    visited[x][y] = True

    # Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m, hasCornerCell)
    dfs(matrix, visited, x, y + 1, n, m, hasCornerCell)
    dfs(matrix, visited, x - 1, y, n, m, hasCornerCell)
    dfs(matrix, visited, x, y - 1, n, m, hasCornerCell)

# Function that counts the closed island
def countClosedIsland(matrix, n, m):

    # Create boolean 2D visited matrix
    # to keep track of visited cell

    # Initially all elements are
    # unvisited.
    visited = [[False for i in range(m)]
                      for j in range(n)]
    result = 0

    # Mark visited all lands
    # that are reachable from edge
    for i in range(n):
        for j in range(m):
            if ((i != 0 and j != 0 and
                 i != n - 1 and j != m - 1) and
                 matrix[i][j] == 1 and
                visited[i][j] == False):

                # Determine if the island is closed
                hasCornerCell = False

                # hasCornerCell will be updated to
                # true while DFS traversal if there
                # is a cell with value '1' on the corner
                dfs(matrix, visited, i, j,
                    n, m, hasCornerCell)

                # If the island is closed
                if (not hasCornerCell):
                    result = result + 1

    # Return the final count
    return result

# Driver Code

# Given size of Matrix
N, M = 5, 8

# Given Matrix
matrix = [ [ 0, 0, 0, 0, 0, 0, 0, 1 ],
           [ 0, 1, 1, 1, 1, 0, 0, 1 ],
           [ 0, 1, 0, 1, 0, 0, 0, 1 ],
           [ 0, 1, 1, 1, 1, 0, 1, 0 ],
           [ 0, 0, 0, 0, 0, 0, 0, 1 ] ]

# Function Call
print(countClosedIsland(matrix, N, M))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // DFS Traversal to find the count of
  // island surrounded by water
  static void dfs(int[,] matrix, bool[,] visited,
                  int x, int y, int n, int m,
                  bool hasCornerCell)
  {

    // If the land is already visited
    // or there is no land or the
    // coordinates gone out of matrix
    // break function as there
    // will be no islands
    if (x < 0 || y < 0 || x >= n || y >= m ||
        visited[x, y] == true || matrix[x, y] == 0)
      return;

    if (x == 0 || y == 0 ||
        x == n - 1 || y == m - 1)
    {
      if (matrix[x, y] == 1)
        hasCornerCell = true;
    }

    // Mark land as visited
    visited[x, y] = true;

    // Traverse to all adjacent elements
    dfs(matrix, visited, x + 1, y, n, m,
        hasCornerCell);
    dfs(matrix, visited, x, y + 1, n, m,
        hasCornerCell);
    dfs(matrix, visited, x - 1, y, n, m,
        hasCornerCell);
    dfs(matrix, visited, x, y - 1, n, m,
        hasCornerCell);
  }

  // Function that counts the closed island
  static int countClosedIsland(int[,] matrix, int n,
                               int m)
  {

    // Create boolean 2D visited matrix
    // to keep track of visited cell

    // Initially all elements are
    // unvisited.
    bool[,] visited = new bool[n, m];
    int result = 0;

    // Mark visited all lands
    // that are reachable from edge
    for(int i = 0; i < n; ++i)
    {
      for(int j = 0; j < m; ++j)
      {
        if ((i != 0 && j != 0 &&
             i != n - 1 && j != m - 1) &&
            matrix[i, j] == 1 &&
            visited[i, j] == false)
        {

          // Determine if the island is closed
          bool hasCornerCell = false;

          // hasCornerCell will be updated to
          // true while DFS traversal if there
          // is a cell with value '1' on the corner
          dfs(matrix, visited, i, j, n, m,
              hasCornerCell);

          // If the island is closed
          if (!hasCornerCell)
            result = result + 1;
        }
      }
    }

    // Return the final count
    return result;
  }

  // Driver code
  static void Main()
  {

    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    int[,] matrix = { { 0, 0, 0, 0, 0, 0, 0, 1 },
                       { 0, 1, 1, 1, 1, 0, 0, 1 },
                       { 0, 1, 0, 1, 0, 0, 0, 1 },
                       { 0, 1, 1, 1, 1, 0, 1, 0 },
                       { 0, 0, 0, 0, 0, 0, 0, 1 } };

    // Function Call
    Console.WriteLine(countClosedIsland(matrix, N, M));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // DFS Traversal to find the count of
    // island surrounded by water
    function dfs(matrix, visited, x, y, n, m, hasCornerCell)
    {

        // If the land is already visited
        // or there is no land or the
        // coordinates gone out of matrix
        // break function as there
        // will be no islands
        if (x < 0 || y < 0 || x >= n || y >= m ||
            visited[x][y] == true || matrix[x][y] == 0)
            return;

        if (x == 0 || y == 0 ||
            x == n - 1 || y == m - 1)
        {
            if (matrix[x][y] == 1)
                hasCornerCell = true;
        }

        // Mark land as visited
        visited[x][y] = true;

        // Traverse to all adjacent elements
        dfs(matrix, visited, x + 1, y, n, m,
            hasCornerCell);
        dfs(matrix, visited, x, y + 1, n, m,
            hasCornerCell);
        dfs(matrix, visited, x - 1, y, n, m,
            hasCornerCell);
        dfs(matrix, visited, x, y - 1, n, m,
            hasCornerCell);
    }

    // Function that counts the closed island
    function countClosedIsland(matrix, n, m)
    {

        // Create boolean 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        let visited = new Array(n);
        for(let i = 0; i < n; ++i)
        {
            visited[i] = new Array(m);
            for(let j = 0; j < m; ++j)
            {
                visited[i][j] = false;
            }
        }
        let result = 0;

        // Mark visited all lands
        // that are reachable from edge
        for(let i = 0; i < n; ++i)
        {
            for(let j = 0; j < m; ++j)
            {
                if ((i != 0 && j != 0 &&
                     i != n - 1 && j != m - 1) &&
                     matrix[i][j] == 1 &&
                     visited[i][j] == false)
                {

                    // Determine if the island is closed
                    let hasCornerCell = false;

                    // hasCornerCell will be updated to
                    // true while DFS traversal if there
                    // is a cell with value '1' on the corner
                    dfs(matrix, visited, i, j, n, m, hasCornerCell);

                    // If the island is closed
                    if (!hasCornerCell)
                        result = result + 1;
                }
            }
        }

        // Return the final count
        return result;
    }

    // Given size of Matrix
    let N = 5, M = 8;

    // Given Matrix
    let matrix = [ [ 0, 0, 0, 0, 0, 0, 0, 1 ],
                       [ 0, 1, 1, 1, 1, 0, 0, 1 ],
                       [ 0, 1, 0, 1, 0, 0, 0, 1 ],
                       [ 0, 1, 1, 1, 1, 0, 1, 0 ],
                       [ 0, 0, 0, 0, 0, 0, 0, 1 ] ];

    // Function Call
    document.write(countClosedIsland(matrix, N, M));

</script>
```

**Output**

```
2
```

**方法 2–使用** [**BFS 遍历**](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) **:** 想法是使用 BFS 访问拐角处每个值为 1 的单元格，然后遍历给定的矩阵，如果遇到任何值为 1 的未访问单元格，则增加该岛的计数，并使与其连接的所有 1 都为已访问。以下是步骤:

1.  初始化一个 2D 访问矩阵(比如说 **vis[][]** )来跟踪给定矩阵中遍历的单元。
2.  在给定矩阵的所有角上执行 **BFS 遍历**，如果任何元素的值为 1，则将值为 1 的所有单元格标记为已访问，因为它不能在结果计数中计数。
3.  对所有剩余的未访问单元执行 **BFS 遍历**，如果遇到的值为 1，则将该单元标记为已访问，在结果计数中对该岛进行计数，并将所有 4 个方向(即左、右、上、下)的每个单元标记为已访问，以使所有连接到当前单元的 **1s** 。
4.  重复上述步骤，直到值为 1 的所有单元格都没有被访问。
5.  完成以上步骤后，打印岛屿计数。

下面是上述方法的实现

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.LinkedList;
import java.util.Queue;

class GFG{

static int dx[] = { -1, 0, 1, 0 };
static int dy[] = { 0, 1, 0, -1 };

// To store the row and columne index
// of the popped cell
static class Cell
{
    int first, second;
    Cell(int x, int y)
    {
        this.first = x;
        this.second = y;
    }
}

// BFS Traversal to find the count of
// island surrounded by water
static void bfs(int[][] matrix, boolean[][] visited,
                int x, int y, int n, int m)
{

    // To store the popped cell
    Cell temp;

    // To store the cell of BFS
    Queue<Cell> Q = new LinkedList<Cell>();

    // Push the current cell
    Q.add(new Cell(x, y));

    // Until Q is not empty
    while (!Q.isEmpty())
    {
        temp = Q.peek();
        Q.poll();

        // Mark current cell
        // as visited
        visited[temp.first][temp.second] = true;

        // Iterate in all four directions
        for(int i = 0; i < 4; i++)
        {
            int xIndex = temp.first + dx[i];
            int yIndex = temp.second + dy[i];

            // Cell out of the matrix
            if (xIndex < 0 || yIndex < 0 || xIndex >= n ||
                yIndex >= m || visited[xIndex][yIndex] == true ||
                matrix[xIndex][yIndex] == 0)
            {
                continue;
            }

            // Check is adjacent cell is
            // 1 and not visited
            if (visited[xIndex][yIndex] == false &&
                 matrix[xIndex][yIndex] == 1)
            {
                Q.add(new Cell(xIndex, yIndex));
            }
        }
    }
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
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {

            // Traverse corners
            if ((i * j == 0 || i == n - 1 || j == m - 1) &&
                matrix[i][j] == 1 && visited[i][j] == false)
            {
                bfs(matrix, visited, i, j, n, m);
            }
        }
    }

    // To stores number of closed islands
    int result = 0;

    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < m; ++j)
        {

            // If the land not visited
            // then there will be atleast
            // one closed island
            if (visited[i][j] == false &&
                 matrix[i][j] == 1)
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
    System.out.println(countClosedIsland(matrix, N, M));
}
}

// This code is contributed by jainlovely450
```

## 蟒蛇 3

```
# Python program for the above approach
dx = [-1, 0, 1, 0 ]
dy = [0, 1, 0, -1]

global matrix

# DFS Traversal to find the count of
# island surrounded by water
def bfs(x, y, n, m):

    # To store the popped cell
    temp = []

    # To store the cell of BFS
    Q = []

    # Push the current cell
    Q.append([x, y])

    # Until Q is not empty
    while(len(Q) > 0):
        temp = Q.pop()

        # Mark current cell
        # as visited
        visited[temp[0]][temp[1]] = True

        # Iterate in all four directions
        for i in range(4):
            x = temp[0] + dx[i]
            y = temp[1] + dy[i]

            # Cell out of the matrix
            if(x < 0 or y < 0 or x >= n or y >= n or visited[x][y] == True or matrix[x][y] == 0):
                continue
            # Check is adjacent cell is
            # 1 and not visited
            if(visited[x][y] == False and matrix[x][y] == 1):
                Q.append([x, y])

# Function that counts the closed island
def countClosedIsland(n, m):

    # Create boolean 2D visited matrix
    # to keep track of visited cell

    # Initially all elements are
    # unvisited.
    global visited
    visited = [[False for i in range(m)] for j in range(n)]

    # Mark visited all lands
    # that are reachable from edge
    for i in range(n):
        for j in range(m):

            # Traverse corners
            if((i * j == 0 or i == n - 1 or j == m - 1) and matrix[i][j] == 1 and visited[i][j] == False):
                bfs(i, j, n, m);

    # To stores number of closed islands
    result = 0
    for i in range(n):
        for j in range(m):

            # If the land not visited
            # then there will be atleast
            # one closed island
            if(visited[i][j] == False and matrix[i][j] == 1):
                result += 1

                # Mark all lands associated
                # with island visited
                bfs(i, j, n, m);

    # Return the final count
    return result

# Driver Code

# Given size of Matrix
N = 5
M = 8

# Given Matrix
matrix = [[ 0, 0, 0, 0, 0, 0, 0, 1],
          [0, 1, 1, 1, 1, 0, 0, 1],
          [0, 1, 0, 1, 0, 0, 0, 1 ],
          [0, 1, 1, 1, 1, 0, 1, 0 ],
          [0, 0, 0, 0, 0, 0, 0, 1]]

# Function Call
print(countClosedIsland(N, M))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    static int[,] matrix;
    static bool[,] visited;
    static int[] dx = {-1, 0, 1, 0 };
    static int[] dy = {0, 1, 0, -1};

    // DFS Traversal to find the count of
    // island surrounded by water
    static void bfs(int x, int y, int n, int m)
    {
        // To store the popped cell
        Tuple<int,int> temp;

        // To store the cell of BFS
        List<Tuple<int,int>> Q = new List<Tuple<int,int>>();

        // Push the current cell
        Q.Add(new Tuple<int, int>(x, y));

        // Until Q is not empty
        while(Q.Count <= 0)
        {
            temp = Q[0];
            Q.RemoveAt(0);

            // Mark current cell
            // as visited
            visited[temp.Item1,temp.Item2] = true;

            // Iterate in all four directions
            for(int i = 0; i < 4; i++)
            {
                int xIndex = temp.Item1 + dx[i];
                int yIndex = temp.Item2 + dy[i];

                // Cell out of the matrix
                if (xIndex < 0 || yIndex < 0 || xIndex >= n ||
                    yIndex >= m || visited[xIndex,yIndex] == true ||
                    matrix[xIndex,yIndex] == 0)
                {
                    continue;
                }

                // Check is adjacent cell is
                // 1 and not visited
                if (visited[xIndex,yIndex] == false &&
                     matrix[xIndex,yIndex] == 1)
                {
                    Q.Add(new Tuple<int, int>(x, y));
                }
            }
        }
    }

    // Function that counts the closed island
    static int countClosedIsland(int n, int m)
    {
        // Create boolean 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        visited = new bool[n, m];
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                visited[i,j] = false;
            }
        }

        // Mark visited all lands
        // that are reachable from edge
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                // Traverse corners
                if((i * j == 0 || i == n - 1 || j == m - 1) && matrix[i,j] == 1 && visited[i,j] == false)
                {
                    bfs(i, j, n, m);
                }
            }
        }

        // To stores number of closed islands
        int result = 2;
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                // If the land not visited
                // then there will be atleast
                // one closed island
                if(visited[i,j] == false && matrix[i,j] == 1)
                {
                    result = 2;

                    // Mark all lands associated
                    // with island visited
                    bfs(i, j, n, m);
                 }
             }
         }

        // Return the final count
        return result;
   }

  static void Main() {
    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    matrix = new int[5,8]
    { { 0, 0, 0, 0, 0, 0, 0, 1 },
       { 0, 1, 1, 1, 1, 0, 0, 1 },
       { 0, 1, 0, 1, 0, 0, 0, 1 },
       { 0, 1, 1, 1, 1, 0, 1, 0 },
       { 0, 0, 0, 0, 0, 0, 0, 1 } };

    // Function Call
    Console.Write(countClosedIsland(N, M));
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach
    let matrix;
    let visited;
    let dx = [-1, 0, 1, 0 ];
    let dy = [0, 1, 0, -1];

    // DFS Traversal to find the count of
    // island surrounded by water
    function bfs(x, y, n, m)
    {
        // To store the popped cell
        let temp;

        // To store the cell of BFS
        let Q = [];

        // Push the current cell
        Q.push([x, y]);

        // Until Q is not empty
        while(Q.length > 0)
        {
            temp = Q[0];
            Q.pop();

            // Mark current cell
            // as visited
            visited[temp[0]][temp[1]] = true;

            // Iterate in all four directions
            for(let i = 0; i < 4; i++)
            {
                let x = temp[0] + dx[i];
                let y = temp[1] + dy[i];

                // Cell out of the matrix
                if(x < 0 || y < 0 || x >= n || y >= n || visited[x][y] == true || matrix[x][y] == 0)
                {
                    continue;
                }
                // Check is adjacent cell is
                // 1 and not visited
                if(visited[x][y] == false && matrix[x][y] == 1)
                {
                    Q.push([x, y]);
                }
              }
        }
    }

    // Function that counts the closed island
    function countClosedIsland(n, m)
    {
        // Create boolean 2D visited matrix
        // to keep track of visited cell

        // Initially all elements are
        // unvisited.
        visited = new Array(n);
        for(let i = 0; i < n; i++)
        {
            visited[i] = new Array(m);
            for(let j = 0; j < m; j++)
            {
                visited[i][j] = false;
            }
        }

        // Mark visited all lands
        // that are reachable from edge
        for(let i = 0; i < n; i++)
        {
            for(let j = 0; j < m; j++)
            {
                // Traverse corners
                if((i * j == 0 || i == n - 1 || j == m - 1) && matrix[i][j] == 1 && visited[i][j] == false)
                {
                    bfs(i, j, n, m);
                }
            }
         }

        // To stores number of closed islands
        let result = 2;
        for(let i = 0; i < n; i++)
        {
            for(let j = 0; j < m; j++)
            {
                // If the land not visited
                // then there will be atleast
                // one closed island
                if(visited[i][j] == false && matrix[i][j] == 1)
                {
                    result += 1;

                    // Mark all lands associated
                    // with island visited
                    bfs(i, j, n, m);
                 }
             }
         }

        // Return the final count
        return result;
   }

  // Given size of Matrix
  let N = 5, M = 8;

  // Given Matrix
  matrix
    = [ [ 0, 0, 0, 0, 0, 0, 0, 1 ],
    [ 0, 1, 1, 1, 1, 0, 0, 1 ],
    [ 0, 1, 0, 1, 0, 0, 0, 1 ],
    [ 0, 1, 1, 1, 1, 0, 1, 0 ],
    [ 0, 0, 0, 0, 0, 0, 0, 1 ] ];

  // Function Call
  document.write(countClosedIsland(matrix, N, M));

// This code is contributed by decode2207.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*

**方法 3–使用** [**不相交-集合(联合-查找)**](https://www.geeksforgeeks.org/union-find/) **:**

1.  遍历给定的矩阵，将所有的 **1s** 和连接在矩阵角上的 **0s** 改变为。
2.  现在再次遍历矩阵，对于所有连接的 **1s** 集合，创建一条连接所有 1s 的边。
3.  使用不相交集方法查找存储的所有边的连接组件。
4.  完成上述步骤后，打印组件数量。

下面是上述方法的实现:

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG{

static class Edge
{
    int first, second;

    Edge(int x, int y)
    {
        this.first = x;
        this.second = y;
    }
}

// Function that implements the Find
static int Find(int[] hashSet, int val)
{

    // Get the val
    int parent = val;

    // Until parent is not found
    while (parent != hashSet[parent])
    {
        parent = hashSet[parent];
    }

    // Return the parent
    return parent;
}

// Function that implements the Union
static void Union(int[] hashSet, int first, int second)
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
static void change(char[][] matrix, int x, int y,
                                    int n, int m)
{

    // If already zero then return
    if (x < 0 || y < 0 || x > m - 1 ||
        y > n - 1 || matrix[x][y] == '0')
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
static void changeCorner(char[][] matrix)
{

    // Dimensions of matrix
    int m = matrix.length;
    int n = matrix[0].length;

    // Traverse the matrix
    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // If corner cell
            if (i * j == 0 || i == m - 1 || j == n - 1)
            {

                // If value is 1s, then
                // recursively change to 0
                if (matrix[i][j] == '1')
                {
                    change(matrix, i, j, n, m);
                }
            }
        }
    }
}

// Function that counts the number
// of island in the given matrix
static int numIslands(char[][] matrix)
{
    if (matrix.length == 0)
        return 0;

    // Dimensions of the matrix
    int m = matrix.length;
    int n = matrix[0].length;

    // Make all the corners connecting
    // 1s to zero
    changeCorner(matrix);

    // First convert to 1 dimension
    // position and convert all the
    // connections to edges
    ArrayList<Edge> edges = new ArrayList<Edge>();

    for(int i = 0; i < m; i++)
    {
        for(int j = 0; j < n; j++)
        {

            // If the cell value is 1
            if (matrix[i][j] == '1')
            {
                int id = i * n + j;

                // Move right
                if (j + 1 < n)
                {

                    // If right cell is
                    // 1 then make it as
                    // an edge
                    if (matrix[i][j + 1] == '1')
                    {
                        int right = i * n + j + 1;

                        // Push in edge vector
                        edges.add(new Edge(id, right));
                    }
                }

                // Move down
                if (i + 1 < m)
                {

                    // If right cell is
                    // 1 then make it as
                    // an edge
                    if (matrix[i + 1][j] == '1')
                    {
                        int down = (i + 1) * n + j;

                        // Push in edge vector
                        edges.add(new Edge(id, down));
                    }
                }
            }
        }
    }

    // Construct the Union Find structure
    int[] hashSet = new int[m * n];
    for(int i = 0; i < m * n; i++)
    {
        hashSet[i] = i;
    }

    // Next apply Union Find for all
    // the edges stored
    for(Edge edge : edges)
    {
        Union(hashSet, edge.first, edge.second);
    }

    // To count the number of connected
    // islands
    int numComponents = 0;

    // Traverse to find the islands
    for(int i = 0; i < m * n; i++)
    {
        if (matrix[i / n][i % n] == '1' &&
            hashSet[i] == i)
            numComponents++;
    }

    // Return the count of the island
    return numComponents;
}

// Driver Code
public static void main(String[] args)
{

    // Given size of Matrix
    int N = 5, M = 8;

    // Given Matrix
    char[][] matrix = { { '0', '0', '0', '0',
                          '0', '0', '0', '1' },
                        { '0', '1', '1', '1',
                          '1', '0', '0', '1' },
                        { '0', '1', '0', '1',
                          '0', '0', '0', '1' },
                        { '0', '1', '1', '1',
                          '1', '0', '1', '0' },
                        { '0', '0', '0', '0',
                          '0', '0', '0', '1' } };

    // Function Call
    System.out.println(numIslands(matrix));
}
}

// This code is contributed by jainlovely450
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function that implements the Find
def Find(hashSet, val):

    # Get the val
    parent = val

    # Until parent is not found
    while (parent != hashSet[parent]):
        parent = hashSet[parent]

    # Return the parent
    return parent

# Function that implements the Union
def Union(hashSet, first, second):

    # Find the first father
    first_father = Find(hashSet, first)

    # Find the second father
    second_father = Find(hashSet, second)

    # If both are unequals then update
    # first father as ssecond_father
    if (first_father != second_father):
        hashSet[first_father] = second_father

# Recursive Function that change all
# the corners connected 1s to 0s
def change(matrix, x, y, n, m):

    # If already zero then return
    if (x < 0 or y < 0 or x > m - 1 or y > n - 1 or matrix[x][y] == '0'):
        return

    # Change the current cell to '0'
    matrix[x][y] = '0'

    # Recursive Call for all the
    # four corners
    change(matrix, x + 1, y, n, m)
    change(matrix, x, y + 1, n, m)
    change(matrix, x - 1, y, n, m)
    change(matrix, x, y - 1, n, m)

# Function that changes all the
# connected 1s to 0s at the corners
def changeCorner(matrix):

    # Dimensions of matrix
    m = len(matrix)
    n = len(matrix[0])

    # Traverse the matrix
    for i in range(m):
        for j in range(n):

            # If corner cell
            if (i * j == 0 or i == m - 1 or j == n - 1):

                # If value is 1s, then
                # recursively change to 0
                if (matrix[i][j] == '1'):
                    change(matrix, i, j, n, m)

# Function that counts the number
# of island in the given matrix
def numIslands(matrix):
    if (len(matrix) == 0):
        return 0

    # Dimensions of the matrix
    m = len(matrix)
    n = len(matrix[0])

    # Make all the corners connecting
    # 1s to zero
    changeCorner(matrix)

    # First convert to 1 dimension
    # position and convert all the
    # connections to edges
    edges = []
    for i in range(m):
        for j in range(n):

            # If the cell value is 1
            if (matrix[i][j] == '1'):
                id = i * n + j

                # Move right
                if (j + 1 < n):
                    # If right cell is
                    # 1 then make it as
                    # an edge
                    if (matrix[i][j + 1] == '1'):
                        right = i * n + j + 1

                        # Push in edge vector
                        edges.append([id, right])
                # Move down
                if (i + 1 < m):

                    # If right cell is
                    # 1 then make it as
                    # an edge
                    if (matrix[i + 1][j] == '1'):
                        down = (i + 1) * n + j

                        # Push in edge vector
                        edges.append([id, down])

    # Construct the Union Find structure
    hashSet = [0 for i in range(m*n)]
    for i in range(m*n):
        hashSet[i] = i

    # Next apply Union Find for all
    # the edges stored
    for edge in edges:
        Union(hashSet, edge[0], edge[1])

    # To count the number of connected
    # islands
    numComponents = 0

    # Traverse to find the islands
    for i in range(m*n):
        if (matrix[i // n][i % n] == '1' and hashSet[i] == i):
            numComponents += 1

    # Return the count of the island
    return numComponents

# Driver Code
if __name__ == '__main__':

    # Given size of Matrix
    N = 5
    M = 8

    # Given Matrix
    matrix = [['0', '0', '0', '0', '0', '0', '0', '1'],
              ['0', '1', '1', '1', '1', '0', '0', '1'],
              ['0', '1', '0', '1', '0', '0', '0', '1'],
              ['0', '1', '1', '1', '1', '0', '1', '0'],
              ['0', '0', '0', '0', '0', '0', '0', '1']]

    # Function Call
    print(numIslands(matrix))

    # This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function that implements the Find
function Find(hashSet, val)
{

    // Get the val
    var parent = val;

    // Until parent is not found
    while (parent != hashSet[parent]) {
      parent = hashSet[parent];
    }

    // Return the parent
    return parent;
  }

  // Function that implements the Union
  function Union(hashSet, first, second) {
    // Find the first father
    var first_father = Find(hashSet, first);
    // Find the second father
    var second_father = Find(hashSet, second);

    // If both are unequals then update
    // first father as ssecond_father
    if (first_father != second_father) {
      hashSet[first_father] = second_father;
    }
  }

  // Recursive Function that change all
  // the corners connected 1s to 0s
  function change(matrix, x, y, n, m) {
    // If already zero then return
    if (x < 0 || y < 0 || x > m - 1 || y > n - 1 || matrix[x][y] == "0") {
      return;
    }

    // Change the current cell to '0'
    matrix[x][y] = "0";

    // Recursive Call for all the
    // four corners
    change(matrix, x + 1, y, n, m);
    change(matrix, x, y + 1, n, m);
    change(matrix, x - 1, y, n, m);
    change(matrix, x, y - 1, n, m);
  }

  // Function that changes all the
  // connected 1s to 0s at the corners
  function changeCorner(matrix) {
    // Dimensions of matrix
    var m = matrix.length;
    var n = matrix[0].length;

    // Traverse the matrix
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < n; j++) {
        // If corner cell
        if (i * j == 0 || i == m - 1 || j == n - 1) {
          // If value is 1s, then
          // recursively change to 0
          if (matrix[i][j] == "1") {
            change(matrix, i, j, n, m);
          }
        }
      }
    }
  }

  // Function that counts the number
  // of island in the given matrix
  function numIslands(matrix) {
    if (matrix.length == 0) {
      return 0;
    }

    // Dimensions of the matrix
    var m = matrix.length;
    var n = matrix[0].length;

    // Make all the corners connecting
    // 1s to zero
    changeCorner(matrix);

    // First convert to 1 dimension
    // position and convert all the
    // connections to edges
    var edges = [];
    for (let i = 0; i < m; i++) {
      for (let j = 0; j < n; j++) {
        // If the cell value is 1
        if (matrix[i][j] == "1") {
          id = i * n + j;

          // Move right
          if (j + 1 < n) {
            // If right cell is
            // 1 then make it as
            // an edge
            if (matrix[i][j + 1] == "1") {
              var right = i * n + j + 1;

              // Push in edge vector
              edges.push([id, right]);
            }
          }
          // Move down
          if (i + 1 < m) {
            // If right cell is
            // 1 then make it as
            // an edge
            if (matrix[i + 1][j] == "1") {
              var down = (i + 1) * n + j;

              // Push in edge vector
              edges.push([id, down]);
            }
          }
        }
      }
    }
    // Construct the Union Find structure
    var hashSet = Array(m * n).fill(0);
    for (let i = 0; i < m * n; i++) {
      hashSet[i] = i;
    }
    // Next apply Union Find for all
    // the edges stored
    for (let i =0; i<edges.length; i++ ) {
      Union(hashSet, edges[i][0], edges[i][1]);
    }
    // To count the number of connected
    // islands
    var numComponents = 0;

    // Traverse to find the islands
    for (let i = 0; i < m * n; i++) {
      if (matrix[parseInt(i / n)][i % n] == "1" && hashSet[i] == i) {
        numComponents += 1;
      }
    }
    // Return the count of the island
    return numComponents;
  }

  // Driver Code
  // Given size of Matrix
  var N = 5;
  var M = 8;

  // Given Matrix
  var matrix = [
    ["0", "0", "0", "0", "0", "0", "0", "1"],
    ["0", "1", "1", "1", "1", "0", "0", "1"],
    ["0", "1", "0", "1", "0", "0", "0", "1"],
    ["0", "1", "1", "1", "1", "0", "1", "0"],
    ["0", "0", "0", "0", "0", "0", "0", "1"],
  ];

  // Function Call
  document.write(numIslands(matrix));

  // This code is contributed by rdtank.
</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*