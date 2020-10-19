# 使用`O(1)`额外空间打印`n x n`螺旋矩阵

> 原文： [https://www.geeksforgeeks.org/print-n-x-n-spiral-matrix-using-o1-extra-space/](https://www.geeksforgeeks.org/print-n-x-n-spiral-matrix-using-o1-extra-space/)

给定数字`n`，请使用`O(1)`空间沿顺时针方向打印`n x n`螺旋矩阵（从 1 到`n x n`的数字）。

**示例**：

```
Input: n = 5
Output:
25 24 23 22 21
10  9  8  7 20
11  2  1  6 19
12  3  4  5 18
13 14 15 16 17
```

**我们强烈建议您最小化浏览器，然后自己尝试。**

如果允许额外的空间，则解决方案变得简单。 我们为`n x n`矩阵分配内存，并为从`n * n`到 1 的每个元素分配以螺旋顺序填充矩阵。 为了维持螺旋顺序，使用了四个循环，每个循环用于矩阵的顶部，右侧，底部和左侧。

**但是如何在`O(1)`空间中解决呢？**

一个`n x n`矩阵具有`ceil(n / 2)`个平方周期。 循环由第`i`行，第`n - i + 1`列，第`n - i + 1`行和第`i`列构成，其中`i`从 1 到`ceil(n / 2)`变化。

```
25 24 23 22 21 
10 9  8  7  20
11 2  1  6  19
12 3  4  5 18
13 14 15 16 17

```

1.  第一个循环由其第一行，最后一列，最后一行和第一列（用红色标记）组成。 第一个循环包含从`n * n`到`(n-2) * (n-2) + 1`的元素，即从 25 到 10。

2.  第二周期由第二行，倒数第二列，倒数第二行和第二列（由蓝色标记）组成。 第二个周期由`(n-2) * (n-2)`至`(n-4) * (n-4) + 1`组成，即 9 至 2。

3.  第三循环由第三行，倒数第三列，倒数第三行和第三列（由**黑色**标记）组成。 第三个周期包含从`(n-4) * (n-4)`到 1 的元素，即仅 1。

这个想法是针对每个平方周期，我们将一个标记与其关联。 对于外部循环，标记的值为 0，对于第二循环，标记的值为 1，对于第三循环，标记的值为 2。通常，对于`n x n`矩阵，第`i`个循环的标记值为`i – 1`。

如果将矩阵分为两部分，右上三角形（由橙色标记）和左下三角形（由绿色标记），则使用标记`x`，我们可以轻松地计算出 使用以下公式将在任何`nxn`螺旋矩阵中的索引`(i, j)`上出现的值：

```
25  24 23 22 21 
10 9  8  7  20 
11  2  1 6  19 
12  3  4 5  18 
13  14 15 16 17 

```

```
For upper right half,
mat[i][j] = (n-2*x)*(n-2*x)-(i-x)-(j-x)

For lower left half,
mat[i][j] = (n-2*x-2)*(n-2*x-2) + (i-x) + (j-x)

```

以下是该想法的实现。

## C++ 

```cpp

// C++ program to print a n x n spiral matrix 
// in clockwise direction using O(1) space 
#include <bits/stdc++.h> 
using namespace std; 

// Prints spiral matrix of size n x n containing 
// numbers from 1 to n x n 
void printSpiral(int n) 
{ 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < n; j++) 
        { 
            // x stores the layer in which (i, j)th 
            // element lies 
            int x; 

            // Finds minimum of four inputs 
            x = min(min(i, j), min(n-1-i, n-1-j)); 

            // For upper right half 
            if (i <= j) 
                printf("%d\t ", (n-2*x)*(n-2*x) - (i-x) 
                    - (j-x)); 

            // for lower left half 
            else
                printf("%d\t ", (n-2*x-2)*(n-2*x-2) + (i-x) 
                    + (j-x)); 
        } 
        printf("\n"); 
    } 
} 

// Driver code 
int main() 
{ 
    int n = 5; 

    // print a n x n spiral matrix in O(1) space 
    printSpiral(n); 

    return 0; 
} 

```

## Java

```
// Java program to print a n x n spiral matrix 
// in clockwise direction using O(1) space 
  
import java.io.*; 
import java.util.*; 
  
class GFG { 
  
    // Prints spiral matrix of size n x n  
    // containing numbers from 1 to n x n 
    static void printSpiral(int n) 
    { 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < n; j++) { 
                  
                // x stores the layer in which (i, j)th 
                // element lies 
                int x; 
  
                // Finds minimum of four inputs 
                x = Math.min(Math.min(i, j),  
                    Math.min(n - 1 - i, n - 1 - j)); 
  
                // For upper right half 
                if (i <= j) 
                    System.out.print((n - 2 * x) * (n - 2 * x) -  
                                     (i - x) - (j - x) + "\t"); 
  
                // for lower left half 
                else
                    System.out.print((n - 2 * x - 2) * (n - 2 * x - 2) + 
                                     (i - x) + (j - x) + "\t"); 
            } 
            System.out.println(); 
        } 
    } 
  
    // Driver code 
    public static void main(String args[]) 
    { 
        int n = 5; 
  
        // print a n x n spiral matrix in O(1) space 
        printSpiral(n); 
    } 
} 
  
/*This code is contributed by Nikita Tiwari.*/
```

## Python3

```
# Python3 program to print a n x n spiral matrix 
# in clockwise direction using O(1) space 
  
# Prints spiral matrix of size n x n  
# containing numbers from 1 to n x n 
def printSpiral(n) : 
      
    for i in range(0, n) : 
        for j in range(0, n) : 
              
            # Finds minimum of four inputs 
            x = min(min(i, j), min(n - 1 - i, n - 1 - j)) 
              
            # For upper right half 
            if (i <= j) : 
                print((n - 2 * x) * (n - 2 * x) -
                      (i - x)- (j - x), end = "\t") 
  
            # For lower left half 
            else : 
                print(((n - 2 * x - 2) *
                       (n - 2 * x - 2) +
                       (i - x) + (j - x)), end = "\t") 
        print() 
          
# Driver code 
n = 5
  
# print a n x n spiral matrix 
# in O(1) space 
printSpiral(n) 
  
# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to print a n x n  
// spiral matrix in clockwise 
// direction using O(1) space 
using System; 
  
class GFG { 
  
    // Prints spiral matrix of  
    // size n x n containing 
    // numbers from 1 to n x n 
    static void printSpiral(int n) 
    { 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = 0; j < n; j++) 
            { 
                  
                // x stores the layer in which  
                // (i, j)th element lies 
                int x; 
  
                // Finds minimum of four inputs 
                x = Math.Min(Math.Min(i, j),  
                    Math.Min(n - 1 - i, n - 1 - j)); 
  
                // For upper right half 
                if (i <= j) 
                    Console.Write((n - 2 * x) *  
                                  (n - 2 * x) -  
                                  (i - x) - (j - x) + "\t"); 
  
                // for lower left half 
                else
                    Console.Write((n - 2 * x - 2) *  
                                  (n - 2 * x - 2) +  
                                  (i - x) + (j - x) + "\t"); 
            } 
            Console.WriteLine(); 
        } 
    } 
  
    // Driver code 
    public static void Main() 
    { 
        int n = 5; 
  
        // print a n x n spiral  
        // matrix in O(1) space 
        printSpiral(n); 
    } 
} 
  
// This code is contributed by KRV
```

## PHP

```
<?php 
// PHP program to print a n x n  
// spiral matrix in clockwise  
// direction using O(1) space 
  
// Prints spiral matrix of size  
// n x n containing numbers  
// from 1 to n x n 
function printSpiral($n) 
{ 
    for ($i = 0; $i < $n; $i++) 
    { 
        for ($j = 0; $j < $n; $j++) 
        { 
            // x stores the layer in  
            // which (i, j)th element lies 
            $x; 
  
            // Finds minimum of four inputs 
            $x = min(min($i, $j), min($n - 1 - $i,  
                                      $n - 1 - $j)); 
  
            // For upper right half 
            if ($i <= $j) 
                echo "\t ", ($n - 2 * $x) *  
                            ($n - 2 * $x) -  
                            ($i - $x) - ($j - $x); 
  
            // for lower left half 
            else
                echo "\t ", ($n - 2 * $x - 2) *  
                            ($n - 2 * $x - 2) +  
                            ($i - $x) + ($j - $x); 
        } 
        echo "\n"; 
    } 
} 
  
// Driver code 
$n = 5; 
  
// print a n x n spiral 
// matrix in O(1) space 
printSpiral($n); 
  
// This code is contributed by ajit 
?>
```

输出：

```
25     24     23     22     21     
10     9     8     7     20     
11     2     1     6     19     
12     3     4     5     18     
13     14     15     16     17
```

练习：

对于给定的数字`n`，使用`O(1)`空间沿逆时针方向打印`n x n`螺旋矩阵。