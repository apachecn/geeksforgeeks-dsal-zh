# 在二进制矩阵中查找以 1s 构成的形状的周长

> 原文： [https://www.geeksforgeeks.org/find-perimeter-shapes-formed-1s-binary-matrix/](https://www.geeksforgeeks.org/find-perimeter-shapes-formed-1s-binary-matrix/)

给定一个`N`行和`M`列的矩阵，由 0 和 1 组成。 任务是找到矩阵中仅包含 1 的子图形的周长。 单 1 的周长是 4，因为它可以从所有 4 侧覆盖。 双 11 的周长是 6。

```

|  1  |           |  1    1  |

```

例子：

```
Input : mat[][] = 
               {
                 1, 0,
                 1, 1,
               }
Output : 8
Cell (1,0) and (1,1) making a L shape whose perimeter is 8.

Input :  mat[][] = 
                {   
                    0, 1, 0, 0, 0,
                    1, 1, 1, 0, 0,
                    1, 0, 0, 0, 0
                }
Output : 12

```



想法是遍历矩阵，找到所有矩阵，并找到它们在周长中的作用。 如果 1 被全 0 包围，则其最大贡献为 4。 贡献减少 1 左右。

解决此问题的算法：

1.  遍历整个矩阵并找到值等于 1 的单元格。

2.  计算该单元格的封闭面数量，然后将 4 – 封闭面数量添加到总周长中。

下面是此方法的实现：

## C++ 

```cpp

// C++ program to find perimeter of area coverede by 
// 1 in 2D matrix consisits of 0's and  1's. 
#include<bits/stdc++.h> 
using namespace std; 
#define R 3 
#define C 5 

// Find the number of covered side for mat[i][j]. 
int numofneighbour(int mat[][C], int i, int j) 
{ 
    int count = 0; 

    // UP 
    if (i > 0 && mat[i - 1][j]) 
        count++; 

    // LEFT 
    if (j > 0 && mat[i][j - 1]) 
        count++; 

    // DOWN 
    if (i < R-1 && mat[i + 1][j]) 
        count++; 

    // RIGHT 
    if (j < C-1 && mat[i][j + 1]) 
        count++; 

    return count; 
} 

// Returns sum of perimeter of shapes formed with 1s 
int findperimeter(int mat[R][C]) 
{ 
    int perimeter = 0; 

    // Traversing the matrix and finding ones to 
    // calculate their contribution. 
    for (int i = 0; i < R; i++) 
        for (int j = 0; j < C; j++) 
            if (mat[i][j]) 
                perimeter += (4 - numofneighbour(mat, i ,j)); 

    return perimeter; 
} 

// Driven Program 
int main() 
{ 
    int mat[R][C] = 
    { 
        0, 1, 0, 0, 0, 
        1, 1, 1, 0, 0, 
        1, 0, 0, 0, 0, 
    }; 

    cout << findperimeter(mat) << endl; 

    return 0; 
} 

```

## Java

```java

// Java program to find perimeter of area 
// coverede by 1 in 2D matrix consisits  
// of 0's and 1's 
class GFG { 

    static final int R = 3; 
    static final int C = 5; 

    // Find the number of covered side  
    // for mat[i][j]. 
    static int numofneighbour(int mat[][],  
                            int i, int j)  
    { 

        int count = 0; 

        // UP 
        if (i > 0 && mat[i - 1][j] == 1) 
            count++; 

        // LEFT 
        if (j > 0 && mat[i][j - 1] == 1) 
            count++; 

        // DOWN 
        if (i < R - 1 && mat[i + 1][j] == 1) 
            count++; 

        // RIGHT 
        if (j < C - 1 && mat[i][j + 1] == 1) 
            count++; 

        return count; 
    } 

    // Returns sum of perimeter of shapes 
    // formed with 1s 
    static int findperimeter(int mat[][])  
    { 

        int perimeter = 0; 

        // Traversing the matrix and  
        // finding ones to calculate  
        // their contribution. 
        for (int i = 0; i < R; i++) 
            for (int j = 0; j < C; j++) 
                if (mat[i][j] == 1) 
                    perimeter += (4 -  
                    numofneighbour(mat, i, j)); 

        return perimeter; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        int mat[][] = {{0, 1, 0, 0, 0},  
                       {1, 1, 1, 0, 0},  
                       {1, 0, 0, 0, 0}}; 

        System.out.println(findperimeter(mat)); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python 3

```py

# Python 3 program to find perimeter of area  
# covered by 1 in 2D matrix consisits of 0's and 1's. 

R = 3
C = 5

# Find the number of covered side for mat[i][j]. 
def numofneighbour(mat, i, j): 

    count = 0; 

    # UP 
    if (i > 0 and mat[i - 1][j]): 
        count+= 1; 

    # LEFT 
    if (j > 0 and mat[i][j - 1]): 
        count+= 1; 

    # DOWN 
    if (i < R-1 and mat[i + 1][j]): 
        count+= 1

    # RIGHT 
    if (j < C-1 and mat[i][j + 1]): 
        count+= 1; 

    return count; 

# Returns sum of perimeter of shapes formed with 1s 
def findperimeter(mat): 

    perimeter = 0; 

    # Traversing the matrix and finding ones to 
    # calculate their contribution. 
    for i in range(0, R): 
        for j in range(0, C): 
            if (mat[i][j]): 
                perimeter += (4 - numofneighbour(mat, i, j)); 

    return perimeter; 

# Driver Code 
mat = [ [0, 1, 0, 0, 0], 
        [1, 1, 1, 0, 0], 
        [1, 0, 0, 0, 0] ] 

print(findperimeter(mat), end="\n"); 

# This code is contributed by Akanksha Rai 

```

## C# 

```cs

using System; 

// C# program to find perimeter of area  
// coverede by 1 in 2D matrix consisits   
// of 0's and 1's  
public class GFG 
{ 

    public  const int R = 3; 
    public const int C = 5; 

    // Find the number of covered side   
    // for mat[i][j].  
    public static int numofneighbour(int[][] mat, int i, int j) 
    { 

        int count = 0; 

        // UP  
        if (i > 0 && mat[i - 1][j] == 1) 
        { 
            count++; 
        } 

        // LEFT  
        if (j > 0 && mat[i][j - 1] == 1) 
        { 
            count++; 
        } 

        // DOWN  
        if (i < R - 1 && mat[i + 1][j] == 1) 
        { 
            count++; 
        } 

        // RIGHT  
        if (j < C - 1 && mat[i][j + 1] == 1) 
        { 
            count++; 
        } 

        return count; 
    } 

    // Returns sum of perimeter of shapes  
    // formed with 1s  
    public static int findperimeter(int[][] mat) 
    { 

        int perimeter = 0; 

        // Traversing the matrix and   
        // finding ones to calculate   
        // their contribution.  
        for (int i = 0; i < R; i++) 
        { 
            for (int j = 0; j < C; j++) 
            { 
                if (mat[i][j] == 1) 
                { 
                    perimeter += (4 - numofneighbour(mat, i, j)); 
                } 
            } 
        } 

        return perimeter; 
    } 

    // Driver code  
    public static void Main(string[] args) 
    { 
        int[][] mat = new int[][] 
        { 
            new int[] {0, 1, 0, 0, 0}, 
            new int[] {1, 1, 1, 0, 0}, 
            new int[] {1, 0, 0, 0, 0} 
        }; 

        Console.WriteLine(findperimeter(mat)); 
    } 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php 
// PHP program to find perimeter of area  
// covered by 1 in 2D matrix consisits 
// of 0's and 1's.  
$R = 3;  
$C = 5;  

// Find the number of covered side 
// for mat[i][j].  
function numofneighbour($mat, $i, $j)  
{  
    global $R;  
    global $C; 
    $count = 0;  

    // UP  
    if ($i > 0 && ($mat[$i - 1][$j]))  
        $count++;  

    // LEFT  
    if ($j > 0 && ($mat[$i][$j - 1]))  
        $count++;  

    // DOWN  
    if (($i < $R-1 )&& ($mat[$i + 1][$j]))  
        $count++;  

    // RIGHT  
    if (($j < $C-1) && ($mat[$i][$j + 1]))  
        $count++;  

    return $count;  
}  

// Returns sum of perimeter of shapes 
// formed with 1s  
function findperimeter($mat)  
{  
    global $R;  
    global $C; 
    $perimeter = 0;  

    // Traversing the matrix and finding ones  
    // to calculate their contribution.  
    for ($i = 0; $i < $R; $i++)  
        for ( $j = 0; $j < $C; $j++)  
            if ($mat[$i][$j])  
                $perimeter += (4 -  
                numofneighbour($mat, $i, $j));  

    return $perimeter;  
}  

// Driver Code 
$mat = array(array(0, 1, 0, 0, 0),  
             array(1, 1, 1, 0, 0),  
             array(1, 0, 0, 0, 0));  

echo findperimeter($mat), "\n";  

// This code is contributed by Sach_Code 
?> 

```

**输出**：

```
12

```

**时间复杂度**：`O(RC)`。



