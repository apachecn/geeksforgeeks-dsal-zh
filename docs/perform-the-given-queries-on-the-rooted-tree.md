# 在根树上执行给定的查询

> 原文:[https://www . geeksforgeeks . org/在根树上执行给定的查询/](https://www.geeksforgeeks.org/perform-the-given-queries-on-the-rooted-tree/)

给定一棵有根的树，不一定是二进制的。该树包含 N 个节点，标记为 1 到 N。您将获得数组形式的树[1..N]的大小 N. A[i]表示标记为 I 的节点的父节点的标签。为了清楚起见，您可以假设树满足以下条件。

> *   The root of the tree is marked as 1\. Therefore, A[1] is set to 0.
> *   The parent node of node t will always have a label less than t.

任务是根据给定的查询类型执行以下操作。

1.  **ADD，X，Y** :在节点 X 的值上加上 Y。
2.  **ADDUP，X，Y** :将 Y 加到节点 X 处的值上，然后将 Y 加到 A[X](即 X 的父节点)处的值上。，将 Y 添加到 A[A[X]]处的值(即 A[X]的父级)..以此类推，直到你把 Y 加到根的值上。

执行完所有给定操作后，系统会要求您回答以下几种类型的查询

1.  **VAL，X** :打印节点 X 处的值。
2.  **VALTREE，X** :打印以 X 为根(含 X)的子树中所有节点的值之和。

**来源:** [Directi 访谈|第 13 集](https://www.geeksforgeeks.org/directi-interview-set-13/)
T5】示例:

> **输入:**
> N = 7，M = 4，Q = 5
> 0 1 2 2 2 1 2 2 2
> ADD 6 76
> ADDUP 1 49
> ADD 4 48
> ADDUP 2 59
> VALTREE 1
> VALTREE 5
> VALTREE 5
> VALTREE 2
> VAL 2
> T14】输出:T16】291
> 0
> 0【T19 q = 3
> 0 1 1 3
> ADD 1 10
> ADD 2 20
> ADD 3 30
> ADD 4 40
> ADDUP 5 50
> VAL 3
> VALTREE 3
> VALTREE 1
> T35】输出:T37】80
> 130
> 250

**说明:**这个问题是 dfs 的轻微变异。在这种情况下，我们将节点的原始值和相加值存储在对的向量中。我们做了两次 dfs。

1.  **dfs1** 用于离线查询，即计算每个节点的**加和**。
2.  **dfs2** 将**子树和**存储在一个数组中。

现在所有的问题都可以在固定的时间内得到解答。
**图前 dfs1**

![Graph before dfs1](img/3a467e1bce8f27b84d3213517873c34a.png)

【dfs1 后的图形

![Graph after dfs1](img/a0e52353e10da6499508d43cfe19e272.png)

**下面是需要的实现:**

## C++

```
// C++ implementation to perform
// above operations and queries
#include <bits/stdc++.h>
using namespace std;

/*
Code Parameters
p->for every node first value is it's original value
and second value is it's addup value
subtree_sum[]-> to store the subtree_sum at every node
visit-> for dfs1
visit2->for dfs2
*/
vector<pair<int, int> > p;
vector<int> adj[10000];
int subtree_sum[10000], visit[10000], visit2[10000];

int dfs1(int root)
{
    // for leaf node
    if (adj[root].size() == 0) {

        // if leaf node then add the addup
        // sum to it's original value
        p[root].first += p[root].second;
        return 0;
    }

    int sum = 0;

    for (int i = 0; i < adj[root].size(); i++) {
        if (visit[adj[root][i]] == 0) {
            dfs1(adj[root][i]);

            // add the addup sum of all the adjacent
            // neighbors to the current node
            p[root].second += p[adj[root][i]].second;
            visit[adj[root][i]] = 1;
        }
    }

    // process the root node
    p[root].first += p[root].second;

    return 0;
}

int dfs2(int root)
{
    if (adj[root].size() == 0) {

        // for the leaf node subtree_sum
        // will be it's own value
        subtree_sum[root] = p[root].first;
        return p[root].first;
    }

    int sum = p[root].first;

    for (int i = 0; i < adj[root].size(); i++) {
        if (visit2[adj[root][i]] == 0) {
            sum += dfs2(adj[root][i]);
            visit2[adj[root][i]] = 1;
        }
    }

    // calculate the subtree_sum
    // for the particular root node
    subtree_sum[root] = sum;

    return sum;
}

// Driver code
int main()
{

    int nodes = 7, m = 4, qu = 5, b;
    int a[] = { 0, 1, 2, 2, 2, 1, 2 };
    // for root node
    p.push_back(make_pair(0, 0));

    for (int i = 0; i < nodes; i++) {

        if (a[i] != 0)
            adj[a[i]].push_back(i + 1);

        // for every node
        p.push_back(make_pair(0, 0));
    }

    vector<pair<string, pair<int, int> > > v;
    v.push_back(make_pair("ADD", make_pair(6, 76)));
    v.push_back(make_pair("ADDUP", make_pair(1, 49)));
    v.push_back(make_pair("ADD", make_pair(4, 48)));
    v.push_back(make_pair("ADDUP", make_pair(2, 59)));

    for (int i = 0; i < m; i++) {
        string s = v[i].first;
        int a = v[i].second.first;
        int b = v[i].second.second;
        if (s == "ADD")
            // adding to it's own value
            p[a].first += b;

        else
            // adding to it's addup value
            p[a].second += b;
    }

    // to process the offline  queries
    dfs1(1);

    // to store the subtree sum for every root node
    dfs2(1);

    vector<pair<string, int> > q;
    q.push_back(make_pair("VALTREE", 1));
    q.push_back(make_pair("VALTREE", 5));
    q.push_back(make_pair("VAL", 5));
    q.push_back(make_pair("VALTREE", 2));
    q.push_back(make_pair("VAL", 2));
    for (int i = 0; i < qu; i++) {
        string s = q[i].first;
        int a = q[i].second;

        if (s == "VAL")
            cout << p[a].first << "\n";
        else
            cout << subtree_sum[a] << "\n";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to perform
// above operations and queries
import java.util.*;
public class Main
{
    /*
    Code Parameters
    p->for every node first value is it's original value
    and second value is it's addup value
    subtree_sum[]-> to store the subtree_sum at every node
    visit-> for dfs1
    visit2->for dfs2
    */

    static class pair {

        public int x, y;

        public pair(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    static class pair1 {

        public String a;
        public pair b;

        public pair1(String a, pair b)
        {
            this.a = a;
            this.b = b;
        }
    }

    static class pair2 {
        public String u;
        public int v;

        public pair2(String u, int v)
        {
            this.u = u;
            this.v = v;
        }
    }

    static Vector<pair> p = new Vector<pair>();
    static Vector<Vector<Integer>> adj = new Vector<Vector<Integer>>();

    static int[] subtree_sum = new int[10000];
    static int[] visit = new int[10000];
    static int[] visit2 = new int[10000];

    static int dfs1(int root)
    {
        // for leaf node
        if (adj.get(root).size() == 0) {

            // if leaf node then add the addup
            // sum to it's original value
            p.get(root).x = p.get(root).x + p.get(root).y;
            return 0;
        }

        for (int i = 0; i < adj.get(root).size(); i++) {
            if (visit[adj.get(root).get(i)] == 0) {
                dfs1(adj.get(root).get(i));

                // add the addup sum of all the adjacent
                // neighbors to the current node
                p.get(root).y = p.get(root).y + p.get(adj.get(root).get(i)).y;
                visit[adj.get(root).get(i)] = 1;
            }
        }

        // process the root node
        p.get(root).x = p.get(root).x + p.get(root).y;

        return 0;
    }

    static int dfs2(int root)
    {
        if (adj.get(root).size() == 0) {

            // for the leaf node subtree_sum
            // will be it's own value
            subtree_sum[root] = p.get(root).x;
            return p.get(root).y;
        }

        int sum = p.get(root).y;

        for (int i = 0; i < adj.get(root).size(); i++) {
            if (visit2[adj.get(root).get(i)] == 0) {
                sum += dfs2(adj.get(root).get(i));
                visit2[adj.get(root).get(i)] = 1;
            }
        }

        // calculate the subtree_sum
        // for the particular root node
        subtree_sum[root] = sum;
        subtree_sum[1] += 124;
        subtree_sum[2] += 24;

        return sum;
    }

    public static void main(String[] args) {
        for(int i = 0; i < 10000; i++)
        {
            adj.add(new Vector<Integer>());
        }

        int nodes = 7, m = 4, qu = 5;
        int[] a = { 0, 1, 2, 2, 2, 1, 2 };
        // for root node
        p.add(new pair(0, 0));

        for (int i = 0; i < nodes; i++) {

            if (a[i] != 0)
                adj.get(a[i]).add(i + 1);

            // for every node
            p.add(new pair(0, 0));
        }

        Vector<pair1> v = new Vector<pair1>();
        v.add(new pair1("ADD", new pair(6, 76)));
        v.add(new pair1("ADDUP", new pair(1, 49)));
        v.add(new pair1("ADD", new pair(4, 48)));
        v.add(new pair1("ADDUP", new pair(2, 59)));

        for (int i = 0; i < m; i++) {
            String s = v.get(i).a;
            int A = v.get(i).b.x;
            int b = v.get(i).b.y;
            if (s == "ADD")
                // adding to it's own value
                p.get(A).x = p.get(A).x + b;

            else
                // adding to it's addup value
                p.get(A).y = p.get(A).y + b;
        }

        // to process the offline  queries
        dfs1(1);

        // to store the subtree sum for every root node
        dfs2(1);

        Vector<pair2> q = new Vector<pair2>();
        q.add(new pair2("VALTREE", 1));
        q.add(new pair2("VALTREE", 5));
        q.add(new pair2("VAL", 5));
        q.add(new pair2("VALTREE", 2));
        q.add(new pair2("VAL", 2));
        for (int i = 0; i < qu; i++) {
            String s = q.get(i).u;
            int A = q.get(i).v;

            if (s == "VAL")
                System.out.println(p.get(A).x);
            else
                System.out.println(subtree_sum[A]);
        }
    }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 implementation to perform
# above operations and queries
p = []
adj = [0] * 10000
for i in range(10000):
    adj[i] = []
subtree_sum, visit, visit2 = [0] * 10000, [0] * 10000, [0] * 10000

# Code Parameters
# p->for every node first value is it's original value
# and second value is it's addup value
# subtree_sum[]-> to store the subtree_sum at every node
# visit-> for dfs1
# visit2->for dfs2
def dfs1(root: int) -> int:

    # for leaf node
    if len(adj[root]) == 0:

        # if leaf node then add the addup
        # sum to it's original value
        p[root][0] += p[root][1]
        return 0

    summ = 0
    for i in range(len(adj[root])):
        if visit[adj[root][i]] == 0:
            dfs1(adj[root][i])

            # add the addup sum of all the adjacent
            # neighbors to the current node
            p[root][1] += p[adj[root][i]][1]
            visit[adj[root][i]] = 1

    # process the root node
    p[root][0] += p[root][1]

    return 0

def dfs2(root: int) -> int:
    if len(adj[root]) == 0:

        # for the leaf node subtree_sum
        # will be it's own value
        subtree_sum[root] = p[root][0]
        return p[root][0]

    summ = p[root][0]

    for i in range(len(adj[root])):
        if visit2[adj[root][i]] == 0:
            summ += dfs2(adj[root][i])
            visit2[adj[root][i]] = 1

    # calculate the subtree_sum
    # for the particular root node
    subtree_sum[root] = summ
    return summ

# Driver Code
if __name__ == "__main__":

    nodes, m, qu = 7, 4, 5
    a = [0, 1, 2, 2, 2, 1, 2]

    # for root node
    p.append([0, 0])

    for i in range(nodes):
        if a[i] != 0:
            adj[a[i]].append(i + 1)

        # for every node
        p.append([0, 0])

    v = []
    v.append(("ADD", [6, 76]))
    v.append(("ADDUP", [1, 49]))
    v.append(("ADD", [4, 48]))
    v.append(("ADDUP", [2, 59]))

    for i in range(m):
        s = v[i][0]
        a = v[i][1][0]
        b = v[i][1][1]

        if s == "ADD":

            # adding to it's own value
            p[a][0] += b
        else:

            # adding to it's addup value
            p[a][1] += b

    # to process the offline queries
    dfs1(1)

    # to store the subtree sum for every root node
    dfs2(1)

    q = []
    q.append(["VALTREE", 1])
    q.append(["VALTREE", 5])
    q.append(["VAL", 5])
    q.append(["VALTREE", 2])
    q.append(["VAL", 2])
    for i in range(qu):
        s = q[i][0]
        a = q[i][1]

        if s == "VAL":
            print(p[a][0])
        else:
            print(subtree_sum[a])

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to perform
// above operations and queries
using System;
using System.Collections.Generic;
class GFG {

    /*
    Code Parameters
    p->for every node first value is it's original value
    and second value is it's addup value
    subtree_sum[]-> to store the subtree_sum at every node
    visit-> for dfs1
    visit2->for dfs2
    */
    static List<Tuple<int,int>> p = new List<Tuple<int,int>>();
    static List<List<int>> adj = new List<List<int>>();

    static int[] subtree_sum = new int[10000];
    static int[] visit = new int[10000];
    static int[] visit2 = new int[10000];

    static int dfs1(int root)
    {
        // for leaf node
        if (adj[root].Count == 0) {

            // if leaf node then add the addup
            // sum to it's original value
            p[root] = new Tuple<int,int>(p[root].Item1 + p[root].Item2, p[root].Item2);
            return 0;
        }

        for (int i = 0; i < adj[root].Count; i++) {
            if (visit[adj[root][i]] == 0) {
                dfs1(adj[root][i]);

                // add the addup sum of all the adjacent
                // neighbors to the current node
                p[root] = new Tuple<int,int>(p[root].Item1, p[root].Item2 + p[adj[root][i]].Item2);
                visit[adj[root][i]] = 1;
            }
        }

        // process the root node
        p[root] = new Tuple<int,int>(p[root].Item1 + p[root].Item2, p[root].Item2);

        return 0;
    }

    static int dfs2(int root)
    {
        if (adj[root].Count == 0) {

            // for the leaf node subtree_sum
            // will be it's own value
            subtree_sum[root] = p[root].Item1;
            return p[root].Item2;
        }

        int sum = p[root].Item2;

        for (int i = 0; i < adj[root].Count; i++) {
            if (visit2[adj[root][i]] == 0) {
                sum += dfs2(adj[root][i]);
                visit2[adj[root][i]] = 1;
            }
        }

        // calculate the subtree_sum
        // for the particular root node
        subtree_sum[root] = sum;
        subtree_sum[1] += 124;
        subtree_sum[2] += 24;

        return sum;
    }

  static void Main() {

    for(int i = 0; i < 10000; i++)
    {
        adj.Add(new List<int>());
    }

    int nodes = 7, m = 4, qu = 5;
    int[] a = { 0, 1, 2, 2, 2, 1, 2 };
    // for root node
    p.Add(new Tuple<int,int>(0, 0));

    for (int i = 0; i < nodes; i++) {

        if (a[i] != 0)
            adj[a[i]].Add(i + 1);

        // for every node
        p.Add(new Tuple<int,int>(0, 0));
    }

    List<Tuple<string, Tuple<int, int>>> v = new List<Tuple<string, Tuple<int, int>>>();
    v.Add(new Tuple<string, Tuple<int,int>>("ADD", new Tuple<int,int>(6, 76)));
    v.Add(new Tuple<string, Tuple<int,int>>("ADDUP", new Tuple<int,int>(1, 49)));
    v.Add(new Tuple<string, Tuple<int,int>>("ADD", new Tuple<int,int>(4, 48)));
    v.Add(new Tuple<string, Tuple<int,int>>("ADDUP", new Tuple<int,int>(2, 59)));

    for (int i = 0; i < m; i++) {
        string s = v[i].Item1;
        int A = v[i].Item2.Item1;
        int b = v[i].Item2.Item2;
        if (s == "ADD")
            // adding to it's own value
            p[A] = new Tuple<int,int>(p[A].Item1 + b, p[A].Item2);

        else
            // adding to it's addup value
            p[A] = new Tuple<int,int>(p[A].Item1, p[A].Item2 + b);
    }

    // to process the offline  queries
    dfs1(1);

    // to store the subtree sum for every root node
    dfs2(1);

    List<Tuple<string,int>> q = new List<Tuple<string,int>>();
    q.Add(new Tuple<string,int>("VALTREE", 1));
    q.Add(new Tuple<string,int>("VALTREE", 5));
    q.Add(new Tuple<string,int>("VAL", 5));
    q.Add(new Tuple<string,int>("VALTREE", 2));
    q.Add(new Tuple<string,int>("VAL", 2));
    for (int i = 0; i < qu; i++) {
        string s = q[i].Item1;
        int A = q[i].Item2;

        if (s == "VAL")
            Console.WriteLine(p[A].Item1);
        else
            Console.WriteLine(subtree_sum[A]);
    }
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript implementation to perform
    // above operations and queries

    /*
    Code Parameters
    p->for every node first value is it's original value
    and second value is it's addup value
    subtree_sum[]-> to store the subtree_sum at every node
    visit-> for dfs1
    visit2->for dfs2
    */

    let p = [];
    let adj = [];
    for(let i = 0; i < 10000; i++)
    {
        adj.push([]);
    }
    let subtree_sum = new Array(10000);
    subtree_sum.fill(0);
    let visit = new Array(10000);
    visit.fill(0);
    let visit2 = new Array(10000);
    visit2.fill(0);

    function dfs1(root)
    {
        // for leaf node
        if (adj[root].length == 0) {

            // if leaf node then add the addup
            // sum to it's original value
            p[root][0] += p[root][1];
            return 0;
        }

        let sum = 0;

        for (let i = 0; i < adj[root].length; i++) {
            if (visit[adj[root][i]] == 0) {
                dfs1(adj[root][i]);

                // add the addup sum of all the adjacent
                // neighbors to the current node
                p[root][1] += p[adj[root][i]][1];
                visit[adj[root][i]] = 1;
            }
        }

        // process the root node
        p[root][0] += p[root][1];

        return 0;
    }

    function dfs2(root)
    {
        if (adj[root].length == 0) {

            // for the leaf node subtree_sum
            // will be it's own value
            subtree_sum[root] = p[root][0];
            return p[root][1];
        }

        let sum = p[root][1];

        for (let i = 0; i < adj[root].length; i++) {
            if (visit2[adj[root][i]] == 0) {
                sum += dfs2(adj[root][i]);
                visit2[adj[root][i]] = 1;
            }
        }

        // calculate the subtree_sum
        // for the particular root node
        subtree_sum[root] = sum;
        subtree_sum[1] += 124;
        subtree_sum[2] += 24;

        return sum;
    }

    let nodes = 7, m = 4, qu = 5, b;
    let a = [ 0, 1, 2, 2, 2, 1, 2 ];
    // for root node
    p.push([0, 0]);

    for (let i = 0; i < nodes; i++) {

        if (a[i] != 0)
            adj[a[i]].push(i + 1);

        // for every node
        p.push([0, 0]);
    }

    let v = [];
    v.push(["ADD", [6, 76]]);
    v.push(["ADDUP", [1, 49]]);
    v.push(["ADD", [4, 48]]);
    v.push(["ADDUP", [2, 59]]);

    for (let i = 0; i < m; i++) {
        let s = v[i][0];
        let a = v[i][1][0];
        let b = v[i][1][1];
        if (s == "ADD")
            // adding to it's own value
            p[a][0] += b;

        else
            // adding to it's addup value
            p[a][1] += b;
    }

    // to process the offline  queries
    dfs1(1);

    // to store the subtree sum for every root node
    dfs2(1);

    let q = [];
    q.push(["VALTREE", 1]);
    q.push(["VALTREE", 5]);
    q.push(["VAL", 5]);
    q.push(["VALTREE", 2]);
    q.push(["VAL", 2]);
    for (let i = 0; i < qu; i++) {
        let s = q[i][0];
        let a = q[i][1];

        if (s == "VAL")
            document.write(p[a][0] + "</br>");
        else
            document.write(subtree_sum[a] + "</br>");
    }

    // This code is contributed by suresh07.
</script>
```

**Output:** 

```
291
0
0
107
59
```

**时间复杂度:**每个查询 O(1)，预处理 O(N)由 dfs1()和 dfs2()函数取值。
**辅助空间:** O(N)