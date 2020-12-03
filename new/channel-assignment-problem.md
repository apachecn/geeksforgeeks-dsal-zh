# 频道分配问题

> 原文： [https://www.geeksforgeeks.org/channel-assignment-problem/](https://www.geeksforgeeks.org/channel-assignment-problem/)

有 M 个发射机站和 N 个接收机站。 给定一个矩阵，该矩阵跟踪要从给定的发送器发送到接收器的数据包的数量。 如果矩阵的第（i; j）项是 k，则意味着此时站 i 有 k 个数据包要传输到站 j。
在一个时隙中，发送器只能发送一个数据包，而接收器只能接收一个数据包。 查找信道分配，以便在下一个时隙期间将最大数量的数据包从发送器传输到接收器。
**例如**：

```
0 2 0
3 0 1
2 4 0
```

以上是输入格式。 我们称上述矩阵为 M。每个值 M [i; j]代表发送方“ i”必须发送给接收方“ j”的数据包数量。 输出应为：

```
The number of maximum packets sent in the time slot is 3
T1 -> R2
T2 -> R3
T3 -> R1 
```

请注意，在任何插槽中可以传输的最大数据包数是 min（M，N）。

**算法**：
发送方和接收方之间的信道分配问题可以轻松转换为最大二分匹配（MBP）问题，可以通过将其转换为流网络来解决。

**步骤 1：建立流网络**
流网络中必须有源和汇。 因此，我们添加了虚拟源，并将源中的边添加到所有发件人。 同样，将所有接收器的边添加到虚拟接收器。 所有增加的边的容量标记为 1 个单位。

**步骤 2：找到最大流量。**
我们使用 [Ford-Fulkerson 算法](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)在步骤 1 中构建的流量网络中找到最大流量。最大流量实际上是在不干扰带宽的情况下可以传输的最大数据包数。 一个时隙。

**实现**：
首先定义输入和输出形式。 输入采用 Edmonds 矩阵的形式，该矩阵是 2D 数组“ table [M] [N]”，其中 M 行（对于 M 个发送者）和 N 列（对于 N 个接收者）。 值表[i] [j]是必须从发送方“ i”发送到接收方“ j”的数据包数量。 输出是在一个时隙中可以无带宽干扰地传输的最大数据包数。
一种简单的实现方法是创建一个矩阵，该矩阵表示具有 M + N + 2 个顶点的有向图的邻接矩阵表示。 调用 fordFulkerson（）作为矩阵。 此实现需要 O（（M + N）*（M + N））额外空间。
使用图形是两部分的事实，可以减少额外的空间，并可以简化代码。 这个想法是使用 DFS 遍历来查找发送器的接收器（类似于 Ford-Fulkerson 中的增强路径）。 我们为每个申请人调用 bpm（），bpm（）是基于 DFS 的函数，它尝试将接收者分配给发送者的所有可能性。 在 bpm（）中，我们一步一步地尝试发送方“ u”感兴趣的所有接收方，直到找到接收方，或者所有接收方都没有运气。
对于我们尝试的每个接收者，我们都会执行以下操作：
如果未将接收者分配给任何人，我们只需将其分配给发送者并返回 true。 如果一个接收者被分配给其他人，比如说 x，那么我们递归检查 x 是否可以被分配给其他接收者。 为确保 x 不会再次收到相同的接收者，我们在对 x 进行递归调用之前将接收者标记为“ v”。 如果 x 可以获取其他接收者，则我们将接收者“ v”的发送者更改为 true。 我们使用数组 maxR [0..N-1]来存储分配给不同接收者的发送者。
如果 bmp（）返回 true，则表示流网络中存在扩展路径，并将 1 单位流添加到 maxBPM（）的结果中。

**时空复杂度分析**：
在二分匹配问题的情况下，F？ | V | 因为只能有| V | 来自源节点的可能边。 因此，总运行时间为 O（m’n）= O（（m + n）n）。 空间复杂度也从 O（（M + N）*（M + N））大大减少到大小为 M 的一维数组，从而存储了 M 和 N 之间的映射。

## C

```c

#include <iostream> 
#include <string.h> 
#include <vector> 
#define M 3 
#define N 4 
using namespace std; 

// A Depth First Search based recursive function that returns true 
// if a matching for vertex u is possible 
bool bpm(int table[M][N], int u, bool seen[], int matchR[]) 
{ 
    // Try every receiver one by one 
    for (int v = 0; v < N; v++) 
    { 
        // If sender u has packets to send to receiver v and 
        // receiver v is not already mapped to any other sender 
        // just check if the number of packets is greater than '0' 
        // because only one packet can be sent in a time frame anyways 
        if (table[u][v]>0 && !seen[v]) 
        { 
            seen[v] = true; // Mark v as visited 

            // If receiver 'v' is not assigned to any sender OR 
            // previously assigned sender for receiver v (which is 
            // matchR[v]) has an alternate receiver available. Since 
            // v is marked as visited in the above line, matchR[v] in 
            // the following recursive call will not get receiver 'v' again 
            if (matchR[v] < 0 || bpm(table, matchR[v], seen, matchR)) 
            { 
                matchR[v] = u; 
                return true; 
            } 
        } 
    } 
    return false; 
} 

// Returns maximum number of packets that can be sent parallely in 1 
// time slot from sender to receiver 
int maxBPM(int table[M][N]) 
{ 
    // An array to keep track of the receivers assigned to the senders. 
    // The value of matchR[i] is the sender ID assigned to receiver i. 
    // the value -1 indicates nobody is assigned. 
    int matchR[N]; 

    // Initially all receivers are not mapped to any senders 
    memset(matchR, -1, sizeof(matchR)); 

    int result = 0; // Count of receivers assigned to senders 
    for (int u = 0; u < M; u++) 
    { 
        // Mark all receivers as not seen for next sender 
        bool seen[N]; 
        memset(seen, 0, sizeof(seen)); 

        // Find if the sender 'u' can be assigned to the receiver 
        if (bpm(table, u, seen, matchR)) 
            result++; 
    } 

    cout << "The number of maximum packets sent in the time slot is "
         << result << "\n"; 

    for (int x=0; x<N; x++) 
        if (matchR[x]+1!=0) 
            cout << "T" << matchR[x]+1 << "-> R" << x+1 << "\n"; 
    return result; 
} 

// Driver program to test above function 
int main() 
{ 
    int table[M][N] = {{0, 2, 0}, {3, 0, 1}, {2, 4, 0}}; 
    int max_flow = maxBPM(table); 
    return 0; 
} 

```

## Java

```java

import java.util.*; 
class GFG  
{ 
static int M = 3; 
static int N = 3; 

// A Depth First Search based recursive function  
// that returns true if a matching for vertex u is possible 
static boolean bpm(int table[][], int u, 
                   boolean seen[], int matchR[]) 
{ 
    // Try every receiver one by one 
    for (int v = 0; v < N; v++) 
    { 
        // If sender u has packets to send  
        // to receiver v and receiver v is not  
        // already mapped to any other sender 
        // just check if the number of packets is  
        // greater than '0' because only one packet  
        // can be sent in a time frame anyways 
        if (table[u][v] > 0 && !seen[v]) 
        { 
            seen[v] = true; // Mark v as visited 

            // If receiver 'v' is not assigned to  
            // any sender OR previously assigned sender  
            // for receiver v (which is matchR[v]) has an  
            // alternate receiver available. Since v is  
            // marked as visited in the above line,  
            // matchR[v] in the following recursive call  
            // will not get receiver 'v' again 
            if (matchR[v] < 0 || bpm(table, matchR[v],  
                                      seen, matchR)) 
            { 
                matchR[v] = u; 
                return true; 
            } 
        } 
    } 
    return false; 
} 

// Returns maximum number of packets  
// that can be sent parallely in 
// 1 time slot from sender to receiver 
static int maxBPM(int table[][]) 
{ 
    // An array to keep track of the receivers  
    // assigned to the senders. The value of matchR[i]  
    // is the sender ID assigned to receiver i.  
    // The value -1 indicates nobody is assigned. 
    int []matchR = new int[N]; 

    // Initially all receivers are 
    // not mapped to any senders 
    Arrays.fill(matchR, -1); 

    int result = 0; // Count of receivers assigned to senders 
    for (int u = 0; u < M; u++) 
    { 
        // Mark all receivers as not seen for next sender 
        boolean []seen = new boolean[N]; 
        Arrays.fill(seen, false); 

        // Find if the sender 'u' can be 
        // assigned to the receiver 
        if (bpm(table, u, seen, matchR)) 
            result++; 
    } 

    System.out.println("The number of maximum packets" +  
                       " sent in the time slot is " + result); 

    for (int x = 0; x < N; x++) 
        if (matchR[x] + 1 != 0) 
            System.out.println("T" + (matchR[x] + 1) + 
                               "-> R" + (x + 1)); 
    return result; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    int table[][] = {{0, 2, 0}, 
                     {3, 0, 1},  
                     {2, 4, 0}}; 

    maxBPM(table); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python

```py

# A Depth First Search based recursive  
# function that returns true if a matching 
# for vertex u is possible  
def bpm(table, u, seen, matchR): 
    global M, N 

    # Try every receiver one by one  
    for v in range(N): 

        # If sender u has packets to send to  
        # receiver v and receiver v is not  
        # already mapped to any other sender  
        # just check if the number of packets  
        # is greater than '0' because only one 
        # packet can be sent in a time frame anyways  
        if (table[u][v] > 0 and not seen[v]): 
            seen[v] = True # Mark v as visited  

            # If receiver 'v' is not assigned to any  
            # sender OR previously assigned sender  
            # for receiver v (which is matchR[v]) has  
            # an alternate receiver available. Since  
            # v is marked as visited in the above line,   
            # matchR[v] in the following recursive call 
            # will not get receiver 'v' again  
            if (matchR[v] < 0 or bpm(table, matchR[v],  
                                       seen, matchR)): 
                matchR[v] = u  
                return True
    return False

# Returns maximum number of packets  
# that can be sent parallely in 1  
# time slot from sender to receiver  
def maxBPM(table): 
    global M, N 

    # An array to keep track of the receivers  
    # assigned to the senders. The value of  
    # matchR[i] is the sender ID assigned to  
    # receiver i. The value -1 indicates nobody  
    # is assigned. 

    # Initially all receivers are not mapped 
    # to any senders  
    matchR = [-1] * N 

    result = 0 # Count of receivers assigned to senders 
    for u in range(M): 

        # Mark all receivers as not seen  
        # for next sender  
        seen = [0] * N 

        # Find if the sender 'u' can be assigned 
        # to the receiver  
        if (bpm(table, u, seen, matchR)):  
            result += 1

    print("The number of maximum packets sent",  
          "in the time slot is", result) 

    for x in range(N): 
        if (matchR[x] + 1 != 0):  
            print("T", matchR[x] + 1, "-> R", x + 1)  
    return result 

# Driver Code 
M = 3
N = 4

table = [[0, 2, 0], [3, 0, 1], [2, 4, 0]] 
max_flow = maxBPM(table) 

# This code is contributed by PranchalK 

```

## C#

```cs

// C# implementation of the above approach 
using System; 

class GFG  
{ 
static int M = 3; 
static int N = 3; 

// A Depth First Search based recursive function  
// that returns true if a matching for vertex u is possible 
static Boolean bpm(int [,]table, int u, 
                   Boolean []seen, int []matchR) 
{ 
    // Try every receiver one by one 
    for (int v = 0; v < N; v++) 
    { 
        // If sender u has packets to send  
        // to receiver v and receiver v is not  
        // already mapped to any other sender 
        // just check if the number of packets is  
        // greater than '0' because only one packet  
        // can be sent in a time frame anyways 
        if (table[u, v] > 0 && !seen[v]) 
        { 
            seen[v] = true; // Mark v as visited 

            // If receiver 'v' is not assigned to  
            // any sender OR previously assigned sender  
            // for receiver v (which is matchR[v]) has an  
            // alternate receiver available. Since v is  
            // marked as visited in the above line,  
            // matchR[v] in the following recursive call  
            // will not get receiver 'v' again 
            if (matchR[v] < 0 || bpm(table, matchR[v],  
                                     seen, matchR)) 
            { 
                matchR[v] = u; 
                return true; 
            } 
        } 
    } 
    return false; 
} 

// Returns maximum number of packets  
// that can be sent parallely in 
// 1 time slot from sender to receiver 
static int maxBPM(int [,]table) 
{ 
    // An array to keep track of the receivers  
    // assigned to the senders. The value of matchR[i]  
    // is the sender ID assigned to receiver i.  
    // The value -1 indicates nobody is assigned. 
    int []matchR = new int[N]; 

    // Initially all receivers are 
    // not mapped to any senders 
    for(int i = 0; i < N; i++) 
        matchR[i] = -1; 

    int result = 0; // Count of receivers assigned to senders 
    for (int u = 0; u < M; u++) 
    { 
        // Mark all receivers as not seen for next sender 
        Boolean []seen = new Boolean[N]; 

        // Find if the sender 'u' can be 
        // assigned to the receiver 
        if (bpm(table, u, seen, matchR)) 
            result++; 
    } 

    Console.WriteLine("The number of maximum packets" +  
                      " sent in the time slot is " + result); 

    for (int x = 0; x < N; x++) 
        if (matchR[x] + 1 != 0) 
            Console.WriteLine("T" + (matchR[x] + 1) + 
                              "-> R" + (x + 1)); 
    return result; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    int [,]table = {{0, 2, 0}, 
                    {3, 0, 1},  
                    {2, 4, 0}}; 

    maxBPM(table); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
The number of maximum packets sent in the time slot is 3
T3-> R1
T1-> R2
T2-> R3

```

本文由 [Vignesh Narayanan](https://webapp4.asu.edu/directory/person/2207851) 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

