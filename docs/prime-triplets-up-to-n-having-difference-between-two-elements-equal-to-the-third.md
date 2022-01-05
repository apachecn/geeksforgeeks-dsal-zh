# 素数三元组，由两个元素之差最大为 N 的值组成，等于第三个

> 原文:[https://www . geesforgeks . org/prime-triples-高达-n-两个元素之间有差异-等于三分之一/](https://www.geeksforgeeks.org/prime-triplets-up-to-n-having-difference-between-two-elements-equal-to-the-third/)

给定一个正整数 **N** ，任务是找到所有的[素数三元组](https://www.geeksforgeeks.org/prime-triplet/) **{P，Q，R}** ，使得**P = R–Q**和 **P** 、 **Q** 和 **R** 小于 **N** 。

**示例:**

> ***输入:** N = 8*
> ***输出:***
> *2 3 5*
> *2 5 7*
> ***解释:***
> *满足给定条件的仅有 2 个素数三元组是:*
> 
> *   {2，3，5}: P = 2，Q = 3，R = 5。因此，P，Q 和 R 是素数，P = R–Q。
> *   {2，5，7}: P = 2，Q = 5，R = 7。因此，P，Q 和 R 是素数，P = R–Q。
> 
> ***输入:**N = 5*
> T5**输出:** 2 3 5

**方法:**给定的问题可以基于以下观察来解决:

*   通过重新排列给定的方程，可以观察到 **P + Q = R** ，**两个奇数**之和为**偶数**，**一个奇数**和**一个偶数**之和为**奇数**。
*   因为只有一个偶数素数，即 **2** 。让 **P** 为奇素数， **Q** 为奇素数那么 **R** 永远不可能是素数，所以 **P** 必须永远是 **2** 也就是**偶素数**， **Q** 就是**奇素数**那么 **R** 应该是**奇素数**。所以有必要找质数 **Q** 这样 **Q > 2** 和 **R = P + Q ≤ N(其中 P = 2)，R 应该是质数**。

按照以下步骤解决问题:

*   使用厄拉多塞的[筛预计算范围**【1，N】**内的所有](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[质数](https://www.geeksforgeeks.org/prime-numbers/)。
*   初始化一个向量的[向量，比如 **V** ，来存储所有的结果三元组。](https://www.geeksforgeeks.org/vector-of-vectors-in-c-stl-with-examples/)
*   [使用一个变量迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【3，N】**，比如说 **i** 。[如果 **i** 和 **(i + 2)** 为素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)和 **2 + i ≤ N** ，则将当前三元组存储在向量 **V** 中。
*   完成以上步骤后，打印 **V[]** 中存储的所有三胞胎。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores 1 and 0 at indices which
// are prime and non-prime respectively
bool prime[100000];

// Function to find all prime
// numbers from the range [0, N]
void SieveOfEratosthenes(int n)
{
    // Consider all numbers to prime initially
    memset(prime, true, sizeof(prime));

    // Iterate over the range [2, sqrt(N)]
    for (int p = 2; p * p <= n; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Update all tultiples
            // of p as false
            for (int i = p * p;
                 i <= n; i += p) {
                prime[i] = false;
            }
        }
    }
}

// Function to find all prime triplets
// satisfying the given conditions
void findTriplets(int N)
{
    // Generate all primes up to N
    SieveOfEratosthenes(N);

    // Stores the triplets
    vector<vector<int> > V;

    // Iterate over the range [3, N]
    for (int i = 3; i <= N; i++) {

        // Check for the condition
        if (2 + i <= N && prime[i]
            && prime[2 + i]) {

            // Store the triplets
            V.push_back({ 2, i, i + 2 });
        }
    }

    // Print all the stored triplets
    for (int i = 0; i < V.size(); i++) {
        cout << V[i][0] << " "
             << V[i][1] << " "
             << V[i][2] << "\n";
    }
}

// Driver Code
int main()
{
    int N = 8;
    findTriplets(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Stores 1 and 0 at indices which
// are prime and non-prime respectively
static boolean[] prime = new boolean[100000];

static void initialize()
{
    for(int i = 0; i < 100000; i++)
        prime[i] = true;
}

// Function to find all prime
// numbers from the range [0, N]
static void SieveOfEratosthenes(int n)
{

    // Iterate over the range [2, sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all tultiples
            // of p as false
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to find all prime triplets
// satisfying the given conditions
static void findTriplets(int N)
{

    // Generate all primes up to N
    SieveOfEratosthenes(N);

    // Stores the triplets
    ArrayList<ArrayList<Integer>> V = new ArrayList<ArrayList<Integer>>();
    // List<List<int> > V = new List<List<int>>();

    // Iterate over the range [3, N]
    for(int i = 3; i <= N; i++)
    {

        // Check for the condition
        if (2 + i <= N && prime[i] && prime[2 + i])
        {

            // Store the triplets
            ArrayList<Integer> a1 = new ArrayList<Integer>();
            a1.add(2);
            a1.add(i);
            a1.add(i + 2);
            V.add(a1);
        }
    }

    // Print all the stored triplets
    for(int i = 0; i < V.size(); i++)
    {
        System.out.println(V.get(i).get(0) + " " +
                           V.get(i).get(1) + " " +
                           V.get(i).get(2));
    }
}

// Driver Code
public static void main(String args[])
{
    initialize();
    int N = 8;

    findTriplets(N);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt

# Stores 1 and 0 at indices which
# are prime and non-prime respectively
prime = [True for i in range(100000)]

# Function to find all prime
# numbers from the range [0, N]
def SieveOfEratosthenes(n):

    # Iterate over the range [2, sqrt(N)]
    for p in range(2, int(sqrt(n)) + 1, 1):

        # If p is a prime
        if (prime[p] == True):

            # Update all tultiples
            # of p as false
            for i in range(p * p, n + 1, p):
                prime[i] = False

# Function to find all prime triplets
# satisfying the given conditions
def findTriplets(N):

    # Generate all primes up to N
    SieveOfEratosthenes(N)

    # Stores the triplets
    V = []

    # Iterate over the range [3, N]
    for i in range(3, N + 1, 1):

        # Check for the condition
        if (2 + i <= N and prime[i] and prime[2 + i]):

            # Store the triplets
            V.append([2, i, i + 2])

    # Print all the stored triplets
    for i in range(len(V)):
        print(V[i][0], V[i][1], V[i][2])

# Driver Code
if __name__ == '__main__':
    N = 8
    findTriplets(N)

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Stores 1 and 0 at indices which
// are prime and non-prime respectively
static bool[] prime = new bool[100000];

static void initialize()
{
    for(int i = 0; i < 100000; i++)
        prime[i] = true;
}

// Function to find all prime
// numbers from the range [0, N]
static void SieveOfEratosthenes(int n)
{

    // Iterate over the range [2, sqrt(N)]
    for(int p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all tultiples
            // of p as false
            for(int i = p * p; i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to find all prime triplets
// satisfying the given conditions
static void findTriplets(int N)
{

    // Generate all primes up to N
    SieveOfEratosthenes(N);

    // Stores the triplets
    List<List<int>> V = new List<List<int>>();

    // Iterate over the range [3, N]
    for(int i = 3; i <= N; i++)
    {

        // Check for the condition
        if (2 + i <= N && prime[i] ==
                  true && prime[2 + i])
        {

            // Store the triplets
            List<int> a1 = new List<int>();
            a1.Add(2);
            a1.Add(i);
            a1.Add(i + 2);
            V.Add(a1);
        }
    }

    // Print all the stored triplets
    for(int i = 0; i < V.Count; i++)
    {
        Console.WriteLine(V[i][0] + " " +
                          V[i][1] + " " +
                          V[i][2]);
    }
}

// Driver Code
public static void Main()
{
    initialize();
    int N = 8;

    findTriplets(N);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Stores 1 and 0 at indices which
// are prime and non-prime respectively
var prime = new Array(100000);

// Function to find all prime
// numbers from the range [0, N]
function SieveOfEratosthenes(n)
{

    // Consider all numbers to prime initially
    prime.fill(true);

    // Iterate over the range [2, sqrt(N)]
    for(var p = 2; p * p <= n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Update all tultiples
            // of p as false
            for(var i = p * p;
                    i <= n; i += p)
            {
                prime[i] = false;
            }
        }
    }
}

// Function to find all prime triplets
// satisfying the given conditions
function findTriplets(N)
{

    // Generate all primes up to N
    SieveOfEratosthenes(N);

    // Stores the triplets
    var V = [];

    // Iterate over the range [3, N]
    for(var i = 3; i <= N; i++)
    {

        // Check for the condition
        if (2 + i <= N && prime[i] == true &&
                          prime[2 + i] == true)
        {

            // Store the triplets
            var a1 = [2, i, i + 2];

            V.push(a1);
        }
    }

    // Print all the stored triplets
    for(var i = 0; i < V.length; i++)
    {
        document.write(V[i][0] + " " +
                       V[i][1] + " " +
                       V[i][2] + "<br>");
    }
}

// Driver code
N = 8;

findTriplets(N);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
2 3 5
2 5 7
```

**时间复杂度:** O(N*log(log(N)))
**辅助空间:** O(1)