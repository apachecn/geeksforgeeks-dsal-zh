# 通过在每个步骤中替换一位数字，将 N 位素数转换为另一个数的最小步骤

> 原文： [https://www.geeksforgeeks.org/min-steps-to-convert-n-digit-prime-number-into-another-by-replacing-a-digit-in-each-step/](https://www.geeksforgeeks.org/min-steps-to-convert-n-digit-prime-number-into-another-by-replacing-a-digit-in-each-step/)

给定两个`N`位素数`A`和`B`，任务是找到将 A 转换为 A 的最小步骤数 B.转换的条件是当前质数只能修改 1 位，这样形成的新数字也是质数。 如果无法进行这种转换，请打印-1。

**注意**：N 的范围是[1，5]。
**范例**：

> **输入**：N = 4，A = 1033，B = 8179
> **输出**：6
> **说明**：转换步骤为 1033-[ > 1733-> 3733-> 3739-> 3779-> 8779->8179。从 1033- > 1733 更改数字时，它们仅相差一个数字，并且发生相同的情况 用于后续步骤。
> 
> **输入**：N = 4，A = 1373，B = 8179
> **输出**：7
> 
> **输入**：N = 2，A = 11，B = 37
> **输出**：2
> **说明**：转换步骤为 11-> 17-> 37

**方法**：使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)算法

1.  查找所有 N 位素数，并用这些数字作图。
2.  将每个质数都视为图的一个节点，如果每个节点之间相差一个数字，则创建从一个节点到另一个节点的边。
3.  应用 BFS 遍历并找出 A 和 B 之间的边数。
4.  如果没有路径，则打印-1。
5.  否则打印编号。 边，这是必需的解决方案。

下面是上述方法的实现。

```

// C++ program for the above problem 

#include <bits/stdc++.h> 
using namespace std; 

#define ll long long 
#define mod 1000000007 
#define pb push_back 
#define mod 1000000007 
#define vi vector<int> 

// adjacency list for numbers 
// till 100001 
vi lis[100001]; 
vi primes; 

// visited array 
int vis[100001]; 

// to store distance of every 
// vertex from A 
int dis[100001]; 

// function to check if number 
// is a prime 
bool isPrime(int n) 
{ 
    for (int i = 2; 
         i * i <= n; i++) { 
        if (n % i == 0) 
            return false; 
    } 
    return true; 
} 

// function to check if numbers 
// differ by only a single-digit 
bool valid(int a, int b) 
{ 
    int c = 0; 
    while (a) { 

        // check the last digit of 
        // both numbers and increase 
        // count if different 
        if ((a % 10) != (b % 10)) { 
            c++; 
        } 
        a = a / 10; 
        b = b / 10; 
    } 
    if (c == 1) { 
        return true; 
    } 
    else { 
        return false; 
    } 
} 

void makePrimes(int N) 
{ 
    int i, j; 
    int L = pow(10, N - 1); 
    int R = pow(10, N) - 1; 
    // generate all N digit primes 
    for (int i = L; i <= R; i++) { 
        if (isPrime(i)) { 
            primes.pb(i); 
        } 
    } 
    for (i = 0; 
         i < primes.size(); i++) { 

        // for every prime number i 
        // check if an edge 
        // can be made. 
        for (j = i + 1; 
             j < primes.size(); j++) { 
            int a = primes[i]; 
            int b = primes[j]; 

            // for every prime number 
            // i check if an edge can 
            // be made from i to j. 
            if (valid(a, b)) { 

                // if edge is possible then 
                // insert in the adjacency 
                // list 
                lis[a].pb(b); 
                lis[b].pb(a); 
            } 
        } 
    } 
} 

// function to count distance 
void bfs(int src) 
{ 
    queue<int> q; 
    q.push(src); 
    vis[src] = 1; 
    dis[src] = 0; 
    while (!q.empty()) { 
        int curr = q.front(); 
        q.pop(); 
        for (int x : lis[curr]) { 

            // if unvisited push onto queue 
            // and mark visited as 1 and 
            // add the distance of curr+1\. 
            if (vis[x] == 0) { 
                vis[x] = 1; 
                q.push(x); 
                dis[x] = dis[curr] + 1; 
            } 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    int N = 4; 
    makePrimes(N); 
    int A = 1033, B = 8179; 

    // Call bfs traversal 
    // with root as node A 
    bfs(A); 

    if (dis[B] == -1) 
        // incdicates not possible 
        cout << "-1" << endl; 
    else
        cout << dis[B] << endl; 

    return 0; 
} 

```

**Output:**

```
6

```

***时间复杂度**：O（10 <sup>2N</sup> ）
**辅助空间复杂度**：O（10 <sup>5</sup> ）*

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。