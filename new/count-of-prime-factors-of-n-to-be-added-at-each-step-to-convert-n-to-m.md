# 在每个步骤中将 N 转换为 M 的 N 的质因子数

> 原文： [https://www.geeksforgeeks.org/count-of-prime-factors-of-n-to-be-added-at-each-step-to-convert-n-to-m/](https://www.geeksforgeeks.org/count-of-prime-factors-of-n-to-be-added-at-each-step-to-convert-n-to-m/)

给定两个整数`N`和`M`，任务是找出将`N`转换​​为`M`所需的最小操作数。 每个操作都涉及将`N`当前值的[主因子](http://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)之一相加。 如果有可能获得 M，则打印操作数。 否则，打印`-1`。

**示例**：

> **输入**：N = 6，M = 10
> **输出**：2
> **说明**：
> 6 的质因子是[2，3 ]。
> 将 N 加 2，得到 8。
> 8 的素数是[2]。
> 将 N 加 2，我们得到 10，这是期望的结果。
> 因此，总步数= 2
> 
> **输入**：N = 2，M = 3
> **输出**：-1
> **说明**：
> 无法转换 N = 2 至 M = 3

**方法**：
该问题可以通过使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 获得达到 M 的最小步长和[硅酮筛网](http://www.geeksforgeeks.org/sieve-of-eratosthenes/)来预先计算质数来解决。
请按照以下步骤解决问题：

*   使用 Sieve 存储并预计算所有素数。
*   现在，如果 N 已经等于 M，则打印 0，因为不需要加法运算。
*   将此问题可视化为执行 **BFS** 的图形问题。 在每个级别上，通过添加质数来存储上一级别中 N 的值可获得的数字。
*   现在，首先在队列中插入**（N，0）**，其中 N 表示该值，0 表示达到该值的操作数。
*   在队列的每个级别，通过提取 [front（）](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)处的元素来逐个遍历所有元素，然后执行以下操作：
    1.  将 **q.front（）。first（）**存储在 **newNum** 中，将 **q.front（）。second（）**存储在**距离**中，其中 **newNum** 是当前值，**距离**是达到该值所需的操作次数。
    2.  将 **newNum** 的所有素因子存储在[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。
    3.  如果 **newNum** 等于`M`，则打印距离，因为它是所需的最小操作。
    4.  如果 **newNum** 大于 M，则中断。
    5.  否则，newNum 小于 M。因此，通过逐个添加其主要因子 i 来更新 newNum，并将**（newNum + i，距离+ 1）**存储在队列中，并为下一级重复上述步骤 。
*   如果搜索继续到队列变空的级别，则意味着无法从 N 获得 M。打印-1。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the minimum
// steps required to convert a number
// N to M.
#include <bits/stdc++.h>
using namespace std;

// Array to store shortest prime
// factor of every integer
int spf[100009];

// Function to precompute
// shortest prime factors
void sieve()
{
    memset(spf, -1, 100005);
    for (int i = 2; i * i <= 100005; i++) {
        for (int j = i; j <= 100005; j += i) {
            if (spf[j] == -1) {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
set<int> findPrimeFactors(set<int> s,
                          int n)
{
    // Store distinct prime
    // factors
    while (n > 1) {
        s.insert(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    queue<pair<int, int> > q;

    // Set to store distinct
    // prime factors
    set<int> s;

    // Run BFS
    q.push({ n, 0 });
    while (!q.empty()) {

        int newNum = q.front().first;
        int distance = q.front().second;

        q.pop();

        // Find out the prime factors of newNum
        set<int> k = findPrimeFactors(s,
                                      newNum);

        // Iterate over every prime
        // factor of newNum.
        for (auto i : k) {

            // If M is obtained
            if (newNum == m) {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m) {
                break;
            }

            // Otherwise
            else {

                // Update and store the new
                // number obtained by prime factor
                q.push({ newNum + i,
                         distance + 1 });
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
int main()
{
    int N = 7, M = 16;

    sieve();

    cout << MinimumSteps(N, M);
}

```

## Java

```java

// Java program to find the minimum
// steps required to convert a number
// N to M.
import java.util.*;

class GFG{

static class pair
{ 
    int first, second; 

    public pair(int first, int second)  
    { 
        this.first = first; 
        this.second = second; 
    }    
} 

// Array to store shortest prime
// factor of every integer
static int []spf = new int[100009];

// Function to precompute
// shortest prime factors
static void sieve()
{
    for(int i = 0; i < 100005; i++)
        spf[i] = -1;

    for(int i = 2; i * i <= 100005; i++) 
    {
        for(int j = i; j <= 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
static HashSet<Integer> findPrimeFactors(HashSet<Integer> s,
                                         int n)
{

    // Store distinct prime
    // factors
    while (n > 1)
    {
        s.add(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
static int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    Queue<pair > q = new LinkedList<>();

    // Set to store distinct
    // prime factors
    HashSet<Integer> s = new HashSet<Integer>();

    // Run BFS
    q.add(new pair(n, 0));

    while (!q.isEmpty()) 
    {
        int newNum = q.peek().first;
        int distance = q.peek().second;

        q.remove();

        // Find out the prime factors of newNum
        HashSet<Integer> k = findPrimeFactors(s,
                                      newNum);

        // Iterate over every prime
        // factor of newNum.
        for(int i : k) 
        {

            // If M is obtained
            if (newNum == m)
            {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m)
            {
                break;
            }

            // Otherwise
            else
            {

                // Update and store the new
                // number obtained by prime factor
                q.add(new pair(newNum + i,
                             distance + 1 ));
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
public static void main(String[] args)
{
    int N = 7, M = 16;

    sieve();

    System.out.print(MinimumSteps(N, M));
}
}

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program to find the minimum
// steps required to convert a number
// N to M.
using System;
using System.Collections.Generic;

class GFG{

class pair
{ 
    public int first, second; 

    public pair(int first, int second)  
    { 
        this.first = first; 
        this.second = second; 
    }    
} 

// Array to store shortest prime
// factor of every integer
static int []spf = new int[100009];

// Function to precompute
// shortest prime factors
static void sieve()
{
    for(int i = 0; i < 100005; i++)
        spf[i] = -1;

    for(int i = 2; i * i <= 100005; i++) 
    {
        for(int j = i; j <= 100005; j += i)
        {
            if (spf[j] == -1)
            {
                spf[j] = i;
            }
        }
    }
}

// Function to insert distinct prime factors
// of every integer into a set
static HashSet<int> findPrimeFactors(HashSet<int> s,
                                             int n)
{

    // Store distinct prime
    // factors
    while (n > 1)
    {
        s.Add(spf[n]);
        n /= spf[n];
    }
    return s;
}

// Function to return minimum
// steps using BFS
static int MinimumSteps(int n, int m)
{

    // Queue of pairs to store
    // the current number and
    // distance from root.
    Queue<pair> q = new Queue<pair>();

    // Set to store distinct
    // prime factors
    HashSet<int> s = new HashSet<int>();

    // Run BFS
    q.Enqueue(new pair(n, 0));

    while (q.Count != 0) 
    {
        int newNum = q.Peek().first;
        int distance = q.Peek().second;

        q.Dequeue();

        // Find out the prime factors of newNum
        HashSet<int> k = findPrimeFactors(s,
                                          newNum);

        // Iterate over every prime
        // factor of newNum.
        foreach(int i in k) 
        {

            // If M is obtained
            if (newNum == m)
            {

                // Return number of
                // operations
                return distance;
            }

            // If M is exceeded
            else if (newNum > m)
            {
                break;
            }

            // Otherwise
            else
            {

                // Update and store the new
                // number obtained by prime factor
                q.Enqueue(new pair(newNum + i,
                                 distance + 1));
            }
        }
    }

    // If M cannot be obtained
    return -1;
}

// Driver code
public static void Main(String[] args)
{
    int N = 7, M = 16;

    sieve();

    Console.Write(MinimumSteps(N, M));
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
2

```

***时间复杂度**：O（N * log（N））*
***辅助空间**：O（N）*

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。