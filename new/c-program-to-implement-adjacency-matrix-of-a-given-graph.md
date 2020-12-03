# C 程序，用于实现给定图

的邻接矩阵

> 原文： [https://www.geeksforgeeks.org/c-program-to-implement-adjacency-matrix-of-a-given-graph/](https://www.geeksforgeeks.org/c-program-to-implement-adjacency-matrix-of-a-given-graph/)

给定`N`顶点 1 至`N`和`M`顶点的无向[图](https://www.geeksforgeeks.org/graph-and-its-representations/)，其二维数组为[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **] arr [] []** ，每行由两个数字`X`和`Y`组成，这表示 X 和 Y 之间存在边沿，任务是编写 C 程序 创建给定图的[邻接矩阵。](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/)

**示例**：

> **输入**：N = 5，M = 4，arr [] [] = {{1，2}，{2，3}，{4，5}，{1，5}}
> **输出**：
> 0 1 0 0 1
> 1 0 1 0 0
> 0 1 0 0 0
> 0 0 0 0 1
> 1 0 0 1 0
> 
> **输入**：N = 3，M = 4，arr [] [] = {{1，2}，{2，3}，{3，1}，{2，2}}
> **输出**：
> 0 1 1
> 1 1 1
> 1 1 0

**方法**：这个想法是使用大小为 **NxN** 的方阵来创建邻接矩阵。 步骤如下：

1.  创建大小为 NxN 的 2D 数组（例如 **Adj [N + 1] [N + 1]** ），并将该矩阵的所有值初始化为零。

2.  对于 arr [] []（例如 **X 和 Y** ）中的每个边，更新 **Adj [X] [Y]** 和 **Adj [Y] [X]的值 HTG5]设为 1，表示 X 和 Y 之间有一条边。**

3.  对所有 **arr [] []** 中的对进行上述操作后，显示邻接矩阵。

下面是上述方法的实现：

```

// C program for the above approach 
#include <stdio.h> 

// N vertices and M Edges 
int N, M; 

// Function to create Adjacency Matrix 
void createAdjMatrix(int Adj[][N + 1], 
                     int arr[][2]) 
{ 

    // Initialise all value to this 
    // Adjacency list to zero 
    for (int i = 0; i < N + 1; i++) { 

        for (int j = 0; j < N + 1; j++) { 
            Adj[i][j] = 0; 
        } 
    } 

    // Traverse the array of Edges 
    for (int i = 0; i < M; i++) { 

        // Find X and Y of Edges 
        int x = arr[i][0]; 
        int y = arr[i][1]; 

        // Update value to 1 
        Adj[x][y] = 1; 
        Adj[y][x] = 1; 
    } 
} 

// Function to print the created 
// Adjacency Matrix 
void printAdjMatrix(int Adj[][N + 1]) 
{ 

    // Traverse the Adj[][] 
    for (int i = 1; i < N + 1; i++) { 
        for (int j = 1; j < N + 1; j++) { 

            // Print the value at Adj[i][j] 
            printf("%d ", Adj[i][j]); 
        } 
        printf("\n"); 
    } 
} 

// Driver Code 
int main() 
{ 

    // Number of vertices 
    N = 5; 

    // Given Edges 
    int arr[][2] 
        = { { 1, 2 }, { 2, 3 },  
            { 4, 5 }, { 1, 5 } }; 

    // Number of Edges 
    M = sizeof(arr) / sizeof(arr[0]); 

    // For Adjacency Matrix 
    int Adj[N + 1][N + 1]; 

    // Function call to create 
    // Adjacency Matrix 
    createAdjMatrix(Adj, arr); 

    // Print Adjacency Matrix 
    printAdjMatrix(Adj); 

    return 0; 
} 

```

**Output:**

```
0 1 0 0 1 
1 0 1 0 0 
0 1 0 0 0 
0 0 0 0 1 
1 0 0 1 0

```

***时间复杂度**：O（N <sup>2</sup> ）*，其中 N 是图形中顶点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。