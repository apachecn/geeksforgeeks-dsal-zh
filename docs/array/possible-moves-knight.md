# 骑士的可能举动

> 原文： [https://www.geeksforgeeks.org/possible-moves-knight/](https://www.geeksforgeeks.org/possible-moves-knight/)

给定尺寸为`m * n`的棋盘。 查找骑士可以从给定位置在棋盘上移动的可能动作数。 如果`mat[i][j] = 1`，则该块将填充其他内容，否则为空。 假设该棋盘由所有相同颜色的棋子组成，即没有被攻击的方块。

 **示例**：

```
Input : mat[][] = {{1, 0, 1, 0},
                   {0, 1, 1, 1},
                   {1, 1, 0, 1},
                   {0, 1, 1, 1}}
        pos = (2, 2)
Output : 4
Knight can moved from (2, 2) to (0, 1), (0, 3), 
(1, 0) ans (3, 0).

```



我们可以观察到骑士在棋盘上移动了：

1.  水平移动 2 步，垂直移动

2.  垂直移动 2 步，水平移动 1 步

这个想法是存储所有可能的骑士动作，然后计算有效动作的数量。 在以下情况下，移动将无效：

1.  一个块已被另一块占用。

2.  移动超出了棋盘。

## C++ 

```cpp

// CPP program to find number of possible moves of knight 
#include <bits/stdc++.h> 
#define n 4 
#define m 4 
using namespace std; 

// To calculate possible moves 
int findPossibleMoves(int mat[n][m], int p, int q) 
{ 
    // All possible moves of a knight 
    int X[8] = { 2, 1, -1, -2, -2, -1, 1, 2 }; 
    int Y[8] = { 1, 2, 2, 1, -1, -2, -2, -1 }; 

    int count = 0; 

    // Check if each possible move is valid or not 
    for (int i = 0; i < 8; i++) { 

        // Position of knight after move 
        int x = p + X[i]; 
        int y = q + Y[i]; 

        // count valid moves 
        if (x >= 0 && y >= 0 && x < n && y < m 
            && mat[x][y] == 0) 
            count++; 
    } 

    // Return number of possible moves 
    return count; 
} 

// Driver program to check findPossibleMoves() 
int main() 
{ 
    int mat[n][m] = { { 1, 0, 1, 0 }, 
                      { 0, 1, 1, 1 }, 
                      { 1, 1, 0, 1 }, 
                      { 0, 1, 1, 1 } }; 

    int p = 2, q = 2; 

    cout << findPossibleMoves(mat, p, q); 

    return 0; 
} 

```

## Java

```java

// Java program to find number of possible moves of knight 
public class Main { 
public static final int n = 4; 
public static final int m = 4; 

    // To calculate possible moves 
    static int findPossibleMoves(int mat[][], int p, int q) 
    { 
        // All possible moves of a knight 
        int X[] = { 2, 1, -1, -2, -2, -1, 1, 2 }; 
        int Y[] = { 1, 2, 2, 1, -1, -2, -2, -1 }; 

        int count = 0; 

        // Check if each possible move is valid or not 
        for (int i = 0; i < 8; i++) { 

            // Position of knight after move 
            int x = p + X[i]; 
            int y = q + Y[i]; 

            // count valid moves 
            if (x >= 0 && y >= 0 && x < n && y < m 
                && mat[x][y] == 0) 
                count++; 
        } 

        // Return number of possible moves 
        return count; 
    } 

    // Driver program to check findPossibleMoves() 
    public static void main(String[] args) 
    { 
        int mat[][] = { { 1, 0, 1, 0 }, 
                        { 0, 1, 1, 1 }, 
                        { 1, 1, 0, 1 }, 
                        { 0, 1, 1, 1 } }; 

        int p = 2, q = 2; 

        System.out.println(findPossibleMoves(mat, p, q)); 
    } 
} 

```

## Python3

```py

# Python3 program to find number 
# of possible moves of knight 
n = 4; 
m = 4; 

# To calculate possible moves 
def findPossibleMoves(mat, p, q): 
    global n, m; 

    # All possible moves of a knight 
    X = [2, 1, -1, -2, -2, -1, 1, 2]; 
    Y = [1, 2, 2, 1, -1, -2, -2, -1]; 

    count = 0; 

    # Check if each possible move 
    # is valid or not 
    for i in range(8): 

        # Position of knight after move 
        x = p + X[i]; 
        y = q + Y[i]; 

        # count valid moves 
        if(x >= 0 and y >= 0 and x < n and
           y < m and mat[x][y] == 0): 
            count += 1; 

    # Return number of possible moves 
    return count; 

# Driver code 
if __name__ == '__main__': 
    mat = [[1, 0, 1, 0], [0, 1, 1, 1],  
           [1, 1, 0, 1], [0, 1, 1, 1]]; 

    p, q = 2, 2; 

    print(findPossibleMoves(mat, p, q)); 

# This code is contributed by 29AjayKumar 

```

## C# 

```cs

// C# program to find number of 
// possible moves of knight 
using System; 

class GFG 
{ 
    static int n = 4; 
    static int m = 4; 

    // To calculate  
    // possible moves 
    static int findPossibleMoves(int [,]mat,  
                                 int p, int q) 
    { 
        // All possible moves 
        // of a knight 
        int []X = { 2, 1, -1, -2, 
                   -2, -1, 1, 2 }; 
        int []Y = { 1, 2, 2, 1,  
                   -1, -2, -2, -1 }; 

        int count = 0; 

        // Check if each possible 
        // move is valid or not 
        for (int i = 0; i < 8; i++) 
        { 

            // Position of knight 
            // after move 
            int x = p + X[i]; 
            int y = q + Y[i]; 

            // count valid moves 
            if (x >= 0 && y >= 0 &&  
                x < n && y < m &&  
                mat[x, y] == 0) 
                count++; 
        } 

        // Return number  
        // of possible moves 
        return count; 
    } 

    // Driver Code 
    static public void Main () 
    { 
        int [,]mat = { { 1, 0, 1, 0 }, 
                       { 0, 1, 1, 1 }, 
                       { 1, 1, 0, 1 }, 
                       { 0, 1, 1, 1 }}; 

        int p = 2, q = 2; 

        Console.WriteLine(findPossibleMoves(mat,  
                                            p, q)); 
    } 
} 

// This code is contributed by m_kit 

```

## PHP

```php

<?php 
// PHP program to find number  
// of possible moves of knight 
$n = 4; 
$m = 4; 

// To calculate possible moves 
function findPossibleMoves($mat,  
                           $p, $q) 
{ 
    global $n; 
    global $m; 

    // All possible moves  
    // of a knight 
    $X = array(2, 1, -1, -2,  
              -2, -1, 1, 2); 
    $Y = array(1, 2, 2, 1, 
              -1, -2, -2, -1); 

    $count = 0; 

    // Check if each possible 
    // move is valid or not 
    for ($i = 0; $i < 8; $i++)  
    { 

        // Position of 
        // knight after move 
        $x = $p + $X[$i]; 
        $y = $q + $Y[$i]; 

        // count valid moves 
        if ($x >= 0 && $y >= 0 &&  
            $x < $n && $y < $m &&  
            $mat[$x][$y] == 0) 
            $count++; 
    } 

    // Return number  
    // of possible moves 
    return $count; 
} 

// Driver Code 
$mat = array(array(1, 0, 1, 0), 
             array(0, 1, 1, 1), 
             array(1, 1, 0, 1), 
             array(0, 1, 1, 1)); 

$p = 2; $q = 2; 

echo findPossibleMoves($mat,  
                       $p, $q); 

// This code is contributed by ajit 
?> 

```

**输出**：

```
4

```

**参考**：

[https://en.wikipedia.org/wiki/Knight_(chess)](https://en.wikipedia.org/wiki/Knight_(chess))


