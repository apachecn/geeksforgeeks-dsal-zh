# 打印奇数节点和偶数节点的级别

> 原文:[https://www . geesforgeks . org/print-levels-带奇数节点和偶数节点/](https://www.geeksforgeeks.org/print-levels-with-odd-number-of-nodes-and-even-number-of-nodes/)

给定一个 **N 元**树，打印所有节点数为奇数和偶数的级别。

**示例**:

```
For example consider the following tree
          1               - Level 1
       /     \
      2       3           - Level 2
    /   \       \
   4     5       6        - Level 3
        /  \     /
       7    8   9         - Level 4

The levels with odd number of nodes are: 1 3 4 
The levels with even number of nodes are: 2
```

**注**:级别号从 1 开始。也就是说，根节点处于级别 1。

**接近**:

*   将所有连接节点插入二维向量树。
*   在树上运行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，使高度【节点】= 1 +高度【父节点】
*   完成 DFS 遍历后，对于每个节点的级别，将 count[]数组增加 1。
*   从第一级迭代到最后一级，将 count[]值为奇数的所有节点打印出来，得到奇数个节点的级别。
*   从第一级迭代到最后一级，将 count[]值为偶数的所有节点打印出来，得到偶数个节点的级别。

下面是上述方法的实现:

## C++

```
// C++ program to print all levels
// with odd and even number of nodes

#include <bits/stdc++.h>
using namespace std;

// Function for DFS in a tree
void dfs(int node, int parent, int height[], int vis[],
         vector<int> tree[])
{
    // calculate the level of every node
    height[node] = 1 + height[parent];

    // mark every node as visited
    vis[node] = 1;

    // iterate in the subtree
    for (auto it : tree[node]) {

        // if the node is not visited
        if (!vis[it]) {

            // call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
void insertEdges(int x, int y, vector<int> tree[])
{
    tree[x].push_back(y);
    tree[y].push_back(x);
}

// Function to print all levels
void printLevelsOddEven(int N, int vis[], int height[])
{
    int mark[N + 1];
    memset(mark, 0, sizeof mark);

    int maxLevel = 0;
    for (int i = 1; i <= N; i++) {

        // count number of nodes
        // in every level
        if (vis[i])
            mark[height[i]]++;

        // find the maximum height of tree
        maxLevel = max(height[i], maxLevel);
    }

    // print odd number of nodes
    cout << "The levels with odd number of nodes are: ";
    for (int i = 1; i <= maxLevel; i++) {
        if (mark[i] % 2)
            cout << i << " ";
    }

    // print even number of nodes
    cout << "\nThe levels with even number of nodes are: ";
    for (int i = 1; i <= maxLevel; i++) {
        if (mark[i] % 2 == 0)
            cout << i << " ";
    }
}

// Driver Code
int main()
{
    // Construct the tree

    /*   1
       /   \
      2     3
     / \     \
    4    5    6
        / \  /
       7   8 9  */

    const int N = 9;

    vector<int> tree[N + 1];

    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int height[N + 1];
    int vis[N + 1] = { 0 };

    height[0] = 0;

    // call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelsOddEven(N, vis, height);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all levels
// with odd and even number of nodes
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

// Function for DFS in a tree
static void dfs(int node, int parent,
                int []height, int []vis,
                ArrayList []tree)
{

    // Calculate the level of every node
    height[node] = 1 + height[parent];

    // Mark every node as visited
    vis[node] = 1;

    // Iterate in the subtree
    for(int it : (ArrayList<Integer>)tree[node])
    {

        // If the node is not visited
        if (vis[it] == 0)
        {

            // Call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
static void insertEdges(int x, int y,
                        ArrayList []tree)
{
    tree[x].add(y);
    tree[y].add(x);
}

// Function to print all levels
static void printLevelsOddEven(int N, int []vis,
                               int []height)
{
    int []mark = new int[N + 1];
    Arrays.fill(mark, 0);
    int maxLevel = 0;

    for(int i = 1; i <= N; i++)
    {

        // Count number of nodes
        // in every level
        if (vis[i] != 0)
            mark[height[i]]++;

        // Find the maximum height of tree
        maxLevel = Math.max(height[i], maxLevel);
    }

    // Print odd number of nodes
    System.out.print("The levels with odd " +
                     "number of nodes are: ");

    for(int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] % 2 != 0)
        {
            System.out.print(i + " ");
        }
    }

    // Print even number of nodes
    System.out.print("\nThe levels with even " +
                     "number of nodes are: ");

    for(int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] % 2 == 0)
        {
            System.out.print(i + " ");
        }
    }
}

// Driver code 
public static void main(String []s)
{

    // Construct the tree

    /*   1
       /   \
      2     3
     / \     \
    4    5    6
        / \  /
       7   8 9  */

    int N = 9;

    ArrayList []tree = new ArrayList[N + 1];

    for(int i = 0; i < N + 1; i++)
    {
        tree[i] = new ArrayList();
    }

    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int []height = new int[N + 1];
    int []vis = new int[N + 1];
    Arrays.fill(vis, 0);

    height[0] = 0;

    // Call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelsOddEven(N, vis, height);
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to print all levels
# with odd and even number of nodes

# Function for DFS in a tree
def dfs(node, parent, height, vis, tree):

    # calculate the level of every node
    height[node] = 1 + height[parent]

    # mark every node as visited
    vis[node] = 1

    # iterate in the subtree
    for it in tree[node]:

        # if the node is not visited
        if not vis[it]:

            # call the dfs function
            dfs(it, node, height, vis, tree)

# Function to insert edges
def insertEdges(x, y, tree):

    tree[x].append(y)
    tree[y].append(x)

# Function to print all levels
def printLevelsOddEven(N, vis, height):

    mark = [0] * (N + 1)

    maxLevel = 0
    for i in range(1, N + 1):

        # count number of nodes in every level
        if vis[i]:
            mark[height[i]] += 1

        # find the maximum height of tree
        maxLevel = max(height[i], maxLevel)

    # print odd number of nodes
    print("The levels with odd number",
          "of nodes are: ", end = "")
    for i in range(1, maxLevel + 1):
        if mark[i] % 2:
            print(i, end = " ")

    # print even number of nodes
    print("\nThe levels with even number",
          "of nodes are: ", end = "")
    for i in range(1, maxLevel + 1):
        if mark[i] % 2 == 0:
            print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    # Construct the tree
    N = 9
    tree = [[] for i in range(N + 1)]

    insertEdges(1, 2, tree)
    insertEdges(1, 3, tree)
    insertEdges(2, 4, tree)
    insertEdges(2, 5, tree)
    insertEdges(5, 7, tree)
    insertEdges(5, 8, tree)
    insertEdges(3, 6, tree)
    insertEdges(6, 9, tree)

    height = [0] * (N + 1)
    vis = [0] * (N + 1)

    # call the dfs function
    dfs(1, 0, height, vis, tree)

    # Function to print
    printLevelsOddEven(N, vis, height)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to print all levels
// with odd and even number of nodes
using System;
using System.Collections;

class GFG{

// Function for DFS in a tree
static void dfs(int node, int parent,
                int []height, int []vis,
                ArrayList []tree)
{

    // Calculate the level of every node
    height[node] = 1 + height[parent];

    // Mark every node as visited
    vis[node] = 1;

    // Iterate in the subtree
    foreach (int it in tree[node])
    {

        // If the node is not visited
        if (vis[it] == 0)
        {

            // Call the dfs function
            dfs(it, node, height, vis, tree);
        }
    }
}

// Function to insert edges
static void insertEdges(int x, int y,
                        ArrayList []tree)
{
    tree[x].Add(y);
    tree[y].Add(x);
}

// Function to print all levels
static void printLevelsOddEven(int N, int []vis,
                               int []height)
{
    int []mark = new int[N + 1];
    Array.Fill(mark, 0);

    int maxLevel = 0;
    for(int i = 1; i <= N; i++)
    {

        // Count number of nodes
        // in every level
        if (vis[i] != 0)
            mark[height[i]]++;

        // Find the maximum height of tree
        maxLevel = Math.Max(height[i], maxLevel);
    }

    // Print odd number of nodes
    Console.Write("The levels with odd " +
                  "number of nodes are: ");

    for(int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] % 2 != 0)
        {
            Console.Write(i + " ");
        }
    }

    // Print even number of nodes
    Console.Write("\nThe levels with even " +
                  "number of nodes are: ");

    for(int i = 1; i <= maxLevel; i++)
    {
        if (mark[i] % 2 == 0)
        {
            Console.Write(i + " ");
        }
    }
}

// Driver code 
static void Main()
{

    // Construct the tree

    /*   1
       /   \
      2     3
     / \     \
    4    5    6
        / \  /
       7   8 9  */

    int N = 9;

    ArrayList []tree = new ArrayList[N + 1];

    for(int i = 0; i < N + 1; i++)
    {
        tree[i] = new ArrayList();
    }

    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    int []height = new int[N + 1];
    int []vis = new int[N + 1];
    Array.Fill(vis, 0);

    height[0] = 0;

    // Call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelsOddEven(N, vis, height);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

    // JavaScript program to print all levels
    // with odd and even number of nodes

    // Function for DFS in a tree
    function dfs(node, parent, height, vis, tree)
    {

        // Calculate the level of every node
        height[node] = 1 + height[parent];

        // Mark every node as visited
        vis[node] = 1;

        // Iterate in the subtree
        for(let it = 0; it < tree[node].length; it++)
        {

            // If the node is not visited
            if (vis[tree[node][it]] == 0)
            {

                // Call the dfs function
                dfs(tree[node][it], node, height, vis, tree);
            }
        }
    }

    // Function to insert edges
    function insertEdges(x, y, tree)
    {
        tree[x].push(y);
        tree[y].push(x);
    }

    // Function to print all levels
    function printLevelsOddEven(N, vis, height)
    {
        let mark = new Array(N + 1);
        mark.fill(0);
        let maxLevel = 0;

        for(let i = 1; i <= N; i++)
        {

            // Count number of nodes
            // in every level
            if (vis[i] != 0)
                mark[height[i]]++;

            // Find the maximum height of tree
            maxLevel = Math.max(height[i], maxLevel);
        }

        // Print odd number of nodes
        document.write("The levels with odd " +
                         "number of nodes are: ");

        for(let i = 1; i <= maxLevel; i++)
        {
            if (mark[i] % 2 != 0)
            {
                document.write(i + " ");
            }
        }

        // Print even number of nodes
        document.write("</br>" + "The levels with even " +
                         "number of nodes are: ");

        for(let i = 1; i <= maxLevel; i++)
        {
            if (mark[i] % 2 == 0)
            {
                document.write(i + " ");
            }
        }
    }

    // Construct the tree

    /*   1
       /   \
      2     3
     / \     \
    4    5    6
        / \  /
       7   8 9  */

    let N = 9;

    let tree = new Array(N + 1);

    for(let i = 0; i < N + 1; i++)
    {
        tree[i] = [];
    }

    insertEdges(1, 2, tree);
    insertEdges(1, 3, tree);
    insertEdges(2, 4, tree);
    insertEdges(2, 5, tree);
    insertEdges(5, 7, tree);
    insertEdges(5, 8, tree);
    insertEdges(3, 6, tree);
    insertEdges(6, 9, tree);

    let height = new Array(N + 1);
    let vis = new Array(N + 1);
    vis.fill(0);

    height[0] = 0;

    // Call the dfs function
    dfs(1, 0, height, vis, tree);

    // Function to print
    printLevelsOddEven(N, vis, height);

</script>
```

**Output:** 

```
The levels with odd number of nodes are: 1 3 4 
The levels with even number of nodes are: 2
```

**时间复杂度**:O(N)
T3】辅助空间 : O(N)