# 使用回溯实现旅行商问题

> 原文:[https://www . geeksforgeeks . org/旅行推销员-问题-实现-使用-回溯/](https://www.geeksforgeeks.org/travelling-salesman-problem-implementation-using-backtracking/)

[**旅行推销员问题(TSP):**](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/) 给定一组城市和每对城市之间的距离，问题是找到恰好访问每个城市一次并返回起点的最短可能路线。
注意 [**哈密顿圈**](https://www.geeksforgeeks.org/backtracking-set-7-hamiltonian-cycle/) 和 TSP 的区别。哈密尔顿循环问题是要找出是否存在一个每座城市只参观一次的旅游。这里我们知道哈密顿圈是存在的(因为图是完整的)，事实上很多这样的圈是存在的，问题是找到一个最小权重的哈密顿圈。
例如，考虑图中所示的图表。图中的 TSP 行程为 1 - > 2 - > 4 - > 3 - > 1。旅游费用是 10 + 25 + 30 + 15 也就是 80。
问题是著名的 NP 难问题。这个问题没有多项式时间的已知解。

![TSP](img/5ed402d46a5ae77ea6bbb8f81947428f.png)

> **给定图形的输出:**
> 最小权重哈密顿圈:10 + 25 + 30 + 15 = 80

**方法:**本文讨论简单解决方案的实现。

*   考虑城市 1(假设第 0 个节点)作为起点和终点。由于路线是循环的，我们可以考虑任何一个点作为起点。
*   开始以 dfs 方式从源节点遍历到其相邻节点。
*   计算每次遍历的成本，跟踪最小成本，并不断更新最小成本存储值的值。
*   以最小的代价返回置换。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define V 4

// Function to find the minimum weight Hamiltonian Cycle
void tsp(int graph[][V], vector<bool>& v, int currPos,
         int n, int count, int cost, int& ans)
{

    // If last node is reached and it has a link
    // to the starting node i.e the source then
    // keep the minimum value out of the total cost
    // of traversal and "ans"
    // Finally return to check for more possible values
    if (count == n && graph[currPos][0]) {
        ans = min(ans, cost + graph[currPos][0]);
        return;
    }

    // BACKTRACKING STEP
    // Loop to traverse the adjacency list
    // of currPos node and increasing the count
    // by 1 and cost by graph[currPos][i] value
    for (int i = 0; i < n; i++) {
        if (!v[i] && graph[currPos][i]) {

            // Mark as visited
            v[i] = true;
            tsp(graph, v, i, n, count + 1,
                cost + graph[currPos][i], ans);

            // Mark ith node as unvisited
            v[i] = false;
        }
    }
};

// Driver code
int main()
{
    // n is the number of nodes i.e. V
    int n = 4;

    int graph[][V] = {
        { 0, 10, 15, 20 },
        { 10, 0, 35, 25 },
        { 15, 35, 0, 30 },
        { 20, 25, 30, 0 }
    };

    // Boolean array to check if a node
    // has been visited or not
    vector<bool> v(n);
    for (int i = 0; i < n; i++)
        v[i] = false;

    // Mark 0th node as visited
    v[0] = true;
    int ans = INT_MAX;

    // Find the minimum weight Hamiltonian Cycle
    tsp(graph, v, 0, n, 1, 0, ans);

    // ans is the minimum weight Hamiltonian Cycle
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find the minimum weight
    // Hamiltonian Cycle
    static int tsp(int[][] graph, boolean[] v,
                   int currPos, int n,
                   int count, int cost, int ans)
    {

        // If last node is reached and it has a link
        // to the starting node i.e the source then
        // keep the minimum value out of the total cost
        // of traversal and "ans"
        // Finally return to check for more possible values
        if (count == n && graph[currPos][0] > 0)
        {
            ans = Math.min(ans, cost + graph[currPos][0]);
            return ans;
        }

        // BACKTRACKING STEP
        // Loop to traverse the adjacency list
        // of currPos node and increasing the count
        // by 1 and cost by graph[currPos,i] value
        for (int i = 0; i < n; i++)
        {
            if (v[i] == false && graph[currPos][i] > 0)
            {

                // Mark as visited
                v[i] = true;
                ans = tsp(graph, v, i, n, count + 1,
                          cost + graph[currPos][i], ans);

                // Mark ith node as unvisited
                v[i] = false;
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        // n is the number of nodes i.e. V
        int n = 4;

        int[][] graph = {{0, 10, 15, 20},
                         {10, 0, 35, 25},
                         {15, 35, 0, 30},
                         {20, 25, 30, 0}};

        // Boolean array to check if a node
        // has been visited or not
        boolean[] v = new boolean[n];

        // Mark 0th node as visited
        v[0] = true;
        int ans = Integer.MAX_VALUE;

        // Find the minimum weight Hamiltonian Cycle
        ans = tsp(graph, v, 0, n, 1, 0, ans);

        // ans is the minimum weight Hamiltonian Cycle
        System.out.println(ans);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
V = 4
answer = []

# Function to find the minimum weight
# Hamiltonian Cycle
def tsp(graph, v, currPos, n, count, cost):

    # If last node is reached and it has
    # a link to the starting node i.e
    # the source then keep the minimum
    # value out of the total cost of
    # traversal and "ans"
    # Finally return to check for
    # more possible values
    if (count == n and graph[currPos][0]):
        answer.append(cost + graph[currPos][0])
        return

    # BACKTRACKING STEP
    # Loop to traverse the adjacency list
    # of currPos node and increasing the count
    # by 1 and cost by graph[currPos][i] value
    for i in range(n):
        if (v[i] == False and graph[currPos][i]):

            # Mark as visited
            v[i] = True
            tsp(graph, v, i, n, count + 1,
                cost + graph[currPos][i])

            # Mark ith node as unvisited
            v[i] = False

# Driver code

# n is the number of nodes i.e. V
if __name__ == '__main__':
    n = 4
    graph= [[ 0, 10, 15, 20 ],
            [ 10, 0, 35, 25 ],
            [ 15, 35, 0, 30 ],
            [ 20, 25, 30, 0 ]]

    # Boolean array to check if a node
    # has been visited or not
    v = [False for i in range(n)]

    # Mark 0th node as visited
    v[0] = True

    # Find the minimum weight Hamiltonian Cycle
    tsp(graph, v, 0, n, 1, 0)

    # ans is the minimum weight Hamiltonian Cycle
    print(min(answer))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the minimum weight Hamiltonian Cycle
static int tsp(int [,]graph, bool []v, int currPos,
        int n, int count, int cost, int ans)
{

    // If last node is reached and it has a link
    // to the starting node i.e the source then
    // keep the minimum value out of the total cost
    // of traversal and "ans"
    // Finally return to check for more possible values
    if (count == n && graph[currPos,0] > 0)
    {
        ans = Math.Min(ans, cost + graph[currPos,0]);
        return ans;
    }

    // BACKTRACKING STEP
    // Loop to traverse the adjacency list
    // of currPos node and increasing the count
    // by 1 and cost by graph[currPos,i] value
    for (int i = 0; i < n; i++) {
        if (v[i] == false && graph[currPos,i] > 0)
        {

            // Mark as visited
            v[i] = true;
            ans = tsp(graph, v, i, n, count + 1,
                cost + graph[currPos,i], ans);

            // Mark ith node as unvisited
            v[i] = false;
        }
    }
    return ans;
}

// Driver code
static void Main()
{
    // n is the number of nodes i.e. V
    int n = 4;

    int [,]graph = {
        { 0, 10, 15, 20 },
        { 10, 0, 35, 25 },
        { 15, 35, 0, 30 },
        { 20, 25, 30, 0 }
    };

    // Boolean array to check if a node
    // has been visited or not
    bool[] v = new bool[n];

    // Mark 0th node as visited
    v[0] = true;
    int ans = int.MaxValue;

    // Find the minimum weight Hamiltonian Cycle
    ans = tsp(graph, v, 0, n, 1, 0, ans);

    // ans is the minimum weight Hamiltonian Cycle
    Console.Write(ans);

}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var V = 4;
var ans = 1000000000;
// Boolean array to check if a node
// has been visited or not
var v = Array(n).fill(false);
// Mark 0th node as visited
v[0] = true;

// Function to find the minimum weight Hamiltonian Cycle
function tsp(graph, currPos, n, count, cost)
{

    // If last node is reached and it has a link
    // to the starting node i.e the source then
    // keep the minimum value out of the total cost
    // of traversal and "ans"
    // Finally return to check for more possible values
    if (count == n && graph[currPos][0]) {
        ans = Math.min(ans, cost + graph[currPos][0]);
        return;
    }

    // BACKTRACKING STEP
    // Loop to traverse the adjacency list
    // of currPos node and increasing the count
    // by 1 and cost by graph[currPos][i] value
    for (var i = 0; i < n; i++) {
        if (!v[i] && graph[currPos][i]) {

            // Mark as visited
            v[i] = true;
            tsp(graph, i, n, count + 1,
                cost + graph[currPos][i]);

            // Mark ith node as unvisited
            v[i] = false;
        }
    }
};

// Driver code
// n is the number of nodes i.e. V
var n = 4;
var graph = [
    [ 0, 10, 15, 20 ],
    [ 10, 0, 35, 25 ],
    [ 15, 35, 0, 30 ],
    [ 20, 25, 30, 0 ]
];

// Find the minimum weight Hamiltonian Cycle
tsp(graph, 0, n, 1, 0);
// ans is the minimum weight Hamiltonian Cycle
document.write( ans);

</script>
```

**Output:** 

```
80
```

**时间复杂度:** O(N！)，对于第一个节点有 N 种可能性，对于第二个节点有 N–1 种可能性。
对于 N 个节点，时间复杂度= N *(N–1)*。。。1 = 0(N！)
**辅助空间:** O(N)