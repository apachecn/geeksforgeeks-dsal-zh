# 使用 Bellman Ford 算法

从图的最小成本最大流

> 原文： [https://www.geeksforgeeks.org/minimum-cost-maximum-flow-from-a-graph-using-bellman-ford-algorithm/](https://www.geeksforgeeks.org/minimum-cost-maximum-flow-from-a-graph-using-bellman-ford-algorithm/)

给定一个源节点 **S，**一个宿节点`T`，两个矩阵 **Cap [] []** 和 **Cost [] []** 图，其中 **Cap [i] [j]** 是从节点`i`到节点`j`和 **cost [i] [ j]** 是从节点`i`到节点`j`沿着有向边发送一个单位流的成本，任务是查找成本最小最大值的流 给定图的-flow 可能。

> **最小成本最大流量**：从给定图表中提供最大流量所需的最小成本（每单位流量）。

**示例**：

> **输入**：S = 0，T = 4，cap [] [] = {{0，3，4，5，0}，{0，0，2，0，0}，{0， 0，0，4，1}，{0，0，0，0，10}，{0，0，0，0，0}}，
> cost [] [] = {{0，1，0 ，0，0}，{0，0，0，0，0}，{0，0，0，0，0}，{0，0，0，0，0}，{0，0，0，0 ，0}}
> **输出**：10 1
> **说明**：
> 对于给定的图形，最大流量= 10，最小成本= 1。
> 
> **输入**：S = 0，T = 4，cost [] [] = {{0，1，0，0，2}，{0，0，0，3，0}，{0， 0，0，0，0}，{0，0，0，0，1}，{0，0，0，0，0}}
> 
> cap [] [] = {{0，3，1，0，3}，{0，0，2，0，0}，{0，0，0，1，6}，{0，0，0， 0，2}，{0，0，0，0，0}}}
> **输出**：6 8

**方法**：

成本网络中的负周期是循环的，周期中所有边的成本之和为负。 可以使用 [Bellman Ford 算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)检测到它们。 应该将它们消除，因为实际上不允许通过这样的循环。 考虑一个**负成本周期**，如果所有流程都必须经过该周期，则总成本始终在每个完成的周期中减少。 这将导致**的需求无限循环，从而使总成本**降至最低。 因此，每当成本网络包含负周期时，这意味着可以进一步最小化成本（通过流过周期的另一侧而不是当前考虑的那一侧）。 通过使[瓶颈容量](https://en.wikipedia.org/wiki/Bottleneck_(production)#:~:text=In%20production%20and%20project%20management, customers%2C%20and%20low%20employee%20morale.)流经循环中的所有边，可以消除一旦检测到的负循环。

现在，看看什么是供需节点：

> **供应节点**：这些是添加到流中并生成流的正节点。
> **需求节点**：这是从流程中减去的负节点。
> 
> **每个节点上的供应（或需求）** =流出节点的总流量–流入节点的总流量

通过向瓶颈周期的所有边发送瓶颈容量来解决负周期问题，可以解决给定的问题。 另外，由于涉及需求节点，因此调用 [Bellman Ford 算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)。

请按照以下步骤解决问题：

*   将边的**容量和该边**的**成本存储在两个单独的阵列中。**

*   给定源节点`S`和宿节点`T`，拾取边沿 **p <sub>i</sub>** ，需求节点 **d <sub>a [</sub>** 和节点 **dist** 之间的距离，搜索是否有可能从`S`到`T`流动。

*   如果存在流，则计算距离，**值= dist + pi – pi [k] – cost [k]** 。

*   将 **dist []** 中的距离值与**值**比较，并不断更新，直到获得**最小流量**。

下面是上述方法的实现：

## Java

```java

// Java Program to implement 
// the above approach 
import java.util.*; 

public class MinCostMaxFlow { 

    // Stores the found edges 
    boolean found[]; 

    // Stores the number of nodes 
    int N; 

    // Stores the capacity 
    // of each edge 
    int cap[][]; 

    int flow[][]; 

    // Stores the cost per 
    // unit flow of each edge 
    int cost[][]; 

    // Stores the distance from each node 
    // and picked edges for each node 
    int dad[], dist[], pi[]; 

    static final int INF 
        = Integer.MAX_VALUE / 2 - 1; 

    // Function to check if it is possible to 
    // have a flow from the src to sink 
    boolean search(int src, int sink) 
    { 

        // Initialise found[] to false 
        Arrays.fill(found, false); 

        // Initialise the dist[] to INF 
        Arrays.fill(dist, INF); 

        // Distance from the source node 
        dist[src] = 0; 

        // Iterate untill src reaches N 
        while (src != N) { 

            int best = N; 
            found[src] = true; 

            for (int k = 0; k < N; k++) { 

                // If already found 
                if (found[k]) 
                    continue; 

                // Evaluate while flow 
                // is still in supply 
                if (flow[k][src] != 0) { 

                    // Obtain the total value 
                    int val 
                        = dist[src] + pi[src] 
                          - pi[k] - cost[k][src]; 

                    // If dist[k] is > minimum value 
                    if (dist[k] > val) { 

                        // Update 
                        dist[k] = val; 
                        dad[k] = src; 
                    } 
                } 

                if (flow[src][k] < cap[src][k]) { 

                    int val = dist[src] + pi[src] 
                              - pi[k] + cost[src][k]; 

                    // If dist[k] is > minimum value 
                    if (dist[k] > val) { 

                        // Update 
                        dist[k] = val; 
                        dad[k] = src; 
                    } 
                } 

                if (dist[k] < dist[best]) 
                    best = k; 
            } 

            // Update src to best for 
            // next iteration 
            src = best; 
        } 

        for (int k = 0; k < N; k++) 
            pi[k] 
                = Math.min(pi[k] + dist[k], 
                           INF); 

        // Return the value obtained at sink 
        return found[sink]; 
    } 

    // Function to obtain the maximum Flow 
    int[] getMaxFlow(int cap[][], int cost[][], 
                     int src, int sink) 
    { 

        this.cap = cap; 
        this.cost = cost; 

        N = cap.length; 
        found = new boolean[N]; 
        flow = new int[N][N]; 
        dist = new int[N + 1]; 
        dad = new int[N]; 
        pi = new int[N]; 

        int totflow = 0, totcost = 0; 

        // If a path exist from src to sink 
        while (search(src, sink)) { 

            // Set the default amount 
            int amt = INF; 
            for (int x = sink; x != src; x = dad[x]) 

                amt = Math.min(amt, 
                               flow[x][dad[x]] != 0
                                   ? flow[x][dad[x]] 
                                   : cap[dad[x]][x] 
                                         - flow[dad[x]][x]); 

            for (int x = sink; x != src; x = dad[x]) { 

                if (flow[x][dad[x]] != 0) { 
                    flow[x][dad[x]] -= amt; 
                    totcost -= amt * cost[x][dad[x]]; 
                } 
                else { 
                    flow[dad[x]][x] += amt; 
                    totcost += amt * cost[dad[x]][x]; 
                } 
            } 
            totflow += amt; 
        } 

        // Return pair total cost and sink 
        return new int[] { totflow, totcost }; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 

        // Creating an object flow 
        MinCostMaxFlow flow = new MinCostMaxFlow(); 

        int s = 0, t = 4; 

        int cap[][] = { { 0, 3, 1, 0, 3 }, 
                        { 0, 0, 2, 0, 0 }, 
                        { 0, 0, 0, 1, 6 }, 
                        { 0, 0, 0, 0, 2 }, 
                        { 0, 0, 0, 0, 0 } }; 

        int cost[][] = { { 0, 1, 0, 0, 2 }, 
                         { 0, 0, 0, 3, 0 }, 
                         { 0, 0, 0, 0, 0 }, 
                         { 0, 0, 0, 0, 1 }, 
                         { 0, 0, 0, 0, 0 } }; 

        int ret[] = flow.getMaxFlow(cap, cost, s, t); 

        System.out.println(ret[0] + " " + ret[1]); 
    } 
} 

```

**Output:**

```
6 8

```

***时间复杂度**：O（V <sup>2</sup> * E <sup>2</sup> ）其中 V 是顶点数，E 是边数。*

***辅助空间**：O（V）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。