# 查询加权树中给定节点到每个叶节点的距离之和

> 原文:[https://www . geesforgeks . org/query-to-find-给定节点到加权树中每个叶节点的距离总和/](https://www.geeksforgeeks.org/queries-to-find-sum-of-distance-of-a-given-node-to-every-leaf-node-in-a-weighted-tree/)

给定一个有 **N** 个节点和 **E** 条边的无向加权树。给定 **Q** 个查询，每个查询指示一个起始节点。任务是打印从给定起始节点**到加权树中每个叶节点的距离总和。
**示例:****

> **输入:** N = 5，E = 4，Q = 3
> **1**
> (4)/\(2)
> /\
> **4****2**
> (5)/\(3)
> /\
> **5****3**
> 查询 1: S **=** 1
> 
> 对于 S = 1，从节点 1 到叶节点的距离之和为:d(1，4) + d(1，3) + d(1，5) = 4 + (2 + 5) + (2 + 3) = 16。
> 对于 S = 3，节点 3 到其叶节点的距离之和为:d(3，4) + d(3，3) + d(3，5) = (3 + 2 + 4) + 0 + (3 + 5) = 17
> 对于 S = 5，节点 5 到其叶节点的距离之和为:d(5，4) + d(5，3) + d(5，5) = (5 + 2 + 4) + (5 + 3) + 0 = 19
> 
> **输入:** N = 3，E = 2，Q = 2
> **1**
> (9)/\(1)
> /\
> **2****3**T12】查询 1: S **=** 1
> 查询 2: S = 2
> 查询 3: S = 3
> **输出:**
> 10 【T23

**天真方法:**
对于每个查询，遍历整个树，找到从给定源节点到所有叶节点的距离总和。

***时间复杂度:** O(Q * N)*

**高效方法:**思想是利用[树上动态规划算法](https://www.geeksforgeeks.org/dynamic-programming-trees-set-1/)预先计算每个节点到所有叶节点的距离之和，在恒定时间内得到每个查询的答案。

按照以下步骤解决问题

*   初始化一个向量 **dp** 来存储从每个节点 **i** 到树的所有叶节点的距离之和。
*   初始化一个向量**叶子**来存储节点 **i** 的子树中叶子节点的计数，考虑 **1** 作为根节点。
*   使用改进的[深度优先搜索算法，将 **1** 视为根节点，计算从节点 **i** 到 **i** 子树中所有叶节点的距离总和。](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)

> 让节点 **a** 成为节点 **i** 的父节点
> 
> *   叶子[a] +=叶子[I]；
> *   dp[a] += dp[i] +叶[i] *节点(a，I)之间的边的权重；

*   使用重新生根技术，找出不在节点 **i** 的子树中的树的剩余叶子的距离。为了计算这些距离，使用另一个修改的深度优先搜索(DFS)算法来寻找并添加叶节点到节点 **i** 的距离之和。

> 让 **a** 为父节点， **i** 为子节点，然后
> 让存在于子树 **a** 中的子树 **i** 外的叶节点数为 **L**
> 
> *   L =叶子[a]–叶子[I]；
> *   DP[I]+=(DP[a]–DP[I])+(节点(a，I)之间的边的权重)*(L–叶子[I])；
> *   叶子[I]+= L；

下面是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// MAX size
const int N = 1e5 + 5;

// graph with {destination, weight};
vector<vector<pair<int, int> > > v(N);

// for storing the sum for ith node
vector<int> dp(N);

// leaves in subtree of ith.
vector<int> leaves(N);
int n;

// dfs to find sum of distance
// of leaves in the
// subtree of a node
void dfs(int a, int par)
{
    // flag is the node is
    // leaf or not;
    bool leaf = 1;
    for (auto& i : v[a]) {
        // skipping if parent
        if (i.first == par)
            continue;

        // setting flag to false
        leaf = 0;

        // doing dfs call
        dfs(i.first, a);
    }

    // doing calculation
    // in postorder.
    if (leaf == 1) {

        // if the node is leaf then
        // we just increment
        // the no. of leaves under
        // the subtree of a node
        leaves[a] += 1;
    }
    else {

        for (auto& i : v[a]) {
            if (i.first == par)
                continue;

            // adding num of leaves
            leaves[a]
                += leaves[i.first];

            // calculating answer for
            // the sum in the subtree
            dp[a] = dp[a]
                    + dp[i.first]
                    + leaves[i.first]
                          * i.second;
        }
    }
}

// dfs function to find the
// sum of distance of leaves
// outside the subtree
void dfs2(int a, int par)
{
    for (auto& i : v[a]) {
        if (i.first == par)
            continue;

        // number of leaves other
        // than the leaves in the
        // subtree of i
        int leafOutside = leaves[a] - leaves[i.first];

        // adding the contribution
        // of leaves outside to
        // the ith node
        dp[i.first] += (dp[a] - dp[i.first]);

        dp[i.first] += i.second
                       * (leafOutside
                          - leaves[i.first]);

        // adding the leafs outside
        // to ith node's leaves.
        leaves[i.first]
            += leafOutside;
        dfs2(i.first, a);
    }
}

void answerQueries(
    vector<int> queries)
{

    // calculating the sum of
    // distance of leaves in the
    // subtree of a node assuming
    // the root of the tree is 1
    dfs(1, 0);

    // calculating the sum of
    // distance of leaves outside
    // the subtree of node
    // assuming the root of the
    // tree is 1
    dfs2(1, 0);

    // answering the queries;
    for (int i = 0;
         i < queries.size(); i++) {
        cout << dp[queries[i]] << endl;
    }
}

// Driver Code
int main()
{
    // Driver Code
    /*
             1
       (4) /   \ (2)
          /     \
         4       2
             (5)/  \ (3)
               /    \
              5      3
    */

    n = 5;

    // initialising tree
    v[1].push_back(
        make_pair(4, 4));
    v[4].push_back(
        make_pair(1, 4));
    v[1].push_back(
        make_pair(2, 2));
    v[2].push_back(
        make_pair(1, 2));
    v[2].push_back(
        make_pair(3, 3));
    v[3].push_back(
        make_pair(2, 3));
    v[2].push_back(
        make_pair(5, 5));
    v[5].push_back(
        make_pair(2, 5));

    vector<int>
        queries = { 1, 3, 5 };
    answerQueries(queries);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;
import java.lang.*;

class GFG{

static class pair
{
    int first, second;

    pair(int f, int s)
    {
        this.first = f;
        this.second = s;
    }
}

// MAX size
static final int N = (int)1e5 + 5;

// Graph with {destination, weight};
static ArrayList<ArrayList<pair>> v;

// For storing the sum for ith node
static int[] dp = new int[N];

// Leaves in subtree of ith.
static int[] leaves = new int[N];
static int n;

// dfs to find sum of distance
// of leaves in the subtree of
// a node
static void dfs(int a, int par)
{

    // Flag is the node is
    // leaf or not;
    int leaf = 1;

    for(pair i : v.get(a))
    {

        // Skipping if parent
        if (i.first == par)
            continue;

        // Setting flag to false
        leaf = 0;

        // Doing dfs call
        dfs(i.first, a);
    }

    // Doing calculation
    // in postorder.
    if (leaf == 1)
    {

        // If the node is leaf then
        // we just increment the
        // no. of leaves under
        // the subtree of a node
        leaves[a] += 1;
    }
    else
    {
        for(pair i : v.get(a))
        {
            if (i.first == par)
                continue;

            // Adding num of leaves
            leaves[a] += leaves[i.first];

            // Calculating answer for
            // the sum in the subtree
            dp[a] = dp[a] + dp[i.first] +
                        leaves[i.first] *
                               i.second;
        }
    }
}

// dfs function to find the
// sum of distance of leaves
// outside the subtree
static void dfs2(int a, int par)
{
    for(pair i : v.get(a))
    {
        if (i.first == par)
            continue;

        // Number of leaves other
        // than the leaves in the
        // subtree of i
        int leafOutside = leaves[a] -
                          leaves[i.first];

        // Adding the contribution
        // of leaves outside to
        // the ith node
        dp[i.first] += (dp[a] - dp[i.first]);

        dp[i.first] += i.second *
                   (leafOutside -
                    leaves[i.first]);

        // Adding the leafs outside
        // to ith node's leaves.
        leaves[i.first] += leafOutside;
        dfs2(i.first, a);
    }
}

static void answerQueries(int[] queries)
{

    // Calculating the sum of
    // distance of leaves in the
    // subtree of a node assuming
    // the root of the tree is 1
    dfs(1, 0);

    // Calculating the sum of
    // distance of leaves outside
    // the subtree of node
    // assuming the root of the
    // tree is 1
    dfs2(1, 0);

    // Answering the queries;
    for(int i = 0; i < queries.length; i++)
    {
        System.out.println(dp[queries[i]]);
    }
}

// Driver code
public static void main(String[] args)
{

    /*
             1
       (4) /   \ (2)
          /     \
         4       2
             (5)/  \ (3)
               /    \
              5      3
    */

    n = 5;

    v = new ArrayList<>();
    for(int i = 0; i <= n; i++)
        v.add(new ArrayList<pair>());

    // Initialising tree
    v.get(1).add(new pair(4, 4));
    v.get(4).add(new pair(1, 4));
    v.get(1).add(new pair(2, 2));
    v.get(2).add(new pair(1, 2));
    v.get(2).add(new pair(3, 3));
    v.get(3).add(new pair(2, 3));
    v.get(2).add(new pair(5, 5));
    v.get(5).add(new pair(2, 5));

    // System.out.println(v);
    int[] queries = { 1, 3, 5 };

    answerQueries(queries);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above problem

# MAX size
N = 10 ** 5 + 5

# Graph with {destination, weight}
v = [[] for i in range(N)]

# For storing the sum for ith node
dp = [0] * N

# Leaves in subtree of ith.
leaves = [0] * (N)
n = 0

# dfs to find sum of distance
# of leaves in the subtree of
# a node
def dfs(a, par):

    # flag is the node is
    # leaf or not
    leaf = 1

    for i in v[a]:

        # Skipping if parent
        if (i[0] == par):
            continue

        # Setting flag to false
        leaf = 0

        # Doing dfs call
        dfs(i[0], a)

    # Doing calculation
    # in postorder.
    if (leaf == 1):

        # If the node is leaf then
        # we just increment
        # the no. of leaves under
        # the subtree of a node
        leaves[a] += 1
    else:
        for i in v[a]:
            if (i[0] == par):
                continue

            # Adding num of leaves
            leaves[a] += leaves[i[0]]

            # Calculating answer for
            # the sum in the subtree
            dp[a] = (dp[a] + dp[i[0]] +
                 leaves[i[0]] * i[1])

# dfs function to find the
# sum of distance of leaves
# outside the subtree
def dfs2(a, par):

    for i in v[a]:
        if (i[0] == par):
            continue

        # Number of leaves other
        # than the leaves in the
        # subtree of i
        leafOutside = leaves[a] - leaves[i[0]]

        # Adding the contribution
        # of leaves outside to
        # the ith node
        dp[i[0]] += (dp[a] - dp[i[0]])

        dp[i[0]] += i[1] * (leafOutside -
                            leaves[i[0]])

        # Adding the leafs outside
        # to ith node's leaves.
        leaves[i[0]] += leafOutside
        dfs2(i[0], a)

def answerQueries(queries):

    # Calculating the sum of
    # distance of leaves in the
    # subtree of a node assuming
    # the root of the tree is 1
    dfs(1, 0)

    # Calculating the sum of
    # distance of leaves outside
    # the subtree of node
    # assuming the root of the
    # tree is 1
    dfs2(1, 0)

    # Answering the queries
    for i in range(len(queries)):
        print(dp[queries[i]])

# Driver Code
if __name__ == '__main__':

    #          1
    #    (4) /   \ (2)
    #       /     \
    #      4       2
    #          (5)/  \ (3)
    #            /    \
    #           5      3
    #

    n = 5

    # Initialising tree
    v[1].append([4, 4])
    v[4].append([1, 4])
    v[1].append([2, 2])
    v[2].append([1, 2])
    v[2].append([3, 3])
    v[3].append([2, 3])
    v[2].append([5, 5])
    v[5].append([2, 5])

    queries = [ 1, 3, 5 ]

    answerQueries(queries)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above problem
using System;
using System.Collections.Generic;
class GFG {

    // MAX size
    static int N = 100005;

    // Graph with {destination, weight}
    static List<List<Tuple<int,int>>> v = new List<List<Tuple<int,int>>>();

    // For storing the sum for ith node
    static int[] dp = new int[N];

    // Leaves in subtree of ith.
    static int[] leaves = new int[N];

    // dfs to find sum of distance
    // of leaves in the subtree of
    // a node
    static void dfs(int a, int par)
    {
        // flag is the node is
        // leaf or not
        bool leaf = true;

        foreach(Tuple<int,int> i in v[a])
        {
            // Skipping if parent
            if (i.Item1 == par)
                continue;

            // Setting flag to false
            leaf = false;

            // Doing dfs call
            dfs(i.Item1, a);
        }

        // Doing calculation
        // in postorder.
        if (leaf == true)
        {
            // If the node is leaf then
            // we just increment
            // the no. of leaves under
            // the subtree of a node
            leaves[a] += 1;
        }
        else
        {
            foreach(Tuple<int,int> i in v[a])
            {
                if (i.Item1 == par)
                    continue;

                // Adding num of leaves
                leaves[a] += leaves[i.Item1];

                // Calculating answer for
                // the sum in the subtree
                dp[a] = (dp[a] + dp[i.Item1] + leaves[i.Item1] * i.Item2);
            }
        }
    }

    // dfs function to find the
    // sum of distance of leaves
    // outside the subtree
    static void dfs2(int a, int par)
    {
        foreach(Tuple<int,int> i in v[a])
        {
            if (i.Item1 == par)
                continue;

            // Number of leaves other
            // than the leaves in the
            // subtree of i
            int leafOutside = leaves[a] - leaves[i.Item1];

            // Adding the contribution
            // of leaves outside to
            // the ith node
            dp[i.Item1] += (dp[a] - dp[i.Item1]);

            dp[i.Item1] += i.Item2 * (leafOutside - leaves[i.Item1]);

            // Adding the leafs outside
            // to ith node's leaves.
            leaves[i.Item1] += leafOutside;
            dfs2(i.Item1, a);
        }
    }

    static void answerQueries(List<int> queries)
    {
        // Calculating the sum of
        // distance of leaves in the
        // subtree of a node assuming
        // the root of the tree is 1
        dfs(1, 0);

        // Calculating the sum of
        // distance of leaves outside
        // the subtree of node
        // assuming the root of the
        // tree is 1
        dfs2(1, 0);

        // Answering the queries
        for(int i = 0; i < queries.Count; i++)
            Console.WriteLine(dp[queries[i]]);
    }

  static void Main() {
    // Driver Code
    /*
             1
       (4) /   \ (2)
          /     \
         4       2
             (5)/  \ (3)
               /    \
              5      3
    */

    for(int i = 0; i < N; i++)
    {
        v.Add(new List<Tuple<int,int>>());
    }

    // initialising tree
    v[1].Add(new Tuple<int,int>(4,4));
    v[4].Add(new Tuple<int,int>(1,4));
    v[1].Add(new Tuple<int,int>(2,2));
    v[2].Add(new Tuple<int,int>(1,2));
    v[2].Add(new Tuple<int,int>(3,3));
    v[3].Add(new Tuple<int,int>(2,3));
    v[2].Add(new Tuple<int,int>(5,5));
    v[5].Add(new Tuple<int,int>(2,5));

    List<int> queries = new List<int>{ 1, 3, 5 };
    answerQueries(queries);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// JavaScript program for the above problem

class pair
{
    constructor(f,s)
    {
        this.first = f;
        this.second = s;
    }
}

// MAX size
let N = 1e5 + 5;

// Graph with {destination, weight};
let v=[];

// For storing the sum for ith node
let dp = new Array(N);

// Leaves in subtree of ith.
let leaves = new Array(N);
for(let i=0;i<N;i++)
{
    dp[i]=0;
    leaves[i]=0;
}

let n;

// dfs to find sum of distance
// of leaves in the subtree of
// a node
function dfs(a,par)
{
    // Flag is the node is
    // leaf or not;
    let leaf = 1;

    for(let i=0;i<v[a].length;i++)
    {

        // Skipping if parent
        if (v[a][i].first == par)
            continue;

        // Setting flag to false
        leaf = 0;

        // Doing dfs call
        dfs(v[a][i].first, a);
    }

    // Doing calculation
    // in postorder.
    if (leaf == 1)
    {

        // If the node is leaf then
        // we just increment the
        // no. of leaves under
        // the subtree of a node
        leaves[a] += 1;
    }
    else
    {
        for(let i=0;i<v[a].length;i++)
        {
            if (v[a][i].first == par)
                continue;

            // Adding num of leaves
            leaves[a] += leaves[v[a][i].first];

            // Calculating answer for
            // the sum in the subtree
            dp[a] = dp[a] + dp[v[a][i].first] +
                        leaves[v[a][i].first] *
                               v[a][i].second;
        }
    }
}

// dfs function to find the
// sum of distance of leaves
// outside the subtree
function dfs2(a,par)
{
    for(let i=0;i< v[a].length;i++)
    {
        if (v[a][i].first == par)
            continue;

        // Number of leaves other
        // than the leaves in the
        // subtree of i
        let leafOutside = leaves[a] -
                          leaves[v[a][i].first];

        // Adding the contribution
        // of leaves outside to
        // the ith node
        dp[v[a][i].first] += (dp[a] - dp[v[a][i].first]);

        dp[v[a][i].first] += v[a][i].second *
                   (leafOutside -
                    leaves[v[a][i].first]);

        // Adding the leafs outside
        // to ith node's leaves.
        leaves[v[a][i].first] += leafOutside;
        dfs2(v[a][i].first, a);
    }
}

function answerQueries(queries)
{
    // Calculating the sum of
    // distance of leaves in the
    // subtree of a node assuming
    // the root of the tree is 1
    dfs(1, 0);

    // Calculating the sum of
    // distance of leaves outside
    // the subtree of node
    // assuming the root of the
    // tree is 1
    dfs2(1, 0);

    // Answering the queries;
    for(let i = 0; i < queries.length; i++)
    {
        document.write(dp[queries[i]]+"<br>");
    }
}

// Driver code
/*
             1
       (4) /   \ (2)
          /     \
         4       2
             (5)/  \ (3)
               /    \
              5      3
    */

n = 5;

v = [];
for(let i = 0; i <= n; i++)
    v.push([]);

// Initialising tree
v[1].push(new pair(4, 4));
v[4].push(new pair(1, 4));
v[1].push(new pair(2, 2));
v[2].push(new pair(1, 2));
v[2].push(new pair(3, 3));
v[3].push(new pair(2, 3));
v[2].push(new pair(5, 5));
v[5].push(new pair(2, 5));

// System.out.println(v);
let queries = [ 1, 3, 5 ];

answerQueries(queries);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
16
17
19
```

***时间复杂度:** O(N + Q)*
***辅助空间:** O(N)*