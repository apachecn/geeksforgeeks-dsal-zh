# 矩阵概率问题

> 原文： [https://www.geeksforgeeks.org/a-matrix-probability-question/](https://www.geeksforgeeks.org/a-matrix-probability-question/)

给定一个矩形矩阵，我们可以以相同的概率从当前单元向 4 个方向移动。 4 个方向是右，左，上或下。 计算在 N 从矩阵中的给定位置（i，j）移动之后，我们在任何点都不会越过矩阵边界的概率。

**我们强烈建议您最小化浏览器，然后自己尝试。**

这个想法是执行类似于 DFS 的操作。 我们在 4 个允许的方向中的每个方向上进行递归遍历，对于遇到的每个像元，我们只需移动一小步即可计算出所需的概率。 由于每个方向具有相等的概率，因此每个方向将贡献该单元的总概率的 1/4，即 0.25。 如果我们走出矩阵，则返回 0；如果完成 N 个步但不跨越矩阵边界，则返回 1。

以下是上述想法的实现：

## C++

```cpp

/// C++ program to find the probability  
// that we do not cross boundary of a  
// matrix after N moves. 
#include <bits/stdc++.h> 
using namespace std; 

// check if (x, y) is valid matrix coordinate 
bool isSafe(int x, int y, int m, int n) 
{ 
    return (x >= 0 && x < m &&  
            y >= 0 && y < n); 
} 

// Function to calculate probability  
// that after N moves from a given  
// position (x, y) in m x n matrix,  
// boundaries of the matrix will not be crossed. 
double findProbability(int m, int n, int x,  
                       int y, int N) 
{ 
    // boundary crossed 
    if (!isSafe(x, y, m, n)) 
        return 0.0; 

    // N steps taken 
    if (N == 0) 
        return 1.0; 

    // Initialize result 
    double prob = 0.0; 

    // move up 
    prob += findProbability(m, n, x - 1,  
                            y, N - 1) * 0.25; 

    // move right 
    prob += findProbability(m, n, x,  
                            y + 1, N - 1) * 0.25; 

    // move down 
    prob += findProbability(m, n, x + 1, 
                            y, N - 1) * 0.25; 

    // move left 
    prob += findProbability(m, n, x,  
                            y - 1, N - 1) * 0.25; 

    return prob; 
} 

// Driver code 
int main() 
{ 
    // matrix size 
    int m = 5, n = 5; 

    // coordinates of starting point 
    int i = 1, j = 1; 

    // Number of steps 
    int N = 2; 

    cout << "Probability is "
        << findProbability(m, n, i, j, N); 

    return 0; 
} 

```