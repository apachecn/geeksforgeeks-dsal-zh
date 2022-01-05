# 克隆一个有多个连通分支的无向图

> 原文:[https://www . geesforgeks . org/clone-一个有多个连接组件的无向图/](https://www.geeksforgeeks.org/clone-an-undirected-graph-with-multiple-connected-components/)

给定一个有多个连通分量的无向图，任务是克隆该图。克隆一个有单个连通分量的图可以在这里看到。

**示例:**

```
An example of an undirected graph 
with 3 connected components:
```

![](img/7fc49dd2a4d2edca373c5adf9becb0a0.png)

**方法:**
想法是遵循为[克隆连通图](https://www.geeksforgeeks.org/clone-an-undirected-graph/)发布的相同方法，但是每个节点都是这样，这样我们就可以克隆具有多个连接组件的图。

我们将使用一个 GraphNode 类和一个 Graph 类。Graph 类是强制性的，因为我们可能有多个连接的组件(见上面的例子)，我们不能处理只有一个 GraphNode 作为输入的组件。对于 Graph 类，我们实际需要的是一个 GraphNodes 列表。也可以列出节点列表，而不是创建一个类，两种方法都可以。

为了跟踪被访问的节点，我们需要一个数据结构；映射是合适的，因为我们可以从“旧”节点映射到“新”节点(克隆的)。因此，我们定义了一个主函数，它创建地图，并使用一个辅助函数来填充它。一旦创建了地图，就可以使用地图中的克隆节点创建新的图形。
辅助函数将放置节点之间的连接(除了填充地图)。当我们处理一个完整的关联组件时，将会采用类似于 BFS 的方法。

请注意，在主函数中，我们没有为 Graph 中的每个节点调用 helper 函数；如果节点存储在地图中，这意味着我们已经访问了它并处理了它的连接组件，因此不需要再次重复这些步骤。
为了检查图形是否被正确克隆，我们可以打印节点的内存地址，并进行比较，看看我们是克隆了，还是复制了。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// GraphNode class represents each
// Node of the Graph
class GraphNode
{
    int data;
    list<GraphNode *> children;

    // Constructor to initialize the
    // node with value
    public:
        GraphNode(int data)
        {
            this->data = data;
        }

        // Function to add a child to the
        // current node
        void addChild(GraphNode *node)
        {
            this->children.push_back(node);
        }

        // Function to return a list of children
        // for the current node
        list<GraphNode *> getChildren()
        {
            return children;
        }

        // Function to set the node's value
        void setData(int data)
        {
            this->data = data;
        }

        // Function to return the node's value
        int getData()
        {
            return data;
        }
};

// Class to represent the graph
class Graph
{
    list<GraphNode *> nodes;

    public:
        Graph(){}

        // Constructor to set the graph's nodes
        Graph(list<GraphNode *> nodes)
        {
            this->nodes = nodes;
        }

        // Function to add a node to the graph
        void addNode(GraphNode *node)
        {
            this->nodes.push_back(node);
        }

        // Function to return the list of nodes
        // for the graph
        list<GraphNode *> getNodes()
        {
            return this->nodes;
        }
};

class GFG{

// Function to clone the graph
// Function to clone the connected components
void cloneConnectedComponent(GraphNode *node,
                             map<GraphNode *,
                             GraphNode *> &map)
{
    queue<GraphNode *> queue;
    queue.push(node);

    while (!queue.empty())
    {
        GraphNode *current = queue.front();
        queue.pop();
        GraphNode *currentCloned = NULL;

        if (map.find(current) != map.end())
        {
            currentCloned = map[current];
        }
        else
        {
            currentCloned = new GraphNode(
                current->getData());
            map[current] = currentCloned;
        }

        list<GraphNode *> children = current->getChildren();
        for(auto child : children)
        {
            if (map.find(child) != map.end())
            {
                currentCloned->addChild(map[child]);
            }
            else
            {
                GraphNode *childCloned = new GraphNode(
                    child->getData());
                map[child] = childCloned;
                currentCloned->addChild(childCloned);
                queue.push(child);
            }
        }
    }
}

public:
    Graph *cloneGraph(Graph *graph)
    {
        map<GraphNode *, GraphNode *> mapp;
        for(auto node : graph->getNodes())
        {
            if (mapp.find(node) == mapp.end())
                cloneConnectedComponent(node, mapp);
        }
        Graph *cloned = new Graph();
        for(auto current : mapp)
            cloned->addNode(current.second);

        return cloned;
    }

// Function to build the graph
Graph *buildGraph()
{

    // Create graph
    Graph *g = new Graph();

    // Adding nodes to the graph
    GraphNode *g1 = new GraphNode(1);
    g->addNode(g1);
    GraphNode *g2 = new GraphNode(2);
    g->addNode(g2);
    GraphNode *g3 = new GraphNode(3);
    g->addNode(g3);
    GraphNode *g4 = new GraphNode(4);
    g->addNode(g4);
    GraphNode *g5 = new GraphNode(5);
    g->addNode(g5);
    GraphNode *g6 = new GraphNode(6);
    g->addNode(g6);

    // Adding edges
    g1->addChild(g2);
    g1->addChild(g3);
    g2->addChild(g1);
    g2->addChild(g4);
    g3->addChild(g1);
    g3->addChild(g4);
    g4->addChild(g2);
    g4->addChild(g3);
    g5->addChild(g6);
    g6->addChild(g5);

    return g;
}

// Function to print the connected components
void printConnectedComponent(GraphNode *node,
                         set<GraphNode *> &visited)
{
    if (visited.find(node) != visited.end())
        return;
    queue<GraphNode *> q;
    q.push(node);

    while (!q.empty())
    {
        GraphNode *currentNode = q.front();
        q.pop();

        if (visited.find(currentNode) != visited.end())
            continue;

        visited.insert(currentNode);
        cout << "Node " << currentNode->getData()
             << " - " << currentNode << endl;
        for(GraphNode *child : currentNode->getChildren())
        {
            cout << "\tNode " << child->getData()
                 << " - " << child << endl;
            q.push(child);
        }
    }
}
};

// Driver code
int main()
{
    GFG *gfg = new GFG();
    Graph *g = gfg->buildGraph();

    // Original graph
    cout << "\tINITIAL GRAPH\n";
    set<GraphNode *> visited;
    for(GraphNode *n : g->getNodes())
        gfg->printConnectedComponent(n, visited);

    // Cloned graph
    cout << "\n\n\tCLONED GRAPH\n";
    Graph *cloned = gfg->cloneGraph(g);
    visited.clear();
    for(GraphNode *node : cloned->getNodes())
        gfg->printConnectedComponent(node, visited);
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Queue;
import java.util.Set;

// Class to represent the graph
class Graph {

    private List<GraphNode> nodes;

    // Constructor to create an empty ArrayList
    // to store the nodes of the graph
    public Graph()
    {
        this.nodes = new ArrayList<GraphNode>();
    }

    // Constructor to set the graph's nodes
    public Graph(List<GraphNode> nodes)
    {
        this.nodes = nodes;
        this.nodes = new ArrayList<GraphNode>();
    }

    // Function to add a node to the graph
    public void addNode(GraphNode node)
    {
        this.nodes.add(node);
    }

    // Function to return the list of nodes
    // for the graph
    public List<GraphNode> getNodes()
    {
        return this.nodes;
    }
}

// GraphNode class represents each
// Node of the Graph
class GraphNode {

    private int data;
    private List<GraphNode> children;

    // Constructor to initialize the node with value
    public GraphNode(int data)
    {
        this.data = data;
        this.children = new ArrayList<GraphNode>();
    }

    // Function to add a child to the current node
    public void addChild(GraphNode node)
    {
        this.children.add(node);
    }

    // Function to return a list of children
    // for the current node
    public List<GraphNode> getChildren()
    {
        return children;
    }

    // Function to set the node's value
    public void setData(int data)
    {
        this.data = data;
    }

    // Function to return the node's value
    public int getData()
    {
        return data;
    }
}

public class GFG {

    // Function to clone the graph
    public Graph cloneGraph(Graph graph)
    {
        Map<GraphNode, GraphNode> map
            = new HashMap<GraphNode, GraphNode>();
        for (GraphNode node : graph.getNodes()) {
            if (!map.containsKey(node))
                cloneConnectedComponent(node, map);
        }

        Graph cloned = new Graph();
        for (GraphNode current : map.values())
            cloned.addNode(current);

        return cloned;
    }

    // Function to clone the connected components
    private void cloneConnectedComponent(GraphNode node,
                          Map<GraphNode, GraphNode> map)
    {
        Queue<GraphNode> queue = new LinkedList<GraphNode>();
        queue.add(node);

        while (!queue.isEmpty()) {
            GraphNode current = queue.poll();
            GraphNode currentCloned = null;
            if (map.containsKey(current)) {
                currentCloned = map.get(current);
            }
            else {
                currentCloned = new GraphNode(current.getData());
                map.put(current, currentCloned);
            }

            List<GraphNode> children = current.getChildren();
            for (GraphNode child : children) {
                if (map.containsKey(child)) {
                    currentCloned.addChild(map.get(child));
                }
                else {
                    GraphNode childCloned
                        = new GraphNode(child.getData());
                    map.put(child, childCloned);
                    currentCloned.addChild(childCloned);
                    queue.add(child);
                }
            }
        }
    }

    // Function to build the graph
    public Graph buildGraph()
    {

        // Create graph
        Graph g = new Graph();

        // Adding nodes to the graph
        GraphNode g1 = new GraphNode(1);
        g.addNode(g1);
        GraphNode g2 = new GraphNode(2);
        g.addNode(g2);
        GraphNode g3 = new GraphNode(3);
        g.addNode(g3);
        GraphNode g4 = new GraphNode(4);
        g.addNode(g4);
        GraphNode g5 = new GraphNode(5);
        g.addNode(g5);
        GraphNode g6 = new GraphNode(6);
        g.addNode(g6);

        // Adding edges
        g1.addChild(g2);
        g1.addChild(g3);
        g2.addChild(g1);
        g2.addChild(g4);
        g3.addChild(g1);
        g3.addChild(g4);
        g4.addChild(g2);
        g4.addChild(g3);
        g5.addChild(g6);
        g6.addChild(g5);

        return g;
    }

    // Function to print the connected components
    public void printConnectedComponent(GraphNode node,
                                        Set<GraphNode> visited)
    {
        if (visited.contains(node))
            return;

        Queue<GraphNode> q = new LinkedList<GraphNode>();
        q.add(node);

        while (!q.isEmpty()) {
            GraphNode currentNode = q.remove();
            if (visited.contains(currentNode))
                continue;
            visited.add(currentNode);
            System.out.println("Node "
                               + currentNode.getData() + " - " + currentNode);
            for (GraphNode child : currentNode.getChildren()) {
                System.out.println("\tNode "
                                   + child.getData() + " - " + child);
                q.add(child);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        GFG gfg = new GFG();
        Graph g = gfg.buildGraph();

        // Original graph
        System.out.println("\tINITIAL GRAPH");
        Set<GraphNode> visited = new HashSet<GraphNode>();
        for (GraphNode n : g.getNodes())
            gfg.printConnectedComponent(n, visited);

        // Cloned graph
        System.out.println("\n\n\tCLONED GRAPH\n");
        Graph cloned = gfg.cloneGraph(g);
        visited = new HashSet<GraphNode>();
        for (GraphNode node : cloned.getNodes())
            gfg.printConnectedComponent(node, visited);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque as dq

# GraphNode class represents each
#  Node of the Graph
class GraphNode:   
    # Constructor to initialize the
    # node with value
    def __init__(self,data):
        self.__data = data
        self.__children=[]

    # Function to add a child to the
    # current node
    def addChild(self,node):
        self.__children.append(node)

    # Function to return a list of children
    # for the current node
    def getChildren(self):
        return self.__children

    # Function to set the node's value
    def setData(self,data):
        self.__data = data

    # Function to return the node's value
    def getData(self):
        return self.__data

# Class to represent the graph
class Graph:

    # Constructor to set the graph's nodes
    def __init__(self,nodes):
        self.__nodes = nodes

    # Function to add a node to the graph
    def addNode(self,node):
        self.__nodes.append(node)

    # Function to return the list of nodes
    # for the graph
    def getNodes(self):
        return self.__nodes

class GFG:

    # Function to clone the connected components
    def cloneConnectedComponent(self, node, mp):

        queue=dq([node,])

        while (queue):
            current = queue.popleft()
            currentCloned = None

            if (current in mp):
                currentCloned = mp[current]
            else:
                currentCloned = GraphNode(current.getData())
                mp[current] = currentCloned

            children = current.getChildren()
            for child in children:

                if (child in mp):
                    currentCloned.addChild(mp[child])
                else:
                    childCloned = GraphNode(child.getData())
                    mp[child] = childCloned
                    currentCloned.addChild(childCloned)
                    queue.append(child)

    # Function to clone the graph
    def cloneGraph(self,graph):
        mapp=dict()
        for node in graph.getNodes():
            if (node not in mapp):
                self.cloneConnectedComponent(node, mapp)

        cloned = Graph([])
        for current in mapp:
            cloned.addNode(mapp[current])

        return cloned

    # Function to build the graph
    def buildGraph(self):

        # Create graph
        G = Graph([])

        # Adding nodes to the graph
        g1 = GraphNode(1)
        G.addNode(g1)
        g2 = GraphNode(2)
        G.addNode(g2)
        g3 = GraphNode(3)
        G.addNode(g3)
        g4 = GraphNode(4)
        G.addNode(g4)
        g5 = GraphNode(5)
        G.addNode(g5)
        g6 = GraphNode(6)
        G.addNode(g6)

        # Adding edges
        g1.addChild(g2)
        g1.addChild(g3)
        g2.addChild(g1)
        g2.addChild(g4)
        g3.addChild(g1)
        g3.addChild(g4)
        g4.addChild(g2)
        g4.addChild(g3)
        g5.addChild(g6)
        g6.addChild(g5)

        return G

    # Function to print the connected components
    def printConnectedComponent(self,node, visited):

        if (node in visited):
            return
        q=dq([node,])

        while (q):
            currentNode = q.popleft()

            if (currentNode in visited):
                continue

            visited.add(currentNode)
            print("Node {} - {}".format(currentNode.getData(),hex(id(currentNode))))
            for child in currentNode.getChildren():
                print("\tNode {} - {}".format(child.getData(),hex(id(child))))
                q.append(child)

# Driver code
if __name__ == '__main__':
    gfg = GFG()
    g = gfg.buildGraph()

    # Original graph
    print("\tINITIAL GRAPH")
    visited=set()
    for n in g.getNodes():
        gfg.printConnectedComponent(n, visited)

    # Cloned graph
    print("\n\n\tCLONED GRAPH")
    cloned = gfg.cloneGraph(g)
    visited.clear()
    for node in cloned.getNodes():
        gfg.printConnectedComponent(node, visited)

    # This code is contributed by Amartya Ghosh
```

**Output:** 

```
INITIAL GRAPH
Node 1 - GraphNode@232204a1
    Node 2 - GraphNode@4aa298b7
    Node 3 - GraphNode@7d4991ad
Node 2 - GraphNode@4aa298b7
    Node 1 - GraphNode@232204a1
    Node 4 - GraphNode@28d93b30
Node 3 - GraphNode@7d4991ad
    Node 1 - GraphNode@232204a1
    Node 4 - GraphNode@28d93b30
Node 4 - GraphNode@28d93b30
    Node 2 - GraphNode@4aa298b7
    Node 3 - GraphNode@7d4991ad
Node 5 - GraphNode@1b6d3586
    Node 6 - GraphNode@4554617c
Node 6 - GraphNode@4554617c
    Node 5 - GraphNode@1b6d3586

    CLONED GRAPH

Node 1 - GraphNode@74a14482
    Node 2 - GraphNode@1540e19d
    Node 3 - GraphNode@677327b6
Node 2 - GraphNode@1540e19d
    Node 1 - GraphNode@74a14482
    Node 4 - GraphNode@14ae5a5
Node 3 - GraphNode@677327b6
    Node 1 - GraphNode@74a14482
    Node 4 - GraphNode@14ae5a5
Node 4 - GraphNode@14ae5a5
    Node 2 - GraphNode@1540e19d
    Node 3 - GraphNode@677327b6
Node 6 - GraphNode@7f31245a
    Node 5 - GraphNode@6d6f6e28
Node 5 - GraphNode@6d6f6e28
    Node 6 - GraphNode@7f31245a
```

**时间复杂度** : O(V + E)，其中 V 和 E 分别是图中的顶点数和边数。
**辅助空间** : O(V + E)。