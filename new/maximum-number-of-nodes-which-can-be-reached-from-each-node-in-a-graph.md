# 从图中的每个节点可以到达的最大节点数。

> 原文： [https://www.geeksforgeeks.org/maximum-number-of-nodes-which-can-be-reached-from-each-node-in-a-graph/](https://www.geeksforgeeks.org/maximum-number-of-nodes-which-can-be-reached-from-each-node-in-a-graph/)

给定一个具有 N 个节点和它们之间的 K 个双向边的图，可以找到特定节点可到达的节点数。 如果我们可以使用任意数量的边在 X 处开始并在 Y 处结束，则可以说两个节点 X 和 Y 是可到达的。

**注意：节点自身可达。**

```
Input : N = 7
       1            5
        \          / \
         2        6 __ 7
          \  
           3
            \
             4

Output :4 4 4 4 3 3 3 
From node 1 ,nodes {1,2,3,4} can be visited
hence the answer is equal to 4
From node 5,nodes {5,6,7} can be visited.
hence the answer is equal to 3.
Similarly, print the count for every node.

Input : N = 8
      1              7
    /   \             \
   2     3              8   
    \   / \
      5    6
Output :6 6 6 6 6 6 2 2
```

**方法**：

要查找从特定节点可到达的节点数，要观察的一件事是，只有当节点 X 位于相同连通组件中时，我们才能从节点 X 到达节点 Y。

由于该图是双向的，因此连通组件中的任何节点都与同一连通组件中的其他任何节点相同。 因此，对于特定的节点 X，可到达的节点数将是该特定组件中的节点数。使用深度优先搜索来找到答案。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
const int maxx = 100005;
vector<int> graph[maxx];

// Function to perform the DFS calculating the 
// count of the elements in a connected component
void dfs(int curr, int& cnt, int* 
             visited, vector<int>& duringdfs)
{
    visited[curr] = 1;

    // Number of nodes in this component
    ++cnt;

    // Stores the nodes which belong 
    // to current component
    duringdfs.push_back(curr);
    for (auto& child : graph[curr]) {

        // If the child is not visited
        if (visited[child] == 0) {
            dfs(child, cnt, visited, duringdfs);
        }
    }
}

// Function to return the desired 
// count for every node in the graph
void MaximumVisit(int n, int k)
{
    // To keep track of nodes we visit
    int visited[maxx];

    // Mark every node unvisited
    memset(visited, 0, sizeof visited);
    int ans[maxx];

    // No of connected elements for each node
    memset(ans, 0, sizeof ans);
    vector<int> duringdfs; 
    for (int i = 1; i <= n; ++i) {
        duringdfs.clear();
        int cnt = 0;

        // If a node is not visited, perform a DFS as 
        // this node belongs to a different component
        // which is not yet visited
        if (visited[i] == 0) {
            cnt = 0;
            dfs(i, cnt, visited, duringdfs);
        }

        // Now store the count of all the visited
        // nodes for any particular component.
        for (auto& x : duringdfs) {
            ans[x] = cnt;
        }
    }

    // Print the result
    for (int i = 1; i <= n; ++i) {
        cout << ans[i] << " ";
    }
    cout << endl;
    return;
}

// Function to build the graph
void MakeGraph(){
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[2].push_back(3);
    graph[3].push_back(2);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[5].push_back(6);
    graph[6].push_back(5);
    graph[6].push_back(7);
    graph[7].push_back(6);
    graph[5].push_back(7);
    graph[7].push_back(5);
}

// Driver code
int main()
{
    int N = 7, K = 6;

    // Build the graph
    MakeGraph();

    MaximumVisit(N, K);
    return 0;
}

```

## Java

```java

// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG
{

    static final int maxx = 100005;
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] graph = new Vector[maxx];
    static Vector<Integer> duringdfs = new Vector<>();
    static int cnt = 0;

    // Function to perform the DFS calculating the
    // count of the elements in a connected component
    static void dfs(int curr, int[] visited) 
    {
        visited[curr] = 1;

        // Number of nodes in this component
        ++cnt;

        // Stores the nodes which belong
        // to current component
        duringdfs.add(curr);
        for (int child : graph[curr])
        {

            // If the child is not visited
            if (visited[child] == 0)
                dfs(child, visited);
        }
    }

    // Function to return the desired
    // count for every node in the graph
    static void maximumVisit(int n, int k)
    {

        // To keep track of nodes we visit
        int[] visited = new int[maxx];

        // Mark every node unvisited
        Arrays.fill(visited, 0);

        int[] ans = new int[maxx];

        // No of connected elements for each node
        Arrays.fill(ans, 0);

        for (int i = 1; i <= n; i++)
        {
            duringdfs.clear();

            // If a node is not visited, perform a DFS as
            // this node belongs to a different component
            // which is not yet visited
            if (visited[i] == 0) 
            {
                cnt = 0;
                dfs(i, visited);
            }

            // Now store the count of all the visited
            // nodes for any particular component.
            for (int x : duringdfs)
                ans[x] = cnt;
        }

        // Print the result
        for (int i = 1; i <= n; i++)
            System.out.print(ans[i] + " ");
        System.out.println();
        return;
    }

    // Function to build the graph
    static void makeGraph()
    {
        // Initializing graph
        for (int i = 0; i < maxx; i++)
            graph[i] = new Vector<>();

        graph[1].add(2);
        graph[2].add(1);
        graph[2].add(3);
        graph[3].add(2);
        graph[3].add(4);
        graph[4].add(3);
        graph[5].add(6);
        graph[6].add(5);
        graph[6].add(7);
        graph[7].add(6);
        graph[5].add(7);
        graph[7].add(5);
    }

    // Driver Code
    public static void main(String[] args) 
    {
        int N = 7, K = 6;

        // Build the graph
        makeGraph();

        maximumVisit(N, K);
    }
}

// This code is contributed by
// sanjeev2552

```

## Python

```py

# Python3 implementation of the above approach 
maxx = 100005
graph = [[] for i in range(maxx)]

# Function to perform the DFS calculating the  
# count of the elements in a connected component 
def dfs(curr, cnt, visited, duringdfs):

    visited[curr] = 1

    # Number of nodes in this component 
    cnt += 1

    # Stores the nodes which belong  
    # to current component 
    duringdfs.append(curr)

    for child in graph[curr]:

        # If the child is not visited 
        if (visited[child] == 0):
            cnt, duringdfs = dfs(child, cnt, 
                                 visited, duringdfs)

    return cnt, duringdfs

# Function to return the desired  
# count for every node in the graph 
def MaximumVisit(n, k):

    # To keep track of nodes we visit 
    visited = [0 for i in range(maxx)]

    ans = [0 for i in range(maxx)]

    duringdfs = []

    for i in range(1, n + 1):
        duringdfs.clear()

        cnt = 0

        # If a node is not visited, perform a DFS as  
        # this node belongs to a different component 
        # which is not yet visited 
        if (visited[i] == 0):
            cnt = 0
            cnt, duringdfs = dfs(i, cnt, 
                                 visited, duringdfs)

        # Now store the count of all the visited 
        # nodes for any particular component. 
        for x in duringdfs:
            ans[x] = cnt

    # Print the result 
    for i in range(1, n + 1):
        print(ans[i], end = ' ')

    print()

    return

# Function to build the graph 
def MakeGraph():

    graph[1].append(2)
    graph[2].append(1) 
    graph[2].append(3) 
    graph[3].append(2) 
    graph[3].append(4) 
    graph[4].append(3) 
    graph[5].append(6) 
    graph[6].append(5) 
    graph[6].append(7) 
    graph[7].append(6) 
    graph[5].append(7) 
    graph[7].append(5) 

# Driver code 
if __name__=='__main__':

    N = 7
    K = 6

    # Build the graph 
    MakeGraph()

    MaximumVisit(N, K)

# This code is contributed by rutvik_56

```

**Output:** 

```
4 4 4 4 3 3 3
```

**时间复杂度**：`O(N)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。