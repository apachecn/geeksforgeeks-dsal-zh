# 使用 Floyd Warshall

检测负周期

> 原文： [https://www.geeksforgeeks.org/detecting-negative-cycle-using-floyd-warshall/](https://www.geeksforgeeks.org/detecting-negative-cycle-using-floyd-warshall/)

我们得到一个有向图。 我们需要计算图是否具有负周期。 负周期是指周期总和为负的周期。

![negative_cycle](img/425a4d791640aa1b3e6d0c72a65b71dd.png)

在图表的各种应用中都可以找到负权重。 例如，如果您沿着路径行进，则无需为路径付费，而可以得到一些好处。

例子：

```
Input : 4 4
        0 1 1
        1 2 -1
        2 3 -1
        3 0 -1

Output : Yes
The graph contains a negative cycle.

```

我们已经讨论了基于 [Bellman Ford 算法](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/)的解决方案。

在本文中，将讨论基于 [Floyd Warshall 算法](https://www.geeksforgeeks.org/dynamic-programming-set-16-floyd-warshall-algorithm/)的解决方案，该解决方案可用于连接图和断开图。

任何节点与自身的距离始终为零。 但是在某些情况下，如本例所示，当我们进一步从 4 遍历到 1 时，距离变为-2，即 1 与 1 的距离变为-2。 这是我们的收获，我们只需要检查节点与自身的距离，如果结果为负，我们将检测到所需的负周期。

## C++

```cpp

// C++ Program to check if there is a negative weight 
// cycle using Floyd Warshall Algorithm 
#include<bits/stdc++.h> 
using namespace std; 

// Number of vertices in the graph 
#define V 4 

/* Define Infinite as a large enough value. This  
   value will be used for vertices not connected  
   to each other */
#define INF 99999 

// A function to print the solution matrix 
void printSolution(int dist[][V]); 

// Returns true if graph has negative weight cycle 
// else false. 
bool negCyclefloydWarshall(int graph[][V]) 
{ 
    /* dist[][] will be the output matrix that will  
       finally have the shortest  
    distances between every pair of vertices */
    int dist[V][V], i, j, k; 

    /* Initialize the solution matrix same as input 
      graph matrix. Or we can say the initial values  
      of shortest distances are based on shortest  
      paths considering no intermediate vertex. */
    for (i = 0; i < V; i++) 
        for (j = 0; j < V; j++) 
            dist[i][j] = graph[i][j]; 

    /* Add all vertices one by one to the set of  
       intermediate vertices. 
    ---> Before start of a iteration, we have shortest 
         distances between all pairs of vertices such  
         that the shortest distances consider only the 
         vertices in set {0, 1, 2, .. k-1} as intermediate  
         vertices. 
    ----> After the end of a iteration, vertex no. k is  
          added to the set of intermediate vertices and  
          the set becomes {0, 1, 2, .. k} */
    for (k = 0; k < V; k++) 
    { 
        // Pick all vertices as source one by one 
        for (i = 0; i < V; i++) 
        { 
            // Pick all vertices as destination for the 
            // above picked source 
            for (j = 0; j < V; j++) 
            { 
                // If vertex k is on the shortest path from 
                // i to j, then update the value of dist[i][j] 
                if (dist[i][k] + dist[k][j] < dist[i][j]) 
                        dist[i][j] = dist[i][k] + dist[k][j]; 
            } 
        } 
    } 

    // If distance of any verex from itself 
    // becomes negative, then there is a negative 
    // weight cycle. 
    for (int i = 0; i < V; i++) 
        if (dist[i][i] < 0) 
            return true; 
    return false;  
} 

 // driver program 
int main() 
{ 
    /* Let us create the following weighted graph 
            1 
    (0)----------->(1) 
    /|\             | 
     |              | 
  -1 |              | -1 
     |             \|/ 
    (3)<-----------(2) 
        -1       */

    int graph[V][V] = { {0   , 1   , INF , INF}, 
                        {INF , 0   , -1  , INF}, 
                        {INF , INF , 0   ,  -1}, 
                        {-1  , INF , INF ,   0}}; 

    if (negCyclefloydWarshall(graph)) 
       cout << "Yes"; 
    else
       cout << "No";  
    return 0; 
} 

```

## Java

```java

// Java Program to check if there is a negative weight 
// cycle using Floyd Warshall Algorithm 
class GFG 
{ 

    // Number of vertices in the graph 
    static final int V = 4; 

    /* Define Infinite as a large enough value. This  
    value will be used for vertices not connected  
    to each other */
    static final int INF = 99999; 

    // Returns true if graph has negative weight cycle 
    // else false. 
    static boolean negCyclefloydWarshall(int graph[][]) 
    { 

        /* dist[][] will be the output matrix that will  
        finally have the shortest  
        distances between every pair of vertices */
        int dist[][] = new int[V][V], i, j, k; 

        /* Initialize the solution matrix same as input 
        graph matrix. Or we can say the initial values  
        of shortest distances are based on shortest  
        paths considering no intermediate vertex. */
        for (i = 0; i < V; i++) 
            for (j = 0; j < V; j++) 
                dist[i][j] = graph[i][j]; 

        /* Add all vertices one by one to the set of  
        intermediate vertices. 
        ---> Before start of a iteration, we have shortest 
            distances between all pairs of vertices such  
            that the shortest distances consider only the 
            vertices in set {0, 1, 2, .. k-1} as intermediate  
            vertices. 
        ----> After the end of a iteration, vertex no. k is  
            added to the set of intermediate vertices and  
            the set becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++) 
        { 

            // Pick all vertices as source one by one 
            for (i = 0; i < V; i++) 
            { 

                // Pick all vertices as destination for the 
                // above picked source 
                for (j = 0; j < V; j++) 
                { 

                    // If vertex k is on the shortest path from 
                    // i to j, then update the value of dist[i][j] 
                    if (dist[i][k] + dist[k][j] < dist[i][j]) 
                            dist[i][j] = dist[i][k] + dist[k][j]; 
                } 
            } 
        } 

        // If distance of any verex from itself 
        // becomes negative, then there is a negative 
        // weight cycle. 
        for (i = 0; i < V; i++) 
            if (dist[i][i] < 0) 
                return true; 

        return false;  
    } 

    // Driver code 
    public static void main (String[] args) 
    { 

    /* Let us create the following weighted graph 
                1 
        (0)----------->(1) 
        /|\               | 
         |               | 
      -1 |               | -1 
         |                \|/ 
        (3)<-----------(2) 
            -1     */

        int graph[][] = { {0, 1, INF, INF}, 
                          {INF, 0, -1, INF}, 
                          {INF, INF, 0, -1}, 
                          {-1, INF, INF, 0}}; 

        if (negCyclefloydWarshall(graph)) 
            System.out.print("Yes"); 
        else
            System.out.print("No");  
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python

```py

# Python Program to check 
# if there is a 
# negative weight 
# cycle using Floyd 
# Warshall Algorithm 

# Number of vertices 
# in the graph 
V = 4

# Define Infinite as a 
# large enough value. This  
# value will be used  
#for vertices not connected  
# to each other  
INF = 99999

# Returns true if graph has 
# negative weight cycle 
# else false. 
def negCyclefloydWarshall(graph): 

    # dist[][] will be the 
    # output matrix that will  
    # finally have the shortest  
    # distances between every 
    # pair of vertices  
    dist=[[0 for i in range(V+1)]for j in range(V+1)] 

    # Initialize the solution 
    # matrix same as input 
    # graph matrix. Or we can 
    # say the initial values  
    # of shortest distances 
    # are based on shortest  
    # paths considering no 
    # intermediate vertex.  
    for i in range(V): 
        for j in range(V): 
            dist[i][j] = graph[i][j] 

    ''' Add all vertices one 
        by one to the set of  
        intermediate vertices. 
    ---> Before start of a iteration, 
         we have shortest 
        distances between all pairs 
        of vertices such  
        that the shortest distances 
        consider only the 
        vertices in set {0, 1, 2, .. k-1} 
        as intermediate vertices. 
    ----> After the end of a iteration, 
          vertex no. k is  
        added to the set of 
        intermediate vertices and  
        the set becomes {0, 1, 2, .. k} '''
    for k in range(V): 

        # Pick all vertices  
        # as source one by one 
        for i in range(V): 

            # Pick all vertices as 
            # destination for the 
            # above picked source 
            for j in range(V): 

                # If vertex k is on 
                # the shortest path from 
                # i to j, then update 
                # the value of dist[i][j] 
                if (dist[i][k] + dist[k][j] < dist[i][j]): 
                        dist[i][j] = dist[i][k] + dist[k][j] 

    # If distance of any 
    # vertex from itself 
    # becomes negative, then 
    # there is a negative 
    # weight cycle. 
    for i in range(V): 
        if (dist[i][i] < 0): 
            return True

    return False 

# Driver code 

''' Let us create the 
    following weighted graph 
            1 
    (0)----------->(1) 
    /|\               | 
     |               | 
  -1 |               | -1 
     |                \|/ 
    (3)<-----------(2) 
        -1     '''

graph = [ [0, 1, INF, INF], 
          [INF, 0, -1, INF], 
          [INF, INF, 0, -1], 
          [-1, INF, INF, 0]] 

if (negCyclefloydWarshall(graph)): 
    print("Yes") 
else: 
    print("No")  

# This code is contributed 
# by Anant Agarwal. 

```

## C#

```cs

// C# Program to check if there 
// is a negative weight cycle 
// using Floyd Warshall Algorithm 

using System; 

namespace Cycle 
{ 
public class GFG 
{      

    // Number of vertices in the graph 
    static int V = 4; 

    /* Define Infinite as a large enough value. This  
    value will be used for vertices not connected  
    to each other */
    static int INF = 99999; 

    // Returns true if graph has negative weight cycle 
    // else false. 
    static bool negCyclefloydWarshall(int [,]graph) 
    { 

        /* dist[][] will be the output matrix that will  
        finally have the shortest  
        distances between every pair of vertices */
        int [,]dist = new int[V,V]; 
        int i, j, k; 

        /* Initialize the solution matrix same as input 
        graph matrix. Or we can say the initial values  
        of shortest distances are based on shortest  
        paths considering no intermediate vertex. */
        for (i = 0; i < V; i++) 
            for (j = 0; j < V; j++) 
                dist[i,j] = graph[i,j]; 

        /* Add all vertices one by one to the set of  
        intermediate vertices. 
        ---> Before start of a iteration, we have shortest 
            distances between all pairs of vertices such  
            that the shortest distances consider only the 
            vertices in set {0, 1, 2, .. k-1} as intermediate  
            vertices. 
        ----> After the end of a iteration, vertex no. k is  
            added to the set of intermediate vertices and  
            the set becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++) 
        { 

            // Pick all vertices as source one by one 
            for (i = 0; i < V; i++) 
            { 

                // Pick all vertices as destination for the 
                // above picked source 
                for (j = 0; j < V; j++) 
                { 

                    // If vertex k is on the shortest path from 
                    // i to j, then update the value of dist[i][j] 
                    if (dist[i,k] + dist[k,j] < dist[i,j]) 
                            dist[i,j] = dist[i,k] + dist[k,j]; 
                } 
            } 
        } 

        // If distance of any verex from itself 
        // becomes negative, then there is a negative 
        // weight cycle. 
        for (i = 0; i < V; i++) 
            if (dist[i,i] < 0) 
                return true; 

        return false;  
    } 

    // Driver code 
    public static void Main() 
    { 

    /* Let us create the following weighted graph 
                1 
        (0)----------->(1) 
        /|\             | 
        |             | 
    -1 |             | -1 
        |             \|/ 
        (3)<-----------(2) 
            -1     */

        int [,]graph = { {0, 1, INF, INF}, 
                        {INF, 0, -1, INF}, 
                        {INF, INF, 0, -1}, 
                        {-1, INF, INF, 0}}; 

        if (negCyclefloydWarshall(graph)) 
            Console.Write("Yes"); 
        else
            Console.Write("No");  
    } 
}  
} 

// This code is contributed by Sam007\. 

```

Output:

```
Yes

```

本文由 [**Shivani Mittal**](https://auth.geeksforgeeks.org/profile.php?user=shivani.mittal&list=practice) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

