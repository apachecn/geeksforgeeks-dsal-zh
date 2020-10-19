# 程序检查矩阵是否对称

> 原文： [https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-symmetric/](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-symmetric/)

如果矩阵的转置与给定矩阵相同，则称方矩阵为**对称矩阵**。 **对称矩阵**可以通过将行更改为列，将列更改为行来获得。

例子：

```
Input : 1 2 3
        2 1 4
        3 4 3
Output : Yes

Input : 3 5 8
        3 4 7
        8 5 3
Output : No

```



一个**简单解决方案**要执行以下操作。

1.  创建给定矩阵的转置。

2.  检查转置矩阵和给定矩阵是否相同，

## C++ 

```cpp

// Simple c++ code for check a matrix is 
// symmetric or not. 
#include <iostream> 
using namespace std; 

const int MAX = 100; 

// Fills transpose of mat[N][N] in tr[N][N] 
void transpose(int mat[][MAX], int tr[][MAX], int N) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            tr[i][j] = mat[j][i]; 
} 

// Returns true if mat[N][N] is symmetric, else false 
bool isSymmetric(int mat[][MAX], int N) 
{ 
    int tr[N][MAX]; 
    transpose(mat, tr, N); 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] != tr[i][j]) 
                return false; 
    return true; 
} 

// Driver code 
int main() 
{ 
    int mat[][MAX] = { { 1, 3, 5 }, 
                       { 3, 2, 4 }, 
                       { 5, 4, 1 } }; 

    if (isSymmetric(mat, 3)) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
} 

```

## Java

```
// Simple java code for check a matrix is 
// symmetric or not. 
  
import java.io.*; 
  
class GFG { 
      
  
  
 static int  MAX = 100; 
  
// Fills transpose of mat[N][N] in tr[N][N] 
 static void transpose(int mat[][], int tr[][], int N) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            tr[i][j] = mat[j][i]; 
} 
  
// Returns true if mat[N][N] is symmetric, else false 
 static boolean isSymmetric(int mat[][], int N) 
{ 
    int tr[][] = new int[N][MAX]; 
    transpose(mat, tr, N); 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] != tr[i][j]) 
                return false; 
    return true; 
} 
  
// Driver code 
    public static void main (String[] args) 
 { 
          
        int mat[][] = { { 1, 3, 5 }, 
                    { 3, 2, 4 }, 
                    { 5, 4, 1 } }; 
  
    if (isSymmetric(mat, 3)) 
        System.out.println( "Yes"); 
    else
        System.out.println ( "No"); 
      
    } 
}
```

## Python

```
# Simple Python code for check a matrix is 
# symmetric or not. 
   
# Fills transpose of mat[N][N] in tr[N][N] 
def transpose(mat, tr, N): 
    for i in range(N): 
        for j in range(N): 
            tr[i][j] = mat[j][i] 
   
# Returns true if mat[N][N] is symmetric, else false 
def isSymmetric(mat, N): 
      
    tr = [ [0 for j in range(len(mat[0])) ] for i in range(len(mat)) ] 
    transpose(mat, tr, N) 
    for i in range(N): 
        for j in range(N): 
            if (mat[i][j] != tr[i][j]): 
                return False
    return True
   
# Driver code 
mat = [ [ 1, 3, 5 ], [ 3, 2, 4 ], [ 5, 4, 1 ] ] 
if (isSymmetric(mat, 3)): 
    print "Yes"
else: 
    print "No"
  
# This code is contributed by Sachin Bisht
```

## C#

```
// Simple C# code for check a matrix is 
// symmetric or not. 
  
using System; 
  
class GFG { 
      
    static int MAX = 100; 
      
    // Fills transpose of mat[N][N] in tr[N][N] 
    static void transpose(int [,]mat, int [,]tr, int N) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 
                tr[i,j] = mat[j,i]; 
    } 
      
    // Returns true if mat[N][N] is symmetric, else false 
    static bool isSymmetric(int [,]mat, int N) 
    { 
        int [,]tr = new int[N,MAX]; 
        transpose(mat, tr, N); 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 
                if (mat[i,j] != tr[i,j]) 
                    return false; 
        return true; 
    } 
      
    // Driver code 
    public static void Main () 
    { 
              
        int [,]mat = { { 1, 3, 5 }, 
                        { 3, 2, 4 }, 
                        { 5, 4, 1 } }; 
      
        if (isSymmetric(mat, 3)) 
            Console.WriteLine( "Yes"); 
        else
            Console.WriteLine( "No"); 
          
      } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// Simple PHP code for check a matrix is 
// symmetric or not. 
  
// Returns true if mat[N][N] is  
// symmetric, else false 
function isSymmetric($mat, $N) 
{ 
    $tr = array(array()); 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 
            $tr[$i][$j] = $mat[$j][$i]; 
      
    // Fills transpose of  
    // mat[N][N] in tr[N][N]  
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 
            if ($mat[$i][$j] != $tr[$i][$j]) 
                return false; 
    return true; 
} 
  
    // Driver code 
    $mat= array(array(1, 3, 5), 
                array(3, 2, 4), 
                array(5, 4, 1)); 
                  
    if (isSymmetric($mat, 3)) 
        echo "Yes"; 
    else
        echo "No"; 
  
// This code is contributed by Sam007 
?>
```

输出：

```
 Yes
```

时间复杂度：`O(N x N)`。

辅助空间：`O(N x N)`。

检查矩阵是否对称的有效解决方案是比较矩阵元素而不创建转置。 我们基本上需要比较`mat[i][j]`和`mat[j][i]`。

## C++

```
// Efficient c++ code for check a matrix is 
// symmetric or not. 
#include <iostream> 
using namespace std; 
  
const int MAX = 100; 
  
// Returns true if mat[N][N] is symmetric, else false 
bool isSymmetric(int mat[][MAX], int N) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] != mat[j][i]) 
                return false; 
    return true; 
} 
  
// Driver code 
int main() 
{ 
    int mat[][MAX] = { { 1, 3, 5 }, 
                       { 3, 2, 4 }, 
                       { 5, 4, 1 } }; 
  
    if (isSymmetric(mat, 3)) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
}
```

## Java

```
// Efficient Java code for check a matrix is 
// symmetric or no 
  
import java.io.*; 
  
class GFG { 
     
  
static int MAX = 100; 
  
// Returns true if mat[N][N] 
// is symmetric, else false 
 static boolean isSymmetric(int mat[][], int N) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = 0; j < N; j++) 
            if (mat[i][j] != mat[j][i]) 
                return false; 
    return true; 
} 
  
// Driver code 
      
    public static void main (String[] args) 
 { 
            int mat[][] = { { 1, 3, 5 }, 
                    { 3, 2, 4 }, 
                    { 5, 4, 1 } }; 
  
    if (isSymmetric(mat, 3)) 
        System.out.println(  "Yes"); 
    else
          
        System.out.println("NO"); 
          
    } 
} 
// This article is contributed by vt_m.
```

## Python

```
# Efficient Python code for check a matrix is 
# symmetric or not. 
  
# Returns true if mat[N][N] is symmetric, else false 
def isSymmetric(mat, N): 
    for i in range(N): 
        for j in range(N): 
            if (mat[i][j] != mat[j][i]): 
                return False
    return True
   
# Driver code 
mat = [ [ 1, 3, 5 ], [ 3, 2, 4 ], [ 5, 4, 1 ] ] 
if (isSymmetric(mat, 3)): 
    print "Yes"
else: 
    print "No"
  
# This code is contributed by Sachin Bisht
```

## C#

```
// Efficient C# code for check a matrix is 
// symmetric or no 
  
using System; 
  
class GFG  
{ 
    //static int MAX = 100; 
      
    // Returns true if mat[N][N] 
    // is symmetric, else false 
    static bool isSymmetric(int [,]mat, int N) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = 0; j < N; j++) 
                if (mat[i, j] != mat[j, i]) 
                    return false; 
        return true; 
    } 
      
    // Driver code 
    public static void Main () 
    { 
        int [,]mat = { { 1, 3, 5 }, 
                    { 3, 2, 4 }, 
                    { 5, 4, 1 } }; 
  
        if (isSymmetric(mat, 3)) 
            Console.WriteLine( "Yes"); 
        else
              
            Console.WriteLine("NO"); 
          
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```
<?php 
// Efficient PHP code for  
// check a matrix is 
// symmetric or not. 
  
$MAX = 100; 
  
// Returns true if mat[N][N]  
// is symmetric, else false 
function isSymmetric($mat, $N) 
{ 
    for ($i = 0; $i < $N; $i++) 
        for ($j = 0; $j < $N; $j++) 
            if ($mat[$i][$j] != $mat[$j][$i]) 
                return false; 
    return true; 
} 
  
// Driver code 
$mat = array(array(1, 3, 5), 
             array(3, 2, 4), 
             array(5, 4, 1)); 
  
if (isSymmetric($mat, 3)) 
    echo("Yes"); 
else
    echo("No"); 
  
// This code is contributed by Ajit. 
?>
```

输出：

```
Yes
```

时间复杂度：`O(N x N)`。

辅助空间：`O(1)`。