# 图中从源 S 到目标 D 的最短路径，其中多个查询正好具有 K 个边

> 原文： [https://www.geeksforgeeks.org/shortest-path-in-a-graph-from-a-source-s-to-destination-d-with-exactly-k-edges-for-multiple-queries/](https://www.geeksforgeeks.org/shortest-path-in-a-graph-from-a-source-s-to-destination-d-with-exactly-k-edges-for-multiple-queries/)

给定一个具有`N`个节点的图，节点`S`和`Q`分别查询由节点`D`和`K`，则任务是为每个查询找到从节点`S`到节点`D`的`K`个边的最短路径。 如果不存在这样的路径，则打印`-1`。

**注意**：`K`始终小于 **2 * N** 。

**示例**：

> **输入**：N = 3，edges [] [] = {{1，2，5}，{2，3，3}，{3，1，4}}，S = 1，Q = {{1，0}，{2，1}，{3，1}，{3，2}，{3，5}}
> **输出**：0 5 -1 8 20 ] 1.从 1 到 1 的最短路径为 0。
> 2.从 1 到 2 的最短路径为 5，即 1- > 2\.
> 3.无路径 节点 1 和 3 之间存在 1 个边缘的其中之一。 使用 5 条边线的 1 到 3 将为 20，即 1- > 2- > 3- > 1- > 2- > 3。
> 
> **输入**：N = 4，边缘[] [] = {{1、2、8}，{2、3、5}，{3、4、7}}，S = 1，Q = {{1，0}，{2，1}，{3，1}，{3，2}，{4，5}}
> **输出**：0 8 -1 13 -1

**方法**：

*   可以通过[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)创建线性解决方案来解决此问题。
*   初始化 [2-d 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，dp [N] [2 * N]的初始值为'inf'，但 dp [S] [0]为 0。
*   对图形进行预处理，以找到{0 到 N-1}之间的每个边长，到源的每个节点的最短距离。 数组 dp [] []将用于存储预处理结果。
*   对于预处理，对范围[1，2 * N-1]中的 J 运行循环，以找到图中每个边的 dp [X] [J]，其中 **dp [X] [J]** 是从节点'S'到节点'X'的最短路径，总共使用了精确的'J'边。
*   我们可以借助递归关系找到 dp [X] [J + 1]：

> dp [edge.second] [i] = **min** （dp [edge.second] [i]，dp [edge.first] [i-1] + weight（edge））

*   对于 Q 中的每个查询，if（dp [X] [k] == inf）然后返回-1，否则返回 dp [X] [k]

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

#define inf 100000000

// Function to find the shortest path
// between S and D with exactly K edges
void ansQueries(int s,
                vector<pair<pair<int, int>, int> > ed,
                int n, vector<pair<int, int> > q)
{

    // To store the dp states
    int dp[n + 1][2 * n];

    // Initialising the dp[][] array
    for (int i = 0; i <= n; i++)
        dp[i][0] = inf;
    dp[s][0] = 0;

    // Pre-Processing
    for (int i = 1; i <= 2 * n - 1; i++) {

        // Initialising current state
        for (int j = 0; j <= n; j++)
            dp[j][i] = inf;

        // Updating current state
        for (auto it : ed) {
            dp[it.first.second][i]
                = min(
                    dp[it.first.second][i],
                    dp[it.first.first][i - 1] + it.second);
        }
    }

    for (int i = 0; i < q.size(); i++) {
        if (dp[q[i].first][q[i].second] == inf)
            cout << -1 << endl;
        else
            cout << dp[q[i].first][q[i].second]
                 << endl;
    }
}

// Driver code
int main()
{
    int n = 3;
    vector<pair<pair<int, int>, int> > ed;

    // Edges
    ed = { { { 1, 2 }, 5 },
           { { 2, 3 }, 3 },
           { { 3, 1 }, 4 } };

    // Source
    int s = 1;

    // Queries
    vector<pair<int, int> > q = { { 1, 0 },
                                  { 2, 1 },
                                  { 3, 1 },
                                  { 3, 2 },
                                  { 3, 5 } };

    // Function to answer queries
    ansQueries(s, ed, n, q);

    return 0;
}

```

## Java

```java

// Java implementation of the approach 
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

static int inf = 100000000; 

// Function to find the shortest path 
// between S and D with exactly K edges 
static void ansQueries(int s, 
                       int[][] ed, 
                int n, int[][] q) 
{ 

    // To store the dp states 
    int[][] dp = new int[n + 1][2 * n]; 

    // Initialising the dp[][] array 
    for(int i = 0; i <= n; i++) 
        dp[i][0] = inf; 

    dp[s][0] = 0; 

    // Pre-Processing 
    for(int i = 1; i <= 2 * n - 1; i++)
    { 

        // Initialising current state 
        for(int j = 0; j <= n; j++) 
            dp[j][i] = inf; 

        // Updating current state 
        for(int[] it : ed)
        { 
            dp[it[1]][i] = Math.min(dp[it[1]][i],
                                    dp[it[0]][i - 1] + 
                                       it[2]); 
        } 
    } 

    for(int i = 0; i < q.length; i++) 
    { 
        if (dp[q[i][0]][q[i][1]] == inf)  
            System.out.println(-1);  
        else 
            System.out.println(dp[q[i][0]][q[i][1]]);
    } 
} 

// Driver code
public static void main(String[] args)
{
    int n = 3; 

    // Edges 
    int[][] ed = { { 1, 2, 5 }, 
                   { 2, 3, 3 }, 
                   { 3, 1, 4 } }; 

    // Source 
    int s = 1; 

    // Queries 
    int[][] q = { { 1, 0 }, 
                  { 2, 1 }, 
                  { 3, 1 }, 
                  { 3, 2 }, 
                  { 3, 5 } }; 

    // Function to answer queries 
    ansQueries(s, ed, n, q); 
}
}

// This code is contributed by offbeat

```

## Python

```py

# Python3 implementation of the approach 
import sys,numpy as np

inf = sys.maxsize;

# Function to find the shortest path 
# between S and D with exactly K edges 
def ansQueries(s, ed, n, q) :

    # To store the dp states 
    dp = np.zeros((n + 1, 2 * n)); 

    # Initialising the dp[][] array 
    for i in range(n + 1) : 
        dp[i][0] = inf; 

    dp[s][0] = 0; 

    # Pre-Processing 
    for i in range( 1, 2 * n) :

        # Initialising current state 
        for j in range( n + 1) :
            dp[j][i] = inf; 

        # Updating current state 
        for it in ed :
            dp[it[1]][i] = min( dp[it[1]][i], 
                                dp[it[0]][i - 1] + ed[it]); 

    for i in range(len(q)) :
        if (dp[q[i][0]][q[i][1]] == inf) :
            print(-1); 
        else :
            print(dp[q[i][0]][q[i][1]]);

# Driver code 
if __name__ == "__main__" : 

    n = 3; 

    # Edges 
    ed = { ( 1, 2 ) : 5 , 
        ( 2, 3 ) : 3 , 
        ( 3, 1 ) : 4 }; 

    # Source 
    s = 1; 

    # Queries 
    q = [ 
        ( 1, 0 ), 
        ( 2, 1 ), 
        ( 3, 1 ), 
        ( 3, 2 ), 
        ( 3, 5 )
        ]; 

    # Function to answer queries 
    ansQueries(s, ed, n, q); 

# This code is contributed by AnkitRai01

```

**Output:** 

```
0
5
-1
8
20
```

**时间复杂度**：O（Q + N * E）
**空间复杂度**：O（N * N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。