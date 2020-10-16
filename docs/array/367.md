# 以逆时针螺旋形式打印给定矩阵

> 原文： [https://www.geeksforgeeks.org/print-given-matrix-counter-clock-wise-spiral-form/](https://www.geeksforgeeks.org/print-given-matrix-counter-clock-wise-spiral-form/)

给定 2D 数组，以逆时针螺旋形式打印。 请参阅以下示例。

**示例**：

```
Input:
        1    2   3   4
        5    6   7   8
        9   10  11  12
        13  14  15  16
Output: 
1 5 9 13 14 15 16 12 8 4 3 2 6 10 11 7 

Input:
        1   2   3   4  5   6
        7   8   9  10  11  12
        13  14  15 16  17  18
Output: 
1 7 13 14 15 16 17 18 12 6 5 4 3 2 8 9 10 11 

```

**说明**：

![](img/69aa8becefb2e263dcd2d4cf441ac19f.png)

下面是实现：

## C++ 

```cpp

// C++ implementation to print 
// the counter clock wise 
// spiral traversal of matrix 
#include <bits/stdc++.h> 
using namespace std; 

#define R 4 
#define C 4 

// function to print the 
// required traversal 
void counterClockspiralPrint(int m,  
                             int n,  
                             int arr[R][C]) 
{ 
    int i, k = 0, l = 0; 

    //  k - starting row index 
    //    m - ending row index 
    //    l - starting column index 
    //    n - ending column index 
    //    i - iterator  

    // initialize the count 
    int cnt = 0; 

    // total number of  
    // elements in matrix 
    int total = m * n; 

    while (k < m && l < n)  
    { 
        if (cnt == total) 
            break; 

        // Print the first column  
        // from the remaining columns 
        for (i = k; i < m; ++i) 
        { 
            cout << arr[i][l] << " "; 
            cnt++; 
        } 
        l++; 

        if (cnt == total) 
            break; 

        // Print the last row from 
        // the remaining rows  
        for (i = l; i < n; ++i)  
        { 
            cout << arr[m - 1][i] << " "; 
            cnt++; 
        } 
        m--; 

        if (cnt == total) 
            break; 

        // Print the last column  
        // from the remaining columns  
        if (k < m)  
        { 
            for (i = m - 1; i >= k; --i)  
            { 
                cout << arr[i][n - 1] << " "; 
                cnt++; 
            } 
            n--; 
        } 

        if (cnt == total) 
            break; 

        // Print the first row  
        // from the remaining rows  
        if (l < n)  
        { 
            for (i = n - 1; i >= l; --i)  
            { 
                cout << arr[k][i] << " "; 
                cnt++; 
            } 
            k++; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    int arr[R][C] = {{ 1, 2, 3, 4 }, 
                     { 5, 6, 7, 8 }, 
                     { 9, 10, 11, 12 }, 
                     { 13, 14, 15, 16 }}; 
    counterClockspiralPrint(R, C, arr); 
    return 0; 
} 

```