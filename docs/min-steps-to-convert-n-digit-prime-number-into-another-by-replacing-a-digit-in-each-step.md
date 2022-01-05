# 通过在每一步中替换一个数字将 N 位质数转换成另一个质数的最小步骤

> 原文:[https://www . geesforgeks . org/min-steps-通过每一步替换一位数字将 n 位质数转换为另一位质数/](https://www.geeksforgeeks.org/min-steps-to-convert-n-digit-prime-number-into-another-by-replacing-a-digit-in-each-step/)

给定两个 **N** 位质数 **A** 和 **B** ，任务是找到将 A 转换为 B 所采取的最小步骤数。转换的条件是当前质数只有 1 位可以修改，这样形成的新数也是质数。如果无法进行这样的转换，请打印-1。

**注:**N 的范围为[1，5]。

**示例:**

> **输入:** N = 4，A = 1033，B = 8179
> **输出:** 6
> **说明:**转换的步骤为 1033->1733->3733->3739->3779->8779->8179。从 1033- > 1733 更改数字时，它们仅相差一个数字，后续步骤也是如此。
> 
> **输入:** N = 4，A = 1373，B = 8179
> T3】输出: 7
> 
> **输入:** N = 2，A = 11，B = 37
> **输出:** 2
> **说明:**转换的步骤为 11 - > 17 - > 37

**方法:**使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)算法

1.  找出所有 N 位素数，用这些数画一个图。
2.  将每个素数视为图的一个节点，如果它们相差一位数，则创建一条从一个节点到另一个节点的边。
3.  应用 BFS 遍历，找出 A 和 b 之间的边数
4.  如果不存在路径，打印-1。
5.  否则打印边数，这是必需的解决方案。

下面是上述方法的实现。

## C++

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
            // add the distance of curr+1.
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

        // Indicates not possible
        cout << "-1" << endl;
    else
        cout << dis[B] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.*;
public class GFG
{

  // Adjacency list for numbers
  // till 100001
  static Vector<Vector<Integer>> lis = new Vector<Vector<Integer>>();    
  static Vector<Integer> primes = new Vector<Integer>();

  // Visited array
  static int[] vis = new int[100001];

  // To store distance of every
  // vertex from A
  static int[] dis = new int[100001];

  // Function to check if number
  // is a prime
  static boolean isPrime(int n)
  {
    int i = 2;
    while (i * i <= n)
    {
      if (n % i == 0)
        return false;
      i += 1;
    }
    return true;
  }

  // Function to check if numbers
  // differ by only a single-digit
  static boolean valid(int a, int b)
  {
    int c = 0;       
    while(a > 0)
    {

      // Check the last digit of
      // both numbers and increase
      // count if different
      if ((a % 10) != (b % 10))
        c += 1;            
      a = a / 10;
      b = b / 10;
    }    
    if (c == 1)
      return true;
    else
      return false;
  }

  static void makePrimes(int N)
  {

    // Generate all N digit primes
    int L = (int)Math.pow(10, N - 1);
    int R = (int)Math.pow(10, N) - 1;

    for(int i = L; i < R + 1; i++)
    {
      if (isPrime(i))
        primes.add(i);
    }

    for(int i = 0; i < primes.size(); i++)
    {

      // For every prime number i
      // check if an edge
      // can be made.
      for(int j = i + 1; j < primes.size(); j++)
      {
        int a = primes.get(i);
        int b = primes.get(j);

        // For every prime number
        // i check if an edge can
        // be made from i to j.
        if (valid(a, b))
        {

          // If edge is possible then
          // insert in the adjacency
          // list
          lis.get(a).add(b);
          lis.get(b).add(a);
        }
      }
    }
  }

  // Function to count distance
  static void bfs(int src)
  {
    Vector<Integer> q = new Vector<Integer>();
    q.add(src);
    vis[src] = 1;
    dis[src] = 0;
    while (q.size() != 0)
    {
      int curr = q.get(0);
      q.remove(0);
      for(int x : lis.get(curr))
      {
        // If unvisited push onto queue
        // and mark visited as 1 and
        // add the distance of curr+1.
        if (vis[x] == 0)
        {
          vis[x] = 1;
          q.add(x);
          dis[x] = dis[curr] + 1;
        }
      }
    }
  }

  // Driver code
  public static void main(String[] args)
  {
    for(int i = 0; i < 100001; i++)
    {
      lis.add(new Vector<Integer>());
    }
    int N = 4;
    makePrimes(N);
    int A = 1033;
    int B = 8179;

    // Call bfs traversal
    // with root as node A
    bfs(A);

    if (dis[B] == -1)
    {
      // Indicates not possible
      System.out.print(-1);
    }
    else
    {
      System.out.print(dis[B]);
    }
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above problem
mod = 1000000007

# Adjacency list for numbers
# till 100001
lis = [[] for i in range(100001)]
primes = []

# Visited array
vis = [0 for i in range(100001)]

# To store distance of every
# vertex from A
dis = [0 for i in range(100001)]

# Function to check if number
# is a prime
def isPrime(n):

    i = 2
    while (i * i <= n):
        if (n % i == 0):
            return False

        i += 1

    return True

# Function to check if numbers
# differ by only a single-digit
def valid(a, b):

    c = 0

    while(a):

        # Check the last digit of
        # both numbers and increase
        # count if different
        if ((a % 10) != (b % 10)):
            c += 1

        a = int(a / 10)
        b = int(b / 10)

    if (c == 1):
        return True
    else:
        return False

def makePrimes(N):

    global primes
    global lis
    i = 0
    j = 0

    # Generate all N digit primes
    L = pow(10, N - 1)
    R = pow(10, N) - 1

    for i in range(L, R + 1):
        if (isPrime(i)):
            primes.append(i)

    for i in range(len(primes)):

        # For every prime number i
        # check if an edge
        # can be made.
        for j in range(i + 1, len(primes)):
            a = primes[i]
            b = primes[j]

            # For every prime number
            # i check if an edge can
            # be made from i to j.
            if (valid(a, b)):

                # If edge is possible then
                # insert in the adjacency
                # list
                lis[a].append(b)
                lis[b].append(a)

# Function to count distance
def bfs(src):

    global vis
    global dis
    q = []
    q.append(src)
    vis[src] = 1
    dis[src] = 0

    while (len(q) != 0):
        curr = q[0]
        q.pop(0)

        for x in lis[curr]:

            # If unvisited push onto queue
            # and mark visited as 1 and
            # add the distance of curr+1.
            if (vis[x] == 0):
                vis[x] = 1
                q.append(x)
                dis[x] = dis[curr] + 1

# Driver code
N = 4
makePrimes(N)
A = 1033
B = 8179

# Call bfs traversal
# with root as node A
bfs(A)

if (dis[B] == -1):

    # Indicates not possible
    print(-1)
else:
    print(dis[B])

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above problem
using System;
using System.Collections.Generic;
class GFG {

    // Adjacency list for numbers
    // till 100001
    static List<List<int>> lis = new List<List<int>>();

    static List<int> primes = new List<int>();

    // Visited array
    static int[] vis = new int[100001];

    // To store distance of every
    // vertex from A
    static int[] dis = new int[100001];

    // Function to check if number
    // is a prime
    static bool isPrime(int n)
    {
        int i = 2;
        while (i * i <= n)
        {
            if (n % i == 0)
                return false;
            i += 1;
        }
        return true;
    }

    // Function to check if numbers
    // differ by only a single-digit
    static bool valid(int a, int b)
    {
        int c = 0;

        while(a > 0)
        {
            // Check the last digit of
            // both numbers and increase
            // count if different
            if ((a % 10) != (b % 10))
                c += 1;

            a = a / 10;
            b = b / 10;
        }

        if (c == 1)
            return true;
        else
            return false;
    }

    static void makePrimes(int N)
    {

        // Generate all N digit primes
        int L = (int)Math.Pow(10, N - 1);
        int R = (int)Math.Pow(10, N) - 1;

        for(int i = L; i < R + 1; i++)
        {
            if (isPrime(i))
                primes.Add(i);
        }

        for(int i = 0; i < primes.Count; i++)
        {

            // For every prime number i
            // check if an edge
            // can be made.
            for(int j = i + 1; j < primes.Count; j++)
            {
                int a = primes[i];
                int b = primes[j];

                // For every prime number
                // i check if an edge can
                // be made from i to j.
                if (valid(a, b))
                {
                    // If edge is possible then
                    // insert in the adjacency
                    // list
                    lis[a].Add(b);
                    lis[b].Add(a);
                }
            }
        }
    }

    // Function to count distance
    static void bfs(int src)
    {
        List<int> q = new List<int>();
        q.Add(src);
        vis[src] = 1;
        dis[src] = 0;

        while (q.Count != 0)
        {
            int curr = q[0];
            q.RemoveAt(0);

            foreach(int x in lis[curr])
            {
                // If unvisited push onto queue
                // and mark visited as 1 and
                // add the distance of curr+1.
                if (vis[x] == 0)
                {
                    vis[x] = 1;
                    q.Add(x);
                    dis[x] = dis[curr] + 1;
                }
            }
        }
    }

  // Driver code
  static void Main()
  {
    for(int i = 0; i < 100001; i++)
    {
        lis.Add(new List<int>());
    }
    int N = 4;
    makePrimes(N);
    int A = 1033;
    int B = 8179;

    // Call bfs traversal
    // with root as node A
    bfs(A);

    if (dis[B] == -1)
    {
        // Indicates not possible
        Console.Write(-1);
    }
    else
    {
        Console.Write(dis[B]);
    }
  }
}
```

**Output:** 

```
6
```

***时间复杂度:**O(10<sup>2N</sup>)*
***辅助空间复杂度:** O(10 <sup>5</sup> )*