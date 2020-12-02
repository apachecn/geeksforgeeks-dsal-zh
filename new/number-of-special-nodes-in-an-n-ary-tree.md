# 一元树

中特殊节点的数量

> 原文： [https://www.geeksforgeeks.org/number-of-special-nodes-in-an-n-ary-tree/](https://www.geeksforgeeks.org/number-of-special-nodes-in-an-n-ary-tree/)

给定一棵以顶点 1 为根的 n 元树。该树具有 n 个顶点和 n-1 个边。 每个节点都有一个与之关联的值，并且树以邻接表的形式输入。 任务是找到树中特殊节点的数量。 如果从根到节点的路径由不同的值节点组成，则该节点是特殊的。

**示例**：

```
Input: val[] = {1, 2, 3, 4, 5, 7, 2, 3}
                1
               / \
              2   3
             / \   \
            4   5   7
               / \
              2   3

Output: 7
All nodes except the leaf node 2 are special.

Input: val[] = {2, 1, 4, 3, 4, 8, 10, 2, 5, 1}
                2
               / \
              1   4
            / \ \  \
           3  4  8  10
            / \ \
           2  5  1

Output: 8
Leaf nodes 2 and 1 are not special.

```

**方法**：这个想法是使用邻接表在给定的树上执行 dfs。 在执行 dfs 时，插入集合中访问的节点的值。 如果当前节点的值已存在于集合中，则当前节点和以当前节点为根的子树中的所有节点都不特殊。 遍历以当前节点为根的子树后，将当前节点的值从 set 中删除，因为此值或该节点不在从根到所有其他未访问节点的路径上。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// DFS function to traverse the tree and find 
// number of special nodes 
void dfs(int val[], int n, vector<int> adj[], int v, 
         unordered_set<int>& values, int& ans) 
{ 

    // If value of current node is already 
    // present earlier in path then this 
    // node and all other nodes connected to 
    // it are not special 
    if (values.count(val[v])) 
        return; 

    // Insert value of current node in 
    // set of values traversed 
    ans++; 
    values.insert(val[v]); 

    // Call dfs on all adjacent nodes 
    for (auto ele : adj[v]) { 
        dfs(val, n, adj, ele, values, ans); 
    } 

    // Erase value of current node as all paths 
    // passing through current node are traversed 
    values.erase(val[v]); 
} 

// Driver code 
int main() 
{ 
    int val[] = { 0, 2, 1, 4, 3, 4, 8, 10, 2, 5, 1 }; 
    int n = sizeof(val) / sizeof(val[0]); 

    vector<int> adj[n]; 

    adj[1].push_back(2); 
    adj[1].push_back(3); 
    adj[2].push_back(4); 
    adj[2].push_back(5); 
    adj[2].push_back(6); 
    adj[3].push_back(7); 
    adj[5].push_back(8); 
    adj[5].push_back(9); 
    adj[5].push_back(10); 

    unordered_set<int> values; 

    int ans = 0; 

    dfs(val, n, adj, 1, values, ans); 

    cout << ans; 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 

class GFG 
{ 

static int ans; 

// DFS function to traverse the tree and find 
// number of special nodes 
static void dfs(int val[], int n, Vector<Integer> adj[], int v, 
        HashSet<Integer> values) 
{ 

    // If value of current node is already 
    // present earlier in path then this 
    // node and all other nodes connected to 
    // it are not special 
    if (values.contains(val[v])) 
        return; 

    // Insert value of current node in 
    // set of values traversed 
    ans++; 
    values.add(val[v]); 

    // Call dfs on all adjacent nodes 
    for (int ele : adj[v]) 
    { 
        dfs(val, n, adj, ele, values); 
    } 

    // Erase value of current node as all paths 
    // passing through current node are traversed 
    values.remove(val[v]); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int val[] = { 0, 2, 1, 4, 3, 4, 8, 10, 2, 5, 1 }; 
    int n = val.length; 

    Vector<Integer> []adj = new Vector[n]; 
    for(int i = 0; i < n ; i++)  
    { 
        adj[i] = new Vector<Integer>(); 
    } 
    adj[1].add(2); 
    adj[1].add(3); 
    adj[2].add(4); 
    adj[2].add(5); 
    adj[2].add(6); 
    adj[3].add(7); 
    adj[5].add(8); 
    adj[5].add(9); 
    adj[5].add(10); 

    ans = 0; 
    dfs(val, n, adj, 1, new HashSet<Integer>()); 
    System.out.print(ans); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python

```py

# Python3 implementation of the approach  

# DFS function to traverse the tree  
# and find number of special nodes  
def dfs(val, n, adj, v, values):  

    # If value of current node is already  
    # present earlier in path then this  
    # node and all other nodes connected 
    # to it are not special  
    if val[v] in values:  
        return

    global ans 

    # Insert value of current node in  
    # set of values traversed  
    ans += 1
    values.add(val[v])  

    # Call dfs on all adjacent nodes  
    for ele in adj[v]:  
        dfs(val, n, adj, ele, values)  

    # Erase value of current node as all  
    # paths passing through current node  
    # are traversed  
    values.remove(val[v])  

# Driver code  
if __name__ == "__main__": 

    val = [0, 2, 1, 4, 3, 4, 8, 10, 2, 5, 1]  
    n = len(val)  

    adj = [[] for i in range(n)]  

    adj[1].append(2)  
    adj[1].append(3)  
    adj[2].append(4)  
    adj[2].append(5)  
    adj[2].append(6)  
    adj[3].append(7)  
    adj[5].append(8)  
    adj[5].append(9)  
    adj[5].append(10)  

    values = set()  
    ans = 0
    dfs(val, n, adj, 1, values)  
    print(ans)  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

static int ans; 

// DFS function to traverse the tree and find 
// number of special nodes 
static void dfs(int []val, int n, List<int> []adj, int v, 
        HashSet<int> values) 
{ 

    // If value of current node is already 
    // present earlier in path then this 
    // node and all other nodes connected to 
    // it are not special 
    if (values.Contains(val[v])) 
        return; 

    // Insert value of current node in 
    // set of values traversed 
    ans++; 
    values.Add(val[v]); 

    // Call dfs on all adjacent nodes 
    foreach (int ele in adj[v]) 
    { 
        dfs(val, n, adj, ele, values); 
    } 

    // Erase value of current node as all paths 
    // passing through current node are traversed 
    values.Remove(val[v]); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int []val = { 0, 2, 1, 4, 3, 4, 8, 10, 2, 5, 1 }; 
    int n = val.Length; 

    List<int> []adj = new List<int>[n]; 
    for(int i = 0; i < n ; i++)  
    { 
        adj[i] = new List<int>(); 
    } 
    adj[1].Add(2); 
    adj[1].Add(3); 
    adj[2].Add(4); 
    adj[2].Add(5); 
    adj[2].Add(6); 
    adj[3].Add(7); 
    adj[5].Add(8); 
    adj[5].Add(9); 
    adj[5].Add(10); 

    ans = 0; 
    dfs(val, n, adj, 1, new HashSet<int>()); 
    Console.Write(ans); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
8

```

**时间复杂度**：O（n）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。