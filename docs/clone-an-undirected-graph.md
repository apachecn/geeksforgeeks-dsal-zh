# 克隆无向图

> 原文:[https://www.geeksforgeeks.org/clone-an-undirected-graph/](https://www.geeksforgeeks.org/clone-an-undirected-graph/)

克隆带有随机指针的[链表](https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/)和[二叉树](https://www.geeksforgeeks.org/clone-binary-tree-random-pointers/)已经讨论过了。克隆图表背后的想法非常相似。

其思想是对该图进行 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)，并在访问一个节点时创建该节点的克隆节点(原始节点的副本)。如果遇到已经访问过的节点，那么它已经有一个克隆节点。

**如何跟踪访问/克隆的节点？**
需要一个 HashMap/Map 来维护所有已经创建的节点。
*关键字存储*:原始节点的引用/地址
*值存储*:克隆节点的引用/地址

所有图形节点都已复制，**如何连接克隆节点？**
在访问一个节点的相邻顶点时 *u* 为 u 获取对应的克隆节点，我们称之为*克隆节点*，现在访问 *u* 的所有相邻节点，为每个相邻节点找到对应的克隆节点(如果没有找到创建一个)，然后推入*克隆节点*的相邻向量。

**如何验证克隆图是否正确？**
做一个 BFS 遍历前后的克隆图。在 BFS 遍历中，显示节点的值及其地址/引用。
如果两个遍历的值相同，但地址/引用不同，则比较节点的显示顺序，以确定克隆图是否正确。

## C++

```
// A C++ program to Clone an Undirected Graph
#include<bits/stdc++.h>
using namespace std;

struct GraphNode
{
    int val;

    //A neighbour vector which contains addresses to
    //all the neighbours of a GraphNode
    vector<GraphNode*> neighbours;
};

// A function which clones a Graph and
// returns the address to the cloned
// src node
GraphNode *cloneGraph(GraphNode *src)
{
    //A Map to keep track of all the
    //nodes which have already been created
    map<GraphNode*, GraphNode*> m;
    queue<GraphNode*> q;

    // Enqueue src node
    q.push(src);
    GraphNode *node;

    // Make a clone Node
    node = new GraphNode();
    node->val = src->val;

    // Put the clone node into the Map
    m[src] = node;
    while (!q.empty())
    {
        //Get the front node from the queue
        //and then visit all its neighbours
        GraphNode *u = q.front();
        q.pop();
        vector<GraphNode *> v = u->neighbours;
        int n = v.size();
        for (int i = 0; i < n; i++)
        {
            // Check if this node has already been created
            if (m[v[i]] == NULL)
            {
                // If not then create a new Node and
                // put into the HashMap
                node = new GraphNode();
                node->val = v[i]->val;
                m[v[i]] = node;
                q.push(v[i]);
            }

            // add these neighbours to the cloned graph node
            m[u]->neighbours.push_back(m[v[i]]);
        }
    }

    // Return the address of cloned src Node
    return m[src];
}

// Build the desired graph
GraphNode *buildGraph()
{
    /*
        Note : All the edges are Undirected
        Given Graph:
        1--2
        | |
        4--3
    */
    GraphNode *node1 = new GraphNode();
    node1->val = 1;
    GraphNode *node2 = new GraphNode();
    node2->val = 2;
    GraphNode *node3 = new GraphNode();
    node3->val = 3;
    GraphNode *node4 = new GraphNode();
    node4->val = 4;
    vector<GraphNode *> v;
    v.push_back(node2);
    v.push_back(node4);
    node1->neighbours = v;
    v.clear();
    v.push_back(node1);
    v.push_back(node3);
    node2->neighbours = v;
    v.clear();
    v.push_back(node2);
    v.push_back(node4);
    node3->neighbours = v;
    v.clear();
    v.push_back(node3);
    v.push_back(node1);
    node4->neighbours = v;
    return node1;
}

// A simple bfs traversal of a graph to
// check for proper cloning of the graph
void bfs(GraphNode *src)
{
    map<GraphNode*, bool> visit;
    queue<GraphNode*> q;
    q.push(src);
    visit[src] = true;
    while (!q.empty())
    {
        GraphNode *u = q.front();
        cout << "Value of Node " << u->val << "\n";
        cout << "Address of Node " <<u << "\n";
        q.pop();
        vector<GraphNode *> v = u->neighbours;
        int n = v.size();
        for (int i = 0; i < n; i++)
        {
            if (!visit[v[i]])
            {
                visit[v[i]] = true;
                q.push(v[i]);
            }
        }
    }
    cout << endl;
}

// Driver program to test above function
int main()
{
    GraphNode *src = buildGraph();
    cout << "BFS Traversal before cloning\n";
    bfs(src);
    GraphNode *newsrc = cloneGraph(src);
    cout << "BFS Traversal after cloning\n";
    bfs(newsrc);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Clone an Undirected Graph
import java.util.*;

// GraphNode class represents each
// Node of the Graph
class GraphNode
{
    int val;

    // A neighbour Vector which contains references to
    // all the neighbours of a GraphNode
    Vector<GraphNode> neighbours;
    public GraphNode(int val)
    {
        this.val = val;
        neighbours = new Vector<GraphNode>();
    }
}

class Graph
{
    // A method which clones the graph and
    // returns the reference of new cloned source node
    public GraphNode cloneGraph(GraphNode source)
    {
        Queue<GraphNode> q = new LinkedList<GraphNode>();
        q.add(source);

        // An HashMap to keep track of all the
        // nodes which have already been created
        HashMap<GraphNode,GraphNode> hm =
                        new HashMap<GraphNode,GraphNode>();

        //Put the node into the HashMap
        hm.put(source,new GraphNode(source.val));

        while (!q.isEmpty())
        {
            // Get the front node from the queue
            // and then visit all its neighbours
            GraphNode u = q.poll();

            // Get corresponding Cloned Graph Node
            GraphNode cloneNodeU = hm.get(u);
            if (u.neighbours != null)
            {
                Vector<GraphNode> v = u.neighbours;
                for (GraphNode graphNode : v)
                {
                    // Get the corresponding cloned node
                    // If the node is not cloned then we will
                    // simply get a null
                    GraphNode cloneNodeG = hm.get(graphNode);

                    // Check if this node has already been created
                    if (cloneNodeG == null)
                    {
                        q.add(graphNode);

                        // If not then create a new Node and
                        // put into the HashMap
                        cloneNodeG = new GraphNode(graphNode.val);
                        hm.put(graphNode,cloneNodeG);
                    }

                    // add the 'cloneNodeG' to neighbour
                    // vector of the cloneNodeG
                    cloneNodeU.neighbours.add(cloneNodeG);
                }
            }
        }

        // Return the reference of cloned source Node
        return hm.get(source);
    }

    // Build the desired graph
    public GraphNode buildGraph()
    {
        /*
            Note : All the edges are Undirected
            Given Graph:
            1--2
            |  |
            4--3
        */
        GraphNode node1 = new GraphNode(1);
        GraphNode node2 = new GraphNode(2);
        GraphNode node3 = new GraphNode(3);
        GraphNode node4 = new GraphNode(4);
        Vector<GraphNode> v = new Vector<GraphNode>();
        v.add(node2);
        v.add(node4);
        node1.neighbours = v;
        v = new Vector<GraphNode>();
        v.add(node1);
        v.add(node3);
        node2.neighbours = v;
        v = new Vector<GraphNode>();
        v.add(node2);
        v.add(node4);
        node3.neighbours = v;
        v = new Vector<GraphNode>();
        v.add(node3);
        v.add(node1);
        node4.neighbours = v;
        return node1;
    }

    // BFS traversal of a graph to
    // check if the cloned graph is correct
    public void bfs(GraphNode source)
    {
        Queue<GraphNode> q = new LinkedList<GraphNode>();
        q.add(source);
        HashMap<GraphNode,Boolean> visit =
                          new HashMap<GraphNode,Boolean>();
        visit.put(source,true);
        while (!q.isEmpty())
        {
            GraphNode u = q.poll();
            System.out.println("Value of Node " + u.val);
            System.out.println("Address of Node " + u);
            if (u.neighbours != null)
            {
                Vector<GraphNode> v = u.neighbours;
                for (GraphNode g : v)
                {
                    if (visit.get(g) == null)
                    {
                        q.add(g);
                        visit.put(g,true);
                    }
                }
            }
        }
        System.out.println();
    }
}

// Driver code
class Main
{
    public static void main(String args[])
    {
        Graph graph = new Graph();
        GraphNode source = graph.buildGraph();
        System.out.println("BFS traversal of a graph before cloning");
        graph.bfs(source);
        GraphNode newSource = graph.cloneGraph(source);
        System.out.println("BFS traversal of a graph after cloning");
        graph.bfs(newSource);
    }
}
```

Output in Java:

```
BFS traversal of a graph before cloning
Value of Node 1
Address of Node GraphNode@15db9742
Value of Node 2
Address of Node GraphNode@6d06d69c
Value of Node 4
Address of Node GraphNode@7852e922
Value of Node 3
Address of Node GraphNode@4e25154f

BFS traversal of a graph after cloning
Value of Node 1
Address of Node GraphNode@70dea4e
Value of Node 2
Address of Node GraphNode@5c647e05
Value of Node 4
Address of Node GraphNode@33909752
Value of Node 3
Address of Node GraphNode@55f96302

```

C++中的输出:

```
BFS Traversal before cloning
Value of Node 1
Address of Node 0x24ccc20
Value of Node 2
Address of Node 0x24ccc50
Value of Node 4
Address of Node 0x24cccb0
Value of Node 3
Address of Node 0x24ccc80

BFS Traversal after cloning
Value of Node 1
Address of Node 0x24cd030
Value of Node 2
Address of Node 0x24cd0e0
Value of Node 4
Address of Node 0x24cd170
Value of Node 3
Address of Node 0x24cd200

```

[克隆一个有多个连通分支的无向图](https://www.geeksforgeeks.org/clone-an-undirected-graph-with-multiple-connected-components/)

本文由 **Chirag Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。