# 检查通过所有可能的路径从任何节点到任何其他节点的成本是否相同

> 原文:[https://www . geesforgeks . org/check-从任何节点到任何其他节点的所有可能路径的成本是否相同/](https://www.geeksforgeeks.org/check-whether-the-cost-of-going-from-any-node-to-any-other-node-via-all-possible-paths-is-same/)

给定有向图的[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)表示，任务是检查通过所有可能的路径从任何顶点到任何其他顶点的成本是否相等。如果存在从顶点 **A** 到顶点 **B** 的费用 **c** ，那么从顶点 **B** 到顶点 **A** 的旅行费用将为 **-c** 。

**示例:**

> **输入:** arr[][] = {{0，2，0，1}，{-2，0，1，0}，{0，-1，0，-2}，{-1，0，2，0}}
> **输出:**是
> **解释:**
> 
> ![](img/ceae0f41ba58cdf56e0ffbe928fa260c.png)
> 
> 这里，从任何节点到任何其他节点的成本对于所有可能的路径都是相等的。例如，如果我们从 1 到 4 通过(1 -> 2 -> 3 -> 4)，其成本为(2 + 1 + (-2))，即 1 和通过(1 -> 4)，其是成本为 1 的反向边。同样，所有其他路径的成本是相等的。
> 
> **输入:** arr[][] = {{0，1，0，3，0}，{-1，0，3，0，4}，{0，-3，0，1，1}，{-3，0，-1，0，0}，{0，-4，-1，0，0}}
> **输出:**否
> **说明:**
> 
> ![](img/5b2aa7f5576c8bd1cff6249700613a5c.png)
> 
> 对于从边缘 1 到 4 的以下两条路径，(1 -> 2 -> 3 -> 4)，成本= (1 + 3 + 1) = 5 和(1 -> 4)，成本= 3。由于成本不同，答案是否定的

**方法:**想法是维持两个阵列**dis【】**维持行进路径的距离，以及**访问【】**维持访问顶点。使用成对的 [2D 矢量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)存储图形。该对的第一个值是目的节点，第二个值是与之相关的成本。现在， [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 在图上运行。每个顶点都有以下两种情况:

1.  如果下一个要到达的节点没有被访问，则 **dis** 数组用值 dis[current_node] +从 2D 向量找到的新边的成本来更新，即当前节点到下一个要到达的节点，并且用未访问的相同节点调用相同的函数。
2.  如果节点被访问，则下一个要到达的节点的距离与到达下一个节点的 dis[curr] +边缘成本进行比较。如果它们相等，则布尔变量标志更新为真，循环继续到下一个顶点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
vector<pair<int, int> > adj[100005];

// Initialize distance and visited array
int vis[100005] = { 0 },
    dist[100005] = { 0 },
    flg;

// Function to perform dfs and check
// For a given vertex If the distance
// for all the paths is equal or not
void dfs(int curr)
{
    vis[curr] = 1;
    for (int i = 0; i < adj[curr].size(); i++) {

        // Checking the next node to reach
        // is visited or not
        if (vis[adj[curr][i].first]) {

            // Case 2: comparing the distance
            if (dist[adj[curr][i].first]
                != dist[curr] + adj[curr][i].second)
                flg = 1;
        }
        else {

            // Case 1: Adding the distance
            // and updating the array
            dist[adj[curr][i].first] = dist[curr]
                                       + adj[curr][i].second;

            // Calling the function again with the
            // same node
            dfs(adj[curr][i].first);
        }
    }
}

// Driver code
int main()
{
    int n = 4, m = 4;
    flg = 0;
    // Creating the graph as mentioned
    // in example 1
    adj[0].push_back({ 1, 2 });
    adj[1].push_back({ 0, -2 });
    adj[1].push_back({ 2, 1 });
    adj[2].push_back({ 1, -1 });
    adj[2].push_back({ 3, -2 });
    adj[3].push_back({ 2, 2 });
    adj[3].push_back({ 0, -1 });
    adj[0].push_back({ 3, 1 });
    for (int i = 0; i < n; i++) {
        if (flg)

            // If for any vertex, flg is true,
            // then the distance is not equal
            break;

        if (!vis[i])

            // Calling the DFS function if
            // the vertex is not visited
            dfs(i);
    }
    if (flg)
        cout << "No" << endl;
    else
        cout << "Yes" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG {
    static class pair {
        int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    static Vector<pair>[] adj = new Vector[100005];

    // Initialize distance and visited array
    static int[] vis = new int[100005];
    static int[] dist = new int[100005];
    static int flg;

    // Function to perform dfs and check
    // For a given vertex If the distance
    // for all the paths is equal or not
    static void dfs(int curr) {
        vis[curr] = 1;
        for (int i = 0; i < adj[curr].size(); i++) {

            // Checking the next node to reach
            // is visited or not
            if (vis[adj[curr].get(i).first] > 0) {

                // Case 2: comparing the distance
                if (dist[adj[curr].get(i).first] !=
                    dist[curr] + adj[curr].get(i).second)
                    flg = 1;
            } else {

                // Case 1: Adding the distance
                // and updating the array
                dist[adj[curr].get(i).first] =
                    dist[curr] + adj[curr].get(i).second;

                // Calling the function again with the
                // same node
                dfs(adj[curr].get(i).first);
            }
        }
    }

    // Driver code
    public static void main(String[] args) {
        int n = 4, m = 4;
        flg = 0;
        for (int i = 0; i < adj.length; i++) {
            adj[i] = new Vector<pair>();
        }
        // Creating the graph as mentioned
        // in example 1
        adj[0].add(new pair(1, 2));
        adj[1].add(new pair(0, -2));
        adj[1].add(new pair(2, 1));
        adj[2].add(new pair(1, -1));
        adj[2].add(new pair(3, -2));
        adj[3].add(new pair(2, 2));
        adj[3].add(new pair(0, -1));
        adj[0].add(new pair(3, 1));
        for (int i = 0; i < n; i++) {
            if (flg == 1)

                // If for any vertex, flg is true,
                // then the distance is not equal
                break;

            if (vis[i] != 1)

                // Calling the DFS function if
                // the vertex is not visited
                dfs(i);
        }
        if (flg == 1)
            System.out.print("No" + "\n");
        else
            System.out.print("Yes" + "\n");
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
adj = [[] for i in range(100005)]

# Initialize distance and visited array
vis = [0]*100005
dist = [0]*100005
flg = 0

# Function to perform dfs and check
# For a given vertex If the distance
# for all the paths is equal or not
def dfs(curr):
    vis[curr] = 1
    for i in range(len(adj[curr])):

        # Checking the next node to reach
        # is visited or not
        if (vis[adj[curr][i][0]]):

            # Case 2: comparing the distance
            if (dist[adj[curr][i][0]]
                != dist[curr] + adj[curr][i][1]):
                flg = 1
        else:

            # Case 1: Adding the distance
            # and updating the array
            dist[adj[curr][i][0]] = dist[curr]+ adj[curr][i][1]

            # Calling the function again with the
            # same node
            dfs(adj[curr][i][0])

# Driver code

n = 4
m = 4
flg = 0

# Creating the graph as mentioned
# in example 1
adj[0].append([1, 2])
adj[1].append([0, -2])
adj[1].append([2, 1])
adj[2].append([1, -1])
adj[2].append([3, -2])
adj[3].append([2, 2])
adj[3].append([0, -1])
adj[0].append([3, 1])

for i in range(n):
    if (flg):

        # If for any vertex, flg is true,
        # then the distance is not equal
        break

    if (vis[i] == 0):

        # Calling the DFS function if
        # the vertex is not visited
        dfs(i)

if (flg):
    print("No")
else:
    print("Yes")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG {
    class pair {
        public int first, second;
        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    static List<pair>[] adj = new List<pair>[100005];

    // Initialize distance and visited array
    static int[] vis = new int[100005];
    static int[] dist = new int[100005];
    static int flg;

    // Function to perform dfs and check
    // For a given vertex If the distance
    // for all the paths is equal or not
    static void dfs(int curr) {
        vis[curr] = 1;
        for (int i = 0; i < adj[curr].Count; i++) {

            // Checking the next node to reach
            // is visited or not
            if (vis[adj[curr][i].first] > 0) {

                // Case 2: comparing the distance
                if (dist[adj[curr][i].first] !=
                    dist[curr] + adj[curr][i].second)
                    flg = 1;
            } else {

                // Case 1: Adding the distance
                // and updating the array
                dist[adj[curr][i].first] =
                    dist[curr] + adj[curr][i].second;

                // Calling the function again with the
                // same node
                dfs(adj[curr][i].first);
            }
        }
    }

    // Driver code
    public static void Main(String[] args) {
        int n = 4;
        flg = 0;
        for (int i = 0; i < adj.Length; i++) {
            adj[i] = new List<pair>();
        }
        // Creating the graph as mentioned
        // in example 1
        adj[0].Add(new pair(1, 2));
        adj[1].Add(new pair(0, -2));
        adj[1].Add(new pair(2, 1));
        adj[2].Add(new pair(1, -1));
        adj[2].Add(new pair(3, -2));
        adj[3].Add(new pair(2, 2));
        adj[3].Add(new pair(0, -1));
        adj[0].Add(new pair(3, 1));
        for (int i = 0; i < n; i++) {
            if (flg == 1)

                // If for any vertex, flg is true,
                // then the distance is not equal
                break;

            if (vis[i] != 1)

                // Calling the DFS function if
                // the vertex is not visited
                dfs(i);
        }
        if (flg == 1)
            Console.Write("No" + "\n");
        else
            Console.Write("Yes" + "\n");
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
let  adj = new Array(100005);

// Initialize distance and visited array
let vis = new Array(100005);
let dist = new Array(100005);
for(let i = 0; i < 100005; i++)
{
    vis[i] = 0;
    dist[i] = 0;
}

let flg;

// Function to perform dfs and check
// For a given vertex If the distance
// for all the paths is equal or not
function dfs(curr)
{
    vis[curr] = 1;
    for(let i = 0; i < adj[curr].length; i++)
    {

        // Checking the next node to reach
        // is visited or not
        if (vis[adj[curr][i][0]] > 0)
        {

            // Case 2: comparing the distance
            if (dist[adj[curr][i][0]] != 
                dist[curr] + adj[curr][i][1])
                flg = 1;
        }
        else
        {

            // Case 1: Adding the distance
            // and updating the array
            dist[adj[curr][i][0]] =  dist[curr] +
                                      adj[curr][i][1];

            // Calling the function again with the
            // same node
            dfs(adj[curr][i][0]);
        }
    }
}

// Driver code
let n = 4, m = 4;
flg = 0;
for(let i = 0; i < adj.length; i++)
{
    adj[i] = [];
}

// Creating the graph as mentioned
// in example 1
adj[0].push([1, 2]);
adj[1].push([0, -2]);
adj[1].push([2, 1]);
adj[2].push([1, -1]);
adj[2].push([3, -2]);
adj[3].push([2, 2]);
adj[3].push([0, -1]);
adj[0].push([3, 1]);
for(let i = 0; i < n; i++)
{
    if (flg == 1)

        // If for any vertex, flg is true,
        // then the distance is not equal
        break;

    if (vis[i] != 1)

        // Calling the DFS function if
        // the vertex is not visited
        dfs(i);
}

if (flg == 1)
    document.write("No" + "<br>");
else
    document.write("Yes" + "<br>");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(V + E)，其中 V 没有顶点，E 没有边