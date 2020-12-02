# 克隆具有多个连接组件的无向图

> 原文： [https://www.geeksforgeeks.org/clone-an-undirected-graph-with-multiple-connected-components/](https://www.geeksforgeeks.org/clone-an-undirected-graph-with-multiple-connected-components/)

给定具有多个连接组件的无向图，任务是克隆图。 在中可以看到具有单个连接组件的克隆图。

**示例**：

```
An example of an undirected graph 
with 3 connected components:

```

**方法**：
的想法是采用与[克隆连接图](https://www.geeksforgeeks.org/clone-an-undirected-graph/)相同的方法，但是对于每个节点，以便我们可以克隆具有多个连接组件的图。

我们将使用 GraphNode 类和 Graph 类。 Graph 类是强制性的，因为我们可能有多个连接的组件（请参见上面的示例），并且我们不能仅以 GraphNode 作为输入来处理它们。 对于 Graph 类，我们实际需要的是 GraphNodes 列表。 两种方法都可以列出节点列表而不是创建类。

为了跟踪访问的节点，我们需要一个数据结构。 映射是一个合适的映射，因为我们可以从“旧”节点映射到“新”节点（克隆节点）。 因此，我们正在定义一个主要函数，该函数创建地图，并使用一个辅助函数来填充它。 创建地图后，可以使用地图中的克隆节点创建新图。

helper 函数将在节点之间建立连接（除了填充地图外）。 当我们处理整个连接的组件时，将采用类似的 BFS 方法。

请注意，在 main 函数中，我们没有为 Graph 中的每个节点调用 helper 函数； 如果该节点存储在地图中，则意味着我们已经访问过该节点并处理了其连接的组件，因此无需再次重复这些步骤。

为了检查图表是否已正确克隆，我们可以打印节点的内存地址，并对其进行比较以查看是否已克隆或已复制它们。

下面是上述方法的实现：

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



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。