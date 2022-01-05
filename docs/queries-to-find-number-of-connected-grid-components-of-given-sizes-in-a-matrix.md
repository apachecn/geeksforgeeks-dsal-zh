# 在矩阵中查找给定大小的连接网格组件数量的查询

> 原文:[https://www . geeksforgeeks . org/query-to-find-数量-矩阵中给定尺寸的连接网格组件/](https://www.geeksforgeeks.org/queries-to-find-number-of-connected-grid-components-of-given-sizes-in-a-matrix/)

给定一个仅包含 **0** s 和 **1** s 的[矩阵](https://www.geeksforgeeks.org/matrix/)**mat【】【】【】**以及一个查询【】的数组**，对于每个查询，比如说 **k** ，任务是找到大小为 **k** 的连接的网格组件的数量(*单元由 **1** s* 组成)。
***注意:**如果两个像元在上、下、左、右方向共享一条边而不是对角线，则它们是连接的。***

**示例:**

> **输入:**mat[][]=[[1 1 1 1 1 1 1 1]，
> [1 1 0 0 0 0 0 0]，
> [0 0 0 1 1 1]，
> [0 0 0 1 1 1 1]，
> [0 0 1 0 0 0]，
> [1 0 0 0 0]]
> 查询[]=**【6，1，8，2】 **T13】输出:【1，2 我们可以看到，不同大小的连接组件的数量在图像中标记为:****
> 
> ******输入:**矩阵[][] = [[1 1 0 0 0]，
> [1 0 0 1 0]，
> [0 0 1 1 0]，
> [1 1 0 0]]
> 查询[]= [3，1，2，4]
> **输出:** [2，0，1，0]
> **解释:**大小为 3，2 的连接组件数量为 2，1 所有其他大小均为零，因此输出数组为****

********方法:**思想是使用网格中的 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) / [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 来计数和存储[无序图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中所有大小的连通分量的数量的频率，然后我们可以[迭代查询数组](https://www.geeksforgeeks.org/how-to-iterate-over-an-array-using-for-loop-in-golang/)并为数组中每个给定大小分配连通分量的计数。
以下是解决问题的步骤:******

*   ****迭代矩阵，从包含“1”的未访问单元格执行 BFS 运算****
*   ****检查未访问的有效相邻单元格是否包含 1，并将这些单元格推入队列。****
*   ****对所有包含 1 的未访问单元格重复上述两个步骤。****
*   ****在查询中打印具有每个给定大小的连接组件数量的数组。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

const int n = 6;
const int m = 6;

const int dx[] = { 0, 1, -1, 0 };
const int dy[] = { 1, 0, 0, -1 };

// stores information about  which cell
// are already visited in a particular BFS
int visited[n][m];

// Stores the count of cells in
// the largest connected component
int COUNT;

// Function checks if a cell is valid, i.e.
// it is inside the grid and equal to 1
bool is_valid(int x, int y, int matrix[n][m])
{
    if (x < n && y < m && x >= 0 && y >= 0) {
        if (visited[x][y] == false
            && matrix[x][y] == 1)
            return true;
        else
            return false;
    }
    else
        return false;
}

// Map to count the frequency of
// each connected component
map<int, int> mp;

// function to calculate the
// largest connected component
void findComponentSize(int matrix[n][m])
{
    // Iterate over every cell
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (!visited[i][j] && matrix[i][j] == 1) {
                COUNT = 0;

                // Stores the indices of the matrix cells
                queue<pair<int, int> > q;

                // Mark the starting cell as visited
                // and push it into the queue
                q.push({ i, j });
                visited[i][j] = true;

                // Iterate while the queue
                // is not empty
                while (!q.empty()) {

                    pair<int, int> p = q.front();
                    q.pop();
                    int x = p.first, y = p.second;
                    COUNT++;

                    // Go to the adjacent cells
                    for (int i = 0; i < 4; i++) {

                        int newX = x + dx[i];
                        int newY = y + dy[i];

                        if (is_valid(newX, newY, matrix)) {
                            q.push({ newX, newY });
                            visited[newX][newY] = true;
                        }
                    }
                }

                mp[COUNT]++;
            }
        }
    }
}
// Drivers Code
int main()
{
    // Given input array of 1s and 0s
    int matrix[n][m]
        = { { 1, 1, 1, 1, 1, 1 }, { 1, 1, 0, 0, 0, 0 },
            { 0, 0, 0, 1, 1, 1 }, { 0, 0, 0, 1, 1, 1 },
            { 0, 0, 1, 0, 0, 0 }, { 1, 0, 0, 0, 0, 0 } };

    // queries array
    int queries[] = { 6, 1, 8, 2 };

    // sizeof queries array
    int N = sizeof(queries) / sizeof(queries[0]);

    // Initialize all cells unvisited
    memset(visited, false, sizeof visited);

    // Count the frequency of each connected component
    findComponentSize(matrix);

    // Iterate over the given queries array and
    // And answer the queries
    for (int i = 0; i < N; i++)
        cout << mp[queries[i]] << " ";

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java implementation for the above approach

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
static int n = 6;
static int m = 6;

static int dx[] = { 0, 1, -1, 0 };
static int dy[] = { 1, 0, 0, -1 };

// stores information about  which cell
// are already visited in a particular BFS
static int [][]visited = new int[n][m];

// Stores the final result grid
static int[][] result = new int[n][m];

// Stores the count of cells in
// the largest connected component
static int COUNT;

// Function checks if a cell is valid, i.e.
// it is inside the grid and equal to 1
static boolean is_valid(int x, int y, int matrix[][])
{
    if (x < n && y < m && x >= 0 && y >= 0) {
        if (visited[x][y] == 0
            && matrix[x][y] == 1)
            return true;
        else
            return false;
    }
    else
        return false;
}

// Map to count the frequency of
// each connected component
static HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

// function to calculate the
// largest connected component
static void findComponentSize(int matrix[][])
{
    // Iterate over every cell
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (visited[i][j]==0 && matrix[i][j] == 1) {
                COUNT = 0;

                // Stores the indices of the matrix cells
                Queue<pair > q = new LinkedList<>();

                // Mark the starting cell as visited
                // and push it into the queue
                q.add(new pair( i, j ));
                visited[i][j] = 1;

                // Iterate while the queue
                // is not empty
                while (!q.isEmpty()) {

                    pair p = q.peek();
                    q.remove();
                    int x = p.first, y = p.second;
                    COUNT++;

                    // Go to the adjacent cells
                    for (int k = 0; k < 4; k++) {

                        int newX = x + dx[k];
                        int newY = y + dy[k];

                        if (is_valid(newX, newY, matrix)) {
                            q.add(new pair(newX, newY ));
                            visited[newX][newY] = 1;
                        }
                    }
                }

                if(mp.containsKey(COUNT)){
                    mp.put(COUNT, mp.get(COUNT)+1);
                }
                else{
                    mp.put(COUNT, 1);
                }
            }
        }
    }
}
// Drivers Code
public static void main(String[] args)
{
    // Given input array of 1s and 0s
    int matrix[][]
        = { { 1, 1, 1, 1, 1, 1 }, { 1, 1, 0, 0, 0, 0 },
            { 0, 0, 0, 1, 1, 1 }, { 0, 0, 0, 1, 1, 1 },
            { 0, 0, 1, 0, 0, 0 }, { 1, 0, 0, 0, 0, 0 } };

    // queries array
    int queries[] = { 6, 1, 8, 2 };

    // sizeof queries array
    int N = queries.length;

    // Count the frequency of each connected component
    findComponentSize(matrix);

    // Iterate over the given queries array and
    // And answer the queries
    for (int i = 0; i < N; i++)
        System.out.print((mp.get(queries[i])!=null?mp.get(queries[i]):0)+ " ");

}
}

// This code is contributed by 29AjayKumar**
```

## ****蟒蛇 3****

```
**# Python 3 implementation for the above approach

n = 6
m = 6

dx = [0, 1, -1, 0]
dy = [1, 0, 0, -1]

# stores information about  which cell
# are already visited in a particular BFS
visited = [[False for i in range(m)] for j in range(n)]

# Stores the final result grid
result = [[0 for i in range(m)] for j in range(n)]

# Stores the count of cells in
# the largest connected component
COUNT = 0

# Function checks if a cell is valid, i.e.
# it is inside the grid and equal to 1
def is_valid(x, y, matrix):
    if (x < n and y < m and x >= 0 and y >= 0):
        if (visited[x][y] == False and matrix[x][y] == 1):
            return True
        else:
            return False
    else:
        return False

# Map to count the frequency of
# each connected component
mp = {}

# function to calculate the
# largest connected component
def findComponentSize(matrix):
    # Iterate over every cell
    for i in range(n):
        for j in range(m):
            if(visited[i][j]== False and matrix[i][j] == 1):
                COUNT = 0

                # Stores the indices of the matrix cells
                q = []

                # Mark the starting cell as visited
                # and push it into the queue
                q.append([i, j])
                visited[i][j] = True

                # Iterate while the queue
                # is not empty
                while (len(q)!=0):
                    p = q[0]
                    q = q[1:]
                    x = p[0]
                    y = p[1]
                    COUNT += 1

                    # Go to the adjacent cells
                    for i in range(4):
                        newX = x + dx[i]
                        newY = y + dy[i]

                        if (is_valid(newX, newY, matrix)):
                            q.append([newX, newY])
                            visited[newX][newY] = True
                if COUNT in mp:
                    mp[COUNT] += 1
                else:
                    mp[COUNT] = 1

# Drivers Code
if __name__ == '__main__':
    # Given input array of 1s and 0s
    matrix = [[1, 1, 1, 1, 1, 1],
              [1, 1, 0, 0, 0, 0],
              [0, 0, 0, 1, 1, 1],
              [0, 0, 0, 1, 1, 1],
              [0, 0, 1, 0, 0, 0],
              [1, 0, 0, 0, 0, 0]]

    # queries array
    queries = [6, 1, 8, 2]

    # sizeof queries array
    N = len(queries)

    # Count the frequency of each connected component
    findComponentSize(matrix)

    # Iterate over the given queries array and
    # And answer the queries
    for i in range(N):
        if queries[i] in mp:
          print(mp[queries[i]],end = " ")
        else:
          print(0,end = " ")

          # This code is contributed by SURENDRA_GANGWAR.**
```

## ****C#****

```
**// C# implementation for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    class pair
    {
        public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
static int n = 6;
static int m = 6;

static int []dx = { 0, 1, -1, 0 };
static int []dy = { 1, 0, 0, -1 };

// stores information about  which cell
// are already visited in a particular BFS
static int [,]visited = new int[n,m];

// Stores the count of cells in
// the largest connected component
static int COUNT;

// Function checks if a cell is valid, i.e.
// it is inside the grid and equal to 1
static bool is_valid(int x, int y, int [,]matrix)
{
    if (x < n && y < m && x >= 0 && y >= 0) {
        if (visited[x,y] == 0
            && matrix[x,y] == 1)
            return true;
        else
            return false;
    }
    else
        return false;
}

// Map to count the frequency of
// each connected component
static Dictionary<int,int> mp = new Dictionary<int,int>();

// function to calculate the
// largest connected component
static void findComponentSize(int [,]matrix)
{
    // Iterate over every cell
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (visited[i,j]==0 && matrix[i,j] == 1) {
                COUNT = 0;

                // Stores the indices of the matrix cells
                List<pair> q = new List<pair>();

                // Mark the starting cell as visited
                // and push it into the queue
                q.Add(new pair( i, j ));
                visited[i,j] = 1;

                // Iterate while the queue
                // is not empty
                while (q.Count>0) {

                    pair p = q[0];
                    q.RemoveAt();
                    int x = p.first, y = p.second;
                    COUNT++;

                    // Go to the adjacent cells
                    for (int k = 0; k < 4; k++) {

                        int newX = x + dx[k];
                        int newY = y + dy[k];

                        if (is_valid(newX, newY, matrix)) {
                            q.Add(new pair(newX, newY ));
                            visited[newX,newY] = 1;
                        }
                    }
                }

                if(mp.ContainsKey(COUNT)){
                    mp[COUNT] += 1;
                }
                else{
                    mp.Add(COUNT, 1);
                }
            }
        }
    }
}
// Drivers Code
public static void Main()
{
    // Given input array of 1s and 0s
    int [,]matrix
        = new int[,]{ { 1, 1, 1, 1, 1, 1 }, { 1, 1, 0, 0, 0, 0 },
            { 0, 0, 0, 1, 1, 1 }, { 0, 0, 0, 1, 1, 1 },
            { 0, 0, 1, 0, 0, 0 }, { 1, 0, 0, 0, 0, 0 } };

    // queries array
    int []queries = { 6, 1, 8, 2 };

    // sizeof queries array
    int N = queries.Length;
    for(int i=0;i<n;i++){
      for(int j=0;j<m;j++){
        visited[i,j] = 0;
      }
    }

    // Count the frequency of each connected component
    findComponentSize(matrix);

    // Iterate over the given queries array and
    // And answer the queries
    for (int i = 0; i < N; i++)
        if(mp.ContainsKey(queries[i])!=false)
        Console.Write(mp[queries[i]] + " ");

}
}

// This code is contributed by 29AjayKumar**
```

******Output:** 

```
1 2 1 0
```**** 

******时间复杂度:**O(n * m)
T3】空间复杂度: O(n*m)****