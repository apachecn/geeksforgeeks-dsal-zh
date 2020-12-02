# 找出 2D 矩阵中不同岛的数量

> 原文： [https://www.geeksforgeeks.org/find-the-number-of-distinct-islands-in-a-2d-matrix/](https://www.geeksforgeeks.org/find-the-number-of-distinct-islands-in-a-2d-matrix/)

给定一个布尔 2D 矩阵。 任务是找到一组独立的岛的数量，其中一组相连的 1（水平或垂直）形成一个岛。 当且仅当一个岛与另一个岛相等（未旋转或反射）时，才认为两个岛是不同的。

**示例**：

> **输入**：网格[] [] =
> {{1、1、0、0、0}，
> 1、1、0、0、0}，
> 0、0 ，0，1，1}，
> 0，0，0，1，1}}
> 
> **输出**：1
> 左上角的岛 1，1 与右下角的岛 1，1 相同
> 
> **输入**：网格[] [] =
> {{1、1、0、1、1}，
> 1、0、0、0、0}，
> 0、0 ，0，0，1}，
> 1，1，0，1，1}}
> 
> **输出**：3
> 上例中的不同岛为：1，左上角为 1； 1，右上角为 1，右下角为 1。 我们忽略左下角的岛 1、1，因为 1、1 与右上角相同。

**方法**：此问题是问题[岛屿数](https://www.geeksforgeeks.org/find-number-of-islands/)的扩展。

问题的核心是知道两个岛是否相等。 主要标准是两者的数字应相同。 但这并不是我们在上面的示例 2 中看到的唯一标准。 那么我们怎么知道？ 我们可以使用 1 的位置/坐标。

如果我们将任何岛屿的第一个坐标作为基点，然后从该基点计算其他点的坐标，则可以消除重复项以得到不同的岛屿数。 因此，使用这种方法，可以将上面示例 1 中 2 个岛的坐标表示为：[（0，0），（0，1），（1，0），（1，1）]。

**以下是上述方法的实现**：

## C ++

```

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// 2D array for the storing the horizontal and vertical 
// directions. (Up, left, down, right} 
vector<vector<int> > dirs = { { 0, -1 }, 
                              { -1, 0 }, 
                              { 0, 1 }, 
                              { 1, 0 } }; 

// Function to perform dfs of the input grid 
void dfs(vector<vector<int> >& grid, int x0, int y0, 
         int i, int j, vector<pair<int, int> >& v) 
{ 
    int rows = grid.size(), cols = grid[0].size(); 

    if (i < 0 || i >= rows || j < 0 
        || j >= cols || grid[i][j] <= 0) 
        return; 

    // marking the visited element as -1 
    grid[i][j] *= -1; 

    // computing coordinates with x0, y0 as base 
    v.push_back({ i - x0, j - y0 }); 

    // repeat dfs for neighbors 
    for (auto dir : dirs) { 
        dfs(grid, x0, y0, i + dir[0], j + dir[1], v); 
    } 
} 

// Main function that returns distinct count of islands in 
// a given boolean 2D matrix 
int countDistinctIslands(vector<vector<int> >& grid) 
{ 
    int rows = grid.size(); 
    if (rows == 0) 
        return 0; 

    int cols = grid[0].size(); 
    if (cols == 0) 
        return 0; 

    set<vector<pair<int, int> > > coordinates; 

    for (int i = 0; i < rows; ++i) { 
        for (int j = 0; j < cols; ++j) { 

            // If a cell is not 1 
            // no need to dfs 
            if (grid[i][j] != 1) 
                continue; 

            // vector to hold coordinates 
            // of this island 
            vector<pair<int, int> > v; 
            dfs(grid, i, j, i, j, v); 

            // insert the coordinates for 
            // this island to set 
            coordinates.insert(v); 
        } 
    } 

    return coordinates.size(); 
} 

// Driver code 
int main() 
{ 
    vector<vector<int> > grid = { { 1, 1, 0, 1, 1 }, 
                                  { 1, 0, 0, 0, 0 }, 
                                  { 0, 0, 0, 0, 1 }, 
                                  { 1, 1, 0, 1, 1 } }; 

    cout << "Number of distinct islands is "
         << countDistinctIslands(grid); 

    return 0; 
} 

```