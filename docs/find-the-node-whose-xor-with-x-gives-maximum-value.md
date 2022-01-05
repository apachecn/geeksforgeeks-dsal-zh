# 找到与 x 异或得到最大值的节点

> 原文:[https://www . geesforgeks . org/find-the-node-what-xor-with-x-给出-最大值/](https://www.geeksforgeeks.org/find-the-node-whose-xor-with-x-gives-maximum-value/)

给定一棵树，所有节点的权重和一个整数 **x** ，任务是找到一个节点 **i** ，使得**权重【I】xor x**最大。
**举例:**

> **输入:**
> 
> ![](img/107072b5f698ad7b63297c5c333d9375.png)
> 
> x = 15
> **输出:** 1
> 节点 1: 5 异或 15 = 10
> 节点 2: 10 异或 15 = 5
> 节点 3: 11 异或 15 = 4
> 节点 4: 8 异或 15 = 7
> 节点 5: 6 异或 15 = 9

**方法:**在树上执行 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 并跟踪其与 **x** 的加权异或得到最大值的节点。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int maximum = INT_MIN, x, ans;

vector<int> graph[100];
vector<int> weight(100);

// Function to perform dfs to find
// the maximum xored value
void dfs(int node, int parent)
{
    // If current value is less than
    // the current maximum
    if (maximum < (weight[node] ^ x)) {
        maximum = weight[node] ^ x;
        ans = node;
    }
    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
int main()
{
    x = 15;

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[2].push_back(4);
    graph[1].push_back(5);

    dfs(1, 1);

    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static int maximum = Integer.MIN_VALUE, x, ans;

    @SuppressWarnings("unchecked")
    static Vector<Integer>[] graph = new Vector[100];
    static int[] weight = new int[100];

    // This block is executed even before main() function
    // This is necessary otherwise this program will
    // throw "NullPointerException"
    static
    {
        for (int i = 0; i < 100; i++)
            graph[i] = new Vector<>();
    }

    // Function to perform dfs to find
    // the maximum xored value
    static void dfs(int node, int parent)
    {

        // If current value is less than
        // the current maximum
        if (maximum < (weight[node] ^ x))
        {
            maximum = weight[node] ^ x;
            ans = node;
        }
        for (int to : graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        x = 15;

        // Weights of the node
        weight[1] = 5;
        weight[2] = 10;
        weight[3] = 11;
        weight[4] = 8;
        weight[5] = 6;

        // Edges of the tree
        graph[1].add(2);
        graph[2].add(3);
        graph[2].add(4);
        graph[1].add(5);

        dfs(1, 1);

        System.out.println(ans);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys
maximum = -sys.maxsize - 1
graph = [[0 for i in range(100)]
            for j in range(100)]
weight = [0 for i in range(100)]
ans = []

# Function to perform dfs to find
# the maximum xored value
def dfs(node, parent):
    global maximum

    # If current value is less than
    # the current maximum
    if (maximum < (weight[node] ^ x)):
        maximum = weight[node] ^ x
        ans.append(node)

    for to in graph[node]:
        if (to == parent):
            continue
        dfs(to, node)

# Driver code
if __name__ == '__main__':
    x = 15

    # Weights of the node
    weight[1] = 5
    weight[2] = 10
    weight[3] = 11
    weight[4] = 8
    weight[5] = 6

    # Edges of the tree
    graph[1].append(2)
    graph[2].append(3)
    graph[2].append(4)
    graph[1].append(5)

    dfs(1, 1)

    print(ans[0])

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int maximum = int.MinValue, x,
ans = int.MaxValue;

static List<List<int>> graph = new List<List<int>>();
static List<int> weight = new List<int>();

// Function to perform dfs to find
// the maximum value
static void dfs(int node, int parent)
{
    // If current value is less than
    // the current maximum
    if (maximum < (weight[node] ^ x))
    {
        maximum = weight[node] ^ x;
        ans = node;
    }

    for (int i = 0; i < graph[node].Count; i++)
    {
        if (graph[node][i] == parent)
            continue;
        dfs(graph[node][i], node);
    }
}

// Driver code
public static void Main()
{
    x = 15;

    // Weights of the node
    weight.Add(0);
    weight.Add(5);
    weight.Add(10);
    weight.Add(11);;
    weight.Add(8);
    weight.Add(6);

    for(int i = 0; i < 100; i++)
    graph.Add(new List<int>());

    // Edges of the tree
    graph[1].Add(2);
    graph[2].Add(3);
    graph[2].Add(4);
    graph[1].Add(5);

    dfs(1, 1);
    Console.Write( ans);
}
}

// This code is contributed by SHUBHAMSINGH10
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let maximum = Number.MIN_SAFE_INTEGER;
let ans = [];

let graph = new Array();

for(let i = 0; i < 100; i++){
    graph.push(new Array().fill(0));
}

let weight = new Array(100).fill(0);

// Function to perform dfs to find
// the maximum xored value
function dfs(node, parent) {
    // If current value is less than
    // the current maximum
    if (maximum < (weight[node] ^ x)) {
        maximum = weight[node] ^ x;
        ans = node;
    }
    for (let to of graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code

let x = 15;

// Weights of the node
weight[1] = 5;
weight[2] = 10;
weight[3] = 11;
weight[4] = 8;
weight[5] = 6;

// Edges of the tree
graph[1].push(2);
graph[2].push(3);
graph[2].push(4);
graph[1].push(5);

dfs(1, 1);

document.write(ans);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
1
```

**<u>复杂度分析:</u>**

*   **时间复杂度:** O(N)。
    在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 dfs 而导致的复杂性是 O(N)。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(1)。
    不需要任何额外的空间，所以空间复杂度不变。