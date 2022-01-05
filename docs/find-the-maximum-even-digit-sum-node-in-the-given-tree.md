# 在给定的树中找到最大偶数和节点

> 原文:[https://www . geeksforgeeks . org/find-给定树中的最大偶数和节点/](https://www.geeksforgeeks.org/find-the-maximum-even-digit-sum-node-in-the-given-tree/)

给定一个具有所有节点权重的**树**，任务是找到权重为偶数和的最大加权节点。

**示例:**

```
Input: Tree =
                 5
               /  \
             10    6
            /  \ 
           11   8  
Output: 11
Explanation:
The tree node weights are:
5 -> 5
10 -> 1 + 0 = 1
6 -> 6
11 -> 1 + 1 = 2
8 -> 8
Here, digit sum for nodes
containing 11, 6 and 8 are even.
Hence, the maximum weighing
even digit sum node is 11.

Input: Tree =
                1
               /  \
              4    7
             / \   / \
            11  3 15  8
Output: 15
Explanation:
Here, digit sum for nodes containing
4, 11, 15 and 8 are even. 
Hence, the maximum weighing 
even digit sum node is 15.
```

**方法:**要解决上述问题，请遵循以下步骤:

*   这个想法是对树和每个节点执行[深度优先搜索](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。
*   首先，通过迭代每个数字找到节点中权重的数字和，然后检查节点是否有偶数数字和。
*   最后，如果它有一个偶数和，那么检查这个节点是否是我们到目前为止找到的最大偶数和节点，如果是，那么使这个节点成为最大偶数和节点。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// maximum weighing node
// in the tree whose weight
// has an Even Digit Sum

#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;
int ans = -1;

vector<int> graph[100];
vector<int> weight(100);

// Function to find the digit sum
// for a number
int digitSum(int num)
{
    int sum = 0;
    while (num)
    {
        sum += (num % 10);
        num /= 10;
    }

    return sum;
}

// Function to perform dfs
void dfs(int node, int parent)
{
    // Check if the digit sum
    // of the node weight
    // is even or not
    if (!(digitSum(weight[node]) & 1))
        ans = max(ans, weight[node]);

    // Performing DFS to iterate the
    // remaining nodes
    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
int main()
{
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

    // Call the dfs function to
    // traverse through the tree
    dfs(1, 1);

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum weighing node
// in the tree whose weight
// has an Even Digit Sum
import java.util.*;
class GFG
{

    static int sz = (int)1e5;
    static int ans = -1;

    static Vector<Integer>[] graph = new Vector[100];
    static int[] weight = new int[100];

    // Function to find the digit sum
    // for a number
    static int digitSum(int num)
    {
        int sum = 0;
        while (num > 0)
        {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    // Function to perform dfs
    static void dfs(int node, int parent)
    {
        // Check if the digit sum
        // of the node weight
        // is even or not
        if (!(digitSum(weight[node]) % 2 == 1))
            ans = Math.max(ans, weight[node]);

        // Performing DFS to iterate the
        // remaining nodes
        for (int to : graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Weights of the node
        weight[1] = 5;
        weight[2] = 10;
        weight[3] = 11;
        weight[4] = 8;
        weight[5] = 6;
        for (int i = 0; i < graph.length; i++)
            graph[i] = new Vector<Integer>();
        // Edges of the tree
        graph[1].add(2);
        graph[2].add(3);
        graph[2].add(4);
        graph[1].add(5);

        // Call the dfs function to
        // traverse through the tree
        dfs(1, 1);

        System.out.print(ans + "\n");
    }
}

// This code contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum weighing node
# in the tree whose weight
# has an Even Digit Sum
sz = 1e5
ans = -1

graph = [[] for i in range(100)]
weight = [-1] * 100

# Function to find the digit sum
# for a number

def digitSum(num):
    sum = 0

    while num:
        sum += num % 10
        num = num // 10

    return sum

# Function to perform dfs

def dfs(node, parent):
    global ans

    # Check if the digit sum
    # of the node weight
    # is even or not
    if not(digitSum(weight[node]) & 1):
        ans = max(ans, weight[node])

    # Performing DFS to iterate the
    # remaining nodes
    for to in graph[node]:
        if to == parent:
            continue

        dfs(to, node)

# Driver code

def main():

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

    # Call the dfs function to
    # traverse through the tree
    dfs(1, 1)

    print(ans)

main()

# This code is contributed by stutipathak31jan
```

## C#

```
// C# program to find the
// maximum weighing node
// in the tree whose weight
// has an Even Digit Sum
using System;
using System.Collections.Generic;
class GFG
{

    static int sz = (int)1e5;
    static int ans = -1;

    static List<int>[] graph = new List<int>[ 100 ];
    static int[] weight = new int[100];

    // Function to find the digit sum
    // for a number
    static int digitSum(int num)
    {
        int sum = 0;
        while (num > 0)
        {
            sum += (num % 10);
            num /= 10;
        }
        return sum;
    }

    // Function to perform dfs
    static void dfs(int node, int parent)
    {
        // Check if the digit sum
        // of the node weight
        // is even or not
        if (!(digitSum(weight[node]) % 2 == 1))
            ans = Math.Max(ans, weight[node]);

        // Performing DFS to iterate the
        // remaining nodes
        foreach(int to in graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Weights of the node
        weight[1] = 5;
        weight[2] = 10;
        weight[3] = 11;
        weight[4] = 8;
        weight[5] = 6;
        for (int i = 0; i < graph.Length; i++)
            graph[i] = new List<int>();

        // Edges of the tree
        graph[1].Add(2);
        graph[2].Add(3);
        graph[2].Add(4);
        graph[1].Add(5);

        // Call the dfs function to
        // traverse through the tree
        dfs(1, 1);

        Console.Write(ans + "\n");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // maximum weighing node
    // in the tree whose weight
    // has an Even Digit Sum

    let sz = 1e5;
    let ans = -1;

    let graph = new Array(100);
    let weight = new Array(100);

    // Function to find the digit sum
    // for a number
    function digitSum(num)
    {
        let sum = 0;
        while (num > 0)
        {
            sum += (num % 10);
            num = parseInt(num / 10, 10);
        }
        return sum;
    }

    // Function to perform dfs
    function dfs(node, parent)
    {
        // Check if the digit sum
        // of the node weight
        // is even or not
        if (!(digitSum(weight[node]) % 2 == 1))
            ans = Math.max(ans, weight[node]);

        // Performing DFS to iterate the
        // remaining nodes
        for (let to = 0; to < graph[node].length; to++)
        {
            if (graph[node][to] == parent)
                continue;
            dfs(graph[node][to], node);
        }
    }

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;
    for (let i = 0; i < graph.length; i++)
      graph[i] = [];

    // Edges of the tree
    graph[1].push(2);
    graph[2].push(3);
    graph[2].push(4);
    graph[1].push(5);

    // Call the dfs function to
    // traverse through the tree
    dfs(1, 1);

    document.write(ans + "</br>");

// This code is contributed by decode2207.
</script>
```

**Output**

```
11
```

**<u>复杂度分析:</u>**

**时间复杂度:** O(N)。
在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 dfs 而导致的复杂性是 O(N)。此外，为了处理每个节点，使用了复杂度为 O(d)的 DigitSum()函数，其中 d 是节点权重中的位数，但是由于任何节点的权重都是整数，因此最多只能有 10 位，因此该函数不会影响整体时间复杂度。因此，时间复杂度为 O(N)。

**辅助空间:** O(1)。
不需要任何额外的空间，所以空间复杂度不变。