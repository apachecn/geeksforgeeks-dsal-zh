# 从源

到网格角的最小距离

> 原文： [https://www.geeksforgeeks.org/minimum-distance-to-the-corner-of-a-grid-from-source/](https://www.geeksforgeeks.org/minimum-distance-to-the-corner-of-a-grid-from-source/)

给定二阶网格 **r * c** 和初始位置。 任务是找到从源到网格任何角落的最小距离。 仅当 **grid [i] [j] = 0** 并且仅剩下，**时，才能移动到单元格 **grid [i] [j]** 允许向右**，**向上**和**向下**移动。 如果没有有效的路径，则打印`-1`。

**示例**：

> **输入**：i = 1，j = 1，grid [] [] = {{0，0，1}，{0，0，0}，{1，1，1}}
> **输出**：2
> （1、1）->（1、0）->（0、0）
> 
> **输入**：i = 0，j = 0，grid [] [] = {{0，1}，{1，1}}
> **输出**：0
> 源已经是网格的一角。

**方法**：

*   如果来源已经在角落，则打印`0`。

*   使用 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 从源开始遍历网格：

    *   在队列中插入单元格位置。

    *   从队列中弹出元素，并将其标记为已访问。

    *   对于与弹出的动作相邻的每个有效动作，将单元格位置插入队列。

    *   每次移动时，更新单元格到初始位置的最小距离。

*   BFS 完成后，找到从源到每个角的最小距离。

*   最后打印其中的最小值。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 
#define row 5 
#define col 5 

// Global variables for grid, minDistance and visited array 
int minDistance[row + 1][col + 1], visited[row + 1][col + 1]; 

// Queue for BFS 
queue<pair<int, int> > que; 

// Function to find whether the move is valid or not 
bool isValid(int grid[][col], int i, int j) 
{ 
    if (i < 0 || j < 0 
        || j >= col || i >= row 
        || grid[i][j] || visited[i][j]) 
        return false; 

    return true; 
} 

// Function to return the minimum distance 
// from source to the end of the grid 
int minDistance(int grid[][col], 
                           int sourceRow, int sourceCol) 
{ 
    // If source is one of the destinations 
    if ((sourceCol == 0 && sourceRow == 0) 
        || (sourceCol == col - 1 && sourceRow == 0) 
        || (sourceCol == 0 && sourceRow == row - 1) 
        || (sourceCol == col - 1 && sourceRow == row - 1)) 
        return 0; 

    // Set minimum value 
    int minFromSource = row * col; 

    // Precalculate minDistance of each grid with R * C 
    for (int i = 0; i < row; i++) 
        for (int j = 0; j < col; j++) 
            minDistance[i][j] = row * col; 

    // Insert source position in queue 
    que.push(make_pair(sourceRow, sourceCol)); 

    // Update minimum distance to visit source 
    minDistance[sourceRow][sourceCol] = 0; 

    // Set source to visited 
    visited[sourceRow][sourceCol] = 1; 

    // BFS approach for calculating the minDistance 
    // of each cell from source 
    while (!que.empty()) { 

        // Iterate over all four cells adjacent 
        // to current cell 
        pair<int, int> cell = que.front(); 

        // Initialize position of current cell 
        int cellRow = cell.first; 
        int cellCol = cell.second; 

        // Cell below the current cell 
        if (isValid(grid, cellRow + 1, cellCol)) { 

            // Push new cell to the queue 
            que.push(make_pair(cellRow + 1, cellCol)); 

            // Update one of its neightbor's distance 
            minDistance[cellRow + 1][cellCol] 
                = min(minDistance[cellRow + 1][cellCol], 
                      minDistance[cellRow][cellCol] + 1); 
            visited[cellRow + 1][cellCol] = 1; 
        } 

        // Above the current cell 
        if (isValid(grid, cellRow - 1, cellCol)) { 
            que.push(make_pair(cellRow - 1, cellCol)); 
            minDistance[cellRow - 1][cellCol] 
                = min(minDistance[cellRow - 1][cellCol], 
                      minDistance[cellRow][cellCol] + 1); 
            visited[cellRow - 1][cellCol] = 1; 
        } 

        // Right cell 
        if (isValid(grid, cellRow, cellCol + 1)) { 
            que.push(make_pair(cellRow, cellCol + 1)); 
            minDistance[cellRow][cellCol + 1] 
                = min(minDistance[cellRow][cellCol + 1], 
                      minDistance[cellRow][cellCol] + 1); 
            visited[cellRow][cellCol + 1] = 1; 
        } 

        // Left cell 
        if (isValid(grid, cellRow, cellCol - 1)) { 
            que.push(make_pair(cellRow, cellCol - 1)); 
            minDistance[cellRow][cellCol - 1] 
                = min(minDistance[cellRow][cellCol - 1], 
                      minDistance[cellRow][cellCol] + 1); 
            visited[cellRow][cellCol - 1] = 1; 
        } 

        // Pop the visited cell 
        que.pop(); 
    } 

    int i; 

    // Minimum distance to the corner 
    // of the first row, first column 
    minFromSource = min(minFromSource, 
                        minDistance[0][0]); 

    // Minimum distance to the corner 
    // of the last row, first column 
    minFromSource = min(minFromSource, 
                        minDistance[row - 1][0]); 

    // Minimum distance to the corner 
    // of the last row, last column 
    minFromSource = min(minFromSource, 
                        minDistance[row - 1][col - 1]); 

    // Minimum distance to the corner 
    // of the first row, last column 
    minFromSource = min(minFromSource, 
                        minDistance[0][col - 1]); 

    // If no path exists 
    if (minFromSource == row * col) 
        return -1; 

    // Return the minimum distance 
    return minFromSource; 
} 

// Driver code 
int main() 
{ 
    int sourceRow = 3, sourceCol = 3; 
    int grid[row][col] = { 1, 1, 1, 0, 0, 
                           0, 0, 1, 0, 1, 
                           0, 0, 1, 0, 1, 
                           1, 0, 0, 0, 1, 
                           1, 1, 0, 1, 0 }; 

    cout << minDistance(grid, sourceRow, sourceCol); 

    return 0; 
} 

```