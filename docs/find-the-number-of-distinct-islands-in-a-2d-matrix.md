# 找出 2D 矩阵中不同岛屿的数量

> 原文:[https://www . geeksforgeeks . org/find-2d 矩阵中不同岛屿的数量/](https://www.geeksforgeeks.org/find-the-number-of-distinct-islands-in-a-2d-matrix/)

给定一个布尔 2D 矩阵。任务是找出不同岛屿的数量，在这些岛屿上，一组相连的 1(水平或垂直)形成一个岛屿。当且仅当一个岛等于另一个岛(未旋转或反射)时，两个岛被认为是不同的。
**例:**

> **输入:**网格[][] =
> {{1，1，0，0，0}，
> 1，1，0，0，0}，
> 0，0，0，1，1}，
> 0，0，0，1，1，1}}
> **输出:** 1
> 左上角的岛 1，1 与右下角的岛 1，1 相同
> **输入:**网格[]=【T11 0，1，1}}
> **输出:** 3
> 上例中的不同岛屿为:左上角 1，1； 1，右上角 1，右下角 1。我们忽略左下角的岛 1，1，因为 1，1 与右上角相同。

**处理方式:**这个问题是问题[岛屿数量](https://www.geeksforgeeks.org/find-number-of-islands/)的延伸。
问题的核心是知道两个岛是否相等。主要标准是 1 的数量在两者中应该相同。但是这不是我们在上面的例子 2 中看到的唯一标准。那我们怎么知道呢？我们可以使用 1 的位置/坐标。
如果我们将任何岛屿的第一个坐标作为基点，然后从基点计算其他点的坐标，我们可以消除重复以获得岛屿的不同计数。因此，使用这种方法，上面示例 1 中的 2 个岛的坐标可以表示为:[(0，0)，(0，1)，(1，0)，(1，1)]。
**以下是上述方法的实施:**

## C++

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

## 蟒蛇 3

```
# Python implementation of above approach

# 2D array for the storing the horizontal and vertical
# directions. (Up, left, down, right
dirs = [ [ 0, -1 ],
        [ -1, 0 ],
        [ 0, 1 ],
        [ 1, 0 ] ]

# Function to perform dfs of the input grid
def dfs(grid, x0, y0, i, j, v):
    rows = len(grid)
    cols = len(grid[0])

    if i < 0 or i >= rows or j < 0 or j >= cols or grid[i][j] <= 0:
        return
    # marking the visited element as -1
    grid[i][j] *= -1

    # computing coordinates with x0, y0 as base
    v.append( (i - x0, j - y0) )

    # repeat dfs for neighbors
    for dir in dirs:
        dfs(grid, x0, y0, i + dir[0], j + dir[1], v)

# Main function that returns distinct count of islands in
# a given boolean 2D matrix
def countDistinctIslands(grid):
    rows = len(grid)
    if rows == 0:
        return 0

    cols = len(grid[0])
    if cols == 0:
        return 0

    coordinates = set()

    for i in range(rows):
        for j in range(cols):

            # If a cell is not 1
            # no need to dfs
            if grid[i][j] != 1:
                continue

            # to hold coordinates
            # of this island
            v = []
            dfs(grid, i, j, i, j, v)

            # insert the coordinates for
            # this island to set
            coordinates.add(tuple(v))

    return len(coordinates)

# Driver code
grid = [[ 1, 1, 0, 1, 1 ],
[ 1, 0, 0, 0, 0 ],
[ 0, 0, 0, 0, 1 ],
[ 1, 1, 0, 1, 1 ] ]

print("Number of distinct islands is", countDistinctIslands(grid))

# This code is contributed by ankush_953
```

**Output:** 

```
Number of distinct islands is 3
```

**时间复杂度:**O(row * cols)，其中 row 为矩阵中的行数，cols 为矩阵中的列数。
**空间复杂度:** O(行*列)