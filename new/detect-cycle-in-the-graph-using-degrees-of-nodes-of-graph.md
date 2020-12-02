# 使用图

的节点度来检测图中的周期

> 原文： [https://www.geeksforgeeks.org/detect-cycle-in-the-graph-using-degrees-of-nodes-of-graph/](https://www.geeksforgeeks.org/detect-cycle-in-the-graph-using-degrees-of-nodes-of-graph/)

给定一个图形，任务是使用图形中节点的度数检测图形中的一个循环，并打印出任何循环中涉及的所有节点。 如果图形中没有循环，则打印 **-1** 。

**示例**：

> **输入**：
> 
> ![](img/9bf1aa7de08062127bf26d54b62a46b4.png)
> 
> **输出**：0 1 2

**方法**：递归删除度 1 的所有顶点。这可以通过将顶点的[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储到其度数来有效地完成。
首先，遍历地图并将度数= 1 的所有顶点存储在队列中。 只要队列不为空，就遍历该队列。 对于队列中的每个节点，将其标记为已访问，并遍历所有与其连接的节点（使用邻接表），并在映射中将每个节点的度数减一。 将所有度等于 1 的节点添加到队列中。 在该算法的最后，所有未访问的节点都是循环的一部分。

下面是上述方法的实现：

## C ++ 14

```

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Graph class
class Graph
{
public:

    // No. of vertices of graph
    int v;

    // Adjacency List
    vector<int> *l;

    Graph(int v)
    {
        this->v = v;
        this->l = new vector<int>[v];
    }

    void addedge(int i, int j)
    {
        l[i].push_back(j);
        l[j].push_back(i);
    }
};

// Function to find a cycle in the given graph if exists
void findCycle(int n, int r, Graph g)
{
    // HashMap to store the degree of each node
    unordered_map<int, int> degree;

    for (int i = 0; i < g.v; i++)
        degree[i] = g.l[i].size();

    // Array to track visited nodes
    int visited[g.v] = {0};

    // Queue to store the nodes of degree 1
    queue<int> q;

    // Continuously adding those nodes whose
    // degree is 1 to the queue
    while (true)
    {
        // Adding nodes to queue whose degree is 1
        // and is not visited
        for (int i = 0; i < degree.size(); i++)
            if (degree.at(i) == 1 and !visited[i])
                q.push(i);

        // If queue becomes empty then get out
        // of the continuous loop
        if (q.empty())
            break;

        while (!q.empty())
        {
            // Remove the front element from the queue
            int temp = q.front();
            q.pop();

            // Mark the removed element visited
            visited[temp] = 1;

            // Decrement the degree of all those nodes
            // adjacent to removed node
            for (int i = 0; i < g.l[temp].size(); i++)
            {
                int value = degree[g.l[temp][i]];
                degree[g.l[temp][i]] = --value;
            }
        }
    }
    int flag = 0;

    // Checking all the nodes which are not visited
    // i.e. they are part of the cycle
    for (int i = 0; i < g.v; i++)
        if (visited[i] == 0)
            flag = 1;

    if (flag == 0)
        cout << "-1";
    else
    {
        for (int i = 0; i < g.v; i++)
            if (visited[i] == 0)
                cout << i << " ";
    }
}

// Driver Code
int main()
{
    // No of nodes
    int n = 5;

    // No of edges
    int e = 5;
    Graph g(n);

    g.addedge(0, 1);
    g.addedge(0, 2);
    g.addedge(0, 3);
    g.addedge(1, 2);
    g.addedge(3, 4);

    findCycle(n, e, g);
    return 0;
}

// This code is contributed by
// sanjeev2552

```

## 爪哇

```

// Java implementation of the approach
import java.util.*;

// Graph class
class Graph {

    // No. of vertices of graph
    int v;

    // Adjacency List
    LinkedList l[];

    Graph(int v)
    {
        this.v = v;
        this.l = new LinkedList[v];
        for (int i = 0; i < v; i++) {
            l[i] = new LinkedList();
        }
    }
    void addedge(int i, int j)
    {
        l[i].add(j);
        l[j].add(i);
    }
}

class GFG {

    // Function to find a cycle in the given graph if exists
    static void findCycle(int n, int e, Graph g)
    {

        // HashMap to store the degree of each node
        HashMap degree = new HashMap();

        for (int i = 0; i < g.l.length; i++)
            degree.put(i, g.l[i].size());

        // Array to track visited nodes
        int visited[] = new int[g.v];

        // Initially all nodes are not visited
        for (int i = 0; i < visited.length; i++)
            visited[i] = 0;

        // Queue to store the nodes of degree 1
        LinkedList q = new LinkedList();

        // Continuously adding those nodes whose
        // degree is 1 to the queue
        while (true) {

            // Adding nodes to queue whose degree is 1
            // and is not visited

            for (int i = 0; i < degree.size(); i++)
                if ((int)degree.get(i) == 1 && visited[i] == 0)
                    q.add(i);

            // If queue becomes empty then get out
            // of the continuous loop
            if (q.isEmpty())
                break;

            while (!q.isEmpty()) {

                // Remove the front element from the queue
                int temp = (int)q.remove();

                // Mark the removed element visited
                visited[temp] = 1;

                // Decrement the degree of all those nodes
                // adjacent to removed node
                for (int i = 0; i < g.l[temp].size(); i++) {
                    int value = (int)degree.get((int)g.l[temp].get(i));
                    degree.replace(g.l[temp].get(i), --value);
                }
            }
        }

        int flag = 0;

        // Checking all the nodes which are not visited
        // i.e. they are part of the cycle
        for (int i = 0; i < visited.length; i++)
            if (visited[i] == 0)
                flag = 1;

        if (flag == 0)
            System.out.print("-1");
        else {
            for (int i = 0; i < visited.length; i++)
                if (visited[i] == 0)
                    System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        // No of nodes
        int n = 5;

        // No of edges
        int e = 5;
        Graph g = new Graph(n);

        g.addedge(0, 1);
        g.addedge(0, 2);
        g.addedge(0, 3);
        g.addedge(1, 2);
        g.addedge(3, 4);

        findCycle(n, e, g);
    }
}

```

## Python3

```

# Python3 implementation of the approach

# Graph class
class Graph:
    def __init__(self, v):

        # No. of vertices of graph
        self.v = v

        # Adjacency List
        self.l = [0] * v
        for i in range(self.v):
            self.l[i] = []

    def addedge(self, i: int, j: int):
        self.l[i].append(j)
        self.l[j].append(i)

# Function to find a cycle in the given graph if exists
def findCycle(n: int, e: int, g: Graph) -> None:

    # HashMap to store the degree of each node
    degree = dict()

    for i in range(len(g.l)):
        degree[i] = len(g.l[i])

    # Array to track visited nodes
    visited = [0] * g.v

    # Initially all nodes are not visited
    for i in range(len(visited)):
        visited[i] = 0

    # Queue to store the nodes of degree 1
    q = list()

    # Continuously adding those nodes whose
    # degree is 1 to the queue
    while True:

        # Adding nodes to queue whose degree is 1
        # and is not visited
        for i in range(len(degree)):
            if degree[i] == 1 and visited[i] == 0:
                q.append(i)

        # If queue becomes empty then get out
        # of the continuous loop
        if len(q) == 0:
            break

        while q:

            # Remove the front element from the queue
            temp = q.pop()

            # Mark the removed element visited
            visited[temp] = 1

            # Decrement the degree of all those nodes
            # adjacent to removed node
            for i in range(len(g.l[temp])):
                value = degree[g.l[temp][i]]
                degree[g.l[temp][i]] = value - 1

    flag = 0

    # Checking all the nodes which are not visited
    # i.e. they are part of the cycle
    for i in range(len(visited)):
        if visited[i] == 0:
            flag = 1

    if flag == 0:
        print("-1")
    else:
        for i in range(len(visited)):
            if visited[i] == 0:
                print(i, end = " ")

# Driver Code
if __name__ == "__main__":

    # No of nodes
    n = 5

    # No of edges
    e = 5
    g = Graph(n)

    g.addedge(0, 1)
    g.addedge(0, 2)
    g.addedge(0, 3)
    g.addedge(1, 2)
    g.addedge(3, 4)

    findCycle(n, e, g)

# This code is contributed by
# sanjeev2552

```

## C＃

```

// C# implementation of the approach
using System;
using System.Collections.Generic;

// Graph class
public class Graph 
{

    // No. of vertices of graph
    public int v;

    // Adjacency List
    public  List<int> []l;

    public Graph(int v)
    {
        this.v = v;
        this.l = new List<int>[v];
        for(int i = 0; i < v; i++) 
        {
            l[i] = new List<int>();
        }
    }
    public void addedge(int i, int j)
    {
        l[i].Add(j);
        l[j].Add(i);
    }
}

class GFG{

// Function to find a cycle in the 
// given graph if exists
static void findCycle(int n, int e, Graph g)
{

    // Dictionary to store the degree of each node
    Dictionary<int,
               int> degree = new Dictionary<int,
                                            int>();

    for(int i = 0; i < g.l.Length; i++)
        degree.Add(i, g.l[i].Count);

    // Array to track visited nodes
    int []visited = new int[g.v];

    // Initially all nodes are not visited
    for(int i = 0; i < visited.Length; i++)
        visited[i] = 0;

    // Queue to store the nodes of degree 1
    List<int> q = new List<int>();

    // Continuously adding those nodes whose
    // degree is 1 to the queue
    while (true)
    {

        // Adding nodes to queue whose degree is 1
        // and is not visited
        for(int i = 0; i < degree.Count; i++)
            if ((int)degree[i] == 1 && visited[i] == 0)
                q.Add(i);

        // If queue becomes empty then get out
        // of the continuous loop
        if (q.Count!=0)
            break;

        while (q.Count != 0) 
        {

            // Remove the front element from the queue
            int temp = q[0];    
            q.RemoveAt(0);

            // Mark the removed element visited
            visited[temp] = 1;

            // Decrement the degree of all those nodes
            // adjacent to removed node
            for(int i = 0; i < g.l[temp].Count; i++)
            {
                int value = (int)degree[(int)g.l[temp][i]];
                degree[g.l[temp][i]] = value -= 1;
            }
        }
    }

    int flag = 0;

    // Checking all the nodes which are not visited
    // i.e. they are part of the cycle
    for(int i = 0; i < visited.Length; i++)
        if (visited[i] == 0)
            flag = 1;

    if (flag == 0)
        Console.Write("-1");
    else
    {
        for(int i = 0; i < visited.Length-2; i++)
            if (visited[i] == 0)
                Console.Write(i + " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    // No of nodes
    int n = 5;

    // No of edges
    int e = 5;
    Graph g = new Graph(n);

    g.addedge(0, 1);
    g.addedge(0, 2);
    g.addedge(0, 3);
    g.addedge(1, 2);
    g.addedge(3, 4);

    findCycle(n, e, g);
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
0 1 2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。