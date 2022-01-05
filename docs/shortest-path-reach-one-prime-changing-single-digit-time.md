# 每次改变一个数字到达另一个素数的最短路径

> 原文:[https://www . geesforgeks . org/最短路径-到达-一个质数-变化-个位数-时间/](https://www.geeksforgeeks.org/shortest-path-reach-one-prime-changing-single-digit-time/)

给定两个四位数的素数，假设 1033 和 8179，我们需要通过一次只改变一个位数来找到从 1033 到 8179 的最短路径，这样我们在改变一个位数后得到的每个数都是素数。例如，解决方案是 1033、1733、3733、3739、3779、8779、8179

**示例:**

```
Input : 1033 8179
Output :6

Input : 1373 8017
Output : 7

Input  :  1033 1033
Output : 0

```

这个问题可以通过*[【BFS】](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)*来解决，作为初学者的入门问题，解决起来还是蛮有意思的。我们首先利用厄拉多塞的[筛技术找出 9999 年以前的所有 4 位素数。然后用这些数字组成了使用邻接表](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的[图。在形成邻接表之后，我们使用简单的 BFS 来解决这个问题。](https://www.geeksforgeeks.org/graph-and-its-representations/) 

## C++

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
    // in pset[], we find indexes of num1 and num2.
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

## 蟒蛇 3

```
# Python3 program to reach a prime number 
# from another by changing single digits  
# and using only prime numbers.
import queue 

class Graph: 

    def __init__(self, V):
        self.V = V; 
        self.l = [[] for i in range(V)]

    def addedge(self, V1, V2):
        self.l[V1].append(V2); 
        self.l[V2].append(V1);

    # in1 and in2 are two vertices of graph  
    # which are actually indexes in pset[] 
    def bfs(self, in1, in2):
        visited = [0] * self.V
        que = queue.Queue()
        visited[in1] = 1
        que.put(in1)
        while (not que.empty()): 
            p = que.queue[0] 
            que.get()
            i = 0
            while i < len(self.l[p]):
                if (not visited[self.l[p][i]]):
                    visited[self.l[p][i]] = visited[p] + 1
                    que.put(self.l[p][i])
                if (self.l[p][i] == in2):
                    return visited[self.l[p][i]] - 1
                i += 1

    # Returns true if num1 and num2 
    # differ by single digit.

# Finding all 4 digit prime numbers 
def SieveOfEratosthenes(v):

    # Create a boolean array "prime[0..n]" and  
    # initialize all entries it as true. A value 
    # in prime[i] will finally be false if i is 
    # Not a prime, else true. 
    n = 9999
    prime = [True] * (n + 1)

    p = 2
    while p * p <= n:

        # If prime[p] is not changed, 
        # then it is a prime 
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * p, n + 1, p):
                prime[i] = False
        p += 1

    # Forming a vector of prime numbers
    for p in range(1000, n + 1):
        if (prime[p]): 
            v.append(p)

def compare(num1, num2):

    # To compare the digits 
    s1 = str(num1) 
    s2 = str(num2)
    c = 0
    if (s1[0] != s2[0]):
        c += 1
    if (s1[1] != s2[1]):
        c += 1
    if (s1[2] != s2[2]):
        c += 1
    if (s1[3] != s2[3]): 
        c += 1

    # If the numbers differ only by a single 
    # digit return true else false 
    return (c == 1)

def shortestPath(num1, num2):

    # Generate all 4 digit 
    pset = [] 
    SieveOfEratosthenes(pset) 

    # Create a graph where node numbers 
    # are indexes in pset[] and there is 
    # an edge between two nodes only if 
    # they differ by single digit. 
    g = Graph(len(pset))
    for i in range(len(pset)):
        for j in range(i + 1, len(pset)):
            if (compare(pset[i], pset[j])): 
                g.addedge(i, j)     

    # Since graph nodes represent indexes 
    # of numbers in pset[], we find indexes
    # of num1 and num2. 
    in1, in2 = None, None
    for j in range(len(pset)):
        if (pset[j] == num1):
            in1 = j
    for j in range(len(pset)):
        if (pset[j] == num2): 
            in2 = j

    return g.bfs(in1, in2)

# Driver code 
if __name__ == '__main__':

    num1 = 1033
    num2 = 8179
    print(shortestPath(num1, num2))

# This code is contributed by PranchalK
```

**Output :**

```
6
```