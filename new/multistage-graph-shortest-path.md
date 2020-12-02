# 多阶段图（最短路径）

> 原文： [https://www.geeksforgeeks.org/multistage-graph-shortest-path/](https://www.geeksforgeeks.org/multistage-graph-shortest-path/)

**多阶段图**是有向图，其中的节点可以划分为一组阶段，从而所有边仅是从一个阶段到下一个阶段（换句话说，同一阶段的顶点之间没有边缘） 从当前阶段的顶点到上一阶段）。

我们提供了一个多阶段图，一个源和一个目标，我们需要找到从源到目标的最短路径。 按照惯例，我们将第 1 阶段的源视为最后一个阶段。

以下是我们将在本文中考虑的示例图：-
![](img/6b9b89e1caa76f1eee293f38b7ee9098.png)

现在有多种策略可以应用：

*   **蛮力**方法，用于查找源和目标之间的所有可能路径，然后找到最小值。 那是最糟糕的策略。
*   **Dijkstra 的单一来源最短路径算法**。 此方法将查找从源到所有其他节点的最短路径，在这种情况下不需要。 因此，这将花费大量时间，并且甚至没有使用此多阶段图所具有的 SPECIAL 功能。
*   **简单贪婪方法** –在每个节点上，选择最短的传出路径。 如果将这种方法应用于上面给出的示例图，我们得到的解为 1 + 4 + 18 =23。但是快速浏览该图将显示比 23 更短的路径。因此，贪婪方法失败了！
*   最好的选择是动态编程。 因此，我们需要找到**最优子结构，递归方程和重叠子问题。**

**最佳子结构和递归方程：-**
 **我们定义表示法：-M（x，y）是从阶段 x，节点 y 到 T（目标节点）的最小成本 。**

 **```
Shortest distance from stage 1, node 0 to 
destination, i.e., 7 is M(1, 0).

// From 0, we can go to 1 or 2 or 3 to
// reach 7\.              
M(1, 0) = min(1 + M(2, 1),
              2 + M(2, 2),
              5 + M(2, 3))

```

这意味着我们的 0-> 7 问题现在细分为 3 个子问题：

```
So if we have total 'n' stages and target
as T, then the stopping condition  will be :-
M(n-1, i) = i ---> T + M(n, T) = i ---> T

```

**递归树和重叠子问题：-**
因此，M（x，y）评估的层次结构看起来像这样：-

```
In M(i, j), i is stage number and
j is node number

                   M(1, 0)
           /          |         \                             
          /           |          \                            
       M(2, 1)      M(2, 2)        M(2, 3)
    /      \        /     \         /    \
M(3, 4)  M(3, 5)  M(3, 4)  M(3, 5) M(3, 6)  M(3, 6)
 .         .       .       .          .        .
 .         .       .       .          .        .
 .         .       .       .          .        .

```

因此，在这里我们绘制了递归树的一小部分，并且我们已经可以看到重叠子问题。 我们可以使用动态编程大大减少 M（x，y）个评估的数量。

**实现细节**：
以下实现假定从第一阶段（源）到最后阶段（目标）从 0 到 N-1 编号节点。 我们还假设输入图是多阶段的。

## C++

```cpp

// CPP program to find shortest distance 
// in a multistage graph. 
#include<bits/stdc++.h> 
using namespace std; 

#define N 8 
#define INF INT_MAX 

// Returns shortest distance from 0 to 
// N-1\. 
int shortestDist(int graph[N][N]) { 

    // dist[i] is going to store shortest 
    // distance from node i to node N-1\. 
    int dist[N]; 

    dist[N-1] = 0; 

    // Calculating shortest path for 
    // rest of the nodes 
    for (int i = N-2 ; i >= 0 ; i--) 
    { 

        // Initialize distance from i to 
        // destination (N-1) 
        dist[i] = INF; 

        // Check all nodes of next stages 
        // to find shortest distance from 
        // i to N-1\. 
        for (int j = i ; j < N ; j++) 
        { 
            // Reject if no edge exists 
            if (graph[i][j] == INF) 
                continue; 

            // We apply recursive equation to 
            // distance to target through j. 
            // and compare with minimum distance  
            // so far. 
            dist[i] = min(dist[i], graph[i][j] + 
                                        dist[j]); 
        } 
    } 

    return dist[0]; 
} 

// Driver code 
int main() 
{ 
    // Graph stored in the form of an 
    // adjacency Matrix 
    int graph[N][N] = 
      {{INF, 1, 2, 5, INF, INF, INF, INF}, 
       {INF, INF, INF, INF, 4, 11, INF, INF}, 
       {INF, INF, INF, INF, 9, 5, 16, INF}, 
       {INF, INF, INF, INF, INF, INF, 2, INF}, 
       {INF, INF, INF, INF, INF, INF, INF, 18}, 
       {INF, INF, INF, INF, INF, INF, INF, 13}, 
       {INF, INF, INF, INF, INF, INF, INF, 2}}; 

    cout << shortestDist(graph); 
    return 0; 
} 

```

## Java

```java

// Java program to find shortest distance  
// in a multistage graph. 
class GFG  
{ 

    static int N = 8; 
    static int INF = Integer.MAX_VALUE; 

    // Returns shortest distance from 0 to  
    // N-1.  
    public static int shortestDist(int[][] graph)  
    { 

        // dist[i] is going to store shortest  
        // distance from node i to node N-1.  
        int[] dist = new int[N]; 

        dist[N - 1] = 0; 

        // Calculating shortest path for  
        // rest of the nodes  
        for (int i = N - 2; i >= 0; i--)  
        { 

            // Initialize distance from i to  
            // destination (N-1)  
            dist[i] = INF; 

            // Check all nodes of next stages  
            // to find shortest distance from  
            // i to N-1.  
            for (int j = i; j < N; j++)  
            { 
                // Reject if no edge exists  
                if (graph[i][j] == INF)  
                { 
                    continue; 
                } 

                // We apply recursive equation to  
                // distance to target through j.  
                // and compare with minimum distance  
                // so far.  
                dist[i] = Math.min(dist[i], graph[i][j] 
                        + dist[j]); 
            } 
        } 

        return dist[0]; 
    } 

    // Driver code  
    public static void main(String[] args)  
    { 
        // Graph stored in the form of an  
        // adjacency Matrix  
        int[][] graph = new int[][]{{INF, 1, 2, 5, INF, INF, INF, INF}, 
        {INF, INF, INF, INF, 4, 11, INF, INF}, 
        {INF, INF, INF, INF, 9, 5, 16, INF}, 
        {INF, INF, INF, INF, INF, INF, 2, INF}, 
        {INF, INF, INF, INF, INF, INF, INF, 18}, 
        {INF, INF, INF, INF, INF, INF, INF, 13}, 
        {INF, INF, INF, INF, INF, INF, INF, 2}}; 

        System.out.println(shortestDist(graph)); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

## Python

```py

# Python3 program to find shortest  
# distance in a multistage graph.  

# Returns shortest distance from  
# 0 to N-1.  
def shortestDist(graph): 
    global INF 

    # dist[i] is going to store shortest  
    # distance from node i to node N-1.  
    dist = [0] * N  

    dist[N - 1] = 0

    # Calculating shortest path  
    # for rest of the nodes  
    for i in range(N - 2, -1, -1): 

        # Initialize distance from   
        # i to destination (N-1)  
        dist[i] = INF  

        # Check all nodes of next stages  
        # to find shortest distance from  
        # i to N-1\. 
        for j in range(N): 

            # Reject if no edge exists  
            if graph[i][j] == INF: 
                continue

            # We apply recursive equation to  
            # distance to target through j.  
            # and compare with minimum  
            # distance so far.  
            dist[i] = min(dist[i],  
                          graph[i][j] + dist[j]) 

    return dist[0] 

# Driver code  
N = 8
INF = 999999999999

# Graph stored in the form of an  
# adjacency Matrix  
graph = [[INF, 1, 2, 5, INF, INF, INF, INF],  
         [INF, INF, INF, INF, 4, 11, INF, INF],  
         [INF, INF, INF, INF, 9, 5, 16, INF],  
         [INF, INF, INF, INF, INF, INF, 2, INF],  
         [INF, INF, INF, INF, INF, INF, INF, 18], 
         [INF, INF, INF, INF, INF, INF, INF, 13],  
         [INF, INF, INF, INF, INF, INF, INF, 2]]  

print(shortestDist(graph)) 

# This code is contributed by PranchalK 

```

## C#

```cs

// C# program to find shortest distance  
// in a multistage graph. 
using System;  

class GFG  
{  
    static int N = 8;  
    static int INF = int.MaxValue;  

    // Returns shortest distance from 0 to  
    // N-1.  
    public static int shortestDist(int[,] graph) {  

        // dist[i] is going to store shortest  
        // distance from node i to node N-1.  
        int[] dist = new int[N];  

        dist[N-1] = 0;  

        // Calculating shortest path for  
        // rest of the nodes  
        for (int i = N-2 ; i >= 0 ; i--)  
        {  

            // Initialize distance from i to  
            // destination (N-1)  
            dist[i] = INF;  

            // Check all nodes of next stages  
            // to find shortest distance from  
            // i to N-1.  
            for (int j = i ; j < N ; j++)  
            {  
                // Reject if no edge exists  
                if (graph[i,j] == INF)  
                    continue;  

                // We apply recursive equation to  
                // distance to target through j.  
                // and compare with minimum distance   
                // so far.  
                dist[i] = Math.Min(dist[i], graph[i,j] +  
                                            dist[j]);  
            }  
        }  

        return dist[0];  
    }  

    // Driver code  
    static void Main()  
    {  
        // Graph stored in the form of an  
        // adjacency Matrix  
        int[,] graph = new int[,]  
          {{INF, 1, 2, 5, INF, INF, INF, INF},  
           {INF, INF, INF, INF, 4, 11, INF, INF},  
           {INF, INF, INF, INF, 9, 5, 16, INF},  
           {INF, INF, INF, INF, INF, INF, 2, INF},  
           {INF, INF, INF, INF, INF, INF, INF, 18},  
           {INF, INF, INF, INF, INF, INF, INF, 13},  
           {INF, INF, INF, INF, INF, INF, INF, 2}};  

        Console.Write(shortestDist(graph)); 
    } 
} 

// This code is contributed by DrRoot_ 

```

**Output:**

```
9

```

**时间复杂度**：O（n <sup>2</sup> ）

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。**