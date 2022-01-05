# 检查方向矩阵中给定单元之间是否存在有效路径

> 原文:[https://www . geesforgeks . org/check-如果给定方向矩阵中的单元之间存在有效路径/](https://www.geeksforgeeks.org/check-if-a-valid-path-exists-between-given-cells-in-a-directional-matrix/)

给定一个**N×M**矩阵。矩阵的每个单元都有一个指向下一个单元的**数值**。矩阵[i][j]的值可以是:

*   **1** 表示去**右边的牢房**。(即从矩阵[i][j]到矩阵[i][j + 1])
*   **2** 表示去**左边的牢房**。(即从矩阵[i][j]到矩阵[I][j–1])
*   **3** 表示转到**下**单元。(即从矩阵[i][j]到矩阵[i + 1][j])
*   **4** 表示转到**上层**细胞。(即从矩阵[i][j]转到矩阵[I–1][j])

**给出源**小区(x1，y1)和**目的地**小区(x2，y2)。任务是找出给定源单元格和目标单元格之间是否存在路径。

**示例**:

> **输入**:矩阵[][] = {{3，2，2，2}，{3，4，2，3}，{1，3，4，4}，{2，1，1，2}，{4，4，3，3}，源单元格= {0，3}，目标单元格= {3，1}
> **输出**:是
> 
> <figure class="table">
> 
> | three | Two | Two | Two |
> | three | four | Two | three |
> | one | three | four | four |
> | Two | one | one | Two |
> | four | four | three | three |
> 
> </figure>
> 
> **说明**:从单元格(0，3)开始，按照基于方向规则的路径。按照以下顺序遍历单元格:(0，3)- > (0，2)- > (0，1)- > (0，0)- > (1，0)- > (2，0)- > (2，1)- > (3，1)哪个是目的地。
> 
> **输入**:矩阵[][]={{1，4，3}，{2，3，2}，{4，1，4}}，源单元格= {1，1}，目标单元格= {0，3}
> **输出**:否
> 
> <figure class="table">
> 
> | one | four | three |
> | Two | three | Two |
> | four | one | four |
> 
> **说明**:从单元格(1，1)开始，按照基于方向规则的路径。遍历单元格为:(1，1)- > (2，1)- > (2，2)- > (1，2)- > (1，1)，这里再次访问源单元格，因此在任何情况下都不访问目标单元格。
> 
> </figure>

**接近**:可以使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 或者 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 解决任务。

*   可以观察到要遵循的路径是**固定的**，我们需要根据指定的**方向**规则遍历矩阵。
*   从源单元格启动 DFS 或 BFS，并根据上述**方向**规则**移动**。
*   如果到达目标小区，则找到一条**有效的**路径。
*   如果某个**访问的**小区再次**重访**或者当前小区的索引超出了的范围**，则该路径无法到达目的小区，否则继续。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a valid path
// exists or not
bool uniquepath(vector<vector<int> >& matrix, int curr_x,
                int curr_y, int dest_x, int dest_y,
                vector<vector<bool> >& visited)
{
    // Check if destination cell is reached
    if (curr_x == dest_x && curr_y == dest_y)
        return true;

    // Base Cases
    if (!(curr_x >= 0 && curr_x < matrix.size()
          && curr_y >= 0 && curr_y < matrix[0].size()))
        return false;

    // Check whether a visited cell is
    // re-visited again
    if (visited[curr_x][curr_y] == true)
        return false;

    // Mark current cell as visited
    visited[curr_x][curr_y] = true;

    // Moving based on direction rule
    if (matrix[curr_x][curr_y] == 1)
        return uniquepath(matrix, curr_x, curr_y + 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 2)
        return uniquepath(matrix, curr_x, curr_y - 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 3)
        return uniquepath(matrix, curr_x + 1, curr_y,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 4)
        return uniquepath(matrix, curr_x - 1, curr_y,
                          dest_x, dest_y, visited);
}

// Driver code
int main()
{
    vector<vector<int> > matrix = { { 3, 2, 2, 2 },
                                    { 3, 4, 2, 3 },
                                    { 1, 3, 4, 4 },
                                    { 2, 1, 1, 2 },
                                    { 4, 4, 1, 2 } };
    int start_x = 0, start_y = 3;
    int dest_x = 3, dest_y = 1;
    int n = matrix.size();
    int m = matrix[0].size();
    vector<vector<bool> > visited(
        n,
        vector<bool>(m, false));
    if (uniquepath(matrix, start_x, start_y,
                   dest_x, dest_y,
                   visited))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check whether a valid path
// exists or not
static boolean uniquepath(int[][]matrix, int curr_x,
                          int curr_y, int dest_x,
                          int dest_y, boolean[][] visited)
{

    // Check if destination cell is reached
    if (curr_x == dest_x && curr_y == dest_y)
        return true;

    // Base Cases
    if (!(curr_x >= 0 && curr_x < matrix.length &&
          curr_y >= 0 && curr_y < matrix[0].length))
        return false;

    // Check whether a visited cell is
    // re-visited again
    if (visited[curr_x][curr_y] == true)
        return false;

    // Mark current cell as visited
    visited[curr_x][curr_y] = true;

    // Moving based on direction rule
    if (matrix[curr_x][curr_y] == 1)
        return uniquepath(matrix, curr_x, curr_y + 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 2)
        return uniquepath(matrix, curr_x, curr_y - 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 3)
        return uniquepath(matrix, curr_x + 1, curr_y,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x][curr_y] == 4)
        return uniquepath(matrix, curr_x - 1, curr_y,
                          dest_x, dest_y, visited);

    return false;
}

// Driver code
public static void main(String[] args)
{
    int[][] matrix = { { 3, 2, 2, 2 },
                       { 3, 4, 2, 3 },
                       { 1, 3, 4, 4 },
                       { 2, 1, 1, 2 },
                       { 4, 4, 1, 2 } };

    int start_x = 0, start_y = 3;
    int dest_x = 3, dest_y = 1;
    int n = matrix.length;
    int m = matrix[0].length;

    boolean[][] visited = new boolean[n][m];
    if (uniquepath(matrix, start_x, start_y,
                   dest_x, dest_y, visited))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

# Function to check whether a valid path
# exists or not
def uniquepath(matrix, curr_x, curr_y, dest_x, dest_y, visited):

    # Check if destination cell is reached
    if (curr_x == dest_x and curr_y == dest_y):
        return True

    # Base Cases
    if (not(curr_x >= 0 and curr_x < len(matrix) and curr_y >= 0 and curr_y < len(matrix[0]))):
        return False

    # Check whether a visited cell is
    # re-visited again
    if (visited[curr_x][curr_y] == True):
        return False

    # Mark current cell as visited
    visited[curr_x][curr_y] = True

    # Moving based on direction rule
    if (matrix[curr_x][curr_y] == 1):
        return uniquepath(matrix, curr_x, curr_y + 1, dest_x, dest_y, visited)
    elif (matrix[curr_x][curr_y] == 2):
        return uniquepath(matrix, curr_x, curr_y - 1, dest_x, dest_y, visited)
    elif (matrix[curr_x][curr_y] == 3):
        return uniquepath(matrix, curr_x + 1, curr_y, dest_x, dest_y, visited)
    elif (matrix[curr_x][curr_y] == 4):
        return uniquepath(matrix, curr_x - 1, curr_y, dest_x, dest_y, visited)

# Driver code
if __name__ == "__main__":

    matrix = [[3, 2, 2, 2],
              [3, 4, 2, 3],
              [1, 3, 4, 4],
              [2, 1, 1, 2],
              [4, 4, 1, 2]
              ]
    start_x = 0
    start_y = 3
    dest_x = 3
    dest_y = 1
    n = len(matrix)
    m = len(matrix[0])
    visited = [[False for _ in range(m)] for _ in range(n)]
    if (uniquepath(matrix, start_x, start_y, dest_x, dest_y, visited)):
        print("Yes")
    else:
        print("No")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to check whether a valid path
// exists or not
static bool uniquepath(int[,]matrix, int curr_x,
                          int curr_y, int dest_x,
                          int dest_y, bool[,] visited)
{

    // Check if destination cell is reached
    if (curr_x == dest_x && curr_y == dest_y)
        return true;

    // Base Cases
    if (!(curr_x >= 0 && curr_x < matrix.GetLength(0) &&
          curr_y >= 0 && curr_y < matrix.GetLength(1)))
        return false;

    // Check whether a visited cell is
    // re-visited again
    if (visited[curr_x,curr_y] == true)
        return false;

    // Mark current cell as visited
    visited[curr_x,curr_y] = true;

    // Moving based on direction rule
    if (matrix[curr_x,curr_y] == 1)
        return uniquepath(matrix, curr_x, curr_y + 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x,curr_y] == 2)
        return uniquepath(matrix, curr_x, curr_y - 1,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x,curr_y] == 3)
        return uniquepath(matrix, curr_x + 1, curr_y,
                          dest_x, dest_y, visited);
    else if (matrix[curr_x,curr_y] == 4)
        return uniquepath(matrix, curr_x - 1, curr_y,
                          dest_x, dest_y, visited);

    return false;
}

// Driver code
public static void Main(String[] args)
{
    int[,] matrix = { { 3, 2, 2, 2 },
                       { 3, 4, 2, 3 },
                       { 1, 3, 4, 4 },
                       { 2, 1, 1, 2 },
                       { 4, 4, 1, 2 } };

    int start_x = 0, start_y = 3;
    int dest_x = 3, dest_y = 1;
    int n = matrix.GetLength(0);
    int m = matrix.GetLength(1);

    bool[,] visited = new bool[n,m];
    if (uniquepath(matrix, start_x, start_y,
                   dest_x, dest_y, visited))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check whether a valid path
// exists or not
function uniquepath(matrix, curr_x, curr_y, dest_x, dest_y, visited)
{

  // Check if destination cell is reached
  if (curr_x == dest_x && curr_y == dest_y) return true;

  // Base Cases
  if (
    !(
      curr_x >= 0 &&
      curr_x < matrix.length &&
      curr_y >= 0 &&
      curr_y < matrix[0].length
    )
  )
    return false;

  // Check whether a visited cell is
  // re-visited again
  if (visited[curr_x][curr_y] == true) return false;

  // Mark current cell as visited
  visited[curr_x][curr_y] = true;

  // Moving based on direction rule
  if (matrix[curr_x][curr_y] == 1)
    return uniquepath(matrix, curr_x, curr_y + 1, dest_x, dest_y, visited);
  else if (matrix[curr_x][curr_y] == 2)
    return uniquepath(matrix, curr_x, curr_y - 1, dest_x, dest_y, visited);
  else if (matrix[curr_x][curr_y] == 3)
    return uniquepath(matrix, curr_x + 1, curr_y, dest_x, dest_y, visited);
  else if (matrix[curr_x][curr_y] == 4)
    return uniquepath(matrix, curr_x - 1, curr_y, dest_x, dest_y, visited);
}

// Driver code

let matrix = [
  [3, 2, 2, 2],
  [3, 4, 2, 3],
  [1, 3, 4, 4],
  [2, 1, 1, 2],
  [4, 4, 1, 2],
];
let start_x = 0,
  start_y = 3;
let dest_x = 3,
  dest_y = 1;
let n = matrix.length;
let m = matrix[0].length;

let visited = new Array(n).fill(0).map(() => new Array(m).fill(false));
if (uniquepath(matrix, start_x, start_y, dest_x, dest_y, visited))
  document.write("Yes");
else document.write("No");

// This code is contributed by gfgking.
</script>
```

**Output**

```
Yes
```

***时间复杂度*** : O(n*m)
***辅助空间*** : O(n*m)