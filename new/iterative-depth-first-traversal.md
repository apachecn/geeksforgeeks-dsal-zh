# 图

的迭代深度优先遍历

> 原文： [https://www.geeksforgeeks.org/iterative-depth-first-traversal/](https://www.geeksforgeeks.org/iterative-depth-first-traversal/)

图的[深度优先遍历（或搜索）](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)与树的[深度优先遍历（DFS）相似。 唯一的问题是，与树不同，图可能包含循环，因此一个节点可能会被访问​​两次。 为避免多次处理节点，请使用布尔访问数组。](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

**示例**：

> **输入**：n = 4，e = 6
> 0-> 1，0-> 2，1-> 2，2-> 0，2-> 3，3-> 3
> **输出**：来自顶点 1 的 DFS：1 2 0 3
> **说明**：
> DFS 图：
> ![](img/e5406fefbd33eb60daf3b49b93627347.png)
> 
> **输入**：n = 4，e = 6
> 2-> 0，0-> 2，1，-> 2，0-> 1，3-> 3，1-> 3
> **输出**：来自顶点 2 的 DFS：2 0 1 3
> **说明**：
> DFS 图：
> ![](img/def377ed85130fe8c5056325ec0f3116.png)

已经讨论了 DFS 的递归实现：[先前的文章](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。

<u>**解决方案**：</u>

*   **方法**：深度优先搜索是一种用于遍历或搜索树或图形数据结构的算法。 该算法从根节点开始（在图形的情况下，选择一些任意节点作为根节点），并在回溯之前尽可能沿着每个分支进行探索。 因此，基本思想是从根节点或任意节点开始，标记该节点，然后移至相邻的未标记节点，然后继续此循环，直到没有未标记的相邻节点为止。 然后回溯并检查其他未标记的节点并遍历它们。 最后打印路径中的节点。

    迭代 DFS 与递归 DFS 之间的唯一区别是，递归堆栈由节点堆栈代替。

*   **算法**：

    1.  创建了一个节点堆栈并访问了数组。

    2.  将根插入堆栈。

    3.  循环运行，直到堆栈不为空。

    4.  从堆栈中弹出元素并打印该元素。

    5.  对于当前节点的每个相邻且不可见的节点，标记该节点并将其插入堆栈。

*   **Implementation of Iterative DFS:** *This is similar to [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/), the only difference is queue is replaced by stack.*

    ## C++

    ```

    // An Iterative C++ program to do DFS traversal from 
    // a given source vertex. DFS(int s) traverses vertices 
    // reachable from s. 
    #include<bits/stdc++.h> 
    using namespace std; 

    // This class represents a directed graph using adjacency 
    // list representation 
    class Graph 
    { 
        int V;    // No. of vertices 
        list<int> *adj;    // adjacency lists 
    public: 
        Graph(int V);  // Constructor 
        void addEdge(int v, int w); // to add an edge to graph 
        void DFS(int s);  // prints all vertices in DFS manner 
        // from a given source. 
    }; 

    Graph::Graph(int V) 
    { 
        this->V = V; 
        adj = new list<int>[V]; 
    } 

    void Graph::addEdge(int v, int w) 
    { 
        adj[v].push_back(w); // Add w to v’s list. 
    } 

    // prints all not yet visited vertices reachable from s 
    void Graph::DFS(int s) 
    { 
        // Initially mark all verices as not visited 
        vector<bool> visited(V, false); 

        // Create a stack for DFS 
        stack<int> stack; 

        // Push the current source node. 
        stack.push(s); 

        while (!stack.empty()) 
        { 
            // Pop a vertex from stack and print it 
            s = stack.top(); 
            stack.pop(); 

            // Stack may contain same vertex twice. So 
            // we need to print the popped item only 
            // if it is not visited. 
            if (!visited[s]) 
            { 
                cout << s << " "; 
                visited[s] = true; 
            } 

            // Get all adjacent vertices of the popped vertex s 
            // If a adjacent has not been visited, then push it 
            // to the stack. 
            for (auto i = adj[s].begin(); i != adj[s].end(); ++i) 
                if (!visited[*i]) 
                    stack.push(*i); 
        } 
    } 

    // Driver program to test methods of graph class 
    int main() 
    { 
        Graph g(5); // Total 5 vertices in graph 
        g.addEdge(1, 0); 
        g.addEdge(0, 2); 
        g.addEdge(2, 1); 
        g.addEdge(0, 3); 
        g.addEdge(1, 4); 

        cout << "Following is Depth First Traversal\n"; 
        g.DFS(0); 

        return 0; 
    } 

    ```

    ## 爪哇

    ```

    //An Iterative Java program to do DFS traversal from 
    //a given source vertex. DFS(int s) traverses vertices 
    //reachable from s. 

    import java.util.*; 

    public class GFG  
    { 
        // This class represents a directed graph using adjacency 
        // list representation 
        static class Graph 
        { 
            int V; //Number of Vertices 

            LinkedList<Integer>[] adj; // adjacency lists 

            //Constructor 
            Graph(int V) 
            { 
                this.V = V; 
                adj = new LinkedList[V]; 

                for (int i = 0; i < adj.length; i++) 
                    adj[i] = new LinkedList<Integer>(); 

            } 

            //To add an edge to graph 
            void addEdge(int v, int w) 
            { 
                adj[v].add(w); // Add w to v’s list. 
            } 

            // prints all not yet visited vertices reachable from s 
            void DFS(int s) 
            { 
                // Initially mark all vertices as not visited 
                Vector<Boolean> visited = new Vector<Boolean>(V); 
                for (int i = 0; i < V; i++) 
                    visited.add(false); 

                // Create a stack for DFS 
                Stack<Integer> stack = new Stack<>(); 

                // Push the current source node 
                stack.push(s); 

                while(stack.empty() == false) 
                { 
                    // Pop a vertex from stack and print it 
                    s = stack.peek(); 
                    stack.pop(); 

                    // Stack may contain same vertex twice. So 
                    // we need to print the popped item only 
                    // if it is not visited. 
                    if(visited.get(s) == false) 
                    { 
                        System.out.print(s + " "); 
                        visited.set(s, true); 
                    } 

                    // Get all adjacent vertices of the popped vertex s 
                    // If a adjacent has not been visited, then push it 
                    // to the stack. 
                    Iterator<Integer> itr = adj[s].iterator(); 

                    while (itr.hasNext())  
                    { 
                        int v = itr.next(); 
                        if(!visited.get(v)) 
                            stack.push(v); 
                    } 

                } 
            } 
        } 

        // Driver program to test methods of graph class 
        public static void main(String[] args)  
        { 
            // Total 5 vertices in graph 
            Graph g = new Graph(5); 

            g.addEdge(1, 0); 
            g.addEdge(0, 2); 
            g.addEdge(2, 1); 
            g.addEdge(0, 3); 
            g.addEdge(1, 4); 

            System.out.println("Following is the Depth First Traversal"); 
            g.DFS(0); 
        } 
    } 

    ```

    ## Python3

    ```

    # An Iterative Python program to do DFS traversal from  
    # a given source vertex. DFS(int s) traverses vertices  
    # reachable from s.  

    # This class represents a directed graph using adjacency  
    # list representation  
    class Graph:  
        def __init__(self,V): # Constructor  
            self.V = V        # No. of vertices  
            self.adj  = [[] for i in range(V)]  # adjacency lists  

        def addEdge(self,v, w):     # to add an edge to graph 
            self.adj[v].append(w)    # Add w to v’s list.  

        # prints all not yet visited vertices reachable from s  
        def DFS(self,s):            # prints all vertices in DFS manner from a given source. 
                                    # Initially mark all verices as not visited  
            visited = [False for i in range(self.V)]  

            # Create a stack for DFS  
            stack = [] 

            # Push the current source node.  
            stack.append(s)  

            while (len(stack)):  
                # Pop a vertex from stack and print it  
                s = stack[-1]  
                stack.pop() 

                # Stack may contain same vertex twice. So  
                # we need to print the popped item only  
                # if it is not visited.  
                if (not visited[s]):  
                    print(s,end=' ') 
                    visited[s] = True 

                # Get all adjacent vertices of the popped vertex s  
                # If a adjacent has not been visited, then push it  
                # to the stack.  
                for node in self.adj[s]:  
                    if (not visited[node]):  
                        stack.append(node)  

    # Driver program to test methods of graph class  

    g = Graph(5); # Total 5 vertices in graph  
    g.addEdge(1, 0);  
    g.addEdge(0, 2);  
    g.addEdge(2, 1);  
    g.addEdge(0, 3);  
    g.addEdge(1, 4);  

    print("Following is Depth First Traversal")  
    g.DFS(0) 

    # This code is contributed by ankush_953 

    ```

    ## C＃

    ```

    // An Iterative C# program to do DFS traversal from 
    // a given source vertex. DFS(int s) traverses vertices 
    // reachable from s. 
    using System;  
    using System.Collections.Generic; 

    class GFG  
    { 
        // This class represents a directed graph using adjacency 
        // list representation 
        public class Graph 
        { 
            public int V; // Number of Vertices 

            public LinkedList<int>[] adj; // adjacency lists 

            // Constructor 
            public Graph(int V) 
            { 
                this.V = V; 
                adj = new LinkedList<int>[V]; 

                for (int i = 0; i < adj.Length; i++) 
                    adj[i] = new LinkedList<int>(); 

            } 

            // To add an edge to graph 
            public void addEdge(int v, int w) 
            { 
                adj[v].AddLast(w); // Add w to v’s list. 
            } 

            // prints all not yet visited vertices reachable from s 
            public void DFS(int s) 
            { 
                // Initially mark all vertices as not visited 
                Boolean []visited = new Boolean[V]; 

                // Create a stack for DFS 
                Stack<int> stack = new Stack<int>(); 

                // Push the current source node 
                stack.Push(s); 

                while(stack.Count > 0) 
                { 
                    // Pop a vertex from stack and print it 
                    s = stack.Peek(); 
                    stack.Pop(); 

                    // Stack may contain same vertex twice. So 
                    // we need to print the popped item only 
                    // if it is not visited. 
                    if(visited[s] == false) 
                    { 
                        Console.Write(s + " "); 
                        visited[s] = true; 
                    } 

                    // Get all adjacent vertices of the popped vertex s 
                    // If a adjacent has not been visited, then push it 
                    // to the stack. 
                    foreach(int v in adj[s]) 
                    { 
                        if(!visited[v]) 
                            stack.Push(v); 
                    } 

                } 
            } 
        } 

        // Driver code 
        public static void Main(String []args)  
        { 
            // Total 5 vertices in graph 
            Graph g = new Graph(5); 

            g.addEdge(1, 0); 
            g.addEdge(0, 2); 
            g.addEdge(2, 1); 
            g.addEdge(0, 3); 
            g.addEdge(1, 4); 

            Console.Write("Following is the Depth First Traversal\n"); 
            g.DFS(0); 
        } 
    } 

    // This code is contributed by Arnasb Kundu 

    ```

    **Output:**

    ```
    Following is Depth First Traversal
    0 3 2 1 4 
    ```

*   **Complexity Analysis:**

    *   **时间复杂度**：O（V + E），其中 V 是顶点数量，E 是图形中边的数量。

    *   **空间复杂度**：O（V）。 由于需要一个额外的访问数组，其大小为 V。

**<u>上述解决方案</u>的修改**：请注意，以上实现仅打印从给定顶点可到达的顶点。 例如，如果删除了边 0-3 和 0-2，则上述程序将仅打印 0。要打印图形的所有顶点，请为每个未访问的顶点调用 DFS。

**实施**：

## C++

```cpp

// An Iterative C++ program to do DFS traversal from 
// a given source vertex. DFS(int s) traverses vertices 
// reachable from s. 
#include<bits/stdc++.h> 
using namespace std; 

// This class represents a directed graph using adjacency 
// list representation 
class Graph 
{ 
    int V;    // No. of vertices 
    list<int> *adj;    // adjacency lists 
public: 
    Graph(int V);  // Constructor 
    void addEdge(int v, int w); // to add an edge to graph 
    void DFS();  // prints all vertices in DFS manner 

    // prints all not yet visited vertices reachable from s 
    void DFSUtil(int s, vector<bool> &visited); 
}; 

Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

void Graph::addEdge(int v, int w) 
{ 
    adj[v].push_back(w); // Add w to v’s list. 
} 

// prints all not yet visited vertices reachable from s 
void Graph::DFSUtil(int s, vector<bool> &visited) 
{ 
    // Create a stack for DFS 
    stack<int> stack; 

    // Push the current source node. 
    stack.push(s); 

    while (!stack.empty()) 
    { 
        // Pop a vertex from stack and print it 
        s = stack.top(); 
        stack.pop(); 

        // Stack may contain same vertex twice. So 
        // we need to print the popped item only 
        // if it is not visited. 
        if (!visited[s]) 
        { 
            cout << s << " "; 
            visited[s] = true; 
        } 

        // Get all adjacent vertices of the popped vertex s 
        // If a adjacent has not been visited, then push it 
        // to the stack. 
        for (auto i = adj[s].begin(); i != adj[s].end(); ++i) 
            if (!visited[*i]) 
                stack.push(*i); 
    } 
} 

// prints all vertices in DFS manner 
void Graph::DFS() 
{ 
    // Mark all the vertices as not visited 
    vector<bool> visited(V, false); 

    for (int i = 0; i < V; i++) 
        if (!visited[i]) 
            DFSUtil(i, visited); 
} 

// Driver program to test methods of graph class 
int main() 
{ 
    Graph g(5);  // Total 5 vertices in graph 
    g.addEdge(1, 0); 
    g.addEdge(2, 1); 
    g.addEdge(3, 4); 
    g.addEdge(4, 0); 

    cout << "Following is Depth First Traversal\n"; 
    g.DFS(); 

    return 0; 
} 

```