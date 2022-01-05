# 允许多步或跳跃的迷宫中的大鼠

> 原文:[https://www . geesforgeks . org/允许多步跳迷宫鼠/](https://www.geeksforgeeks.org/rat-in-a-maze-with-multiple-steps-jump-allowed/)

这是[大鼠在迷宫](https://write.geeksforgeeks.org/javapythoncc-code-for-article-backtracking-set-2-rat-in-a-maze/)
中的变异一个迷宫被给出为 N*N 个块的二元矩阵，其中源块是最左上的块即迷宫[0][0]，目的块是最右下的块即迷宫[N-1][N-1]。老鼠从源头开始，必须到达目的地。老鼠只能朝两个方向移动:向前和向下。
在迷宫矩阵中，0 表示块是死胡同，非零数表示块可以用在从源到目的地的路径中。mat[i][j]的非零值表示大鼠可以从细胞 mat[i][j]进行的最大跳跃次数。
在这个变体中，老鼠可以一次跳多步，而不是一步。
**例:**

```
Input : { {2, 1, 0, 0},
         {3, 0, 0, 1},
         {0, 1, 0, 1},
          {0, 0, 0, 1}
        }
Output : { {1, 0, 0, 0},
           {1, 0, 0, 1},
           {0, 0, 0, 1},
           {0, 0, 0, 1}
         }

Explanation 
Rat started with M[0][0] and can jump upto 2 steps right/down. 
Let's try in horizontal direction - 
M[0][1] won't lead to solution and M[0][2] is 0 which is dead end. 
So, backtrack and try in down direction. 
Rat jump down to M[1][0] which eventually leads to solution.  

Input : { 
      {2, 1, 0, 0},
      {2, 0, 0, 1},
      {0, 1, 0, 1},
      {0, 0, 0, 1}
    }
Output : Solution doesn't exist
```

**朴素算法**
朴素算法是生成从源到目的地的所有路径，并逐一检查生成的路径是否满足约束。

```
while there are untried paths
{
   generate the next path
   if this path has all blocks as non-zero
   {
      print this path;
   }
}
```

**回溯算法**

```
If destination is reached
    print the solution matrix
Else
   a) Mark current cell in solution matrix as 1\. 
   b) Move forward/jump (for each valid steps) in horizontal direction 
      and recursively check if this move leads to a solution. 
   c) If the move chosen in the above step doesn't lead to a solution
       then move down and check if this move leads to a solution. 
   d) If none of the above solutions work then unmark this cell as 0 
       (BACKTRACK) and return false.
```

**实施回溯解决方案**

## C++

```
/* C/C++ program to solve Rat in a Maze problem
using backtracking */
#include <stdio.h>

// Maze size
#define N 4

bool solveMazeUtil(int maze[N][N], int x, int y,
                                int sol[N][N]);

/* A utility function to print solution matrix
sol[N][N] */
void printSolution(int sol[N][N])
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++)
            printf(" %d ", sol[i][j]);
        printf("\n");
    }
}

/* A utility function to check if x, y is valid
index for N*N maze */
bool isSafe(int maze[N][N], int x, int y)
{
    // if (x, y outside maze) return false
    if (x >= 0 && x < N && y >= 0 &&
    y < N && maze[x][y] != 0)
        return true;

    return false;
}

/* This function solves the Maze problem using
Backtracking. It mainly uses solveMazeUtil() to
solve the problem. It returns false if no path
is possible, otherwise return true and prints
the path in the form of 1s. Please note that
there may be more than one solutions,
this function prints one of the feasible solutions.*/
bool solveMaze(int maze[N][N])
{
    int sol[N][N] = { { 0, 0, 0, 0 },
                    { 0, 0, 0, 0 },
                    { 0, 0, 0, 0 },
                    { 0, 0, 0, 0 } };

    if (solveMazeUtil(maze, 0, 0, sol) == false) {
        printf("Solution doesn't exist");
        return false;
    }

    printSolution(sol);
    return true;
}

/* A recursive utility function to solve Maze problem */
bool solveMazeUtil(int maze[N][N], int x, int y,
                                int sol[N][N])
{
    // if (x, y is goal) return true
    if (x == N - 1 && y == N - 1) {
        sol[x][y] = 1;
        return true;
    }

    // Check if maze[x][y] is valid
    if (isSafe(maze, x, y) == true) {

        // mark x, y as part of solution path
        sol[x][y] = 1;

        /* Move forward in x direction */
        for (int i = 1; i <= maze[x][y] && i < N; i++) {

            /* Move forward in x direction */
            if (solveMazeUtil(maze, x + i, y, sol) == true)
                return true;

            /* If moving in x direction doesn't give
            solution then Move down in y direction */
            if (solveMazeUtil(maze, x, y + i, sol) == true)
                return true;
        }

        /* If none of the above movements work then
        BACKTRACK: unmark x, y as part of solution
        path */
        sol[x][y] = 0;
        return false;
    }

    return false;
}

// driver program to test above function
int main()
{
    int maze[N][N] = { { 2, 1, 0, 0 },
                    { 3, 0, 0, 1 },
                    { 0, 1, 0, 1 },
                    { 0, 0, 0, 1 } };

    solveMaze(maze);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve Rat in a Maze problem
// using backtracking
class GFG
{

    // Maze size
    static int N = 4;

    /* A utility function to print solution matrix
    sol[N][N] */
    static void printSolution(int sol[][])
    {
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                System.out.printf(" %d ", sol[i][j]);
            }
            System.out.printf("\n");
        }
    }

    /* A utility function to check if x, y is valid
    index for N*N maze */
    static boolean isSafe(int maze[][], int x, int y)
    {

        // if (x, y outside maze) return false
        if (x >= 0 && x < N && y >= 0 &&
             y < N && maze[x][y] != 0)
        {
            return true;
        }

        return false;
    }

    /* This function solves the Maze problem using
    Backtracking. It mainly uses solveMazeUtil() to
    solve the problem. It returns false if no path
    is possible, otherwise return true and prints
    the path in the form of 1s. Please note that
    there may be more than one solutions,
    this function prints one of the feasible solutions.*/
    static boolean solveMaze(int maze[][])
    {
        int sol[][] = {{0, 0, 0, 0},
                       {0, 0, 0, 0},
                       {0, 0, 0, 0},
                       {0, 0, 0, 0}};

        if (solveMazeUtil(maze, 0, 0, sol) == false)
        {
            System.out.printf("Solution doesn't exist");
            return false;
        }

        printSolution(sol);
        return true;
    }

    /* A recursive utility function to solve Maze problem */
    static boolean solveMazeUtil(int maze[][], int x,
                                 int y, int sol[][])
    {
        // if (x, y is goal) return true
        if (x == N - 1 && y == N - 1)
        {
            sol[x][y] = 1;
            return true;
        }

        // Check if maze[x][y] is valid
        if (isSafe(maze, x, y) == true)
        {

            // mark x, y as part of solution path
            sol[x][y] = 1;

            /* Move forward in x direction */
            for (int i = 1; i <= maze[x][y] && i < N; i++)
            {

                /* Move forward in x direction */
                if (solveMazeUtil(maze, x + i, y, sol) == true)
                {
                    return true;
                }

                /* If moving in x direction doesn't give
                solution then Move down in y direction */
                if (solveMazeUtil(maze, x, y + i, sol) == true)
                {
                    return true;
                }
            }

            /* If none of the above movements work then
            BACKTRACK: unmark x, y as part of solution
            path */
            sol[x][y] = 0;
            return false;
        }

        return false;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int maze[][] = {{2, 1, 0, 0},
                        {3, 0, 0, 1},
                        {0, 1, 0, 1},
                        {0, 0, 0, 1}};

        solveMaze(maze);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
""" Python3 program to solve Rat in a
Maze problem using backtracking """

# Maze size
N = 4

""" A utility function to prsolution matrix
sol """
def printSolution(sol):
    for i in range(N):
        for j in range(N):
            print(sol[i][j], end = " ")
        print()

""" A utility function to check if
x, y is valid index for N*N maze """
def isSafe(maze, x, y):

    # if (x, y outside maze) return false
    if (x >= 0 and x < N and y >= 0 and
         y < N and maze[x][y] != 0):
        return True
    return False

""" This function solves the Maze problem using
Backtracking. It mainly uses solveMazeUtil() to
solve the problem. It returns false if no path
is possible, otherwise return True and prints
the path in the form of 1s. Please note that
there may be more than one solutions,
this function prints one of the feasible solutions."""
def solveMaze(maze):
    sol = [[0, 0, 0, 0],
           [0, 0, 0, 0],
           [0, 0, 0, 0],
           [0, 0, 0, 0]]
    if (solveMazeUtil(maze, 0, 0, sol) == False):
        print("Solution doesn't exist")
        return False
    printSolution(sol)
    return True

""" A recursive utility function
to solve Maze problem """
def solveMazeUtil(maze, x, y, sol):

    # if (x, y is goal) return True
    if (x == N - 1 and y == N - 1) :
        sol[x][y] = 1
        return True

    # Check if maze[x][y] is valid
    if (isSafe(maze, x, y) == True):

        # mark x, y as part of solution path
        sol[x][y] = 1

        """ Move forward in x direction """
        for i in range(1, N):
            if (i <= maze[x][y]):

                """ Move forward in x direction """
                if (solveMazeUtil(maze, x + i,
                                  y, sol) == True):
                    return True

                """ If moving in x direction doesn't give
                solution then Move down in y direction """
                if (solveMazeUtil(maze, x,
                                  y + i, sol) == True):
                    return True

        """ If none of the above movements work then
        BACKTRACK: unmark x, y as part of solution
        path """
        sol[x][y] = 0
        return False
    return False

# Driver Code
maze = [[2, 1, 0, 0],
        [3, 0, 0, 1],
        [0, 1, 0, 1],
        [0, 0, 0, 1]]
solveMaze(maze)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to solve Rat in a Maze problem
// using backtracking
using System;

class GFG
{

    // Maze size
    static int N = 4;

    /* A utility function to print
    solution matrix sol[N, N] */
    static void printSolution(int [,]sol)
    {
        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                Console.Write(" {0} ", sol[i, j]);
            }
            Console.Write("\n");
        }
    }

    /* A utility function to check if
    x, y is valid index for N*N maze */
    static Boolean isSafe(int [,]maze,
                          int x, int y)
    {

        // if (x, y outside maze) return false
        if (x >= 0 && x < N && y >= 0 &&
            y < N && maze[x, y] != 0)
        {
            return true;
        }

        return false;
    }

    /* This function solves the Maze problem using
    Backtracking. It mainly uses solveMazeUtil() to
    solve the problem. It returns false if no path
    is possible, otherwise return true and prints
    the path in the form of 1s. Please note that
    there may be more than one solutions,
    this function prints one of the feasible solutions.*/
    static Boolean solveMaze(int [,]maze)
    {
        int [,]sol = {{0, 0, 0, 0},
                      {0, 0, 0, 0},
                      {0, 0, 0, 0},
                      {0, 0, 0, 0}};

        if (solveMazeUtil(maze, 0, 0, sol) == false)
        {
            Console.Write("Solution doesn't exist");
            return false;
        }

        printSolution(sol);
        return true;
    }

    /* A recursive utility function to solve Maze problem */
    static Boolean solveMazeUtil(int [,]maze, int x,
                                 int y, int [,]sol)
    {
        // if (x, y is goal) return true
        if (x == N - 1 && y == N - 1)
        {
            sol[x, y] = 1;
            return true;
        }

        // Check if maze[x,y] is valid
        if (isSafe(maze, x, y) == true)
        {

            // mark x, y as part of solution path
            sol[x, y] = 1;

            /* Move forward in x direction */
            for (int i = 1;
                     i <= maze[x, y] && i < N; i++)
            {

                /* Move forward in x direction */
                if (solveMazeUtil(maze, x + i,
                                  y, sol) == true)
                {
                    return true;
                }

                /* If moving in x direction doesn't give
                solution then Move down in y direction */
                if (solveMazeUtil(maze, x,
                                  y + i, sol) == true)
                {
                    return true;
                }
            }

            /* If none of the above movements work then
            BACKTRACK: unmark x, y as part of solution
            path */
            sol[x, y] = 0;
            return false;
        }

        return false;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int [,]maze = {{2, 1, 0, 0},
                       {3, 0, 0, 1},
                       {0, 1, 0, 1},
                       {0, 0, 0, 1}};

        solveMaze(maze);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to solve Rat in a Maze problem
// using backtracking

    // Maze size
    let N = 4;

    /* A utility function to print solution matrix
    sol[N][N] */
    function printSolution(sol)
    {
        for (let i = 0; i < N; i++)
        {
            for (let j = 0; j < N; j++)
            {
                 document.write(sol[i][j] + " ");
            }
             document.write("<br/>");
        }
    }

    /* A utility function to check if x, y is valid
    index for N*N maze */
    function isSafe(maze, x, y)
    {

        // if (x, y outside maze) return false
        if (x >= 0 && x < N && y >= 0 &&
             y < N && maze[x][y] != 0)
        {
            return true;
        }

        return false;
    }

    /* This function solves the Maze problem using
    Backtracking. It mainly uses solveMazeUtil() to
    solve the problem. It returns false if no path
    is possible, otherwise return true and print
    the path in the form of 1s. Please note that
    there may be more than one solutions,
    this function prints one of the feasible solutions.*/
    function solveMaze(maze)
    {
        let sol = [[0, 0, 0, 0],
                       [0, 0, 0, 0],
                       [0, 0, 0, 0],
                       [0, 0, 0, 0]];

        if (solveMazeUtil(maze, 0, 0, sol) == false)
        {
             document.write("Solution doesn't exist");
            return false;
        }

        printSolution(sol);
        return true;
    }

    /* A recursive utility function to solve Maze problem */
    function solveMazeUtil(maze,  x,
                                 y, sol)
    {
        // if (x, y is goal) return true
        if (x == N - 1 && y == N - 1)
        {
            sol[x][y] = 1;
            return true;
        }

        // Check if maze[x][y] is valid
        if (isSafe(maze, x, y) == true)
        {

            // mark x, y as part of solution path
            sol[x][y] = 1;

            /* Move forward in x direction */
            for (let i = 1; i <= maze[x][y] && i < N; i++)
            {

                /* Move forward in x direction */
                if (solveMazeUtil(maze, x + i, y, sol) == true)
                {
                    return true;
                }

                /* If moving in x direction doesn't give
                solution then Move down in y direction */
                if (solveMazeUtil(maze, x, y + i, sol) == true)
                {
                    return true;
                }
            }

            /* If none of the above movements work then
            BACKTRACK: unmark x, y as part of solution
            path */
            sol[x][y] = 0;
            return false;
        }

        return false;
    }

// Driver code

        let maze = [[2, 1, 0, 0],
                        [3, 0, 0, 1],
                        [0, 1, 0, 1],
                        [0, 0, 0, 1]];

        solveMaze(maze);

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
1  0  0  0 
1  0  0  1 
0  0  0  1 
0  0  0  1
```