# 布尔矩阵问题

> 原文： [https://www.geeksforgeeks.org/a-boolean-matrix-question/](https://www.geeksforgeeks.org/a-boolean-matrix-question/)

给定大小为`MXN`的布尔矩阵`mat[M][N]`，请对其进行修改，以使如果矩阵单元`mat[i][j]`为 1（或`true`），则使第`i`行和第`j`列的所有单元格均为 1。

```
Example 1
The matrix
1 0
0 0
should be changed to following
1 1
1 0

Example 2
The matrix
0 0 0
0 0 1
should be changed to following
0 0 1
1 1 1

Example 3
The matrix
1 0 0 1
0 0 1 0
0 0 0 0
should be changed to following
1 1 1 1
1 1 1 1
1 0 1 1

```



**方法 1（使用两个临时数组）**：

1.  创建两个临时数组`row[M]`和`col[N]`。 将`row[]`和`col[]`的所有值初始化为 0。

2.  遍历输入矩阵`mat[M][N]`。 如果看到输入`mat[i][j]`为`true`，则将`row[i]`和`col[j]`标记为`true`。

3.  再次遍历输入矩阵`mat[M][N]`。 对于每个入口`mat[i][j]`，检查`row[i]`和`col[j]`的值。 如果两个值（`row[i]`或`col[j]`）中的任何一个为`true`，则将`mat[i][j]`标记为`true`。

感谢 Dixit Sethi 提出了这种方法。

## C++ 

```cpp

// C++ Code For A Boolean Matrix Question 
#include <bits/stdc++.h> 

using namespace std; 
#define R 3 
#define C 4 

void modifyMatrix(bool mat[R][C]) 
{ 
    bool row[R]; 
    bool col[C]; 

    int i, j; 

    /* Initialize all values of row[] as 0 */
    for (i = 0; i < R; i++) 
    { 
    row[i] = 0; 
    } 

    /* Initialize all values of col[] as 0 */
    for (i = 0; i < C; i++) 
    { 
    col[i] = 0; 
    } 

    // Store the rows and columns to be marked as 
    // 1 in row[] and col[] arrays respectively 
    for (i = 0; i < R; i++) 
    { 
        for (j = 0; j < C; j++) 
        { 
            if (mat[i][j] == 1) 
            { 
                row[i] = 1; 
                col[j] = 1; 
            } 
        } 
    } 

    // Modify the input matrix mat[] using the  
    // above constructed row[] and col[] arrays 
    for (i = 0; i < R; i++) 
    { 
        for (j = 0; j < C; j++) 
        { 
            if ( row[i] == 1 || col[j] == 1 ) 
            { 
                mat[i][j] = 1; 
            } 
        } 
    } 
} 

/* A utility function to print a 2D matrix */
void printMatrix(bool mat[R][C]) 
{ 
    int i, j; 
    for (i = 0; i < R; i++) 
    { 
        for (j = 0; j < C; j++) 
        { 
            cout << mat[i][j]; 
        } 
        cout << endl; 
    } 
} 

// Driver Code 
int main() 
{ 
    bool mat[R][C] = { {1, 0, 0, 1}, 
                       {0, 0, 1, 0}, 
                       {0, 0, 0, 0}}; 

    cout << "Input Matrix \n"; 
    printMatrix(mat); 

    modifyMatrix(mat); 

    printf("Matrix after modification \n"); 
    printMatrix(mat); 

    return 0; 
} 

// This code is contributed  
// by Akanksha Rai(Abby_akku) 

```

## Java

```java
// Java Code For A Boolean Matrix Question 
class GFG 
{ 
    public static void modifyMatrix(int mat[ ][ ], int R, int C) 
    { 
        int row[ ]= new int [R]; 
        int col[ ]= new int [C]; 
        int i, j; 
      
        /* Initialize all values of row[] as 0 */
        for (i = 0; i < R; i++) 
        { 
        row[i] = 0; 
        } 
      
      
        /* Initialize all values of col[] as 0 */
        for (i = 0; i < C; i++) 
        { 
        col[i] = 0; 
        } 
      
      
        /* Store the rows and columns to be marked as 
        1 in row[] and col[] arrays respectively */
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                if (mat[i][j] == 1) 
                { 
                    row[i] = 1; 
                    col[j] = 1; 
                } 
            } 
        } 
      
        /* Modify the input matrix mat[] using the 
        above constructed row[] and col[] arrays */
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                if ( row[i] == 1 || col[j] == 1 ) 
                { 
                    mat[i][j] = 1; 
                } 
            } 
        } 
    } 
      
    /* A utility function to print a 2D matrix */
    public static void printMatrix(int mat[ ][ ], int R, int C) 
    { 
        int i, j; 
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                System.out.print(mat[i][j]+ " "); 
            } 
            System.out.println(); 
        } 
    } 
      
    /* Driver program to test above functions */
    public static void main(String[] args)  
    { 
        int mat[ ][ ] = { {1, 0, 0, 1}, 
                          {0, 0, 1, 0}, 
                          {0, 0, 0, 0},}; 
                      
                System.out.println("Matrix Intially"); 
                  
                printMatrix(mat, 3, 4); 
              
                modifyMatrix(mat, 3, 4); 
                System.out.println("Matrix after modification n"); 
                printMatrix(mat, 3, 4); 
              
    }  
  
} 
  
// This code is contributed by Kamal Rawal 
```

## Python3

```py
# Python3 Code For A Boolean Matrix Question 
R = 3
C = 4
  
def modifyMatrix(mat): 
    row = [0] * R  
    col = [0] * C  
      
    # Initialize all values of row[] as 0  
    for i in range(0, R): 
        row[i] = 0
          
    # Initialize all values of col[] as 0  
    for i in range(0, C) : 
        col[i] = 0
  
  
    # Store the rows and columns to be marked  
    # as 1 in row[] and col[] arrays respectively  
    for i in range(0, R) : 
          
        for j in range(0, C) : 
            if (mat[i][j] == 1) : 
                row[i] = 1
                col[j] = 1
              
    # Modify the input matrix mat[] using the  
    # above constructed row[] and col[] arrays  
    for i in range(0, R) : 
          
        for j in range(0, C): 
            if ( row[i] == 1 or col[j] == 1 ) : 
                mat[i][j] = 1
                  
# A utility function to print a 2D matrix  
def printMatrix(mat) : 
    for i in range(0, R): 
          
        for j in range(0, C) : 
            print(mat[i][j], end = " ") 
        print() 
          
# Driver Code 
mat = [ [1, 0, 0, 1], 
        [0, 0, 1, 0], 
        [0, 0, 0, 0] ]  
  
print("Input Matrix n") 
printMatrix(mat) 
  
modifyMatrix(mat) 
  
print("Matrix after modification n") 
printMatrix(mat) 
  
# This code is contributed by Nikita Tiwari. 
```

## C#

```cs
// C# Code For A Boolean 
// Matrix Question 
using System; 
  
class GFG 
{ 
    public static void modifyMatrix(int [,]mat,  
                                    int R, int C) 
    { 
        int []row = new int [R]; 
        int []col = new int [C]; 
        int i, j; 
      
        /* Initialize all values 
        of row[] as 0 */
        for (i = 0; i < R; i++) 
        { 
        row[i] = 0; 
        } 
      
      
        /* Initialize all values 
        of col[] as 0 */
        for (i = 0; i < C; i++) 
        { 
        col[i] = 0; 
        } 
      
      
        /* Store the rows and columns  
        to be marked as 1 in row[]  
        and col[] arrays respectively */
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                if (mat[i, j] == 1) 
                { 
                    row[i] = 1; 
                    col[j] = 1; 
                } 
            } 
        } 
      
        /* Modify the input matrix  
        mat[] using the above  
        constructed row[] and  
        col[] arrays */
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                if (row[i] == 1 || col[j] == 1) 
                { 
                    mat[i, j] = 1; 
                } 
            } 
        } 
    } 
      
    /* A utility function to 
    print a 2D matrix */
    public static void printMatrix(int [,]mat,  
                                   int R, int C) 
    { 
        int i, j; 
        for (i = 0; i < R; i++) 
        { 
            for (j = 0; j < C; j++) 
            { 
                Console.Write(mat[i, j] + " "); 
            } 
            Console.WriteLine(); 
        } 
    } 
      
    // Driver code 
    static public void Main () 
    { 
        int [,]mat = {{1, 0, 0, 1}, 
                      {0, 0, 1, 0}, 
                      {0, 0, 0, 0}}; 
              
        Console.WriteLine("Matrix Intially"); 
          
        printMatrix(mat, 3, 4); 
      
        modifyMatrix(mat, 3, 4); 
        Console.WriteLine("Matrix after "+ 
                        "modification n"); 
        printMatrix(mat, 3, 4); 
          
    } 
} 
  
// This code is contributed by ajit 
```

## PHP

```php
<?php  
// PHP Code For A Boolean 
// Matrix Question 
$R = 3; 
$C = 4; 
  
function modifyMatrix(&$mat) 
{ 
    global $R,$C; 
    $row = array(); 
    $col = array(); 
  
    /* Initialize all values  
       of row[] as 0 */
    for ($i = 0; $i < $R; $i++) 
    { 
        $row[$i] = 0; 
    } 
  
  
    /* Initialize all values  
       of col[] as 0 */
    for ($i = 0; $i < $C; $i++) 
    { 
        $col[$i] = 0; 
    } 
  
  
    /* Store the rows and columns  
       to be marked as 1 in row[]  
       and col[] arrays respectively */
    for ($i = 0; $i < $R; $i++) 
    { 
        for ($j = 0; $j < $C; $j++) 
        { 
            if ($mat[$i][$j] == 1) 
            { 
                $row[$i] = 1; 
                $col[$j] = 1; 
            } 
        } 
    } 
  
    /* Modify the input matrix mat[] 
       using the above constructed  
       row[] and col[] arrays */
    for ($i = 0; $i < $R; $i++) 
    { 
        for ($j = 0; $j < $C; $j++) 
        { 
            if ($row[$i] == 1 ||  
                $col[$j] == 1 ) 
            { 
                $mat[$i][$j] = 1; 
            } 
        } 
    } 
} 
  
/* A utility function to 
   print a 2D matrix */
function printMatrix(&$mat) 
{ 
    global $R, $C; 
    for ($i = 0; $i < $R; $i++) 
    { 
        for ($j = 0; $j < $C; $j++) 
        { 
            echo $mat[$i][$j] . " "; 
        } 
        echo "\n"; 
    } 
} 
  
// Driver code  
$mat = array(array(1, 0, 0, 1), 
             array(0, 0, 1, 0), 
             array(0, 0, 0, 0)); 
  
echo "Input Matrix \n"; 
printMatrix($mat); 
  
modifyMatrix($mat); 
  
echo "Matrix after modification \n"; 
printMatrix($mat); 
  
// This code is contributed  
// by ChitraNayal 
?> 
```

输出：

```
Input Matrix
1 0 0 1
0 0 1 0
0 0 0 0
Matrix after modification
1 1 1 1
1 1 1 1
1 0 1 1
```

时间复杂度：`O(M * N)`。

辅助空间：`O(M + N)`。

方法 2（方法 1 的空间优化版本）：

该方法是上述方法 1 的空间优化版本。该方法使用输入矩阵的第一行和第一列代替方法 1 的辅助数组`row[]`和`col[]`。因此，我们要做的是：首先注意第一行和第一列，并将这两个信息存储在两个标志变量`rowFlag`和`colFlag`中。获得此信息后，我们可以将第一行和第一列用作辅助数组，并将方法1应用于大小为`(M-1) * (N-1)`）的子矩阵（不包括第一行和第一列的矩阵）。

1）扫描第一行并设置一个变量`rowFlag`以指示是否需要在第一行中设置全 1。
2）扫描第一列并设置变量`colFlag`以指示是否需要在第一列中设置全 1。
3）分别使用第一行和第一列作为辅助数组`row[]`和`col[]`，将矩阵视为从第二行和第二列开始的子矩阵，并应用方法 1。
4）最后，如果需要，使用`rowFlag`和`colFlag`更新第一行和第一列。

时间复杂度：`O(M * N)`。

辅助空间：`O(1)`。

感谢 Sidh 提出了这种方法。

## C++

```cpp
#include <bits/stdc++.h> 
using namespace std; 
#define R 3 
#define C 4 
  
void modifyMatrix(int mat[R][C]) 
{ 
    // variables to check if there are any 1 
    // in first row and column 
    bool row_flag = false; 
    bool col_flag = false; 
  
    // updating the first row and col if 1 
    // is encountered 
    for (int i = 0; i < R; i++) { 
        for (int j = 0; j < C; j++) { 
            if (i == 0 && mat[i][j] == 1) 
                row_flag = true; 
  
            if (j == 0 && mat[i][j] == 1) 
                col_flag = true; 
  
            if (mat[i][j] == 1) { 
  
                mat[0][j] = 1; 
                mat[i][0] = 1; 
            } 
        } 
    } 
  
    // Modify the input matrix mat[] using the 
    // first row and first column of Matrix mat 
    for (int i = 1; i < R; i++) { 
        for (int j = 1; j < C; j++) { 
  
            if (mat[0][j] == 1 || mat[i][0] == 1) { 
                mat[i][j] = 1; 
            } 
        } 
    } 
  
    // modify first row if there was any 1 
    if (row_flag == true) { 
        for (int i = 0; i < C; i++) { 
            mat[0][i] = 1; 
        } 
    } 
  
    // modify first col if there was any 1 
    if (col_flag == true) { 
        for (int i = 0; i < R; i++) { 
            mat[i][0] = 1; 
        } 
    } 
} 
  
/* A utility function to print a 2D matrix */
void printMatrix(int mat[R][C]) 
{ 
    for (int i = 0; i < R; i++) { 
        for (int j = 0; j < C; j++) { 
            cout << mat[i][j]; 
        } 
        cout << "\n"; 
    } 
} 
  
// Driver function to test the above function 
int main() 
{ 
  
    int mat[R][C] = { { 1, 0, 0, 1 }, 
                      { 0, 0, 1, 0 }, 
                      { 0, 0, 0, 0 } }; 
  
    cout << "Input Matrix :\n"; 
    printMatrix(mat); 
  
    modifyMatrix(mat); 
  
    cout << "Matrix After Modification :\n"; 
    printMatrix(mat); 
    return 0; 
} 
  
// This code is contributed by Nikita Tiwari 
```

## Java

```java
class GFG 
{  
    public static void modifyMatrix(int mat[][]){ 
                  
        // variables to check if there are any 1  
        // in first row and column 
        boolean row_flag = false; 
        boolean col_flag = false; 
                  
        // updating the first row and col if 1 
        // is encountered 
        for (int i = 0; i < mat.length; i++ ){ 
                for (int j = 0; j < mat[0].length; j++){ 
                        if (i == 0 && mat[i][j] == 1) 
                            row_flag = true; 
                          
                        if (j == 0 && mat[i][j] == 1) 
                            col_flag = true; 
                          
                        if (mat[i][j] == 1){ 
                              
                            mat[0][j] = 1; 
                            mat[i][0] = 1; 
                        } 
                          
                    } 
                } 
                  
        // Modify the input matrix mat[] using the  
        // first row and first column of Matrix mat 
        for (int i = 1; i < mat.length; i ++){ 
                for (int j = 1; j < mat[0].length; j ++){ 
                          
                    if (mat[0][j] == 1 || mat[i][0] == 1){ 
                            mat[i][j] = 1; 
                        } 
                    } 
                } 
                  
        // modify first row if there was any 1 
        if (row_flag == true){ 
            for (int i = 0; i < mat[0].length; i++){ 
                        mat[0][i] = 1; 
                    } 
                } 
                  
        // modify first col if there was any 1 
        if (col_flag == true){ 
            for (int i = 0; i < mat.length; i ++){ 
                        mat[i][0] = 1; 
            } 
        } 
    } 
              
    /* A utility function to print a 2D matrix */
    public static void printMatrix(int mat[][]){ 
        for (int i = 0; i < mat.length; i ++){ 
            for (int j = 0; j < mat[0].length; j ++){ 
                System.out.print( mat[i][j] ); 
            } 
                System.out.println(""); 
        } 
    } 
              
    // Driver function to test the above function 
    public static void main(String args[] ){ 
                  
        int mat[][] = {{1, 0, 0, 1}, 
                {0, 0, 1, 0}, 
                {0, 0, 0, 0}}; 
                  
        System.out.println("Input Matrix :"); 
        printMatrix(mat); 
              
        modifyMatrix(mat); 
              
        System.out.println("Matrix After Modification :"); 
        printMatrix(mat); 
              
    } 
} 
  
// This code is contributed by Arnav Kr. Mandal. 
```

## Python3

```py
# Python3 Code For A Boolean Matrix Question 
def modifyMatrix(mat) : 
      
    # variables to check if there are any 1  
    # in first row and column 
    row_flag = False
    col_flag = False
              
    # updating the first row and col  
    # if 1 is encountered 
    for i in range(0, len(mat)) : 
          
        for j in range(0, len(mat)) : 
            if (i == 0 and mat[i][j] == 1) : 
                row_flag = True
                      
            if (j == 0 and mat[i][j] == 1) : 
                col_flag = True
              
            if (mat[i][j] == 1) : 
                mat[0][j] = 1
                mat[i][0] = 1
                  
    # Modify the input matrix mat[] using the  
    # first row and first column of Matrix mat 
    for i in range(1, len(mat)) : 
          
        for j in range(1, len(mat) + 1) : 
            if (mat[0][j] == 1 or mat[i][0] == 1) : 
                mat[i][j] = 1
                  
    # modify first row if there was any 1 
    if (row_flag == True) : 
        for i in range(0, len(mat)) : 
            mat[0][i] = 1
              
    # modify first col if there was any 1 
    if (col_flag == True) : 
        for i in range(0, len(mat)) : 
            mat[i][0] = 1
              
# A utility function to print a 2D matrix 
def printMatrix(mat) : 
      
    for i in range(0, len(mat)) : 
        for j in range(0, len(mat) + 1) : 
            print( mat[i][j], end = "" ) 
          
        print() 
          
# Driver Code 
mat = [ [1, 0, 0, 1], 
        [0, 0, 1, 0], 
        [0, 0, 0, 0] ] 
          
print("Input Matrix :") 
printMatrix(mat) 
      
modifyMatrix(mat) 
      
print("Matrix After Modification :") 
printMatrix(mat) 
  
# This code is contributed by Nikita tiwari. 
```

## C#

```cs
// C# Code For A Boolean 
// Matrix Question 
using System; 
  
class GFG 
{  
    public static void modifyMatrix(int[,] mat) 
    { 
                  
        // variables to check  
        // if there are any 1  
        // in first row and column 
        bool row_flag = false; 
        bool col_flag = false; 
                  
        // updating the first 
        // row and col if 1 
        // is encountered 
        for (int i = 0; 
                 i < mat.GetLength(0); i++ ) 
        { 
                for (int j = 0;  
                         j < mat.GetLength(1); j++) 
                { 
                        if (i == 0 && mat[i, j] == 1) 
                            row_flag = true; 
                          
                        if (j == 0 && mat[i, j] == 1) 
                            col_flag = true; 
                          
                        if (mat[i, j] == 1) 
                        { 
                            mat[0, j] = 1; 
                            mat[i,0] = 1; 
                        } 
                          
                    } 
                } 
                  
        // Modify the input matrix mat[]  
        // using the first row and first 
        // column of Matrix mat 
        for (int i = 1;  
                 i < mat.GetLength(0); i ++) 
        { 
                for (int j = 1;  
                         j < mat.GetLength(1); j ++) 
                { 
                          
                    if (mat[0, j] == 1 ||  
                        mat[i, 0] == 1) 
                    { 
                            mat[i, j] = 1; 
                        } 
                    } 
                } 
                  
        // modify first row 
        // if there was any 1 
        if (row_flag == true) 
        { 
            for (int i = 0;  
                     i < mat.GetLength(1); i++) 
            { 
                        mat[0, i] = 1; 
            } 
        } 
                  
        // modify first col if 
        // there was any 1 
        if (col_flag == true) 
        { 
            for (int i = 0;  
                     i < mat.GetLength(0); i ++) 
            { 
                        mat[i, 0] = 1; 
            } 
        } 
    } 
              
    /* A utility function  
    to print a 2D matrix */
    public static void printMatrix(int[,] mat) 
    { 
        for (int i = 0;  
                 i < mat.GetLength(0); i ++) 
        { 
            for (int j = 0;  
                     j < mat.GetLength(1); j ++) 
            { 
                Console.Write(mat[i, j] + " " ); 
            } 
                Console.Write("\n"); 
        } 
    } 
              
    // Driver Code 
    public static void Main() 
    { 
        int[,] mat = {{1, 0, 0, 1}, 
                      {0, 0, 1, 0}, 
                      {0, 0, 0, 0}}; 
                  
        Console.Write("Input Matrix :\n"); 
        printMatrix(mat); 
              
        modifyMatrix(mat); 
              
        Console.Write("Matrix After " +  
                      "Modification :\n"); 
        printMatrix(mat); 
    } 
} 
  
// This code is contributed 
// by ChitraNayal 
```

## PHP

```php
<?php  
// PHP Code For A Boolean 
// Matrix Question 
$R = 3; 
$C = 4; 
  
function modifyMatrix(&$mat) 
{ 
    global $R, $C; 
      
    // variables to check if  
    // there are any 1 in  
    // first row and column 
    $row_flag = false; 
    $col_flag = false; 
  
    // updating the first  
    // row and col if 1 
    // is encountered 
    for ($i = 0; $i < $R; $i++)  
    { 
        for ($j = 0; $j < $C; $j++)  
        { 
            if ($i == 0 && $mat[$i][$j] == 1) 
                $row_flag = true; 
  
            if ($j == 0 && $mat[$i][$j] == 1) 
                $col_flag = true; 
  
            if ($mat[$i][$j] == 1)  
            { 
                $mat[0][$j] = 1; 
                $mat[$i][0] = 1; 
            } 
        } 
    } 
  
    // Modify the input matrix  
    // mat[] using the first  
    // row and first column of  
    // Matrix mat 
    for ($i = 1; $i < $R; $i++)  
    { 
        for ($j = 1; $j < $C; $j++) 
        { 
            if ($mat[0][$j] == 1 ||  
                $mat[$i][0] == 1) 
            { 
                $mat[$i][$j] = 1; 
            } 
        } 
    } 
  
    // modify first row  
    // if there was any 1 
    if ($row_flag == true)  
    { 
        for ($i = 0; $i < $C; $i++) 
        { 
            $mat[0][$i] = 1; 
        } 
    } 
  
    // modify first col  
    // if there was any 1 
    if ($col_flag == true)  
    { 
        for ($i = 0; $i < $R; $i++) 
        { 
            $mat[$i][0] = 1; 
        } 
    } 
} 
  
/* A utility function 
to print a 2D matrix */
function printMatrix(&$mat) 
{ 
    global $R, $C; 
    for ($i = 0; $i < $R; $i++)  
    { 
        for ($j = 0; $j < $C; $j++) 
        { 
            echo $mat[$i][$j]." "; 
        } 
        echo "\n"; 
    } 
} 
  
// Driver Code 
$mat = array(array(1, 0, 0, 1 ), 
             array(0, 0, 1, 0 ), 
             array(0, 0, 0, 0 )); 
  
echo "Input Matrix :\n"; 
printMatrix($mat); 
  
modifyMatrix($mat); 
  
echo "Matrix After Modification :\n"; 
printMatrix($mat); 
  
// This code is conrtributed  
// by ChitraNayal 
?> 
```

输出：

```
Input Matrix :
1001
0010
0000
Matrix After Modification :
1111
1111
1011
```

