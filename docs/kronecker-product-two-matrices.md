# 两个矩阵的 Kronecker 积

> 原文： [https://www.geeksforgeeks.org/kronecker-product-two-matrices/](https://www.geeksforgeeks.org/kronecker-product-two-matrices/)

给定`m x n`矩阵`A`和`p x q`矩阵`B`，它们的 **Kronecker 积**`C = A tensor B`，也称为它们的矩阵直接积，是`mp x nq`矩阵。

```
A tensor B =  |a11B   a12B|
              |a21B   a22B|

= |a11b11   a11b12   a12b11  a12b12|
  |a11b21   a11b22   a12b21  a12b22| 
  |a11b31   a11b32   a12b31  a12b32|
  |a21b11   a21b12   a22b11  a22b12|
  |a21b21   a21b22   a22b21  a22b22|
  |a21b31   a21b32   a22b31  a22b32|

```

**示例**：

```
1\. The matrix direct(kronecker) product of the 2×2 matrix A 
   and the 2×2 matrix B is given by the 4×4 matrix :

Input : A = 1 2    B = 0 5
            3 4        6 7

Output : C = 0  5  0  10
             6  7  12 14
             0  15 0  20
             18 21 24 28

2\. The matrix direct(kronecker) product of the 2×3 matrix A 
   and the 3×2 matrix B is given by the 6×6 matrix :

Input : A = 1 2    B = 0 5 2
            3 4        6 7 3
            1 0

Output : C = 0      5    2    0     10    4    
             6      7    3   12     14    6    
             0     15    6    0     20    8    
            18     21    9   24     28   12    
             0      5    2    0      0    0    
             6      7    3    0      0    0    

```



下面是找到两个矩阵的 **Kronecker 乘积**并将其存储为矩阵 C 的代码：

## C++ 

```cpp

// C++ code to find the Kronecker Product of two 
// matrices and stores it as matrix C 
#include <iostream> 
using namespace std; 

// rowa and cola are no of rows and columns 
// of matrix A 
// rowb and colb are no of rows and columns 
// of matrix B 
const int cola = 2, rowa = 3, colb = 3, rowb = 2; 

// Function to computes the Kronecker Product 
// of two matrices 
void Kroneckerproduct(int A[][cola], int B[][colb]) 
{ 

    int C[rowa * rowb][cola * colb]; 

    // i loops till rowa 
    for (int i = 0; i < rowa; i++) { 

        // k loops till rowb 
        for (int k = 0; k < rowb; k++) { 

            // j loops till cola 
            for (int j = 0; j < cola; j++) { 

                // l loops till colb 
                for (int l = 0; l < colb; l++) { 

                    // Each element of matrix A is 
                    // multiplied by whole Matrix B 
                    // resp and stored as Matrix C 
                    C[i + l + 1][j + k + 1] = A[i][j] * B[k][l]; 
                    cout << C[i + l + 1][j + k + 1] << " "; 
                } 
            } 
            cout << endl; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int A[3][2] = { { 1, 2 }, { 3, 4 }, { 1, 0 } }, 
        B[2][3] = { { 0, 5, 2 }, { 6, 7, 3 } }; 

    Kroneckerproduct(A, B); 
    return 0; 
} 

//This code is contributed by shubhamsingh10 

```

## Java

```java
// Java code to find the Kronecker Product of 
// two matrices and stores it as matrix C 
import java.io.*; 
import java.util.*; 
  
class GFG { 
          
    // rowa and cola are no of rows and columns 
    // of matrix A 
    // rowb and colb are no of rows and columns 
    // of matrix B 
    static int cola = 2, rowa = 3, colb = 3, rowb = 2; 
      
    // Function to computes the Kronecker Product 
    // of two matrices 
    static void Kroneckerproduct(int A[][], int B[][]) 
    { 
      
        int[][] C= new int[rowa * rowb][cola * colb]; 
      
        // i loops till rowa 
        for (int i = 0; i < rowa; i++)  
        { 
      
            // k loops till rowb 
            for (int k = 0; k < rowb; k++) 
            { 
      
                // j loops till cola 
                for (int j = 0; j < cola; j++)  
                { 
      
                    // l loops till colb 
                    for (int l = 0; l < colb; l++) 
                    { 
      
                        // Each element of matrix A is 
                        // multiplied by whole Matrix B 
                        // resp and stored as Matrix C 
                        C[i + l + 1][j + k + 1] = A[i][j] * B[k][l]; 
                        System.out.print( C[i + l + 1][j + k + 1]+" "); 
                    } 
                } 
                System.out.println(); 
            } 
        } 
    } 
      
    // Driver program 
    public static void main (String[] args) 
    { 
        int A[][] = { { 1, 2 }, 
                      { 3, 4 },  
                      { 1, 0 } }; 
                        
        int B[][] = { { 0, 5, 2 }, 
                      { 6, 7, 3 } }; 
      
        Kroneckerproduct(A, B);  
    } 
} 
  
// This code is contributed by Gitanjali.
```

## Python3

```py
# Python3 code to find the Kronecker Product of two 
# matrices and stores it as matrix C 
   
# rowa and cola are no of rows and columns 
# of matrix A 
# rowb and colb are no of rows and columns 
# of matrix B 
cola = 2
rowa = 3
colb = 3
rowb = 2
   
# Function to computes the Kronecker Product 
# of two matrices 
  
def Kroneckerproduct( A , B ): 
      
    C = [[0 for j in range(cola * colb)] for i in range(rowa * rowb)] 
   
    # i loops till rowa 
    for i in range(0, rowa): 
          
        # k loops till rowb 
        for k in range(0, rowb): 
   
            # j loops till cola 
            for j in range(0, cola): 
   
                # l loops till colb 
                for l in range(0, colb): 
   
                    # Each element of matrix A is 
                    # multiplied by whole Matrix B 
                    # resp and stored as Matrix C 
                    C[i + l + 1][j + k + 1] = A[i][j] * B[k][l] 
                    print (C[i + l + 1][j + k + 1],end=' ') 
              
              
            print ("\n") 
          
  
# Driver code. 
  
A = [[0 for j in range(2)] for i in range(3)] 
B = [[0 for j in range(3)] for i in range(2)] 
  
A[0][0] = 1
A[0][1] = 2
A[1][0] = 3
A[1][1] = 4
A[2][0] = 1
A[2][1] = 0
  
B[0][0] = 0
B[0][1] = 5
B[0][2] = 2
B[1][0] = 6
B[1][1] = 7
B[1][2] = 3
  
Kroneckerproduct( A , B ) 
  
# This code is contributed by Saloni.
```

## C#

```cs
// C# code to find the Kronecker Product of 
// two matrices and stores it as matrix C 
using System; 
  
class GFG { 
          
    // rowa and cola are no of rows  
    // and columns of matrix A 
    // rowb and colb are no of rows 
    //  and columns of matrix B 
    static int cola = 2, rowa = 3; 
    static int colb = 3, rowb = 2; 
      
    // Function to computes the Kronecker  
    // Product of two matrices 
    static void Kroneckerproduct(int [,]A, int [,]B) 
    { 
      
        int [,]C= new int[rowa * rowb,  
                          cola * colb]; 
      
        // i loops till rowa 
        for (int i = 0; i < rowa; i++)  
        { 
      
            // k loops till rowb 
            for (int k = 0; k < rowb; k++) 
            { 
      
                // j loops till cola 
                for (int j = 0; j < cola; j++)  
                { 
      
                    // l loops till colb 
                    for (int l = 0; l < colb; l++) 
                    { 
      
                        // Each element of matrix A is 
                        // multiplied by whole Matrix B 
                        // resp and stored as Matrix C 
                        C[i + l + 1, j + k + 1] = A[i, j] *  
                                                  B[k, l]; 
                        Console.Write( C[i + l + 1,  
                                       j + k + 1] + " "); 
                    } 
                } 
                Console.WriteLine(); 
            } 
        } 
    } 
      
    // Driver Code 
    public static void Main () 
    { 
        int [,]A = {{1, 2}, 
                   {3, 4},  
                   {1, 0}}; 
                          
        int [,]B = {{0, 5, 2}, 
                   {6, 7, 3}}; 
      
        Kroneckerproduct(A, B);  
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// PHP code to find the 
// Kronecker Product of two 
  
// rowa and cola are no of  
// rows and columns of matrix A 
// rowb and colb are no of  
// rows and columns of matrix B 
$cola = 2; 
$rowa = 3; 
$colb = 3; 
$rowb = 2; 
  
// Function to computes the  
// Kronecker Product of two matrices 
function Kroneckerproduct($A, $B) 
{ 
    global $cola; 
    global $rowa; 
    global $colb; 
    global $rowb; 
  
  
    //$C[$rowa * $rowb][$cola * $colb]; 
    $C; 
  
    // i loops till rowa 
    for ( $i = 0; $i < $rowa; $i++) 
    { 
  
        // k loops till rowb 
        for ($k = 0; $k < $rowb; $k++)  
        { 
  
            // j loops till cola 
            for ( $j = 0; $j < $cola; $j++)   
            { 
  
                // l loops till colb 
                for ($l = 0; $l < $colb; $l++)  
                { 
  
                    // Each element of matrix A is 
                    // multiplied by whole Matrix B 
                    // resp and stored as Matrix C 
                    $C[$i + $l + 1][$j + $k + 1] = $A[$i][$j] *  
                                                   $B[$k][$l]; 
                    echo ($C[$i + $l + 1][$j + $k + 1]), "\t" ; 
                } 
            } 
        echo "\n"; 
        } 
    } 
} 
  
// Driver Code 
$A = array (array (1, 2),  
            array (3, 4),  
            array (1, 0)); 
$B = array (array (0, 5, 2), 
            array (6, 7, 3)); 
  
Kroneckerproduct($A, $B); 
  
// This code is contributed by ajit 
?>
```

输出：

```
0    5    2    0    10    4    
6    7    3    12   14    6    
0    15   6    0    20    8    
18   21   9    24   28    12    
0    5    2    0    0     0    
6    7    3    0    0     0
```

