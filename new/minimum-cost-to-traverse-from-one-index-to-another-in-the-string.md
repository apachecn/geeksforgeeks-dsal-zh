# 字符串

中从一个索引遍历到另一个索引的最低成本

> 原文： [https://www.geeksforgeeks.org/minimum-cost-to-traverse-from-one-index-to-another-in-the-string/](https://www.geeksforgeeks.org/minimum-cost-to-traverse-from-one-index-to-another-in-the-string/)

给定长度为`N`的字符串`S`由小写字母组成，任务是找到从索引`i`到索引 **j 的最小开销** 。

在任何索引`k`处，跳到索引 **k + 1** 和 **k-1** （无界）的成本为 1。

此外，跳到任何索引`m`使得 **S [m] = S [k]** 的成本为 0。

**示例**：

> **输入**：S =“ abcde”，i = 0，j = 4
> **输出**：4
> **说明**：
> 最短路径 将会是：
> 0- > 1- > 2- > 3- > 4
> 因此，答案将是 4。
> 
> **输入**：S =“ abcdefb”，i = 0，j = 5
> **输出**：2
> **说明**：
> 0- > 1- > 6- > 5
> 0- > 1 边权重为 1，1- > 6 边权重为 0，而 6- > 5 边权重为 1。
> 因此，答案将是 2

**方法**：

1.  解决此问题的一种方法是 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 。

2.  可以将设置可视化为具有`N`个节点的图形。

3.  所有节点将连接到权重为“ 1”的相邻节点，并且具有相同字符的权重为“ 0”的节点。

4.  在此设置中，可以运行 [0-1 BFS](https://www.geeksforgeeks.org/0-1-bfs-shortest-path-binary-graph/) 来查找从索引“ i”到索引“ j”的最短路径。

**时间复杂度**：`O(N^2)`–顶点数为`O(N^2)`

**有效方法**：

1.  对于每个字符`X`，找到与之相邻的所有字符。

2.  创建图时，将节点数作为字符串中不同字符的数目，每个节点代表一个字符。

3.  每个节点`X`将具有权重 1 的边，所有节点代表与字符`X`相邻的字符。

4.  然后， [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 可以在这个新图中从代表 S [i]的节点运行到代表 S [j]的节点

**时间复杂度**：`O(N)`

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach. 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the minimum cost 
int findMinCost(string s, int i, int j) 
{ 
    // graph 
    vector<vector<int> > gr(26); 

    // adjacency matrix 
    bool edge[26][26]; 

    // initialising adjacency matrix 
    for (int k = 0; k < 26; k++) 
        for (int l = 0; l < 26; l++) 
            edge[k][l] = 0; 

    // creating adjacency list 
    for (int k = 0; k < s.size(); k++) { 
        // pushing left adjacent elelemt for index 'k' 
        if (k - 1 >= 0 
            and !edge[s[k] - 97][s[k - 1] - 97]) 
            gr[s[k] - 97].push_back(s[k - 1] - 97), 
                edge[s[k] - 97][s[k - 1] - 97] = 1; 
        // pushing right adjacent element for index 'k' 
        if (k + 1 <= s.size() - 1 
            and !edge[s[k] - 97][s[k + 1] - 97]) 
            gr[s[k] - 97].push_back(s[k + 1] - 97), 
                edge[s[k] - 97][s[k + 1] - 97] = 1; 
    } 

    // queue to perform BFS 
    queue<int> q; 
    q.push(s[i] - 97); 

    // visited array 
    bool v[26] = { 0 }; 

    // variable to store depth of BFS 
    int d = 0; 

    // BFS 
    while (q.size()) { 

        // number of elements in the current level 
        int cnt = q.size(); 

        // inner loop 
        while (cnt--) { 

            // current element 
            int curr = q.front(); 

            // popping queue 
            q.pop(); 

            // base case 
            if (v[curr]) 
                continue; 
            v[curr] = 1; 

            // checking if the current node is required node 
            if (curr == s[j] - 97) 
                return d; 

            // iterating through the current node 
            for (auto it : gr[curr]) 
                q.push(it); 
        } 

        // updating depth 
        d++; 
    } 

    return -1; 
} 

// Driver Code 
int main() 
{ 
    // input variables 
    string s = "abcde"; 
    int i = 0; 
    int j = 4; 

    // function to find the minimum cost 
    cout << findMinCost(s, i, j); 
} 

```