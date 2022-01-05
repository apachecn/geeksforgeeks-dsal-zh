# 给定一个 n 元树，计算子节点数多于父节点数的节点数

> 原文:[https://www . geesforgeks . org/given-n-ary-tree-count-number-nodes-number-children-parent/](https://www.geeksforgeeks.org/given-n-ary-tree-count-number-nodes-number-children-parent/)

给定一个用邻接表表示的 N 叉树，我们需要编写一个程序来计算这个树中所有这样的节点，这个树的子节点比它的父节点多。
例如

![](img/2b95d48f92fe81b043f264aab93f6bd5.png)

在上面的树中，计数将为 1，因为只有一个这样的节点“2”比它的父节点有更多的子节点。2 有三个孩子(4、5 和 6)，而它的父母 1 只有两个孩子(2 和 3)。

我们可以使用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 和 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 算法来解决这个问题。我们将在这里详细解释如何使用 BFS 算法解决这个问题。
由于树是用邻接表表示的。因此，对于任何一个节点，比如说“u”，这个节点的子节点数可以用 adj[u]来表示。大小()。
现在的想法是在给定的树上应用 BFS，当遍历节点“u”的子节点时，说“v”，我们将简单地检查 is adj[v]。尺寸()>可调。大小()。
以下是上述思路的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count number of nodes
// which has more children than its parent

#include<bits/stdc++.h>
using namespace std;

// function to count number of nodes
// which has more children than its parent
int countNodes(vector<int> adj[], int root)
{   
    int count = 0;

    // queue for applying BFS
    queue<int> q;

    // BFS algorithm
    q.push(root);

    while (!q.empty())
    {
        int node = q.front();
        q.pop();

        // traverse children of node
        for( int i=0;i<adj[node].size();i++)
        {   
            // children of node
            int children = adj[node][i];

            // if number of childs of children
            // is greater than number of childs
            // of node, then increment count
            if (adj[children].size() > adj[node].size())
                count++;
            q.push(children);
        }
    }

    return count;
}

// Driver program to test above functions
int main()
{   
    // adjacency list for n-ary tree
    vector<int> adj[10];

    // construct n ary tree as shown
    // in above diagram
    adj[1].push_back(2);
    adj[1].push_back(3);
    adj[2].push_back(4);
    adj[2].push_back(5);
    adj[2].push_back(6);
    adj[3].push_back(9);
    adj[5].push_back(7);
    adj[5].push_back(8);

    int root = 1;

    cout << countNodes(adj, root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of nodes
// which has more children than its parent
import java.util.*;

class GFG
{

// function to count number of nodes
// which has more children than its parent
static int countNodes(Vector<Integer> adj[], int root)
{
    int count = 0;

    // queue for applying BFS
    Queue<Integer> q = new LinkedList<>();

    // BFS algorithm
    q.add(root);

    while (!q.isEmpty())
    {
        int node = q.peek();
        q.remove();

        // traverse children of node
        for( int i=0;i<adj[node].size();i++)
        {
            // children of node
            int children = adj[node].get(i);

            // if number of childs of children
            // is greater than number of childs
            // of node, then increment count
            if (adj[children].size() > adj[node].size())
                count++;
            q.add(children);
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    // adjacency list for n-array tree
    Vector<Integer> []adj = new Vector[10];
    for(int i= 0; i < 10 ; i++) {
        adj[i] = new Vector<>();
    }

    // conn array tree as shown
    // in above diagram
    adj[1].add(2);
    adj[1].add(3);
    adj[2].add(4);
    adj[2].add(5);
    adj[2].add(6);
    adj[3].add(9);
    adj[5].add(7);
    adj[5].add(8);

    int root = 1;

    System.out.print(countNodes(adj, root));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to count number of nodes
# which has more children than its parent
from collections import deque

adj = [[] for i in range(100)]

# function to count number of nodes
# which has more children than its parent
def countNodes(root):

    count = 0

    # queue for applying BFS
    q = deque()

    # BFS algorithm
    q.append(root)

    while len(q) > 0:

        node = q.popleft()

        # traverse children of node
        for i in adj[node]:
            # children of node
            children = i

            # if number of childs of children
            # is greater than number of childs
            # of node, then increment count
            if (len(adj[children]) > len(adj[node])):
                count += 1
            q.append(children)

    return count

# Driver program to test above functions

# construct n ary tree as shown
# in above diagram
adj[1].append(2)
adj[1].append(3)
adj[2].append(4)
adj[2].append(5)
adj[2].append(6)
adj[3].append(9)
adj[5].append(7)
adj[5].append(8)

root = 1

print(countNodes(root))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count number of nodes
// which has more children than its parent
using System;
using System.Collections.Generic;

class GFG
{

// function to count number of nodes
// which has more children than its parent
static int countNodes(List<int> []adj, int root)
{
    int count = 0;

    // queue for applying BFS
    List<int> q = new List<int>();

    // BFS algorithm
    q.Add(root);

    while (q.Count != 0)
    {
        int node = q[0];
        q.RemoveAt(0);

        // traverse children of node
        for( int i = 0; i < adj[node].Count; i++)
        {
            // children of node
            int children = adj[node][i];

            // if number of childs of children
            // is greater than number of childs
            // of node, then increment count
            if (adj[children].Count > adj[node].Count)
                count++;
            q.Add(children);
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    // adjacency list for n-array tree
    List<int> []adj = new List<int>[10];
    for(int i= 0; i < 10 ; i++) {
        adj[i] = new List<int>();
    }

    // conn array tree as shown
    // in above diagram
    adj[1].Add(2);
    adj[1].Add(3);
    adj[2].Add(4);
    adj[2].Add(5);
    adj[2].Add(6);
    adj[3].Add(9);
    adj[5].Add(7);
    adj[5].Add(8);

    int root = 1;

    Console.Write(countNodes(adj, root));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to count number of nodes
// which has more children than its parent

    // function to count number of nodes
// which has more children than its parent
    function countNodes(adj,root)
    {
        let count = 0;

    // queue for applying BFS
    let q = [];

    // BFS algorithm
    q.push(root);

    while (q.length!=0)
    {
        let node = q[0];
        q.shift();

        // traverse children of node
        for( let i=0;i<adj[node].length;i++)
        {
            // children of node
            let children = adj[node][i];

            // if number of childs of children
            // is greater than number of childs
            // of node, then increment count
            if (adj[children].length > adj[node].length)
                count++;
            q.push(children);
        }
    }
    return count;
    }

    // Driver code

     // adjacency list for n-array tree
    let adj = [];
    for(let i= 0; i < 10 ; i++) {
        adj[i] = [];
    }

    // conn array tree as shown
    // in above diagram
    adj[1].push(2);
    adj[1].push(3);
    adj[2].push(4);
    adj[2].push(5);
    adj[2].push(6);
    adj[3].push(9);
    adj[5].push(7);
    adj[5].push(8);

    let root = 1;

    document.write(countNodes(adj, root));

// This code is contributed by patel2127
</script>
```

**输出:**

```
1
```

**时间复杂度** : O( n)，其中 n 为树中节点数。

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。