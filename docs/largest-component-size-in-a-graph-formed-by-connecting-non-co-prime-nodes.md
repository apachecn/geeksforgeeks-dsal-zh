# 通过连接非同素节点形成的图中最大的组件尺寸

> 原文:[https://www . geesforgeks . org/最大组件-图形中的大小-通过连接非同素节点形成/](https://www.geeksforgeeks.org/largest-component-size-in-a-graph-formed-by-connecting-non-co-prime-nodes/)

给定一个图，其中 N 个节点及其值在数组 A 中定义，任务是通过连接非同素节点来找到图中最大的组件大小。一条边在两个节点 U 和 V 之间，如果它们不是同素的，这意味着 A[U]和 A[V]的最大公约数应该大于 1。

**示例:**

```
Input : A = [4, 6, 15, 35]
Output : 4
Graph will be :
         4
         |
         6
         |
         15
         |
         35

Input : A = [2, 3, 6, 7, 4, 12, 21, 39]
Output : 8
```

**天真方法:**
我们可以迭代所有的节点对，检查它们是否同素。如果它们不是同素的，我们将连接它们。一旦创建了图形，我们将应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来找到最大的组件大小。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int dfs(int u, vector<int>* adj, int vis[])
{
    // mark this node as visited
    vis[u] = 1;
    int componentSize = 1;

    // apply dfs and add nodes belonging to this component
    for (auto it : adj[u]) {
        if (!vis[it]) {
            componentSize += dfs(it, adj, vis);
        }
    }
    return componentSize;
}

int maximumComponentSize(int a[], int n)
{
    // create graph and store in adjacency list form
    vector<int> adj[n];

    // iterate over all pair of nodes
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            // if not co-prime
            if (__gcd(a[i], a[j]) > 1)
                // build undirected graph
                adj[i].push_back(j);
            adj[j].push_back(i);
        }
    }
    int answer = 0;

    // visited array for dfs
    int vis[n];
    for(int k=0;k<n;k++){
      vis[k]=0;
    }
    for (int i = 0; i < n; i++) {
        if (!vis[i]) {
            answer = max(answer, dfs(i, adj, vis));
        }
    }
    return answer;
}

// Driver Code
int main()
{
    int n = 8;
    int A[] = { 2, 3, 6, 7, 4, 12, 21, 39 };
    cout << maximumComponentSize(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

static int dfs(int u, Vector<Integer> []adj,
               int vis[])
{

    // Mark this node as visited
    vis[u] = 1;
    int componentSize = 1;

    // Apply dfs and add nodes belonging
    // to this component
    for(int it : adj[u])
    {
        if (vis[it] == 0)
        {
            componentSize += dfs(it, adj, vis);
        }
    }
    return componentSize;
}

static int maximumComponentSize(int a[], int n)
{

    // Create graph and store in adjacency
    // list form
    @SuppressWarnings("unchecked")
    Vector<Integer> []adj = new Vector[n];
    for(int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    // Iterate over all pair of nodes
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If not co-prime
            if (__gcd(a[i], a[j]) > 1)

                // Build undirected graph
                adj[i].add(j);

            adj[j].add(i);
        }
    }
    int answer = 0;

    // Visited array for dfs
    int []vis = new int[n];
    for(int k = 0; k < n; k++)
    {
        vis[k] = 0;
    }

    for(int i = 0; i < n; i++)
    {
        if (vis[i] == 0)
        {
            answer = Math.max(answer,
                              dfs(i, adj, vis));
        }
    }
    return answer;
}

static int __gcd(int a, int b)
{ 
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int n = 8;
    int A[] = { 2, 3, 6, 7, 4, 12, 21, 39 };

    System.out.print(maximumComponentSize(A, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
from math import gcd
def dfs(u, adj, vis):

    # mark this node as visited
    vis[u] = 1
    componentSize = 1

    # apply dfs and add nodes belonging to this component
    for x in adj[u]:
        if (vis[x] == 0):
            componentSize += dfs(x, adj, vis)
    return componentSize

def maximumComponentSize(a,n):

    # create graph and store in adjacency list form
    adj = [[] for i in range(n)]

    # iterate over all pair of nodes
    for i in range(n):
        for j in range(i + 1, n):
            # if not co-prime
            if (gcd(a[i], a[j]) > 1):
                # build undirected graph
                adj[i].append(j)
            adj[j].append(i)
    answer = 0

    # visited array for dfs
    vis = [0 for i in range(n)]
    for i in range(n):
        if (vis[i]==False):
            answer = max(answer, dfs(i, adj, vis))
    return answer

# Driver Code
if __name__ == '__main__':
    n = 8
    A = [2, 3, 6, 7, 4, 12, 21, 39]
    print(maximumComponentSize(A, n))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static int dfs(int u,
               List<int> []adj,
               int []vis)
{   
  // Mark this node as visited
  vis[u] = 1;
  int componentSize = 1;

  // Apply dfs and add nodes belonging
  // to this component
  foreach(int it in adj[u])
  {
    if (vis[it] == 0)
    {
      componentSize += dfs(it,
                           adj, vis);
    }
  }
  return componentSize;
}

  static int maximumComponentSize(int []a,
                                  int n)
  {   
    // Create graph and store in adjacency
    // list form

    List<int> []adj = new List<int>[n];
    for(int i = 0; i < adj.Length; i++)
      adj[i] = new List<int>();

    // Iterate over all pair of nodes
    for(int i = 0; i < n; i++)
    {
      for(int j = i + 1; j < n; j++)
      {           
        // If not co-prime
        if (__gcd(a[i], a[j]) > 1)

          // Build undirected graph
          adj[i].Add(j);

        adj[j].Add(i);
      }
    }
    int answer = 0;

    // Visited array for dfs
    int []vis = new int[n];
    for(int k = 0; k < n; k++)
    {
      vis[k] = 0;
    }

    for(int i = 0; i < n; i++)
    {
      if (vis[i] == 0)
      {
        answer = Math.Max(answer,
                          dfs(i,
                              adj, vis));
      }
    }
    return answer;
}

static int __gcd(int a, int b)
{ 
  return b == 0 ? a :
         __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
  int n = 8;
  int []A = {2, 3, 6, 7,
             4, 12, 21, 39};
  Console.Write(maximumComponentSize(A, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function dfs(u, adj, vis)
{  
      // Mark this node as visited
    vis[u] = 1;
    let componentSize = 1;

      // Apply dfs and add nodes belonging
      // to this component
    for(let it in adj[u])
    {
          if (vis[it] == 0)
        {
              componentSize += dfs(it,
                           adj, vis);
        }
      }
      return componentSize;
}

function maximumComponentSize(a, n)
{  
    // Create graph and store in adjacency
    // list form

    let adj = new Array(n);
    for (var i = 0; i < adj.length; i++) {
        adj[i] = new Array(2);
    }
    for (var i = 0; i < adj.length; i++) {
        for (var j = 0; j < adj.length; j++) {
            adj[i][j] = 0;
        }
    }

    // Iterate over all pair of nodes
    for(let i = 0; i < n; i++)
    {
        for(let j = i + 1; j < n; j++)
          {          
            // If not co-prime
            if (__gcd(a[i], a[j]) > 1)

              // Build undirected graph
              adj[i].push(j);

            adj[j].push(i);
          }
    }
    let answer = 0;

    // Visited array for dfs
    let vis = Array.from({length: n}, (_, i) => 0);
    for(let k = 0; k < n; k++)
    {
          vis[k] = 0;
    }

    for(let i = 0; i < n; i++)
    {
          if (vis[i] == 0)
          {
            answer = Math.max(answer,
                          dfs(i,
                              adj, vis));
          }
       }
    return answer;
}

function __gcd(a, b)
{
      return b == 0 ? a :
         __gcd(b, a % b);   
}

// Driver Code

    let n = 8;
    let A = [2, 3, 6, 7, 4, 12, 21, 39];

    document.write(maximumComponentSize(A, n));

</script>
```

**输出:**

```
8
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N)

**高效方法**

*   对于任何两个非同素数，它们必须至少有一个公共因子。因此，与其遍历所有对，不如对每个节点值进行质因数分解。这个想法是把有共同因素的数字组合成一组。
*   利用厄拉多塞的[筛可以有效地进行素分解。对于聚集在一起的节点，我们将使用](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[不相交集合数据结构(通过等级和路径压缩的联合)](https://www.geeksforgeeks.org/disjoint-set-data-structures/)。
*   将存储以下信息:

> par[i] ->代表节点 I 的父节点
> size[i] - >代表组件节点 I 所属的大小
> id[p] - >代表哪个节点素数 p 最早被视为 A[i]的因子

*   对于每个节点值，我们将分解并存储 s 集合中的质因数，迭代 s 的每个元素，如果第一次看到质数是某个数的因数(id[p]为零)，那么用当前索引标记这个质数 id。如果这个素数已经被标记，那么只需将这个节点与 id[p]的节点合并。
    这样，所有节点最后都会属于某个组件，大小[i]就是组件节点 I 所属的大小。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>

using namespace std;

// smallest prime factor
int spf[100005];

// Sieve of Eratosthenes
void sieve()
{
    for (int i = 2; i < 100005; i++) {
        // is spf[i] = 0, then it's prime
        if (spf[i] == 0) {
            spf[i] = i;

            for (int j = 2 * i; j < 100005; j += i) {

                // smallest prime factor of all multiples is i
                if (spf[j] == 0)
                    spf[j] = i;
            }
        }
    }
}

// Prime factorise n,
// and store prime factors in set s
void factorize(int n, set<int>& s)
{

    while (n > 1) {
        int z = spf[n];
        s.insert(z);
        while (n % z == 0)
            n /= z;
    }
}

// for implementing DSU
int id[100005];
int par[100005];
int sizeContainer[100005];

// root of component of node i
int root(int i)
{
    if (par[i] == i)
        return i;
    // finding root as well as applying
    // path compression
    else
        return par[i] = root(par[i]);
}

// merging two components
void merge(int a, int b)
{

    // find roots of both components
    int p = root(a);
    int q = root(b);

    // if already belonging to the same component
    if (p == q)
        return;

    // Union by rank, the rank in this case is
    // sizeContainer of the component.
    // Smaller sizeContainer will be merged into
    // larger, so the larger's root will be
    // final root
    if (sizeContainer[p] > sizeContainer[q])
        swap(p, q);

    par[p] = q;
    sizeContainer[q] += sizeContainer[p];
}

// Function to find the maximum sized container
int maximumComponentsizeContainer(int a[], int n)
{

    // intitalise the parents,
    // and component sizeContainer
    for (int i = 0; i < 100005; i++) {
        // intitally all component sizeContainers are 1
        // ans each node it parent of itself
        par[i] = i;
        sizeContainer[i] = 1;
    }

    sieve();

    for (int i = 0; i < n; i++) {
        // store prime factors of a[i] in s
        set<int> s;
        factorize(a[i], s);

        for (auto it : s) {
            // if this prime is seen as a factor
            // for the first time
            if (id[it] == 0)
                id[it] = i + 1;
            // if not then merge with that component
            // in which this prime was previously seen
            else
                merge(i + 1, id[it]);
        }
    }

    int answer = 0;

    // maximum of sizeContainer of all components
    for (int i = 0; i < n; i++)
        answer = max(answer, sizeContainer[i]);

    return answer;
}

// Driver Code
int main()
{
    int n = 8;
    int A[] = { 2, 3, 6, 7, 4, 12, 21, 39 };

    cout << maximumComponentsizeContainer(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// smallest prime factor
static int []spf = new int[100005];

// Sieve of Eratosthenes
static void sieve()
{
    for (int i = 2; i < 100005; i++)
    {
        // is spf[i] = 0, then it's prime
        if (spf[i] == 0)
        {
            spf[i] = i;
            for (int j = 2 * i; j < 100005; j += i)
            {
                // smallest prime factor of all
                // multiples is i
                if (spf[j] == 0)
                    spf[j] = i;
            }
        }
    }
}

// Prime factorise n,
// and store prime factors in set s
static void factorize(int n, HashSet<Integer> s)
{
    while (n > 1)
    {
        int z = spf[n];
        s.add(z);
        while (n % z == 0)
            n /= z;
    }
}

// for implementing DSU
static int []id = new int[100005];
static int []par = new int[100005];
static int []sizeContainer = new int[100005];

// root of component of node i
static int root(int i)
{
    if (par[i] == i)
        return i;
    // finding root as well as applying
    // path compression
    else
        return par[i] = root(par[i]);
}

// merging two components
static void merge(int a, int b)
{
    // find roots of both components
    int p = root(a);
    int q = root(b);

    // if already belonging to the same component
    if (p == q)
        return;

    // Union by rank, the rank in this case is
    // sizeContainer of the component.
    // Smaller sizeContainer will be merged into
    // larger, so the larger's root will be
    // final root
    if (sizeContainer[p] > sizeContainer[q])
    {
        p = p + q;
        q = p - q;
        p = p - q;
    }
    par[p] = q;
    sizeContainer[q] += sizeContainer[p];
}

// Function to find the maximum sized container
static int maximumComponentsizeContainer(int a[],
                                         int n)
{
    // intitalise the parents,
    // and component sizeContainer
    for (int i = 0; i < 100005; i++)
    {
        // intitally all component sizeContainers are 1
        // ans each node it parent of itself
        par[i] = i;
        sizeContainer[i] = 1;
    }
    sieve();

    for (int i = 0; i < n; i++)
    {
        // store prime factors of a[i] in s
        HashSet<Integer> s = new HashSet<Integer>();
        factorize(a[i], s);

        for (int it : s)
        {
            // if this prime is seen as a factor
            // for the first time
            if (id[it] == 0)
                id[it] = i + 1;
            // if not then merge with that component
            // in which this prime was previously seen
            else
                merge(i + 1, id[it]);
        }
    }
    int answer = 0;

    // maximum of sizeContainer of all components
    for (int i = 0; i < n; i++)
        answer = Math.max(answer, sizeContainer[i]);

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int n = 8;
    int A[] = {2, 3, 6, 7,
               4, 12, 21, 39};
    System.out.print(
           maximumComponentsizeContainer(A, n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# smallest prime factor
spf = [0 for i in range(100005)]

# Sieve of Eratosthenes
def sieve():

    for i in range(2, 100005):

        # is spf[i] = 0, then it's prime
        if (spf[i] == 0):

            spf[i] = i;
            for j in range(2 * i, 100005, i):

                # smallest prime factor of all
                # multiples is i
                if (spf[j] == 0):
                    spf[j] = i;

# Prime factorise n,
# and store prime factors in set s
def factorize(n, s):
    while (n > 1):  
        z = spf[n];
        s.add(z);
        while (n % z == 0):
            n //= z;

# for implementing DSU
id = [0 for i in range(100005)]
par = [0 for i in range(100005)]
sizeContainer = [0 for i in range(100005)]

# root of component of node i
def root(i):

    if (par[i] == i):
        return i;

    # finding root as well as applying
    # path compression
    else:
        return root(par[i]);
        return par[i]

# merging two components
def merge(a, b):

    # find roots of both components
    p = root(a);
    q = root(b);

    # if already belonging to the same component
    if (p == q):
        return;

    # Union by rank, the rank in this case is
    # sizeContainer of the component.
    # Smaller sizeContainer will be merged into
    # larger, so the larger's root will be
    # final root
    if (sizeContainer[p] > sizeContainer[q]):   
        p = p + q;
        q = p - q;
        p = p - q;  
    par[p] = q;
    sizeContainer[q] += sizeContainer[p];

# Function to find the maximum sized container
def maximumComponentsizeContainer(a, n):

    # intitalise the parents,
    # and component sizeContainer
    for i in range(100005):

        # intitally all component sizeContainers are 1
        # ans each node it parent of itself
        par[i] = i;
        sizeContainer[i] = 1;
    sieve();

    for i in range(n):

        # store prime factors of a[i] in s
        s = set()       
        factorize(a[i], s); 
        for it in s:

            # if this prime is seen as a factor
            # for the first time
            if (id[it] == 0):
                id[it] = i + 1;

            # if not then merge with that component
            # in which this prime was previously seen
            else:
                merge(i + 1, id[it]);       
    answer = 0;

    # maximum of sizeContainer of all components
    for i in range(n): 
        answer = max(answer, sizeContainer[i]);
    return answer;

# Driver Code
if __name__=='__main__':

    n = 8;
    A = [2, 3, 6, 7, 4, 12, 21, 39]
    print(maximumComponentsizeContainer(A, n));

# This code is contributed by Pratham76
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Smallest prime factor
static int []spf = new int[100005];

// Sieve of Eratosthenes
static void sieve()
{
    for(int i = 2; i < 100005; i++)
    {

        // Is spf[i] = 0, then it's prime
        if (spf[i] == 0)
        {
            spf[i] = i;
            for(int j = 2 * i; j < 100005; j += i)
            {

                // Smallest prime factor of all
                // multiples is i
                if (spf[j] == 0)
                    spf[j] = i;
            }
        }
    }
}

// Prime factorise n, and store
// prime factors in set s
static void factorize(int n, HashSet<int> s)
{
    while (n > 1)
    {
        int z = spf[n];
        s.Add(z);

        while (n % z == 0)
            n /= z;
    }
}

// For implementing DSU
static int []id = new int[100005];
static int []par = new int[100005];
static int []sizeContainer = new int[100005];

// Root of component of node i
static int root(int i)
{
    if (par[i] == i)
        return i;

    // Finding root as well as applying
    // path compression
    else
        return par[i] = root(par[i]);
}

// Merging two components
static void merge(int a, int b)
{

    // Find roots of both components
    int p = root(a);
    int q = root(b);

    // If already belonging to
    // the same component
    if (p == q)
        return;

    // Union by rank, the rank in this case is
    // sizeContainer of the component.
    // Smaller sizeContainer will be merged into
    // larger, so the larger's root will be
    // readonly root
    if (sizeContainer[p] > sizeContainer[q])
    {
        p = p + q;
        q = p - q;
        p = p - q;
    }
    par[p] = q;
    sizeContainer[q] += sizeContainer[p];
}

// Function to find the maximum sized container
static int maximumComponentsizeContainer(int []a,
                                         int n)
{

    // Initialise the parents,
    // and component sizeContainer
    for(int i = 0; i < 100005; i++)
    {

        // Intitally all component sizeContainers
        // are 1 ans each node it parent of itself
        par[i] = i;
        sizeContainer[i] = 1;
    }
    sieve();

    for(int i = 0; i < n; i++)
    {

        // Store prime factors of a[i] in s
        HashSet<int> s = new HashSet<int>();
        factorize(a[i], s);

        foreach(int it in s)
        {

            // If this prime is seen as a factor
            // for the first time
            if (id[it] == 0)
                id[it] = i + 1;

            // If not then merge with that component
            // in which this prime was previously seen
            else
                merge(i + 1, id[it]);
        }
    }
    int answer = 0;

    // Maximum of sizeContainer of all components
    for(int i = 0; i < n; i++)
        answer = Math.Max(answer, sizeContainer[i]);

    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 8;
    int []A = { 2, 3, 6, 7,
                4, 12, 21, 39 };

    Console.Write(
        maximumComponentsizeContainer(A, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// smallest prime factor
var spf = Array(100005).fill(0);

// Sieve of Eratosthenes
function sieve()
{
    for (var i = 2; i < 100005; i++) {
        // is spf[i] = 0, then it's prime
        if (spf[i] == 0) {
            spf[i] = i;

            for (var j = 2 * i; j < 100005; j += i) {

                // smallest prime factor of all multiples is i
                if (spf[j] == 0)
                    spf[j] = i;
            }
        }
    }
}

// Prime factorise n,
// and store prime factors in set s
function factorize(n, s)
{

    while (n > 1) {
        var z = spf[n];
        s.add(z);
        while (n % z == 0)
            n = parseInt(n/z);
    }
    return s;
}

// for implementing DSU
var id = Array(100005).fill(0);
var par =Array(100005).fill(0);
var sizeContainer = Array(100005).fill(0);

// root of component of node i
function root(i)
{
    if (par[i] == i)
        return i;
    // finding root as well as applying
    // path compression
    else
        return par[i] = root(par[i]);
}

// merging two components
function merge(a, b)
{

    // find roots of both components
    var p = root(a);
    var q = root(b);

    // if already belonging to the same component
    if (p == q)
        return;

    // Union by rank, the rank in this case is
    // sizeContainer of the component.
    // Smaller sizeContainer will be merged into
    // larger, so the larger's root will be
    // final root
    if (sizeContainer[p] > sizeContainer[q])
    {
        [p, q] = [q, p]
    }

    par[p] = q;
    sizeContainer[q] += sizeContainer[p];
}

// Function to find the maximum sized container
function maximumComponentsizeContainer(a, n)
{

    // intitalise the parents,
    // and component sizeContainer
    for (var i = 0; i < 100005; i++) {
        // intitally all component sizeContainers are 1
        // ans each node it parent of itself
        par[i] = i;
        sizeContainer[i] = 1;
    }

    sieve();

    for (var i = 0; i < n; i++) {
        // store prime factors of a[i] in s
        var s = new Set();
        s = factorize(a[i], s);

        s.forEach(it => {

            // if this prime is seen as a factor
            // for the first time
            if (id[it] == 0)
                id[it] = i + 1;
            // if not then merge with that component
            // in which this prime was previously seen
            else
                merge(i + 1, id[it]);
        });
    }

    var answer = 0;

    // maximum of sizeContainer of all components
    for (var i = 0; i < n; i++)
        answer = Math.max(answer, sizeContainer[i]);

    return answer;
}

// Driver Code
var n = 8;
var A = [2, 3, 6, 7, 4, 12, 21, 39];

document.write( maximumComponentsizeContainer(A, n));

</script>
```

**输出:**

```
 8
```

**时间复杂度:** O(N * log(最大(A)))

**辅助空间:** O(10 <sup>5</sup>