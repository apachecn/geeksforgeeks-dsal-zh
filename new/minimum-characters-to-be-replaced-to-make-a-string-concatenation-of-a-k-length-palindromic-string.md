# 替换为 K 长度回文字符串的字符串连接的最小字符

> 原文： [https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-to-make-a-string-concatenation-of-a-k-length-palindromic-string/](https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-to-make-a-string-concatenation-of-a-k-length-palindromic-string/)

给定大小为`N`的[字符串](https://www.geeksforgeeks.org/string-data-structure/)`S`和正整数`K`（其中 **N％K = 0）** ，任务是找到需要替换的最小字符数，以使该字符串为`K`-句点，而`K`-长度的定期字符串必须为[回文[](https://www.geeksforgeeks.org/tag/palindrome/) 。

**示例**：

> **输入**：S =“ abaaba”，K = 3
> **输出**：0
> **说明**：给定的字符串已经是 K 周期且 定期字符串“ aba”是回文的。
> 
> **输入**：S =“ abaaba”，K = 2
> **输出**：2
> **说明**：将索引 1 和 4 的字符更改为 “ a”，更新的字符串“ aaaaaa”是 K 周期，而周期字符串“ aa”是回文。 因此，要求的最小更改为 2。

**方法**：的想法是从给定的字符串索引创建[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，并执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)以查找所需的更改次数。 请按照以下步骤解决此问题：

*   将总计为的变量**初始化为`0`，以存储所需的更改计数。**

*   根据给定的条件，从字符串创建图形，并在最终字符串中的所有位置 **i，K − i + 1，K + i，2K − i + 1、2K + i，3K − i + 1，…对于所有 **1≤i≤K** 的**应该相等。

*   在 **[0，N]** 范围内进行迭代，并在索引`i`和**（N – i – 1）**之间添加无方向的边。

*   在 **[0，N – M]** 范围内迭代，并在索引`i`和**（i + K）**之间添加无方向的边。

*   为了最大程度地减少所需的操作次数，请使所有字母最多等于出现在这些位置的字母，只需对字符串执行 [DFS 遍历](https://www.geeksforgeeks.org/iterative-depth-first-traversal/)即可轻松找到。

*   对所有未访问的节点，在创建的图形上执行 [**DFS 遍历**](https://www.geeksforgeeks.org/print-the-dfs-traversal-step-wise-backtracking-also/) ：

    *   在该遍历中访问的字符中找到频率最高的最大元素（例如 **maxFrequency** ）。

    *   通过 **DFS 遍历**中所有已访问字符的计数与上一步中的最大频率之差，更新字符的更改总数。

*   完成上述步骤后，打印**总计**的值作为结果。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include "bits/stdc++.h" 
using namespace std; 

// Function to add an edge to graph 
void addEdge(vector<int> adj[], int u, 
             int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// Function to perform DFS traversal on the 
// graph recursively from a given vertex u 
void DFS(int u, vector<int> adj[], 
         int& cnt, vector<bool>& visited, 
         int fre[], string S) 
{ 
    // Visit the current vertex 
    visited[u] = true; 

    // Total number of nodes 
    // in this component 
    cnt++; 

    // Increment the frequency of u 
    fre[S[u] - 'a']++; 

    for (int i = 0; 
         i < adj[u].size(); i++) { 
        if (!visited[adj[u][i]]) { 
            DFS(adj[u][i], adj, cnt, 
                visited, fre, S); 
        } 
    } 
} 

// Function for finding the minimum 
// number changes required in given string 
int minimumOperations(string& S, int m) 
{ 
    int V = 100; 
    vector<int> adj[V]; 
    int total = 0, N = S.length(); 

    // Form the edges according to the 
    // given conditions 
    for (int i = 0; i < N; i++) { 
        addEdge(adj, i, N - i - 1); 
        addEdge(adj, N - i - 1, i); 
    } 

    for (int i = 0; i < N - m; i++) { 
        addEdge(adj, i, i + m); 
        addEdge(adj, i + m, i); 
    } 

    // Find minimum number of operations 
    vector<bool> visited(V, 0); 

    for (int i = 0; i < N; i++) { 

        // Frequency array for finding 
        // the most frequent character 
        if (!visited[i]) { 

            // Frequency array for finding 
            // the most frequent character 
            int fre[26] = { 0 }; 
            int cnt = 0, maxx = -1; 

            DFS(i, adj, cnt, visited, fre, S); 

            // Finding most frequent character 
            for (int j = 0; j < 26; j++) 
                maxx = max(maxx, fre[j]); 

            // Change rest of the characters 
            // to most frequent one 
            total += cnt - maxx; 
        } 
    } 

    // Print total number of changes 
    cout << total; 
} 

// Driver Code 
int main() 
{ 
    string S = "abaaba"; 
    int K = 2; 

    // Function Call 
    minimumOperations(S, K); 

    return 0; 
} 

```

**Output:**

```
2

```

***时间复杂度**：`O(N)`*

***辅助空间**：`O(N)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。