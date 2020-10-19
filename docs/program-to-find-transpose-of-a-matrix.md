# 查找矩阵转置的程序

> 原文： [https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/](https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/)

通过将行更改为列并将列更改为行来获得矩阵的转置。 换句话说，通过将`A[i][j]`更改为`A[j][i]`可获得`A[][]`的转置。

![matrix-transpose](img/e368eb2a9ca0cd036dc0c86015b59151.png)



**对于方阵**：

下面的程序找到`A[][]`的转置，并将结果存储在`B[][]`中，我们可以将`N`更改为不同的维数。

## C++ 

```cpp

#include <stdio.h> 
#define N 4 

// This function stores transpose of A[][] in B[][] 
void transpose(int A[][N], int B[][N]) 
{ 
    int i, j; 
    for (i = 0; i < N; i++) 
        for (j = 0; j < N; j++) 
            B[i][j] = A[j][i]; 
} 

int main() 
{ 
    int A[N][N] = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}, 
                    {4, 4, 4, 4}}; 

    int B[N][N], i, j; 

    transpose(A, B); 

    printf("Result matrix is \n"); 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < N; j++) 
           printf("%d ", B[i][j]); 
        printf("\n"); 
    } 

    return 0; 
} 

```

## Java

```
// Java Program to find  
// transpose of a matrix 
  
class GFG 
{ 
    static final int N = 4; 
      
    // This function stores transpose 
    // of A[][] in B[][] 
    static void transpose(int A[][], int B[][]) 
    { 
        int i, j; 
        for (i = 0; i < N; i++) 
            for (j = 0; j < N; j++) 
                B[i][j] = A[j][i]; 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int A[][] = { {1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}, 
                      {4, 4, 4, 4}}; 
      
        int B[][] = new int[N][N], i, j; 
      
        transpose(A, B); 
      
        System.out.print("Result matrix is \n"); 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < N; j++) 
            System.out.print(B[i][j] + " "); 
            System.out.print("\n"); 
        } 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```
# Python3 Program to find 
# transpose of a matrix 
  
N = 4
   
# This function stores 
# transpose of A[][] in B[][] 
  
def transpose(A,B): 
  
    for i in range(N): 
        for j in range(N): 
            B[i][j] = A[j][i] 
  
# driver code 
A = [ [1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3], 
    [4, 4, 4, 4]] 
   
   
B = [[0,0,0,0],[0,0,0,0],[0,0,0,0],[0,0,0,0]] # To store result  
  
transpose(A, B) 
   
print("Result matrix is") 
for i in range(N): 
    for j in range(N): 
        print(B[i][j], " ", end='') 
    print() 
      
# This code is contributed 
# by Anant Agarwal.
```

## C#

```
// C# Program to find  
// transpose of a matrix 
using System; 
  
class GFG 
{ 
    static int N = 4; 
      
    // This function stores transpose 
    // of A[][] in B[][] 
    static void transpose(int [,]A, int [,]B) 
    { 
        int i, j; 
        for (i = 0; i < N; i++) 
            for (j = 0; j < N; j++) 
                B[i,j] = A[j,i]; 
    } 
      
    // Driver code 
    public static void Main () 
    { 
        int [,]A = { {1, 1, 1, 1}, 
                     {2, 2, 2, 2}, 
                     {3, 3, 3, 3}, 
                     {4, 4, 4, 4}}; 
      
        int [,]B = new int[N,N]; 
          
        // Function calling 
        transpose(A, B); 
      
        Console.Write("Result matrix is \n"); 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < N; j++) 
            Console.Write(B[i,j] + " "); 
            Console.Write("\n"); 
        } 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```
<?php 
  
// This function stores transpose  
// of A[][] in B[][] 
function transpose(&$A, &$B) 
{ 
    $N = 4; 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 
            $B[$i][$j] = $A[$j][$i]; 
} 
  
// Driver code 
$A = array(array(1, 1, 1, 1), 
           array(2, 2, 2, 2), 
           array(3, 3, 3, 3), 
           array(4, 4, 4, 4)); 
  
$N = 4; 
  
transpose($A, $B); 
  
echo "Result matrix is \n"; 
for ($i = 0; $i < $N; $i++) 
{ 
    for ($j = 0; $j < $N; $j++) 
    { 
        echo $B[$i][$j]; 
        echo " "; 
    } 
    echo "\n"; 
} 
  
// This code is contributed 
// by Shivi_Aggarwal  
?>
```

输出：

```
Result matrix is
1 2 3 4
1 2 3 4
1 2 3 4
1 2 3 4
```

对于矩形矩阵：

下面的程序查找`A[][]`的转置，并将结果存储在`B[][]`中。

## C++

```
#include <stdio.h> 
#define M 3 
#define N 4 
  
// This function stores transpose of A[][] in B[][] 
void transpose(int A[][N], int B[][M]) 
{ 
    int i, j; 
    for (i = 0; i < N; i++) 
        for (j = 0; j < M; j++) 
            B[i][j] = A[j][i]; 
} 
  
int main() 
{ 
    int A[M][N] = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}}; 
  
    // Note dimensions of B[][] 
    int B[N][M], i, j; 
  
    transpose(A, B); 
  
    printf("Result matrix is \n"); 
    for (i = 0; i < N; i++) 
    { 
        for (j = 0; j < M; j++) 
        printf("%d ", B[i][j]); 
        printf("\n"); 
    } 
  
    return 0; 
}
```

## Java

```
// Java Program to find  
// transpose of a matrix 
  
class GFG 
{ 
    static final int M = 3; 
    static final int N = 4; 
      
    // This function stores transpose 
    // of A[][] in B[][] 
    static void transpose(int A[][], int B[][]) 
    { 
        int i, j; 
        for (i = 0; i < N; i++) 
            for (j = 0; j < M; j++) 
                B[i][j] = A[j][i]; 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int A[][] = { {1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}}; 
      
        int B[][] = new int[N][M], i, j; 
      
        transpose(A, B); 
      
        System.out.print("Result matrix is \n"); 
        for (i = 0; i < N; i++) 
        { 
            for (j = 0; j < M; j++) 
            System.out.print(B[i][j] + " "); 
            System.out.print("\n"); 
        } 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```
# Python3 Program to find 
# transpose of a matrix 
  
M = 3
N = 4
  
# This function stores 
# transpose of A[][] in B[][] 
  
def transpose(A, B): 
  
    for i in range(N): 
        for j in range(M): 
            B[i][j] = A[j][i] 
  
# driver code 
A = [ [1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3]] 
  
  
# To store result 
B = [[0 for x in range(M)] for y in range(N)]  
  
transpose(A, B) 
  
print("Result matrix is") 
for i in range(N): 
    for j in range(M): 
        print(B[i][j], " ", end='') 
    print()
```

## C#

```
// C# Program to find  
// transpose of a matrix 
 using System; 
class GFG { 
  
    static  int M = 3; 
    static  int N = 4; 
       
    // This function stores transpose 
    // of A[][] in B[][] 
    static void transpose(int [,]A, int [,]B) 
    { 
        int i, j; 
        for (i = 0; i < N; i++) 
            for (j = 0; j < M; j++) 
                B[i,j] = A[j,i]; 
    } 
       
    // Driver code 
    public static void Main () 
    { 
        int [,]A = { {1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}}; 
       
        int [,]B= new int[N,M]; 
       
        transpose(A, B); 
       
        Console.WriteLine("Result matrix is \n"); 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < M; j++) 
            Console.Write(B[i,j] + " "); 
            Console.Write("\n"); 
        } 
    } 
} 
   
// This code is contributed by nitin mittal
```

## PHP

```
<?php 
  
// This function stores transpose 
// of A[][] in B[][] 
function transpose(&$A, &$B) 
{ 
    $N = 4; 
    $M = 3; 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $M; $j++) 
            $B[$i][$j] = $A[$j][$i]; 
} 
  
// Driver code 
  
$A = array(array(1, 1, 1, 1), 
           array(2, 2, 2, 2), 
           array(3, 3, 3, 3)); 
  
$N = 4; 
$M = 3; 
transpose($A, $B); 
  
echo "Result matrix is \n"; 
for ($i = 0; $i < $N; $i++) 
{ 
    for ($j = 0; $j < $M; $j++) 
    { 
    echo $B[$i][$j]; 
    echo " "; 
    } 
    echo "\n"; 
} 
  
// This code is contributed 
// by Shivi_Aggarwal  
?>
```

输出：

```
Result matrix is
1 2 3 
1 2 3 
1 2 3 
1 2 3
```

方阵的原地算法：

## C++

```
#include <bits/stdc++.h> 
using namespace std; 
  
#define N 4 
  
// Converts A[][] to its transpose 
void transpose(int A[][N]) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = i+1; j < N; j++) 
            swap(A[i][j], A[j][i]); 
} 
  
int main() 
{ 
    int A[N][N] = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}, 
                    {4, 4, 4, 4}}; 
  
    transpose(A); 
  
    printf("Modified matrix is \n"); 
    for (int i = 0; i < N; i++) 
    { 
        for (int j = 0; j < N; j++) 
           printf("%d ", A[i][j]); 
        printf("\n"); 
    } 
  
    return 0; 
}
```

## Java

```
// Java Program to find  
// transpose of a matrix 
  
class GFG 
{ 
    static final int N = 4; 
      
    // Finds transpose of A[][] in-place 
    static void transpose(int A[][]) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = i+1; j < N; j++) 
            { 
                 int temp = A[i][j]; 
                 A[i][j] = A[j][i]; 
                 A[j][i] = temp; 
            } 
    } 
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int A[][] = { {1, 1, 1, 1}, 
                      {2, 2, 2, 2}, 
                      {3, 3, 3, 3}, 
                      {4, 4, 4, 4}}; 
         
        transpose(A); 
      
        System.out.print("Modified matrix is \n"); 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < N; j++) 
            System.out.print(A[i][j] + " "); 
            System.out.print("\n"); 
        } 
    } 
}
```

## Python3

```
# Python3 Program to find 
# transpose of a matrix 
  
N = 4
   
# Finds transpose of A[][] in-place 
def transpose(A): 
  
    for i in range(N): 
        for j in range(i+1, N): 
            A[i][j], A[j][i] = A[j][i], A[i][j] 
  
# driver code 
A = [ [1, 1, 1, 1], 
    [2, 2, 2, 2], 
    [3, 3, 3, 3], 
    [4, 4, 4, 4]] 
   
 transpose(A) 
   
print("Modified matrix is") 
for i in range(N): 
    for j in range(N): 
        print(A[i][j], " ", end='') 
    print() 
      
# This code is contributed 
# by Anant Agarwal.
```

## C#

```
// C# Program to find transpose of 
// a matrix 
using System; 
  
class GFG { 
      
    static int N = 4; 
      
    // Finds transpose of A[][] in-place 
    static void transpose(int [,]A) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = i+1; j < N; j++) 
            { 
                int temp = A[i,j]; 
                A[i,j] = A[j,i]; 
                A[j,i] = temp; 
            } 
    } 
      
    // Driver code 
    public static void Main () 
    { 
        int [,]A = { {1, 1, 1, 1}, 
                    {2, 2, 2, 2}, 
                    {3, 3, 3, 3}, 
                    {4, 4, 4, 4}}; 
          
        transpose(A); 
      
        Console.WriteLine("Modified matrix is "); 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < N; j++) 
                Console.Write(A[i,j] + " "); 
                  
            Console.WriteLine(); 
        } 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```
<?php 
// Converts A[][] to its transpose 
function transpose(&$A) 
{ 
    $N = 4; 
    for ($i = 0; $i < $N; $i++) 
        for ($j = $i + 1; $j < $N; $j++) 
            { 
                $temp = $A[$i][$j]; 
                $A[$i][$j] = $A[$j][$i]; 
                $A[$j][$i] = $temp; 
            } 
} 
  
// Driver Code 
$N = 4; 
$A = array(array(1, 1, 1, 1), 
            array(2, 2, 2, 2), 
           array(3, 3, 3, 3), 
           array(4, 4, 4, 4)); 
  
transpose($A); 
  
echo "Modified matrix is " . "\n"; 
for ($i = 0; $i < $N; $i++) 
{ 
    for ($j = 0; $j < $N; $j++) 
        echo $A[$i][$j] . " "; 
    echo "\n"; 
} 
  
// This code is contributed 
// by Akanksha Rai(Abby_akku) 
?>
```

输出：

```
Modified matrix is
1 2 3 4
1 2 3 4
1 2 3 4
1 2 3 4
```

