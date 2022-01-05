# 打印高度为素数的二叉树的节点

> 原文:[https://www . geeksforgeeks . org/print-the-the-nodes-of-the-the-the-the-the-the-the-the-the-the-nodes-of-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-the-](https://www.geeksforgeeks.org/print-the-nodes-of-the-binary-tree-whose-height-is-a-prime-number/)

给定一棵[](https://www.geeksforgeeks.org/binary-tree-data-structure/)**二叉树，我们的任务是从根节点开始打印高度为[素数](https://www.geeksforgeeks.org/prime-numbers/)的节点。**

****例:****

```
**Input:**     
             1
           /   \
          2     3
         /  \
        4    5
**Output:** 4 5
**Explanation:**
For this tree: 
Height of Node 1 - 0, 
Height of Node 2 - 1, 
Height of Node 3 - 1, 
Height of Node 4 - 2, 
Height of Node 5 - 2\. 
Hence, the nodes whose height
is a prime number are 4, and 5.

**Input:**     
             1
           /   \
          2     5
         /  \
        3    4
**Output:** 3 4
**Explanation:**
For this tree: 
Height of Node 1 - 0, 
Height of Node 2 - 1, 
Height of Node 3 - 2, 
Height of Node 4 - 2, 
Height of Node 5 - 1\. 
Hence, the nodes whose height
is a prime number are 3, and 4.
```

****方法:**为了解决上面提到的问题，**

***   We must perform [**Depth First Search (DFS)**](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) on the tree, and for each node, store the [height](https://www.geeksforgeeks.org/sum-heights-individual-nodes-binary-tree/) of each node when we move down.*   Iterate the height array of each node and check whether it is prime [or prime](https://www.geeksforgeeks.org/prime-numbers/) .*   If yes, print the node; otherwise, ignore it.**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of nodes
// at prime height in the given tree

#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

vector<int> graph[MAX + 1];

// To store Prime Numbers
vector<bool> Prime(MAX + 1, true);

// To store height of each node
int height[MAX + 1];

// Function to find the
// prime numbers till 10^5
void SieveOfEratosthenes()
{

    int i, j;
    Prime[0] = Prime[1] = false;
    for (i = 2; i * i <= MAX; i++) {

        // Traverse all multiple of i
        // and make it false
        if (Prime[i]) {

            for (j = 2 * i; j < MAX; j += i) {
                Prime[j] = false;
            }
        }
    }
}

// Function to perform dfs
void dfs(int node, int parent, int h)
{
    // Store the height of node
    height[node] = h;

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node, h + 1);
    }
}

// Function to find the nodes
// at prime height
void primeHeightNode(int N)
{
    // To precompute prime number till 10^5
    SieveOfEratosthenes();

    for (int i = 1; i <= N; i++) {
        // Check if height[node] is prime
        if (Prime[height[i]]) {
            cout << i << " ";
        }
    }
}

// Driver code
int main()
{
    // Number of nodes
    int N = 5;

    // Edges of the tree
    graph[1].push_back(2);
    graph[1].push_back(3);
    graph[2].push_back(4);
    graph[2].push_back(5);

    dfs(1, 1, 0);

    primeHeightNode(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of nodes
// at prime height in the given tree
import java.util.*;

class GFG{

static final int MAX = 100000;

@SuppressWarnings("unchecked")
static Vector<Integer> []graph = new Vector[MAX + 1];

// To store Prime Numbers
static boolean []Prime = new boolean[MAX + 1];

// To store height of each node
static int []height = new int[MAX + 1];

// Function to find the
// prime numbers till 10^5
static void SieveOfEratosthenes()
{
    int i, j;

    Prime[0] = Prime[1] = false;
    for(i = 2; i * i <= MAX; i++)
    {

        // Traverse all multiple of i
        // and make it false
        if (Prime[i])
        {

            for(j = 2 * i; j < MAX; j += i)
            {
                Prime[j] = false;
            }
        }
    }
}

// Function to perform dfs
static void dfs(int node, int parent, int h)
{

    // Store the height of node
    height[node] = h;

    for(int to : graph[node])
    {
        if (to == parent)
            continue;

        dfs(to, node, h + 1);
    }
}

// Function to find the nodes
// at prime height
static void primeHeightNode(int N)
{

    // To precompute prime number till 10^5
    SieveOfEratosthenes();

    for(int i = 1; i <= N; i++)
    {

        // Check if height[node] is prime
        if (Prime[height[i]])
        {
            System.out.print(i + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Number of nodes
    int N = 5;
    for(int i = 0; i < Prime.length; i++)
        Prime[i] = true;

    for(int i = 0; i < graph.length; i++)
        graph[i] = new Vector<Integer>();

    // Edges of the tree
    graph[1].add(2);
    graph[1].add(3);
    graph[2].add(4);
    graph[2].add(5);

    dfs(1, 1, 0);

    primeHeightNode(N);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 implementation of nodes
# at prime height in the given tree
MAX = 100000

graph = [[] for i in range(MAX + 1)]

# To store Prime Numbers
Prime = [True for i in range(MAX + 1)]

# To store height of each node
height = [0 for i in range(MAX + 1)]

# Function to find the
# prime numbers till 10^5
def SieveOfEratosthenes():

    Prime[0] = Prime[1] = False
    i = 2

    while i * i <= MAX:

        # Traverse all multiple of i
        # and make it false
        if (Prime[i]):
            for j in range(2 * i, MAX, i):
                Prime[j] = False

        i += 1

# Function to perform dfs
def dfs(node, parent, h):

    # Store the height of node
    height[node] = h

    for to in  graph[node]:
        if (to == parent):
            continue

        dfs(to, node, h + 1)

# Function to find the nodes
# at prime height
def primeHeightNode(N):

    # To precompute prime
    # number till 10^5
    SieveOfEratosthenes()

    for i in range(1, N + 1):

        # Check if height[node] is prime
        if (Prime[height[i]]):
            print(i, end = ' ')

# Driver code
if __name__=="__main__":

    # Number of nodes
    N = 5

    # Edges of the tree
    graph[1].append(2)
    graph[1].append(3)
    graph[2].append(4)
    graph[2].append(5)

    dfs(1, 1, 0)

    primeHeightNode(N)

# This code is contributed by rutvik_56
```

## **C#**

```
// C# implementation of nodes
// at prime height in the given tree
using System;
using System.Collections.Generic;
class GFG{
    static readonly int MAX = 100000;
    static List<int>[] graph = new List<int>[ MAX + 1 ];

    // To store Prime Numbers
    static bool[] Prime = new bool[MAX + 1];

    // To store height of each node
    static int[] height = new int[MAX + 1];

    // Function to find the
    // prime numbers till 10^5
    static void SieveOfEratosthenes()
    {
        int i, j;
        Prime[0] = Prime[1] = false;
        for (i = 2; i * i <= MAX; i++)
        {

            // Traverse all multiple of i
            // and make it false
            if (Prime[i])
            {
                for (j = 2 * i; j < MAX; j += i)
                {
                    Prime[j] = false;
                }
            }
        }
    }

    // Function to perform dfs
    static void dfs(int node, int parent, int h)
    {

        // Store the height of node
        height[node] = h;

        foreach(int to in graph[node])
        {
            if (to == parent)
                continue;
            dfs(to, node, h + 1);
        }
    }

    // Function to find the nodes
    // at prime height
    static void primeHeightNode(int N)
    {

        // To precompute prime number till 10^5
        SieveOfEratosthenes();

        for (int i = 1; i <= N; i++)
        {

            // Check if height[node] is prime
            if (Prime[height[i]])
            {
                Console.Write(i + " ");
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Number of nodes
        int N = 5;
        for (int i = 0; i < Prime.Length; i++)
            Prime[i] = true;

        for (int i = 0; i < graph.Length; i++)
            graph[i] = new List<int>();

        // Edges of the tree
        graph[1].Add(2);
        graph[1].Add(3);
        graph[2].Add(4);
        graph[2].Add(5);

        dfs(1, 1, 0);
        primeHeightNode(N);
    }
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>
// Javascript implementation of nodes
// at prime height in the given tree

let MAX = 100000;

let graph = []

for(let i = 0; i < MAX + 1; i++){
    graph.push([])
}

// To store Prime Numbers
let Prime = new Array(MAX + 1).fill(true);

// To store height of each node
let height = new Array(MAX + 1);

// Function to find the
// prime numbers till 10^5
function SieveOfEratosthenes()
{

    let i, j;
    Prime[0] = Prime[1] = false;
    for (i = 2; i * i <= MAX; i++) {

        // Traverse all multiple of i
        // and make it false
        if (Prime[i]) {

            for (j = 2 * i; j < MAX; j += i) {
                Prime[j] = false;
            }
        }
    }
}

// Function to perform dfs
function dfs(node, parent, h)
{
    // Store the height of node
    height[node] = h;

    for (let to of graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node, h + 1);
    }
}

// Function to find the nodes
// at prime height
function primeHeightNode(N)
{
    // To precompute prime number till 10^5
    SieveOfEratosthenes();

    for (let i = 1; i <= N; i++) {
        // Check if height[node] is prime
        if (Prime[height[i]]) {
            document.write(i + " ");
        }
    }
}

// Driver code
    // Number of nodes
    let N = 5;

    // Edges of the tree
    graph[1].push(2);
    graph[1].push(3);
    graph[2].push(4);
    graph[2].push(5);

    dfs(1, 1, 0);

    primeHeightNode(N);

// This code is contributed by gfgking
</script>
```

****Output:** 

```
4 5
```** 

**时间复杂度:0(N)**

**辅助空间:0(最大)**