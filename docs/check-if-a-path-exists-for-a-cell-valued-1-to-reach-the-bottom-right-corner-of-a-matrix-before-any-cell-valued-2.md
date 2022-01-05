# 检查值为 1 的单元格在值为 2 的单元格之前是否存在到达矩阵右下角的路径

> 原文:[https://www . geesforgeks . org/check-if-a-path-exists-for-a-cell-value-1-to-reach-a-matrix-右下角-any-cell-value-2/](https://www.geeksforgeeks.org/check-if-a-path-exists-for-a-cell-valued-1-to-reach-the-bottom-right-corner-of-a-matrix-before-any-cell-valued-2/)

给定尺寸为 **N * M** 的矩阵 **arr[][]** ，具有元素 **0** 、 **1** 和 **2** 。矩阵中只有一个值为 **1** 的单元格。任务是检查 **1** 是否有可能在任何有值的单元格 **2** 之前到达右下角，或者不使用以下操作:

*   **2** 可以在 1 个单位的时间内在所有四个方向复制自身 1 个单位。
*   **1** 如果该位置的元素为 **0** ，则只能在所有四个方向中的一个方向上移动。

如果值为 **1** 的单元格到达右下角的时间少于或等于任何值为 **2** 的单元格到达右下角的时间，则打印“**是”**。否则，打印“**1”**。

**示例:**

> **输入:** N = 3，M = 3，arr[][] = {{0，2，0}，{0，1，0}，{0，0，0}}
> **输出**:是
> **说明:**
> 1 可以在 2 次移动中移动到右下角，2 可以在 3 次移动中移动到右下角。
> 因为值为 1 的单元格比值为 2 的单元格先到达。因此，打印“是”。
> 
> **输入:** N = 3，M = 3，arr[][] = {{0，2，0}，{0，1，0}，{0，2，0}}
> **输出:**否
> **说明:**
> 1 在 2 次移动中可以移动到右下角，单元格最后一行的 2 在 1 次移动中可以移动到右下角。
> 因为值为 2 的单元格比值为 1 的单元格先到达。因此，打印编号。

**进场:**思路是使用[多源 BFS](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/) 。要执行多源 BFS 遍历，将矩阵中存在的所有 **1** 和 **2** 的位置以指定的顺序添加到一个[德格](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/)中。通过弹出添加的位置并添加尚未访问的相邻位置，对该出列执行 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。按照以下步骤解决问题:

1.  为多源 BFS 创建出列。
2.  首先在前面加上 **1** 的位置，然后在后面加上 **2** 的位置。这是因为如果 **1** 和 **2** 同时到达右下方，则 **1** 被认为超过了 **2** 。
3.  从出列的前面弹出元素，直到出列为空，然后执行以下操作:
    *   如果弹出的位置已经被访问过，进入下一个位置。
    *   如果该位置未被访问，检查其是否为右下位置，以及检查其中的元素是否为 **1** 。如果发现是真的，那么打印**是**。
    *   否则，对于所有四个方向，在**出列**中插入当前位置。
4.  一旦上述操作结束，如果未发现值为 **1** 的单元格到达右下角位置，则打印**否**。

下面是上述方法的实现:

## C++

```
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

    // If 1 can't reach the bottom
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

    // If 1 can't reach the bottom
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

## 蟒蛇 3

```
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

    # If 1 can't reach the bottom
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

```
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

  // If 1 can't reach the bottom
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

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if cell with
// value 1 doesn't reaches the bottom
// right cell or not
function reachesBottom(a)
{
    // Number of rows and columns
    var n = a.length;
    var m = a[0].length;

    // Initialise the deque
    var q = [];

    // Traverse the matrix
    for (var i = 0; i < n; i++) {

        for (var j = 0; j < m; j++) {

            // Push 1 to front of queue
            if (a[i][j] == 1) {
                q.slice(0,0,[i, j, 1]);
            }

            // Push 2 to back of queue
            else if (a[i][j] == 2) {
                q.push([i, j, 2 ]);
            }

            a[i][j] = 0;
        }
    }

    // Store all the possible direction
    // of the current cell
    var dx = [-1, 0, 1, 0 ];
    var dy = [ 0, 1, 0, -1 ];

    // Run multi-source BFS
    while (!q.length) {

        // Get the front element
        var front = q[0];

        // Pop the front element
        q.shift();

        var i = front[0], j = front[1];
        var t = front[2];

        if (a[i][j])
            continue;

        a[i][j] = 1;

        // If 1 reached corner first
        if (t == 1 && (i == n - 1
                        && j == m - 1)) {
            return true;
        }

        for (var d = 0; d < 4; d++) {
            var ni = i + dx[d];
            var nj = j + dy[d];

            // Insert new point in queue
            if (ni >= 0 && ni < n
               && nj >= 0 && nj < m) {
                q.push([ ni, nj, t ]);
            }
        }
    }

    // If 1 can't reach the bottom
    // right then return false
    return false;
}

// Driver Code
// Given matrix
var matrix = [[ 0, 2, 0 ],
                             [ 0, 1, 0 ],
                             [0, 2, 0 ]];
// Function Call
if (reachesBottom(matrix)) {
    document.write( "YES");
}
else {
    document.write( "NO");
}

</script>
```

**Output:** 

```
NO
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*