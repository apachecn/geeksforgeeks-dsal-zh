# 程序用矩阵的下对角元素交换上对角元素。

> 原文： [https://www.geeksforgeeks.org/program-swap-upper-diagonal-elements-lower-diagonal-elements-matrix/](https://www.geeksforgeeks.org/program-swap-upper-diagonal-elements-lower-diagonal-elements-matrix/)

给定一个正方形矩阵，将矩阵的上对角线元素与矩阵的下对角线元素交换。

**示例**：

```
Input:   2  3  5  6
         4  5  7  9
         8  6  4  9
         1  3  5  6

Output:  2  4  8  1
         3  5  6  3
         5  7  4  5
         6  9  9  6

Input:   1  2  3 
         4  5  6
         7  8  9

Output:  1  4  7
         2  5  8
         3  6  9

```



以下是上述想法的实现：

## C++ 

```cpp

// CPP Program to implement matrix 
// for swapping the upper diagonal 
// elements with lower diagonal  
// elements of matrix. 
#include <bits/stdc++.h> 
#define n 4 
using namespace std; 

// Function to swap the diagonal  
// elements in a matrix. 
void swapUpperToLower(int arr[n][n]) 
{ 
    // Loop for swap the elements of matrix. 
    for (int i = 0; i < n; i++) { 
        for (int j = i + 1; j < n; j++) { 
            int temp = arr[i][j]; 
            arr[i][j] = arr[j][i]; 
            arr[j][i] = temp; 
        } 
    } 

    // Loop for print the matrix elements. 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < n; j++) 
            cout << arr[i][j] << " "; 
        cout << endl; 
    } 
} 

// Driver function to run the program 
int main() 
{ 
    int arr[n][n] = { { 2, 3, 5, 6 }, 
                    { 4, 5, 7, 9 }, 
                    { 8, 6, 4, 9 }, 
                    { 1, 3, 5, 6 } }; 

    // Function call 
    swapUpperToLower(arr); 
    return 0; 
} 

} 

```

## Java

```
// java Program to implement matrix 
// for swapping the upper diagonal 
// elements with lower diagonal  
// elements of matrix. 
import java.io.*; 
  
class GFG 
{ 
    static int n = 4; 
      
    // Function to swap the diagonal  
    // elements in a matrix. 
    static void swapUpperToLower(int arr[][]) 
    { 
        // Loop for swap the elements of matrix. 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = i + 1; j < n; j++)  
            { 
                int temp = arr[i][j]; 
                arr[i][j] = arr[j][i]; 
                arr[j][i] = temp; 
            } 
        } 
          
        // Loop for print the matrix elements. 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = 0; j < n; j++) 
                System.out.print( arr[i][j] +" "); 
                System.out.println(); 
        } 
          
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int arr[][] = { { 2, 3, 5, 6 }, 
                        { 4, 5, 7, 9 }, 
                        { 8, 6, 4, 9 }, 
                        { 1, 3, 5, 6 } }; 
  
        // Function call 
        swapUpperToLower(arr); 
              
    } 
} 
  
// This code is contributed by vt_m.
```

## Python 3

```
# Python Program to implement matrix 
# for swapping the upper diagonal 
# elements with lower diagonal  
# elements of matrix. 
  
# Function to swap the diagonal  
# elements in a matrix. 
def swapUpperToLower(arr): 
    n = 4; 
      
    # Loop for swap the elements 
    # of matrix. 
    for i in range(0, n):  
        for j in range(i + 1, n):  
            temp = arr[i][j]; 
            arr[i][j] = arr[j][i]; 
            arr[j][i] = temp; 
          
    # Loop for print the matrix elements. 
    for i in range(0, n):  
        for j in range(0, n):  
            print(arr[i][j], end = " "); 
        print(" "); 
      
# Driver Code 
  
arr = [[2, 3, 5, 6 ],[ 4, 5, 7, 9 ], 
       [8, 6, 4, 9 ],[ 1, 3, 5, 6 ]]; 
  
# Function call 
swapUpperToLower(arr); 
  
# This code is contributed  
# by Shivi_Aggarwal
```

## C#

```
// C# Program to implement matrix 
// for swapping the upper diagonal 
// elements with lower diagonal  
// elements of matrix. 
using System; 
  
class GFG 
{ 
    static int n = 4; 
      
    // Function to swap the diagonal  
    // elements in a matrix. 
    static void swapUpperToLower(int [,]arr) 
    { 
        // Loop for swap the elements of matrix. 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = i + 1; j < n; j++)  
            { 
                int temp = arr[i, j]; 
                arr[i, j] = arr[j, i]; 
                arr[j, i] = temp; 
            } 
        } 
          
        // Loop for print the matrix elements. 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = 0; j < n; j++) 
                Console.Write(arr[i, j] +" "); 
                Console.WriteLine(); 
        } 
          
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int [,]arr = {{ 2, 3, 5, 6 }, 
                      { 4, 5, 7, 9 }, 
                      { 8, 6, 4, 9 }, 
                      { 1, 3, 5, 6 }}; 
  
        // Function call 
        swapUpperToLower(arr); 
              
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// PHP Program to implement matrix 
// for swapping the upper diagonal 
// elements with lower diagonal  
// elements of matrix. 
  
$n = 4; 
// Function to swap the diagonal  
// elements in a matrix. 
function swapUpperToLower($arr) 
{ 
    global $n; 
      
    // Loop for swap the elements of matrix. 
    for ($i = 0; $i < $n; $i++)  
    { 
        for ($j = $i + 1; $j < $n; $j++)  
        { 
            $temp = $arr[$i][$j]; 
            $arr[$i][$j] = $arr[$j][$i]; 
            $arr[$j][$i] = $temp; 
        } 
    } 
      
    // Loop for print the matrix elements. 
    for ($i = 0; $i < $n; $i++)  
    { 
        for ($j = 0; $j < $n; $j++) 
            echo($arr[$i][$j] . " "); 
        echo("\n"); 
    } 
} 
  
// Driver Code 
$arr = array(array(2, 3, 5, 6), 
             array(4, 5, 7, 9), 
             array(8, 6, 4, 9), 
             array(1, 3, 5, 6)); 
  
// Function call 
swapUpperToLower($arr); 
  
// This code is contributed by Ajit. 
?>
```

输出：

```
2 4 8 1 
3 5 6 3 
5 7 4 5 
6 9 9 6 
```

