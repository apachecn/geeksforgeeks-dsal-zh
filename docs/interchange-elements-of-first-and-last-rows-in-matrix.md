# 矩阵中第一行和最后一行的交换元素

> 原文： [https://www.geeksforgeeks.org/interchange-elements-of-first-and-last-rows-in-matrix/](https://www.geeksforgeeks.org/interchange-elements-of-first-and-last-rows-in-matrix/)

给定`4 x 4`矩阵，我们必须交换第一行和最后一行的元素，并显示结果矩阵。

**示例**：

```
Input : 3 4 5 0
        2 6 1 2
        2 7 1 2
        2 1 1 2
Output : 2 1 1 2
         2 6 1 2
         2 7 1 2
         3 4 5 0

Input : 9 7 5 1
        2 3 4 1
        5 6 6 5
        1 2 3 1
Output : 1 2 3 1
         2 3 4 1
         5 6 6 5
         9 7 5 1

```



该方法非常简单，我们可以简单地交换矩阵第一行和最后一行的元素，以获取所需的矩阵作为输出。

下面是该方法的实现：

## C++ 

```cpp

// C++ code to swap the element of first 
// and last row and display the result 
#include <iostream> 
using namespace std; 

#define n 4 

void interchangeFirstLast(int m[][n]) 
{ 
        int rows = n; 

        // swapping of element between first 
        // and last rows 
        for (int i = 0; i < n; i++) 
        { 
            int t = m[0][i]; 
            m[0][i] = m[rows - 1][i]; 
            m[rows - 1][i] = t; 
        } 
}  

// Driver function 
int main() 
{ 
    // input in the array 
    int m[n][n] = { { 8, 9, 7, 6 }, 
                { 4, 7, 6, 5 }, 
                { 3, 2, 1, 8 }, 
                { 9, 9, 7, 7 } };  

    interchangeFirstLast(m);  

    // printing the interchanged matrix 
    for (int i = 0; i < n; i++) 
    { 
        for (int j = 0; j < n; j++)  
            cout << m[i][j] << " "; 
        cout << endl; 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Java

```
// Java code to swap the element of first 
// and last row and display the result 
import java.io.*; 
  
public class Interchange { 
      
    static void interchangeFirstLast(int m[][]) 
    { 
        int rows = m.length; 
          
        // swapping of element between first 
        // and last rows 
        for (int i = 0; i < m[0].length; i++) { 
            int t = m[0][i]; 
            m[0][i] = m[rows-1][i]; 
            m[rows-1][i] = t; 
        } 
    } 
      
    // Driver code 
    public static void main(String args[]) throws IOException 
    { 
        // input in the array 
        int m[][] = { { 8, 9, 7, 6 }, 
                    { 4, 7, 6, 5 }, 
                    { 3, 2, 1, 8 }, 
                    { 9, 9, 7, 7 } };  
                      
        interchangeFirstLast(m);  
          
        // printing the interchanged matrix 
        for (int i = 0; i < m.length; i++) { 
            for (int j = 0; j < m[0].length; j++)  
                System.out.print(m[i][j] + " "); 
            System.out.println(); 
        } 
    } 
}
```

## Python3

```
# Python code to swap the element 
# of first and last row and display 
# the result 
  
def interchangeFirstLast(mat, n, m): 
    rows = n 
      
    # swapping of element between 
    # first and last rows 
    for i in range(n): 
        t = mat[0][i] 
        mat[0][i] = mat[rows-1][i] 
        mat[rows-1][i] = t 
  
# Driver Program 
mat = [[8, 9, 7, 6], 
          [4, 7, 6, 5], 
       [3, 2, 1, 8], 
       [9, 9, 7, 7]] 
  
n = 4
m = 4
interchangeFirstLast(mat, n, m) 
  
# printing the interchanged matrix 
for i in range(n): 
    for j in range(m): 
        print(mat[i][j], end = " ") 
    print("\n") 
  
# This code is contributed by Shrikant13.
```

## C#

```
// C# code to swap the element of first  
// and last row and display the result  
using System; 
  
class GFG 
{ 
  
public static void interchangeFirstLast(int[][] m) 
{ 
    int rows = m.Length; 
  
    // swapping of element between first  
    // and last rows  
    for (int i = 0; i < m[0].Length; i++) 
    { 
        int t = m[0][i]; 
        m[0][i] = m[rows - 1][i]; 
        m[rows - 1][i] = t; 
    } 
} 
  
// Driver code  
public static void Main(string[] args) 
{ 
    // input in the array  
    int[][] m = new int[][] 
    { 
        new int[] {8, 9, 7, 6}, 
        new int[] {4, 7, 6, 5}, 
        new int[] {3, 2, 1, 8}, 
        new int[] {9, 9, 7, 7} 
    }; 
  
    interchangeFirstLast(m); 
  
    // printing the interchanged matrix  
    for (int i = 0; i < m.Length; i++) 
    { 
        for (int j = 0; j < m[0].Length; j++) 
        { 
            Console.Write(m[i][j] + " "); 
        } 
        Console.WriteLine(); 
    } 
} 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```
<?php  
// PHP code to swap the element of first 
// and last row and display the result 
$n = 4; 
  
function interchangeFirstLast(&$m) 
{ 
        global $n; 
        $rows = $n; 
           
        // swapping of element between first 
        // and last rows 
        for ($i = 0; $i < $n; $i++) 
        { 
            $t = $m[0][$i]; 
            $m[0][$i] = $m[$rows - 1][$i]; 
            $m[$rows - 1][$i] = $t; 
        } 
}  
   
// Driver function 
  
// input in the array 
$m = array(array(8, 9, 7, 6), 
            array(4, 7, 6, 5), 
            array( 3, 2, 1, 8), 
            array(9, 9, 7, 7));  
               
interchangeFirstLast($m);  
   
// printing the interchanged matrix 
for ($i = 0; $i < $n; $i++) 
{ 
    for ($j = 0; $j < $n; $j++)  
        echo $m[$i][$j] . " "; 
    echo "\n"; 
} 
?>
```

输出：

```
9 9 7 7 
4 7 6 5 
3 2 1 8 
8 9 7 6 
```

