# 通道分配问题

> 原文:[https://www.geeksforgeeks.org/channel-assignment-problem/](https://www.geeksforgeeks.org/channel-assignment-problem/)

有 M 个发射机站和 N 个接收机站。给定一个跟踪要从给定发射机发送到接收机的数据包数量的矩阵。如果(I；j)矩阵的第 k 个条目是 k，这意味着此时站 I 有 k 个分组要发送到站 j。
在一个时隙期间，发射机只能发送一个分组，接收机只能接收一个分组。找到信道分配，以便在下一个时隙期间从发射机向接收机传输最大数量的数据包。
**例:**

```
0 2 0
3 0 1
2 4 0
```

以上是输入格式。我们称上面的矩阵为 M。每个值 M[I；j]表示发送方‘I’必须发送给接收方‘j’的数据包数量。输出应该是:

```
The number of maximum packets sent in the time slot is 3
T1 -> R2
T2 -> R3
T3 -> R1 
```

请注意，在任何时隙中可以传输的最大数据包数是最小值(M，N)。
**算法:**
发送方和接收方之间的信道分配问题可以很容易地转化为最大二部匹配(MBP)问题，将其转化为流网络即可解决。
**第一步:构建流量网络**
流量网络中必须有源和汇。因此，我们添加一个虚拟源，并从源向所有发送方添加边。同样，将所有接收器的边缘添加到虚拟接收器。所有添加边的容量标记为 1 个单位。
**第二步:找到最大流量。**
我们使用[福特-富尔克森算法](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)在步骤 1 构建的流量网络中寻找最大流量。最大流量实际上是在一个时隙内没有带宽干扰可以传输的最大数据包数量。
**实现:**
我们先定义输入输出形式。输入采用埃德蒙兹矩阵的形式，这是一个 2D 数组“表[M][N]”，其中有 M 行(用于 M 个发送方)和 N 列(用于 N 个接收方)。值表[i][j]是必须从发送器‘I’发送到接收器‘j’的数据包数量。Output 是在一个时隙内，在没有带宽干扰的情况下，可以传输的最大数据包数量。
实现这一点的简单方法是创建一个矩阵，该矩阵表示具有 M+N+2 个顶点的有向图的邻接矩阵表示。为矩阵调用 fordFulkerson()。此实现需要 O((M+N)*(M+N))个额外空间。
利用图是二分图的事实，可以减少额外的空间，简化代码。其思想是使用 DFS 遍历来为发送器找到接收器(类似于福特-富尔克森中的扩充路径)。我们为每个申请人都调用 bpm()，bpm()是基于 DFS 的函数，它尝试了所有的可能性来将接收者分配给发送者。在 bpm()中，我们一个接一个地尝试发送方“u”感兴趣的所有接收方，直到找到接收方，或者所有接收方都尝试了，但没有成功。
对于我们尝试的每一个接收者，我们都遵循:
如果接收者没有分配给任何人，我们只需将其分配给发送者并返回 true。如果一个接收者被分配给其他人，比如 x，那么我们递归地检查 x 是否可以被分配给其他接收者。为了确保 x 不会再次获得相同的接收者，我们在递归调用 x 之前将接收者标记为“v”。如果 x 可以获得其他接收者，我们将发送者更改为接收者“v ”,并返回 true。我们使用一个数组 maxR[0..N-1]存储分配给不同接收者的发送者。
如果 bmp()返回 true，则表示在流网络中有一个扩充路径，并且在 maxBPM()中向结果添加了 1 个流单位。
**时空复杂度分析:**
在二分匹配问题的情况下，F？|V|因为只有|V|条可能的边从源节点出来。所以总运行时间为 O(m'n) = O((m + n)n)。空间复杂度也从 0((M+N)*(M+N))大幅降低至仅 M 大小的一维数组，从而存储 M 和 N 之间的映射

## C

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
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

```
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

## java 描述语言

```
<script>

let M = 3;
let N = 3;

// A Depth First Search based recursive function
// that returns true if a matching for vertex u is possible
function bpm(table,u,seen,matchR)
{
    // Try every receiver one by one
    for (let v = 0; v < N; v++)
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
function maxBPM(table)
{
    // An array to keep track of the receivers
    // assigned to the senders. The value of matchR[i]
    // is the sender ID assigned to receiver i.
    // The value -1 indicates nobody is assigned.
    let matchR = new Array(N);

    // Initially all receivers are
    // not mapped to any senders
    for(let i=0;i<N;i++)
    {
        matchR[i]=-1;
    }

    let result = 0; // Count of receivers assigned to senders
    for (let u = 0; u < M; u++)
    {
        // Mark all receivers as not seen for next sender
        let seen = new Array(N);
        for(let i=0;i<N;i++)
        {
            seen[i]=false;
        }

        // Find if the sender 'u' can be
        // assigned to the receiver
        if (bpm(table, u, seen, matchR))
            result++;
    }

    document.write("The number of maximum packets" +
                   " sent in the time slot is " + result+"<br>");

    for (let x = 0; x < N; x++)
        if (matchR[x] + 1 != 0)
            document.write("T" + (matchR[x] + 1) +
                               "-> R" + (x + 1)+"<br>");
    return result;
}

// Driver Code
let table= [[0, 2, 0],
                     [3, 0, 1],
                     [2, 4, 0]];
maxBPM(table);

// This code is contributed by rag2127

</script>
```

**输出:**

```
The number of maximum packets sent in the time slot is 3
T3-> R1
T1-> R2
T2-> R3
```

本文由 [Vignesh Narayanan](https://webapp4.asu.edu/directory/person/2207851) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息