# 检查值为 1 的单元格是否在到达值为 2 的任何单元格之前到达矩阵右下角的路径

> 原文： [https://www.geeksforgeeks.org/check-if-a-path-exists-for-a-cell-valued-1-to-reach-the-bottom-right-corner-of-a-matrix-before-any-cell-valued-2/](https://www.geeksforgeeks.org/check-if-a-path-exists-for-a-cell-valued-1-to-reach-the-bottom-right-corner-of-a-matrix-before-any-cell-valued-2/)

给定尺寸为`N * M`的矩阵`arr[][]`，其元素为`0`，`1`和`2`。 矩阵中只有一个值`1`的单元格。 任务是检查`1`是否有可能在值`2`的任何单元格之前到达右下角，或者不使用以下操作：

*  `2`可以在 1 个单位时间内在所有四个方向上复制 1 个单位。

*  `1`仅可以在所有四个方向中的一个方向上移动，前提是该位置的元素为`0`。

如果值`1`的单元格比任何值`2`的单元格在少于或相等的时间内到达右下角，请打印`Yes`。 否则，打印`No`。

**示例**：

> **输入**：`N = 3, M = 3, arr[][] = {{0, 2, 0}, {0, 1, 0}, {0, 0, 0}}`
>
> **输出**：`Yes`
>
> **说明**：
>
> 1 可以移动 2 步到右下角 ，`2`可以移动 3 步到右下角。
>
> 由于值 1 的单元格比值 2 的单元格先到达。因此，打印是。
> 
> **输入**：`N = 3, M = 3, arr[][] = {{0, 2, 0}, {0, 1, 0}, {0, 2, 0}}`
>
> **输出**：`No`
>
> **说明**：
>
> 1 可以移动 2 步到右下角，而单元格最后一行的 2 可以移动 1 步到右下角。
>
> 因为值 2 的单元格比值 1 的单元格先到达。因此，打印`No`。

**方法**：这个想法是使用[多源 BFS](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/) 。 要执行多源 BFS 遍历，请按指定顺序以[双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)将矩阵中存在的`1`和`2`的所有位置相加。 通过弹出添加的位置并添加尚未访问的相邻位置，对该出队执行 [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。 请按照以下步骤解决问题：

1.  为多源 BFS 创建双端队列。

2.  首先，在前面添加`1`的位置，然后在后面添加`2`的位置。 这是因为如果`1`和`2`同时到达右下角，则`1`被认为比`2`高。

3.  从出队队列的前面弹出元素，直到出队队列为空，然后执行以下操作：

    *   如果弹出位置已被访问，则继续下一个位置。

    *   如果没有访问该位置，请检查该位置是否在右下角，以及检查其中的元素是否为`1`。 如果发现是真的，则打印**是**。

    *   否则，对于所有四个方向，将当前位置插入**出队**中。

4.  完成上述操作后，如果未找到值`1`的单元到达右下位置，则打印 **No** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if cell with
// value 1 doesn't reaches the bottom
// right cell or not
bool reachesBottom(vector<vector<int> >& a)
{
    // Number of rows and columns
    int n = a.size();
    int m = a[0].size();

    // Initialise the deque
    deque<vector<int> > q;

    // Traverse the matrix
    for (int i = 0; i < n; i++) {

        for (int j = 0; j < m; j++) {

            // Push 1 to front of queue
            if (a[i][j] == 1) {
                q.push_front({ i, j, 1 });
            }

            // Push 2 to back of queue
            else if (a[i][j] == 2) {
                q.push_back({ i, j, 2 });
            }

            a[i][j] = 0;
        }
    }

    // Store all the possible direction
    // of the current cell
    int dx[] = { -1, 0, 1, 0 };
    int dy[] = { 0, 1, 0, -1 };

    // Run multi-source BFS
    while (!q.empty()) {

        // Get the front element
        auto front = q.front();

        // Pop the front element
        q.pop_front();

        int i = front[0], j = front[1];
        int t = front[2];

        if (a[i][j])
            continue;

        a[i][j] = 1;

        // If 1 reached corner first
        if (t == 1 and (i == n - 1
                        && j == m - 1)) {
            return true;
        }

        for (int d = 0; d < 4; d++) {
            int ni = i + dx[d];
            int nj = j + dy[d];

            // Insert new point in queue
            if (ni >= 0 and ni < n
                and nj >= 0 and nj < m) {
                q.push_back({ ni, nj, t });
            }
        }
    }

    // If 1 can't reach the botton
    // right then return false
    return false;
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<int> > matrix{ { 0, 2, 0 },
                                 { 0, 1, 0 },
                                 { 0, 2, 0 } };

    // Function Call
    if (reachesBottom(matrix)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }

    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to check if cell with
// value 1 doesn't reaches the bottom
// right cell or not
static boolean reachesBottom(int[][] a)
{

    // Number of rows and columns
    int n = a.length;
    int m = a[0].length;

    // Initialise the deque
    Deque<int[]> q = new LinkedList<>();

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Push 1 to front of queue
            if (a[i][j] == 1)
            {
                q.addFirst(new int[]{ i, j, 1 });
            }

            // Push 2 to back of queue
            else if (a[i][j] == 2)
            {
                q.addLast(new int[]{ i, j, 2 });
            }
            a[i][j] = 0;
        }
    }

    // Store all the possible direction
    // of the current cell
    int dx[] = { -1, 0, 1, 0 };
    int dy[] = { 0, 1, 0, -1 };

    // Run multi-source BFS
    while (!q.isEmpty())
    {

        // Get the front element
        int[] front = q.peekFirst();

        // Pop the front element
        q.removeFirst();

        int i = front[0], j = front[1];
        int t = front[2];

        if (a[i][j] == 1)
            continue;

        a[i][j] = 1;

        // If 1 reached corner first
        if (t == 1 && (i == n - 1 && 
                       j == m - 1))
        {
            return true;
        }

        for(int d = 0; d < 4; d++)
        {
            int ni = i + dx[d];
            int nj = j + dy[d];

            // Insert new point in queue
            if (ni >= 0 && ni < n && 
                nj >= 0 && nj < m)
            {
                q.addLast(new int[]{ ni, nj, t });
            }
        }
    }

    // If 1 can't reach the botton
    // right then return false
    return false;
}

// Driver Code
public static void main (String[] args)
{

    // Given matrix
    int[][] matrix = { { 0, 2, 0 },
                       { 0, 1, 0 },
                       { 0, 2, 0 } };

    // Function call
    if (reachesBottom(matrix))
    {
        System.out.print("YES");
    }
    else
    {
        System.out.print("NO");
    }
}
}

// This code is contributed by offbeat

```

## Python

```py

# Python3 program for the above approach
from collections import deque

# Function to check if cell with
# value 1 doesn't reaches the bottom
# right cell or not
def reachesBottom(a):

    # Number of rows and columns
    n = len(a)
    m = len(a[0])

    # Initialise the deque
    q = deque()

    # Traverse the matrix
    for i in range(n):
        for j in range(m):

            # Push 1 to front of queue
            if (a[i][j] == 1):
                q.appendleft([i, j, 1])

            # Push 2 to back of queue
            elif (a[i][j] == 2):
                q.append([i, j, 2])

            a[i][j] = 0

    # Store all the possible direction
    # of the current cell
    dx = [ -1, 0, 1, 0 ]
    dy = [ 0, 1, 0, -1 ]

    # Run multi-source BFS
    while (len(q) > 0):

        # Get the front element
        front = q.popleft()
        i = front[0]
        j = front[1]
        t = front[2]

        if (a[i][j]):
            continue

        a[i][j] = 1

        # If 1 reached corner first
        if (t == 1 and (i == n - 1 and
                        j == m - 1)):
            return True

        for d in range(4):
            ni = i + dx[d]
            nj = j + dy[d]

            # Insert new poin queue
            if (ni >= 0 and ni < n and
                nj >= 0 and nj < m):
                q.append([ni, nj, t])

    # If 1 can't reach the botton
    # right then return false
    return False

# Driver Code
if __name__ == '__main__':

    # Given matrix
    matrix = [ [ 0, 2, 0 ],
               [ 0, 1, 0 ],
               [ 0, 2, 0 ] ]

    # Function call
    if (reachesBottom(matrix)):
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if cell with
// value 1 doesn't reaches the bottom
// right cell or not
static bool reachesBottom(int [,]a, 
                          int n, int m)
{
  // Initialise the deque
  Queue<int[]> q = new Queue<int[]>();

  // Traverse the matrix
  for(int i = 0; i < n; i++)
  {
    for(int j = 0; j < m; j++)
    {
      // Push 1 to front of queue
      if (a[i, j] == 1)
      {
        q.Enqueue(new int[]{i, j, 1});
      }

      // Push 2 to back of queue
      else if (a[i, j] == 2)
      {
        q.Enqueue(new int[]{i, j, 2});
      }
      a[i, j] = 0;
    }
  }

  // Store all the possible direction
  // of the current cell
  int []dx = {-1, 0, 1, 0};
  int []dy = {0, 1, 0, -1};

  // Run multi-source BFS
  while (q.Count != 0)
  {
    // Get the front element
    int[] front = q.Peek();

    // Pop the front element
    q.Dequeue();

    int i = front[0], j = front[1];
    int t = front[2];

    if (a[i, j] == 1)
      continue;

    a[i, j] = 1;

    // If 1 reached corner first
    if (t == 1 && (i == n - 1 && 
                   j == m - 1))
    {
      return true;
    }

    for(int d = 0; d < 4; d++)
    {
      int ni = i + dx[d];
      int nj = j + dy[d];

      // Insert new point in queue
      if (ni >= 0 && ni < n && 
          nj >= 0 && nj < m)
      {
        q.Enqueue(new int[]{ni, nj, t});
      }
    }
  }

  // If 1 can't reach the botton
  // right then return false
  return false;
}

// Driver Code
public static void Main(String[] args)
{
  // Given matrix
  int[,] matrix = {{0, 2, 0},
                   {0, 1, 0},
                   {0, 2, 0}};

  // Function call
  if (reachesBottom(matrix, 3, 3))
  {
    Console.Write("YES");
  }
  else
  {
    Console.Write("NO");
  }
}
}

// This code is contributed by gauravrajput1

```

**Output:** 

```
NO

```

**时间复杂度**：`O(N * M)`

**辅助空间**：`O(N * M)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。