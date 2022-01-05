# 在图形的 DFS 中打印访问前和访问后时间

> 原文:[https://www . geeksforgeeks . org/printing-图中 dfs 的访问前和访问后时间/](https://www.geeksforgeeks.org/printing-pre-and-post-visited-times-in-dfs-of-a-graph/)

[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) (DFS)将图的所有顶点标记为已访问。因此，为了使 DFS 有用，还可以存储一些附加信息。例如，运行 DFS 时访问顶点的顺序。

访问前和访问后号码是在图表上运行 DFS 时可以存储的额外信息，事实证明这些信息非常有用。前访号告诉节点进入递归栈的时间，后访号告诉节点从 DFS 递归栈出来的时间。

**示例:**

![](img/6703e1d73a81214b5ac8e7a1942e76eb.png)

括号内的数字表示【就诊前号、就诊后号】。

> **Pre** 和 **Post** 数字广泛用于**图形算法**。例如，它们可以用于找出特定的**节点是否位于另一个节点**的子树中。
> 为了发现 **u** 是否位于 **v** 的**子树**中，我们只需比较 u 和 v 的前置和后置编号，如果**前置【u】>前置【v】**和**后置【u】<后置【v】**则 **u** 位于 **v** 的子树中，否则不会。你可以看上面的例子来获得更多的说明。

通过简单的 DFS 可以找到访问前和访问后的号码。我们将采用两个数组，一个用于存储前置数字，一个用于后置数字，并采用一个变量来记录时间。下面给出了相同的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Variable to keep track of time
int Time = 1;

// Function to perform DFS starting from node u
void dfs(int u, vector<vector<int>> aList,
                       vector<int> &pre,
                       vector<int> &post,
                       vector<int> &vis)
{

    // Storing the pre number whenever
    // the node comes into recursion stack
    pre[u] = Time;

    // Increment time
    Time++;
    vis[u] = 1;

    for(int v : aList[u])
    {
        if (vis[v] == 0)
            dfs(v, aList, pre, post, vis);
    }

    // Storing the post number whenever
    // the node goes out of recursion stack
    post[u] = Time;
    Time++;
}

// Driver Code   
int main()
{

    // Number of nodes in graph
    int n = 6;

    // Adjacency list
    vector<vector<int>> aList(n + 1);

    vector<int> pre(n + 1);
    vector<int> post(n + 1);

    // Visited array
    vector<int> vis(n + 1);

    // Edges
    aList[1].push_back(2);
    aList[2].push_back(1);
    aList[2].push_back(4);
    aList[4].push_back(2);
    aList[1].push_back(3);
    aList[3].push_back(1);
    aList[3].push_back(4);
    aList[4].push_back(3);
    aList[3].push_back(5);
    aList[5].push_back(3);
    aList[5].push_back(6);
    aList[6].push_back(5);

    // DFS starting at Node 1
    dfs(1, aList, pre, post, vis);

    // Number of nodes in graph
    for(int i = 1; i <= n; i++)
        cout << "Node " << i << " Pre number "
             << pre[i] << " Post number "
             << post[i] << endl;

    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class GFG {

    // Variable to keep track of time
    static int time = 1;

    // Function to perform DFS starting from node u
    static void dfs(int u, ArrayList<ArrayList<Integer> > aList,
                    int pre[], int post[], int vis[])
    {

        // Storing the pre number whenever
        // the node comes into recursion stack
        pre[u] = time;

        // Increment time
        time++;
        vis[u] = 1;
        for (int v : aList.get(u)) {
            if (vis[v] == 0)
                dfs(v, aList, pre, post, vis);
        }

        // Storing the post number whenever
        // the node goes out of recursion stack
        post[u] = time;
        time++;
    }

    // Driver code
    public static void main(String args[])
    {

        // Number of nodes in graph
        int n = 6;

        // Adjacency list
        ArrayList<ArrayList<Integer> > aList
            = new ArrayList<ArrayList<Integer> >(n + 1);
        for (int i = 1; i <= n; i++) {
            ArrayList<Integer> list = new ArrayList<>();
            aList.add(list);
        }
        aList.add(new ArrayList<Integer>());
        int pre[] = new int[n + 1];
        int post[] = new int[n + 1];

        // Visited array
        int vis[] = new int[n + 1];

        // Edges
        aList.get(1).add(2);
        aList.get(2).add(1);
        aList.get(2).add(4);
        aList.get(4).add(2);
        aList.get(1).add(3);
        aList.get(3).add(1);
        aList.get(3).add(4);
        aList.get(4).add(3);
        aList.get(3).add(5);
        aList.get(5).add(3);
        aList.get(5).add(6);
        aList.get(6).add(5);

        // DFS starting at Node 1
        dfs(1, aList, pre, post, vis);

        // Number of nodes in graph
        for (int i = 1; i <= n; i++)
            System.out.println("Node " + i + " Pre number "
                               + pre[i] + " Post number " + post[i]);
    }
}
```

## 蟒蛇 3

```
# Variable to keep track of time
time = 1

# Function to perform DFS starting
# from node u
def dfs(u, aList, pre, post, vis):

    global time

    # Storing the pre number whenever
    # the node comes into recursion stack
    pre[u] = time

    # Increment time
    time += 1

    vis[u] = 1

    for v in aList[u]:
        if (vis[v] == 0):
            dfs(v, aList, pre, post, vis)

    # Storing the post number whenever
    # the node goes out of recursion stack
    post[u] = time
    time += 1

# Driver code
if __name__=='__main__':

    # Number of nodes in graph
    n = 6

    # Adjacency list
    aList = [[] for i in range(n + 1)]

    pre = [0 for i in range(n + 1)]
    post = [0 for i in range(n + 1)]

    # Visited array
    vis = [0 for i in range(n + 1)]

    # Edges
    aList[1].append(2)
    aList[2].append(1)
    aList[2].append(4)
    aList[4].append(2)
    aList[1].append(3)
    aList[3].append(1)
    aList[3].append(4)
    aList[4].append(3)
    aList[3].append(5)
    aList[5].append(3)
    aList[5].append(6)
    aList[6].append(5)

    # DFS starting at Node 1
    dfs(1, aList, pre, post, vis)

    # Number of nodes in graph
    for i in range(1, n + 1):
        print("Node " + str(i) +
              " Pre number " + str(pre[i]) +
              " Post number " + str(post[i]))

# This code is contributed by rutvik_56
```

## C#

```
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Variable to keep track of time
static int time = 1;

// Function to perform DFS starting from node u
static void dfs(int u, ArrayList aList,
                int []pre, int []post,
                int []vis)
{

    // Storing the pre number whenever
    // the node comes into recursion stack
    pre[u] = time;

    // Increment time
    time++;
    vis[u] = 1;

    foreach(int v in (ArrayList)aList[u])
    {
        if (vis[v] == 0)
            dfs(v, aList, pre, post, vis);
    }

    // Storing the post number whenever
    // the node goes out of recursion stack
    post[u] = time;
    time++;
}

// Driver code
public static void Main(string []args)
{

    // Number of nodes in graph
    int n = 6;

    // Adjacency list
    ArrayList aList = new ArrayList(n + 1);

    for(int i = 1; i <= n; i++)
    {
        ArrayList list = new ArrayList();
        aList.Add(list);
    }
    aList.Add(new ArrayList());
    int []pre = new int[n + 1];
    int []post = new int[n + 1];

    // Visited array
    int []vis = new int[n + 1];

    // Edges
    ((ArrayList)aList[1]).Add(2);
    ((ArrayList)aList[2]).Add(1);
    ((ArrayList)aList[2]).Add(4);
    ((ArrayList)aList[4]).Add(2);
    ((ArrayList)aList[1]).Add(3);
    ((ArrayList)aList[3]).Add(1);
    ((ArrayList)aList[3]).Add(4);
    ((ArrayList)aList[4]).Add(3);
    ((ArrayList)aList[3]).Add(5);
    ((ArrayList)aList[5]).Add(3);
    ((ArrayList)aList[5]).Add(6);
    ((ArrayList)aList[6]).Add(5);

    // DFS starting at Node 1
    dfs(1, aList, pre, post, vis);

    // Number of nodes in graph
    for(int i = 1; i <= n; i++)
        Console.WriteLine("Node " + i +
                          " Pre number " + pre[i] +
                          " Post number " + post[i]);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>
    // Variable to keep track of time
    let time = 1;

    // Function to perform DFS starting
    // from node u
    function dfs(u, aList, pre, post, vis)
    {

        // Storing the pre number whenever
        // the node comes into recursion stack
        pre[u] = time;

        // Increment time
        time += 1;

        vis[u] = 1;

        for(let v = 0; v < aList[u].length; v++)
        {
            if (vis[aList[u][v]] == 0)
                dfs(aList[u][v], aList, pre, post, vis);
        }

        // Storing the post number whenever
        // the node goes out of recursion stack
        post[u] = time;
        time += 1;
   }

  // Number of nodes in graph
  let n = 6;

  // Adjacency list
  let aList = [];
  for(let i = 0; i < (n + 1); i++)
  {
      aList.push([]);
  }

  let pre = new Array(n+1);
  let post = new Array(n+1);
  pre.fill(0);
  post.fill(0);

  // Visited array
  let vis = new Array(n+1);
  vis.fill(0);

  // Edges
  aList[1].push(2);
  aList[2].push(1);
  aList[2].push(4);
  aList[4].push(2);
  aList[1].push(3);
  aList[3].push(1);
  aList[3].push(4);
  aList[4].push(3);
  aList[3].push(5);
  aList[5].push(3);
  aList[5].push(6);
  aList[6].push(5);

  // DFS starting at Node 1
  dfs(1, aList, pre, post, vis);

  // Number of nodes in graph
  for(let i = 1; i < n + 1; i++)
  {
    document.write("Node " + i +
          " Pre number " + pre[i] +
          " Post number " + post[i] + "</br>")
  }

 // This code is contributed by suresh07.
</script>
```

**Output:** 

```
Node 1 Pre number 1 Post number 12
Node 2 Pre number 2 Post number 11
Node 3 Pre number 4 Post number 9
Node 4 Pre number 3 Post number 10
Node 5 Pre number 5 Post number 8
Node 6 Pre number 6 Post number 7
```