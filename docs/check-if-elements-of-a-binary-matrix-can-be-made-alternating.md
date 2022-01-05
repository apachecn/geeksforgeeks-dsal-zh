# 检查二元矩阵的元素是否可以交替出现

> 原文:[https://www . geeksforgeeks . org/check-if-elements-of-a-binary-matrix-can-make-alternative/](https://www.geeksforgeeks.org/check-if-elements-of-a-binary-matrix-can-be-made-alternating/)

给定一个大小为 **N * M** 的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **网格[][]** ，由字符**“1”【0】**和**“***组成，其中**“***表示一个空格，可以用**“1”**或**“0”**替换。任务是填充网格，使得**“0”**和**“1”**交替出现，并且没有两个连续的字符同时出现，即(101010)有效，而(101101)无效，因为两个**“1”**同时出现。如果可以，打印**是**和可能的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)。否则，打印**否**。

**示例:**

> **输入:** N = 4，M = 4 格[][] = { {**10}，{****}，{****}，{**01}}
> **输出:**是
> 1010
> 0101
> 1010
> 0101
> **解释:**创建一个“1”和“0”字符交替出现的格，这样答案是肯定的，后面是填充字符。
> 
> **输入:** N = 4，M = 4，网格[][] = {{*1*0}，{ * * * }，{**10}，{ * * * * * } }
> **输出:**否
> **说明:**第一行 1 和 0 有一个单元格空白，既不能填 1 也不能填 0。

**方法:**一个可能的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)只有两种可能，一种是从 **1** 开始，一种是从 **0 开始。**生成两者，并检查其中任何一个是否与给定的[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **网格[][]匹配。**按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **创建网格(char grid[][1001]，bool is1，int N，int M)** 并执行以下任务:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
            *   如果**为 1** 为**真，**则将**网格【I】【j】**设置为**‘0’**，将**为 1** 设置为**假。**
            *   否则，将**网格【I】【j】**设置为**【1】**，将 **is1** 设置为**真。**
        *   如果 **M%2** 等于 **0，**则将**的值设为 1** 而不是**的值设为 1。**
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **测试网格(char testGrid[][1001]，char Grid[][1001]，int N，int M)** 并执行以下任务:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
            *   如果**网格[i][j]** 不等于**' ***和**测试网格[i][j]** 不等于**网格[i][j]，**则返回 **false。**
    *   执行上述步骤后，返回**真值**作为答案。
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **打印网格(char grid[][1001]，int N，int M)** ，并执行以下任务:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
            *   打印**网格[i][j]的值。**
*   初始化两个[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **网格 1[N][1001]** 和**网格 2[N][1001]** 来存储可能的交替网格。
*   调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **创建网格(gridTest1，true，N，M)** 和**创建网格(gridTest2，false，N，M)** 形成可能的交替网格。
*   如果[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **测试网格(gridTest1，网格，N，M)** 返回**真，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **打印网格(gridTest1，N，M)** 打印网格作为答案。
*   否则如果[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **测试网格(gridTest2，网格，N，M)** 返回**真，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **打印网格(gridTest2，N，M)** 打印网格作为答案。
*   否则，打印**否**作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to create the possible grids
void createGrid(char grid[][1001], bool is1,
                int N, int M)
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            if (is1) {
                grid[i][j] = '0';
                is1 = false;
            }
            else {
                grid[i][j] = '1';
                is1 = true;
            }
        }
        if (M % 2 == 0)
            is1 = !is1;
    }
}

// Function to test if any one of them
// matches with the given 2-D array
bool testGrid(char testGrid[][1001],
              char Grid[][1001],
              int N, int M)
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            if (Grid[i][j] != '*') {

                if (Grid[i][j] != testGrid[i][j]) {
                    return false;
                }
            }
        }
    }
    return true;
}

// Function to print the grid, if possible
void printGrid(char grid[][1001], int N, int M)
{
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            cout << grid[i][j] << " ";
        }
        cout << endl;
    }
}

// Function to check if the grid
// can be made alternating or not
void findPossibleGrid(int N, int M,
                      char grid[][1001])
{
    // Grids to store the possible grids
    char gridTest1[N][1001], gridTest2[N][1001];

    createGrid(gridTest1, true, N, M);

    createGrid(gridTest2, false, N, M);

    if (testGrid(gridTest1, grid, N, M)) {

        cout << "Yes\n";
        printGrid(gridTest1, N, M);
    }
    else if (testGrid(gridTest2, grid, N, M)) {

        cout << "Yes\n";
        printGrid(gridTest2, N, M);
    }
    else {
        cout << "No\n";
    }
}

// Driver Code
int main()
{
    int N = 4, M = 4;
    char grid[][1001] = { { '*', '*', '1', '0' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '0', '1' } };

    findPossibleGrid(N, M, grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to create the possible grids
public static void createGrid(char[][] grid,
                              boolean is1,
                              int N, int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (is1)
            {
                grid[i][j] = '0';
                is1 = false;
            }
            else
            {
                grid[i][j] = '1';
                is1 = true;
            }
        }
        if (M % 2 == 0)
            is1 = !is1;
    }
}

// Function to test if any one of them
// matches with the given 2-D array
public static boolean testGrid(char[][] testGrid,
                               char[][] Grid, int N,
                               int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (Grid[i][j] != '*')
            {
                if (Grid[i][j] != testGrid[i][j])
                {
                    return false;
                }
            }
        }
    }
    return true;
}

// Function to print the grid, if possible
public static void printGrid(char[][] grid, int N,
                             int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            System.out.print(grid[i][j] + " ");
        }
        System.out.println();
    }
}

// Function to check if the grid
// can be made alternating or not
public static void findPossibleGrid(int N, int M,
                                    char[][] grid)
{

    // Grids to store the possible grids
    char[][] gridTest1 = new char[N][1001];
    char[][] gridTest2 = new char[N][1001];

    createGrid(gridTest1, true, N, M);
    createGrid(gridTest2, false, N, M);

    if (testGrid(gridTest1, grid, N, M))
    {
        System.out.println("Yes");
        printGrid(gridTest1, N, M);
    }
    else if (testGrid(gridTest2, grid, N, M))
    {
        System.out.println("Yes");
        printGrid(gridTest2, N, M);
    }
    else
    {
        System.out.println("No");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 4, M = 4;
    char[][] grid = { { '*', '*', '1', '0' },
                      { '*', '*', '*', '*' },
                      { '*', '*', '*', '*' },
                      { '*', '*', '0', '1' } };

    findPossibleGrid(N, M, grid);
}
}

// This code is contributed by maddler
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to create the possible grids
def createGrid(grid, is1, N, M):
    for i in range(N):
        for j in range(M):
            if (is1):
                grid[i][j] = '0'
                is1 = False

            else:
                grid[i][j] = '1'
                is1 = True

        if (M % 2 == 0):
            is1 = True if is1 == False else False

# Function to test if any one of them
# matches with the given 2-D array
def testGrid(testGrid, Grid, N, M):
    for i in range(N):
        for j in range(M):
            if (Grid[i][j] != '*'):
                if (Grid[i][j] != testGrid[i][j]):
                    return False

    return True

# Function to print the grid, if possible
def printGrid(grid, N, M):
    for i in range(N):
        for j in range(M):
            print(grid[i][j],end = " ")
        print("\n",end = "")

# Function to check if the grid
# can be made alternating or not
def findPossibleGrid(N, M, grid):
    # Grids to store the possible grids
    gridTest1 = [['' for i in range(1001)] for j in range(N)]
    gridTest2 = [['' for i in range(1001)] for j in range(N)]

    createGrid(gridTest1, True, N, M)

    createGrid(gridTest2, False, N, M)

    if(testGrid(gridTest1, grid, N, M)):
        print("Yes")
        printGrid(gridTest1, N, M)

    elif(testGrid(gridTest2, grid, N, M)):
        print("Yes")
        printGrid(gridTest2, N, M)
    else:
        print("No")

# Driver Code
if __name__ == '__main__':
    N = 4
    M = 4
    grid  = [['*', '*', '1', '0'],
             ['*', '*', '*', '*'],
             ['*', '*', '*', '*'],
             ['*', '*', '0', '1']]

    findPossibleGrid(N, M, grid)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to create the possible grids
public static void createGrid(char[,] grid,
                              bool is1,
                              int N, int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (is1)
            {
                grid[i, j] = '0';
                is1 = false;
            }
            else
            {
                grid[i, j] = '1';
                is1 = true;
            }
        }
        if (M % 2 == 0)
            is1 = !is1;
    }
}

// Function to test if any one of them
// matches with the given 2-D array
public static bool testGrid(char[,] testGrid,
                            char[,] Grid, int N,
                            int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            if (Grid[i, j] != '*')
            {
                if (Grid[i, j] != testGrid[i, j])
                {
                    return false;
                }
            }
        }
    }
    return true;
}

// Function to print the grid, if possible
public static void printGrid(char[,] grid, int N,
                             int M)
{
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            Console.Write(grid[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Function to check if the grid
// can be made alternating or not
public static void findPossibleGrid(int N, int M,
                                    char[,] grid)
{

    // Grids to store the possible grids
    char[,] gridTest1 = new char[N, 1001];
    char[,] gridTest2 = new char[N, 1001];

    createGrid(gridTest1, true, N, M);
    createGrid(gridTest2, false, N, M);

    if (testGrid(gridTest1, grid, N, M))
    {
        Console.WriteLine("Yes");
        printGrid(gridTest1, N, M);
    }
    else if (testGrid(gridTest2, grid, N, M))
    {
        Console.WriteLine("Yes");
        printGrid(gridTest2, N, M);
    }
    else
    {
        Console.WriteLine("No");
    }
}

// Driver code
public static void Main()
{
    int N = 4, M = 4;
    char[,] grid = { { '*', '*', '1', '0' },
                     { '*', '*', '*', '*' },
                     { '*', '*', '*', '*' },
                     { '*', '*', '0', '1' } };

    findPossibleGrid(N, M, grid);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to create the possible grids
function createGrid(grid, is1, N, M) {
  for (let i = 0; i < N; i++) {
    for (let j = 0; j < M; j++) {
      if (is1) {
        grid[i][j] = "0";
        is1 = false;
      } else {
        grid[i][j] = "1";
        is1 = true;
      }
    }
    if (M % 2 == 0) is1 = !is1;
  }
}

// Function to test if any one of them
// matches with the given 2-D array
function testGrid(testGrid, Grid, N, M) {
  for (let i = 0; i < N; i++) {
    for (let j = 0; j < M; j++) {
      if (Grid[i][j] != "*") {
        if (Grid[i][j] != testGrid[i][j]) {
          return false;
        }
      }
    }
  }
  return true;
}

// Function to print the grid, if possible
function printGrid(grid, N, M) {
  for (let i = 0; i < N; i++) {
    for (let j = 0; j < M; j++) {
      document.write(grid[i][j] + " ");
    }
    document.write("<br>");
  }
}

// Function to check if the grid
// can be made alternating or not
function findPossibleGrid(N, M, grid) {
  // Grids to store the possible grids
  let gridTest1 = new Array(N).fill(0).map(() => new Array(1001));
  let gridTest2 = new Array(N).fill(0).map(() => new Array(1001));

  createGrid(gridTest1, true, N, M);

  createGrid(gridTest2, false, N, M);

  if (testGrid(gridTest1, grid, N, M)) {
    document.write("Yes<br>");
    printGrid(gridTest1, N, M);
  } else if (testGrid(gridTest2, grid, N, M)) {
    document.write("Yes<br>");
    printGrid(gridTest2, N, M);
  } else {
    document.write("No<br>");
  }
}

// Driver Code

let N = 4,
  M = 4;
let grid = [
  ["*", "*", "1", "0"],
  ["*", "*", "*", "*"],
  ["*", "*", "*", "*"],
  ["*", "*", "0", "1"],
];

findPossibleGrid(N, M, grid);

</script>
```

**Output**

```
Yes
1 0 1 0 
0 1 0 1 
1 0 1 0 
0 1 0 1 
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*

**有效方法:**想法是使用两个变量，而不是创建[二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)来保持可能的交替数组。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.)**posCheck(char grid[][1001]，int N，int M，char check)** 并执行以下任务:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
            *   如果**网格【I】【j】**等于 **'*，**则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
            *   否则，如果 **(i+j)%2** 等于**1****格【I】【j】**不等于**则勾选**，则返回 **false。**
            *   否则，如果 **(i+j)%2** 等于 **0** ，**网格【I】【j】**等于**勾选**，则返回 **false。**
    *   执行上述步骤后，返回**真值**作为答案。
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.)**posCheck(char grid[][1001]，int N，int M，char 奇数，char 偶数)**并执行以下任务:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
        *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
            *   如果 **(i+j)%2** 等于 **1，**则将**网格【I】【j】**的值设置为**奇数**否则**偶数。**
*   将布尔变量**标志**初始化为**真。**
*   将变量 **k** 和 **o** 初始化为 **-1** ，存储第一个没有字符 **'* '的单元格的值。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
        *   如果**网格【I】【j】**不等于 **'*，**则将 **k** 的值设置为 **i** ，o**为 **j** ，[断开](https://www.geeksforgeeks.org/break-statement-cc/) **。****
    *   如果 **k** 不等于 **-1，**则[破](https://www.geeksforgeeks.org/break-statement-cc/)。
*   如果 **k** 不等于 **-1，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **PosCheck(grid，n，m，' 1')** 并将[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.)返回的值存储在变量**标志**中，如果**标志**为 **true，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **填充(grid，n，m，' 1 '，' 0 ')**
*   如果**标志**为**假，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **PosCheck(grid，n，m，' 0')** 并将[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.)返回的值存储在变量**标志**中，如果**标志**为**真，**则调用[函数](https://www.geeksforgeeks.org/functions-in-c/#:~:text=C%20also%20allows%20to%20declare, Below%20is%20an%20example%20declaration.&text=The%20parameters%20passed%20to%20function%20are%20called%20actual%20parameters.) **填充(grid，n，m，' 0 '，' 1')** 进行填充
*   如果 **k** 等于 **-1，**则初始化 char 变量 **h** 为**‘0’**。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
    *   将**网格【0】【I】**的值设置为 **h** ，如果 **h** 为“ **0** ，则设置为“ **1** ，否则**为“0”。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下任务:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M】**，并执行以下任务:
        *   如果 **i-1** 小于 **0，**则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
        *   如果**网格【I-1】【j】**为**【1】，**则设置为**【0】，**否则**【1】。**
*   将**标志**的值设置为**真**，因为网格是交替的**。**
*   如果**标志**为**假，**则打印**“否”**。
*   否则，打印**“是”**并打印**网格的元素[][]。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check for the grid in
// one of the alternating ways
bool PosCheck(char a[][1001], int n,
              int m, char check)
{

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Iterate over the range
        for (int j = 0; j < m; j++) {

            if (a[i][j] == '*') {
                continue;
            }
            else {

                // (i+j)%2==1 cells should be with
                // the character check and the rest
                // should be with the other character
                if (((i + j) & 1) && a[i][j] != check) {
                    return false;
                }
                if (!((i + j) & 1) && a[i][j] == check) {
                    return false;
                }
            }
        }
    }
    return true;
}

// Function to fill the grid in a possible way
void fill(char a[][1001], int n, int m,
          char odd, char even)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if ((i + j) & 1) {
                a[i][j] = odd;
            }
            else {
                a[i][j] = even;
            }
        }
    }
}

// Function to find if the grid can be made alternating
void findPossibleGrid(int n, int m, char a[][1001])
{
    bool flag = true;
    int k = -1, o = -1;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            if (a[i][j] != '*') {

                // If grid contains atleast
                // one 1 or 0
                k = i;
                o = j;
                break;
            }
        }
        if (k != -1) {
            break;
        }
    }
    if (k != -1) {
        flag = PosCheck(a, n, m, '1');
        if (flag) {
            fill(a, n, m, '1', '0');
        }
        else {
            flag = PosCheck(a, n, m, '0');
            if (flag) {
                fill(a, n, m, '0', '1');
            }
        }
    }
    else {
        // Fill the grid in any possible way
        char h = '1';
        for (int i = 0; i < m; i++) {
            a[0][i] = h;
            if (h == '1') {
                h = '0';
            }
            else {
                h = '1';
            }
        }
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (i - 1 < 0) {
                    continue;
                }
                if (a[i - 1][j] == '1') {
                    a[i][j] = '0';
                }
                else {
                    a[i][j] = '1';
                }
            }
        }
        flag = true;
    }

    if (!flag) {
        cout << "NO\n";
    }
    else {
        cout << "YES\n";
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                cout << a[i][j];
            }
            cout << endl;
        }
    }
}

// Driver Code
int main()
{
    int n = 4, m = 4;
    char grid[][1001] = { { '*', '*', '1', '0' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '0', '1' } };

    findPossibleGrid(n, m, grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    public static boolean PosCheck(char[][] a, int n, int m,
                                   char check)
    {

        // Iterate over the range
        for (int i = 0; i < n; i++) {

            // Iterate over the range
            for (int j = 0; j < m; j++) {

                if (a[i][j] == '*') {
                    continue;
                }
                else {

                    // (i+j)%2==1 cells should be with
                    // the character check and the rest
                    // should be with the other character
                    if ((((i + j) & 1) == 1)
                        && a[i][j] != check) {
                        return false;
                    }
                    if (!(((i + j) & 1) == 1)
                        && a[i][j] == check) {
                        return false;
                    }
                }
            }
        }
        return true;
    }

    // Function to fill the grid in a possible way
    public static void fill(char[][] a, int n, int m,
                            char odd, char even)
    {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (((i + j) & 1) == 1) {
                    a[i][j] = odd;
                }
                else {
                    a[i][j] = even;
                }
            }
        }
    }

    // Function to find if the grid can be made alternating
    public static void findPossibleGrid(int n, int m,
                                        char[][] a)
    {
        boolean flag = true;
        int k = -1, o = -1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                if (a[i][j] != '*') {

                    // If grid contains atleast
                    // one 1 or 0
                    k = i;
                    o = j;
                    break;
                }
            }
            if (k != -1) {
                break;
            }
        }
        if (k != -1) {
            flag = PosCheck(a, n, m, '1');
            if (flag) {
                fill(a, n, m, '1', '0');
            }
            else {
                flag = PosCheck(a, n, m, '0');
                if (flag) {
                    fill(a, n, m, '0', '1');
                }
            }
        }
        else {
            // Fill the grid in any possible way
            char h = '1';
            for (int i = 0; i < m; i++) {
                a[0][i] = h;
                if (h == '1') {
                    h = '0';
                }
                else {
                    h = '1';
                }
            }
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    if (i - 1 < 0) {
                        continue;
                    }
                    if (a[i - 1][j] == '1') {
                        a[i][j] = '0';
                    }
                    else {
                        a[i][j] = '1';
                    }
                }
            }
            flag = true;
        }

        if (!flag) {
            System.out.println("No");
        }
        else {
            System.out.println("Yes");
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    System.out.print(a[i][j]);
                }
                System.out.println();
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4, m = 4;
        char[][] grid = { { '*', '*', '1', '0' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '0', '1' } };

        findPossibleGrid(n, m, grid);
    }
}

// This code is contributed by maddler.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    public static bool PosCheck(char[,] a, int n, int m,
                                   char check)
    {

        // Iterate over the range
        for (int i = 0; i < n; i++) {

            // Iterate over the range
            for (int j = 0; j < m; j++) {

                if (a[i, j] == '*') {
                    continue;
                }
                else {

                    // (i+j)%2==1 cells should be with
                    // the character check and the rest
                    // should be with the other character
                    if ((((i + j) & 1) == 1)
                        && a[i, j] != check) {
                        return false;
                    }
                    if (!(((i + j) & 1) == 1)
                        && a[i, j] == check) {
                        return false;
                    }
                }
            }
        }
        return true;
    }

    // Function to fill the grid in a possible way
    public static void fill(char[,] a, int n, int m,
                            char odd, char even)
    {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (((i + j) & 1) == 1) {
                    a[i, j] = odd;
                }
                else {
                    a[i, j] = even;
                }
            }
        }
    }

    // Function to find if the grid can be made alternating
    public static void findPossibleGrid(int n, int m,
                                        char[,] a)
    {
        bool flag = true;
        int k = -1, o = -1;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                if (a[i, j] != '*') {

                    // If grid contains atleast
                    // one 1 or 0
                    k = i;
                    o = j;
                    break;
                }
            }
            if (k != -1) {
                break;
            }
        }
        if (k != -1) {
            flag = PosCheck(a, n, m, '1');
            if (flag) {
                fill(a, n, m, '1', '0');
            }
            else {
                flag = PosCheck(a, n, m, '0');
                if (flag) {
                    fill(a, n, m, '0', '1');
                }
            }
        }
        else {
            // Fill the grid in any possible way
            char h = '1';
            for (int i = 0; i < m; i++) {
                a[0, i] = h;
                if (h == '1') {
                    h = '0';
                }
                else {
                    h = '1';
                }
            }
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    if (i - 1 < 0) {
                        continue;
                    }
                    if (a[i - 1, j] == '1') {
                        a[i, j] = '0';
                    }
                    else {
                        a[i, j] = '1';
                    }
                }
            }
            flag = true;
        }

        if (!flag) {
            Console.WriteLine("No");
        }
        else {
            Console.WriteLine("Yes");
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < m; j++) {
                    Console.Write(a[i, j]);
                }
                Console.WriteLine();
            }
        }
    }

// Driver Code
public static void Main()
{
        int n = 4, m = 4;
        char[,] grid = { { '*', '*', '1', '0' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '*', '*' },
                          { '*', '*', '0', '1' } };

        findPossibleGrid(n, m, grid);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check for the grid in
// one of the alternating ways
function PosCheck(a, n, m, check)
{

  // Iterate over the range
  for (let i = 0; i < n; i++)
  {

    // Iterate over the range
    for (let j = 0; j < m; j++)
    {
      if (a[i][j] == "*")
      {
        continue;
      }
      else
      {

        // (i+j)%2==1 cells should be with
        // the character check and the rest
        // should be with the other character
        if ((i + j) & 1 && a[i][j] != check) {
          return false;
        }
        if (!((i + j) & 1) && a[i][j] == check) {
          return false;
        }
      }
    }
  }
  return true;
}

// Function to fill the grid in a possible way
function fill(a, n, m, odd, even) {
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < m; j++) {
      if ((i + j) & 1) {
        a[i][j] = odd;
      } else {
        a[i][j] = even;
      }
    }
  }
}

// Function to find if the grid can be made alternating
function findPossibleGrid(n, m, a) {
  let flag = true;
  let k = -1,
    o = -1;
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < m; j++) {
      if (a[i][j] != "*")
      {

        // If grid contains atleast
        // one 1 or 0
        k = i;
        o = j;
        break;
      }
    }
    if (k != -1) {
      break;
    }
  }
  if (k != -1) {
    flag = PosCheck(a, n, m, "1");
    if (flag) {
      fill(a, n, m, "1", "0");
    } else {
      flag = PosCheck(a, n, m, "0");
      if (flag) {
        fill(a, n, m, "0", "1");
      }
    }
  }
  else
  {

    // Fill the grid in any possible way
    let h = "1";
    for (let i = 0; i < m; i++) {
      a[0][i] = h;
      if (h == "1") {
        h = "0";
      } else {
        h = "1";
      }
    }
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < m; j++) {
        if (i - 1 < 0) {
          continue;
        }
        if (a[i - 1][j] == "1") {
          a[i][j] = "0";
        } else {
          a[i][j] = "1";
        }
      }
    }
    flag = true;
  }

  if (!flag) {
    document.write("NO<br>");
  } else {
    document.write("YES<br>");
    for (let i = 0; i < n; i++)
    {
      for (let j = 0; j < m; j++)
      {
        document.write(a[i][j]);
      }
      document.write("<br>");
    }
  }
}

// Driver Code

let n = 4,
  m = 4;
let grid = [
  ["*", "*", "1", "0"],
  ["*", "*", "*", "*"],
  ["*", "*", "*", "*"],
  ["*", "*", "0", "1"],
];

findPossibleGrid(n, m, grid);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
YES
1010
0101
1010
0101
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*