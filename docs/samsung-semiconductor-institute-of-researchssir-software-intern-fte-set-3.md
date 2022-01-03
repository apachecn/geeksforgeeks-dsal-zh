# 三星半导体研究所（SSIR 软件）实习生/ FTE | 系列 3

> 原文： [https://www.geeksforgeeks.org/samsung-semiconductor-institute-of-researchssir-software-intern-fte-set-3/](https://www.geeksforgeeks.org/samsung-semiconductor-institute-of-researchssir-software-intern-fte-set-3/)

我们给定 m * n 矩阵，该矩阵可以具有 0 到 7 之间的数字。每个数字代表具有以下形状的管道：

![Pipes](img/bd2c309899392ab2dc25a1ea3fc5f5b4.png)

如果两端连接，则认为两个管道已连接。

> 示例：
> 如果矩阵如下：
> 0040
> 1360
> 5000
> 
> 管道 1 和 3 {1 向右打开。 3 向左打开}已连接。 其他连接的管道是 3 和 6（3 向右打开。6 向左打开）。
> 
> 未连接 4 和 6，因为 6 未打开至顶部，4 未打开至底部。
> 
> 1 和 5 也没有连接，即使 1 打开到底部，5 没有打开到顶部。

给定该矩阵，起点（X，Y）和探针工具“ L”的长度，找出可以达到多少个管道{矩阵元素}。

注意：探针工具：是一种测量工具，如果可以达到 6 个管道但探针工具的长度为 4。如果可以达到 3 个管道但探针工具的长度为 4，答案为 4。答案为 3。

> 示例：
> 起始索引：（1、0）
> 探针长度：4
> 矩阵：
> 0040
> 1360
> 5000
> 通过探针连接的管道-（1、0 ）->（1、1）->（1、2）
> Ans-3
> 
> 起始索引：（0，0）
> 探针长度：4
> 矩阵：
> 0040
> 1360
> 5000
> 通过探针-0
> Ans-0 连接管道
> 
> 起始索引：（1，0）
> 探针长度：2
> 矩阵：
> 0040
> 1360
> 5000
> 通过探针-（1，0）->连接的管道 （1，1）
> Ans-2

**要解决的关键步骤**：

查找可以从一个起点访问哪些相邻管道元素{维护详尽的检查清单，以确定如上所述的相邻标准}。

找到一种方法来处理元素，以查找下一组可以访问的元素。 {遍历图表}。 应当注意，我们希望以小于“ L”的距离到达从起始节点可访问的所有节点。 重点不是到达许多节点，而是以从起点（X，Y）较小的动作到达它们。

**递归**：

我们将所有节点标记为未访问，而访问的节点计数为 0。如果在递归过程中处理了标记为未访问的节点，则将访问的节点计数增加 1 并将其标记为已访问。

我们首先访问“开始”节点（X，Y），然后递归访问其所有连接的邻居（基于对上述连接标准的检查），直到递归深度为“ L”。

**缺点**：

如果矩阵高度连接（几乎所有管道都连接在一起，并且存在多种到达管道的方式），我们会多次到达节点并对其进行多次处理，这可能会 导致运行时间长。 我们可以通过检查是否仅在递归级别较低的节点上再次处理该节点来对其进行优化。

这不是 DFS 解决方案，因为即使已经访问过我们也会重新处理节点，因为新的访问可能会将节点的访问深度更新为较低的级别，并且在该节点之后可以达到更大的深度。

**广度优先搜索**：

我们将所有节点标记为未访问，并将访问的节点数标记为 0。如果在处理过程中处理了标记为未访问的节点，则将访问的节点数增加 1。

首先将起始节点（X，Y）推入深度为 1 的队列中，然后开始处理该队列直到其为空。

在每次迭代中，取出队列成员并分析其连接的邻居。 如果不访问邻居并且当前元素的深度不大于 L，则将连接的元素放入队列，将标记为已访问和已访问的节点数增加 1。

由于 BFS 执行节点的级别顺序遍历，因此不可能在更短的距离内到达被访问的节点。 因此，不存在先前方法的缺点。 这是针对此问题的最佳解决方案。

**在简化编码的解决方案中可能会简化**：

由于有 7 种类型的管道，我们将必须放置多个 if 条件，导致嵌套 if 语句难以调试。 通过将 7 个值转换为基于方向的数据可以简化此过程。 例如 每个值都可以转换为具有 4 个布尔变量的结构，每个方向一个。 或者，每个数字都可以映射到一个 4 位数字，其中每个位代表一个方向。 在减少输入之后，检查将变得更简单且复杂度更低。

```

#include <bits/stdc++.h> 
using namespace std; 
#define Max 1000 
#define row_size 3 
#define col_size 4 

int x = 1, y = 0; // starting index(x, y), 
int l = 4; // length of probe tool 

// input matrix containing the pipes 
int mt[row_size][col_size] = { { 0, 0, 4, 0 }, 
                               { 1, 3, 6, 0 }, 
                               { 5, 0, 0, 0 } }; 

// visited matrix checks for cells already visited 
int vi[row_size][col_size];  

// calculates the depth of connection for each cell 
int depth[row_size][col_size];  

int f = 0; 
int r = 0; 

// queue for BFS 
struct node { 
    int x; 
    int y; 
    int d; 
}; 
node q[Max]; 
void push(int a, int b, int d) // push function 
{ 
    node temp; 
    temp.x = a; 
    temp.y = b; 
    temp.d = d; 
    q[r++] = temp; 
    vi[a][b] = 1; 
} 
node pop() // pop function 
{ 
    node temp; 
    temp.x = q[f].x; 
    temp.y = q[f].y; 
    temp.d = q[f].d; 
    f++; 
    return temp; 
} 

// It can be simplified by converting the 7 
// values into direction based data. For e.g.  
// each value can be transformed into a structure 
// with 4 Boolean variables, one for each direction.  
// Alternatively, each number can be mapped to a 4 
// bit number where each bit represents a direction. 
bool s1(int i, int j) // conversion to final direction 
{ 
    if (i >= 0 && i < row_size && j >= 0 && 
        j < col_size && vi[i][j] == 0 && (mt[i][j] == 1 ||  
        mt[i][j] == 3 || mt[i][j] == 6 || mt[i][j] == 7)) 
        return true; 
    else
        return false; 
} 

bool s2(int i, int j) // conversion to final direction 
{ 
    if (i >= 0 && i < row_size && j >= 0 && j < col_size &&  
        vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 2 || 
        mt[i][j] == 4 || mt[i][j] == 7)) 
        return true; 
    else
        return false; 
} 
bool s3(int i, int j) // conversion to final direction 
{ 
    if (i >= 0 && i < row_size && j >= 0 && j < col_size && 
        vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 3 || 
        mt[i][j] == 4 || mt[i][j] == 5)) 
        return true; 
    else
        return false; 
} 
bool s4(int i, int j) // conversion to final direction 
{ 
    if (i >= 0 && i < row_size && j >= 0 && j < col_size &&  
       vi[i][j] == 0 && (mt[i][j] == 1 || mt[i][j] == 2 ||  
       mt[i][j] == 6 || mt[i][j] == 5)) 
        return true; 
    else
        return false; 
} 

// search for connection 
// We start by pushing the start node (X, Y) into a queue 
// with depth 1  and then start processing the queue till  
// it is empty. 
void bfs(int x, int y, int d)  
{ 
    push(x, y, d); 
    while (r > f) { 
        node temp = pop(); 
        int i = temp.x; 
        int j = temp.y; 
        int c = temp.d; 
        depth[i][j] = c; 

        if (mt[i][j] == 1 || mt[i][j] == 3 || 
            mt[i][j] == 4 || mt[i][j] == 5) { 
            if (s1(i, j + 1)) 
                push(i, j + 1, c + 1); 
        } 
        if (mt[i][j] == 1 || mt[i][j] == 2 || 
            mt[i][j] == 6 || mt[i][j] == 5) { 
            if (s2(i + 1, j)) 
                push(i + 1, j, c + 1); 
        } 
        if (mt[i][j] == 1 || mt[i][j] == 3 || 
            mt[i][j] == 7 || mt[i][j] == 6) { 
            if (s3(i, j - 1)) 
                push(i, j - 1, c + 1); 
        } 
        if (mt[i][j] == 1 || mt[i][j] == 2 || 
            mt[i][j] == 4 || mt[i][j] == 7) { 
            if (s4(i - 1, j)) 
                push(i - 1, j, c + 1); 
        } 
    } 
} 
int main() // main function 
{ 

    f = 0; 
    r = 0; 
    // matrix 
    for (int i = 0; i < row_size; i++) { 
        for (int j = 0; j < col_size; j++) { 

            // visited matrix for BFS set to  
            // unvisited for every cell 
            vi[i][j] = 0;  

            // depth set to max intial value 
            depth[i][j] = Max; 
        } 
    } 

    if (mt[x][y] != 0) // condition for BFS 
        bfs(x, y, 1); 

    int nc = 0; 
    for (int i = 0; i < row_size; i++) { 
        for (int j = 0; j < col_size; j++) { 
            if (depth[i][j] <= l) { 
                cout << "(" << i << ", " << j << ")"; 
                nc++; 
            } 
        } 
    } 
    cout << " " << nc << "\n"; 
} 

```

**Output:**

```
(1, 0)(1, 1)(1, 2) 3

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。