# 在迷宫中寻找从角落细胞到中间细胞的路径

> 原文:[https://www . geeksforgeeks . org/find-path-从角落单元格到中间单元格-在迷宫中/](https://www.geeksforgeeks.org/find-paths-from-corner-cell-to-middle-cell-in-maze/)

给定一个包含正数的正方形迷宫，找出从一个角单元(四个极端角中的任何一个)到中间单元的所有路径。我们可以从一个单元在 4 个方向上精确地移动 n 步，即北、东、西、南，其中 **n 是单元的值**，

我们可以从单元格 mat[i][j]移动到 mat[i+n][j]、mat[i][j+n]和 mat[i][j-n]，其中 n 是 mat[i][j]的值。

例子

```
Input:  9 x 9 maze
[ 3, 5, 4, 4, 7, 3, 4, 6, 3 ]
[ 6, 7, 5, 6, 6, 2, 6, 6, 2 ]
[ 3, 3, 4, 3, 2, 5, 4, 7, 2 ]
[ 6, 5, 5, 1, 2, 3, 6, 5, 6 ]
[ 3, 3, 4, 3, 0, 1, 4, 3, 4 ]
[ 3, 5, 4, 3, 2, 2, 3, 3, 5 ]
[ 3, 5, 4, 3, 2, 6, 4, 4, 3 ]
[ 3, 5, 1, 3, 7, 5, 3, 6, 4 ]
[ 6, 2, 4, 3, 4, 5, 4, 5, 1 ]

Output:
(0, 0) -> (0, 3) -> (0, 7) -> 
(6, 7) -> (6, 3) -> (3, 3) -> 
(3, 4) -> (5, 4) -> (5, 2) -> 
(1, 2) -> (1, 7) -> (7, 7) ->
(7, 1) -> (2, 1) -> (2, 4) -> 
(4, 4) -> MID
```

这个想法是使用回溯。我们从迷宫的每个角落单元开始，递归地检查它是否通向解。以下是回溯算法–
如果到达目的地

1.  打印路径

其他

1.  将当前单元格标记为已访问，并将其添加到路径数组中。
2.  在所有 4 个允许的方向上前进，并递归地检查它们中是否有任何一个导致解决方案。
3.  如果以上解决方案都不起作用，则将此单元格标记为不可见，并将其从路径数组中删除。

下面是上述方法的实现:

## C++

```
// C++ program to find a path from corner cell to
// middle cell in maze containing positive numbers
#include <bits/stdc++.h>
using namespace std;

// Rows and columns in given maze
#define N 9

// check whether given cell is a valid cell or not.
bool isValid(set<pair<int, int> > visited,
             pair<int, int> pt)
{
    // check if cell is not visited yet to
    // avoid cycles (infinite loop) and its
    // row and column number is in range
    return (pt.first >= 0) && (pt.first  < N) &&
           (pt.second >= 0) && (pt.second < N) &&
           (visited.find(pt) == visited.end());
}

// Function to print path from source to middle coordinate
void printPath(list<pair<int, int> > path)
{
    for (auto it = path.begin(); it != path.end(); it++)
        cout << "(" << it->first << ", "
             << it->second << ") -> ";

    cout << "MID" << endl << endl;
}

// For searching in all 4 direction
int row[] = {-1, 1, 0, 0};
int col[] = { 0, 0, -1, 1};

// Coordinates of 4 corners of matrix
int _row[] = { 0, 0, N-1, N-1};
int _col[] = { 0, N-1, 0, N-1};

void findPathInMazeUtil(int maze[N][N],
                list<pair<int, int> > &path,
                set<pair<int, int> > &visited,
                pair<int, int> &curr)
{
    // If we have reached the destination cell.
    // print the complete path
    if (curr.first == N / 2 && curr.second == N / 2)
    {
        printPath(path);
        return;
    }

    // consider each direction
    for (int i = 0; i < 4; ++i)
    {
        // get value of current cell
        int n = maze[curr.first][curr.second];

        // We can move N cells in either of 4 directions
        int x = curr.first + row[i]*n;
        int y = curr.second + col[i]*n;

        // Constructs a pair object with its first element
        // set to x and its second element set to y
        pair<int, int> next = make_pair(x, y);

        // if valid pair
        if (isValid(visited, next))
        {
            // mark cell as visited
            visited.insert(next);

            // add cell to current path
            path.push_back(next);

            // recuse for next cell
            findPathInMazeUtil(maze, path, visited, next);

            // backtrack
            path.pop_back();

            // remove cell from current path
            visited.erase(next);
        }
    }
}

// Function to find a path from corner cell to
// middle cell in maze containing positive numbers
void findPathInMaze(int maze[N][N])
{
    // list to store complete path
    // from source to destination
    list<pair<int, int> > path;

    // to store cells already visisted in current path
    set<pair<int, int> > visited;

    // Consider each corners as the starting
    // point and search in maze
    for (int i = 0; i < 4; ++i)
    {
        int x = _row[i];
        int y = _col[i];

        // Constructs a pair object
        pair<int, int> pt = make_pair(x, y);

        // mark cell as visited
        visited.insert(pt);

        // add cell to current path
        path.push_back(pt);

        findPathInMazeUtil(maze, path, visited, pt);

        // backtrack
        path.pop_back();

        // remove cell from current path
        visited.erase(pt);
    }
}

int main()
{
    int maze[N][N] =
    {
        { 3, 5, 4, 4, 7, 3, 4, 6, 3 },
        { 6, 7, 5, 6, 6, 2, 6, 6, 2 },
        { 3, 3, 4, 3, 2, 5, 4, 7, 2 },
        { 6, 5, 5, 1, 2, 3, 6, 5, 6 },
        { 3, 3, 4, 3, 0, 1, 4, 3, 4 },
        { 3, 5, 4, 3, 2, 2, 3, 3, 5 },
        { 3, 5, 4, 3, 2, 6, 4, 4, 3 },
        { 3, 5, 1, 3, 7, 5, 3, 6, 4 },
        { 6, 2, 4, 3, 4, 5, 4, 5, 1 }
    };

    findPathInMaze(maze);

    return 0;
}
```

**输出:**

```
(0, 0) -> (0, 3) -> (0, 7) -> 
(6, 7) -> (6, 3) -> (3, 3) -> 
(3, 4) -> (5, 4) -> (5, 2) -> 
(1, 2) -> (1, 7) -> (7, 7) ->
(7, 1) -> (2, 1) -> (2, 4) -> 
(4, 4) -> MID
```

**更好的方法:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a path from corner cell to
// middle cell in maze containing positive numbers
import java.io.*;

class GFG {
    public static void main (String[] args) {

        // Creating the maze
        int[][] maze = {
            { 3, 5, 4, 4, 7, 3, 4, 6, 3 },
            { 6, 7, 5, 6, 6, 2, 6, 6, 2 },
            { 3, 3, 4, 3, 2, 5, 4, 7, 2 },
            { 6, 5, 5, 1, 2, 3, 6, 5, 6 },
            { 3, 3, 4, 3, 0, 1, 4, 3, 4 },
            { 3, 5, 4, 3, 2, 2, 3, 3, 5 },
            { 3, 5, 4, 3, 2, 6, 4, 4, 3 },
            { 3, 5, 1, 3, 7, 5, 3, 6, 4 },
            { 6, 2, 4, 3, 4, 5, 4, 5, 1 }
        };

        // Calling the printPath function
        printPath(maze,0,0,"");
    }

    public static void printPath(int[][] maze, int i, int j, String ans){

        // If we reach the center cell
        if (i == maze.length/2 && j==maze.length/2){

            // Make the final answer, Print the
                // final answer and Return
            ans += "("+i+", "+j+") -> MID";
            System.out.println(ans);
            return;
        }

        // If the element at the current position
            // in maze is 0, simply Return as it has
            // been visited before.
        if (maze[i][j]==0){
            return;
        }

        // If element is non-zero, then note
            // the element in variable 'k'
        int k = maze[i][j];

        // Mark the cell visited by making the
            // element 0\. Don't worry, the element
            // is safe in 'k'
        maze[i][j]=0;

        // Make recursive calls in all 4
            // directions pro-actively i.e. if the next
            // cell lies in maze or not. Right call
        if (j+k<maze.length){
            printPath(maze, i, j+k, ans+"("+i+", "+j+") -> ");
        }

        // down call
        if (i+k<maze.length){
            printPath(maze, i+k, j, ans+"("+i+", "+j+") -> ");
        }

        // left call
        if (j-k>0){
            printPath(maze, i, j-k, ans+"("+i+", "+j+") -> ");
        }

        // up call
        if (i-k>0){
            printPath(maze, i-k, j, ans+"("+i+", "+j+") -> ");
        }

        // Unmark the visited cell by substituting
            // its original value from 'k'
        maze[i][j] = k;
    }

}
```

## 蟒蛇 3

```
# Python program to find a path from corner cell to
# middle cell in maze containing positive numbers
def printPath(maze, i, j, ans):

    # If we reach the center cell
    if (i == len(maze) // 2 and j == len(maze) // 2):

        # Make the final answer, Print
        # final answer and Return
        ans += "(" + str(i) + ", " + str(j) + ") -> MID";
        print(ans);
        return;

    # If the element at the current position
    # in maze is 0, simply Return as it has
    # been visited before.
    if (maze[i][j] == 0):
        return;

    # If element is non-zero, then note
    # the element in variable 'k'
    k = maze[i][j];

    # Mark the cell visited by making the
    # element 0\. Don't worry, the element
    # is safe in 'k'
    maze[i][j] = 0;

    # Make recursive calls in all 4
    # directions pro-actively i.e. if the next
    # cell lies in maze or not. Right call
    if (j + k < len(maze)):
        printPath(maze, i, j + k, ans + "(" + str(i) + ", " + str(j) + ") -> ");

    # down call
    if (i + k < len(maze)):
        printPath(maze, i + k, j, ans + "(" + str(i) + ", " + str(j) + ") -> ");

    # left call
    if (j - k > 0):
        printPath(maze, i, j - k, ans + "(" + str(i) + ", " + str(j) + ") -> ");

    # up call
    if (i - k > 0):
        printPath(maze, i - k, j, ans + "(" + str(i) + ", " + str(j) + ") -> ");

    # Unmark the visited cell by substituting
    # its original value from 'k'
    maze[i][j] = k;

    # Driver code
if __name__ == '__main__':

    # Creating the maze
    maze = [[ 3, 5, 4, 4, 7, 3, 4, 6, 3 ],[ 6, 7, 5, 6, 6, 2, 6, 6, 2 ],[ 3, 3, 4, 3, 2, 5, 4, 7, 2 ],
            [ 6, 5, 5, 1, 2, 3, 6, 5, 6 ],[ 3, 3, 4, 3, 0, 1, 4, 3, 4 ],[ 3, 5, 4, 3, 2, 2, 3, 3, 5 ],
            [ 3, 5, 4, 3, 2, 6, 4, 4, 3 ],[ 3, 5, 1, 3, 7, 5, 3, 6, 4 ],[ 6, 2, 4, 3, 4, 5, 4, 5, 1 ]] ;

    # Calling the printPath function
    printPath(maze, 0, 0, "");

# This code contributed by gauravrajput1
```

## C#

```
// C# program to find a path from corner
// cell to middle cell in maze containing
// positive numbers
using System;

class GFG{

// Driver Code   
public static void Main(String[] args)
{

    // Creating the maze
    int[,] maze = {
        { 3, 5, 4, 4, 7, 3, 4, 6, 3 },
        { 6, 7, 5, 6, 6, 2, 6, 6, 2 },
        { 3, 3, 4, 3, 2, 5, 4, 7, 2 },
        { 6, 5, 5, 1, 2, 3, 6, 5, 6 },
        { 3, 3, 4, 3, 0, 1, 4, 3, 4 },
        { 3, 5, 4, 3, 2, 2, 3, 3, 5 },
        { 3, 5, 4, 3, 2, 6, 4, 4, 3 },
        { 3, 5, 1, 3, 7, 5, 3, 6, 4 },
        { 6, 2, 4, 3, 4, 5, 4, 5, 1 }
    };

    // Calling the printPath function
    printPath(maze, 0, 0, "");
}

public static void printPath(int[,] maze, int i,
                             int j, String ans)
{

    // If we reach the center cell
    if (i == maze.GetLength(0) / 2 &&
        j == maze.GetLength(1) / 2)
    {

        // Make the readonly answer, Print the
        // readonly answer and Return
        ans += "(" + i + ", " + j + ") -> MID";
        Console.WriteLine(ans);
        return;
    }

    // If the element at the current position
    // in maze is 0, simply Return as it has
    // been visited before.
    if (maze[i, j] == 0)
    {
        return;
    }

    // If element is non-zero, then note
    // the element in variable 'k'
    int k = maze[i, j];

    // Mark the cell visited by making the
    // element 0\. Don't worry, the element
    // is safe in 'k'
    maze[i, j] = 0;

    // Make recursive calls in all 4
    // directions pro-actively i.e. if the next
    // cell lies in maze or not. Right call
    if (j + k < maze.GetLength(1))
    {
        printPath(maze, i, j + k,
                  ans + "(" + i +
                  ", " + j + ") -> ");
    }

    // Down call
    if (i + k < maze.GetLength(0))
    {
        printPath(maze, i + k, j,
                  ans + "(" + i +
                  ", " + j + ") -> ");
    }

    // Left call
    if (j - k > 0)
    {
        printPath(maze, i, j - k,
                  ans + "(" + i +
                  ", " + j + ") -> ");
    }

    // Up call
    if (i - k > 0)
    {
        printPath(maze, i - k, j,
                  ans + "(" + i +
                  ", " + j + ") -> ");
    }

    // Unmark the visited cell by substituting
    // its original value from 'k'
    maze[i, j] = k;
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to find a path from corner cell to
// middle cell in maze containing positive numbers

function printPath( maze,i,j,ans)
{
    // If we reach the center cell
        if (i == Math.floor(maze.length/2) && j == Math.floor(maze.length/2))
        {

            // Make the final answer, Print the
                // final answer and Return
            ans += "("+i+", "+j+") -> MID";
            document.write(ans+"<br>");
            return;
        }

        // If the element at the current position
            // in maze is 0, simply Return as it has
            // been visited before.
        if (maze[i][j] == 0){
            return;
        }

        // If element is non-zero, then note
            // the element in variable 'k'
        let k = maze[i][j];

        // Mark the cell visited by making the
            // element 0\. Don't worry, the element
            // is safe in 'k'
        maze[i][j] = 0;

        // Make recursive calls in all 4
            // directions pro-actively i.e. if the next
            // cell lies in maze or not. Right call
        if (j + k < maze.length){
            printPath(maze, i, j+k, ans+"("+i+", "+j+") -> ");
        }

        // down call
        if (i + k < maze.length){
            printPath(maze, i+k, j, ans+"("+i+", "+j+") -> ");
        }

        // left call
        if (j-k>0){
            printPath(maze, i, j-k, ans+"("+i+", "+j+") -> ");
        }

        // up call
        if (i-k>0){
            printPath(maze, i-k, j, ans+"("+i+", "+j+") -> ");
        }

        // Unmark the visited cell by substituting
            // its original value from 'k'
        maze[i][j] = k;
}

let maze = [[ 3, 5, 4, 4, 7, 3, 4, 6, 3 ],[ 6, 7, 5, 6, 6, 2, 6, 6, 2 ],[ 3, 3, 4, 3, 2, 5, 4, 7, 2 ],
            [ 6, 5, 5, 1, 2, 3, 6, 5, 6 ],[ 3, 3, 4, 3, 0, 1, 4, 3, 4 ],[ 3, 5, 4, 3, 2, 2, 3, 3, 5 ],
            [ 3, 5, 4, 3, 2, 6, 4, 4, 3 ],[ 3, 5, 1, 3, 7, 5, 3, 6, 4 ],[ 6, 2, 4, 3, 4, 5, 4, 5, 1 ]] ;
printPath(maze, 0, 0, "");

// This code is contributed by unknown2108
</script>
```

**输出**:

```
(0, 0) -> (0, 3) -> (0, 7) -> 
(6, 7) -> (6, 3) -> (3, 3) ->
(3, 4) -> (5, 4) -> (5, 2) ->
(1, 2) -> (1, 7) -> (7, 7) -> 
(7, 1) -> (2, 1) -> (2, 4) -> 
(4, 4) -> MID
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息