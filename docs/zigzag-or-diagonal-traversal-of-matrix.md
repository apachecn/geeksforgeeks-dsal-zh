# 矩阵的 Z 字形（或对角线）遍历

> 原文： [https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)

给定 2D 矩阵，以对角线顺序打印给定矩阵的所有元素。 例如，考虑以下`5 X 4`输入矩阵。

```
    1     2     3     4
    5     6     7     8
    9    10    11    12
   13    14    15    16
   17    18    19    20
```

上述矩阵的对角线打印是：

```
    1
    5     2
    9     6     3
   13    10     7     4
   17    14    11     8
   18    15    12
   19    16
   20
```

另一个示例：

![diagonal-matrix](img/cb40b044ad1013046f6267770166bd9e.png) 

## 强烈建议您在继续解决方案之前，单击这里进行练习。

以下是对角线打印的代码。

给定矩阵`matrix[ROW][COL]`的对角打印输出中始终带有`ROW + COL – 1`行。

## C++ 

```cpp

#include <stdio.h> 
#include <stdlib.h> 

#define ROW 5 
#define COL 4 

// A utility function to find min of two integers 
int minu(int a, int b) 
{ return (a < b)? a: b; } 

// A utility function to find min of three integers 
int min(int a, int b, int c) 
{ return minu(minu(a, b), c);} 

// A utility function to find max of two integers 
int max(int a, int b) 
{ return (a > b)? a: b; } 

// The main function that prints given matrix in diagonal order 
void diagonalOrder(int matrix[][COL]) 
{ 
    // There will be ROW+COL-1 lines in the output 
    for (int line=1; line<=(ROW + COL -1); line++) 
    { 
        /* Get column index of the first element in this line of output. 
           The index is 0 for first ROW lines and line - ROW for remaining 
           lines  */
        int start_col =  max(0, line-ROW); 

        /* Get count of elements in this line. The count of elements is 
           equal to minimum of line number, COL-start_col and ROW */
         int count = min(line, (COL-start_col), ROW); 

        /* Print elements of this line */
        for (int j=0; j<count; j++) 
            printf("%5d ", matrix[minu(ROW, line)-j-1][start_col+j]); 

        /* Ptint elements of next diagonal on next line */
        printf("\n"); 
    } 
} 

// Utility function to print a matrix 
void printMatrix(int matrix[ROW][COL]) 
{ 
    for (int i=0; i< ROW; i++) 
    { 
        for (int j=0; j<COL; j++) 
            printf("%5d ", matrix[i][j]); 
        printf("\n"); 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    int M[ROW][COL] = {{1, 2, 3, 4}, 
                       {5, 6, 7, 8}, 
                       {9, 10, 11, 12}, 
                       {13, 14, 15, 16}, 
                       {17, 18, 19, 20}, 
                      }; 
    printf ("Given matrix is \n"); 
    printMatrix(M); 

    printf ("\nDiagonal printing of matrix is \n"); 
    diagonalOrder(M); 
    return 0; 
} 

```

## Java

```java
class GFG { 
static final int ROW = 5; 
static final int COL = 4; 
  
// A utility function to find min  
// of two integers 
static int min(int a, int b) { 
    return (a < b) ? a : b; 
    } 
  
// A utility function to find min 
// of three integers 
static int min(int a, int b, int c) { 
    return min(min(a, b), c); 
    } 
  
// A utility function to find max  
// of two integers 
static int max(int a, int b) {  
    return (a > b) ? a : b; 
    } 
  
// The main function that prints given 
// matrix in diagonal order 
static void diagonalOrder(int matrix[][]) { 
  
    // There will be ROW+COL-1 lines in the output 
    for (int line = 1; line <= (ROW + COL - 1); line++) { 
  
    // Get column index of the first element in this 
    // line of output.The index is 0 for first ROW 
    // lines and line - ROW for remaining lines 
    int start_col = max(0, line - ROW); 
  
    // Get count of elements in this line. The count 
    // of elements is equal to minimum of line number, 
    // COL-start_col and ROW  
    int count = min(line, (COL - start_col), ROW); 
  
    // Print elements of this line  
    for (int j = 0; j < count; j++) 
        System.out.print(matrix[min(ROW, line) - j - 1] 
                            [start_col + j] + " "); 
  
    // Print elements of next diagonal on next line 
    System.out.println(); 
    } 
} 
  
// Utility function to print a matrix 
static void printMatrix(int matrix[][]) { 
    for (int i = 0; i < ROW; i++) { 
    for (int j = 0; j < COL; j++) 
        System.out.print(matrix[i][j] + " "); 
    System.out.print("\n"); 
    } 
} 
  
// Driver code 
public static void main(String[] args) { 
    int M[][] = { 
        {1, 2, 3, 4},     {5, 6, 7, 8},     {9, 10, 11, 12}, 
        {13, 14, 15, 16}, {17, 18, 19, 20}, 
    }; 
    System.out.print("Given matrix is \n"); 
    printMatrix(M); 
  
    System.out.print("\nDiagonal printing of matrix is \n"); 
    diagonalOrder(M); 
} 
} 
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 program to print all elements 
# of given matrix in diagonal order 
ROW = 5
COL = 4
  
# Main function that prints given 
# matrix in diagonal order 
def diagonalOrder(matrix) : 
      
    # There will be ROW+COL-1 lines in the output 
    for line in range(1, (ROW + COL)) : 
        # Get column index of the first element 
        # in this line of output. The index is 0 
        # for first ROW lines and line - ROW for 
        # remaining lines  
        start_col = max(0, line - ROW) 
  
        # Get count of elements in this line. 
        # The count of elements is equal to 
        # minimum of line number, COL-start_col and ROW  
        count = min(line, (COL - start_col), ROW) 
  
        # Print elements of this line  
        for j in range(0, count) : 
            print(matrix[min(ROW, line) - j - 1] 
                        [start_col + j], end = "\t") 
  
        print() 
      
      
# Utility function to print a matrix 
def printMatrix(matrix) : 
    for i in range(0, ROW) : 
        for j in range(0, COL) : 
            print(matrix[i][j], end = "\t") 
              
        print() 
          
  
# Driver COde 
M = [ [1, 2, 3, 4], 
    [5, 6, 7, 8], 
    [9, 10, 11, 12], 
    [13, 14, 15, 16], 
    [17, 18, 19, 20] ] 
print("Given matrix is ") 
printMatrix(M) 
  
print ("\nDiagonal printing of matrix is ") 
diagonalOrder(M) 
  
# This code is contributed by Nikita Tiwari.
```

## C#

```cs
// C# program to print all elements 
// of given matrix in diagonal order 
using System; 
  
class GFG { 
      
    static int ROW = 5; 
    static int COL = 4; 
  
      
    // The main function that prints given 
    // matrix in diagonal order 
    static void diagonalOrder(int [,]matrix) { 
      
        // There will be ROW+COL-1 lines in the output 
        for (int line = 1; line <= (ROW + COL - 1); line++) 
        { 
      
            // Get column index of the first element 
            // in this line of output.The index is 0  
            // for first ROW lines and line - ROW for  
            // remaining lines 
            int start_col = Math.Max(0, line - ROW); 
          
            // Get count of elements in this line. The 
            // count of elements is equal to minimum of  
            // line number, COL-start_col and ROW  
            int count = Math.Min(line, Math.Min( 
                                  (COL - start_col), ROW)); 
      
            // Print elements of this line  
            for (int j = 0; j < count; j++) 
                Console.Write(matrix[ Math.Min(ROW, line)  
                            - j - 1, start_col + j] + " "); 
          
            // Print elements of next diagonal on next line 
            Console.WriteLine(); 
        } 
    } 
      
    // Utility function to print a matrix 
    static void printMatrix(int [,]matrix) { 
        for (int i = 0; i < ROW; i++) { 
            for (int j = 0; j < COL; j++) 
                Console.Write(matrix[i,j] + " "); 
                  
            Console.WriteLine("\n"); 
        } 
    } 
      
    // Driver code 
    public static void Main() { 
        int [,]M = {{1, 2, 3, 4}, 
                    {5, 6, 7, 8}, 
                    {9, 10, 11, 12}, 
                    {13, 14, 15, 16},  
                    {17, 18, 19, 20}}; 
                      
        Console.Write("Given matrix is \n"); 
        printMatrix(M); 
      
        Console.Write("\nDiagonal printing" 
                     + " of matrix is \n"); 
                       
        diagonalOrder(M); 
    } 
} 
  
// This code is contributed by Sam007.
```

## PHP

```php
<?php  
// PHP Code for Zigzag (or diagonal)  
// traversal of Matrix 
$ROW = 5; 
$COL = 4; 
  
// The main function that prints  
// given matrix in diagonal order 
function diagonalOrder(&$matrix) 
{ 
    global $ROW, $COL; 
      
    // There will be ROW+COL-1 
    // lines in the output 
    for ($line = 1;  
         $line <= ($ROW + $COL - 1); $line++) 
    { 
        /* Get column index of the first 
           element in this line of output. 
           The index is 0 for first ROW lines 
           and line - ROW for remaining lines */
        $start_col = max(0, $line - $ROW); 
  
        /* Get count of elements in this line. 
           The count of elements is equal to 
           minimum of line number, COL-start_col  
           and ROW */
        $count = min($line, ($COL -  
                     $start_col), $ROW); 
  
        /* Print elements of this line */
        for ($j = 0; $j < $count; $j++) 
        { 
            echo $matrix[min($ROW, $line) -  
                 $j - 1][$start_col + $j]; 
            echo "\t"; 
        } 
  
        /* Print elements of next  
           diagonal on next line */
        print("\n"); 
    } 
} 
  
// Utility function  
// to print a matrix 
function printMatrix(&$matrix) 
{ 
    global $ROW, $COL; 
    for ($i = 0; $i < $ROW; $i++) 
    { 
        for ($j = 0; $j < $COL; $j++) 
        { 
            echo $matrix[$i][$j] ; 
            echo "\t"; 
        } 
        print("\n"); 
    } 
} 
  
// Driver Code 
$M = array(array(1, 2, 3, 4), 
           array(5, 6, 7, 8), 
           array(9, 10, 11, 12), 
           array(13, 14, 15, 16), 
           array(17, 18, 19, 20)); 
echo "Given matrix is \n"; 
printMatrix($M); 
  
printf ("\nDiagonal printing " . 
        "of matrix is \n"); 
diagonalOrder($M); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
Given matrix is
    1     2     3     4
    5     6     7     8
    9    10    11    12
   13    14    15    16
   17    18    19    20

Diagonal printing of matrix is
    1
    5     2
    9     6     3
   13    10     7     4
   17    14    11     8
   18    15    12
   19    16
   20
```

下面是解决上述问题的替代方法。

```
Matrix =>       1     2     3     4
                5     6     7     8
                9     10    11   12
                13    14    15   16
                17    18    19   20 
   
Observe the sequence
          1 /  2 /  3 /  4
           / 5  /  6 /  7 /  8
               /  9 / 10 / 11 / 12
                   / 13 / 14 / 15 / 16
                       / 17 / 18 / 19 / 20
```

## C++

```cpp
#include<bits/stdc++.h> 
#define R 5 
#define C 4 
using namespace std; 
  
bool isValid(int i, int j) 
{ 
    if (i < 0 || i >= R || j >= C || j < 0) return false; 
    return true; 
} 
  
void diagonalOrder(int arr[][C]) 
{ 
    /* through this for loop we choose each element of first column 
    as starting point and print diagonal starting at it. 
    arr[0][0], arr[1][0]....arr[R-1][0] are all starting points */
    for (int k = 0; k < R; k++) 
    { 
        cout << arr[k][0] << " "; 
        int i = k-1;    // set row index for next point in diagonal 
        int j = 1;        //    set column index for next point in diagonal 
  
        /* Print Diagonally upward */
        while (isValid(i,j)) 
        { 
            cout << arr[i][j] << " "; 
            i--; 
            j++;    // move in upright direction 
        } 
        cout << endl; 
    } 
  
    /* through this for loop we choose each element of last row 
       as starting point (except the [0][c-1] it has already been 
       processed in previous for loop) and print diagonal starting at it. 
       arr[R-1][0], arr[R-1][1]....arr[R-1][c-1] are all starting points */
  
    //Note : we start from k = 1 to C-1; 
    for (int k = 1; k < C; k++) 
    { 
        cout << arr[R-1][k] << " "; 
        int i = R-2; // set row index for next point in diagonal 
        int j = k+1; // set column index for next point in diagonal 
  
        /* Print Diagonally upward */
        while (isValid(i,j)) 
        { 
            cout << arr[i][j] << " "; 
            i--; 
            j++; // move in upright direction 
        } 
        cout << endl; 
    } 
} 
  
// Driver program to test above 
int main() 
{ 
  
    int arr[][C] = {{1, 2, 3, 4}, 
        {5, 6, 7, 8}, 
        {9, 10, 11, 12}, 
        {13, 14, 15, 16}, 
        {17, 18, 19, 20}, 
    }; 
    diagonalOrder(arr); 
    return 0; 
}
```

## Java

```java
// JAVA Code for Zigzag (or diagonal)  
// traversal of Matrix 
    
   class GFG{ 
     
     public static int R,C; 
       
     private static void diagonalOrder(int[][] arr) { 
           
             /* through this for loop we choose each element 
             of first column as starting point and print  
             diagonal starting at it. arr[0][0], arr[1][0] 
             ....arr[R-1][0] are all starting points */
             for (int k = 0; k < R; k++) 
             { 
                 System.out.print(arr[k][0] + " "); 
                   
                 int i = k - 1;    // set row index for next 
                                   // point in diagonal 
                 int j = 1;       //  set column index for  
                                  // next point in diagonal 
            
                 /* Print Diagonally upward */
                 while (isValid(i, j)) 
                 { 
                     System.out.print(arr[i][j] + " "); 
                       
                     i--; 
                     j++;    // move in upright direction 
                 } 
                   
                 System.out.println(""); 
             } 
            
             /* through this for loop we choose each element 
                of last row as starting point (except the  
                [0][c-1] it has already been processed in  
                previous for loop) and print diagonal  
                starting at it. arr[R-1][0], arr[R-1][1].... 
                arr[R-1][c-1] are all starting points */
            
             // Note : we start from k = 1 to C-1; 
             for (int k = 1; k < C; k++) 
             { 
                 System.out.print(arr[R-1][k] + " "); 
                   
                 int i = R - 2; // set row index for next  
                                // point in diagonal 
                 int j = k + 1; // set column index for   
                                // next point in diagonal 
            
                 /* Print Diagonally upward */
                 while (isValid(i, j)) 
                 { 
                     System.out.print(arr[i][j] + " "); 
                       
                     i--; 
                     j++; // move in upright direction 
                 } 
                   
                 System.out.println(""); 
             } 
         } 
              
    public static  boolean isValid(int i, int j) 
     { 
         if (i < 0 || i >= R || j >= C || j < 0) return false; 
         return true; 
     } 
       
          // driver program to test above function 
          public static void main(String[] args) { 
              int arr[][] = { {1, 2, 3, 4}, 
                              {5, 6, 7, 8}, 
                              {9, 10, 11, 12}, 
                              {13, 14, 15, 16}, 
                              {17, 18, 19, 20}, }; 
                
              R=arr.length; 
              C=arr[0].length; 
                
              diagonalOrder(arr); 
        } 
 } 
          
    // This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 program to print all elements 
# of given matrix in diagonal order 
R = 5
C = 4
  
def isValid( i, j) : 
    if (i < 0 or i >= R or j >= C or j < 0) : 
        return False
    return True
      
  
def diagonalOrder(arr) : 
      
    # through this for loop we choose each element 
    # of first column as starting point and print 
    # diagonal starting at it.  
    # arr[0][0], arr[1][0]....arr[R-1][0] 
    # are all starting points  
    for k in range(0, R) : 
        print(arr[k][0], end = "  ") 
          
        # set row index for next point in diagonal 
        i = k - 1 
          
        # set column index for next point in diagonal 
        j = 1    
  
        # Print Diagonally upward  
        while (isValid(i, j)) : 
            print(arr[i][j], end = "  ") 
            i -= 1
            j += 1 # move in upright direction 
          
        print() 
  
    # Through this for loop we choose each  
    # element of last row as starting point 
    # (except the [0][c-1] it has already been 
    # processed in previous for loop) and print 
    # diagonal starting at it. 
    # arr[R-1][0], arr[R-1][1]....arr[R-1][c-1] 
    # are all starting points 
  
    # Note : we start from k = 1 to C-1; 
    for k in range(1, C) : 
        print(arr[R-1][k], end = "  ") 
          
        # set row index for next point in diagonal 
        i = R - 2
          
        # set column index for next point in diagonal 
        j = k + 1     
  
        # Print Diagonally upward  
        while (isValid(i, j)) : 
            print( arr[i][j], end = "  ") 
            i -= 1
            j += 1 # move in upright direction 
          
        print() 
          
# Driver Code 
arr = [ [1, 2, 3, 4], 
        [5, 6, 7, 8], 
        [9, 10, 11, 12], 
        [13, 14, 15, 16], 
        [17, 18, 19, 20] ] 
diagonalOrder(arr) 
  
# This code is contributed by Nikita Tiwari.
```

## C#

```cs
// C# Code for Zigzag (or diagonal)  
// traversal of Matrix 
using System; 
  
class GFG 
{ 
public static int R, C; 
  
private static void diagonalOrder(int[,] arr)  
{ 
      
    /* through this for loop we  
    choose each element of first 
    column as starting point and  
    print diagonal starting at it.  
    arr[0,0], arr[1,0]....arr[R-1,0]  
    are all starting points */
    for (int k = 0; k < R; k++) 
    { 
        Console.Write(arr[k, 0] + " "); 
          
        int i = k - 1;  // set row index for next 
                        // point in diagonal 
        int j = 1;    // set column index for  
                    // next point in diagonal 
      
        /* Print Diagonally upward */
        while (isValid(i, j)) 
        { 
            Console.Write(arr[i, j] + " "); 
              
            i--; 
            j++; // move in upright direction 
        } 
          
        Console.Write("\n"); 
    } 
      
    /*  through this for loop we  
        choose each element of last  
        row as starting point (except  
        the [0][c-1] it has already  
        been processed in previous for  
        loop) and print diagonal starting 
        at it. arr[R-1,0], arr[R-1,1].... 
        arr[R-1,c-1] are all starting points */
      
    // Note : we start from k = 1 to C-1; 
    for (int k = 1; k < C; k++) 
    { 
        Console.Write(arr[R - 1, k] + " "); 
          
        int i = R - 2;  // set row index for next  
                        // point in diagonal 
        int j = k + 1;  // set column index for  
                        // next point in diagonal 
      
        /* Print Diagonally upward */
        while (isValid(i, j)) 
        { 
            Console.Write(arr[i, j] + " "); 
              
            i--; 
            j++; // move in upright direction 
        } 
          
        Console.Write("\n"); 
    } 
} 
      
public static bool isValid(int i, int j) 
{ 
    if (i < 0 || i >= R ||  
        j >= C || j < 0) return false; 
    return true; 
} 
  
// Driver code 
public static void Main()  
{ 
    int [,]arr = {{1, 2, 3, 4}, 
                  {5, 6, 7, 8}, 
                  {9, 10, 11, 12}, 
                  {13, 14, 15, 16}, 
                  {17, 18, 19, 20}}; 
          
    R = arr.GetLength(0); 
    C = arr.GetLength(1); 
          
    diagonalOrder(arr); 
} 
} 
  
// This code is contributed  
// by ChitraNayal
```

## PHP

```php
<?php 
// PHP code for Zigzag (or diagonal)  
// traversal of Matrix 
define("R", 5);  
define("C", 4);  
  
function isValid($i, $j)  
{  
    if ($i < 0 || $i >= R ||  
        $j >= C || $j < 0) return false;  
    return true;  
}  
  
function diagonalOrder(&$arr)  
{  
    /* through this for loop we choose  
    each element of first column as  
    starting point and print diagonal   
    starting at it.  
    arr[0][0], arr[1][0]....arr[R-1][0] 
    are all starting points */
    for ($k = 0; $k < R; $k++)  
    {  
        echo $arr[$k][0] . " ";  
        $i = $k - 1; // set row index for next 
                     // point in diagonal  
        $j = 1; // set column index for next  
                // point in diagonal  
  
        /* Print Diagonally upward */
        while (isValid($i,$j))  
        {  
            echo $arr[$i][$j] . " ";  
            $i--;  
            $j++; // move in upright direction  
        }  
        echo "\n";  
    }  
  
    /* through this for loop we choose each  
    element of last row as starting point  
    (except the [0][c-1] it has already been  
    processed in previous for loop) and print 
    diagonal starting at it. arr[R-1][0], 
    arr[R-1][1]....arr[R-1][c-1] are all  
    starting points */
  
    //Note : we start from k = 1 to C-1;  
    for ($k = 1; $k < C; $k++)  
    {  
        echo $arr[R - 1][$k] . " ";  
        $i = R - 2; // set row index for next  
                    // point in diagonal  
        $j = $k + 1; // set column index for next 
                     // point in diagonal  
  
        /* Print Diagonally upward */
        while (isValid($i, $j))  
        {  
            echo $arr[$i][$j] . " ";  
            $i--;  
            $j++; // move in upright direction  
        }  
        echo "\n"; 
    }  
}  
  
// Driver Code 
$arr = array(array(1, 2, 3, 4),  
             array(5, 6, 7, 8),  
             array(9, 10, 11, 12),  
             array(13, 14, 15, 16),  
             array(17, 18, 19, 20));  
diagonalOrder($arr);  
  
// This code is contributed  
// by rathbhupendra 
?>
```

输出：

```
1
5 2
9 6 3
13 10 7 4
17 14 11 8
18 15 12
19 16
20
```

感谢 Gaurav Ahirwar 提出了这种方法。