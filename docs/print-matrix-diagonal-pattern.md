# 以对角线图案打印矩阵

> 原文： [https://www.geeksforgeeks.org/print-matrix-diagonal-pattern/](https://www.geeksforgeeks.org/print-matrix-diagonal-pattern/)

给定`n * n`大小的矩阵，任务是以对角线图案打印其元素。

![](img/8c366008db60e6d58a5dde6eddec7b8a.png)

```
Input : mat[3][3] = {{1, 2, 3},
                     {4, 5, 6},
                     {7, 8, 9}}
Output : 1 2 4 7 5 3 6 8 9.
Explanation: Start from 1 
Then from upward to downward diagonally i.e. 2 and 4
Then from downward to upward diagonally i.e 7, 5, 3 
Then from up to down diagonally i.e  6, 8 
Then down to up i.e. end at 9.

Input :  mat[4][4] =  {{1,  2,  3,  10},
                      {4,  5,  6,  11},
                      {7,  8,  9,  12},
                      {13, 14, 15, 16}}
Output:  1 2 4 7 5 3 10 6 8 13 14 9 11 12 15 16 .
Explanation: Start from 1 
Then from upward to downward diagonally i.e. 2 and 4
Then from downward to upward diagonally i.e 7, 5, 3 
Then from upward to downward diagonally i.e. 10 6 8 13
Then from downward to upward diagonally i.e 14 9 11
Then from upward to downward diagonally i.e. 12 15
then end at 16

```



**方法**：从图中可以看出，每个元素要么斜向上打印，要么斜向下打印。 从索引`(0, 0)`开始，对角向上打印元素，然后更改方向，改变列，对角向下打印。 该循环一直持续到到达最后一个元素为止。

**算法**：

1.  创建变量`i = 0, j = 0`以存储行和列的当前索引。

2.  运行从 0 到`n * n`的循环，其中`n`是矩阵的边。

3.  使用标志`isUp`来确定方向是向上还是向下。 最初将`isUp = true`设置为向上方向。

4.  如果`isUp = 1`，则通过增加列索引和减少行索引来开始打印元素。

5.  同样，如果`isUp = 0`，则减少列索引并增加行索引。

6.  移至下一个列或行（下一个开始的行和列）。

7.  这样做直到遍历所有元素。

**实现**：

## C++ 

```cpp

// C++ program to print matrix in diagonal order 
#include <bits/stdc++.h> 
using namespace std; 
const int MAX = 100; 

void printMatrixDiagonal(int mat[MAX][MAX], int n) 
{ 
    // Initialize indexes of element to be printed next 
    int i = 0, j = 0; 

    // Direction is initially from down to up 
    bool isUp = true; 

    // Traverse the matrix till all elements get traversed 
    for (int k = 0; k < n * n;) { 
        // If isUp = true then traverse from downward 
        // to upward 
        if (isUp) { 
            for (; i >= 0 && j < n; j++, i--) { 
                cout << mat[i][j] << " "; 
                k++; 
            } 

            // Set i and j according to direction 
            if (i < 0 && j <= n - 1) 
                i = 0; 
            if (j == n) 
                i = i + 2, j--; 
        } 

        // If isUp = 0 then traverse up to down 
        else { 
            for (; j >= 0 && i < n; i++, j--) { 
                cout << mat[i][j] << " "; 
                k++; 
            } 

            // Set i and j according to direction 
            if (j < 0 && i <= n - 1) 
                j = 0; 
            if (i == n) 
                j = j + 2, i--; 
        } 

        // Revert the isUp to change the direction 
        isUp = !isUp; 
    } 
} 

int main() 
{ 
    int mat[MAX][MAX] = { { 1, 2, 3 }, 
                          { 4, 5, 6 }, 
                          { 7, 8, 9 } }; 

    int n = 3; 
    printMatrixDiagonal(mat, n); 
    return 0; 
} 

```

## Java

```java
// Java program to print matrix in diagonal order 
class GFG { 
    static final int MAX = 100; 
  
    static void printMatrixDiagonal(int mat[][], int n) 
    { 
        // Initialize indexes of element to be printed next 
        int i = 0, j = 0; 
  
        // Direction is initially from down to up 
        boolean isUp = true; 
  
        // Traverse the matrix till all elements get traversed 
        for (int k = 0; k < n * n;) { 
            // If isUp = true then traverse from downward 
            // to upward 
            if (isUp) { 
                for (; i >= 0 && j < n; j++, i--) { 
                    System.out.print(mat[i][j] + " "); 
                    k++; 
                } 
  
                // Set i and j according to direction 
                if (i < 0 && j <= n - 1) 
                    i = 0; 
                if (j == n) { 
                    i = i + 2; 
                    j--; 
                } 
            } 
  
            // If isUp = 0 then traverse up to down 
            else { 
                for (; j >= 0 && i < n; i++, j--) { 
                    System.out.print(mat[i][j] + " "); 
                    k++; 
                } 
  
                // Set i and j according to direction 
                if (j < 0 && i <= n - 1) 
                    j = 0; 
                if (i == n) { 
                    j = j + 2; 
                    i--; 
                } 
            } 
  
            // Revert the isUp to change the direction 
            isUp = !isUp; 
        } 
    } 
  
    // Driver code 
    public static void main(String[] args) 
    { 
        int mat[][] = { { 1, 2, 3 }, 
                        { 4, 5, 6 }, 
                        { 7, 8, 9 } }; 
  
        int n = 3; 
        printMatrixDiagonal(mat, n); 
    } 
} 
// This code is contributed by Anant Agarwal.
```

## Python 3

```
# Python 3 program to print matrix in diagonal order 
MAX = 100
  
def printMatrixDiagonal(mat, n): 
    # Initialize indexes of element to be printed next 
    i = 0
    j = 0
    k = 0
    # Direction is initially from down to up 
    isUp = True
  
     # Traverse the matrix till all elements get traversed 
    while k<n * n: 
         # If isUp = True then traverse from downward 
         # to upward 
        if isUp: 
            while i >= 0 and j<n : 
                print(str(mat[i][j]), end = " ") 
                k += 1
                j += 1
                i -= 1
  
              # Set i and j according to direction 
            if i < 0 and j <= n - 1: 
                i = 0
            if j == n: 
                i = i + 2
                j -= 1
  
         # If isUp = 0 then traverse up to down 
        else: 
            while j >= 0 and i<n : 
                print(mat[i][j], end = " ") 
                k += 1
                i += 1
                j -= 1
  
              # Set i and j according to direction 
            if j < 0 and i <= n - 1: 
                j = 0
            if i == n: 
                j = j + 2
                i -= 1
  
         # Revert the isUp to change the direction 
        isUp = not isUp 
  
# Driver program 
if __name__ == "__main__": 
    mat = [[1, 2, 3], 
        [4, 5, 6], 
        [7, 8, 9] ] 
  
   n = 3
   printMatrixDiagonal(mat, n) 
  
# This code is contributed by Chitra Nayal
```

## C#

```cs
// C# program to print matrix in diagonal order 
using System; 
class GFG { 
    static int MAX = 100; 
  
    static void printMatrixDiagonal(int[, ] mat, int n) 
    { 
        // Initialize indexes of element to be printed next 
        int i = 0, j = 0; 
  
        // Direction is initially from down to up 
        bool isUp = true; 
  
        // Traverse the matrix till all elements get traversed 
        for (int k = 0; k < n * n;) { 
            // If isUp = true then traverse from downward 
            // to upward 
            if (isUp) { 
                for (; i >= 0 && j < n; j++, i--) { 
                    Console.Write(mat[i, j] + " "); 
                    k++; 
                } 
  
                // Set i and j according to direction 
                if (i < 0 && j <= n - 1) 
                    i = 0; 
                if (j == n) { 
                    i = i + 2; 
                    j--; 
                } 
            } 
  
            // If isUp = 0 then traverse up to down 
            else { 
                for (; j >= 0 && i < n; i++, j--) { 
                    Console.Write(mat[i, j] + " "); 
                    k++; 
                } 
  
                // Set i and j according to direction 
                if (j < 0 && i <= n - 1) 
                    j = 0; 
                if (i == n) { 
                    j = j + 2; 
                    i--; 
                } 
            } 
  
            // Revert the isUp to change the direction 
            isUp = !isUp; 
        } 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int[, ] mat = { { 1, 2, 3 }, 
                        { 4, 5, 6 }, 
                        { 7, 8, 9 } }; 
  
        int n = 3; 
        printMatrixDiagonal(mat, n); 
    } 
} 
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// php program to print matrix 
// in diagonal order 
  
$MAX = 100; 
  
function printMatrixDiagonal($mat, $n) 
{ 
      
    // Initialize indexes of element 
    // to be printed next 
    $i = 0; 
    $j = 0 ; 
  
    // Direction is initially 
    // from down to up 
    $isUp = true; 
  
    // Traverse the matrix till 
    // all elements get traversed 
    for ($k = 0;$k < $n * $n 
    { 
        // If isUp = true then traverse  
        // from downward to upward 
        if ($isUp) 
        { 
            for ( ;$i >= 0 && $j < $n;$j++, $i--) 
            { 
                echo $mat[$i][$j]." "; 
                $k++; 
            } 
  
            // Set i and j according  
            // to direction 
            if ($i < 0 && $j <= $n - 1) 
                $i = 0; 
            if ($j == $n) 
            { 
                $i = $i + 2; 
                $j--; 
            } 
        } 
  
        // If isUp = 0 then  
        // traverse up to down 
        else
        { 
            for ( ; $j >= 0 &&  
                 $i<$n ; $i++, $j--) 
            { 
                echo $mat[$i][$j]." "; 
                $k++; 
            } 
  
            // Set i and j according 
            // to direction 
            if ($j < 0 && $i <= $n - 1) 
                $j = 0; 
            if ($i == $n) 
            { 
                $j = $j + 2; 
                $i--; 
            } 
        } 
  
        // Revert the isUp to 
        // change the direction 
        $isUp = !$isUp; 
    } 
} 
  
    // Driver code 
    $mat= array(array(1, 2, 3), 
          array(4, 5, 6), 
          array(7, 8, 9)); 
  
    $n = 3; 
    printMatrixDiagonal($mat, $n); 
  
// This code is contributed by mits  
?>
```

输出：

```
1 2 4 7 5 3 6 8 9
```

复杂度分析：

+   时间复杂度：`O(n * n)`。

    要遍历矩阵`O(n * n)`，需要时间复杂度。
+   空间复杂度：`O(1)`。

    由于不需要额外的空间。

替代实现：这是与上述相同方法的另一种简单且紧凑的实现。

## C++

```cpp
// C++ program to print matrix in diagonal order 
#include <bits/stdc++.h> 
using namespace std; 
  
int main() 
{ 
    // Initialize matrix 
    int mat[][4] = { { 1, 2, 3, 4 }, 
                     { 5, 6, 7, 8 }, 
                     { 9, 10, 11, 12 }, 
                     { 13, 14, 15, 16 } }; 
    // n - size 
    // mode - switch to derive up/down traversal 
    // it - iterator count - increases until it 
    // reaches n and then decreases 
    int n = 4, mode = 0, it = 0, lower = 0; 
  
    // 2n will be the number of iterations 
    for (int t = 0; t < (2 * n - 1); t++) { 
        int t1 = t; 
        if (t1 >= n) { 
            mode++; 
            t1 = n - 1; 
            it--; 
            lower++; 
        } 
        else { 
            lower = 0; 
            it++; 
        } 
        for (int i = t1; i >= lower; i--) { 
            if ((t1 + mode) % 2 == 0) { 
                cout << (mat[i][t1 + lower - i]) << endl; 
            } 
            else { 
                cout << (mat[t1 + lower - i][i]) << endl; 
            } 
        } 
    } 
    return 0; 
} 
  
// This code is contributed by princiraj1992
```

## Java

```java
// Java program to print matrix in diagonal order 
public class MatrixDiag { 
  
    public static void main(String[] args) 
    { 
        // Initialize matrix 
        int[][] mat = { { 1, 2, 3, 4 }, 
                        { 5, 6, 7, 8 }, 
                        { 9, 10, 11, 12 }, 
                        { 13, 14, 15, 16 } }; 
        // n - size 
        // mode - switch to derive up/down traversal 
        // it - iterator count - increases until it 
        // reaches n and then decreases 
        int n = 4, mode = 0, it = 0, lower = 0; 
  
        // 2n will be the number of iterations 
        for (int t = 0; t < (2 * n - 1); t++) { 
            int t1 = t; 
            if (t1 >= n) { 
                mode++; 
                t1 = n - 1; 
                it--; 
                lower++; 
            } 
            else { 
                lower = 0; 
                it++; 
            } 
            for (int i = t1; i >= lower; i--) { 
                if ((t1 + mode) % 2 == 0) { 
                    System.out.println(mat[i][t1 + lower - i]); 
                } 
                else { 
                    System.out.println(mat[t1 + lower - i][i]); 
                } 
            } 
        } 
    } 
}
```

## Python3

```py
# Python3 program to prmatrix in diagonal order 
  
# Driver code 
  
# Initialize matrix 
mat = [[ 1, 2, 3, 4 ], 
       [ 5, 6, 7, 8 ], 
       [ 9, 10, 11, 12 ], 
       [ 13, 14, 15, 16 ]]; 
         
# n - size 
# mode - switch to derive up/down traversal 
# it - iterator count - increases until it 
# reaches n and then decreases 
n = 4
mode = 0
it = 0
lower = 0
  
# 2n will be the number of iterations 
for t in range(2 * n - 1): 
    t1 = t 
    if (t1 >= n): 
        mode += 1
        t1 = n - 1
        it -= 1
        lower += 1
    else: 
        lower = 0
        it += 1
  
    for i in range(t1, lower - 1, -1): 
        if ((t1 + mode) % 2 == 0): 
            print((mat[i][t1 + lower - i])) 
        else: 
            print(mat[t1 + lower - i][i]) 
  
# This code is contributed by princiraj1992
```

## C#

```cs
// C# program to print matrix in diagonal order 
using System; 
  
public class MatrixDiag { 
    // Driver code 
    public static void Main(String[] args) 
    { 
        // Initialize matrix 
        int[, ] mat = { { 1, 2, 3, 4 }, 
                        { 5, 6, 7, 8 }, 
                        { 9, 10, 11, 12 }, 
                        { 13, 14, 15, 16 } }; 
        // n - size 
        // mode - switch to derive up/down traversal 
        // it - iterator count - increases until it 
        // reaches n and then decreases 
        int n = 4, mode = 0, it = 0, lower = 0; 
  
        // 2n will be the number of iterations 
        for (int t = 0; t < (2 * n - 1); t++) { 
            int t1 = t; 
            if (t1 >= n) { 
                mode++; 
                t1 = n - 1; 
                it--; 
                lower++; 
            } 
            else { 
                lower = 0; 
                it++; 
            } 
            for (int i = t1; i >= lower; i--) { 
                if ((t1 + mode) % 2 == 0) { 
                    Console.WriteLine(mat[i, t1 + lower - i]); 
                } 
                else { 
                    Console.WriteLine(mat[t1 + lower - i, i]); 
                } 
            } 
        } 
    } 
} 
  
// This code contributed by Rajput-Ji
```

输出：

```
1
2
5
9
6
3
4
7
10
13
14
11
8
12
15
16
```

