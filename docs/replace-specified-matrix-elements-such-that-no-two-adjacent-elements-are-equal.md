# 替换指定的矩阵元素，使相邻元素不相等

> 原文:[https://www . geeksforgeeks . org/replace-specified-matrix-elements-so-no-两个相邻元素相等/](https://www.geeksforgeeks.org/replace-specified-matrix-elements-such-that-no-two-adjacent-elements-are-equal/)

给定尺寸为 **N * M** 的 [**矩阵**](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，由**【O】**或**【F】**组成，其中**【O】**表示障碍物，**【F】**表示自由空间，任务是将给定矩阵中的所有**【F】**替换为**【1】**或【2】

**示例:**

> **输入:** N = 4，M = 4，arr[][]= {'F '，' F '，' F '，' F'}，{ ' F '，' O '，' F '，' F '，' O '，' F '，' F '，' F '，' F '，' F '，' F ' } }
> T3】输出:T5】1 2 1 2 1 2
> 2 1
> 1 2 O 2
> 2 1 2 1
> 
> **输入:** N = 1，M = 1，arr[][]= { { ' O ' } }
> T3】输出:

**天真法:**解决问题最简单的方法是使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)，类似于[数独](https://www.geeksforgeeks.org/sudoku-backtracking-7/)问题。但是，不是将 **N** 不同的值放置在给定的位置，而是要求将 **1** 或 **2** 放置在包含**‘F’**的单元上，使得没有两个相邻的元素彼此相等。按照以下步骤解决问题:

*   创建一个函数来检查矩阵中给定的位置是否有效。
*   如果已经到达矩阵的末尾，即 **i = N，j = M** ，则返回**真**。
*   否则，如果当前索引是自由空间，即 **arr[i][j]=='F'** ，则用 **'1'** 或 **'2'** 填充索引。如果发现某个单元格无效，即相邻单元格的值相同，则打印**“否”**。
*   完成矩阵遍历后，如果所有的“F”被替换，使得没有相邻的矩阵元素相同，则打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if current
// position is safe or not
bool issafe(vector<vector<char> >& v, int i,
            int j, int n, int m, char ch)
{
    // Directions for adjacent cells
    int rowN[] = { 1, -1, 0, 0 };
    int colN[] = { 0, 0, 1, -1 };

    for (int k = 0; k < 4; k++) {

        // Check if any adjacent cell is same
        if (i + rowN[k] >= 0 && i + rowN[k] < n
            && j + colN[k] >= 0 && j + colN[k] < m
            && v[i + rowN[k]][j + colN[k]] == ch) {
            return false;
        }
    }

    // Current index is valid
    return true;
}

// Recursive function for backtracking
bool place(vector<vector<char> >& v,
           int n, int m)
{
    int i, j;
    for (i = 0; i < n; i++) {
        for (j = 0; j < m; j++) {

            // Free cell
            if (v[i][j] == 'F') {
                break;
            }
        }
        if (j != m) {
            break;
        }
    }

    // All positions covered
    if (i == n && j == m) {
        return true;
    }

    // If position is valid for 1
    if (issafe(v, i, j, n, m, '1')) {
        v[i][j] = '1';
        if (place(v, n, m)) {
            return true;
        }
        v[i][j] = 'F';
    }

    // If position is valid for 2
    if (issafe(v, i, j, n, m, '2')) {
        v[i][j] = '2';

        // Recursive call for next
        // unoccupied position
        if (place(v, n, m)) {
            return true;
        }

        // If above conditions fails
        v[i][j] = 'F';
    }
    return false;
}

// Function to print valid matrix
void printMatrix(vector<vector<char> > arr,
                 int n, int m)
{

    place(arr, n, m);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cout << arr[i][j];
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Given matrix
    vector<vector<char> > arr = {
        { 'F', 'F', 'F', 'F' },
        { 'F', 'O', 'F', 'F' },
        { 'F', 'F', 'O', 'F' },
        { 'F', 'F', 'F', 'F' },
    };

    // Give dimensions
    int n = 4, m = 4;

    // Function call
    printMatrix(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    public static boolean issafe(char v[][], int i,
            int j, int n, int m, char ch)
    {
        // Directions for adjacent cells
        int rowN[] = { 1, -1, 0, 0 };
        int colN[] = { 0, 0, 1, -1 };

        for (int k = 0; k < 4; k++) {

            // Check if any adjacent cell is same
            if (i + rowN[k] >= 0 && i + rowN[k] < n
                && j + colN[k] >= 0 && j + colN[k] < m
                && v[i + rowN[k]][j + colN[k]] == ch) {
                return false;
            }
        }

        // Current index is valid
        return true;
    }

    // Recursive function for backtracking
    public static boolean place(char v[][],
           int n, int m)
    {
        int i=0, j=0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < m; j++) {

                // Free cell
                if (v[i][j] == 'F') {
                    break;
                }
            }
            if (j != m) {
                break;
            }
        }

        // All positions covered
        if (i == n && j == m) {
            return true;
        }

        // If position is valid for 1
        if (issafe(v, i, j, n, m, '1')) {
            v[i][j] = '1';
            if (place(v, n, m)) {
                return true;
            }
            v[i][j] = 'F';
        }

        // If position is valid for 2
        if (issafe(v, i, j, n, m, '2')) {
            v[i][j] = '2';

            // Recursive call for next
            // unoccupied position
            if (place(v, n, m)) {
                return true;
            }

            // If above conditions fails
            v[i][j] = 'F';
        }
        return false;
    }
    // Function to print valid matrix
    public static void printMatrix(char arr[][],
                 int n, int m)
    {
        place(arr, n, m);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                System.out.print(arr[i][j]);
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main (String[] args) {
        char arr[][] = {
        { 'F', 'F', 'F', 'F' },
        { 'F', 'O', 'F', 'F' },
        { 'F', 'F', 'O', 'F' },
        { 'F', 'F', 'F', 'F' },
                            };

        // Give dimensions
        int n = 4, m = 4;

        // Function call
        printMatrix(arr, n, m);
    }
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if current
// position is safe or not   
public static bool issafe(char[,] v, int i,
                              int j, int n,
                              int m, char ch)
{

    // Directions for adjacent cells
    int[] rowN = { 1, -1, 0, 0 };
    int[] colN = { 0, 0, 1, -1 };

    for(int k = 0; k < 4; k++)
    {

        // Check if any adjacent cell is same
        if (i + rowN[k] >= 0 && i + rowN[k] < n &&
            j + colN[k] >= 0 && j + colN[k] < m &&
            v[(i + rowN[k]), (j + colN[k])] == ch)
        {
            return false;
        }
    }

    // Current index is valid
    return true;
}

// Recursive function for backtracking
public static bool place(char[,] v,
                         int n, int m)
{
    int i = 0, j = 0;

    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Free cell
            if (v[i, j] == 'F')
            {
                break;
            }
        }
        if (j != m)
        {
            break;
        }
    }

    // All positions covered
    if (i == n && j == m)
    {
        return true;
    }

    // If position is valid for 1
    if (issafe(v, i, j, n, m, '1'))
    {
        v[i, j] = '1';

        if (place(v, n, m))
        {
            return true;
        }
        v[i, j] = 'F';
    }

    // If position is valid for 2
    if (issafe(v, i, j, n, m, '2'))
    {
        v[i, j] = '2';

        // Recursive call for next
        // unoccupied position
        if (place(v, n, m))
        {
            return true;
        }

        // If above conditions fails
        v[i, j] = 'F';
    }
    return false;
}

// Function to print valid matrix
public static void printMatrix(char[,] arr,
                               int n, int m)
{
    place(arr, n, m);

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            Console.Write(arr[i, j]);
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main()
{
    char[,] arr = { { 'F', 'F', 'F', 'F' },
                    { 'F', 'O', 'F', 'F' },
                    { 'F', 'F', 'O', 'F' },
                    { 'F', 'F', 'F', 'F' },};

    // Give dimensions
    int n = 4, m = 4;

    // Function call
    printMatrix(arr, n, m);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

function issafe(v, i,
            j, n, m, ch)
    {
        // Directions for adjacent cells
        let rowN = [ 1, -1, 0, 0 ];
        let colN = [ 0, 0, 1, -1 ];

        for (let k = 0; k < 4; k++) {

            // Check if any adjacent cell is same
            if (i + rowN[k] >= 0 && i + rowN[k] < n
                && j + colN[k] >= 0 && j + colN[k] < m
                && v[i + rowN[k]][j + colN[k]] == ch) {
                return false;
            }
        }

        // Current index is valid
        return true;
    }

    // Recursive function for backtracking
    function place(v, n, m)
    {
        let i=0, j=0;
        for (i = 0; i < n; i++) {
            for (j = 0; j < m; j++) {

                // Free cell
                if (v[i][j] == 'F') {
                    break;
                }
            }
            if (j != m) {
                break;
            }
        }

        // All positions covered
        if (i == n && j == m) {
            return true;
        }

        // If position is valid for 1
        if (issafe(v, i, j, n, m, '1')) {
            v[i][j] = '1';
            if (place(v, n, m)) {
                return true;
            }
            v[i][j] = 'F';
        }

        // If position is valid for 2
        if (issafe(v, i, j, n, m, '2')) {
            v[i][j] = '2';

            // Recursive call for next
            // unoccupied position
            if (place(v, n, m)) {
                return true;
            }

            // If above conditions fails
            v[i][j] = 'F';
        }
        return false;
    }
    // Function to print valid matrix
    function printMatrix(arr,
                 n, m)
    {
        place(arr, n, m);
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
               document.write(arr[i][j]);
            }
            document.write("<br/>");
        }
    }

// Driver code

    let arr = [
        [ 'F', 'F', 'F', 'F' ],
        [ 'F', 'O', 'F', 'F' ],
        [ 'F', 'F', 'O', 'F' ],
        [ 'F', 'F', 'F', 'F' ],
                            ];

        // Give dimensions
        let n = 4, m = 4;

        // Function call
        printMatrix(arr, n, m);

</script>
```

**Output**

```
1212
2O21
12O2
2121
```

***时间复杂度:**O(2<sup>N * M</sup>)*
***辅助空间:** O(N*M)*

**高效方法:**想法是如果单元 **(i，j)** 的奇偶性为 **1** ，即 **(i + j) % 2** 为 **1** ，则简单地用 **1** 替换任何**【F】**。否则，用 **2** 代替**【F】**。按照以下步骤解决问题:

*   [遍历给定矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)。
*   对于遍历的每个单元格 **(i，j)** ，如果单元格 **arr[i][j]** 等于**【F】****(I+j)% 2**等于 **1** ，则分配 **arr[i][j] = 1** 。否则，分配 **arr[i][j] = 2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to display the valid matrix
void print(vector<vector<char> > arr, int n, int m)
{

    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            char a = arr[i][j];

            // If the current cell is a free
            // space and is even-indexed
            if ((i + j) % 2 == 0 && a == 'F') {
                arr[i][j] = '1';
            }
            // If the current cell is a free
            // space and is odd-indexed
            else if (a == 'F') {
                arr[i][j] = '2';
            }
        }
    }

    // Print the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cout << arr[i][j];
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    // Given N and M
    int n = 4, m = 4;

    // Given matrix
    vector<vector<char> > arr = {
        { 'F', 'F', 'F', 'F' },
        { 'F', 'O', 'F', 'F' },
        { 'F', 'F', 'O', 'F' },
        { 'F', 'F', 'F', 'F' },
    };

    // Function call
    print(arr, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{
    // Function to display the valid matrix
    public static void print(char arr[][], int n, int m)
    {
        // Traverse the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                char a = arr[i][j];

                // If the current cell is a free
                // space and is even-indexed
                if ((i + j) % 2 == 0 && a == 'F') {
                    arr[i][j] = '1';
                }
                // If the current cell is a free
                // space and is odd-indexed
                else if (a == 'F') {
                    arr[i][j] = '2';
                }
            }
        }

        // Print the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                System.out.print(arr[i][j]);
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main (String[] args) {
        // Given N and M
        int n = 4, m = 4;

        // Given matrix
        char arr[][] = {
                        { 'F', 'F', 'F', 'F' },
                        { 'F', 'O', 'F', 'F' },
                        { 'F', 'F', 'O', 'F' },
                        { 'F', 'F', 'F', 'F' }};

        // Function call
        print(arr, n, m);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to display the valid matrix
def Print(arr, n, m):

    # Traverse the matrix
    for i in range(n):
        for j in range(m):
            a = arr[i][j]

            # If the current cell is a free
            # space and is even-indexed
            if ((i + j) % 2 == 0 and a == 'F') :
                arr[i][j] = '1'

            # If the current cell is a free
            # space and is odd-indexed
            elif (a == 'F') :
                arr[i][j] = '2'

    # Print the matrix
    for i in range(n) :
        for j in range(m) :
            print(arr[i][j], end = "")

        print()

# Given N and M
n, m = 4, 4

# Given matrix
arr = [
    [ 'F', 'F', 'F', 'F' ],
    [ 'F', 'O', 'F', 'F' ],
    [ 'F', 'F', 'O', 'F' ],
    [ 'F', 'F', 'F', 'F' ]]

# Function call
Print(arr, n, m)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to display the valid matrix
public static void print(char[,] arr, int n,
                                      int m)
{

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            char a = arr[i, j];

            // If the current cell is a free
            // space and is even-indexed
            if ((i + j) % 2 == 0 && a == 'F')
            {
                arr[i, j] = '1';
            }

            // If the current cell is a free
            // space and is odd-indexed
            else if (a == 'F')
            {
                arr[i, j] = '2';
            }
        }
    }

    // Print the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {
            Console.Write(arr[i, j]);
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main()
{

    // Given N and M
    int n = 4, m = 4;

    // Given matrix
    char[,] arr = { { 'F', 'F', 'F', 'F' },
                    { 'F', 'O', 'F', 'F' },
                    { 'F', 'F', 'O', 'F' },
                    { 'F', 'F', 'F', 'F' }};

    // Function call
    print(arr, n, m);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// Java Script program for the above approach

    // Function to display the valid matrix
    function print(arr,n,m)
    {

        // Traverse the matrix
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                let a = arr[i][j];

                // If the current cell is a free
                // space and is even-indexed
                if ((i + j) % 2 == 0 && a == 'F') {
                    arr[i][j] = '1';
                }
                // If the current cell is a free
                // space and is odd-indexed
                else if (a == 'F') {
                    arr[i][j] = '2';
                }
            }
        }

        // Print the matrix
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                document.write(arr[i][j]);
            }
            document.write("<br>");
        }
    }

    // Driver Code

        // Given N and M
        let n = 4, m = 4;

        // Given matrix
        let arr = [
                        ['F', 'F', 'F', 'F' ],
                        [ 'F', 'O', 'F', 'F' ],
                        [ 'F', 'F', 'O', 'F' ],
                        [ 'F', 'F', 'F', 'F' ]];

        // Function call
        print(arr, n, m);

// This code is contributed by sravan.
</script>
```

**Output**

```
1212
2O21
12O2
2121
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*