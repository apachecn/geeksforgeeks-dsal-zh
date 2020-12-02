# 使用拓扑排序

在有向图中检测循环

> 原文： [https://www.geeksforgeeks.org/detect-cycle-in-directed-graph-using-topological-sort/](https://www.geeksforgeeks.org/detect-cycle-in-directed-graph-using-topological-sort/)

给定一个**有向图**，该图由 **N 个**顶点和 **M 个**边缘以及一组 **Edges [] []** 组成 图形是否使用[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)来包含循环。

> 有向图的拓扑排序是其顶点的线性排序，这样，对于从顶点`U`到顶点`V`的每个**有向边 U-> V** ， **在订购中，U 在 V** 之前。

**示例**：

> **输入**：N = 4，M = 6，边线[] [] = {{0，1}，{1，2}，{2，0}，{0，2}，{2， 3}，{3，3}}
> **输出**：是
> **说明**：
> 一个周期 **0-> 2-> 给定图中存在 0**
> 
> **输入**：N = 4，M = 3，Edges [] [] = {{0，1}，{1，2}，{2，3}，{0，2}}}
> **输出**：否

**方法**：
在**拓扑排序**中，想法是先访问**父节点**，再访问**子节点**。 如果给定的图包含**周期**，则至少有**个节点**是父级也是子级，因此这将破坏**拓扑顺序**。 因此，在**拓扑排序**之后，检查每个**有向边**是否遵循该顺序。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

int t, n, m, a;

// Stack to store the
// visited vertices in
// the Topological Sort
stack<int> s;

// Store Topological Order
vector<int> tsort;

// Adjacency list to store edges
vector<int> adj[int(1e5) + 1];

// To ensure visited vertex
vector<int> visited(int(1e5) + 1);

// Function to perform DFS
void dfs(int u)
{
    // Set the vertex as visited
    visited[u] = 1;

    for (auto it : adj[u]) {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    }

    // Push into the stack on
    // complete visit of vertex
    s.push(u);
}

// Function to check and return
// if a cycle exists or not
bool check_cycle()
{
    // Stores the position of
    // vertex in topological order
    unordered_map<int, int> pos;
    int ind = 0;

    // Pop all elements from stack
    while (!s.empty()) {
        pos[s.top()] = ind;

        // Push element to get
        // Topological Order
        tsort.push_back(s.top());

        ind += 1;

        // Pop from the stack
        s.pop();
    }

    for (int i = 0; i < n; i++) {
        for (auto it : adj[i]) {

            // If parent vertex
            // does not appear first
            if (pos[i] > pos[it]) {

                // Cycle exists
                return true;
            }
        }
    }

    // Return false if cycle
    // does not exist
    return false;
}

// Function to add edges
// from u to v
void addEdge(int u, int v)
{
    adj[u].push_back(v);
}

// Driver Code
int main()
{
    n = 4, m = 5;

    // Insert edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 0);
    addEdge(2, 3);

    for (int i = 0; i < n; i++) {
        if (visited[i] == 0) {
            dfs(i);
        }
    }

    // If cycle exist
    if (check_cycle())
        cout << "Yes";
    else
        cout << "No";

    return 0;
}

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*;

class GFG{

static int t, n, m, a;

// Stack to store the
// visited vertices in
// the Topological Sort
static Stack<Integer> s;

// Store Topological Order
static ArrayList<Integer> tsort;

// Adjacency list to store edges
static ArrayList<ArrayList<Integer>> adj;

// To ensure visited vertex
static int[] visited = new int[(int)1e5 + 1];

// Function to perform DFS
static void dfs(int u)
{

    // Set the vertex as visited
    visited[u] = 1;

    for(Integer it : adj.get(u))
    {

        // Visit connected vertices
        if (visited[it] == 0)
            dfs(it);
    }

    // Push into the stack on
    // complete visit of vertex
    s.push(u);
}

// Function to check and return
// if a cycle exists or not
static boolean check_cycle()
{

    // Stores the position of
    // vertex in topological order
    Map<Integer, Integer> pos = new HashMap<>();

    int ind = 0;

    // Pop all elements from stack
    while (!s.isEmpty()) 
    {
        pos.put(s.peek(), ind);

        // Push element to get
        // Topological Order
        tsort.add(s.peek());

        ind += 1;

        // Pop from the stack
        s.pop();
    }

    for(int i = 0; i < n; i++) 
    {
        for(Integer it : adj.get(i))
        {

            // If parent vertex
            // does not appear first
            if (pos.get(i) > pos.get(it))
            {

                // Cycle exists
                return true;
            }
        }
    }

    // Return false if cycle
    // does not exist
    return false;
}

// Function to add edges
// from u to v
static void addEdge(int u, int v)
{
    adj.get(u).add(v);
}

// Driver code    
public static void main (String[] args)
{
    n = 4; m = 5;

    s = new Stack<>();
    adj = new ArrayList<>();
    tsort = new ArrayList<>();

    for(int i = 0; i < 4; i++)
        adj.add(new ArrayList<>());

    // Insert edges
    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 0);
    addEdge(2, 3);

    for(int i = 0; i < n; i++)
    {
        if (visited[i] == 0) 
        {
            dfs(i);
        }
    }

    // If cycle exist
    if (check_cycle())
       System.out.println("Yes");
    else
       System.out.println("No");
}
}

// This code is contributed by offbeat

```

## Python

```py

# Python3 program to implement
# the above approach
t = 0
n = 0
m = 0
a = 0

# Stack to store the
# visited vertices in
# the Topological Sort
s = []

# Store Topological Order
tsort = []

# Adjacency list to store edges
adj = [[] for i in range(100001)]

# To ensure visited vertex
visited = [False for i in range(100001)]

# Function to perform DFS
def dfs(u):

    # Set the vertex as visited
    visited[u] = 1

    for it in adj[u]:

        # Visit connected vertices
        if (visited[it] == 0):
            dfs(it)

    # Push into the stack on
    # complete visit of vertex
    s.append(u)

# Function to check and return
# if a cycle exists or not
def check_cycle():

    # Stores the position of
    # vertex in topological order
    pos = dict()

    ind = 0

    # Pop all elements from stack
    while (len(s) != 0):
        pos[s[-1]] = ind

        # Push element to get
        # Topological Order
        tsort.append(s[-1])

        ind += 1

        # Pop from the stack
        s.pop()

    for i in range(n):
        for it in adj[i]:
            first = 0 if i not in pos else pos[i]
            second = 0 if it not in pos else pos[it]

            # If parent vertex
            # does not appear first
            if (first > second):

                # Cycle exists
                return True

    # Return false if cycle
    # does not exist
    return False

# Function to add edges
# from u to v
def addEdge(u, v):

    adj[u].append(v)

# Driver Code
if __name__ == "__main__":

    n = 4
    m = 5

    # Insert edges
    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 2)
    addEdge(2, 0)
    addEdge(2, 3)

    for i in range(n):
        if (visited[i] == False):
            dfs(i)

    # If cycle exist
    if (check_cycle()):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik_56

```

**Output:** 

```
Yes

```

***时间复杂度**：O（N + M）*
***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。