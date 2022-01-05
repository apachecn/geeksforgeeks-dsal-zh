# 检查一个网格中编号为 1 到 K 的单元在去掉一个阻塞单元的气氛后是否可以连接

> 原文:[https://www . geesforgeks . org/check-if-cells-numbers-1-to-k-in-a-grid-can-to-connected-on-remove-Atmos-one-blocked-cell/](https://www.geeksforgeeks.org/check-if-cells-numbered-1-to-k-in-a-grid-can-be-connected-after-removal-of-atmost-one-blocked-cell/)

给定由范围**【1，K】**中的值表示的 **K** 单元、由-1 表示的一些**阻塞单元和由 0** 表示的剩余**未阻塞单元组成的大小为 **N*M** 的网格**，任务是检查是否有可能通过解除一个**单元的阻塞来直接或间接连接这些 K 单元。只能移动到相邻的水平和垂直单元格。**

**示例**

```
Input:
A = {{0, 5, 6, 0}, 
     {3, -1, -1, 4}, 
     {-1, 2, 1, -1}, 
     {-1, -1, -1, -1}},
K = 6
Output: Yes
Explanation: 
Unblocking cell (2, 2) or (2, 3) or (3, 1) or
(3, 4) would make all the K cells connected.

Input:
A = {{-1, -1, 3, -1}, 
     {1, 0, -1, -1}, 
     {-1, -1, -1, 0}, 
     {-1, 0, 2, -1}},
K = 3
Output: No
Explanation:
Atleast two cells need to be unblocked.
```

**方法:**从编号为 **1 到 K** 的单元格中执行[**【BFS】**](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)，并根据每个单元格所属的组件对其进行标记。检查是否有任何相邻单元属于不同组件的阻塞单元。如果存在，则可以通过解除该单元的阻塞来连接。否则，是不可能的。

**示例:**

> 在执行 **BFS** 并通过其组件数量标记细胞后，数组如下所示:
> A={{1，1，1，1}，{1，-1，-1，1}，{-1，2，2，-1}，{-1，-1，-1，-1}}
> 细胞(2，2)周围不同标记的数量为 2。
> 因此，解开它将连接钾细胞。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;
#define pairs pair<int, int>

void check(int k, vector<vector<int> > a,
           int n, int m)
{
    int cells[k][2];
    bool visited[n][m];
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i][j] != 0
                && a[i][j] != -1) {

                cells[count][0] = i;
                cells[count][1] = j;
                count++;
            }
            visited[i][j] = false;
        }
    }

    // Arrays to make grid traversals easier
    int dx[] = { 0, 0, 1, -1 };
    int dy[] = { 1, -1, 0, 0 };

    // Store number of components
    int component = 0;

    // Perform BFS and mark every cell
    // by the component in which it belongs
    for (int i = 0; i < k; i++) {

        int x = cells[i][0], y = cells[i][1];

        if (visited[x][y])
            continue;
        component++;
        queue<pairs> cells;
        cells.push(make_pair(x, y));
        visited[x][y] = true;

        while (!cells.empty()) {

            pairs z = cells.front();
            cells.pop();
            a[z.first][z.second] = component;

            for (int j = 0; j < 4; j++) {

                int new_x = z.first + dx[j];
                int new_y = z.second + dy[j];
                if (new_x < 0 || new_x >= n
                    || new_y < 0 || new_y >= m)
                    continue;
                if (visited[new_x][new_y]
                    || a[new_x][new_y] == -1)
                    continue;

                cells.push(make_pair(new_x, new_y));
                visited[new_x][new_y] = true;
            }
        }
    }

    int maximum = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i][j] == -1) {
                unordered_set<int> set;
                for (int kk = 0; kk < 4; kk++) {

                    int xx = i + dx[kk];
                    int yy = j + dy[kk];
                    if (xx < 0 || xx >= n
                        || yy < 0 || yy >= m)
                        continue;

                    // if the cell doesn't
                    // belong to any component
                    if (a[xx][yy] <= 0)
                        continue;
                    set.insert(a[xx][yy]);
                }
                int s = set.size();
                maximum = max(s, maximum);
            }
        }
    }

    if (maximum == component) {
        cout << "Yes\n";
    }
    else {
        cout << "No\n";
    }
}
int main()
{
    int k = 6;
    int n = 4, m = 4;
    vector<vector<int> > a
        = { { 0, 5, 6, 0 },
            { 3, -1, -1, 4 },
            { -1, 2, 1, -1 },
            { -1, -1, -1, -1 } };

    check(k, a, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
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
static void check(int k, int [][]a,
           int n, int m)
{
    int [][]cell = new int[k][2];
    boolean [][]visited = new boolean[n][m];
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i][j] != 0
                && a[i][j] != -1) {

                cell[count][0] = i;
                cell[count][1] = j;
                count++;
            }
            visited[i][j] = false;
        }
    }

    // Arrays to make grid traversals easier
    int dx[] = { 0, 0, 1, -1 };
    int dy[] = { 1, -1, 0, 0 };

    // Store number of components
    int component = 0;

    // Perform BFS and mark every cell
    // by the component in which it belongs
    for (int i = 0; i < k; i++) {

        int x = cell[i][0], y = cell[i][1];

        if (visited[x][y])
            continue;
        component++;
        Queue<pair> cells = new LinkedList<>();
        cells.add(new pair(x, y));
        visited[x][y] = true;

        while (!cells.isEmpty()) {

            pair z = cells.peek();
            cells.remove();
            a[z.first][z.second] = component;

            for (int j = 0; j < 4; j++) {

                int new_x = z.first + dx[j];
                int new_y = z.second + dy[j];
                if (new_x < 0 || new_x >= n
                    || new_y < 0 || new_y >= m)
                    continue;
                if (visited[new_x][new_y]
                    || a[new_x][new_y] == -1)
                    continue;

                cells.add(new pair(new_x, new_y));
                visited[new_x][new_y] = true;
            }
        }
    }

    int maximum = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i][j] == -1) {
                HashSet<Integer> set = new HashSet<Integer>();
                for (int kk = 0; kk < 4; kk++) {

                    int xx = i + dx[kk];
                    int yy = j + dy[kk];
                    if (xx < 0 || xx >= n
                        || yy < 0 || yy >= m)
                        continue;

                    // if the cell doesn't
                    // belong to any component
                    if (a[xx][yy] <= 0)
                        continue;
                    set.add(a[xx][yy]);
                }
                int s = set.size();
                maximum = Math.max(s, maximum);
            }
        }
    }

    if (maximum == component) {
        System.out.print("Yes\n");
    }
    else {
        System.out.print("No\n");
    }
}

public static void main(String[] args)
{
    int k = 6;
    int n = 4, m = 4;
    int [][]a
        = { { 0, 5, 6, 0 },
            { 3, -1, -1, 4 },
            { -1, 2, 1, -1 },
            { -1, -1, -1, -1 } };

    check(k, a, n, m);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from collections import deque as queue
def check(k, a, n, m):

    cells = [[0 for i in range(2)] for i in range(k)]
    visited = [[0 for i in range(m)] for i in range(n)]
    count = 0
    for i in range(n):
        for j in range(m):

            if (a[i][j] != 0
                and a[i][j] != -1):

                cells[count][0] = i
                cells[count][1] = j
                count += 1

            visited[i][j] = False

    # Arrays to make grid traversals easier
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]

    # Store number of components
    component = 0

    # Perform BFS and mark every cell
    # by the component in which it belongs
    for i in range(k):

        x = cells[i][0]
        y = cells[i][1]

        if (visited[x][y]):
            continue
        component += 1
        cell = queue()
        cell.append([x, y])
        visited[x][y] = True

        while (len(cell) > 0):

            z = cell.popleft()
            a[z[0]][z[1]] = component

            for j in range(4):

                new_x = z[0] + dx[j]
                new_y = z[1] + dy[j]
                if (new_x < 0 or new_x >= n
                    or new_y < 0 or new_y >= m):
                    continue
                if (visited[new_x][new_y]
                    or a[new_x][new_y] == -1):
                    continue

                cell.append([new_x, new_y])
                visited[new_x][new_y] = True

    maximum = 0
    for i in range(n):
        for j in range(m):

            if (a[i][j] == -1):
                se = dict()
                for kk in range(4):

                    xx = i + dx[kk]
                    yy = j + dy[kk]
                    if (xx < 0 or xx >= n
                        or yy < 0 or yy >= m):
                        continue

                    # if the cell doesn't
                    # belong to any component
                    if (a[xx][yy] <= 0):
                        continue
                    se[a[xx][yy]] = 1

                s = len(se)
                maximum = max(s, maximum)

    if (maximum == component):
        print("Yes\n")

    else:
        print("No\n")

# Driver code
if __name__ == '__main__':
    k = 6
    n = 4
    m = 4
    a=[[0, 5, 6, 0 ],
    [3, -1, -1, 4],
    [-1, 2, 1, -1],
    [-1, -1,-1,-1]]

    check(k, a, n, m)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
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
static void check(int k, int [,]a,
           int n, int m)
{
    int [,]cell = new int[k,2];
    bool [,]visited = new bool[n,m];
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i, j] != 0
                && a[i, j] != -1) {

                cell[count, 0] = i;
                cell[count, 1] = j;
                count++;
            }
            visited[i, j] = false;
        }
    }

    // Arrays to make grid traversals easier
    int []dx = { 0, 0, 1, -1 };
    int []dy = { 1, -1, 0, 0 };

    // Store number of components
    int component = 0;

    // Perform BFS and mark every cell
    // by the component in which it belongs
    for (int i = 0; i < k; i++) {

        int x = cell[i, 0], y = cell[i, 1];

        if (visited[x, y])
            continue;
        component++;
        List<pair> cells = new List<pair>();
        cells.Add(new pair(x, y));
        visited[x, y] = true;

        while (cells.Count != 0) {

            pair z = cells[0];
            cells.RemoveAt(0);
            a[z.first,z.second] = component;

            for (int j = 0; j < 4; j++) {

                int new_x = z.first + dx[j];
                int new_y = z.second + dy[j];
                if (new_x < 0 || new_x >= n
                    || new_y < 0 || new_y >= m)
                    continue;
                if (visited[new_x,new_y]
                    || a[new_x, new_y] == -1)
                    continue;

                cells.Add(new pair(new_x, new_y));
                visited[new_x, new_y] = true;
            }
        }
    }

    int maximum = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i, j] == -1) {
                HashSet<int> set = new HashSet<int>();
                for (int kk = 0; kk < 4; kk++) {

                    int xx = i + dx[kk];
                    int yy = j + dy[kk];
                    if (xx < 0 || xx >= n
                        || yy < 0 || yy >= m)
                        continue;

                    // if the cell doesn't
                    // belong to any component
                    if (a[xx, yy] <= 0)
                        continue;
                    set.Add(a[xx, yy]);
                }
                int s = set.Count;
                maximum = Math.Max(s, maximum);
            }
        }
    }

    if (maximum == component) {
        Console.Write("Yes\n");
    }
    else {
        Console.Write("No\n");
    }
}

public static void Main(String[] args)
{
    int k = 6;
    int n = 4, m = 4;
    int [,]a
        = { { 0, 5, 6, 0 },
            { 3, -1, -1, 4 },
            { -1, 2, 1, -1 },
            { -1, -1, -1, -1 } };

    check(k, a, n, m);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
function check(k, a, n, m)
{
    var cells = Array.from(
        Array(k), () => Array(2).fill(0));
    var visited = Array.from(
        Array(n), () => Array(m).fill(0));
    var count = 0;
    for(var i = 0; i < n; i++)
    {
        for(var j = 0; j < m; j++)
        {
            if (a[i][j] != 0 && a[i][j] != -1)
            {
                cells[count][0] = i;
                cells[count][1] = j;
                count++;
            }
            visited[i][j] = false;
        }
    }

    // Arrays to make grid traversals easier
    var dx = [ 0, 0, 1, -1 ];
    var dy = [ 1, -1, 0, 0 ];

    // Store number of components
    var component = 0;

    // Perform BFS and mark every cell
    // by the component in which it belongs
    for(var i = 0; i < k; i++)
    {
        var x = cells[i][0], y = cells[i][1];

        if (visited[x][y])
            continue;

        component++;
        var cell = [];
        cell.push([x, y]);
        visited[x][y] = true;

        while (cell.length != 0)
        {
            var z = cell[0];
            cell.shift();
            a[z[0]][z[1]] = component;

            for(var j = 0; j < 4; j++)
            {
                var new_x = z[0] + dx[j];
                var new_y = z[1] + dy[j];

                if (new_x < 0 || new_x >= n ||
                    new_y < 0 || new_y >= m)
                    continue;
                if (visited[new_x][new_y] ||
                          a[new_x][new_y] == -1)
                    continue;

                cell.push([new_x, new_y]);
                visited[new_x][new_y] = true;
            }
        }
    }

    var maximum = 0;
    for(var i = 0; i < n; i++)
    {
        for(var j = 0; j < m; j++)
        {
            if (a[i][j] == -1)
            {
                var set = new Set();
                for(var kk = 0; kk < 4; kk++)
                {
                    var xx = i + dx[kk];
                    var yy = j + dy[kk];
                    if (xx < 0 || xx >= n ||
                        yy < 0 || yy >= m)
                        continue;

                    // If the cell doesn't
                    // belong to any component
                    if (a[xx][yy] <= 0)
                        continue;

                    set.add(a[xx][yy]);
                }
                var s = set.size;
                maximum = Math.max(s, maximum);
            }
        }
    }
    if (maximum == component)
    {
        document.write("Yes");
    }
    else
    {
        document.write("No");
    }
}

// Driver code
var k = 6;
var n = 4, m = 4;

var a = [ [ 0, 5, 6, 0 ],
          [ 3, -1, -1, 4 ],
          [ -1, 2, 1, -1 ],
          [ -1, -1, -1, -1 ] ];

check(k, a, n, m);

// This code is contributed by itsok

</script>
```

**Output:** 

```
Yes
```

**性能分析:**

*   **时间复杂度:**在矩阵上执行 BFS 需要 O(N*M)时间和 **O(N*M)** 时间来检查每个阻塞的单元。因此总的时间复杂度将是 **O(N * M)** 。
*   **辅助空间复杂度:** O(N * M)