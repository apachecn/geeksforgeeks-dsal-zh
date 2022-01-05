# 使用 DFS 遍历打印矩阵元素

> 原文:[https://www . geesforgeks . org/print-matrix-elements-using-DFS-traversation/](https://www.geeksforgeeks.org/print-matrix-elements-using-dfs-traversal/)

给定一个具有整数维度 **M × N** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **网格[][]** ，任务是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)打印矩阵元素。

**示例:**

> **输入:** mat[][] = {{1，2，3，4}，{5，6，7，8}，{9，10，11，12}，{13，14，15，16}}
> **输出:**1 2 3 4 8 12 16 15 11 7 6 10 14 13 9 5
> **解释:**矩阵元素的深度优先搜索遍历顺序为 1 2 3 4 8 12 16 16
> 
> **输入:** mat[][] = {{0，1，9，4}，{1，2，3，4}，{0，0，-1，-1}，{-1，-1，0，1}}
> **输出:**0 1 9 4 4-1 1 0-1 3 2 0-1-1 0 1 0 1

[**递归**](https://www.geeksforgeeks.org/recursion/) **方法:**思路是使用[递归深度优先搜索](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)遍历矩阵并打印其元素。按照以下步骤解决问题:

*   初始化一个 [2D 布尔向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)，比如 **vis[][]** ，以跟踪已经访问和未访问的索引。
*   定义一个函数，比如说**是有效的(I，j)** ，检查位置 **(i，j)** 是否有效，也就是说 **(i，j)** 应该在矩阵内部而不是被访问。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **DFS(i，j):**
    *   每次调用时，标记当前位置 **(i，j)** 已访问并打印该位置的元素。
    *   对所有相邻边进行递归调用，即 **DFS(i + 1，j)、DFS(i，j + 1)、DFS(I–1，j)** 和 **DFS(i，j–1)**，如果各自位置有效，即未被访问且在[矩阵](https://www.geeksforgeeks.org/matrix/)内。
*   最后，调用函数 **DFS(0，0)** 启动 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)到[打印矩阵](https://www.geeksforgeeks.org/print-2-d-array-matrix-java/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Direction vectors
int dRow[] = { -1, 0, 1, 0 };
int dCol[] = { 0, 1, 0, -1 };

// Function to check if current
// position is valid or not
bool isValid(vector<vector<bool> >& vis,
             int row, int col,
             int COL, int ROW)
{
    // Check if the cell is out of bounds
    if (row < 0 || col < 0 || col > COL - 1
        || row > ROW - 1)
        return false;

    // Check if the cell is visited or not
    if (vis[row][col] == true)
        return false;

    return true;
}

// Utility function to print matrix
// elements using DFS Traversal
void DFSUtil(int row, int col,
             vector<vector<int> > grid,
             vector<vector<bool> >& vis,
             int M, int N)
{
    // Mark the current cell visited
    vis[row][col] = true;

    // Print the element at the cell
    cout << grid[row][col] << " ";

    // Traverse all four adjacent
    // cells of the current element
    for (int i = 0; i < 4; i++) {

        int x = row + dRow[i];
        int y = col + dCol[i];

        // Check if x and y is
        // valid index or not
        if (isValid(vis, x, y, M, N))
            DFSUtil(x, y, grid, vis, M, N);
    }
}

// Function to print the matrix elements
void DFS(int row, int col,
         vector<vector<int> > grid,
         int M, int N)
{
    // Initialize a visiting matrix
    vector<vector<bool> > vis(
        M + 1, vector<bool>(N + 1, false));

    // Function call to print matrix
    // elements by DFS traversal
    DFSUtil(0, 0, grid, vis, M, N);
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > grid{ { 1, 2, 3, 4 },
                               { 5, 6, 7, 8 },
                               { 9, 10, 11, 12 },
                               { 13, 14, 15, 16 } };

    // Row of the matrix
    int M = grid.size();

    // Column of the matrix
    int N = grid[0].size();

    DFS(0, 0, grid, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{
// Direction vectors
static int dRow[] = { -1, 0, 1, 0 };
static int dCol[] = { 0, 1, 0, -1 };

// Function to check if current
// position is valid or not
static boolean isValid(boolean[][] vis,
             int row, int col,
             int COL, int ROW)
{
    // Check if the cell is out of bounds
    if (row < 0 || col < 0 || col > COL - 1
        || row > ROW - 1)
        return false;

    // Check if the cell is visited or not
    if (vis[row][col] == true)
        return false;

    return true;
}

// Utility function to print matrix
// elements using DFS Traversal
static void DFSUtil(int row, int col,
            int[][] grid,
            boolean[][] vis,
            int M, int N)
{

    // Mark the current cell visited
    vis[row][col] = true;

    // Print the element at the cell
    System.out.print(grid[row][col] + " ");

    // Traverse all four adjacent
    // cells of the current element
    for (int i = 0; i < 4; i++) {

        int x = row + dRow[i];
        int y = col + dCol[i];

        // Check if x and y is
        // valid index or not
        if (isValid(vis, x, y, M, N))
            DFSUtil(x, y, grid, vis, M, N);
    }
}
// Function to print the matrix elements
static void DFS(int row, int col,
        int[][] grid,
         int M, int N)
{
    // Initialize a visiting matrix
    boolean[][] vis = new boolean[M + 1][N + 1];
    for(int i = 0; i < M + 1; i++)
    {
        for(int j = 0; j < N + 1; j++)
        {
            vis[i][j] = false;
        }
    }

    // Function call to print matrix
    // elements by DFS traversal
    DFSUtil(0, 0, grid, vis, M, N);
}

// Driver Code
public static void main(String args[])
{
    // Given matrix
    int[][] grid = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    // Row of the matrix
    int M = grid.length;

    // Column of the matrix
    int N = grid[0].length;

    DFS(0, 0, grid, M, N);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Direction vectors
dRow = [-1, 0, 1, 0]
dCol = [0, 1, 0, -1]

# Function to check if current
# position is valid or not
def isValid(row, col, COL, ROW):
    global vis

    # Check if the cell is out of bounds
    if (row < 0 or col < 0 or col > COL - 1 or row > ROW - 1):
        return False

    # Check if the cell is visited or not
    if (vis[row][col] == True):
        return False
    return True

# Utility function to prmatrix
# elements using DFS Traversal
def DFSUtil(row, col,grid, M, N):
    global vis

    # Mark the current cell visited
    vis[row][col] = True

    # Print element at the cell
    print(grid[row][col], end = " ")

    # Traverse all four adjacent
    # cells of the current element
    for i in range(4):

        x = row + dRow[i]
        y = col + dCol[i]

        # Check if x and y is
        # valid index or not
        if (isValid(x, y, M, N)):
            DFSUtil(x, y, grid, M, N)

# Function to print matrix elementsdef
def DFS(row, col,grid, M, N):
    global vis
    # Initialize a visiting matrix

    # Function call to prmatrix
    # elements by DFS traversal
    DFSUtil(0, 0, grid, M, N)

# Driver Code
if __name__ == '__main__':

    # Given matrix
    grid = [ [ 1, 2, 3, 4 ],
           [ 5, 6, 7, 8 ],
           [ 9, 10, 11, 12 ],
           [ 13, 14, 15, 16 ] ]

    # Row of the matrix
    M = len(grid)

    # Column of the matrix
    N = len(grid[0])
    vis = [[False for i in range(M)] for i in range(N)]
    DFS(0, 0, grid, M, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
public class GFG
{

// Direction vectors
static int []dRow = { -1, 0, 1, 0 };
static int []dCol = { 0, 1, 0, -1 };

// Function to check if current
// position is valid or not
static bool isValid(bool[,] vis,
             int row, int col,
             int COL, int ROW)
{

    // Check if the cell is out of bounds
    if (row < 0 || col < 0 || col > COL - 1
        || row > ROW - 1)
        return false;

    // Check if the cell is visited or not
    if (vis[row,col] == true)
        return false;

    return true;
}

// Utility function to print matrix
// elements using DFS Traversal
static void DFSUtil(int row, int col,
            int[,] grid,
            bool[,] vis,
            int M, int N)
{

    // Mark the current cell visited
    vis[row,col] = true;

    // Print the element at the cell
    Console.Write(grid[row,col] + " ");

    // Traverse all four adjacent
    // cells of the current element
    for (int i = 0; i < 4; i++) {

        int x = row + dRow[i];
        int y = col + dCol[i];

        // Check if x and y is
        // valid index or not
        if (isValid(vis, x, y, M, N))
            DFSUtil(x, y, grid, vis, M, N);
    }
}

// Function to print the matrix elements
static void DFS(int row, int col,
        int[,] grid,
         int M, int N)
{

    // Initialize a visiting matrix
    bool[,] vis = new bool[M + 1,N + 1];
    for(int i = 0; i < M + 1; i++)
    {
        for(int j = 0; j < N + 1; j++)
        {
            vis[i,j] = false;
        }
    }

    // Function call to print matrix
    // elements by DFS traversal
    DFSUtil(0, 0, grid, vis, M, N);
}

// Driver Code
public static void Main(String []args)
{

    // Given matrix
    int[,] grid = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    // Row of the matrix
    int M = grid.GetLength(0);

    // Column of the matrix
    int N = grid.GetLength(1);
    DFS(0, 0, grid, M, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Direction vectors
let dRow = [ -1, 0, 1, 0 ];
let dCol = [ 0, 1, 0, -1 ];

// Function to check if current
// position is valid or not
function isValid(vis, row, col,
             COL, ROW)
{
    // Check if the cell is out of bounds
    if (row < 0 || col < 0 || col > COL - 1
        || row > ROW - 1)
        return false;

    // Check if the cell is visited or not
    if (vis[row][col] == true)
        return false;

    return true;
}

// Utility function to print matrix
// elements using DFS Traversal
function DFSUtil(row, col, grid,
            vis, M, N)
{

    // Mark the current cell visited
    vis[row][col] = true;

    // Print the element at the cell
   document.write(grid[row][col] + " ");

    // Traverse all four adjacent
    // cells of the current element
    for (let i = 0; i < 4; i++) {

        let x = row + dRow[i];
        let y = col + dCol[i];

        // Check if x and y is
        // valid index or not
        if (isValid(vis, x, y, M, N))
            DFSUtil(x, y, grid, vis, M, N);
    }
}
// Function to print the matrix elements
function DFS(row, col, grid, M, N)
{
    // Initialize a visiting matrix
    let vis = new Array(M + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < vis.length; i++) {
        vis[i] = new Array(2);
    }

    for(let i = 0; i < M + 1; i++)
    {
        for(let j = 0; j < N + 1; j++)
        {
            vis[i][j] = false;
        }
    }

    // Function call to print matrix
    // elements by DFS traversal
    DFSUtil(0, 0, grid, vis, M, N);
}

    // Driver Code

    // Given matrix
    let grid = [[ 1, 2, 3, 4 ],
                    [ 5, 6, 7, 8 ],
                    [ 9, 10, 11, 12 ],
                    [ 13, 14, 15, 16 ]];

    // Row of the matrix
    let M = grid.length;

    // Column of the matrix
    let N = grid[0].length;

    DFS(0, 0, grid, M, N);

</script>
```

**Output**

```
1 2 3 4 8 12 16 15 11 7 6 10 14 13 9 5 
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*

**迭代方式:**思路是使用[迭代深度优先搜索](https://www.geeksforgeeks.org/iterative-depth-first-traversal/)遍历矩阵，打印矩阵元素。按照以下步骤解决问题:

*   定义一个函数，比如**是有效的(I，j)** ，检查位置 **(i，j)** 是否有效，即 **(i，j)** 是否位于矩阵内部且未被访问。
*   初始化一个 [2d 布尔向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)，比如说 **vis[][]** ，用于跟踪一个位置比如说 **(i，j)** 是否已经被访问过。
*   初始化一个[栈<对< int，int > >](https://www.geeksforgeeks.org/stack-of-pair-in-c-stl-with-examples/) 说 **S** 来实现 DFS 遍历。
*   首先按下堆栈中的第一个单元格 **(0，0)****S**标记访问的单元格。
*   当[栈](https://www.geeksforgeeks.org/stack-data-structure/)T2 不为空时迭代:
    *   在每次迭代中，标记堆栈的顶部元素，如 **(i，j)** 已访问并打印该位置的元素，并从堆栈中移除顶部元素 **S** 。
    *   如果相应位置有效，即未被访问且在矩阵内，则将相邻单元，即 **(i + 1，j)、(I，j + 1)、(I–1，j)** 和 **(i，j–1)**推入堆栈。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Direction vectors
int dRow[] = { -1, 0, 1, 0 };
int dCol[] = { 0, 1, 0, -1 };

// Function to check if curruent
// position is valid or not
bool isValid(vector<vector<bool> >& vis,
             int row, int col,
             int COL, int ROW)
{
    // Check if the cell is out
    // of bounds
    if (row < 0 || col < 0 || col > COL - 1
        || row > ROW - 1)
        return false;

    // Check if the cell is visited
    if (vis[row][col] == true)
        return false;

    return true;
}

// Function to print the matrix elements
void DFS_iterative(vector<vector<int> > grid,
                   int M, int N)
{

    // Stores if a position in the
    // matrix been visited or not
    vector<vector<bool> > vis(
        M + 5, vector<bool>(N + 5, false));

    // Initialize stack to implement DFS
    stack<pair<int, int> > st;

    // Push the first position of grid[][]
    // in the stack
    st.push({ 0, 0 });

    // Mark the cell (0, 0) visited
    vis[0][0] = true;

    while (!st.empty()) {

        // Stores top element of stack
        pair<int, int> p = st.top();

        // Delete the top() element
        // of stack
        st.pop();

        int row = p.first;
        int col = p.second;

        // Print element at the cell
        cout << grid[row][col] << " ";

        // Traverse in all four adjacent
        // sides of current positions
        for (int i = 0; i < 4; i++) {

            int x = row + dRow[i];
            int y = col + dCol[i];

            // Check if x and y is valid
            // position and then push
            // the position of current
            // cell in the stack
            if (isValid(vis, x, y, M, N)) {

                // Push the current cell
                st.push({ x, y });

                // Mark current cell visited
                vis[x][y] = true;
            }
        }
    }
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > grid{ { 1, 2, 3, 4 },
                               { 5, 6, 7, 8 },
                               { 9, 10, 11, 12 },
                               { 13, 14, 15, 16 } };

    // Row of the matrix
    int M = grid.size();

    // Column of the matrix
    int N = grid[0].size();

    DFS_iterative(grid, M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    public static class Pair {
        int Item1, Item2;
        public Pair(int Item1, int Item2) {
            this.Item1 = Item1;
            this.Item2 = Item2;
        }
    }

    // Direction vectors
    static int[] dRow = { -1, 0, 1, 0 };
    static int[] dCol = { 0, 1, 0, -1 };

    static Vector<Vector<Boolean>> vis;

    // Function to check if curruent
    // position is valid or not
    static boolean isValid(int row, int col, int COL, int ROW)
    {

        // Check if the cell is out
        // of bounds
        if (row < 0 || col < 0 || col > COL - 1 || row > ROW - 1)
            return false;

        // Check if the cell is visited
        if (vis.get(row).get(col) == true)
            return false;

        return true;
    }

    // Function to print the matrix elements
    static void DFS_iterative(int[][] grid, int M, int N)
    {

        // Stores if a position in the
        // matrix been visited or not
        vis = new Vector<Vector<Boolean>>();
        for(int i = 0; i < M + 5; i++)
        {
            vis.add(new Vector<Boolean>());
            for(int j = 0; j < N + 5; j++)
            {
                vis.get(i).add(false);
            }
        }

        // Initialize stack to implement DFS
        Vector<Pair> st = new Vector<Pair>();

        // Push the first position of grid[][]
        // in the stack
        st.add(new Pair(0, 0));

        // Mark the cell (0, 0) visited
        vis.get(0).set(0, true);

        while (st.size() > 0) {

            // Stores top element of stack
            Pair p = st.get(st.size() - 1);

            // Delete the top() element
            // of stack
            st.remove(st.size() - 1);

            int row = p.Item1;
            int col = p.Item2;

            // Print element at the cell
            System.out.print(grid[row][col] + " ");

            // Traverse in all four adjacent
            // sides of current positions
            for (int i = 0; i < 4; i++) {

                int x = row + dRow[i];
                int y = col + dCol[i];

                // Check if x and y is valid
                // position and then push
                // the position of current
                // cell in the stack
                if (isValid(x, y, M, N)) {

                    // Push the current cell
                    st.add(new Pair(x, y));

                    // Mark current cell visited
                    vis.get(x).set(y, true);
                }
            }
        }
    }

    public static void main(String[] args)
    {

        // Given matrix
        int[][] grid = { { 1, 2, 3, 4 },
                       { 5, 6, 7, 8 },
                       { 9, 10, 11, 12 },
                       { 13, 14, 15, 16 } };

        // Row of the matrix
        int M = 4;

        // Column of the matrix
        int N = 4;

        DFS_iterative(grid, M, N);
    }
}

// This code is contributed by suresh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Direction vectors
dRow = [ -1, 0, 1, 0 ]
dCol = [ 0, 1, 0, -1 ]

vis = []

# Function to check if curruent
# position is valid or not
def isValid(row, col, COL, ROW):
    global vis

    # Check if the cell is out
    # of bounds
    if (row < 0 or col < 0 or col > COL - 1 or row > ROW - 1):
        return False

    # Check if the cell is visited
    if (vis[row][col] == True):
        return False

    return True

# Function to print the matrix elements
def DFS_iterative(grid, M, N):
    global vis
    # Stores if a position in the
    # matrix been visited or not
    vis = []
    for i in range(M+5):
        vis.append([])
        for j in range(N + 5):
            vis[i].append(False)

    # Initialize stack to implement DFS
    st = []

    # Push the first position of grid[][]
    # in the stack
    st.append([ 0, 0 ])

    # Mark the cell (0, 0) visited
    vis[0][0] = True

    while (len(st) > 0):
        # Stores top element of stack
        p = st[-1]

        # Delete the top() element
        # of stack
        st.pop()

        row = p[0]
        col = p[1]

        # Print element at the cell
        print(grid[row][col], "", end = "")

        # Traverse in all four adjacent
        # sides of current positions
        for i in range(4):
            x = row + dRow[i]
            y = col + dCol[i]

            # Check if x and y is valid
            # position and then push
            # the position of current
            # cell in the stack
            if (isValid(x, y, M, N)):
                # Push the current cell
                st.append([ x, y ])

                # Mark current cell visited
                vis[x][y] = True

# Given matrix
grid = [ [ 1, 2, 3, 4 ],
        [ 5, 6, 7, 8 ],
        [ 9, 10, 11, 12 ],
        [ 13, 14, 15, 16 ] ]

# Row of the matrix
M = len(grid)

# Column of the matrix
N = len(grid[0])

DFS_iterative(grid, M, N)

# This code is contributed by mukesh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Direction vectors
    static int[] dRow = { -1, 0, 1, 0 };
    static int[] dCol = { 0, 1, 0, -1 };

    static List<List<bool>> vis;

    // Function to check if curruent
    // position is valid or not
    static bool isValid(int row, int col, int COL, int ROW)
    {

        // Check if the cell is out
        // of bounds
        if (row < 0 || col < 0 || col > COL - 1 || row > ROW - 1)
            return false;

        // Check if the cell is visited
        if (vis[row][col] == true)
            return false;

        return true;
    }

    // Function to print the matrix elements
    static void DFS_iterative(int[,] grid, int M, int N)
    {

        // Stores if a position in the
        // matrix been visited or not
        vis = new List<List<bool>>();
        for(int i = 0; i < M + 5; i++)
        {
            vis.Add(new List<bool>());
            for(int j = 0; j < N + 5; j++)
            {
                vis[i].Add(false);
            }
        }

        // Initialize stack to implement DFS
        List<Tuple<int,int>> st = new List<Tuple<int,int>>();

        // Push the first position of grid[][]
        // in the stack
        st.Add(new Tuple<int,int>(0, 0));

        // Mark the cell (0, 0) visited
        vis[0][0] = true;

        while (st.Count > 0) {

            // Stores top element of stack
            Tuple<int,int> p = st[st.Count - 1];

            // Delete the top() element
            // of stack
            st.RemoveAt(st.Count - 1);

            int row = p.Item1;
            int col = p.Item2;

            // Print element at the cell
            Console.Write(grid[row,col] + " ");

            // Traverse in all four adjacent
            // sides of current positions
            for (int i = 0; i < 4; i++) {

                int x = row + dRow[i];
                int y = col + dCol[i];

                // Check if x and y is valid
                // position and then push
                // the position of current
                // cell in the stack
                if (isValid(x, y, M, N)) {

                    // Push the current cell
                    st.Add(new Tuple<int,int>(x, y));

                    // Mark current cell visited
                    vis[x][y] = true;
                }
            }
        }
    }

  static void Main()
  {

    // Given matrix
    int[,] grid = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 },
                   { 13, 14, 15, 16 } };

    // Row of the matrix
    int M = 4;

    // Column of the matrix
    int N = 4;

    DFS_iterative(grid, M, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Direction vectors
    let dRow = [ -1, 0, 1, 0 ];
    let dCol = [ 0, 1, 0, -1 ];

    let vis;

    // Function to check if curruent
    // position is valid or not
    function isValid(row, col,
                 COL, ROW)
    {
        // Check if the cell is out
        // of bounds
        if (row < 0 || col < 0 || col > COL - 1
            || row > ROW - 1)
            return false;

        // Check if the cell is visited
        if (vis[row][col] == true)
            return false;

        return true;
    }

    // Function to print the matrix elements
    function DFS_iterative(grid, M, N)
    {

        // Stores if a position in the
        // matrix been visited or not
        vis = [];
        for(let i = 0; i < M + 5; i++)
        {
            vis.push([]);
            for(let j = 0; j < N + 5; j++)
            {
                vis[i].push(false);
            }
        }

        // Initialize stack to implement DFS
        let st = [];

        // Push the first position of grid[][]
        // in the stack
        st.push([ 0, 0 ]);

        // Mark the cell (0, 0) visited
        vis[0][0] = true;

        while (st.length > 0) {

            // Stores top element of stack
            let p = st[st.length - 1];

            // Delete the top() element
            // of stack
            st.pop();

            let row = p[0];
            let col = p[1];

            // Print element at the cell
            document.write(grid[row][col] + " ");

            // Traverse in all four adjacent
            // sides of current positions
            for (let i = 0; i < 4; i++) {

                let x = row + dRow[i];
                let y = col + dCol[i];

                // Check if x and y is valid
                // position and then push
                // the position of current
                // cell in the stack
                if (isValid(x, y, M, N)) {

                    // Push the current cell
                    st.push([ x, y ]);

                    // Mark current cell visited
                    vis[x][y] = true;
                }
            }
        }
    }

    // Given matrix
    let grid = [ [ 1, 2, 3, 4 ],
                [ 5, 6, 7, 8 ],
                [ 9, 10, 11, 12 ],
                [ 13, 14, 15, 16 ] ];

    // Row of the matrix
    let M = grid.length;

    // Column of the matrix
    let N = grid[0].length;

    DFS_iterative(grid, M, N);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
1 5 9 13 14 15 16 12 8 7 3 4 11 10 6 2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*