# 二进制矩阵中从任何 0 个单元到最近的 1 个单元的所有距离的最大值

> 原文:[https://www . geeksforgeeks . org/find-从二进制矩阵中的任意 0 个单元到最近的 1 个单元的最大距离/](https://www.geeksforgeeks.org/find-the-maximum-of-all-distances-to-the-nearest-1-cell-from-any-0-cell-in-a-binary-matrix/)

给定一个大小为 **N*N** 的[矩阵，其中填充了 **1** 和 **0** ，任务是找到从 0 像元到最近的 1 像元的最大距离。如果矩阵只有 0 或 1，返回-1。](https://www.geeksforgeeks.org/matrix/)

**注意:**矩阵中只允许水平和垂直移动。

**示例:**

```
Input: 
mat[][] = {{0, 1, 0},
           {0, 0, 1},
           {0, 0, 0}}
Output: 3
Explanation: 
Cell number (2, 0) is at the farthest
distance of 3 cells from both the
1-cells (0, 1) and (1, 2).

Input: 
mat[][] = {{1, 0, 0},
           {0, 0, 0},
           {0, 0, 0}}
Output: 4
Explanation: 
Cell number (2, 2) is at the farthest 
distance of 4 cells from the only 
1-cell (1, 1).
```

**方法 1:天真的方法**
对于每个 0 单元，计算它与每个 1 单元的距离，并存储最小值。所有这些最小距离中的最大值就是答案。

下面是上述方法的实现:

## C++

```
// C++ Program to find the maximum
// distance from a 0-cell to a 1-cell

#include <bits/stdc++.h>
using namespace std;

int maxDistance(vector<vector<int> >& grid)
{
    vector<pair<int, int> > one;

    int M = grid.size();
    int N = grid[0].size();
    int ans = -1;

    for (int i = 0; i < M; ++i) {
        for (int j = 0; j < N; ++j) {
            if (grid[i][j] == 1)
                one.emplace_back(i, j);
        }
    }

    // If the matrix consists of only 0's
    // or only 1's
    if (one.empty() || M * N == one.size())
        return -1;

    for (int i = 0; i < M; ++i) {
        for (int j = 0; j < N; ++j) {

            if (grid[i][j] == 1)
                continue;

            // If it's a 0-cell
            int dist = INT_MAX;
            for (auto& p : one) {

                // calculate its distance
                // with every 1-cell
                int d = abs(p.first - i)
                        + abs(p.second - j);

                // Compare and store the minimum
                dist = min(dist, d);

                if (dist <= ans)
                    break;
            }

            // Compare and store the maximum
            ans = max(ans, dist);
        }
    }
    return ans;
}

// Driver code
int main()
{
    vector<vector<int> > arr
        = { { 0, 0, 1 },
            { 0, 0, 0 },
            { 0, 0, 0 } };

    cout << maxDistance(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the maximum
// distance from a 0-cell to a 1-cell

import java.util.*;

class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
} 
static int maxDistance(int [][]grid)
{
    Vector<pair> one = new Vector<pair>();

    int M = grid.length;
    int N = grid[0].length;
    int ans = -1;

    for (int i = 0; i < M; ++i) {
        for (int j = 0; j < N; ++j) {
            if (grid[i][j] == 1)
                one.add(new pair(i, j));
        }
    }

    // If the matrix consists of only 0's
    // or only 1's
    if (one.isEmpty() || M * N == one.size())
        return -1;

    for (int i = 0; i < M; ++i) {
        for (int j = 0; j < N; ++j) {

            if (grid[i][j] == 1)
                continue;

            // If it's a 0-cell
            int dist = Integer.MAX_VALUE;
            for (pair p : one) {

                // calculate its distance
                // with every 1-cell
                int d = Math.abs(p.first - i)
                        + Math.abs(p.second - j);

                // Compare and store the minimum
                dist = Math.min(dist, d);

                if (dist <= ans)
                    break;
            }

            // Compare and store the maximum
            ans = Math.max(ans, dist);
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int [][]arr
        = { { 0, 0, 1 },
            { 0, 0, 0 },
            { 0, 0, 0 } };

    System.out.print(maxDistance(arr) +"\n");
}
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# distance from a 0-cell to a 1-cell
def maxDistance(grid):

  one = []
  M = len(grid)
  N = len(grid[0])
  ans = -1

  for i in range(M):
    for j in range(N):
      if (grid[i][j] == 1):
        one.append([i, j])

  # If the matrix consists of only 0's
  # or only 1's
  if (one == [] or M * N == len(one)):
    return -1

  for i in range(M):
    for j in range(N):
      if (grid[i][j] == 1):
        continue

      # If it's a 0-cell
      dist = float('inf')

      for p in one:

        # Calculate its distance
        # with every 1-cell
        d = abs(p[0] - i) + abs(p[1] - j)

        # Compare and store the minimum
        dist = min(dist, d)

        if (dist <= ans):
          break

        # Compare and store the maximum
        ans = max(ans, dist)

  return ans

# Driver code
arr = [ [ 0, 0, 1 ],
        [ 0, 0, 0 ],
        [ 0, 0, 0 ] ]

print(maxDistance(arr))

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program to find the maximum
// distance from a 0-cell to a 1-cell
using System;
using System.Collections.Generic;

class GFG{
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

static int maxDistance(int [,]grid)
{
    List<pair> one = new List<pair>();

    int M = grid.GetLength(0);
    int N = grid.GetLength(1);
    int ans = -1;

    for(int i = 0; i < M; ++i)
    {
       for(int j = 0; j < N; ++j)
       {
          if (grid[i, j] == 1)
              one.Add(new pair(i, j));
       }
    }

    // If the matrix consists of only 0's
    // or only 1's
    if (one.Count == 0 || M * N == one.Count)
        return -1;

    for(int i = 0; i < M; ++i)
    {
       for(int j = 0; j < N; ++j)
       {
          if (grid[i, j] == 1)
              continue;

          // If it's a 0-cell
          int dist = int.MaxValue;
          foreach (pair p in one)
          {

              // Calculate its distance
              // with every 1-cell
              int d = Math.Abs(p.first - i) +
                      Math.Abs(p.second - j);

              // Compare and store the minimum
              dist = Math.Min(dist, d);

              if (dist <= ans)
                  break;
          }

          // Compare and store the maximum
          ans = Math.Max(ans, dist);
       }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int [,]arr = { { 0, 0, 1 },
                   { 0, 0, 0 },
                   { 0, 0, 0 } };

    Console.Write(maxDistance(arr) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
4
```

**时间复杂度:** *O(M*N*P)* 其中网格大小为**M * N****P**为 1-细胞计数。
**辅助空间:** *O(P)*

**方法 2:使用**[**【BFS】**](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)
从一个 1 单元开始，执行[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)遍历，逐层进行。我们能检索到的最大层数就是我们的答案。

下面是上述方法的实现:

## C++

```
// C++ Program to find the maximum
// distance from a 0-cell to a 1-cell

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum distance
int maxDistance(vector<vector<int> >& grid)
{
    // Queue to store all 1-cells
    queue<pair<int, int> > q;

    // Grid dimensions
    int M = grid.size();
    int N = grid[0].size();
    int ans = -1;

    // Directions traversable from
    // a given a particular cell
    int dirs[4][2] = { { 0, 1 },
                       { 1, 0 },
                       { 0, -1 },
                       { -1, 0 } };

    for (int i = 0; i < M; ++i) {
        for (int j = 0; j < N; ++j) {
            if (grid[i][j] == 1)
                q.emplace(i, j);
        }
    }

    // If the grid contains
    // only 0s or only 1s
    if (q.empty() || M * N == q.size())
        return -1;

    while (q.size()) {

        int cnt = q.size();

        while (cnt--) {

            // Access every 1-cell
            auto p = q.front();
            q.pop();

            // Traverse all possible
            // directions from the cells
            for (auto& dir : dirs) {

                int x = p.first + dir[0];
                int y = p.second + dir[1];

                // Check if the cell is
                // within the boundaries
                // or contains a 1
                if (x < 0 || x >= M
                    || y < 0 || y >= N
                    || grid[x][y])
                    continue;

                q.emplace(x, y);
                grid[x][y] = 1;
            }
        }
        ++ans;
    }
    return ans;
}

// Driver code
int main()
{
    vector<vector<int> > arr = { { 0, 0, 1 },
                                 { 0, 0, 0 },
                                 { 0, 0, 1 } };

    cout << maxDistance(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// distance from a 0-cell to a 1-cell
import java.util.*;

class GFG{
static class pair
{
    int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find the maximum distance
static int maxDistance(int [][]grid)
{

    // Queue to store all 1-cells
    Queue<pair> q = new LinkedList<pair>();

    // Grid dimensions
    int M = grid.length;
    int N = grid[0].length;
    int ans = -1;

    // Directions traversable from
    // a given a particular cell
    int dirs[][] = { { 0, 1 },
                     { 1, 0 },
                     { 0, -1 },
                     { -1, 0 } };

    for(int i = 0; i < M; ++i)
    {
        for(int j = 0; j < N; ++j)
        {
            if (grid[i][j] == 1)
                q.add(new pair(i, j));
        }
    }

    // If the grid contains
    // only 0s or only 1s
    if (q.isEmpty() || M * N == q.size())
        return -1;

    while (q.size() > 0)
    {
        int cnt = q.size();
        while (cnt-->0)
        {

            // Access every 1-cell
            pair p = q.peek();
            q.remove();

            // Traverse all possible
            // directions from the cells
            for(int []dir : dirs)
            {
                int x = p.first + dir[0];
                int y = p.second + dir[1];

                // Check if the cell is
                // within the boundaries
                // or contains a 1
                if (x < 0 || x >= M ||
                    y < 0 || y >= N ||
                    grid[x][y] > 0)
                    continue;

                q.add(new pair(x, y));
                grid[x][y] = 1;
            }
        }
        ++ans;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int [][]arr = { { 0, 0, 1 },
                    { 0, 0, 0 },
                    { 0, 0, 1 } };

    System.out.print(maxDistance(arr) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# distance from a 0-cell to a 1-cell

# Function to find the maximum distance
def maxDistance(grid):

    # Queue to store all 1-cells
    q = []

    # Grid dimensions
    M = len(grid)
    N = len(grid[0])
    ans = -1

    # Directions traversable from
    # a given a particular cell
    dirs = [ [ 0, 1 ], [ 1, 0 ],
             [ 0, -1 ], [ -1, 0 ] ]

    for i in range(M):
        for j in range(N):
            if (grid[i][j] == 1):
                q.append([i, j])

    # If the grid contains
    # only 0s or only 1s
    if (len(q) == 0 or M * N == len(q)):
        return -1

    while (len(q) > 0):
        cnt = len(q)

        while (cnt > 0):

            # Access every 1-cell
            p = q[0]
            q.pop()

            # Traverse all possible
            # directions from the cells
            for Dir in dirs:
                x = p[0] + Dir[0]
                y = p[1] + Dir[1]

                # Check if the cell is
                # within the boundaries
                # or contains a 1
                if (x < 0 or x >= M or
                    y < 0 or y >= N or
                    grid[x][y]):
                    continue

                q.append([x, y])
                grid[x][y] = 1

            cnt -= 1

        ans += 2

    return ans

# Driver code   
arr = [ [ 0, 0, 1 ],
        [ 0, 0, 0 ],
        [ 0, 0, 1 ] ]

print(maxDistance(arr))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find
// the maximum distance
// from a 0-cell to a 1-cell
using System;
using System.Collections.Generic;
class GFG{

static int index = 0;
class pair
{
  public int first, second;
  public pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}

// Function to find the
// maximum distance
static int maxDistance(int [,]grid)
{
  // Queue to store all 1-cells
  Queue<pair> q = new Queue<pair>();

  // Grid dimensions
  int M = grid.GetLength(0);
  int N = grid.GetLength(1);
  int ans = -1;

  // Directions traversable from
  // a given a particular cell
  int [,]dirs = {{0, 1},
                 {1, 0},
                 {0, -1},
                 {-1, 0}};

  for(int i = 0; i < M; ++i)
  {
    for(int j = 0; j < N; ++j)
    {
      if (grid[i, j] == 1)
        q.Enqueue(new pair(i, j));
    }
  }

  // If the grid contains
  // only 0s or only 1s
  if (q.Count==0 || M * N == q.Count)
    return -1;

  while (q.Count > 0)
  {
    int cnt = q.Count;
    while (cnt-- > 0)
    {
      // Access every 1-cell
      pair p = q.Peek();
      q.Dequeue();

      // Traverse all possible
      // directions from the cells

      for(int i = 0; i < dirs.GetLength(0);)
      {
        int []dir = GetRow(dirs, i++);
        int x = p.first + dir[0];
        int y = p.second + dir[1];

        // Check if the cell is
        // within the boundaries
        // or contains a 1
        if (x < 0 || x >= M ||
            y < 0 || y >= N ||
            grid[x, y] > 0)
          continue;

        q.Enqueue(new pair(x, y));
        grid[x, y] = 1;
      }
    }
    ++ans;
  }
  return ans;
}

public static int[] GetRow(int[,] matrix,
                           int row)
{
  var rowLength = matrix.GetLength(1);
  var rowVector = new int[rowLength];

  for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];
  return rowVector;
}

// Driver code
public static void Main(String[] args)
{
  int [,]arr = {{0, 0, 1},
                {0, 0, 0},
                {0, 0, 1}};
  Console.Write(maxDistance(arr) + "\n");
}
}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
3
```

**时间复杂度:***O(M * N)*
T5】辅助空间: *O(M*N)*

**方法 3:使用** [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/)

*   不断更新已行驶的最大距离矩阵。
*   从矩阵左上角单元格 **(0，0)** 向右下角遍历。让网格[i][j]代表离左边或上面最近的 1-cell 的最大距离(当然也包括它本身)。
*   从右下到左上进行第二遍，更新网格数组，将单元格**网格【I】【j】**定义为**网格【I】【j】****网格【I+1】【j】**和**网格【I】【j+1】**的*最小值*。
*   在从右下到左上的遍历过程中跟踪最大值，并在最后返回该值。如果该值为 0，即网格仅填充 0 或 1，则返回-1。

下面是上述方法的实现:

## C++

```
// C++ Program to find the maximum
// distance from a 0-cell to a 1-cell

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum distance
int maxDistance(vector<vector<int> >& grid)
{
    if (!grid.size())
        return -1;
    int N = grid.size();

    int INF = 1000000;

    // DP matrix
    vector<vector<int> >
    dp(N, vector<int>(N, 0));

    grid[0][0] = grid[0][0] == 1
                     ? 0
                     : INF;

    // Set up top row and left column
    for (int i = 1; i < N; i++)
        grid[0][i] = grid[0][i] == 1
                         ? 0
                         : grid[0][i - 1] + 1;
    for (int i = 1; i < N; i++)
        grid[i][0] = grid[i][0] == 1
                         ? 0
                         : grid[i - 1][0] + 1;

    // Pass one: top left to bottom right
    for (int i = 1; i < N; i++) {
        for (int j = 1; j < N; j++) {
            grid[i][j] = grid[i][j] == 1
                             ? 0
                             : min(grid[i - 1][j],
                                   grid[i][j - 1])
                                   + 1;
        }
    }

    // Check if there was no "One" Cell
    if (grid[N - 1][N - 1] >= INF)
        return -1;

    // Set up top row and left column
    int maxi = grid[N - 1][N - 1];
    for (int i = N - 2; i >= 0; i--) {
        grid[N - 1][i]
            = min(grid[N - 1][i],
                  grid[N - 1][i + 1] + 1);
        maxi = max(grid[N - 1][i], maxi);
    }

    for (int i = N - 2; i >= 0; i--) {
        grid[i][N - 1]
            = min(grid[i][N - 1],
                  grid[i + 1][N - 1] + 1);
        maxi = max(grid[i][N - 1], maxi);
    }

    // Past two: bottom right to top left
    for (int i = N - 2; i >= 0; i--) {
        for (int j = N - 2; j >= 0; j--) {
            grid[i][j] = min(grid[i][j],
                             min(grid[i + 1][j] + 1,
                                 grid[i][j + 1] + 1));
            maxi = max(grid[i][j], maxi);
        }
    }

    return !maxi ? -1 : maxi;
}

// Driver code
int main()
{
    vector<vector<int> > arr = { { 0, 0, 1 },
                                 { 0, 0, 0 },
                                 { 0, 0, 0 } };

    cout << maxDistance(arr) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// distance from a 0-cell to a 1-cell
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the maximum distance
static int maxDistance(int[][] grid)
{
    if (grid.length == 0)
        return -1;

    int N = grid.length;
    int INF = 1000000;

    grid[0][0] = grid[0][0] == 1 ? 0 : INF;

    // Set up top row and left column
    for(int i = 1; i < N; i++)
        grid[0][i] = grid[0][i] == 1 ? 0 :
                     grid[0][i - 1] + 1;

    for(int i = 1; i < N; i++)
        grid[i][0] = grid[i][0] == 1 ? 0 :
                     grid[i - 1][0] + 1;

    // Pass one: top left to bottom right
    for(int i = 1; i < N; i++)
    {
        for(int j = 1; j < N; j++)
        {
            grid[i][j] = grid[i][j] == 1 ? 0 :
                Math.min(grid[i - 1][j],
                         grid[i][j - 1]) + 1;
        }
    }

    // Check if there was no "One" Cell
    if (grid[N - 1][N - 1] >= INF)
        return -1;

    // Set up top row and left column
    int maxi = grid[N - 1][N - 1];
    for(int i = N - 2; i >= 0; i--)
    {
        grid[N - 1][i] = Math.min(
            grid[N - 1][i],
            grid[N - 1][i + 1] + 1);

        maxi = Math.max(grid[N - 1][i], maxi);
    }

    for(int i = N - 2; i >= 0; i--)
    {
        grid[i][N - 1] = Math.min(
            grid[i][N - 1],
            grid[i + 1][N - 1] + 1);

        maxi = Math.max(grid[i][N - 1], maxi);
    }

    // Past two: bottom right to top left
    for(int i = N - 2; i >= 0; i--)
    {
        for(int j = N - 2; j >= 0; j--)
        {
            grid[i][j] = Math.min(
                grid[i][j],
                Math.min(grid[i + 1][j] + 1,
                         grid[i][j + 1] + 1));

            maxi = Math.max(grid[i][j], maxi);
        }
    }

    return maxi == 0 ? -1 : maxi;
}

// Driver code
public static void main(String[] args)
{
    int[][] arr = { { 0, 0, 1 },
                    { 0, 0, 0 },
                    { 0, 0, 0 } };

    System.out.println(maxDistance(arr));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# distance from a 0-cell to a 1-cell

# Function to find the maximum distance
def maxDistance(grid):

    if (len(grid) == 0):
        return -1

    N = len(grid)
    INF = 1000000

    if grid[0][0] == 1:
        grid[0][0] = 0
    else:
        grid[0][0] = INF

    # Set up top row and left column
    for i in range(1, N):
        if grid[0][i] == 1:
            grid[0][i] = 0
        else:
            grid[0][i] = grid[0][i - 1] + 1

    for i in range(1, N):
        if grid[i][0] == 1:
            grid[i][0] = 0
        else:
            grid[i][0] = grid[i - 1][0] + 1

    # Pass one: top left to bottom right
    for i in range(1, N):
        for j in range(1, N):
            if grid[i][j] == 1:
                grid[i][j] = 0
            else:
                grid[i][j] = min(grid[i - 1][j],
                                 grid[i][j - 1] + 1)

    # Check if there was no "One" Cell
    if (grid[N - 1][N - 1] >= INF):
        return -1

    # Set up top row and left column
    maxi = grid[N - 1][N - 1]

    for i in range(N - 2, -1, -1):
        grid[N - 1][i] = min(grid[N - 1][i],
                             grid[N - 1][i + 1] + 1)

        maxi = max(grid[N - 1][i], maxi)

    for i in range(N - 2, -1, -1):
        grid[i][N - 1] = min(grid[i][N - 1],
                             grid[i + 1][N - 1] + 1)

        maxi = max(grid[i][N - 1], maxi + 1)

    # Past two: bottom right to top left
    for i in range(N - 2, -1, -1):
        for j in range(N - 2, -1, -1):
            grid[i][j] = min(grid[i][j],
                             min(grid[i + 1][j] + 1,
                                 grid[i][j + 1] + 1))

            maxi = max(grid[i][j], maxi)

    if maxi == 0:
        return -1
    else:
        return maxi

# Driver code       
arr = [ [ 0, 0, 1 ], [ 0, 0, 0 ], [ 0, 0, 0 ] ]

print(maxDistance(arr))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find the maximum
// distance from a 0-cell to a 1-cell
using System;
class GFG {

    // Function to find the maximum distance
    static int maxDistance(int[, ] grid)
    {
        if (grid.GetLength(0) == 0)
            return -1;

        int N = grid.GetLength(0);
        int INF = 1000000;

        grid[0, 0] = grid[0, 0] == 1 ? 0 : INF;

        // Set up top row and left column
        for (int i = 1; i < N; i++)
            grid[0, i]
                = grid[0, i] == 1 ? 0 : grid[0, i - 1] + 1;

        for (int i = 1; i < N; i++)
            grid[i, 0]
                = grid[i, 0] == 1 ? 0 : grid[i - 1, 0] + 1;

        // Pass one: top left to bottom right
        for (int i = 1; i < N; i++) {
            for (int j = 1; j < N; j++) {
                grid[i, j] = grid[i, j] == 1
                                 ? 0
                                 : Math.Min(grid[i - 1, j],
                                            grid[i, j - 1])
                                       + 1;
            }
        }

        // Check if there was no "One" Cell
        if (grid[N - 1, N - 1] >= INF)
            return -1;

        // Set up top row and left column
        int maxi = grid[N - 1, N - 1];
        for (int i = N - 2; i >= 0; i--) {
            grid[N - 1, i] = Math.Min(
                grid[N - 1, i], grid[N - 1, i + 1] + 1);

            maxi = Math.Max(grid[N - 1, i], maxi);
        }

        for (int i = N - 2; i >= 0; i--) {
            grid[i, N - 1] = Math.Min(
                grid[i, N - 1], grid[i + 1, N - 1] + 1);

            maxi = Math.Max(grid[i, N - 1], maxi);
        }

        // Past two: bottom right to top left
        for (int i = N - 2; i >= 0; i--) {
            for (int j = N - 2; j >= 0; j--) {
                grid[i, j] = Math.Min(
                    grid[i, j],
                    Math.Min(grid[i + 1, j] + 1,
                             grid[i, j + 1] + 1));

                maxi = Math.Max(grid[i, j], maxi);
            }
        }

        return maxi == 0 ? -1 : maxi;
    }

    // Driver code
    public static void Main()
    {
        int[, ] arr
            = { { 0, 0, 1 }, { 0, 0, 0 }, { 0, 0, 0 } };

        Console.WriteLine(maxDistance(arr));
    }
}

// This code is contributed by subhammahato348
```

**Output**

```
4
```

**时间复杂度:***O(M * N)*
T5】辅助空间: *O(1)*