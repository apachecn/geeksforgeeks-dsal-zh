# 单位矩阵程序

> 原文： [https://www.geeksforgeeks.org/program-print-identity-matrix/](https://www.geeksforgeeks.org/program-print-identity-matrix/)

**单位矩阵简介**：

**单位矩阵**的字典定义是一个方矩阵，其中主对角线或主对角线的所有元素均为 1，其他所有元素均为零。 在下图中，每个矩阵都是一个单位矩阵。

![](img/80ad1022655aa2228c13b6f959a4e68c.png)

在线性代数中，有时将其称为**单位矩阵**，它是一个方矩阵（大小`= n x n`），主对角线为 1，其他地方为零。 单位矩阵由`I`表示。 有时，`U`或`E`也用于表示单位矩阵。

**单位矩阵的一个特性是，如果将其乘以单位矩阵，则矩阵将保持不变。**

**示例**：

```
Input  : 2
Output : 1 0
         0 1

Input :  4
Output : 1 0 0 0
         0 1 0 0
         0 0 1 0
         0 0 0 1
The explanation is simple. We need to make all
the elements of principal or main diagonal as 
1 and everything else as 0.

```

**打印单位矩阵的程序**：

逻辑很简单。 您需要在行等于矩数组的那些位置打印 1，并将所有其他位置设为 0。

## C++ 

```cpp

// C++ program to print Identity Matrix 
#include<bits/stdc++.h> 
using namespace std; 

int Identity(int num) 
{ 
    int row, col; 

    for (row = 0; row < num; row++) 
    { 
        for (col = 0; col < num; col++) 
        { 
            // Checking if row is equal to column  
            if (row == col) 
                cout << 1 << " "; 
            else
                cout << 0 << " "; 
        }  
        cout << endl; 
    } 
    return 0; 
} 

// Driver Code 
int main() 
{ 
    int size = 5; 
    Identity(size); 
    return 0; 
} 

// This code is contributed by shubhamsingh10 

```

## C

```
// C program to print Identity Matrix 
#include<stdio.h> 
  
int Identity(int num) 
{ 
    int row, col; 
      
    for (row = 0; row < num; row++) 
    { 
        for (col = 0; col < num; col++) 
        { 
            // Checking if row is equal to column  
            if (row == col) 
                printf("%d ", 1); 
            else
                printf("%d ", 0); 
        }  
        printf("\n"); 
    } 
    return 0; 
} 
  
// Driver Code 
int main() 
{ 
    int size = 5; 
    identity(size); 
    return 0; 
}
```

## Java

```
// Java program to print Identity Matrix 
class GFG { 
      
    static int identity(int num) 
    { 
        int row, col; 
           
        for (row = 0; row < num; row++) 
        { 
            for (col = 0; col < num; col++) 
            { 
                // Checking if row is equal to column  
                if (row == col) 
                    System.out.print( 1+" "); 
                else
                    System.out.print( 0+" "); 
            }  
            System.out.println(); 
        } 
        return 0; 
    } 
       
    // Driver Code 
    public static void main(String args[]) 
    { 
        int size = 5; 
        identity(size); 
    } 
} 
  
/*This code is contributed by Nikita tiwari.*/
```

## Python3

```
# Python code to print identity matrix 
  
# Function to print identity matrix 
def Identity(size): 
    for row in range(0, size): 
        for col in range(0, size): 
  
            # Here end is used to stay in same line 
            if (row == col): 
                print("1 ", end=" ") 
            else: 
                print("0 ", end=" ") 
        print() 
  
# Driver Code         
size = 5
Identity(size)
```

## C#

```
// C# program to print Identity Matrix 
using System; 
  
class GFG { 
      
    static int identity(int num) 
    { 
        int row, col; 
          
        for (row = 0; row < num; row++) 
        { 
            for (col = 0; col < num; col++) 
            { 
                // Checking if row is equal to column  
                if (row == col) 
                    Console.Write( 1+" "); 
                else
                    Console.Write( 0+" "); 
            }  
            Console.WriteLine(); 
        } 
        return 0; 
    } 
      
    // Driver Code 
    public static void Main() 
    { 
        int size = 5; 
        identity(size); 
    } 
} 
  
/*This code is contributed by vt_m.*/
```

## PHP

```
<?php 
// PHP program to print  
// Identity Matrix 
  
function Identity($num) 
{ 
    $row; $col; 
      
    for ($row = 0; $row < $num; $row++) 
    { 
        for ($col = 0; $col < $num; $col++) 
        { 
              
            // Checking if row is  
            // equal to column  
            if ($row == $col) 
            echo 1," "; 
            else
            echo 0," "; 
        }  
        echo"\n"; 
    } 
    return 0; 
} 
  
    // Driver Code 
    $size = 5; 
    identity($size); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
1  0  0  0  0  
0  1  0  0  0  
0  0  1  0  0  
0  0  0  1  0  
0  0  0  0  1  
```

检查给定的方阵是否为单位矩阵的程序：

## C++

```
// CPP program to check if a given matrix is identity 
#include<iostream> 
using namespace std; 
  
const int MAX = 100; 
  
bool isIdentity(int mat[][MAX], int N) 
{  
    for (int row = 0; row < N; row++) 
    { 
        for (int col = 0; col < N; col++) 
        { 
            if (row == col && mat[row][col] != 1) 
                return false; 
            else if (row != col && mat[row][col] != 0) 
                return false; 
        }  
    } 
    return true; 
} 
  
// Driver Code 
int main() 
{ 
    int N = 4; 
    int mat[][MAX] = {{1, 0, 0, 0},  
                    {0, 1, 0, 0}, 
                    {0, 0, 1, 0}, 
                    {0, 0, 0, 1}};  
    if (isIdentity(mat, N)) 
       cout << "Yes "; 
    else
       cout << "No "; 
    return 0; 
}
```

## Java

```
// Java program to check if a given  
// matrix is identity 
class GFG { 
      
    int MAX = 100; 
   
    static boolean isIdentity(int mat[][], int N) 
    {  
        for (int row = 0; row < N; row++) 
        { 
            for (int col = 0; col < N; col++) 
            { 
                if (row == col && mat[row][col] != 1) 
                    return false; 
                else if (row != col && mat[row][col] != 0) 
                    return false; 
            }  
        } 
        return true; 
    } 
       
    // Driver Code 
    public static void main(String args[]) 
    { 
        int N = 4; 
        int mat[][] = {{1, 0, 0, 0}, 
                       {0, 1, 0, 0}, 
                       {0, 0, 1, 0}, 
                       {0, 0, 0, 1}};  
          
        if (isIdentity(mat, N)) 
           System.out.println("Yes "); 
        else
           System.out.println("No "); 
    } 
} 
  
  
/*This code is contributed by Nikita Tiwari.*/
```

## Python3

```
# Python3 program to check  
# if a given matrix is identity 
MAX = 100; 
def isIdentity(mat, N): 
    for row in range(N): 
        for col in range(N): 
            if (row == col and 
                mat[row][col] != 1): 
                return False; 
            elif (row != col and 
                  mat[row][col] != 0): 
                return False; 
    return True; 
  
# Driver Code 
N = 4; 
mat = [[1, 0, 0, 0], 
       [0, 1, 0, 0], 
       [0, 0, 1, 0], 
       [0, 0, 0, 1]];  
if (isIdentity(mat, N)): 
    print("Yes "); 
else: 
    print("No "); 
  
# This code is contributed 
# by mits
```

## C#

```
// C# program to check if a given  
// matrix is identity 
using System; 
  
class GFG { 
      
    //int MAX = 100; 
  
    static bool isIdentity(int[,] mat, int N) 
    {  
        for (int row = 0; row < N; row++) 
        { 
            for (int col = 0; col < N; col++) 
            { 
                if (row == col && mat[row,col] != 1) 
                    return false; 
                else if (row != col && mat[row,col] != 0) 
                    return false; 
            }  
        } 
        return true; 
    } 
      
    // Driver Code 
    public static void Main() 
    { 
        int N = 4; 
        int [,]mat = {{1, 0, 0, 0}, 
                      {0, 1, 0, 0}, 
                      {0, 0, 1, 0}, 
                      {0, 0, 0, 1}};  
          
        if (isIdentity(mat, N)) 
        Console.WriteLine("Yes "); 
        else
        Console.WriteLine("No "); 
    } 
} 
  
  
/*This code is contributed by vt_m.*/
```

## PHP

```
<?php 
// PHP program to check if a 
// given matrix is identity 
// $MAX = 100; 
  
function isIdentity($mat, $N) 
{  
    for ($row = 0; $row < $N; $row++) 
    { 
        for ( $col = 0; $col < $N; $col++) 
        { 
            if ($row == $col and 
                $mat[$row][$col] != 1) 
                return false; 
            else if ($row != $col &&  
                     $mat[$row][$col] != 0) 
                return false; 
        }  
    } 
    return true; 
} 
  
    // Driver Code 
    $N = 4; 
    $mat = array(array(1, 0, 0, 0),  
                 array(0, 1, 0, 0), 
                 array(0, 0, 1, 0), 
                 array(0, 0, 0, 1));  
    if (isIdentity($mat, $N)) 
    echo "Yes "; 
    else
    echo "No "; 
  
// This code is contributed by anuj_67. 
?>
```


输出：

```
Yes
```

