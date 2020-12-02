# 查找距银行后卫的最短距离

> 原文： [https://www.geeksforgeeks.org/find-shortest-distance-guard-bank/](https://www.geeksforgeeks.org/find-shortest-distance-guard-bank/)

给定一个填充有“ O”，“ G”和“ W”的矩阵，其中“ O”代表开放空间，“ G”代表守卫，“ W”代表银行的墙。 将矩阵中的所有 O 替换成与警卫的最短距离，而又不能穿过任何墙壁。 同样，在输出矩阵中，将防护装置替换为 0，将墙壁替换为-1。
预期的**对于 M x N 矩阵，时间复杂度**为 O（MN）。

例子：

```
O ==> Open Space
G ==> Guard
W ==> Wall

Input: 
  O  O  O  O  G
  O  W  W  O  O
  O  O  O  W  O
  G  W  W  W  O
  O  O  O  O  G

Output:  
  3  3  2  1  0
  2 -1 -1  2  1
  1  2  3 -1  2
  0 -1 -1 -1  1
  1  2  2  1  0

```

这个想法是做 BFS。 我们首先将所有包含防护的单元排队，然后循环直到队列不为空。 对于循环的每次迭代，我们将前单元从队列中出队，并针对其四个相邻单元中的每一个，如果单元是一个开放区域，并且尚未计算出其与后卫的距离，我们将更新其距离并将其入队。 最后，在 BFS 程序结束后，我们将打印距离矩阵。

以下是上述想法的实现–

## C++

```cpp

// C++ program to replace all of the O's in the matrix
// with their shortest distance from a guard
#include <bits/stdc++.h>
using namespace std;

// store dimensions of the matrix
#define M 5
#define N 5

// An Data Structure for queue used in BFS
struct queueNode
{
    // i, j and distance stores x and y-coordinates
    // of a matrix cell and its distance from guard
    // respectively
    int i, j, distance;
};

// These arrays are used to get row and column
// numbers of 4 neighbors of a given cell
int row[] = { -1, 0, 1, 0};
int col[] = { 0, 1, 0, -1 };

// return true if row number and column number
// is in range
bool isValid(int i, int j)
{
    if ((i < 0 || i > M - 1) || (j < 0 || j > N - 1))
        return false;

    return true;
}

// return true if current cell is an open area and its
// distance from guard is not calculated yet
bool isSafe(int i, int j, char matrix[][N], int output[][N])
{
    if (matrix[i][j] != 'O' || output[i][j] != -1)
        return false;

    return true;
}

// Function to replace all of the O's in the matrix
// with their shortest distance from a guard
void findDistance(char matrix[][N])
{
    int output[M][N];
    queue<queueNode> q;

    // finding Guards location and adding into queue
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
        {
            // initialize each cell as -1
            output[i][j] = -1;
            if (matrix[i][j] == 'G')
            {
                queueNode pos = {i, j, 0};
                q.push(pos);
                // guard has 0 distance
                output[i][j] = 0;
            }
        }
    }

    // do till queue is empty
    while (!q.empty())
    {
        // get the front cell in the queue and update
        // its adjacent cells
        queueNode curr = q.front();
        int x = curr.i, y = curr.j, dist = curr.distance;

        // do for each adjacent cell
        for (int i = 0; i < 4; i++)
        {
            // if adjacent cell is valid, has path and
            // not visited yet, en-queue it.
            if (isSafe(x + row[i], y + col[i], matrix, output)
                && isValid(x + row[i], y + col[i]))
            {
                output[x + row[i]][y + col[i]] = dist + 1;

                queueNode pos = {x + row[i], y + col[i], dist + 1};
                q.push(pos);
            }
        }

        // dequeue the front cell as its distance is found
        q.pop();
    }

    // print output matrix
    for (int i = 0; i < M; i++)
    {
        for (int j = 0; j < N; j++)
            cout << std::setw(3) << output[i][j];
        cout << endl;
    }
}

// Driver code
int main()
{
    char matrix[][N] =
    {
        {'O', 'O', 'O', 'O', 'G'},
        {'O', 'W', 'W', 'O', 'O'},
        {'O', 'O', 'O', 'W', 'O'},
        {'G', 'W', 'W', 'W', 'O'},
        {'O', 'O', 'O', 'O', 'G'}
    };

    findDistance(matrix);

    return 0;
}

```

## Java

```java

// Java program to replace all of the O's
// in the matrix with their shortest 
// distance from a guard 
package Graphs;

import java.util.LinkedList;
import java.util.Queue;

public class MinDistanceFromaGuardInBank{

// Store dimensions of the matrix 
int M = 5;
int N = 5;

class Node 
{
    int i, j, dist;
    Node(int i, int j, int dist)
    {
        this.i = i;
        this.j = j;
        this.dist = dist;
    }
}

// These arrays are used to get row
// and column numbers of 4 neighbors
// of a given cell 
int row[] = { -1, 0, 1, 0 };
int col[] = { 0, 1, 0, -1 };

// Return true if row number and 
// column number is in range 
boolean isValid(int i, int j)
{
    if ((i < 0 || i > M - 1) ||
        (j < 0 || j > N - 1))
        return false;

    return true;
}

// Return true if current cell is 
// an open area and its distance 
// from guard is not calculated yet 
boolean isSafe(int i, int j, char matrix[][],
                              int output[][])
{
    if (matrix[i][j] != 'O' || 
        output[i][j] != -1)
        return false;

    return true;
}

// Function to replace all of the O's 
// in the matrix with their shortest
// distance from a guard 
void findDistance(char matrix[][])
{
    int output[][] = new int[M][N];
    Queue<Node> q = new LinkedList<Node>();

    // Finding Guards location and
    // adding into queue 
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Initialize each cell as -1 
            output[i][j] = -1;

            if (matrix[i][j] == 'G')
            {
                q.add(new Node(i, j, 0));

                // Guard has 0 distance 
                output[i][j] = 0;
            }
        }
    }

    // Do till queue is empty 
    while (!q.isEmpty())
    {

        // Get the front cell in the queue
        // and update its adjacent cells 
        Node curr = q.peek();
        int x = curr.i;
        int y = curr.j;
        int dist = curr.dist;

        // Do for each adjacent cell 
        for (int i = 0; i < 4; i++) 
        {

            // If adjacent cell is valid, has
            // path and not visited yet,
            // en-queue it. 
            if (isValid(x + row[i], y + col[i]))
            {
                if (isSafe(x + row[i], y + col[i],
                           matrix, output)) 
                {
                    output[x + row[i]][y + col[i]] = dist + 1;
                    q.add(new Node(x + row[i],
                                   y + col[i],
                                   dist + 1));
                }
            }
        }

        // Dequeue the front cell as 
        // its distance is found 
        q.poll();
    }

    // Print output matrix 
    for(int i = 0; i < M; i++) 
    {
        for(int j = 0; j < N; j++)
        {
            System.out.print(output[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver code
public static void main(String args[])
{
    char matrix[][] = { { 'O', 'O', 'O', 'O', 'G' },
                        { 'O', 'W', 'W', 'O', 'O' },
                        { 'O', 'O', 'O', 'W', 'O' },
                        { 'G', 'W', 'W', 'W', 'O' },
                        { 'O', 'O', 'O', 'O', 'G' } };

    MinDistanceFromaGuardInBank g = 
    new MinDistanceFromaGuardInBank();

    g.findDistance(matrix);
}
}

// This code is contributed by Shobhit Yadav

```

## Python3

```

# Python3 program to replace all of the O's in the matrix
# with their shortest distance from a guard
from collections import deque as queue

# store dimensions of the matrix
M = 5
N = 5

# These arrays are used to get row and column
# numbers of 4 neighbors of a given cell
row = [-1, 0, 1, 0]
col = [0, 1, 0, -1]

# return true if row number and column number
# is in range
def isValid(i, j):
    if ((i < 0 or i > M - 1) or (j < 0 or j > N - 1)):
        return False

    return True

# return true if current cell is an open area and its
# distance from guard is not calculated yet
def isSafe(i, j,matrix, output):

    if (matrix[i][j] != 'O' or output[i][j] != -1):
        return False

    return True

# Function to replace all of the O's in the matrix
# with their shortest distance from a guard
def findDistance(matrix):
    output = [[ -1 for i in range(N)]for i in range(M)]
    q = queue()

    # finding Guards location and adding into queue
    for i in range(M):
        for j in range(N):

            # initialize each cell as -1
            output[i][j] = -1
            if (matrix[i][j] == 'G'):
                pos = [i, j, 0]
                q.appendleft(pos)

                # guard has 0 distance
                output[i][j] = 0

    # do till queue is empty
    while (len(q) > 0):

        # get the front cell in the queue and update
        # its adjacent cells
        curr = q.pop()
        x, y, dist = curr[0], curr[1], curr[2]

        # do for each adjacent cell
        for i in range(4):

            # if adjacent cell is valid, has path and
            # not visited yet, en-queue it.

            if isValid(x + row[i], y + col[i]) and isSafe(x + row[i], y + col[i], matrix, output) :
                output[x + row[i]][y + col[i]] = dist + 1

                pos = [x + row[i], y + col[i], dist + 1]
                q.appendleft(pos)

    # proutput matrix

    for i in range(M):
        for j in range(N):
            if output[i][j] > 0:
                print(output[i][j], end=" ")
            else:
                print(output[i][j],end=" ")
        print()

# Driver code

matrix = [['O', 'O', 'O', 'O', 'G'],
    ['O', 'W', 'W', 'O', 'O'],
    ['O', 'O', 'O', 'W', 'O'],
    ['G', 'W', 'W', 'W', 'O'],
    ['O', 'O', 'O', 'O', 'G']]

findDistance(matrix)

# This code is contributed by mohit kumar 29

```

**输出**：

```
  3  3  2  1  0
  2 -1 -1  2  1
  1  2  3 -1  2
  0 -1 -1 -1  1
  1  2  2  1  0

```

本文由 **Aditya Goel** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

