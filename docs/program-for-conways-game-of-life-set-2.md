# 康威人生游戏节目|第二集

> 原文:[https://www . geesforgeks . org/program-for-Conway-游戏人生-set-2/](https://www.geeksforgeeks.org/program-for-conways-game-of-life-set-2/)

给定大小为 **N*M** 的二进制**网格[ ][ ]** ，每个单元包含 0 或 1，其中 1 代表**活单元**，0 代表**死单元**。任务是根据以下规则生成下一代单元格:

1.  任何少于两个活邻居的活细胞都会因人口不足而死亡。
2.  任何有两三个活邻居的活细胞都会延续到下一代。
3.  任何有三个以上活邻居的活细胞都会因人口过多而死亡。
4.  任何正好有三个活邻居的死细胞通过繁殖变成活细胞。

这里，一个小区的**邻居**包括其相邻小区以及对角小区，因此对于每个小区，总共有 **8 个**邻居。
**例:**

> **输入:** N = 5，M = 10
> 0000000000
> 00011000000
> 00001000000
> 000000000
> 000000000
> T8】输出:T10】0000000000
> 00011000000
> 00000
> 位于(2，3)的细胞死亡了，正好有 3 个邻居，
> 所以，根据规则 4，它变成了活细胞。
> **输入:** N = 4，M = 5
> 00000
> 01100
> 00010
> 00000
> T30】输出:
> 00000
> 00100
> 00100
> 00000
> T37】解释:
> 在(1，1
> 在(1，2)的细胞是活的，有 2 个邻居，
> 所以，根据规则 2，它活到了下一代。
> 位于(2，2)的细胞死亡，正好有 3 个邻居，
> 所以，根据规则 4，它变成了活细胞。

**天真的方法:**
我们已经在[康威人生游戏节目|第一集](https://www.geeksforgeeks.org/program-for-conways-game-of-life/)中讨论过解决这个问题的方法。在这种方法中，创建了一个额外的网格 **future[ ][ ]** ，其大小为 **N*M** ，用于存储下一代细胞。
***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*
**高效途径:**
A *空间优化的*途径对于这个问题是可能的，它不使用额外的空间。对于每个**活动单元**，每次我们遇到它的活动邻居时，将其值增加 1。并且，对于每一个**死亡细胞**，每次我们遇到它的活邻居时，将其值减 1。现在，如果一个单元格中的值小于 0，则表示它是一个死单元格，如果该值大于 0，则表示它是一个活单元格，同样一个单元格中值的**大小**将表示它的活邻居的**数量。这样，将不需要额外的网格，并且获得空间优化的解决方案。该方法的详细步骤如下:
对于当前的网格位置，我们将查看所有的邻居。**

1.  遍历整个网格。
2.  如果邻居的值为 **> = 1** (即邻居的初始值为 1)
    *   如果当前单元格为 **> = 1** ，则**将当前单元格值增加 1。
        现在，网格[ i ][ j ] > 0 将意味着初始网格[ i ][ j ] == 1。**
    *   否则，当前单元格为 **< = 0** ，只是**将当前单元格值减**1。
        现在，网格[ i ][ j ] < = 0 将意味着初始网格[ i ][ j ] == 0。
3.  现在，使用修改后的网格生成所需的新一代网格。
    *   如果当前单元格值为 **> 0** ，则有 3 种可能的情况:
        *   如果该值小于 3，则将其更改为 0。
        *   否则，如果值< = 4，则将其更改为 1。
        *   否则将该值更改为 0。
    *   否则，当前单元格值为 **< = 0** 。
        *   如果值为 3，则将其更改为 1。
        *   否则将其更改为 0。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

void print(vector<vector<int>> grid)
{
    int p = grid.size(),
    q = grid[0].size();

    for (int i = 0; i < p; i++) {
      for (int j = 0; j < q; j++) {

        cout << grid[i][j];
     }
    cout << endl;
    }
}       
// Function to check if
// index are not out of grid
static bool save(vector<vector<int> > grid,int row, int col)
{
    return (grid.size() > row && grid[0].size() > col && row >= 0 && col >= 0);
}
    // Function to get New Generation
void solve(vector<vector<int> >& grid)
{
      int p = grid.size(),
        q = grid[0].size();
      int u[] = { 1, -1, 0, 1, -1, 0, 1, -1 };
      int v[] = { 0, 0, -1, -1, -1, 1, 1, 1 };
     for (int i = 0; i < p; i++)
     {
      for (int j = 0; j < q; j++)
      {
      // IF the initial value
      // of the grid(i, j) is 1
      if (grid[i][j] > 0)
      {
        for (int k = 0; k < 8; k++)
        {
          if (save(grid, i + u[k],
                   j + v[k]) &&
                   grid[i + u[k]][j + v[k]] > 0)
          {
            // If initial value > 0,
            // just increment it by 1
            grid[i][j]++;
          }
        }
      }

      // IF the initial value
      // of the grid(i, j) is 0
      else
      {
         for (int k = 0; k < 8; k++)
         {
           if (save(grid, i + u[k],
                   j + v[k]) &&
                   grid[i + u[k]][j + v[k]] > 0)
              {
                // If initial value <= 0
                // just decrement it by 1
                grid[i][j]--;
              }
           }
        }
      }
    }

    // Generating new Generation.
    // Now the magnitude of the
    // grid will represent number
    // of neighbours
    for (int i = 0; i < p; i++)
      {
          for (int j = 0; j < q; j++)
         {
        // If initial value was 1.
        if (grid[i][j] > 0)
        {
            // Since Any live cell with
          // < 2 live neighbors dies
           if (grid[i][j] < 3)
              grid[i][j] = 0;

             // Since Any live cell with
            // 2 or 3 live neighbors live
           else if (grid[i][j] <= 4)
            grid[i][j] = 1;

            // Since Any live cell with
             // > 3 live neighbors dies
            else if (grid[i][j] > 4)
              grid[i][j] = 0;
        }
       else
        {
        // Since Any dead cell with
        // exactly 3 live neighbors
        // becomes a live cell
         if (grid[i][j] == -3)
              grid[i][j] = 1;
         else
              grid[i][j] = 0;
            }
        }
     }
}
// Driver code
int main ()
{
  vector<vector<int>> grid = {{0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 1, 1,
                   0,0, 0, 0, 0},
                  {0, 0, 0, 0, 1,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0}};

  // Function to generate
  // New Generation inplace
  solve(grid);

  // Displaying the grid
  print(grid);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
import java.lang.*;
class GFG{

static void print(int[][] grid)
{
  int p = grid.length,
  q = grid[0].length;

  for (int i = 0; i < p; i++)
  {
    for (int j = 0; j < q; j++)
    {
      System.out.print(grid[i][j]);
    }
    System.out.println();;
  }
}

static boolean save(int[][] grid,
                    int row, int col)
{
  return (grid.length > row &&
          grid[0].length > col &&
          row >= 0 && col >= 0);
}

static void solve(int[][] grid)
{
  int p = grid.length,
  q = grid[0].length;

  // Possible neighboring
  // indexes
  int u[] = {1, -1, 0, 1,
             -1, 0, 1, -1};
  int v[] = {0, 0, -1, -1,
             -1, 1, 1, 1};

  for (int i = 0; i < p; i++)
  {
    for (int j = 0; j < q; j++)
    {
      // IF the initial value
      // of the grid(i, j) is 1
      if (grid[i][j] > 0)
      {
        for (int k = 0; k < 8; k++)
        {
          if (save(grid, i + u[k],
                   j + v[k]) &&
                   grid[i + u[k]][j + v[k]] > 0)
          {
            // If initial value > 0,
            // just increment it by 1
            grid[i][j]++;
          }
        }
      }

      // IF the initial value
      // of the grid(i, j) is 0
      else
      {
        for (int k = 0; k < 8; k++)
        {
          if (save(grid, i + u[k],
                   j + v[k]) &&
                   grid[i + u[k]][j + v[k]] > 0)
          {
            // If initial value <= 0
            // just decrement it by 1
            grid[i][j]--;
          }
        }
      }
    }
  }

  // Generating new Generation.
  // Now the magnitude of the
  // grid will represent number
  // of neighbours
  for (int i = 0; i < p; i++)
  {
    for (int j = 0; j < q; j++)
    {
      // If initial value was 1.
      if (grid[i][j] > 0)
      {
        // Since Any live cell with
        // < 2 live neighbors dies
        if (grid[i][j] < 3)
          grid[i][j] = 0;

        // Since Any live cell with
        // 2 or 3 live neighbors live
        else if (grid[i][j] <= 4)
          grid[i][j] = 1;

        // Since Any live cell with
        // > 3 live neighbors dies
        else if (grid[i][j] > 4)
          grid[i][j] = 0;
      }
      else
      {
        // Since Any dead cell with
        // exactly 3 live neighbors
        // becomes a live cell
        if (grid[i][j] == -3)
          grid[i][j] = 1;
        else
          grid[i][j] = 0;
      }
    }
  }
}

// Driver code
public static void main (String[] args)
{
  int[][] grid = {{0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 1, 1,
                   0,0, 0, 0, 0},
                  {0, 0, 0, 0, 1,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0},
                  {0, 0, 0, 0, 0,
                   0, 0, 0, 0, 0}};

  // Function to generate
  // New Generation inplace
  solve(grid);

  // Displaying the grid
  print(grid);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

def print2dArr(grid):
    p = len(grid)
    q = len(grid[0])

    for i in range(p):
        for j in range(q):
            print(grid[i][j], end='')

        print()

# Function to check if
# index are not out of grid
def save(grid, row, col):
    return (len(grid) > row and len(grid[0]) > col and row >= 0 and col >= 0)

# Function to get New Generation

def solve(grid):
    p = len(grid)
    q = len(grid[0])
    u = [1, -1, 0, 1, -1, 0, 1, -1]
    v = [0, 0, -1, -1, -1, 1, 1, 1]
    for i in range(p):
        for j in range(q):
            # IF the initial value
            # of the grid(i, j) is 1
            if (grid[i][j] > 0):
                for k in range(8):
                    if (save(grid, i + u[k], j + v[k]) and grid[i + u[k]][j + v[k]] > 0):
                        # If initial value > 0,
                        # just increment it by 1
                        grid[i][j] += 1

            # IF the initial value
            # of the grid(i, j) is 0
            else:
                for k in range(8):
                    if (save(grid, i + u[k], j + v[k]) and grid[i + u[k]][j + v[k]] > 0):
                        # If initial value <= 0
                        # just decrement it by 1
                        grid[i][j] -= 1
    # Generating new Generation.
    # Now the magnitude of the
    # grid will represent number
    # of neighbours
    for i in range(p):
        for j in range(q):
            # If initial value was 1.
            if (grid[i][j] > 0):
                # Since Any live cell with
                # < 2 live neighbors dies
                if (grid[i][j] < 3):
                    grid[i][j] = 0

                # Since Any live cell with
                # 2 or 3 live neighbors live
                elif (grid[i][j] <= 4):
                    grid[i][j] = 1

                # Since Any live cell with
                # > 3 live neighbors dies
                elif (grid[i][j] > 4):
                    grid[i][j] = 0

            else:
                # Since Any dead cell with
                # exactly 3 live neighbors
                # becomes a live cell
                if (grid[i][j] == -3):
                    grid[i][j] = 1
                else:
                    grid[i][j] = 0

# Driver code
if __name__ == '__main__':
    grid = [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ],
            [0, 0, 0, 1, 1, 0, 0, 0, 0, 0, ],
            [0, 0, 0, 0, 1, 0, 0, 0, 0, 0, ],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ],
            [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, ], ]

    # Function to generate
    # New Generation inplace
    solve(grid)

    # Displaying the grid
    print2dArr(grid)
```

**Output:** 

```
0000000000
0001100000
0001100000
0000000000
0000000000
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*