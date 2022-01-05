# 打印 mXn 矩阵从左上角到右下角的所有可能路径

> 原文:[https://www . geesforgeks . org/print-所有可能的路径-从 a-mxn-matrix 的左上角到右下角/](https://www.geeksforgeeks.org/print-all-possible-paths-from-top-left-to-bottom-right-of-a-mxn-matrix/)

问题是打印 mXn 矩阵从左上方到右下方的所有可能路径，限制条件是从每个单元格 ***只能向右或向下移动*** 。

**例:**

```
Input : 1 2 3
        4 5 6
Output : 1 4 5 6
         1 2 5 6
         1 2 3 6

Input : 1 2 
        3 4
Output : 1 2 4
         1 3 4
```

该算法是一个简单的递归算法，从每个单元格首先通过向下打印所有路径，然后通过向右打印所有路径。对遇到的每个单元格递归执行此操作。

以下是上述算法的实现。

## C++

```
// C++ program to Print all possible paths from
// top left to bottom right of a mXn matrix
#include<iostream>

using namespace std;

/* mat:  Pointer to the starting of mXn matrix
   i, j: Current position of the robot (For the first call use 0,0)
   m, n: Dimensions of given the matrix
   pi:   Next index to be filed in path array
   *path[0..pi-1]: The path traversed by robot till now (Array to hold the
                  path need to have space for at least m+n elements) */
void printAllPathsUtil(int *mat, int i, int j, int m, int n, int *path, int pi)
{
    // Reached the bottom of the matrix so we are left with
    // only option to move right
    if (i == m - 1)
    {
        for (int k = j; k < n; k++)
            path[pi + k - j] = *((mat + i*n) + k);
        for (int l = 0; l < pi + n - j; l++)
            cout << path[l] << " ";
        cout << endl;
        return;
    }

    // Reached the right corner of the matrix we are left with
    // only the downward movement.
    if (j == n - 1)
    {
        for (int k = i; k < m; k++)
            path[pi + k - i] = *((mat + k*n) + j);
        for (int l = 0; l < pi + m - i; l++)
            cout << path[l] << " ";
        cout << endl;
        return;
    }

    // Add the current cell to the path being generated
    path[pi] = *((mat + i*n) + j);

    // Print all the paths that are possible after moving down
    printAllPathsUtil(mat, i+1, j, m, n, path, pi + 1);

    // Print all the paths that are possible after moving right
    printAllPathsUtil(mat, i, j+1, m, n, path, pi + 1);

    // Print all the paths that are possible after moving diagonal
    // printAllPathsUtil(mat, i+1, j+1, m, n, path, pi + 1);
}

// The main function that prints all paths from top left to bottom right
// in a matrix 'mat' of size mXn
void printAllPaths(int *mat, int m, int n)
{
    int *path = new int[m+n];
    printAllPathsUtil(mat, 0, 0, m, n, path, 0);
}

// Driver program to test above functions
int main()
{
    int mat[2][3] = { {1, 2, 3}, {4, 5, 6} };
    printAllPaths(*mat, 2, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
// Java program to Print all possible paths from
// top left to bottom right of a mXn matrix
public class MatrixTraversal
{

    private static void printMatrix(int mat[][], int m, int n,
                                    int i, int j, List<Integer> list)
    {
          //return if i or j crosses matrix size
        if(i > m || j > n)
            return;
        list.add(mat[i][j]);
        if(i == m && j == n){
            System.out.println(list);
        }
        printMatrix(mat, m, n, i+1, j, list);
        printMatrix(mat, m, n, i, j+1, list);
        list.remove(list.size()-1);

    }

    // Driver code
    public static void main(String[] args)
    {
        int m = 2;
        int n = 3;
        int mat[][] = { { 1, 2, 3 },
                        { 4, 5, 6 } };
          List<Integer> list = new ArrayList<>();
        printMatrix(mat, m-1, n-1, 0, 0, list);
    }
}
//This article is contributed by Harneet
```

## 蟒蛇 3

```
# Python3 program to Print all possible paths from
# top left to bottom right of a mXn matrix

'''
/* mat: Pointer to the starting of mXn matrix
i, j: Current position of the robot
     (For the first call use 0, 0)
m, n: Dimensions of given the matrix
pi: Next index to be filed in path array
*path[0..pi-1]: The path traversed by robot till now
                (Array to hold the path need to have
                 space for at least m+n elements) */
'''
def printAllPathsUtil(mat, i, j, m, n, path, pi):

    # Reached the bottom of the matrix
    # so we are left with only option to move right
    if (i == m - 1):
        for k in range(j, n):
            path[pi + k - j] = mat[i][k]

        for l in range(pi + n - j):
            print(path[l], end = " ")
        print()
        return

    # Reached the right corner of the matrix
    # we are left with only the downward movement.
    if (j == n - 1):

        for k in range(i, m):
            path[pi + k - i] = mat[k][j]

        for l in range(pi + m - i):
            print(path[l], end = " ")
        print()
        return

    # Add the current cell
    # to the path being generated
    path[pi] = mat[i][j]

    # Print all the paths
    # that are possible after moving down
    printAllPathsUtil(mat, i + 1, j, m, n, path, pi + 1)

    # Print all the paths
    # that are possible after moving right
    printAllPathsUtil(mat, i, j + 1, m, n, path, pi + 1)

    # Print all the paths
    # that are possible after moving diagonal
    # printAllPathsUtil(mat, i+1, j+1, m, n, path, pi + 1);

# The main function that prints all paths
# from top left to bottom right
# in a matrix 'mat' of size mXn
def printAllPaths(mat, m, n):

    path = [0 for i in range(m + n)]
    printAllPathsUtil(mat, 0, 0, m, n, path, 0)

# Driver Code
mat = [[1, 2, 3],
       [4, 5, 6]]

printAllPaths(mat, 2, 3)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to Print all possible paths from
// top left to bottom right of a mXn matrix
using System;

public class MatrixTraversal
{

    /* mat: Pointer to the starting of mXn matrix
i, j: Current position of the robot (For the first call use 0,0)
m, n: Dimensions of given the matrix
pi: Next index to be filed in path array
*path[0..pi-1]: The path traversed by robot till now (Array to hold the
                path need to have space for at least m+n elements) */
    private static void printMatrix(int [,]mat, int m, int n,
                                    int i, int j, int []path, int idx)
    {
        path[idx] = mat[i,j];

        // Reached the bottom of the matrix so we are left with
        // only option to move right
        if (i == m - 1)
        {
            for (int k = j + 1; k < n; k++)
            {
                path[idx + k - j] = mat[i,k];
            }
            for (int l = 0; l < idx + n - j; l++)
            {
                Console.Write(path[l] + " ");
            }
            Console.WriteLine();
            return;
        }

        // Reached the right corner of the matrix we are left with
        // only the downward movement.
        if (j == n - 1)
        {
            for (int k = i + 1; k < m; k++)
            {
                path[idx + k - i] = mat[k,j];
            }
            for (int l = 0; l < idx + m - i; l++)
            {
                Console.Write(path[l] + " ");
            }
            Console.WriteLine();
            return;
        }

        // Print all the paths that are possible after moving down
        printMatrix(mat, m, n, i + 1, j, path, idx + 1);

        // Print all the paths that are possible after moving right
        printMatrix(mat, m, n, i, j + 1, path, idx + 1);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int m = 2;
        int n = 3;
        int [,]mat = { { 1, 2, 3 },
                        { 4, 5, 6 } };
        int maxLengthOfPath = m + n - 1;
        printMatrix(mat, m, n, 0, 0, new int[maxLengthOfPath], 0);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to Print all possible paths from
// top left to bottom right of a mXn matrix

/* mat:  Pointer to the starting of mXn matrix
   i, j: Current position of the robot (For the first call use 0,0)
   m, n: Dimensions of given the matrix
   pi:   Next index to be filed in path array
   *path[0..pi-1]: The path traversed by robot till now (Array to hold the
                  path need to have space for at least m+n elements) */
function printMatrix(mat,m,n,i,j,path,idx)
{
    path[idx] = mat[i][j];

         // Reached the bottom of the matrix so we are left with
        // only option to move right
        if (i == m - 1)
        {
            for (let k = j + 1; k < n; k++)
            {
                path[idx + k - j] = mat[i][k];
            }
            for (let l = 0; l < idx + n - j; l++)
            {
                document.write(path[l] + " ");
            }
            document.write("<br>");
            return;
        }

        // Reached the right corner of the matrix we are left with
        // only the downward movement.
        if (j == n - 1)
        {
            for (let k = i + 1; k < m; k++)
            {
                path[idx + k - i] = mat[k][j];
            }
            for (let l = 0; l < idx + m - i; l++)
            {
                document.write(path[l] + " ");
            }
            document.write();
            return;
        }
        // Print all the paths that are possible after moving down
        printMatrix(mat, m, n, i + 1, j, path, idx + 1);

         // Print all the paths that are possible after moving right
        printMatrix(mat, m, n, i, j + 1, path, idx + 1);
}

// Driver code
let m = 2;
let n = 3;
let mat = [[ 1, 2, 3 ],
[ 4, 5, 6 ]];
let maxLengthOfPath = m + n - 1;
printMatrix(mat, m, n, 0, 0, new Array(maxLengthOfPath), 0);

// This code is contributed by ab2127
</script>
```

**Output**

```
1 4 5 6 
1 2 5 6 
1 2 3 6 
```

请注意，在上面的代码中，printAllPathsUtil()的最后一行是注释的，如果我们取消对这一行的注释，我们将得到从 nXm 矩阵的左上角到右下角的所有路径，如果对角移动也是允许的话。此外，如果不允许移动到某些单元格，则可以通过将限制数组传递给上述函数来改进相同的代码，这只是一个练习。

本文由 **Hariprasad NG** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息

## c++

```
// C++ program to Print all possible paths from 
// top left to bottom right of a mXn matrix
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> allPaths;

void findPathsUtil(vector<vector<int>> maze, int m,
                                 int n, int i, int j,
                          vector<int> path, int index)
{

    // If we reach the bottom of maze,
    // we can only move right
    if (i == m - 1)
    {
        for(int k = j; k < n; k++)
        {

            //path.append(maze[i][k])
            path[index + k - j] = maze[i][k];
        }

        // If we hit this block, it means one
        // path is completed. Add it to paths
        // list and print
        cout << "[" << path[0] << ", ";
        for(int z = 1; z < path.size() - 1; z++)
        {
            cout << path[z] << ", ";
        }
        cout << path[path.size() - 1] << "]" << endl;
        allPaths.push_back(path);
        return;
    }

    // If we reach to the right most
    // corner, we can only move down
    if (j == n - 1)
    {
        for(int k = i; k < m; k++)
        {
            path[index + k - i] = maze[k][j];
        }

        //path.append(maze[j][k])
        // If we hit this block, it means one
        // path is completed. Add it to paths
        // list and print
        cout << "[" << path[0] << ", ";
        for(int z = 1; z < path.size() - 1; z++)
        {
            cout << path[z] << ", ";
        }
        cout << path[path.size() - 1] << "]" << endl;
        allPaths.push_back(path);
        return;
    }

    // Add current element to the path list
    //path.append(maze[i][j])
    path[index] = maze[i][j];

    // Move down in y direction and call
    // findPathsUtil recursively
    findPathsUtil(maze, m, n, i + 1,
                  j, path, index + 1);

    // Move down in y direction and
    // call findPathsUtil recursively
    findPathsUtil(maze, m, n, i, j + 1,
                        path, index + 1);
}

void findPaths(vector<vector<int>> maze,
                       int m, int n)
{
    vector<int> path(m + n - 1, 0);
    findPathsUtil(maze, m, n, 0, 0, path, 0);
}

// Driver Code
int main()
{
    vector<vector<int>> maze{ { 1, 2, 3 },
                              { 4, 5, 6 },
                              { 7, 8, 9 } };
    findPaths(maze, 3, 3);

    //print(allPaths)
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java

```
// Java program to Print all possible paths from 
// top left to bottom right of a mXn matrix
import java.io.*;
import java.util.*;
class GFG
{
  static ArrayList<ArrayList<Integer>> allPaths =
    new ArrayList<ArrayList<Integer>>();
  static void findPathsUtil(ArrayList<ArrayList<Integer>> maze,
                            int m, int n, int i,int j,
                            ArrayList<Integer> path,int index)
  {

    // If we reach the bottom of maze,
    // we can only move right
    if(i == m - 1)
    {
      for(int k = j; k < n; k++)
      {

        // path.append(maze[i][k])
        path.set(index + k - j, maze.get(i).get(k));

      }

      // If we hit this block, it means one
      // path is completed. Add it to paths
      // list and print
      System.out.print("[" + path.get(0) + ", ");
      for(int z = 1; z < path.size() - 1; z++)
      {
        System.out.print(path.get(z) + ", ");
      }
      System.out.println(path.get(path.size() - 1) + "]");
      allPaths.add(path);
      return;
    }

    // If we reach to the right most
    // corner, we can only move down
    if(j == n - 1)
    {
      for(int k = i; k < m; k++)
      {
        path.set(index + k - i,maze.get(k).get(j));
      }

      // path.append(maze[j][k])
      // If we hit this block, it means one
      // path is completed. Add it to paths
      // list and print
      System.out.print("[" + path.get(0) + ", ");
      for(int z = 1; z < path.size() - 1; z++)
      {
        System.out.print(path.get(z) + ", ");

      }
      System.out.println(path.get(path.size() - 1) + "]");
      allPaths.add(path);
      return;
    }

    // Add current element to the path list
    //path.append(maze[i][j])
    path.set(index,maze.get(i).get(j));

    // Move down in y direction and call
    // findPathsUtil recursively
    findPathsUtil(maze, m, n, i + 1, j, path, index + 1);

    // Move down in y direction and
    // call findPathsUtil recursively
    findPathsUtil(maze, m, n, i, j + 1, path, index + 1);

  }
  static void findPaths(ArrayList<ArrayList<Integer>> maze,
                        int m, int n)
  {
    ArrayList<Integer> path = new ArrayList<Integer>();
    for(int i = 0; i < m + n - 1; i++)
    {
      path.add(0);
    }
    findPathsUtil(maze, m, n, 0, 0, path, 0);
  }

  // Driver code
  public static void main (String[] args)
  {
    ArrayList<ArrayList<Integer>> maze =
      new ArrayList<ArrayList<Integer>>();
    maze.add(new ArrayList<Integer>
             (Arrays.asList(1,2,3)));
    maze.add(new ArrayList<Integer>
             (Arrays.asList(4,5,6)));
    maze.add(new ArrayList<Integer>
             (Arrays.asList(7,8,9)));

    findPaths(maze, 3, 3);       
  }
}

// This code is contributed by avanitrachhadiya2155
```

## python 3

```
# Python3 program to Print all possible paths from
# top left to bottom right of a mXn matrix
allPaths = []
def findPaths(maze,m,n):
    path = [0 for d in range(m+n-1)]
    findPathsUtil(maze,m,n,0,0,path,0)

def findPathsUtil(maze,m,n,i,j,path,index):
    global allPaths
    # if we reach the bottom of maze, we can only move right
    if i==m-1:
        for k in range(j,n):
            #path.append(maze[i][k])
            path[index+k-j] = maze[i][k]
        # if we hit this block, it means one path is completed.
        # Add it to paths list and print
        print(path)
        allPaths.append(path)
        return
    # if we reach to the right most corner, we can only move down
    if j == n-1:
        for k in range(i,m):
            path[index+k-i] = maze[k][j]
          #path.append(maze[j][k])
        # if we hit this block, it means one path is completed.
        # Add it to paths list and print
        print(path)
        allPaths.append(path)
        return

    # add current element to the path list
    #path.append(maze[i][j])
    path[index] = maze[i][j]

    # move down in y direction and call findPathsUtil recursively
    findPathsUtil(maze, m, n, i+1, j, path, index+1)

    # move down in y direction and call findPathsUtil recursively
    findPathsUtil(maze, m, n, i, j+1, path, index+1)

if __name__ == '__main__':
    maze = [[1,2,3],
            [4,5,6],
            [7,8,9]]
    findPaths(maze,3,3)
    #print(allPaths)
```

T20】c#

```
// C# program to Print all possible paths from 
// top left to bottom right of a mXn matrix
using System;
using System.Collections.Generic;
class GFG
{

    static List<List<int>> allPaths = new List<List<int>>();

    static void findPathsUtil(List<List<int>> maze,
                              int m, int n, int i,
                              int j, List<int> path,
                              int index)
    {

        // If we reach the bottom of maze,
        // we can only move right
        if (i == m - 1)
        {
            for(int k = j; k < n; k++)
            {

                // path.append(maze[i][k])
                path[index + k - j] = maze[i][k];
            }

            // If we hit this block, it means one
            // path is completed. Add it to paths
            // list and print
            Console.Write( "[" + path[0] + ", ");
            for(int z = 1; z < path.Count - 1; z++)
            {
                Console.Write(path[z] + ", ");
            }
            Console.WriteLine(path[path.Count - 1] + "]");
            allPaths.Add(path);
            return;
        }

        // If we reach to the right most
        // corner, we can only move down
        if (j == n - 1)
        {
            for(int k = i; k < m; k++)
            {
                path[index + k - i] = maze[k][j];
            }

            // path.append(maze[j][k])
            // If we hit this block, it means one
            // path is completed. Add it to paths
            // list and print
            Console.Write( "[" + path[0] + ", ");
            for(int z = 1; z < path.Count - 1; z++)
            {
                Console.Write(path[z] + ", ");
            }
            Console.WriteLine(path[path.Count - 1] + "]");
            allPaths.Add(path); 
            return;
        }

        // Add current element to the path list
        //path.append(maze[i][j])
        path[index] = maze[i][j];

        // Move down in y direction and call
        // findPathsUtil recursively
        findPathsUtil(maze, m, n, i + 1,
                      j, path, index + 1);

        // Move down in y direction and
        // call findPathsUtil recursively
        findPathsUtil(maze, m, n, i, j + 1,
                            path, index + 1);
    }

    static void findPaths(List<List<int>> maze, int m, int n)
    {
        List<int> path = new List<int>();
        for(int i = 0; i < m + n - 1; i++)
        {
            path.Add(0);
        }
        findPathsUtil(maze, m, n, 0, 0, path, 0);
    }

  // Driver code
  static void Main()
  {
    List<List<int>> maze = new List<List<int>>();
    maze.Add(new List<int> { 1, 2, 3 });
    maze.Add(new List<int> { 4, 5, 6 });
    maze.Add(new List<int> { 7, 8, 9 });

    findPaths(maze, 3, 3);
  }
}

// This code is contributed by divyesh072019
```

输出

```
[1, 4, 7, 8, 9]
[1, 4, 5, 8, 9]
[1, 4, 5, 6, 9]
[1, 2, 5, 8, 9]
[1, 2, 5, 6, 9]
[1, 2, 3, 6, 9]
```

注意以上所有的方法都需要一些额外的时间和空间来解决问题，我们可以简单地使用回溯算法以优化的方式解决问题

## c++

```
#include<bits/stdc++.h>
using namespace std;

// function to display the path
void display(vector<int> &ans) {
  for(auto i :ans ) {
    cout<<i <<" ";
  }
  cout<<endl;
}

// a function which check whether our step is safe or not
bool issafe(int r,int c,vector<vector<int>>& visited,int n,int m) {
  return (r < n and c <m and visited[r] !=-1 );  // return true if all values satisfied else false
}

void FindPaths(vector<vector<int>> &grid,int r,int c, int n,int m,vector<int> &ans) {
  // when we hit the last cell we reach to destination then directly push the path
  if(r == n-1 and c == m-1) {
    ans.push_back(grid[r]);
    display(ans);  // function to display the path stored in ans vector
    ans.pop_back(); // pop back because we need to backtrack to explore more path
    return ;
  } 

  // we will store the current value in ch and mark the visited place as -1
  int ch = grid[r];

  ans.push_back(ch); // push the path in ans array
  grid[r] = -1;  // mark the visited place with -1

  // if is it safe to take next downward step then take it
  if(issafe(r+1,c,grid,n,m)) {
    FindPaths(grid,r+1,c,n,m,ans);
  }

  // if is it safe to take next rightward step then take it
  if(issafe(r,c+1,grid,n,m)) {
    FindPaths(grid,r,c+1,n,m,ans);
  }

  // backtracking step we need to make values original so to we can visit it by some another path
  grid[r] = ch;

  // remove the current path element we explore
  ans.pop_back();
  return ;
}

int main() {
      int n = 3 ,m =3;
      vector<vector<int> >grid{ {1,2,3},{4,5,6},{7,8,9}};
      vector<int>ans ; // it will store the path which we have covered

      FindPaths(grid,0,0,n,m,ans); // here 0,0 are initial position to start with
    return 0;
}
```

**输出**

```
1 4 7 8 9 
1 4 5 8 9 
1 4 5 6 9 
1 2 5 8 9 
1 2 5 6 9 
1 2 3 6 9 
```

所以通过这些方法你可以优化你的代码。

**TC-**o(2 ^ n * m)**sc-**o(n)

**另一种方法(迭代):**

1.在这种方法中，我们将使用 **BFS(广度优先搜索)**来寻找所有可能的路径。

2.我们将创建一个包含以下信息的队列:

a)存储到某个单元的路径的向量。

b)单元的坐标。

3.我们将从左上角的单元格开始，在队列中推送单元格值和坐标。

4.我们将继续探索右下单元(如果可能的话)，直到队列不是空的

并通过更新当前单元向量将它们推入队列。

5.如果我们到达最后一个单元格，那么我们有一个答案，我们将打印答案向量。

## c++

```
// c++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// this structure stores information
// about a particular cell i.e
// path upto that cell and cell's
// coordinates
struct info {
    vector<int> path;
    int i;
    int j;
};

void printAllPaths(vector<vector<int> >& maze)
{
    int n = maze.size();
    int m = maze[0].size();

    queue<info> q;
    // pushing top-left cell into the queue
    q.push({ { maze[0][0] }, 0, 0 });

    while (!q.empty()) {
        info p = q.front();
        q.pop();

        // if we reached the bottom-right cell
        // i.e the destination then print the path
        if (p.i == n - 1 && p.j == m - 1) {
            for (auto x : p.path)
                cout << x << " ";

            cout << "\n";
        }

        // if we are in the last row
        // then only right movement is possible
        else if (p.i == n - 1) {
            vector<int> temp = p.path;
            // updating the current path
            temp.push_back(maze[p.i][p.j + 1]);

            q.push({ temp, p.i, p.j + 1 });
        }

        // if we are in the last column
        // then only down movement is possible
        else if (p.j == m - 1) {
            vector<int> temp = p.path;
            // updating the current path
            temp.push_back(maze[p.i + 1][p.j]);

            q.push({ temp, p.i + 1, p.j });
        }

        // else both right and down movement
        // are possible
        else { // right movement
            vector<int> temp = p.path;
            // updating the current path
            temp.push_back(maze[p.i][p.j + 1]);

            q.push({ temp, p.i, p.j + 1 });

            // down movement
            temp.pop_back();
            // updating the current path
            temp.push_back(maze[p.i + 1][p.j]);

            q.push({ temp, p.i + 1, p.j });
        }
    }
}

// Driver Code
int main()
{
    vector<vector<int> > maze{ { 1, 2, 3 },
                               { 4, 5, 6 },
                               { 7, 8, 9 } };

    printAllPaths(maze);

    return 0;
}
```

**输出**

```
1 2 3 6 9 
1 2 5 6 9 
1 2 5 8 9 
1 4 5 6 9 
1 4 5 8 9 
1 4 7 8 9 
```