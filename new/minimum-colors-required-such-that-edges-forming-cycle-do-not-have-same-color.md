# 使得边缘形成周期不具有相同颜色所需的最小颜色

> 原文： [https://www.geeksforgeeks.org/minimum-colors-required-such-that-edges-forming-cycle-do-not-have-same-color/](https://www.geeksforgeeks.org/minimum-colors-required-such-that-edges-forming-cycle-do-not-have-same-color/)

给定一个带`V`顶点和`E`边且没有自环和多个边的有向图，任务是找到所需的最少颜色数目，以使相同颜色的边不 形成循环并找到每个边缘的颜色。

**示例**：

> **输入**：V = {1、2、3}，E = {（1、2），（2、3），（3、1）}
> **输出**：2
> 1 1 2
> [![](img/da6ff0c82a8dee4176a96dc24126b9bf.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200317210537/Untitled-Diagram66-3.jpg) 
> **说明**：
> 在上面给出的图中，它仅形成一个循环，即
> ，即顶点 连接 1、2、3 形成一个循环
> ，然后将连接 1- > 2 或 2- > 3 或 3- > 1 的边缘涂成
> ，并用不同的颜色着色，从而形成边缘 周期没有相同的颜色
> 
> **输入**：V = {1,2,3,4,5}，E = {（1，2），（1，3），（2，3），（2，4），（ 3，4），（4，5），（5，3）}
> **输出**：2
> 边缘的颜色– 1 1 1 1 1 1 1 2
> **说明 **：
> 在上面给定的图中，它仅形成一个循环，
> 是连接 3、4、5 的顶点，形成一个循环
> ，然后连接 5- > 3 或 4- [ > 5 或 3- > 4 可以用不同的颜色着色
> ，以使形成循环的边没有相同的颜色
> 
> 边缘的最终颜色–
> {1：1，2：1，3：3：1，4：1，5：1，6：1，7：2}
> 上面的数组将对表示为– Edge ： 色标

**方法**：的想法是在图中找到循环，这可以借助的 [DFS 完成，其中当已经访问过的节点再次访问时， 一条新的边缘，然后用另一种颜色着色该边缘，否则，如果没有循环，则所有边缘只能用一种颜色着色。](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

**算法**：

*   用颜色 1 标记每个边缘，将每个顶点标记为未访问。
*   使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历该图并标记访问的节点。
*   如果已经访问了一个节点，则连接顶点的边将标记为用颜色 2 着色。
*   访问所有顶点时，打印边缘的颜色。

**实例说明**：
实例 1 的详细空运行

| 当前顶点 | 当前边缘 | 参观过的顶点 | 边缘的颜色 | 评论 |
| --- | --- | --- | --- | --- |
| 1 | 1–>2 | {1} | {1: 1, 2: 1, 3: 1} | 将节点 1 标记为已访问，并为节点 2 调用 DFS |
| 2 | 2–>3 | {1, 2} | {1: 1, 2: 1, 3: 1} | 将节点 2 标记为已访问，并为节点 3 调用 DFS |
| 3 | 3–>1 | {1, 2} | {1: 1, 2: 1, 3: 2} | 由于 1 已被访问，边缘 3 的颜色更改为 2 |

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the 
// minimum colors required to 
// such that edges forming cycle 
// don't have same color 

#include <bits/stdc++.h> 
using namespace std; 

const int n = 5, m = 7; 

// Variable to store the graph 
vector<pair<int, int> > g[m]; 

// To store that the  
// vertex is visited or not 
int col[n]; 

// Boolean Value to store that 
// graph contains cycle or not 
bool cyc; 

// Variable to store the color 
// of the edges of the graph 
int res[m]; 

// Function to traverse graph 
// using DFS Traversal 
void dfs(int v) 
{ 
    col[v] = 1; 

    // Loop to iterate for all  
    // edges from the source vertex 
    for (auto p : g[v]) { 
        int to = p.first, id = p.second; 

        // If the vertex is not visited 
        if (col[to] == 0) 
        { 
            dfs(to); 
            res[id] = 1; 
        } 

        // Condition to check cross and 
        // forward edges of the graph 
        else if (col[to] == 2) 
        { 
            res[id] = 1; 
        } 

        // Presence of Back Edge 
        else { 
            res[id] = 2; 
            cyc = true; 
        } 
    } 
    col[v] = 2; 
} 

// Driver Code 
int main() 
{ 
    g[0].push_back(make_pair(1, 0)); 
    g[0].push_back(make_pair(2, 1)); 
    g[1].push_back(make_pair(2, 2)); 
    g[1].push_back(make_pair(3, 3)); 
    g[2].push_back(make_pair(3, 4)); 
    g[3].push_back(make_pair(4, 5)); 
    g[4].push_back(make_pair(2, 6)); 

    // Loop to run DFS Traversal on  
    // vertex which is not visited 
    for (int i = 0; i < n; ++i) { 
        if (col[i] == 0) 
        { 
            dfs(i); 
        } 
    } 
    cout << (cyc ? 2 : 1) << endl; 

    // Loop to print the  
    // colors of the edges 
    for (int i = 0; i < m; ++i) { 
        cout << res[i] << ' '; 
    } 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the 
// minimum colors required to 
// such that edges forming cycle 
// don't have same color 
import java.util.*; 

class GFG{ 

static int n = 5, m = 7; 
static class pair 
{  
    int first, second;  
    public pair(int first, int second)   
    {  
        this.first = first;  
        this.second = second;  
    }     
}  

// Variable to store the graph 
static Vector<pair > []g = new Vector[m]; 

// To store that the  
// vertex is visited or not 
static int []col = new int[n]; 

// Boolean Value to store that 
// graph contains cycle or not 
static boolean cyc; 

// Variable to store the color 
// of the edges of the graph 
static int []res = new int[m]; 

// Function to traverse graph 
// using DFS Traversal 
static void dfs(int v) 
{ 
    col[v] = 1; 

    // Loop to iterate for all  
    // edges from the source vertex 
    for (pair  p : g[v]) { 
        int to = p.first, id = p.second; 

        // If the vertex is not visited 
        if (col[to] == 0) 
        { 
            dfs(to); 
            res[id] = 1; 
        } 

        // Condition to check cross and 
        // forward edges of the graph 
        else if (col[to] == 2) 
        { 
            res[id] = 1; 
        } 

        // Presence of Back Edge 
        else { 
            res[id] = 2; 
            cyc = true; 
        } 
    } 
    col[v] = 2; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    for(int i= 0; i < m; i++) 
        g[i] = new Vector<pair>(); 
    g[0].add(new pair(1, 0)); 
    g[0].add(new pair(2, 1)); 
    g[1].add(new pair(2, 2)); 
    g[1].add(new pair(3, 3)); 
    g[2].add(new pair(3, 4)); 
    g[3].add(new pair(4, 5)); 
    g[4].add(new pair(2, 6)); 

    // Loop to run DFS Traversal on  
    // vertex which is not visited 
    for (int i = 0; i < n; ++i) { 
        if (col[i] == 0) 
        { 
            dfs(i); 
        } 
    } 
    System.out.print((cyc ? 2 : 1) +"\n"); 

    // Loop to print the  
    // colors of the edges 
    for (int i = 0; i < m; ++i) { 
        System.out.print(res[i] +" "); 
    } 
} 
} 

// This code is contributed by sapnasingh4991 

```

## C#

```cs

// C# implementation to find the 
// minimum colors required to 
// such that edges forming cycle 
// don't have same color 
using System; 
using System.Collections.Generic; 

class GFG{ 

static int n = 5, m = 7; 
class pair 
{  
    public int first, second;  
    public pair(int first, int second)   
    {  
        this.first = first;  
        this.second = second;  
    }     
}  

// Variable to store the graph 
static List<pair> []g = new List<pair>[m]; 

// To store that the  
// vertex is visited or not 
static int []col = new int[n]; 

// Boolean Value to store that 
// graph contains cycle or not 
static bool cyc; 

// Variable to store the color 
// of the edges of the graph 
static int []res = new int[m]; 

// Function to traverse graph 
// using DFS Traversal 
static void dfs(int v) 
{ 
    col[v] = 1; 

    // Loop to iterate for all  
    // edges from the source vertex 
    foreach (pair  p in g[v]) { 
        int to = p.first, id = p.second; 

        // If the vertex is not visited 
        if (col[to] == 0) 
        { 
            dfs(to); 
            res[id] = 1; 
        } 

        // Condition to check cross and 
        // forward edges of the graph 
        else if (col[to] == 2) 
        { 
            res[id] = 1; 
        } 

        // Presence of Back Edge 
        else { 
            res[id] = 2; 
            cyc = true; 
        } 
    } 
    col[v] = 2; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    for(int i= 0; i < m; i++) 
        g[i] = new List<pair>(); 
    g[0].Add(new pair(1, 0)); 
    g[0].Add(new pair(2, 1)); 
    g[1].Add(new pair(2, 2)); 
    g[1].Add(new pair(3, 3)); 
    g[2].Add(new pair(3, 4)); 
    g[3].Add(new pair(4, 5)); 
    g[4].Add(new pair(2, 6)); 

    // Loop to run DFS Traversal on  
    // vertex which is not visited 
    for (int i = 0; i < n; ++i) { 
        if (col[i] == 0) 
        { 
            dfs(i); 
        } 
    } 
    Console.Write((cyc ? 2 : 1) +"\n"); 

    // Loop to print the  
    // colors of the edges 
    for (int i = 0; i < m; ++i) { 
        Console.Write(res[i] +" "); 
    } 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
2
1 1 1 1 1 1 2

```

**效果分析**：

*   **时间复杂度**：与上述方法一样，图中的 DFS 遍历需要 O（V + E）时间，其中 V 表示顶点数，E 表示边数。 因此，时间复杂度将为 **O（V + E）**。
*   **辅助空间**：O（1）。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。