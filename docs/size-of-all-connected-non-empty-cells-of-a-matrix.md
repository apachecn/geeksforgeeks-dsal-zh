# 矩阵

所有连接的非空单元的大小

> 原文： [https://www.geeksforgeeks.org/size-of-all-connected-non-empty-cells-of-a-matrix/](https://www.geeksforgeeks.org/size-of-all-connected-non-empty-cells-of-a-matrix/)

给定二进制矩阵 **mat [] []** ，任务是找到所有可能的非空连接单元的大小。

> 空单元由`0`表示，非空单元由`1`表示。
> 如果两个单元在水平或垂直方向上相邻，则称为已连接，即 **mat [i] [j] = mat [i] [j – 1]** 或**垫 [i] [j] = mat [i] [j +1]** 或 **mat [i] [j] = mat [i – 1] [j]** 或 **mat [i ] [j] = mat [i +1] [j]** 。

**示例**：

> **输入**：mat [] [] = {{1，1，0，0，0}，{0，1，0，0，1}，{1，0，0，1，1} ，{0，0，0，0，0}，{1，0，1，0，1}}}
> **输出**：3 3 1 1 1 1 1
> **说明**：
> {mat [0] [0]，mat [0] [1]，mat [1] [1]}，{mat [1] [4]，mat [2] [3]，mat [2] [4]}}，{mat [2] [0]}，{mat [4] [0]}，{mat [4] [2]}，{mat [4 [4]} 可能的连接。
> 
> **输入**：mat [] [] = {{1，1，0，0，0}，{1，1，0，1，1}，{1，0，0，1，1} ，{0，0，0，0，0}，{0，0，1，1，1}}}
> **输出**：5 4 3

**方法**：

的想法是在矩阵上使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 和[递归](https://www.geeksforgeeks.org/recursion/)。

请按照以下步骤操作：

*   初始化[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)并插入一个单元格（ **mat [i] [j] = 1** ）。

*   对插入的单元格执行 **BFS** ，并遍历其相邻单元格。

*   检查边界条件，并检查当前元素是否为`1`，然后将其翻转为`0`。

*   标记访问的单元格并更新连接的非空单元格的大小。

*   最后，打印获得的所有连接尺寸。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find size of all the
// islands from the given matrix
int BFS(vector<vector<int> >& mat,
        int row, int col)
{
    int area = 0;

    // Initialize a queue for
    // the BFS traversal
    queue<pair<int, int> > Q;
    Q.push({ row, col });

    // Iterate untill the
    // queue is empty
    while (!Q.empty()) {

        // Top element of queue
        auto it = Q.front();

        // Pop the element
        Q.pop();

        int r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 || r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r] == 0)
            continue;

        // Check if current element is 1
        if (mat[r] == 1) {

            // Mark the cell visited
            mat[r] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.push({ r + 1, c });
        Q.push({ r - 1, c });
        Q.push({ r, c + 1 });
        Q.push({ r, c - 1 });
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
void sizeOfConnections(vector<vector<int> > mat)
{

    // Stores the size of each
    // connected non-empty
    vector<int> result;

    for (int row = 0; row < 5; ++row) {
        for (int col = 0; col < 5; ++col) {

            // Check if the cell is
            // non-empty
            if (mat[row][col] == 1) {

                // Function call
                int area = BFS(mat, row, col);
                result.push_back(area);
            }
        }
    }

    // Print the answer
    for (int val : result)
        cout << val << " ";
}

// Driver Code
int main()
{

    vector<vector<int> > mat
        = { { 1, 1, 0, 0, 0 },
            { 1, 1, 0, 1, 1 },
            { 1, 0, 0, 1, 1 },
            { 1, 0, 0, 0, 0 },
            { 0, 0, 1, 1, 1 } };

    sizeOfConnections(mat);

    return 0;
}

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*;
import java.lang.*;

class GFG{

static class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find size of all the
// islands from the given matrix
static int BFS(int[][] mat,
               int row, int col)
{
    int area = 0;

    // Initialize a queue for
    // the BFS traversal
    Queue<pair> Q = new LinkedList<>();
    Q.add(new pair(row, col));

    // Iterate untill the
    // queue is empty
    while (!Q.isEmpty())
    {

        // Top element of queue
        pair it = Q.peek();

        // Pop the element
        Q.poll();

        int r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 ||
            r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r] == 0)
            continue;

        // Check if current element is 1
        if (mat[r] == 1) 
        {

            // Mark the cell visited
            mat[r] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.add(new pair(r + 1, c));
        Q.add(new pair(r - 1, c));
        Q.add(new pair(r, c + 1));
        Q.add(new pair(r, c - 1));
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
static void sizeOfConnections(int[][] mat)
{

    // Stores the size of each
    // connected non-empty
    ArrayList<Integer> result = new ArrayList<>();

    for(int row = 0; row < 5; ++row)
    {
        for(int col = 0; col < 5; ++col)
        {

            // Check if the cell is
            // non-empty
            if (mat[row][col] == 1)
            {

                // Function call
                int area = BFS(mat, row, col);
                result.add(area);
            }
        }
    }

    // Print the answer
    for(int val : result)
       System.out.print(val + " ");
}

// Driver code
public static void main (String[] args)
{
    int[][] mat = { { 1, 1, 0, 0, 0 },
                    { 1, 1, 0, 1, 1 },
                    { 1, 0, 0, 1, 1 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 0, 1, 1, 1 } };

    sizeOfConnections(mat);
}
}

// This code is contributed by offbeat

```

**Output:** 

```
6 4 3

```

**时间复杂度**：O（row * col）

**辅助空间**：O（row * col）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。