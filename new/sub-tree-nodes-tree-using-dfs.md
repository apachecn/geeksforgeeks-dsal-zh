# 使用 DFS 的树中所有节点的子树

> 原文： [https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/](https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/)

给定树的 n 个节点及其连接，请打印每个节点的 Subtree 节点。

**节点的子树**被定义为树的子节点。 该名称强调了作为树节点后代的所有事物也都是树，并且是较大树的子集。

![](img/0bd437a69765eb606c8b8d3b489dc209.png)

**示例：**

```
Input: N = 5
  0 1
  1 2
  0 3
  3 4
Output: 
Subtree of node 0 is 1 2 3 4 
Subtree of node 1 is 2 
Subtree of node 3 is 4

Input: N = 7
  0 1
  1 2
  2 3
  0 4
  4 5
  4 6
Output:
Subtree of node 0 is 1 2 3 4 5 6 
Subtree of node 1 is 2 3 
Subtree of node 4 is 5 6 

```

**方法：**对每个节点进行 DFS 遍历，并打印从特定节点可访问的所有节点。
**以下代码的解释：**

1.  调用函数 dfs（0，0）时，start [0] = 0，dfs_order.push_back（0），已访问[0] = 1 以跟踪 dfs 顺序。
2.  现在，考虑邻接表（adj [100001]），因为考虑到连接到节点 0 的定向路径元素将在与节点 0 相对应的邻接表中。
3.  现在，递归调用 dfs 函数，直到遍历 adj [0]的所有元素。
4.  现在，调用 dfs（1，2），现在遍历 adj [1]个元素后，start [1] = 1，dfs_order.push_back（1），被访问[1] = 1。
5.  现在遍历 adj [1]，当遍历 adj [2]时，它仅包含节点 2，它不包含任何元素，它将中断并结束 end [1] = 2。
6.  同样，遍历所有节点并将 dfs_order 存储在数组中以找到节点的子树。

## C ++

```

// C++ code to print subtree of all nodes 
#include<bits/stdc++.h> 
using namespace std; 

// arrays for keeping position 
// at each dfs traversal for each node 
int start[100001]; 
int endd[100001]; 

// Storing dfs order 
vector<int>dfs_order; 
vector<int>adj[100001]; 
int visited[100001]; 

// Recursive function for dfs 
// traversal dfsUtil() 
void dfs(int a,int &b) 
{ 

    // keep track of node visited 
    visited[a]=1; 
    b++; 
    start[a]=b; 
    dfs_order.push_back(a); 

    for(vector<int>:: iterator it=adj[a].begin(); 
                           it!=adj[a].end();it++) 
    { 
        if(!visited[*it]) 
        { 
            dfs(*it,b); 
        } 
    } 
    endd[a]=b; 
} 

// Function to print the subtree nodes 
void Print(int n) 
{ 
    for(int i = 0; i < n; i++) 
    { 
        // if node is leaf node 
        // start[i] is equals to endd[i] 
        if(start[i]!=endd[i]) 
        { 
            cout<<"subtree of node "<<i<<" is "; 
            for(int j=start[i]+1;j<=endd[i];j++) 
            { 
                cout<<dfs_order[j-1]<<" "; 
            } 
            cout<<endl; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    // No of nodes n = 10 
    int n =10, c = 0; 

    adj[0].push_back(1); 
    adj[0].push_back(2); 
    adj[0].push_back(3); 
    adj[1].push_back(4); 
    adj[1].push_back(5); 
    adj[4].push_back(7); 
    adj[4].push_back(8); 
    adj[2].push_back(6); 
    adj[6].push_back(9); 

    // Calling dfs for node 0 
    // Considering root node at 0 
    dfs(0, c); 

    // Print child nodes 
    Print(n); 

    return 0; 

} 

```

## Python3

```

# Python3 code to print subtree of all nodes  

# arrays for keeping position at  
# each dfs traversal for each node  
start = [None] * 100001 
endd = [None] * 100001

# Storing dfs order  
dfs_order = []  
adj = [[] for i in range(100001)]  
visited = [False] * 100001

# Recursive function for dfs traversal dfsUtil()  
def dfs(a, b):  

    # keep track of node visited  
    visited[a] = 1 
    b += 1
    start[a] = b  
    dfs_order.append(a)  

    for it in adj[a]:  
        if not visited[it]:  
            b = dfs(it, b)  

    endd[a] = b 
    return b 

# Function to print the subtree nodes  
def Print(n):  

    for i in range(0, n):  

        # If node is leaf node  
        # start[i] is equals to endd[i]  
        if start[i] != endd[i]:  

            print("subtree of node", i, "is", end = " ")  
            for j in range(start[i]+1, endd[i]+1):  

                print(dfs_order[j-1], end = " ")  

            print() 

# Driver code  
if __name__ == "__main__":  

    # No of nodes n = 10  
    n, c = 10, 0 

    adj[0].append(1)  
    adj[0].append(2)  
    adj[0].append(3)  
    adj[1].append(4)  
    adj[1].append(5)  
    adj[4].append(7)  
    adj[4].append(8)  
    adj[2].append(6)  
    adj[6].append(9)  

    # Calling dfs for node 0  
    # Considering root node at 0  
    dfs(0, c)  

    # Print child nodes  
    Print(n) 

# This code is contributed by Rituraj Jain 

```

**Output:**

```
subtree of node 0 is 1 4 7 8 5 2 6 9 3 
subtree of node 1 is 4 7 8 5 
subtree of node 2 is 6 9 
subtree of node 4 is 7 8 
subtree of node 6 is 9

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。