# 打印节点数为奇数和偶数的所有级别| Set-2

> 原文:[https://www . geeksforgeeks . org/print-所有具有奇数和偶数节点数的级别-it-set-2/](https://www.geeksforgeeks.org/print-all-the-levels-with-odd-and-even-number-of-nodes-in-it-set-2/)

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
*   在树上运行一个 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) ，使得高度【节点】= 1 +高度【父节点】
*   一旦 BFS 遍历完成，对于每个节点的级别，将 count[]数组增加 1。
*   从第一级迭代到最后一级，将 count[]值为奇数的所有节点打印出来，得到奇数个节点的级别。
*   从第一级迭代到最后一级，将 count[]值为偶数的所有节点打印出来，得到偶数个节点的级别。

下面是上述方法的实现:

## C++

```
// C++ program to print all levels
// with odd and even number of nodes

#include <bits/stdc++.h>
using namespace std;

// Function for BFS in a tree
void bfs(int node, int parent, int height[], int vis[],
         vector<int> tree[])
{

    // mark first node as visited
    vis[node] = 1;

    // Declare Queue
    queue<int> q;

    // Push the first element
    q.push(1);

    // calculate the level of every node
    height[node] = 1 + height[parent];

    // Check if the queue is empty or not
    while (!q.empty()) {

        // Get the top element in the queue
        int top = q.front();

        // pop the element
        q.pop();

        // mark as visited
        vis[top] = 1;

        // Iterate for the connected nodes
        for (int i = 0; i < tree[top].size(); i++) {

            // if not visited
            if (!vis[tree[top][i]]) {

                // Insert into queue
                q.push(tree[top][i]);

                // Increase level
                height[tree[top][i]] = 1 + height[top];
            }
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

    // call the bfs function
    bfs(1, 0, height, vis, tree);

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
public class Main
{
    // Function for BFS in a tree
    static void bfs(int node, int parent, int[] height, int[] vis, Vector<Vector<Integer>> tree)
    {
        // Mark first node as visited
        vis[node] = 1;

        // Declare Queue
        Queue<Integer> q = new LinkedList<>();

        // Push the first element
        q.add(1);

        // Calculate the level of every node
        height[node] = 1 + height[parent];

        // Check if the queue is empty or not
        while (q.size() != 0)
        {

            // Get the top element in the queue
            int top = (int)q.peek();

            // Pop the element
            q.remove();

            // Mark as visited
            vis[top] = 1;

            // Iterate for the connected nodes
            for(int i = 0; i < tree.get(top).size(); i++)
            {

                // If not visited
                if (vis[(int)tree.get(top).get(i)] == 0)
                {

                    // Insert into queue
                    q.add(tree.get(top).get(i));

                    // Increase level
                    height[(int)tree.get(top).get(i)] = 1 + height[top];
                }
            }
        }
    }

    // Function to insert edges
    static void insertEdges(int x, int y, Vector<Vector<Integer>> tree)
    {
        tree.get(x).add(y);
        tree.get(y).add(x);
    }

    // Function to print all levels
    static void printLevelsOddEven(int N, int[] vis, int[] height)
    {
        int[] mark = new int[N + 1];
        for(int i = 0; i < N + 1; i++)
        {
            mark[i] = 0;
        }

        int maxLevel = 0;
        for(int i = 1; i <= N; i++)
        {

            // Count number of nodes
            // in every level
            if (vis[i]!=0)
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

        // print even number of nodes
        System.out.println();
        System.out.print("The levels with even " +
                      "number of nodes are: ");

        for(int i = 1; i <= maxLevel; i++)
        {
            if (mark[i] % 2 == 0)
            {
                System.out.print(i + " ");
            }
        }
    }

    public static void main(String[] args) {
        // Construct the tree

        /*   1
           /   \
          2     3
         / \     \
        4    5    6
            / \  /
           7   8 9  */

        int N = 9;

        Vector<Vector<Integer>> tree = new Vector<Vector<Integer>>();

        for(int i = 0; i < N + 1; i++)
        {
            tree.add(new Vector<Integer>());
        }

        insertEdges(1, 2, tree);
        insertEdges(1, 3, tree);
        insertEdges(2, 4, tree);
        insertEdges(2, 5, tree);
        insertEdges(5, 7, tree);
        insertEdges(5, 8, tree);
        insertEdges(3, 6, tree);
        insertEdges(6, 9, tree);

        int[] height = new int[N + 1];
        int[] vis = new int[N + 1];
        for(int i = 0; i < N + 1; i++)
        {
            vis[i] = 0;
        }

        height[0] = 0;

        // Call the bfs function
        bfs(1, 0, height, vis, tree);

        // Function to print
        printLevelsOddEven(N, vis, height);
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program to print all levels
# with odd and even number of nodes

# Function for BFS in a tree
def bfs(node, parent, height, vis, tree):

    # mark first node as visited
    vis[node] = 1

    # Declare Queue
    q = []

    # append the first element
    q.append(1)

    # calculate the level of every node
    height[node] = 1 + height[parent]

    # Check if the queue is empty or not
    while (len(q)):

        # Get the top element in
        # the queue
        top = q[0]

        # pop the element
        q.pop(0)

        # mark as visited
        vis[top] = 1

        # Iterate for the connected nodes
        for i in range(len(tree[top])):

            # if not visited
            if (not vis[tree[top][i]]):

                # Insert into queue
                q.append(tree[top][i])

                # Increase level
                height[tree[top][i]] = 1 + height[top]

# Function to insert edges
def insertEdges(x, y, tree):

    tree[x].append(y)
    tree[y].append(x)

# Function to print all levels
def printLevelsOddEven(N, vis, height):

    mark = [0] * (N + 1)

    maxLevel = 0
    for i in range(1, N + 1):

        # count number of nodes
        # in every level
        if (vis[i]) :
            mark[height[i]] += 1

        # find the maximum height of tree
        maxLevel = max(height[i], maxLevel)

    # prodd number of nodes
    print("The levels with odd number",
          "of nodes are:", end = " ")
    for i in range(1, maxLevel + 1):
        if (mark[i] % 2):
            print(i, end = " " )

    # print even number of nodes
    print("\nThe levels with even number",
            "of nodes are:", end = " ")
    for i in range(1, maxLevel ):
        if (mark[i] % 2 == 0):
            print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    # Construct the tree
    """ 1
    / \
    2 3
    / \ \
    4 5 6
        / \ /
    7 8 9 """

    N = 9

    tree = [[0]] * (N + 1)

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

    # call the bfs function
    bfs(1, 0, height, vis, tree)

    # Function to pr
    printLevelsOddEven(N, vis, height)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to print all levels
// with odd and even number of nodes
using System;
using System.Collections;

class GFG{

// Function for BFS in a tree
static void bfs(int node, int parent,
                int []height, int []vis,
                ArrayList []tree)
{

    // Mark first node as visited
    vis[node] = 1;

    // Declare Queue
    Queue q = new Queue();

    // Push the first element
    q.Enqueue(1);

    // Calculate the level of every node
    height[node] = 1 + height[parent];

    // Check if the queue is empty or not
    while (q.Count != 0)
    {

        // Get the top element in the queue
        int top = (int)q.Peek();

        // Pop the element
        q.Dequeue();

        // Mark as visited
        vis[top] = 1;

        // Iterate for the connected nodes
        for(int i = 0; i < tree[top].Count; i++)
        {

            // If not visited
            if (vis[(int)tree[top][i]] == 0)
            {

                // Insert into queue
                q.Enqueue(tree[top][i]);

                // Increase level
                height[(int)tree[top][i]] = 1 + height[top];
            }
        }
    }
}

// Function to insert edges
static void insertEdges(int x, int y, ArrayList []tree)
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
        if (vis[i]!=0)
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

    // print even number of nodes
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

    // Call the bfs function
    bfs(1, 0, height, vis, tree);

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

    // Function for BFS in a tree
    function bfs(node, parent, height, vis, tree)
    {

        // Mark first node as visited
        vis[node] = 1;

        // Declare Queue
        let q = [];

        // Push the first element
        q.push(1);

        // Calculate the level of every node
        height[node] = 1 + height[parent];

        // Check if the queue is empty or not
        while (q.length != 0)
        {

            // Get the top element in the queue
            let top = q[0];

            // Pop the element
            q.shift();

            // Mark as visited
            vis[top] = 1;

            // Iterate for the connected nodes
            for(let i = 0; i < tree[top].length; i++)
            {

                // If not visited
                if (vis[tree[top][i]] == 0)
                {

                    // Insert into queue
                    q.push(tree[top][i]);

                    // Increase level
                    height[tree[top][i]] = 1 + height[top];
                }
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
            if (vis[i]!=0)
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

        // print even number of nodes
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

    // Call the bfs function
    bfs(1, 0, height, vis, tree);

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