# 迷宫中的老鼠|使用堆栈回溯

> 原文:[https://www . geesforgeks . org/迷宫中的老鼠-回溯-使用堆栈/](https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-using-stack/)

**先决条件**–[递归](https://www.geeksforgeeks.org/recursion/)、[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)和[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)。
迷宫是由 N*M 个方块组成的二进制矩阵，在(0，0)处有一只老鼠。迷宫[0][0]老鼠想吃迷宫中某个给定区域(fx，fy)的食物。在迷宫矩阵中，0 表示该块是死胡同，1 表示该块可用于从源到目的地的路径中。老鼠可以在任何方向(不是对角)移动到任何街区，前提是街区不是死胡同。
任务是检查有没有路径，让老鼠够不着食物。不需要打印路径。
**示例** :

```
Input : maze[4][5] = {
            {1, 0, 1, 1, 0},
            {1, 1, 1, 0, 1},
            {0, 1, 0, 1, 1},
            {1, 1, 1, 1, 1}
        }
        fx = 2, fy=3
Output : Path Found!
The path can be: (0, 0) -> (1, 0) -> (1, 1) -> (2, 1) -> (3, 1) -> (3, 2)  -> (3, 3) -> (2, 3)  
```

这就是很多采访中问的著名的[迷宫中的老鼠](https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-2/)问题，可以用递归和回溯来解决。我们已经在[迷宫中的老鼠|回溯-2](https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-2/) 中讨论了这个问题的回溯解决方案。本文讨论了一种使用堆栈的迭代解法。
在前一篇文章[中](https://www.geeksforgeeks.org/rat-in-a-maze-backtracking-2/)、[递归](https://www.geeksforgeeks.org/recursion/)使用调用堆栈来保存每次递归调用的存储，然后在函数结束时弹出。我们将通过使用我们自己的堆栈来消除递归。
节点结构用于存储从该节点探索的(I，j)坐标和方向，以及下一步尝试哪个方向。

> **所用结构:**
> 
> 1.  x:节点的 x 坐标
>     
> 2.  y:节点的 y 坐标
>     
> 3.  dir:这个变量将用于告诉我们已经尝试了哪些方向，下一步选择哪个方向。我们将从“向上”开始以逆时针方式尝试所有方向。最初它将被分配 0。
>     *   如果方向=0，尝试向上方向。
>     *   如果 dir=1，尝试向左。
>     *   如果 dir=2，尝试向下。
>     *   如果 dir=3，尝试向右。

最初，我们将把索引 i=0、j=0 和 dir=0 的节点推入堆栈。我们将以逆时针方式一个接一个地向最顶端节点的所有方向移动，每次当我们尝试一条新路径时，我们都会将该节点(迷宫的区块)推入堆栈中。我们每次都会增加最顶端节点的 *dir* 变量，这样我们每次都可以尝试一个新的方向，除非所有的方向都被探索了。dir=4。如果 dir 等于 4，我们将从堆栈中弹出该节点，这意味着我们将后退一步回到我们原来的路径。
我们还将维护一个访问矩阵，该矩阵将维护迷宫的哪些块已经在路径中使用，或者换句话说，存在于堆栈中。在尝试任何方向时，我们也会检查迷宫的障碍物是否不是死胡同，是否也没有走出迷宫。
我们将在最上面的节点坐标变得等于食物坐标时这样做，这意味着我们已经到达食物，或者堆栈变空，这意味着没有可能到达食物的路径。
以下是上述方法的实施:

## C++

```
// CPP program to solve Rat in a maze
// problem with backtracking using stack

#include <cstring>
#include <iostream>
#include <stack>

using namespace std;

#define N 4
#define M 5

class node {
public:
    int x, y;
    int dir;

    node(int i, int j)
    {
        x = i;
        y = j;

        // Initially direction
        // set to 0
        dir = 0;
    }
};

// maze of n*m matrix
int n = N, m = M;

// Coordinates of food
int fx, fy;
bool visited[N][M];

bool isReachable(int maze[N][M])
{
    // Initially starting at (0, 0).
    int i = 0, j = 0;

    stack<node> s;

    node temp(i, j);

    s.push(temp);

    while (!s.empty()) {

        // Pop the top node and move to the
        // left, right, top, down or retract
        // back according the value of node's
        // dir variable.
        temp = s.top();
        int d = temp.dir;
        i = temp.x, j = temp.y;

        // Increment the direction and
        // push the node in the stack again.
        temp.dir++;
        s.pop();
        s.push(temp);

        // If we reach the Food coordinates
        // return true
        if (i == fx and j == fy) {
            return true;
        }

        // Checking the Up direction.
        if (d == 0) {
            if (i - 1 >= 0 and maze[i - 1][j] and
                                    visited[i - 1][j]) {
                node temp1(i - 1, j);
                visited[i - 1][j] = false;
                s.push(temp1);
            }
        }

        // Checking the left direction
        else if (d == 1) {
            if (j - 1 >= 0 and maze[i][j - 1] and
                                    visited[i][j - 1]) {
                node temp1(i, j - 1);
                visited[i][j - 1] = false;
                s.push(temp1);
            }
        }

        // Checking the down direction
        else if (d == 2) {
            if (i + 1 < n and maze[i + 1][j] and
                                    visited[i + 1][j]) {
                node temp1(i + 1, j);
                visited[i + 1][j] = false;
                s.push(temp1);
            }
        }
        // Checking the right direction
        else if (d == 3) {
            if (j + 1 < m and maze[i][j + 1] and
                                    visited[i][j + 1]) {
                node temp1(i, j + 1);
                visited[i][j + 1] = false;
                s.push(temp1);
            }
        }

        // If none of the direction can take
        // the rat to the Food, retract back
        // to the path where the rat came from.
        else {
            visited[temp.x][temp.y] = true;
            s.pop();
        }
    }

    // If the stack is empty and
    // no path is found return false.
    return false;
}

// Driver code
int main()
{
    // Initially setting the visited
    // array to true (unvisited)
    memset(visited, true, sizeof(visited));

    // Maze matrix
    int maze[N][M] = {
        { 1, 0, 1, 1, 0 },
        { 1, 1, 1, 0, 1 },
        { 0, 1, 0, 1, 1 },
        { 1, 1, 1, 1, 1 }
    };

    // Food coordinates
    fx = 2;
    fy = 3;

    if (isReachable(maze)) {
        cout << "Path Found!" << '\n';
    }
    else
        cout << "No Path Found!" << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve Rat in a maze
// problem with backtracking using stack
import java.util.Stack;

class Node
{
    private int x, y;
    private int dir;

    public Node(int i, int j)
    {
        this.x = i;
        this.y = j;

        // default value for direction set to 0 (Up)
        this.dir = 0;
    }

    public int getX()
    {
        return x;
    }

    public void setX(int x)
    {
        this.x = x;
    }

    public int getY()
    {
        return y;
    }

    public void setY(int y)
    {
        this.y = y;
    }

    public int getDir()
    {
        return dir;
    }

    public void setDir(int dir)
    {
        this.dir = dir;
    }
}

public class RatInMaze
{
    private static final int N = 4;
    private static final int M = 5;

    // maze of n*m matrix
    int n = N, m = M;

    private static boolean[][] visited = new boolean[N][M];

        // Driver code
    public static void main(String[] args)
    {
        // Initially setting the visited
        // array to true (unvisited)
        setVisited(true);

        // Maze matrix
        int maze[][] = {{ 1, 0, 1, 1, 0 },
                        { 1, 1, 1, 0, 1 },
                        { 0, 1, 0, 1, 1 },
                        { 1, 1, 1, 1, 1 } };

        if (isReachable(maze))
        {
            System.out.println("Path Found!\n");
        }
        else
            System.out.println("No Path Found!\n");
    }

    private static void setVisited(boolean b)
    {
        for (int i = 0; i < visited.length; i++)
        {
            for (int j = 0; j < visited[i].length; j++)
            {
                visited[i][j] = b;
            }
        }

    }

    private static boolean isReachable(int maze[][])
    {
        // Initially starting at (0, 0).
        int i = 0, j = 0;

        // Food coordinates
        // Coordinates of food
        int fx, fy;
        fx = 2;
        fy = 3;

        Stack<Node> s = new Stack<Node>();

        Node temp = new Node(i, j);

        s.push(temp);

        while (!s.empty())
        {

            // Pop the top node and move to the
            // left, right, top, down or retract
            // back according the value of node's
            // dir variable.
            temp = s.peek();
            int d = temp.getDir();
            i = temp.getX();
            j = temp.getY();

            // Increment the direction and
            // push the node in the stack again.
            temp.setDir(temp.getDir() + 1);
            s.pop();
            s.push(temp);

            // If we reach the Food coordinates
            // return true
            if (i == fx && j == fy)
            {
                return true;
            }

            if (d == 0)
            {
                // Checking the Up direction.
                if (i - 1 >= 0 && maze[i - 1][j] == 1 &&
                                        visited[i - 1][j])
                {
                    Node temp1 = new Node(i - 1, j);
                    visited[i - 1][j] = false;
                    s.push(temp1);
                }
            }
            else if (d == 1)
            {
                // Checking the left direction
                if (j - 1 >= 0 && maze[i][j - 1] == 1 &&
                                        visited[i][j - 1])
                {
                    Node temp1 = new Node(i, j - 1);
                    visited[i][j - 1] = false;
                    s.push(temp1);
                }
            }
            else if (d == 2)
            {
                // Checking the down direction
                if (i + 1 < N && maze[i + 1][j] == 1 &&
                                        visited[i + 1][j])
                {
                    Node temp1 = new Node(i + 1, j);
                    visited[i + 1][j] = false;
                    s.push(temp1);
                }
            }
            else if (d == 3)
            {
                // Checking the right direction
                if (j + 1 < M && maze[i][j + 1] == 1 &&
                                        visited[i][j + 1])
                {
                    Node temp1 = new Node(i, j + 1);
                    visited[i][j + 1] = false;
                    s.push(temp1);
                }
            }

            // If none of the direction can take
            // the rat to the Food, retract back
            // to the path where the rat came from.
            else
            {
                visited[temp.getX()][temp.getY()] = true;
                s.pop();
            }
        }

        // If the stack is empty and
        // no path is found return false.
        return false;
    }
}

// This code is contributed by nirajtechi
```

## C#

```
// C# program to solve Rat in a maze
// problem with backtracking using stack
using System;
using System.Collections.Generic;

public class Node
{
    private int x, y;
    private int dir;

    public Node(int i, int j)
    {
        this.x = i;
        this.y = j;

        // default value for direction set to 0 (Up)
        this.dir = 0;
    }

    public int getX()
    {
        return x;
    }
    public void setX(int x)
    {
        this.x = x;
    }
    public int getY()
    {
        return y;
    }
    public void setY(int y)
    {
        this.y = y;
    }
    public int getDir()
    {
        return dir;
    }
    public void setDir(int dir)
    {
        this.dir = dir;
    }
}

public class RatInMaze
{
    private static readonly int N = 4;
    private static readonly int M = 5;

    // maze of n*m matrix
    int n = N, m = M;

    private static bool [,]visited = new bool[N,M];

        // Driver code
    public static void Main(String[] args)
    {
        // Initially setting the visited
        // array to true (unvisited)
        setVisited(true);

        // Maze matrix
        int [,]maze = {{ 1, 0, 1, 1, 0 },
                        { 1, 1, 1, 0, 1 },
                        { 0, 1, 0, 1, 1 },
                        { 1, 1, 1, 1, 1 } };

        if (isReachable(maze))
        {
            Console.WriteLine("Path Found!\n");
        }
        else
            Console.WriteLine("No Path Found!\n");
    }

    private static void setVisited(bool b)
    {
        for (int i = 0; i < visited.GetLength(0); i++)
        {
            for (int j = 0; j < visited.GetLength(0); j++)
            {
                visited[i,j] = b;
            }
        }

    }

    private static bool isReachable(int [,]maze)
    {
        // Initially starting at (0, 0).
        int i = 0, j = 0;

        // Food coordinates
        // Coordinates of food
        int fx, fy;
        fx = 2;
        fy = 3;

        Stack<Node> s = new Stack<Node>();

        Node temp = new Node(i, j);

        s.Push(temp);

        while (s.Count!=0)
        {

            // Pop the top node and move to the
            // left, right, top, down or retract
            // back according the value of node's
            // dir variable.
            temp = s.Peek();
            int d = temp.getDir();
            i = temp.getX();
            j = temp.getY();

            // Increment the direction and
            // push the node in the stack again.
            temp.setDir(temp.getDir() + 1);
            s.Pop();
            s.Push(temp);

            // If we reach the Food coordinates
            // return true
            if (i == fx && j == fy)
            {
                return true;
            }

            if (d == 0)
            {
                // Checking the Up direction.
                if (i - 1 >= 0 && maze[i - 1,j] == 1 &&
                                        visited[i - 1,j])
                {
                    Node temp1 = new Node(i - 1, j);
                    visited[i - 1,j] = false;
                    s.Push(temp1);
                }
            }
            else if (d == 1)
            {
                // Checking the left direction
                if (j - 1 >= 0 && maze[i,j - 1] == 1 &&
                                        visited[i,j - 1])
                {
                    Node temp1 = new Node(i, j - 1);
                    visited[i,j - 1] = false;
                    s.Push(temp1);
                }
            }
            else if (d == 2)
            {
                // Checking the down direction
                if (i + 1 < N && maze[i + 1,j] == 1 &&
                                        visited[i + 1,j])
                {
                    Node temp1 = new Node(i + 1, j);
                    visited[i + 1,j] = false;
                    s.Push(temp1);
                }
            }
            else if (d == 3)
            {
                // Checking the right direction
                if (j + 1 < M && maze[i,j + 1] == 1 &&
                                        visited[i,j + 1])
                {
                    Node temp1 = new Node(i, j + 1);
                    visited[i,j + 1] = false;
                    s.Push(temp1);
                }
            }

            // If none of the direction can take
            // the rat to the Food, retract back
            // to the path where the rat came from.
            else
            {
                visited[temp.getX(),temp.getY()] = true;
                s.Pop();
            }
        }

        // If the stack is empty and
        // no path is found return false.
        return false;
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# CPP program to solve Rat in a maze
# problem with backtracking using stack

N=4
M=5

class node:
    def __init__(self,i,j):
        self.x=i
        self.y=j
        self.dirn=0

# maze of n*m matrix
n = N; m = M

# Coordinates of food
fx=0; fy=0
visited=[[True]*N for _ in range(M)]

def isReachable(maze):

    # Initially starting at (0, 0).
    i = 0; j = 0

    s=[]

    temp=node(i, j)

    s.append(temp)

    while s:

        # Pop the top node and move to the
        # left, right, top, down or retract
        # back according the value of node's
        # dirn variable.
        temp = s.pop()
        d = temp.dirn
        i = temp.x; j = temp.y

        # Increment the direction and
        # push the node in the stack again.
        temp.dirn+=1
        s.append(temp)

        # If we reach the Food coordinates
        # return true
        if (i == fx and j == fy):
            return True

        # Checking the Up direction.
        if (d == 0):
            if (i - 1 >= 0 and maze[i - 1][j] and visited[i - 1][j]):
                temp1=node(i - 1, j)
                visited[i - 1][j] = False
                s.append(temp1)

        # Checking the left direction
        elif (d == 1):
            if(j - 1 >= 0 and maze[i][j - 1] and visited[i][j - 1]):
                temp1=node(i, j - 1)
                visited[i][j - 1] = False
                s.append(temp1)

        # Checking the down direction
        elif (d == 2):
            if(i + 1 < n and maze[i + 1][j] and visited[i + 1][j]):
                temp1=node(i + 1, j)
                visited[i + 1][j] = False
                s.append(temp1)

        # Checking the right direction
        elif (d == 3):
            if (j + 1 < m and maze[i][j + 1] and visited[i][j + 1]):
                temp1=node(i, j + 1)
                visited[i][j + 1] = False
                s.append(temp1)

        # If none of the direction can take
        # the rat to the Food, retract back
        # to the path where the rat came from.
        else:
            visited[temp.x][temp.y] = True
            s.pop()

    # If the stack is empty and
    # no path is found return false.
    return False

# Driver code
if __name__ == '__main__':

    # Initially setting the visited
    # array to true (unvisited)

    # Maze matrix
    maze = [
        [ 1, 0, 1, 1, 0 ],
        [ 1, 1, 1, 0, 1 ],
        [ 0, 1, 0, 1, 1 ],
        [ 1, 1, 1, 1, 1 ]
    ]

    # Food coordinates
    fx = 2
    fy = 3

    if (isReachable(maze)):
        print("Path Found!")
    else:
        print("No Path Found!")
```

**Output:** 

```
Path Found!
```

**注意:**我们也可以通过从堆栈中弹出节点来打印路径，然后以相反的顺序打印。
**时间复杂度:** O( ![2 ^ {N * M} ](img/56ea601dda95972459bf4115469e1a2c.png "Rendered by QuickLaTeX.com"))。
**辅助空间:** O( ![N*M ](img/dba42a10005026e72e13fc11c8643763.png "Rendered by QuickLaTeX.com"))。