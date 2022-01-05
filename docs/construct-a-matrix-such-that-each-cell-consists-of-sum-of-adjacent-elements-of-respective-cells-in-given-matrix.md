# 构建一个矩阵，使得每个单元由给定矩阵中各个单元的相邻元素之和组成

> 原文:[https://www . geeksforgeeks . org/construct-a-matrix-so-每个单元由给定矩阵中相应单元的相邻元素之和组成/](https://www.geeksforgeeks.org/construct-a-matrix-such-that-each-cell-consists-of-sum-of-adjacent-elements-of-respective-cells-in-given-matrix/)

给定维度为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是生成一个矩阵，使得任何单元格 **(r，c)** 存储给定矩阵中水平、垂直和对角存在的相邻元素的总和。

**示例:**

> **输入:** arr[][] = {{1，3}，{2，4}}
> **输出:** {{9，7}，{8，6}}
> **解释:**矩阵由以下运算构成:
> 对于单元格(0，0)，arr[1][0]+arr[0][1]+arr[1][1]= 2+3+4 = 9。
> 对于单元格(0，1)，arr[1][0]+arr[0][0]+arr[1][1]= 2+1+4 = 7。
> 对于单元格(1，0)，arr[0][0]+arr[0][1]+arr[1][1]= 1+3+4 = 8。
> 对于单元格(1，1)，arr[1][0]+arr[0][1]+arr[0][0]= 2+3+1 = 6。
> 
> **输入:** arr[][] = {{1}}
> **输出:** {{0}}

**方法:**思路是遍历给定矩阵的每个像元，对于每个像元 **(r，c)** ，存储相邻像元的和 **{{r-1，c-1}，{r+1，c+1}，{r-1，c+1}，{r+1，c-1}，{r，c-1}，{r，c-1 }，{r-1，c}，{r+1，c}，{r，c+1}}** 如果可能。

1.  初始化维度 **N * M** 的矩阵 **v[][]** ，存储每个单元格的结果。
2.  现在，遍历矩阵的每个单元。对于每个单元格，检查有效的相邻单元格，并不断更新它们的总和。
3.  遍历后，打印矩阵 **v[][]** 每个单元格中存储的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Initialize rows and columns
int r, c;

// Store all 8 directions
vector<vector<int> > dir
    = { { 1, 0 },   { -1, 0 }, { 0, 1 }, { 0, -1 },
        { -1, -1 }, { -1, 1 }, { 1, 1 }, { 1, -1 } };

// Function to check if a cell
// (i, j) is valid or not
bool valid(int i, int j)
{
    if (i >= 0 && j >= 0 && i < r && j < c)
        return 1;

    return 0;
}

// Function to find sum of adjacent cells
// for cell (i, j)
int find(int i, int j, vector<vector<int> >& v)
{
    // Initialize sum
    int s = 0;

    // Visit all 8 directions
    for (auto x : dir) {
        int ni = i + x[0], nj = j + x[1];

        // Check if cell is valid
        if (valid(ni, nj))
            s += v[ni][nj];
    }

    // Return sum
    return s;
}

// Function to print sum of adjacent elements
void findsumofneighbors(vector<vector<int> >& M)
{
    // Stores the resultant matrix
    vector<vector<int> > v(r, vector<int>(c, 0));

    // Iterate each elements of matrix
    for (int i = 0; i < r; i++) {
        for (int j = 0; j < c; j++) {

            // Find adjacent sum
            v[i][j] = find(i, j, M);
            cout << v[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{

    // Given matrix
    vector<vector<int> > M
        = { { 1, 4, 1 }, { 2, 4, 5 }, { 3, 1, 2 } };

    // Size of matrix
    r = M.size(), c = M[0].size();

    // Function call
    findsumofneighbors(M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

public class GFG {

    // Initialize rows and columns
    private static int r, c;

    // Store all 8 directions
    static int[][] dir
        = { { 1, 0 },   { -1, 0 }, { 0, 1 }, { 0, -1 },
            { -1, -1 }, { -1, 1 }, { 1, 1 }, { 1, -1 } };

    // Function to check if a cell
    // (i, j) is valid or not
    public static boolean valid(int i, int j)
    {
        if (i >= 0 && j >= 0 && i < r && j < c)
            return true;

        return false;
    }

    // Function to find sum of adjacent cells
    // for cell (i, j)
    static int find(int i, int j, int[][] v)
    {
        // Initialize sum
        int s = 0;

        // Visit all 8 directions
        for (int k = 0; k < 8; k++) {

            int ni = i + dir[k][0], nj = j + dir[k][1];

            // Check if cell is valid
            if (valid(ni, nj))
                s += v[ni][nj];
        }

        // Return sum
        return s;
    }

    // Function to print sum of adjacent elements
    static void findsumofneighbors(int[][] M)
    {
        // Stores the resultant matrix
        int[][] v = new int[r];

        // Iterate each elements of matrix
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {

                // Find adjacent sum
                v[i][j] = find(i, j, M);
                System.out.print(v[i][j] + " ");
            }
            System.out.println("");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given matrix
        int[][] M
            = { { 1, 4, 1 },
               { 2, 4, 5 },
               { 3, 1, 2 } };

        // Size of matrix
        r = M.length;
        c = M[0].length;

        // Function call
        findsumofneighbors(M);
    }
}

// This code is contributed by ajaykr00kj
```

## 蟒蛇 3

```
# Python program for the above approach

# Initialize rows and columns
r, c = 0, 0;

# Store all 8 directions
dir = [[1, 0], [-1, 0], [0, 1], [0, -1],
       [-1, -1], [-1, 1], [1, 1], [1, -1]];

# Function to check if a cell
# (i, j) is valid or not
def valid(i, j):
    if (i >= 0 and j >= 0 and i < r and j < c):
        return True;

    return False;

# Function to find sum of adjacent cells
# for cell (i, j)
def find(i, j, v):

    # Initialize sum
    s = 0;

    # Visit all 8 directions
    for k in range(8):

        ni = i + dir[k][0];
        nj = j + dir[k][1];

        # Check if cell is valid
        if (valid(ni, nj)):
            s += v[ni][nj];

    # Return sum
    return s;

# Function to print sum of adjacent elements
def findsumofneighbors(M):

    # Stores the resultant matrix
    v = [[0 for i in range(c)] for j in range(r)];

    # Iterate each elements of matrix
    for i in range(r):
        for j in range(c):

            # Find adjacent sum
            v[i][j] = find(i, j, M);
            print(v[i][j], end=" ");

        print("");

# Driver code
if __name__ == '__main__':

    # Given matrix
    M = [[1, 4, 1], [2, 4, 5], [3, 1, 2]];

    # Size of matrix
    r = len(M[0]);
    c = len(M[1]);

    # Function call
    findsumofneighbors(M);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Initialize rows and columns
    private static int r, c;

    // Store all 8 directions
    static int[,] dir
        = { { 1, 0 },   { -1, 0 }, { 0, 1 }, { 0, -1 },
            { -1, -1 }, { -1, 1 }, { 1, 1 }, { 1, -1 } };

    // Function to check if a cell
    // (i, j) is valid or not
    public static bool valid(int i, int j)
    {
        if (i >= 0 && j >= 0 && i < r && j < c)
            return true;

        return false;
    }

    // Function to find sum of adjacent cells
    // for cell (i, j)
    static int find(int i, int j, int[,] v)
    {
        // Initialize sum
        int s = 0;

        // Visit all 8 directions
        for (int k = 0; k < 8; k++) {

            int ni = i + dir[k, 0], nj = j + dir[k, 1];

            // Check if cell is valid
            if (valid(ni, nj))
                s += v[ni, nj];
        }

        // Return sum
        return s;
    }

    // Function to print sum of adjacent elements
    static void findsumofneighbors(int[,] M)
    {
        // Stores the resultant matrix
        int[,] v = new int[r, c];

        // Iterate each elements of matrix
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {

                // Find adjacent sum
                v[i,j] = find(i, j, M);
                Console.Write(v[i, j] + " ");
            }
            Console.WriteLine("");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Given matrix
        int[,] M
            = { { 1, 4, 1 },
               { 2, 4, 5 },
               { 3, 1, 2 } };

        // Size of matrix
        r = M.GetLength(0);
        c = M.GetLength(1);

        // Function call
        findsumofneighbors(M);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Initialize rows and columns
    let r, c;

    // Store all 8 directions
    let dir
        = [[ 1, 0 ],   [ -1, 0 ], [ 0, 1 ], [ 0, -1 ],
            [ -1, -1 ], [ -1, 1 ], [ 1, 1 ], [ 1, -1 ]];

    // Function to check if a cell
    // (i, j) is valid or not
   function valid(i, j)
    {
        if (i >= 0 && j >= 0 && i < r && j < c)
            return true;

        return false;
    }

    // Function to find sum of adjacent cells
    // for cell (i, j)
    function find(i, j, v)
    {
        // Initialize sum
        let s = 0;

        // Visit all 8 directions
        for (let k = 0; k < 8; k++) {

            let ni = i + dir[k][0], nj = j + dir[k][1];

            // Check if cell is valid
            if (valid(ni, nj))
                s += v[ni][nj];
        }

        // Return sum
        return s;
    }

    // Function to print sum of adjacent elements
    function findsumofneighbors(M)
    {
        // Stores the resultant matrix
        let v = new Array(r);

        // Loop to create 2D array using 1D array
    for (var i = 0; i < v.length; i++) {
        v[i] = new Array(2);
    }

        // Iterate each elements of matrix
        for (let i = 0; i < r; i++) {
            for (let j = 0; j < c; j++) {

                // Find adjacent sum
                v[i][j] = find(i, j, M);
                document.write(v[i][j] + " ");
            }
            document.write("<br/>" );
        }
    }

// Driver Code

     // Given matrix
      let M
            = [[ 1, 4, 1 ],
               [ 2, 4, 5 ],
               [ 3, 1, 2 ]];

        // Size of matrix
        r = M.length;
        c = M[0].length;

        // Function call
        findsumofneighbors(M);

</script>
```

**Output**

```
10 13 13 
13 19 12 
7 16 10
```

***时间复杂度:** O(N*M)其中 **N * M** 是矩阵的维度。*
***辅助空间:** O(N*M)*