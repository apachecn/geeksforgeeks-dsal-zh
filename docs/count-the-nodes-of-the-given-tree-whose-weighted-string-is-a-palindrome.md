# 计算给定树的加权字符串为回文的节点

> 原文： [https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weighted-string-is-a-palindrome/](https://www.geeksforgeeks.org/count-the-nodes-of-the-given-tree-whose-weighted-string-is-a-palindrome/)

给定一棵树，以及所有节点的权重（以字符串的形式），任务是计算权重为回文的节点。

**示例**：

```
Input: 

Output: 3
Only the weights of the nodes 2, 3 and 5 are palindromes.

```

**方法**：在树上执行 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，对于每个节点，检查其字符串是否为回文。 如果是，则增加计数。

**实施**：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

int cnt = 0; 

vector<int> graph[100]; 
vector<string> weight(100); 

// Function that returns true 
// if x is a palindrome 
bool isPalindrome(string x) 
{ 
    int n = x.size(); 
    for (int i = 0; i < n / 2; i++) { 
        if (x[i] != x[n - 1 - i]) 
            return false; 
    } 
    return true; 
} 

// Function to perform dfs 
void dfs(int node, int parent) 
{ 

    // Weight of the current node 
    string x = weight[node]; 

    // If the weight is a palindrome 
    if (isPalindrome(x)) 
        cnt += 1; 

    for (int to : graph[node]) { 
        if (to == parent) 
            continue; 
        dfs(to, node); 
    } 
} 

// Driver code 
int main() 
{ 

    // Weights of the node 
    weight[1] = "abc"; 
    weight[2] = "aba"; 
    weight[3] = "bcb"; 
    weight[4] = "moh"; 
    weight[5] = "aa"; 

    // Edges of the tree 
    graph[1].push_back(2); 
    graph[2].push_back(3); 
    graph[2].push_back(4); 
    graph[1].push_back(5); 

    dfs(1, 1); 

    cout << cnt; 

    return 0; 
} 

```