# 要添加到图上以满足给定条件的最小边数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-edges-to-be-added-to-a-graph-to-satisfy-the-given-condition/](https://www.geeksforgeeks.org/minimum-number-of-edges-to-be-added-to-a-graph-to-satisfy-the-given-condition/)

给定一个**图**，由`N`个节点组成，编号从`0`到 **N – 1** 和`M`个边 对 **{a，b}** 中，任务是找到要添加到图中的最小边数，使得如果存在从任何节点**，**到节点`b`，那么也应该有从节点`a`到节点 **[a + 1，a + 2，a + 3，...，b – 1]** 的路径 。

**示例**：[

> **输入**：N = 7，M = 3，边线[] [] = {{1，5}，{2，4}，{3，4}}
> **输出**：1
> **说明**：
> 路径从 1 到 5。因此也应该有路径从 1 到 2、3 和 4。
> 添加边线{1，2}将足以到达图的其他两个节点。
> 
> **输入**：N = 8，M = 3 条边线[] [] = {{1，2}，{2，3}，{3，4}}
> **输出**：0

**方法**：

这个想法是使用[不交集或联合查找](https://www.geeksforgeeks.org/union-find/)。 不相交集中的每个组件应具有连续的节点。 这可以通过维护 *maximum_node []* 和 *minimum_node []* 数组来分别存储每个组件中节点的最大值和最小值来完成。 请按照以下步骤解决问题：

*   为不交集联合创建结构。

*   将**答案**初始化为 0，并遍历图中的所有节点以获取当前节点的组件。

*   如果组件是**，则未访问**，则将其标记为已访问。

*   现在，从该组件的最小值到最大值进行迭代，并检查节点是否与当前节点位于同一组件中，并将它们组合为一个组件，然后将**答案**增加 *1* 。

*   最后，打印**答案**。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 
#include <bits/stdc++.h> 
#define MOD 1000000007 

#define int long long int 
using namespace std; 

// Disjoint Set Union 
struct dsu { 

    // Stores the parent 
    // of each node 
    vector<int> parent; 

    // Storing maximum value 
    // in each component 
    vector<int> maximum_node; 

    // Stores the minimum value 
    // in each component 
    vector<int> minimum_node; 

    // Stores the visited nodes 
    vector<int> visited; 

    // Function to initialize the 
    // values in vectors 
    void init(int n) 
    { 
        // Initialize the size of 
        // vectors as n 
        parent.resize(n); 
        maximum_node.resize(n); 
        minimum_node.resize(n); 
        visited.resize(n); 

        for (int i = 0; i < n; i++) { 

            // Initially every component 
            // has only one node 
            parent[i] = i; 
            maximum_node[i] = i; 
            minimum_node[i] = i; 

            // Mark unvisited 
            visited[i] = 0; 
        } 
    } 

    // Function to get identifier node 
    // (superparent) for each component 
    int getsuperparent(int x) 
    { 

        // If parent of a node is that 
        // node itself then the node is 
        // superparent of that component 
        return x == parent[x] 
                   ? x 
                   : parent[x] 
                     = getsuperparent(parent[x]); 
    } 

    // Function to perform union of two 
    // different components 
    void unite(int x, int y) 
    { 

        int superparent_x = getsuperparent(x); 
        int superparent_y = getsuperparent(y); 

        // Set superparent of y as the 
        // parent of superparent of x 
        parent[superparent_x] = superparent_y; 

        // Update the maximum node 
        // in the component containing y 
        maximum_node[superparent_y] 
            = max(maximum_node[superparent_y], 
                  maximum_node[superparent_x]); 

        // Update the minimum node 
        // in the component containing y 
        minimum_node[superparent_y] 
            = min(minimum_node[superparent_y], 
                  minimum_node[superparent_x]); 
    } 
} G; 

// Function to find the minimum number 
// of edges to be added to the Graph 
int minimumEdgesToBeAdded(int n) 
{ 
    // Stores the answer 
    int answer = 0; 

    // Iterate over all nodes 
    for (int i = 0; i < n; i++) { 

        // Get the superparent of 
        // the current node 
        int temp = G.getsuperparent(i); 

        // If the node is not visited 
        if (!G.visited[temp]) { 

            // Set the node as visited 
            G.visited[temp] = 1; 

            // Iterate from the minimum 
            // value to maximum value in 
            // the current component 
            for (int j = G.minimum_node[temp]; 
                 j <= G.maximum_node[temp]; j++) { 

                // If the nodes are in 
                // different components 
                if (G.getsuperparent(j) 
                    != G.getsuperparent(i)) { 

                    // Unite them 
                    G.unite(i, j); 

                    // Increment the answer 
                    answer++; 
                } 
            } 
        } 
    } 

    // Return the answer 
    return answer; 
} 

// Driver Code 
int32_t main() 
{ 
    int N = 7, M = 3; 

    G.init(N); 

    // Insert edges 
    G.unite(1, 5); 
    G.unite(2, 4); 
    G.unite(3, 4); 

    cout << minimumEdgesToBeAdded(N); 
    return 0; 
} 

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*; 

class GFG{ 

static final int MOD = 1000000007; 

// Disjoint Set Union 
static class dsu 
{ 
    public dsu(){} 

    // Stores the parent 
    // of each node 
    int[] parent; 

    // Storing maximum value 
    // in each component 
    int[] maximum_node; 

    // Stores the minimum value 
    // in each component 
    int[] minimum_node; 

    // Stores the visited nodes 
    int[] visited; 

    // Function to initialize the 
    // values in vectors 
    void init(int n) 
    { 

        // Initialize the size of 
        // vectors as n 
        parent = new int[n]; 
        maximum_node = new int[n]; 
        minimum_node = new int[n]; 
        visited = new int[n]; 

        for(int i = 0; i < n; i++) 
        { 

            // Initially every component 
            // has only one node 
            parent[i] = i; 
            maximum_node[i] = i; 
            minimum_node[i] = i; 

            // Mark unvisited 
            visited[i] = 0; 
        } 
    } 

    // Function to get identifier node 
    // (superparent) for each component 
    int getsuperparent(int x) 
    { 

        // If parent of a node is that 
        // node itself then the node is 
        // superparent of that component 
        if(x == parent[x]) 
            return x; 
        else
        { 
            parent[x] = getsuperparent(parent[x]); 
            return parent[x]; 
        } 
    } 

    // Function to perform union of two 
    // different components 
    void unite(int x, int y) 
    { 
        int superparent_x = getsuperparent(x); 
        int superparent_y = getsuperparent(y); 

        // Set superparent of y as the 
        // parent of superparent of x 
        parent[superparent_x] = superparent_y; 

        // Update the maximum node 
        // in the component containing y 
        maximum_node[superparent_y] = Math.max( 
        maximum_node[superparent_y], 
        maximum_node[superparent_x]); 

        // Update the minimum node 
        // in the component containing y 
        minimum_node[superparent_y] = Math.min( 
        minimum_node[superparent_y], 
        minimum_node[superparent_x]); 
    } 
}; 

static dsu G = new dsu(); 

// Function to find the minimum number 
// of edges to be added to the Graph 
static int minimumEdgesToBeAdded(int n) 
{ 

    // Stores the answer 
    int answer = 0; 

    // Iterate over all nodes 
    for(int i = 0; i < n; i++) 
    { 

        // Get the superparent of 
        // the current node 
        int temp = G.getsuperparent(i); 

        // If the node is not visited 
        if (G.visited[temp] == 0) 
        { 

            // Set the node as visited 
            G.visited[temp] = 1; 

            // Iterate from the minimum 
            // value to maximum value in 
            // the current component 
            for(int j = G.minimum_node[temp]; 
                   j <= G.maximum_node[temp]; j++) 
            { 

                // If the nodes are in 
                // different components 
                if (G.getsuperparent(j) !=  
                    G.getsuperparent(i)) 
                { 

                    // Unite them 
                    G.unite(i, j); 

                    // Increment the answer 
                    answer++; 
                } 
            } 
        } 
    } 

    // Return the answer 
    return answer; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    int N = 7; 

    G.init(N); 

    // Insert edges 
    G.unite(1, 5); 
    G.unite(2, 4); 
    G.unite(3, 4); 

    System.out.print(minimumEdgesToBeAdded(N)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# program to implement 
// the above approach 
using System; 

class GFG{ 

//static readonly int MOD = 1000000007; 

// Disjoint Set Union 
class dsu 
{ 
    public dsu(){} 

    // Stores the parent 
    // of each node 
    public int[] parent; 

    // Storing maximum value 
    // in each component 
    public int[] maximum_node; 

    // Stores the minimum value 
    // in each component 
    public int[] minimum_node; 

    // Stores the visited nodes 
    public int[] visited; 

    // Function to initialize the 
    // values in vectors 
    public void init(int n) 
    { 

        // Initialize the size of 
        // vectors as n 
        parent = new int[n]; 
        maximum_node = new int[n]; 
        minimum_node = new int[n]; 
        visited = new int[n]; 

        for(int i = 0; i < n; i++) 
        { 

            // Initially every component 
            // has only one node 
            parent[i] = i; 
            maximum_node[i] = i; 
            minimum_node[i] = i; 

            // Mark unvisited 
            visited[i] = 0; 
        } 
    } 

    // Function to get identifier node 
    // (superparent) for each component 
    public int getsuperparent(int x) 
    { 

        // If parent of a node is that 
        // node itself then the node is 
        // superparent of that component 
        if(x == parent[x]) 
            return x; 
        else
        { 
            parent[x] = getsuperparent(parent[x]); 
            return parent[x]; 
        } 
    } 

    // Function to perform union of two 
    // different components 
    public void unite(int x, int y) 
    { 
        int superparent_x = getsuperparent(x); 
        int superparent_y = getsuperparent(y); 

        // Set superparent of y as the 
        // parent of superparent of x 
        parent[superparent_x] = superparent_y; 

        // Update the maximum node 
        // in the component containing y 
        maximum_node[superparent_y] = Math.Max( 
        maximum_node[superparent_y], 
        maximum_node[superparent_x]); 

        // Update the minimum node 
        // in the component containing y 
        minimum_node[superparent_y] = Math.Min( 
        minimum_node[superparent_y], 
        minimum_node[superparent_x]); 
    } 
}; 

static dsu G = new dsu(); 

// Function to find the minimum number 
// of edges to be added to the Graph 
static int minimumEdgesToBeAdded(int n) 
{ 

    // Stores the answer 
    int answer = 0; 

    // Iterate over all nodes 
    for(int i = 0; i < n; i++) 
    { 

        // Get the superparent of 
        // the current node 
        int temp = G.getsuperparent(i); 

        // If the node is not visited 
        if (G.visited[temp] == 0) 
        { 

            // Set the node as visited 
            G.visited[temp] = 1; 

            // Iterate from the minimum 
            // value to maximum value in 
            // the current component 
            for(int j = G.minimum_node[temp]; 
                   j <= G.maximum_node[temp]; j++) 
            { 

                // If the nodes are in 
                // different components 
                if (G.getsuperparent(j) !=  
                    G.getsuperparent(i)) 
                { 

                    // Unite them 
                    G.unite(i, j); 

                    // Increment the answer 
                    answer++; 
                } 
            } 
        } 
    } 

    // Return the answer 
    return answer; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    int N = 7; 

    G.init(N); 

    // Insert edges 
    G.unite(1, 5); 
    G.unite(2, 4); 
    G.unite(3, 4); 

    Console.Write(minimumEdgesToBeAdded(N)); 
} 
} 

// This code is contributed by Rajput-Ji

```

**Output:** 

```
1

```

***时间复杂度**：O（N），其中 N 是图中的节点数。*

***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。