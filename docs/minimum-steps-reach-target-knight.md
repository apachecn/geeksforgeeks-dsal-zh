# 骑士到达目标的最小步数|设定 1

> 原文:[https://www . geesforgeks . org/最低步数-到达-目标-骑士/](https://www.geeksforgeeks.org/minimum-steps-reach-target-knight/)

给定一个 N×N 大小的正方形棋盘，给出骑士的位置和目标的位置。我们需要找出骑士到达目标位置的最低步骤。
**例:**

```
In above diagram Knight takes 3 step to reach 
from (4, 5) to (1, 1) (4, 5) -> (5, 3) -> (3, 2) 
-> (1, 1)  as shown in diagram
```

**<u>逼近:</u>**
这个问题可以看作是未加权图中的最短路径。所以我们用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 来解决这个问题。我们尝试了骑士可以从其位置到达的所有 8 个可能位置。如果可到达的位置还没有被访问并且在板内，我们将这个状态推入队列，距离比它的父状态多 1。最后我们返回目标位置的距离，当它从队列中弹出时。
下面的代码实现了通过单元格进行搜索的 BFS，其中每个单元格包含其坐标和距起始节点的距离。在最坏的情况下，下面的代码访问板的所有单元，使最坏的情况时间复杂度为 O(N^2)

## C++

```
// C++ program to find minimum steps to reach to
// specific cell in minimum moves by Knight
#include <bits/stdc++.h>
using namespace std;

// structure for storing a cell's data
struct cell {
    int x, y;
    int dis;
    cell() {}
    cell(int x, int y, int dis)
        : x(x), y(y), dis(dis)
    {
    }
};

// Utility method returns true if (x, y) lies
// inside Board
bool isInside(int x, int y, int N)
{
    if (x >= 1 && x <= N && y >= 1 && y <= N)
        return true;
    return false;
}

// Method returns minimum step
// to reach target position
int minStepToReachTarget(
    int knightPos[], int targetPos[],
    int N)
{
    // x and y direction, where a knight can move
    int dx[] = { -2, -1, 1, 2, -2, -1, 1, 2 };
    int dy[] = { -1, -2, -2, -1, 1, 2, 2, 1 };

    // queue for storing states of knight in board
    queue<cell> q;

    // push starting position of knight with 0 distance
    q.push(cell(knightPos[0], knightPos[1], 0));

    cell t;
    int x, y;
    bool visit[N + 1][N + 1];

    // make all cell unvisited
    for (int i = 1; i <= N; i++)
        for (int j = 1; j <= N; j++)
            visit[i][j] = false;

    // visit starting state
    visit[knightPos[0]][knightPos[1]] = true;

    // loop until we have one element in queue
    while (!q.empty()) {
        t = q.front();
        q.pop();

        // if current cell is equal to target cell,
        // return its distance
        if (t.x == targetPos[0] && t.y == targetPos[1])
            return t.dis;

        // loop for all reachable states
        for (int i = 0; i < 8; i++) {
            x = t.x + dx[i];
            y = t.y + dy[i];

            // If reachable state is not yet visited and
            // inside board, push that state into queue
            if (isInside(x, y, N) && !visit[x][y]) {
                visit[x][y] = true;
                q.push(cell(x, y, t.dis + 1));
            }
        }
    }
}

// Driver code to test above methods
int main()
{
    int N = 30;
    int knightPos[] = { 1, 1 };
    int targetPos[] = { 30, 30 };
    cout << minStepToReachTarget(knightPos, targetPos, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java program to find minimum steps to reach to
// specific cell in minimum moves by Knight
class GFG {

    // Class for storing a cell's data
    static class cell {
        int x, y;
        int dis;

        public cell(int x, int y, int dis)
        {
            this.x = x;
            this.y = y;
            this.dis = dis;
        }
    }

    // Utility method returns true if (x, y) lies
    // inside Board
    static boolean isInside(int x, int y, int N)
    {
        if (x >= 1 && x <= N && y >= 1 && y <= N)
            return true;
        return false;
    }

    // Method returns minimum step
    // to reach target position
    static int minStepToReachTarget(
        int knightPos[], int targetPos[],
        int N)
    {
        // x and y direction, where a knight can move
        int dx[] = { -2, -1, 1, 2, -2, -1, 1, 2 };
        int dy[] = { -1, -2, -2, -1, 1, 2, 2, 1 };

        // queue for storing states of knight in board
        Vector<cell> q = new Vector<>();

        // push starting position of knight with 0 distance
        q.add(new cell(knightPos[0], knightPos[1], 0));

        cell t;
        int x, y;
        boolean visit[][] = new boolean[N + 1][N + 1];

        // make all cell unvisited
        for (int i = 1; i <= N; i++)
            for (int j = 1; j <= N; j++)
                visit[i][j] = false;

        // visit starting state
        visit[knightPos[0]][knightPos[1]] = true;

        // loop until we have one element in queue
        while (!q.isEmpty()) {
            t = q.firstElement();
            q.remove(0);

            // if current cell is equal to target cell,
            // return its distance
            if (t.x == targetPos[0] && t.y == targetPos[1])
                return t.dis;

            // loop for all reachable states
            for (int i = 0; i < 8; i++) {
                x = t.x + dx[i];
                y = t.y + dy[i];

                // If reachable state is not yet visited and
                // inside board, push that state into queue
                if (isInside(x, y, N) && !visit[x][y]) {
                    visit[x][y] = true;
                    q.add(new cell(x, y, t.dis + 1));
                }
            }
        }
        return Integer.MAX_VALUE;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 30;
        int knightPos[] = { 1, 1 };
        int targetPos[] = { 30, 30 };
        System.out.println(
            minStepToReachTarget(
                knightPos, targetPos, N));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to find minimum steps to reach
# to specific cell in minimum moves by Knight
class cell:

    def __init__(self, x = 0, y = 0, dist = 0):
        self.x = x
        self.y = y
        self.dist = dist

# checks whether given position is
# inside the board
def isInside(x, y, N):
    if (x >= 1 and x <= N and
        y >= 1 and y <= N):
        return True
    return False

# Method returns minimum step to reach
# target position
def minStepToReachTarget(knightpos,
                         targetpos, N):

    # all possible movments for the knight
    dx = [2, 2, -2, -2, 1, 1, -1, -1]
    dy = [1, -1, 1, -1, 2, -2, 2, -2]

    queue = []

    # push starting position of knight
    # with 0 distance
    queue.append(cell(knightpos[0], knightpos[1], 0))

    # make all cell unvisited
    visited = [[False for i in range(N + 1)]
                      for j in range(N + 1)]

    # visit starting state
    visited[knightpos[0]][knightpos[1]] = True

    # loop until we have one element in queue
    while(len(queue) > 0):

        t = queue[0]
        queue.pop(0)

        # if current cell is equal to target
        # cell, return its distance
        if(t.x == targetpos[0] and
           t.y == targetpos[1]):
            return t.dist

        # iterate for all reachable states
        for i in range(8):

            x = t.x + dx[i]
            y = t.y + dy[i]

            if(isInside(x, y, N) and not visited[x][y]):
                visited[x][y] = True
                queue.append(cell(x, y, t.dist + 1))

# Driver Code    
if __name__=='__main__':
    N = 30
    knightpos = [1, 1]
    targetpos = [30, 30]
    print(minStepToReachTarget(knightpos,
                               targetpos, N))

# This code is contributed by
# Kaustav kumar Chanda
```

## C#

```
// C# program to find minimum steps to reach to
// specific cell in minimum moves by Knight
using System;
using System.Collections.Generic;

class GFG {

    // Class for storing a cell's data
    public class cell {
        public int x, y;
        public int dis;

        public cell(int x, int y, int dis)
        {
            this.x = x;
            this.y = y;
            this.dis = dis;
        }
    }

    // Utility method returns true
    // if (x, y) lies inside Board
    static bool isInside(int x, int y, int N)
    {
        if (x >= 1 && x <= N && y >= 1 && y <= N)
            return true;
        return false;
    }

    // Method returns minimum step
    // to reach target position
    static int minStepToReachTarget(int[] knightPos,
                                    int[] targetPos, int N)
    {
        // x and y direction, where a knight can move
        int[] dx = { -2, -1, 1, 2, -2, -1, 1, 2 };
        int[] dy = { -1, -2, -2, -1, 1, 2, 2, 1 };

        // queue for storing states of knight in board
        Queue<cell> q = new Queue<cell>();

        // push starting position of knight with 0 distance
        q.Enqueue(new cell(knightPos[0],
                           knightPos[1], 0));

        cell t;
        int x, y;
        bool[, ] visit = new bool[N + 1, N + 1];

        // make all cell unvisited
        for (int i = 1; i <= N; i++)
            for (int j = 1; j <= N; j++)
                visit[i, j] = false;

        // visit starting state
        visit[knightPos[0], knightPos[1]] = true;

        // loop until we have one element in queue
        while (q.Count != 0) {
            t = q.Peek();
            q.Dequeue();

            // if current cell is equal to target cell,
            // return its distance
            if (t.x == targetPos[0] && t.y == targetPos[1])
                return t.dis;

            // loop for all reachable states
            for (int i = 0; i < 8; i++) {
                x = t.x + dx[i];
                y = t.y + dy[i];

                // If reachable state is not yet visited and
                // inside board, push that state into queue
                if (isInside(x, y, N) && !visit[x, y]) {
                    visit[x, y] = true;
                    q.Enqueue(new cell(x, y, t.dis + 1));
                }
            }
        }
        return int.MaxValue;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int N = 30;
        int[] knightPos = { 1, 1 };
        int[] targetPos = { 30, 30 };
        Console.WriteLine(
            minStepToReachTarget(
                knightPos,
                targetPos, N));
    }
}
// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find minimum steps to reach to
// specific cell in minimum moves by Knight

// Class for storing a cell's data
class cell
{
    constructor(x,y,dis)
    {
        this.x = x;
            this.y = y;
            this.dis = dis;
    }
}

// Utility method returns true if (x, y) lies
    // inside Board
function isInside(x,y,N)
{
    if (x >= 1 && x <= N && y >= 1 && y <= N)
            return true;
        return false;
}

// Method returns minimum step
    // to reach target position
function minStepToReachTarget(knightPos,targetPos,N)
{
    // x and y direction, where a knight can move
        let dx = [ -2, -1, 1, 2, -2, -1, 1, 2 ];
        let dy = [ -1, -2, -2, -1, 1, 2, 2, 1 ];

        // queue for storing states of knight in board
        let q = [];

        // push starting position of knight with 0 distance
        q.push(new cell(knightPos[0], knightPos[1], 0));

        let t;
        let x, y;
        let visit = new Array(N + 1);

        // make all cell unvisited
        for (let i = 1; i <= N; i++)
        {
            visit[i]=new Array(N+1);
            for (let j = 1; j <= N; j++)
                visit[i][j] = false;
        }

        // visit starting state
        visit[knightPos[0]][knightPos[1]] = true;

        // loop until we have one element in queue
        while (q.length!=0) {
            t = q.shift();

            // if current cell is equal to target cell,
            // return its distance
            if (t.x == targetPos[0] && t.y == targetPos[1])
                return t.dis;

            // loop for all reachable states
            for (let i = 0; i < 8; i++) {
                x = t.x + dx[i];
                y = t.y + dy[i];

                // If reachable state is not yet visited and
                // inside board, push that state into queue
                if (isInside(x, y, N) && !visit[x][y]) {
                    visit[x][y] = true;
                    q.push(new cell(x, y, t.dis + 1));
                }
            }
        }
        return Number.MAX_VALUE;
}

// Driver code
let N = 30;
let knightPos=[1,1];
let targetPos=[30,30];
document.write(
            minStepToReachTarget(
                knightPos, targetPos, N));

// This code is contributed by rag2127
</script>
```

**输出:**

```
20
```

**复杂度分析:**

*   **时间复杂度:** O(N^2).
    最坏的情况下，所有的小区都会被访问，所以时间复杂度是 O(N^2).
*   **辅助空间:** O(N^2).
    节点按队列存储。所以空间的复杂性是 O(N^2).

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。