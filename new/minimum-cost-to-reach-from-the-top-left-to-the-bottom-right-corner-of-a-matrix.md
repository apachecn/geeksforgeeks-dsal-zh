# 从矩阵

的左上角到右下角的最低成本

> 原文： [https://www.geeksforgeeks.org/minimum-cost-to-reach-from-the-top-left-to-the-bottom-right-corner-of-a-matrix/](https://www.geeksforgeeks.org/minimum-cost-to-reach-from-the-top-left-to-the-bottom-right-corner-of-a-matrix/)

给定 **N * M** 矩阵 **mat [] []** 由小写字母组成的任务，任务是找到从单元格 **mat [0]达到的最低成本。 0]** 连接到单元格 **mat [N-1] [M-1]** 。 如果您在 **mat [i] [j]** 单元中，则可以跳到 **mat [i + 1] [j]** ， **mat [i] [ j + 1]** ， **mat [i-1] [j]** ， **mat [i] [j-1]** （无界），费用为`1`。 此外，您可以跳转到任何单元格 **mat [m] [n]** ，使得 **mat [n] [m] = mat [i] [j]** 的成本为 **] 0** 。

**示例**：

> **输入**：mat [] [] = {“ abc”，“ efg”，“ hij”}
> **输出**：4
> 最短路径之一将是：
> {0，0}-> {0，1}-> {0，2}-> {1，2}-> {2，2}
> 所有边 权重为 1，因此答案为 4。
> 
> **输入**：mat [] [] = {“ abc”，“ efg”，“ hbj”}
> **输出**：2
> {0，0}-> {0，1}-> {2，1}-> {2，2}
> 1 + 0 + 1 = 2

**朴素的方法**：解决此问题的一种方法是 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 。 用 **N * M** 个节点将设置可视化为图形。 所有节点将连接到权重为`1`的相邻节点，而具有相同字符的权重为`0`的节点。 现在，可以使用 BFS 查找从单元 **mat [0] [0] [0]** 到单元 mat [N-1] [M-1]的最短路径。 由于边数为 O（（N * M） <sup>2 **O [（N * M） <sup>2</sup> ）** HTG17]）。</sup>

**高效方法**：对于每个字符`X`，找到其相邻的所有字符。 现在，创建一个带有多个节点的图形，该节点为字符串中每个代表一个字符的不同字符的数量。

每个节点`X`将具有权重`1`的边，所有节点代表与实图中字符`X`相邻的字符。 然后，可以从代表 **mat [0] [0]** 的节点到代表 **mat [N-1] [M-1]** 的节点运行 BFS。 该方法的时间复杂度为 **O（N * M）**，用于图形的预处理，并且运行 BFS 的时间复杂度可以认为是恒定的。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

const int MAX = 26; 

// Function to return 
// the value (x - 97) 
int f(int x) 
{ 
    return x - 'a'; 
} 

// Function to return the minimum cost 
int findMinCost(vector<string> arr) 
{ 
    int n = arr.size(); 
    int m = arr[0].size(); 

    // Graph 
    vector<vector<int> > gr(MAX); 

    // Adjacency matrix 
    bool edge[MAX][MAX]; 

    // Initialising the adjacency matrix 
    for (int k = 0; k < MAX; k++) 
        for (int l = 0; l < MAX; l++) 
            edge[k][l] = 0; 

    // Creating the adjacency matrix 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < m; j++) { 
            if (i + 1 < n and !edge[f(arr[i][j])][f(arr[i + 1][j])]) { 
                gr[f(arr[i][j])].push_back(f(arr[i + 1][j])); 
                edge[f(arr[i][j])][f(arr[i + 1][j])] = 1; 
            } 
            if (j - 1 >= 0 and !edge[f(arr[i][j])][f(arr[i][j - 1])]) { 
                gr[f(arr[i][j])].push_back(f(arr[i][j - 1])); 
                edge[f(arr[i][j])][f(arr[i][j - 1])] = 1; 
            } 
            if (j + 1 < m and !edge[f(arr[i][j])][f(arr[i][j + 1])]) { 
                gr[f(arr[i][j])].push_back(f(arr[i][j + 1])); 
                edge[f(arr[i][j])][f(arr[i][j + 1])] = 1; 
            } 
            if (i - 1 >= 0 and !edge[f(arr[i][j])][f(arr[i - 1][j])]) { 
                gr[f(arr[i][j])].push_back(f(arr[i - 1][j])); 
                edge[f(arr[i][j])][f(arr[i - 1][j])] = 1; 
            } 
        } 

    // Queue to perform BFS 
    queue<int> q; 
    q.push(arr[0][0] - 'a'); 

    // Visited array 
    bool v[MAX] = { 0 }; 

    // To store the depth of BFS 
    int d = 0; 

    // BFS 
    while (q.size()) { 

        // Number of elements in 
        // the current level 
        int cnt = q.size(); 

        // Inner loop 
        while (cnt--) { 

            // Current element 
            int curr = q.front(); 

            // Popping queue 
            q.pop(); 

            // If the current node has 
            // already been visited 
            if (v[curr]) 
                continue; 
            v[curr] = 1; 

            // Checking if the current 
            // node is the required node 
            if (curr == arr[n - 1][m - 1] - 'a') 
                return d; 

            // Iterating through the current node 
            for (auto it : gr[curr]) 
                q.push(it); 
        } 

        // Updating the depth 
        d++; 
    } 

    return -1; 
} 

// Driver code 
int main() 
{ 
    vector<string> arr = { "abc", 
                           "def", 
                           "gbi" }; 

    cout << findMinCost(arr); 

    return 0; 
} 

```