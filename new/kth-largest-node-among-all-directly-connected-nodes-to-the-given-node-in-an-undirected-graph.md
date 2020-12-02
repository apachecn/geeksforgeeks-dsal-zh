# 在无向图

中，所有直接连接到给定节点的节点中的第 K 个最大节点

> 原文： [https://www.geeksforgeeks.org/kth-largest-node-among-all-directly-connected-nodes-to-the-given-node-in-an-undirected-graph/](https://www.geeksforgeeks.org/kth-largest-node-among-all-directly-connected-nodes-to-the-given-node-in-an-undirected-graph/)

给定两个数组`u`和`v`，它们表示一个图，使得从 **u [i]** 到 **v [i]** （0≤v [i]，u [i] < N），并且每个节点都有一些值 **val [i]** （0≤i < N）。 对于每个节点，如果直接连接到其上的节点根据其值按降序排序（如果值相等，则根据其索引按升序排序），以 **k [** 位置。 如果总节点为 **< k** ，则打印 **-1** 。

**示例**：

> **输入**：u [] = {0，0，1}，v [] = {2，1，2}，val [] = {2，4，3}，k = 2
> **输出**：
> 2
> 0
> 0
> 对于 0 个节点，直接连接到该节点的节点是 1 和 2
> 分别具有值 4 和 3，因此具有 第二个最大值是 2。
> 对于 1 个节点，直接连接到其的节点是 0 和 2
> 分别具有值 2 和 3，因此，第二个最大值是 0。 直接与其相连的节点分别为 0 和 1
> ，其值分别为 2 和 4，因此具有第二大值的节点为 0。
> 
> **输入**：u [] = {0，2}，v [] = {2，1}，val [] = {2，4，3}，k = 2
> **输出 **：
> -1
> -1
> 0

**方法**：的想法是将直接连接到节点的节点及其值存储在向量中，并按升序对它们进行排序，并且将节点的第 k 个最大值设为 **n [HTG3 直接连接到它的节点数将是**（n – k）**个从最后的节点。**

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print Kth node for each node 
void findKthNode(int u[], int v[], int n, int val[], int V, int k) 
{ 

    // Vector to store nodes directly 
    // connected to ith node along with 
    // their values 
    vector<pair<int, int> > g[V]; 

    // Add edges to the vector along with 
    // the values of the node 
    for (int i = 0; i < n; i++) { 
        g[u[i]].push_back(make_pair(val[v[i]], v[i])); 
        g[v[i]].push_back(make_pair(val[u[i]], u[i])); 
    } 

    // Sort neighbors of every node 
    // and find the Kth node 
    for (int i = 0; i < V; i++) { 
        if (g[i].size() > 0) 
            sort(g[i].begin(), g[i].end()); 

        // Get the kth node 
        if (k <= g[i].size()) 
            printf("%d\n", g[i][g[i].size() - k].second); 

        // If total nodes are < k 
        else
            printf("-1\n"); 
    } 

    return; 
} 

// Driver code 
int main() 
{ 
    int V = 3; 
    int val[] = { 2, 4, 3 }; 
    int u[] = { 0, 0, 1 }; 
    int v[] = { 2, 1, 2 }; 

    int n = sizeof(u) / sizeof(int); 
    int k = 2; 

    findKthNode(u, v, n, val, V, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.*; 

class GFG 
{ 

// pair class 
static class pair 
{ 
    int first,second; 
    pair(int a,int b) 
    { 
        first = a; 
        second = b; 
    } 
} 

// Function to print Kth node for each node  
static void findKthNode(int u[], int v[], int n,  
                        int val[], int V, int k)  
{  

    // Vector to store nodes directly  
    // connected to ith node along with  
    // their values  
    Vector<Vector<pair >> g = new Vector<Vector<pair>>(); 

    for(int i = 0; i < V; i++) 
    g.add(new Vector<pair>()); 

    // Add edges to the Vector along with  
    // the values of the node  
    for (int i = 0; i < n; i++)  
    {  
        g.get(u[i]).add(new pair(val[v[i]], v[i]));  
        g.get(v[i]).add(new pair(val[u[i]], u[i]));  
    }  

    // Sort neighbors of every node  
    // and find the Kth node  
    for (int i = 0; i < V; i++) 
    {  
        if (g.get(i).size() > 0)  
            Collections.sort(g.get(i),new Comparator<pair>()  
        {  
            public int compare(pair p1, pair p2)  
            {  
                return p1.first - p2.first;  
            }  
        });  

        // Get the kth node  
        if (k <= g.get(i).size())  
            System.out.printf("%d\n", g.get(i).get(g.get(i).size() - k).second);  

        // If total nodes are < k  
        else
            System.out.printf("-1\n");  
    }  

    return;  
}  

// Driver code  
public static void main(String args[]) 
{  
    int V = 3;  
    int val[] = { 2, 4, 3 };  
    int u[] = { 0, 0, 1 };  
    int v[] = { 2, 1, 2 };  

    int n = u.length;  
    int k = 2;  

    findKthNode(u, v, n, val, V, k);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation of the approach  

# Function to print Kth node for each node  
def findKthNode(u, v, n, val, V, k):  

    # Vector to store nodes directly connected  
    # to ith node along with their values  
    g = [[] for i in range(V)] 

    # Add edges to the vector along  
    # with the values of the node  
    for i in range(0, n):   
        g[u[i]].append((val[v[i]], v[i]))  
        g[v[i]].append((val[u[i]], u[i]))  

    # Sort neighbors of every node  
    # and find the Kth node  
    for i in range(0, V): 
        if len(g[i]) > 0:  
            g[i].sort()  

        # Get the kth node  
        if k <= len(g[i]):  
            print(g[i][-k][1])  

        # If total nodes are < k  
        else: 
            print("-1")  

    return 

# Driver code  
if __name__ == "__main__": 

    V = 3 
    val = [2, 4, 3]   
    u = [0, 0, 1]  
    v = [2, 1, 2]   
    n, k = len(u), 2

    findKthNode(u, v, n, val, V, k)  

# This code is contributed by Rituraj Jain 

```

**Output:**

```
2
0
0

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。