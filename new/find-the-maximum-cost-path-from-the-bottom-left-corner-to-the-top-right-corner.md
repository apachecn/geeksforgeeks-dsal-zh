# 查找从左下角到右上角的最大成本路径

> 原文： [https://www.geeksforgeeks.org/find-the-maximum-cost-path-from-the-bottom-left-corner-to-the-top-right-corner/](https://www.geeksforgeeks.org/find-the-maximum-cost-path-from-the-bottom-left-corner-to-the-top-right-corner/)

给定一个二维网格，其每个像元包含整数成本，它代表穿越该像元的成本。 任务是找到从左下角到右上角的最大成本路径。

**注意**：仅使用向上和向右移动

**示例**：

```
Input : mat[][] = {{20, -10, 0}, 
                   {1, 5, 10}, 
                   {1, 2, 3}}
Output : 18
(2, 0) ==> (2, 1) ==> (1, 1) ==> (1, 2) ==> (0, 2)  
cost for this path is (1+2+5+10+0) = 18

Input : mat[][] = {{1, -2, -3}, 
                   {1, 15, 10},
                   {1, -2, 3}}
Output : 24

```

**先决条件**：[允许左，右，下和上移动的最小成本路径](https://www.geeksforgeeks.org/minimum-cost-path-left-right-bottom-moves-allowed/)

**方法**：的想法是使用[队列](http://www.geeksforgeeks.org/queue-data-structure/)维护一个单独的阵列，以存储所有单元的最大成本。 对于每个单元格，检查到达该单元格的当前成本是否大于先前的成本。 如果先前的成本最小，则使用当前成本更新单元格。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find maximum cost to reach  
// top right corner from bottom left corner 
#include <bits/stdc++.h> 
using namespace std;  

#define ROW 3 
#define COL 3  

// To store matrix cell coordinates  
struct Point  
{  
    int x;  
    int y;  
};  

// Check whether given cell (row, col)  
// is a valid cell or not.  
bool isValid(Point p)  
{  
    // Return true if row number and column number  
    // is in range  
    return (p.x >=0) && (p.y <COL);  
}  

// Function to find maximum cost to reach  
// top right corner from bottom left corner 
int find_max_cost(int mat[][COL])  
{  
    int max_val[ROW][COL];  
    memset(max_val, 0, sizeof max_val); 
        max_val[ROW-1][0] = mat[ROW-1][0];  

    // Starting point     
    Point src = {ROW-1,0}; 

    // Create a queue for traversal  
    queue<Point> q;  

    q.push(src); // Enqueue source cell  

    // Do a BFS starting from source cell  
    // on the allowed direction 
    while (!q.empty())  
    {  
        Point curr = q.front(); 
        q.pop();  

        // Find up point 
        Point up = {curr.x-1, curr.y}; 

        // if adjacent cell is valid, enqueue it.  
        if (isValid(up))  
        {  
            max_val[up.x][up.y] = max(max_val[up.x][up.y],  
                 mat[up.x][up.y] + max_val[curr.x][curr.y]); 
            q.push(up); 
        } 

        // Find right point     
        Point right = {curr.x, curr.y+1}; 

        if(isValid(right))  
        {  
            max_val[right.x][right.y] = max(max_val[right.x][right.y], 
                mat[right.x][right.y] + max_val[curr.x][curr.y]); 
            q.push(right); 
        } 

    }  

    // Return the required answer 
    return max_val[0][COL-1];  
}  

// Driver code 
int main()  
{  
    int mat[ROW][COL] = { {20, -10, 0}, 
                          {1, 5, 10}, 
                          {1, 2, 3},};  

    std::cout<<"Given matrix is "<<endl; 

    for(int i = 0 ; i<ROW;++i) 
    { 
        for(int j =0; j<COL; ++j) 
            std::cout<<mat[i][j]<<" "; 

        std::cout<<endl; 
    } 

    std::cout<<"Maximum cost is " << find_max_cost(mat);  

    return 0;  
}  

```