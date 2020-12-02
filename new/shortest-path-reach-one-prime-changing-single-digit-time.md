# 通过一次更改一位数字来达到一个质数到另一个质数的最短路径

> 原文： [https://www.geeksforgeeks.org/shortest-path-reach-one-prime-changing-single-digit-time/](https://www.geeksforgeeks.org/shortest-path-reach-one-prime-changing-single-digit-time/)

给定两个四位数的质数，假设 1033 和 8179，我们需要通过一次只更改一位数字来找到从 1033 到 8179 的最短路径，以使我们在更改位数后得到的每个数字都是质数。 例如，解决方案是 1033、1733、3733、3739、3779、8779、8179

**示例**：

```
Input : 1033 8179
Output :6

Input : 1373 8017
Output : 7

Input  :  1033 1033
Output : 0

```

这个问题可以通过 *[BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)* 解决，这对于初学者来说是一个非常有趣的问题。 我们首先使用 Eratosthenes 筛网[的技术找出直到 9999 的所有 4 位素数。 然后使用这些数字通过邻接表](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)形成[图。 形成邻接表后，我们使用简单的 BFS 解决了该问题。](https://www.geeksforgeeks.org/graph-and-its-representations/) 

## C ++

```

// CPP program to reach a prime number from  
// another by changing single digits and  
// using only prime numbers. 
#include <bits/stdc++.h> 

using namespace std; 

class graph { 
    int V;  
    list<int>* l;  
public: 
    graph(int V) 
    { 
        this->V = V; 
        l = new list<int>[V]; 
    } 
    void addedge(int V1, int V2)  
    { 
        l[V1].push_back(V2); 
        l[V2].push_back(V1); 
    } 
    int bfs(int in1, int in2); 
}; 

// Finding all 4 digit prime numbers 
void SieveOfEratosthenes(vector<int>& v)  
{ 
    // Create a boolean array "prime[0..n]" and initialize 
    // all entries it as true. A value in prime[i] will 
    // finally be false if i is Not a prime, else true. 
    int n = 9999; 
    bool prime[n + 1]; 
    memset(prime, true, sizeof(prime)); 

    for (int p = 2; p * p <= n; p++) { 

        // If prime[p] is not changed, then it is a prime 
        if (prime[p] == true) { 

            // Update all multiples of p 
            for (int i = p * p; i <= n; i += p) 
                prime[i] = false; 
        } 
    } 

    // Forming a vector of prime numbers 
    for (int p = 1000; p <= n; p++) 
        if (prime[p]) 
            v.push_back(p);  
} 

// in1 and in2 are two vertices of graph which are  
// actually indexes in pset[] 
int graph::bfs(int in1, int in2)  
{ 
    int visited[V]; 
    memset(visited, 0, sizeof(visited)); 
    queue<int> que; 
    visited[in1] = 1; 
    que.push(in1); 
    list<int>::iterator i; 
    while (!que.empty()) { 
        int p = que.front(); 
        que.pop(); 
        for (i = l[p].begin(); i != l[p].end(); i++) { 
            if (!visited[*i]) { 
                visited[*i] = visited[p] + 1; 
                que.push(*i); 
            } 
            if (*i == in2) { 
                return visited[*i] - 1; 
            } 
        } 
    } 
} 

// Returns true if num1 and num2 differ  
// by single digit. 
bool compare(int num1, int num2) 
{ 
    // To compare the digits 
    string s1 = to_string(num1); 
    string s2 = to_string(num2); 
    int c = 0; 
    if (s1[0] != s2[0]) 
        c++; 
    if (s1[1] != s2[1]) 
        c++; 
    if (s1[2] != s2[2]) 
        c++; 
    if (s1[3] != s2[3]) 
        c++; 

    // If the numbers differ only by a single 
    // digit return true else false 
    return (c == 1); 
} 

int shortestPath(int num1, int num2) 
{ 
    // Generate all 4 digit 
    vector<int> pset;  
    SieveOfEratosthenes(pset); 

    // Create a graph where node numbers are indexes 
    // in pset[] and there is an edge between two  
    // nodes only if they differ by single digit. 
    graph g(pset.size());  
    for (int i = 0; i < pset.size(); i++)  
        for (int j = i + 1; j < pset.size(); j++)  
            if (compare(pset[i], pset[j])) 
                g.addedge(i, j);      

    // Since graph nodes represent indexes of numbers 
    // in pset[], we find indexes of num1 and num2\. 
    int in1, in2; 
    for (int j = 0; j < pset.size(); j++)  
        if (pset[j] == num1) 
            in1 = j;  
    for (int j = 0; j < pset.size(); j++)  
        if (pset[j] == num2) 
            in2 = j;  

    return g.bfs(in1, in2); 
} 

// Driver code 
int main() 
{ 
    int num1 = 1033, num2 = 8179; 
    cout << shortestPath(num1, num2); 
    return 0; 
} 

```