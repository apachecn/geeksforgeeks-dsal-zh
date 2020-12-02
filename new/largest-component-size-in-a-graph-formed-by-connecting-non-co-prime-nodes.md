# 通过连接非互素节点形成的图形中最大的组件大小

> 原文： [https://www.geeksforgeeks.org/largest-component-size-in-a-graph-formed-by-connecting-non-co-prime-nodes/](https://www.geeksforgeeks.org/largest-component-size-in-a-graph-formed-by-connecting-non-co-prime-nodes/)

给定一个具有 N 个节点的图，它们的值在数组 A 中定义，任务是通过连接非互素节点在图中找到最大的组件大小。 如果两个节点 U 和 V 不互质，则它们之间的边为边，这意味着 A [U]和 A [V]的最大公约数应大于 1。
**示例**：

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

**天真的方法**：
我们可以遍历所有节点对，并检查它们是否是互素的。 如果它们不是互质的，我们将它们连接起来。 创建图表后，我们将应用[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来找到最大组件尺寸。
以下是上述方法的实现：

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

**输出**：

```
8

```

时间复杂度：O（N <sup>2</sup> ）

**有效方法**

*   对于任何两个非互质数，它们必须至少具有一个公因子。 因此，最好遍历所有对，而不是遍历每个节点值。 想法是将具有共同因素的数字组成一个小组。
*   可以使用橡皮擦的[筛网有效地完成素数分解。 为了将节点组合在一起，我们将使用](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[不交集数据结构（按等级和路径压缩的并集）](https://www.geeksforgeeks.org/disjoint-set-data-structures/)。
*   The following information will be stored :

    > par [i]- > 表示节点 i 的父节点。
    > size [i]- > 表示组成节点 i 所属节点的大小。
    > id [p]- > 表示节点素数 p 首先被视为 A [i]的因子

*   对于每个节点值，我们将分解素因数并将其存储在集合 S 中。对 S 的每个元素进行迭代。如果首次将素数视为某个因数（id [p]为零），则将 此素数与当前索引的 ID。 如果已经标记了该素数，则只需将此节点与 id [p]合并即可。
    这样，所有节点最终都将属于某个组件，而 size [i]将是我所属的组件节点的大小。

下面是上述方法的实现：

## C++

```cpp

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

    // if already belonging to the same compenent 
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

## Java

```java

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

    // if already belonging to the same compenent 
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

## C#

```cs

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
    // the same compenent 
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

**输出**：

```
 8

```

**时间复杂度**：O（N * log（max（A）））



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。