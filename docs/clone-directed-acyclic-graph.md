# 克隆有向无环图

> 原文:[https://www.geeksforgeeks.org/clone-directed-acyclic-graph/](https://www.geeksforgeeks.org/clone-directed-acyclic-graph/)

有向无环图是一种不包含循环且有向边的图。我们被赋予一个 DAG，我们需要克隆它，即创建另一个图形，它的顶点和边的副本连接它们。

示例:

```
Input :

0 - - - > 1 - - - -> 4
|        /  \        ^   
|       /    \       |  
|      /      \      |
|     /        \     |  
|    /          \    |
|   /            \   |
v  v              v  |
2 - - - - - - - - -> 3

Output : Printing the output of the cloned graph gives: 
0-1
1-2
2-3
3-4
1-3
1-4
0-2
```

克隆一个 DAG，而不将图本身存储在散列(或 Python 中的字典)中。为了克隆它，我们基本上对节点进行深度优先遍历，取原始节点的值并用相同的值初始化新的相邻节点，递归进行，直到原始图被完全遍历。下面是克隆 DAG 的递归方法(在 Python 中)。我们利用 Python 中的动态列表，对该列表的追加操作在恒定时间内发生，从而快速高效地初始化图形。

## C++14

```
// C++ program to clone a directed acyclic graph.
#include <bits/stdc++.h>
using namespace std;

// Class to create a new graph node
class Node
{
    public:
        int key;
        vector<Node *> adj;

        // key is the value of the node
        // adj will be holding a dynamic
        // list of all Node type neighboring
        // nodes
        Node(int key)
        {
            this->key = key;
        }
};

// Function to print a graph,
// depth-wise, recursively
void printGraph(Node *startNode,
                vector<bool> &visited)
{

    // Visit only those nodes who have any
    // neighboring nodes to be traversed
    if (!startNode->adj.empty())
    {

        // Loop through the neighboring nodes
        // of this node. If source node not already
        // visited, print edge from source to
        // neighboring nodes. After visiting all
        // neighbors of source node, mark its visited
        // flag to true
        for(auto i : startNode->adj)
        {
            if (!visited[startNode->key])
            {
                cout << "edge " << startNode
                     << "-" << i
                     << ":" << startNode->key
                     << "-" << i->key
                     << endl;
                if (!visited[i->key])
                {
                    printGraph(i, visited);
                    visited[i->key] = true;
                }
            }
        }
    }
}

// Function to clone a graph. To do this, we
// start reading the original graph depth-wise,
// recursively. If we encounter an unvisited
// node in original graph, we initialize a
// new instance of Node for cloned graph with
// key of original node
Node *cloneGraph(Node *oldSource,
                 Node *newSource,
                 vector<bool> &visited)
{
    Node *clone = NULL;

    if (!visited[oldSource->key] &&
        !oldSource->adj.empty())
    {
        for(auto old : oldSource->adj)
        {

            // Below check is for backtracking, so new
            // nodes don't get initialized everytime
            if (clone == NULL ||
               (clone != NULL &&
               clone->key != old->key))
                clone = new Node(old->key);

            newSource->adj.push_back(clone);
            cloneGraph(old, clone, visited);

            // Once, all neighbors for that particular node
            // are created in cloned graph, code backtracks
            // and exits from that node, mark the node as
            // visited in original graph, and traverse the
            // next unvisited
            visited[old->key] = true;
        }
    }
    return newSource;
}

// Driver Code
int main()
{
    Node *n0 = new Node(0);
    Node *n1 = new Node(1);
    Node *n2 = new Node(2);
    Node *n3 = new Node(3);
    Node *n4 = new Node(4);

    n0->adj.push_back(n1);
    n0->adj.push_back(n2);
    n1->adj.push_back(n2);
    n1->adj.push_back(n3);
    n1->adj.push_back(n4);
    n2->adj.push_back(n3);
    n3->adj.push_back(n4);

    // Flag to check if a node is already visited.
    // Stops indefinite looping during recursion
    vector<bool> visited(5, false);
    cout << "Graph Before Cloning:-\n";
    printGraph(n0, visited);
    visited = { false, false, false, false, false };

    cout << "\nGraph Before Starts:-\n";
    Node *clonedGraphHead = cloneGraph(
        n0, new Node(n0->key), visited);
    cout << "Cloning Process Completes.\n";

    visited = { false, false, false, false, false };
    cout << "\nGraph After Cloning:-\n";
    printGraph(clonedGraphHead, visited);

    return 0;
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to clone a directed acyclic graph.
import java.util.*;

class GFG{

// Class to create a new graph node
static class Node
{
    int key;
    ArrayList<Node> adj = new ArrayList<Node>();

    // key is the value of the node
    // adj will be holding a dynamic
    // list of all Node type neighboring
    // nodes
    Node(int key)
    {
        this.key = key;
    }
}

// Function to print a graph,
// depth-wise, recursively
static void printGraph(Node startNode,
                       boolean[] visited)
{

    // Visit only those nodes who have any
    // neighboring nodes to be traversed
    if (!startNode.adj.isEmpty())
    {

        // Loop through the neighboring nodes
        // of this node. If source node not already
        // visited, print edge from source to
        // neighboring nodes. After visiting all
        // neighbors of source node, mark its visited
        // flag to true
        for(Node i : startNode.adj)
        {
            if (!visited[startNode.key])
            {
                System.out.println("edge " + startNode +
                             "-" + i + ":" + startNode.key +
                             "-" + i.key);

                if (!visited[i.key])
                {
                    printGraph(i, visited);
                    visited[i.key] = true;
                }
            }
        }
    }
}

// Function to clone a graph. To do this, we
// start reading the original graph depth-wise,
// recursively. If we encounter an unvisited
// node in original graph, we initialize a
// new instance of Node for cloned graph with
// key of original node
static Node cloneGraph(Node oldSource,
                       Node newSource,
                       boolean[] visited)
{
    Node clone = null;

    if (!visited[oldSource.key] &&
        !oldSource.adj.isEmpty())
    {
        for(Node old : oldSource.adj)
        {

            // Below check is for backtracking, so new
            // nodes don't get initialized everytime
            if (clone == null ||
               (clone != null &&
                clone.key != old.key))
                clone = new Node(old.key);

            newSource.adj.add(clone);
            cloneGraph(old, clone, visited);

            // Once, all neighbors for that particular node
            // are created in cloned graph, code backtracks
            // and exits from that node, mark the node as
            // visited in original graph, and traverse the
            // next unvisited
            visited[old.key] = true;
        }
    }
    return newSource;
}

// Driver Code
public static void main(String[] args)
{
    Node n0 = new Node(0);
    Node n1 = new Node(1);
    Node n2 = new Node(2);
    Node n3 = new Node(3);
    Node n4 = new Node(4);

    n0.adj.add(n1);
    n0.adj.add(n2);
    n1.adj.add(n2);
    n1.adj.add(n3);
    n1.adj.add(n4);
    n2.adj.add(n3);
    n3.adj.add(n4);

    // Flag to check if a node is already visited.
    // Stops indefinite looping during recursion
    boolean visited[] = new boolean[5];
    System.out.println("Graph Before Cloning:-");
    printGraph(n0, visited);
    Arrays.fill(visited, false);

    System.out.println("\nCloning Process Starts");
    Node clonedGraphHead = cloneGraph(
        n0, new Node(n0.key), visited);
    System.out.println("Cloning Process Completes.");

    Arrays.fill(visited, false);
    System.out.println("\nGraph After Cloning:-");
    printGraph(clonedGraphHead, visited);
}
}

// This code is contributed by adityapande88
```

## 计算机编程语言

```
# Python program to clone a directed acyclic graph.

# Class to create a new graph node
class Node():

    # key is the value of the node
    # adj will be holding a dynamic
    # list of all Node type neighboring
    # nodes
    def __init__(self, key = None, adj = None):
        self.key = key
        self.adj = adj

# Function to print a graph, depth-wise, recursively
def printGraph(startNode, visited):

    # Visit only those nodes who have any
    # neighboring nodes to be traversed
    if startNode.adj is not None:

        # Loop through the neighboring nodes
        # of this node. If source node not already
        # visited, print edge from source to
        # neighboring nodes. After visiting all
        # neighbors of source node, mark its visited
        # flag to true
        for i in startNode.adj:
            if visited[startNode.key] == False :
                print("edge %s-%s:%s-%s"%(hex(id(startNode)), hex(id(i)), startNode.key, i.key))
                if visited[i.key] == False:
                    printGraph(i, visited)
                    visited[i.key] = True

# Function to clone a graph. To do this, we start
# reading the original graph depth-wise, recursively
# If we encounter an unvisited node in original graph,
# we initialize a new instance of Node for
# cloned graph with key of original node
def cloneGraph(oldSource, newSource, visited):
    clone = None
    if visited[oldSource.key] is False and oldSource.adj is not None:
        for old in oldSource.adj:

            # Below check is for backtracking, so new
            # nodes don't get initialized everytime
            if clone is None or(clone is not None and clone.key != old.key):
                clone = Node(old.key, [])
            newSource.adj.append(clone)
            cloneGraph(old, clone, visited)

            # Once, all neighbors for that particular node
            # are created in cloned graph, code backtracks
            # and exits from that node, mark the node as
            # visited in original graph, and traverse the
            # next unvisited
            visited[old.key] = True
    return newSource

# Creating DAG to be cloned
# In Python, we can do as many assignments of
# variables in one single line by using commas
n0, n1, n2 = Node(0, []), Node(1, []), Node(2, [])
n3, n4 = Node(3, []), Node(4)
n0.adj.append(n1)
n0.adj.append(n2)
n1.adj.append(n2)
n1.adj.append(n3)
n1.adj.append(n4)
n2.adj.append(n3)
n3.adj.append(n4)

# flag to check if a node is already visited.
# Stops indefinite looping during recursion
visited = [False]* (5)
print("Graph Before Cloning:-")
printGraph(n0, visited)

visited = [False]* (5)
print("\nCloning Process Starts")
clonedGraphHead = cloneGraph(n0, Node(n0.key, []), visited)
print("Cloning Process Completes.")

visited = [False]*(5)
print("\nGraph After Cloning:-")
printGraph(clonedGraphHead, visited)
```

**输出:**

```
Graph Before Cloning:-
edge 0x7fa03dd43878-0x7fa03dd43908:0-1
edge 0x7fa03dd43908-0x7fa03dd43950:1-2
edge 0x7fa03dd43950-0x7fa03dd43998:2-3
edge 0x7fa03dd43998-0x7fa03dd439e0:3-4
edge 0x7fa03dd43908-0x7fa03dd43998:1-3
edge 0x7fa03dd43908-0x7fa03dd439e0:1-4
edge 0x7fa03dd43878-0x7fa03dd43950:0-2

Cloning Process Starts
Cloning Process Completes.

Graph After Cloning:-
edge 0x7fa03dd43a28-0x7fa03dd43a70:0-1
edge 0x7fa03dd43a70-0x7fa03dd43ab8:1-2
edge 0x7fa03dd43ab8-0x7fa03dd43b00:2-3
edge 0x7fa03dd43b00-0x7fa03dd43b48:3-4
edge 0x7fa03dd43a70-0x7fa03dd43b90:1-3
edge 0x7fa03dd43a70-0x7fa03dd43bd8:1-4
edge 0x7fa03dd43a28-0x7fa03dd43c20:0-2
```

通过将相邻边附加到顶点来创建 DAG 发生在 0(1)时间内。图的克隆需要 O(E+V)时间。

本文由 **Raveena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。

Recommended Posts: