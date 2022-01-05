# 检查无向图中是否存在权重和为奇数的循环

> 原文:[https://www . geeksforgeeks . org/check-如果有一个带有奇数权重和的无向图循环/](https://www.geeksforgeeks.org/check-if-there-is-a-cycle-with-odd-weight-sum-in-an-undirected-graph/)

给定一个加权无向图，我们需要找到这个图中是否存在一个循环，使得这个循环中所有边的权重之和为奇数。
**例:**

```
Input : Number of vertices, n = 4, 
        Number of edges, m = 4
        Weighted Edges = 
        1 2 12
        2 3 1
        4 3 1
        4 1 20
Output : No! There is no odd weight 
         cycle in the given graph
```

![Cyclic graph](img/329521e040cdf64b6336a596ef6b3ef0.png)

```
Input : Number of vertices, n = 5, 
        Number of edges, m = 3
        Weighted Edges = 
        1 2 1
        3 2 1
        3 1 1
Output : Yes! There is an odd weight 
         cycle in the given graph
```

解决方案是基于这样一个事实，即“[如果一个图没有奇数长度的循环，那么它必须是二分的，即它可以用两种颜色](https://www.geeksforgeeks.org/check-graphs-cycle-odd-length/)”
着色。这个想法是将给定的问题转化为一个更简单的问题，我们只需要检查是否有奇数长度的循环。要转换，我们按照
进行

1.  将所有偶数权重边转换为单位权重的两条边。
2.  将所有奇数权重边转换为单位权重的单条边。

让我们为上面显示的图表制作另一个图表(在示例 1 中)

![cycle odd weight undirected graph](img/44b0a74c0e3caf9efd7c90c6dad30129.png)

这里，边[1 — 2]被分成两部分，这样[1-伪 1-2]引入了伪节点。我们这样做是为了我们的每个偶数加权边被考虑两次，而奇数加权边只被计算一次。当我们给我们的周期上色时，这样做将进一步帮助我们。我们用权重 1 分配所有边，然后用 2 色方法遍历整个图。现在我们开始只使用两种颜色给修改后的图着色。在具有偶数个节点的循环中，当我们仅使用两种颜色对其进行着色时，两个相邻的边都没有相同的颜色。而如果我们试着给一个有奇数个边的循环着色，肯定会出现两个相邻边有相同颜色的情况。这是我们的选择！因此，如果我们能够完全使用两种颜色对修改后的图进行着色，并且没有两个相邻的边被分配相同的颜色，那么图中必须没有循环或者有偶数个节点的循环。如果在给只有两种颜色的循环着色时出现任何冲突，那么我们的图中有一个奇数循环。

## C++

```
// C++ program to check if there is a cycle of
// total odd weight
#include <bits/stdc++.h>
using namespace std;

// This function returns true if the current subpart
// of the forest is two colorable, else false.
bool twoColorUtil(vector<int>G[], int src, int N,
                                  int colorArr[]) {

    // Assign first color to source
    colorArr[src] = 1;

    // Create a queue (FIFO) of vertex numbers and
    // enqueue source vertex for BFS traversal
    queue <int> q;
    q.push(src);

    // Run while there are vertices in queue
    // (Similar to BFS)
    while (!q.empty()){

        int u = q.front();
        q.pop();

        // Find all non-colored adjacent vertices
        for (int v = 0; v < G[u].size(); ++v){

            // An edge from u to v exists and
            // destination v is not colored
            if (colorArr[G[u][v]] == -1){

                // Assign alternate color to this
                // adjacent v of u
                colorArr[G[u][v]] = 1 - colorArr[u];
                q.push(G[u][v]);
            }

            //  An edge from u to v exists and destination
            // v is colored with same color as u
            else if (colorArr[G[u][v]] == colorArr[u])          
                return false;
        }
    }
    return true;
}

// This function returns true if graph G[V][V] is two
// colorable, else false      
bool twoColor(vector<int>G[], int N){

    // Create a color array to store colors assigned
    // to all vertices. Vertex number is used as index
    // in this array. The value '-1' of  colorArr[i]
    // is used to indicate that no color is assigned
    // to vertex 'i'.  The value 1 is used to indicate
    // first color is assigned and value 0 indicates
    // second color is assigned.
    int colorArr[N];
    for (int i = 1; i <= N; ++i)
        colorArr[i] = -1;

    // As we are dealing with graph, the input might
    // come as a forest, thus start coloring from a
    // node and if true is returned we'll know that
    // we successfully colored the subpart of our
    // forest and we start coloring again from a new
    // uncolored node. This way we cover the entire forest.
    for (int i = 1; i <= N; i++)
        if (colorArr[i] == -1)
           if (twoColorUtil(G, i, N, colorArr) == false)
             return false;

        return true;
}

// Returns false if an odd cycle is present else true
// int info[][] is the information about our graph
// int n is the number of nodes
// int m is the number of informations given to us
bool isOddSum(int info[][3],int n,int m){

    // Declaring adjacency list of a graph
    // Here at max, we can encounter all the edges with
    // even weight thus there will be 1 pseudo node
    // for each edge
    vector<int> G[2*n];

    int pseudo = n+1;
    int pseudo_count = 0;
    for (int i=0; i<m; i++){

        // For odd weight edges, we directly add it
        // in our graph
        if (info[i][2]%2 == 1){

            int u = info[i][0];
            int v = info[i][1];
            G[u].push_back(v);
            G[v].push_back(u);
        }

        // For even weight edges, we break it
        else{

            int u = info[i][0];
            int v = info[i][1];

            // Entering a pseudo node between u---v
            G[u].push_back(pseudo);
            G[pseudo].push_back(u);
            G[v].push_back(pseudo);
            G[pseudo].push_back(v);

            // Keeping a record of number of pseudo nodes
            // inserted
            pseudo_count++;

            // Making a new pseudo node for next time
            pseudo++;
        }
    }

    // We pass number graph G[][] and total number
    // of node = actual number of nodes + number of
    // pseudo nodes added.
    return twoColor(G,n+pseudo_count);
}

// Driver function
int main() {

    // 'n' correspond to number of nodes in our
    // graph while 'm' correspond to the number 
    // of information about this graph.
    int n = 4, m = 4;
    int info[4][3] = {{1, 2, 12},
                     {2, 3, 1},
                     {4, 3, 1},
                     {4, 1, 20}};

    // This function break the even weighted edges in
    // two parts. Makes the adjacency representation
    // of the graph and sends it for two coloring.
    if (isOddSum(info, n, m) == true)
        cout << "No\n";
    else
        cout << "Yes\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there is
// a cycle of total odd weight
import java.io.*;
import java.util.*;

class GFG
{

// This function returns true if the current subpart
// of the forest is two colorable, else false.
static boolean twoColorUtil(Vector<Integer>[] G,
                            int src, int N,
                            int[] colorArr)
{

    // Assign first color to source
    colorArr[src] = 1;

    // Create a queue (FIFO) of vertex numbers and
    // enqueue source vertex for BFS traversal
    Queue<Integer> q = new LinkedList<>();
    q.add(src);

    // Run while there are vertices in queue
    // (Similar to BFS)
    while (!q.isEmpty())
    {
        int u = q.peek();
        q.poll();

        // Find all non-colored adjacent vertices
        for (int v = 0; v < G[u].size(); ++v)
        {

            // An edge from u to v exists and
            // destination v is not colored
            if (colorArr[G[u].elementAt(v)] == -1)
            {

                // Assign alternate color to this
                // adjacent v of u
                colorArr[G[u].elementAt(v)] = 1 - colorArr[u];
                q.add(G[u].elementAt(v));
            }

            // An edge from u to v exists and destination
            // v is colored with same color as u
            else if (colorArr[G[u].elementAt(v)] == colorArr[u])
                return false;
        }
    }
    return true;
}

// This function returns true if
// graph G[V][V] is two colorable, else false
static boolean twoColor(Vector<Integer>[] G, int N)
{

    // Create a color array to store colors assigned
    // to all vertices. Vertex number is used as index
    // in this array. The value '-1' of colorArr[i]
    // is used to indicate that no color is assigned
    // to vertex 'i'. The value 1 is used to indicate
    // first color is assigned and value 0 indicates
    // second color is assigned.
    int[] colorArr = new int[N + 1];
    for (int i = 1; i <= N; ++i)
        colorArr[i] = -1;

    // As we are dealing with graph, the input might
    // come as a forest, thus start coloring from a
    // node and if true is returned we'll know that
    // we successfully colored the subpart of our
    // forest and we start coloring again from a new
    // uncolored node. This way we cover the entire forest.
    for (int i = 1; i <= N; i++)
        if (colorArr[i] == -1)
            if (twoColorUtil(G, i, N, colorArr) == false)
                return false;

    return true;
}

// Returns false if an odd cycle is present else true
// int info[][] is the information about our graph
// int n is the number of nodes
// int m is the number of informations given to us
static boolean isOddSum(int[][] info, int n, int m)
{

    // Declaring adjacency list of a graph
    // Here at max, we can encounter all the edges with
    // even weight thus there will be 1 pseudo node
    // for each edge
    //@SuppressWarnings("unchecked")
    Vector<Integer>[] G = new Vector[2 * n];

    for (int i = 0; i < 2 * n; i++)
        G[i] = new Vector<>();

    int pseudo = n + 1;
    int pseudo_count = 0;
    for (int i = 0; i < m; i++)
    {

        // For odd weight edges, we directly add it
        // in our graph
        if (info[i][2] % 2 == 1)
        {
            int u = info[i][0];
            int v = info[i][1];
            G[u].add(v);
            G[v].add(u);
        }

        // For even weight edges, we break it
        else
        {
            int u = info[i][0];
            int v = info[i][1];

            // Entering a pseudo node between u---v
            G[u].add(pseudo);
            G[pseudo].add(u);
            G[v].add(pseudo);
            G[pseudo].add(v);

            // Keeping a record of number of
            // pseudo nodes inserted
            pseudo_count++;

            // Making a new pseudo node for next time
            pseudo++;
        }
    }

    // We pass number graph G[][] and total number
    // of node = actual number of nodes + number of
    // pseudo nodes added.
    return twoColor(G, n + pseudo_count);
}

// Driver Code
public static void main(String[] args)
{
    // 'n' correspond to number of nodes in our
    // graph while 'm' correspond to the number
    // of information about this graph.
    int n = 4, m = 3;
    int[][] info = { { 1, 2, 12 }, { 2, 3, 1 },
                     { 4, 3, 1 }, { 4, 1, 20 } };

    // This function break the even weighted edges in
    // two parts. Makes the adjacency representation
    // of the graph and sends it for two coloring.
    if (isOddSum(info, n, m) == true)
        System.out.println("No");
    else
        System.out.println("Yes");
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to check if there
# is a cycle of total odd weight

# This function returns true if the current subpart
# of the forest is two colorable, else false.
def twoColorUtil(G, src, N, colorArr): 

    # Assign first color to source
    colorArr[src] = 1

    # Create a queue (FIFO) of vertex numbers and
    # enqueue source vertex for BFS traversal
    q = [src]

    # Run while there are vertices in queue
    # (Similar to BFS)
    while len(q) > 0:

        u = q.pop(0)

        # Find all non-colored adjacent vertices
        for v in range(0, len(G[u])):

            # An edge from u to v exists and
            # destination v is not colored
            if colorArr[G[u][v]] == -1:

                # Assign alternate color to this
                # adjacent v of u
                colorArr[G[u][v]] = 1 - colorArr[u]
                q.append(G[u][v])

            # An edge from u to v exists and destination
            # v is colored with same color as u
            elif colorArr[G[u][v]] == colorArr[u]:        
                return False

    return True

# This function returns true if graph
# G[V][V] is two colorable, else false    
def twoColor(G, N):

    # Create a color array to store colors assigned
    # to all vertices. Vertex number is used as index
    # in this array. The value '-1' of colorArr[i]
    # is used to indicate that no color is assigned
    # to vertex 'i'. The value 1 is used to indicate
    # first color is assigned and value 0 indicates
    # second color is assigned.
    colorArr = [-1] * N

    # As we are dealing with graph, the input might
    # come as a forest, thus start coloring from a
    # node and if true is returned we'll know that
    # we successfully colored the subpart of our
    # forest and we start coloring again from a new
    # uncolored node. This way we cover the entire forest.
    for i in range(N):
        if colorArr[i] == -1:
            if twoColorUtil(G, i, N, colorArr) == False:
                return False

            return True

# Returns false if an odd cycle is present else true
# int info[][] is the information about our graph
# int n is the number of nodes
# int m is the number of informations given to us
def isOddSum(info, n, m):

    # Declaring adjacency list of a graph
    # Here at max, we can encounter all the
    # edges with even weight thus there will
    # be 1 pseudo node for each edge
    G = [[] for i in range(2*n)]

    pseudo, pseudo_count = n+1, 0
    for i in range(0, m):

        # For odd weight edges, we
        # directly add it in our graph
        if info[i][2] % 2 == 1:

            u, v = info[i][0], info[i][1]
            G[u].append(v)
            G[v].append(u)

        # For even weight edges, we break it
        else:
            u, v = info[i][0], info[i][1]

            # Entering a pseudo node between u---v
            G[u].append(pseudo)
            G[pseudo].append(u)
            G[v].append(pseudo)
            G[pseudo].append(v)

            # Keeping a record of number
            # of pseudo nodes inserted
            pseudo_count += 1

            # Making a new pseudo node for next time
            pseudo += 1

    # We pass number graph G[][] and total number
    # of node = actual number of nodes + number of
    # pseudo nodes added.
    return twoColor(G, n+pseudo_count)

# Driver function
if __name__ == "__main__": 

    # 'n' correspond to number of nodes in our
    # graph while 'm' correspond to the number
    # of information about this graph.
    n, m = 4, 3
    info = [[1, 2, 12],
            [2, 3, 1],
            [4, 3, 1],
            [4, 1, 20]]

    # This function break the even weighted edges in
    # two parts. Makes the adjacency representation
    # of the graph and sends it for two coloring.
    if isOddSum(info, n, m) == True:
        print("No")
    else:
        print("Yes")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to check if there is
// a cycle of total odd weight
using System;
using System.Collections.Generic;

class GFG
{

// This function returns true if the current subpart
// of the forest is two colorable, else false.
static bool twoColorUtil(List<int>[] G,
                        int src, int N,
                        int[] colorArr)
{

    // Assign first color to source
    colorArr[src] = 1;

    // Create a queue (FIFO) of vertex numbers and
    // enqueue source vertex for BFS traversal
    List<int> q = new List<int>();
    q.Add(src);

    // Run while there are vertices in queue
    // (Similar to BFS)
    while (q.Count != 0)
    {
        int u = q[0];
        q.RemoveAt(0);

        // Find all non-colored adjacent vertices
        for (int v = 0; v < G[u].Count; ++v)
        {

            // An edge from u to v exists and
            // destination v is not colored
            if (colorArr[G[u][v]] == -1)
            {

                // Assign alternate color to this
                // adjacent v of u
                colorArr[G[u][v]] = 1 - colorArr[u];
                q.Add(G[u][v]);
            }

            // An edge from u to v exists and destination
            // v is colored with same color as u
            else if (colorArr[G[u][v]] == colorArr[u])
                return false;
        }
    }
    return true;
}

// This function returns true if
// graph G[V,V] is two colorable, else false
static bool twoColor(List<int>[] G, int N)
{

    // Create a color array to store colors assigned
    // to all vertices. Vertex number is used as index
    // in this array. The value '-1' of colorArr[i]
    // is used to indicate that no color is assigned
    // to vertex 'i'. The value 1 is used to indicate
    // first color is assigned and value 0 indicates
    // second color is assigned.
    int[] colorArr = new int[N + 1];
    for (int i = 1; i <= N; ++i)
        colorArr[i] = -1;

    // As we are dealing with graph, the input might
    // come as a forest, thus start coloring from a
    // node and if true is returned we'll know that
    // we successfully colored the subpart of our
    // forest and we start coloring again from a new
    // uncolored node. This way we cover the entire forest.
    for (int i = 1; i <= N; i++)
        if (colorArr[i] == -1)
            if (twoColorUtil(G, i, N, colorArr) == false)
                return false;

    return true;
}

// Returns false if an odd cycle is present else true
// int info[,] is the information about our graph
// int n is the number of nodes
// int m is the number of informations given to us
static bool isOddSum(int[,] info, int n, int m)
{

    // Declaring adjacency list of a graph
    // Here at max, we can encounter all the edges with
    // even weight thus there will be 1 pseudo node
    // for each edge
    //@SuppressWarnings("unchecked")
    List<int>[] G = new List<int>[2 * n];

    for (int i = 0; i < 2 * n; i++)
        G[i] = new List<int>();

    int pseudo = n + 1;
    int pseudo_count = 0;
    for (int i = 0; i < m; i++)
    {

        // For odd weight edges, we directly add it
        // in our graph
        if (info[i, 2] % 2 == 1)
        {
            int u = info[i, 0];
            int v = info[i, 1];
            G[u].Add(v);
            G[v].Add(u);
        }

        // For even weight edges, we break it
        else
        {
            int u = info[i, 0];
            int v = info[i, 1];

            // Entering a pseudo node between u---v
            G[u].Add(pseudo);
            G[pseudo].Add(u);
            G[v].Add(pseudo);
            G[pseudo].Add(v);

            // Keeping a record of number of
            // pseudo nodes inserted
            pseudo_count++;

            // Making a new pseudo node for next time
            pseudo++;
        }
    }

    // We pass number graph G[,] and total number
    // of node = actual number of nodes + number of
    // pseudo nodes added.
    return twoColor(G, n + pseudo_count);
}

// Driver Code
public static void Main(String[] args)
{
    // 'n' correspond to number of nodes in our
    // graph while 'm' correspond to the number
    // of information about this graph.
    int n = 4, m = 3;
    int[,] info = { { 1, 2, 12 }, { 2, 3, 1 },
                    { 4, 3, 1 }, { 4, 1, 20 } };

    // This function break the even weighted edges in
    // two parts. Makes the adjacency representation
    // of the graph and sends it for two coloring.
    if (isOddSum(info, n, m) == true)
        Console.WriteLine("No");
    else
        Console.WriteLine("Yes");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to check if there is
// a cycle of total odd weight

// This function returns true if the current subpart
// of the forest is two colorable, else false.
function twoColorUtil(G, src, N, colorArr)
{

    // Assign first color to source
    colorArr[src] = 1;

    // Create a queue (FIFO) of vertex numbers and
    // enqueue source vertex for BFS traversal
    var q = [];
    q.push(src);

    // Run while there are vertices in queue
    // (Similar to BFS)
    while (q.length != 0)
    {
        var u = q[0];
        q.shift();

        // Find all non-colored adjacent vertices
        for (var v = 0; v < G[u].length; ++v)
        {

            // An edge from u to v exists and
            // destination v is not colored
            if (colorArr[G[u][v]] == -1)
            {

                // Assign alternate color to this
                // adjacent v of u
                colorArr[G[u][v]] = 1 - colorArr[u];
                q.push(G[u][v]);
            }

            // An edge from u to v exists and destination
            // v is colored with same color as u
            else if (colorArr[G[u][v]] == colorArr[u])
                return false;
        }
    }
    return true;
}

// This function returns true if
// graph G[V,V] is two colorable, else false
function twoColor(G, N)
{

    // Create a color array to store colors assigned
    // to all vertices. Vertex number is used as index
    // in this array. The value '-1' of colorArr[i]
    // is used to indicate that no color is assigned
    // to vertex 'i'. The value 1 is used to indicate
    // first color is assigned and value 0 indicates
    // second color is assigned.
    var colorArr =  Array(N+1).fill(-1);

    // As we are dealing with graph, the input might
    // come as a forest, thus start coloring from a
    // node and if true is returned we'll know that
    // we successfully colored the subpart of our
    // forest and we start coloring again from a new
    // uncolored node. This way we cover the entire forest.
    for (var i = 1; i <= N; i++)
        if (colorArr[i] == -1)
            if (twoColorUtil(G, i, N, colorArr) == false)
                return false;

    return true;
}

// Returns false if an odd cycle is present else true
// int info[,] is the information about our graph
// int n is the number of nodes
// int m is the number of informations given to us
function isOddSum(info, n, m)
{

    // Declaring adjacency list of a graph
    // Here at max, we can encounter all the edges with
    // even weight thus there will be 1 pseudo node
    // for each edge
    //@SuppressWarnings("unchecked")
    var G =  Array.from(Array(2*n), ()=>Array());

    var pseudo = n + 1;
    var pseudo_count = 0;

    for (var i = 0; i < m; i++)
    {

        // For odd weight edges, we directly add it
        // in our graph
        if (info[i][2] % 2 == 1)
        {
            var u = info[i][0];
            var v = info[i][1];
            G[u].push(v);
            G[v].push(u);
        }

        // For even weight edges, we break it
        else
        {
            var u = info[i][0];
            var v = info[i][1];

            // Entering a pseudo node between u---v
            G[u].push(pseudo);
            G[pseudo].push(u);
            G[v].push(pseudo);
            G[pseudo].push(v);

            // Keeping a record of number of
            // pseudo nodes inserted
            pseudo_count++;

            // Making a new pseudo node for next time
            pseudo++;
        }
    }

    // We pass number graph G[,] and total number
    // of node = actual number of nodes + number of
    // pseudo nodes added.
    return twoColor(G, n + pseudo_count);
}

// Driver Code
// 'n' correspond to number of nodes in our
// graph while 'm' correspond to the number
// of information about this graph.
var n = 4, m = 3;
var info = [ [ 1, 2, 12 ], [ 2, 3, 1 ],
                [ 4, 3, 1 ], [ 4, 1, 20 ] ];
// This function break the even weighted edges in
// two parts. Makes the adjacency representation
// of the graph and sends it for two coloring.
if (isOddSum(info, n, m) == true)
    document.write("No");
else
    document.write("Yes");

</script>
```

**输出:**

```
No
```

本文由 **Parth Trehan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。