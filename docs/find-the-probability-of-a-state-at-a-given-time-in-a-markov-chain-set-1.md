# 求马尔可夫链中给定时间某个状态的概率|集合 1

> 原文:[https://www . geeksforgeeks . org/find-马尔可夫链中给定时间的状态概率集-1/](https://www.geeksforgeeks.org/find-the-probability-of-a-state-at-a-given-time-in-a-markov-chain-set-1/)

给定一个马氏链 G，如果我们在时间 t = 0 从状态 S 开始，我们可以找到在时间 t = T 到达状态 F 的概率。
马尔可夫链是一个随机过程，由各种状态和从一种状态移动到另一种状态的概率组成。我们可以用有向图来表示它，其中节点代表状态，边代表从一个节点到另一个节点的概率。从一个节点移动到另一个节点需要单位时间。每个节点的输出边的相关概率之和为 1。

考虑如下图所示的给定马尔可夫链:

![](img/e96f85a5c6fe1fc66a33720d249c3b4b.png)

**示例** :

```
Input : S = 1, F = 2, T = 1
Output : 0.23
We start at state 1 at t = 0, 
so there is a probability of 0.23 
that we reach state 2 at t = 1.

Input : S = 4, F = 2, T = 100
Output : 0.284992
```

我们可以用**动态规划**和**深度优先搜索**来解决这个问题，把状态和时间作为两个 DP 变量。我们可以很容易地观察到，在时间 *t* 从状态 A 到状态 B 的概率等于在时间*t–1*处于 A 的概率和与连接 A 和 B 的边相关的概率的乘积。因此，在时间 *t* 处于 B 的概率是与 B 相邻的所有 A 的这个量的和

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Macro for vector of pair to store
// each node with edge
#define vp vector<pair<int, float> >

// Function to calculate the
// probability of reaching F
// at time T after starting
// from S
float findProbability(vector<vp>& G, int N,
                      int F, int S, int T)
{
    // Declaring the DP table
    vector<vector<float> > P(N + 1, vector<float>(T + 1, 0));

    // Probability of being at S
    // at t = 0 is 1.0
    P[S][0] = 1.0;

    // Filling the DP table
    // in bottom-up manner
    for (int i = 1; i <= T; ++i)
        for (int j = 1; j <= N; ++j)
            for (auto k : G[j])
                P[j][i] += k.second * P[k.first][i - 1];

    return P[F][T];
}

// Driver code
int main()
{
    // Adjacency list
    vector<vp> G(7);

    // Building the graph
    // The edges have been stored in the row
    // corresponding to their end-point
    G[1] = vp({ { 2, 0.09 } });
    G[2] = vp({ { 1, 0.23 }, { 6, 0.62 } });
    G[3] = vp({ { 2, 0.06 } });
    G[4] = vp({ { 1, 0.77 }, { 3, 0.63 } });
    G[5] = vp({ { 4, 0.65 }, { 6, 0.38 } });
    G[6] = vp({ { 2, 0.85 }, { 3, 0.37 }, { 4, 0.35 }, { 5, 1.0 } });

    // N is the number of states
    int N = 6;

    int S = 4, F = 2, T = 100;

    cout << "The probability of reaching " << F
         << " at time " << T << " \nafter starting from "
         << S << " is " << findProbability(G, N, F, S, T);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{
    static class pair
    {
        int first;
        double second;

        public pair(int first, double second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to calculate the
    // probability of reaching F
    // at time T after starting
    // from S
    static float findProbability(Vector<pair>[] G,
                        int N, int F, int S, int T)
    {
        // Declaring the DP table
        float[][] P = new float[N + 1][T + 1];

        // Probability of being at S
        // at t = 0 is 1.0
        P[S][0] = (float) 1.0;

        // Filling the DP table
        // in bottom-up manner
        for (int i = 1; i <= T; ++i)
            for (int j = 1; j <= N; ++j)
                for (pair k : G[j])
                    P[j][i] += k.second * P[k.first][i - 1];

        return P[F][T];
    }

    // Driver code
    public static void main(String[] args)
    {
        // Adjacency list
        Vector<pair>[] G = new Vector[7];
        for (int i = 0; i < 7; i++)
        {
            G[i] = new Vector<pair>();
        }

        // Building the graph
        // The edges have been stored in the row
        // corresponding to their end-point
        G[1].add(new pair(2, 0.09));
        G[2].add(new pair(1, 0.23));
        G[2].add(new pair(6, 0.62));
        G[3].add(new pair(2, 0.06));
        G[4].add(new pair(1, 0.77));
        G[4].add(new pair(3, 0.63));
        G[5].add(new pair(4, 0.65));
        G[5].add(new pair(6, 0.38));
        G[6].add(new pair(2, 0.85));
        G[6].add(new pair(3, 0.37));
        G[6].add(new pair(4, 0.35));
        G[6].add(new pair(5, 1.0));

        // N is the number of states
        int N = 6;

        int S = 4, F = 2, T = 100;

        System.out.print("The probability of reaching " + F +
                " at time " + T + " \nafter starting from " +
                S + " is "
                + findProbability(G, N, F, S, T));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Macro for vector of pair to store
# each node with edge
# define vp vector<pair<int, float> >

# Function to calculate the
# probability of reaching F
# at time T after starting
# from S
def findProbability(G, N, F, S, T):

    # Declaring the DP table
    P = [[0 for i in range(T + 1)]
            for j in range(N + 1)]

    # Probability of being at S
    # at t = 0 is 1.0
    P[S][0] = 1.0;

    # Filling the DP table
    # in bottom-up manner
    for i in range(1, T + 1):
        for j in range(1, N + 1):
            for k in G[j]:
                P[j][i] += k[1] * P[k[0]][i - 1];

    return P[F][T]

# Driver code
if __name__=='__main__':

    # Adjacency list
    G = [0 for i in range(7)]

    # Building the graph
    # The edges have been stored in the row
    # corresponding to their end-point
    G[1] = [ [ 2, 0.09 ] ]
    G[2] = [ [ 1, 0.23 ], [ 6, 0.62 ] ]
    G[3] = [ [ 2, 0.06 ] ]
    G[4] = [ [ 1, 0.77 ], [ 3, 0.63 ] ]
    G[5] = [ [ 4, 0.65 ], [ 6, 0.38 ] ]
    G[6] = [ [ 2, 0.85 ], [ 3, 0.37 ],
             [ 4, 0.35 ], [ 5, 1.0 ] ]

    # N is the number of states
    N = 6

    S = 4
    F = 2
    T = 100

    print("The probability of reaching {} at "
          "time {}\nafter starting from {} is {}".format(
          F, T, S, findProbability(G, N, F, S, T)))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{
    class pair
    {
        public int first;
        public double second;

        public pair(int first, double second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to calculate the
    // probability of reaching F
    // at time T after starting
    // from S
    static float findProbability(List<pair>[] G,
                        int N, int F, int S, int T)
    {
        // Declaring the DP table
        float[,] P = new float[N + 1, T + 1];

        // Probability of being at S
        // at t = 0 is 1.0
        P[S, 0] = (float) 1.0;

        // Filling the DP table
        // in bottom-up manner
        for (int i = 1; i <= T; ++i)
            for (int j = 1; j <= N; ++j)
                foreach (pair k in G[j])
                    P[j, i] += (float)k.second *
                                P[k.first, i - 1];

        return P[F, T];
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Adjacency list
        List<pair>[] G = new List<pair>[7];
        for (int i = 0; i < 7; i++)
        {
            G[i] = new List<pair>();
        }

        // Building the graph
        // The edges have been stored in the row
        // corresponding to their end-point
        G[1].Add(new pair(2, 0.09));
        G[2].Add(new pair(1, 0.23));
        G[2].Add(new pair(6, 0.62));
        G[3].Add(new pair(2, 0.06));
        G[4].Add(new pair(1, 0.77));
        G[4].Add(new pair(3, 0.63));
        G[5].Add(new pair(4, 0.65));
        G[5].Add(new pair(6, 0.38));
        G[6].Add(new pair(2, 0.85));
        G[6].Add(new pair(3, 0.37));
        G[6].Add(new pair(4, 0.35));
        G[6].Add(new pair(5, 1.0));

        // N is the number of states
        int N = 6;

        int S = 4, F = 2, T = 100;

        Console.Write("The probability of reaching " + F +
                " at time " + T + " \nafter starting from " +
                S + " is "
                + findProbability(G, N, F, S, T));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to calculate the
// probability of reaching F
// at time T after starting
// from S
function findProbability(G, N, F, S, T)
{
    // Declaring the DP table
    var P = Array.from(Array(N+1), ()=> Array(T+1).fill(0))

    // Probability of being at S
    // at t = 0 is 1.0
    P[S][0] = 1.0;

    // Filling the DP table
    // in bottom-up manner
    for (var i = 1; i <= T; ++i)
        for (var j = 1; j <= N; ++j)
            G[j].forEach(k => {

                P[j][i] += k[1] * P[k[0]][i - 1];
            });

    return P[F][T];
}

// Driver code
// Adjacency list
var G = Array(7);
// Building the graph
// The edges have been stored in the row
// corresponding to their end-point
G[1] = [ [ 2, 0.09 ] ];
G[2] = [ [ 1, 0.23 ], [ 6, 0.62 ] ];
G[3] = [ [ 2, 0.06 ] ];
G[4] = [ [ 1, 0.77 ], [ 3, 0.63 ] ];
G[5] = [ [ 4, 0.65 ], [ 6, 0.38 ] ];
G[6] = [ [ 2, 0.85 ], [ 3, 0.37 ], [ 4, 0.35 ], [ 5, 1.0 ] ];
// N is the number of states
var N = 6;
var S = 4, F = 2, T = 100;
document.write( "The probability of reaching " + F
     + " at time " + T + " <br>after starting from "
     + S + " is " + findProbability(G, N, F, S, T).toFixed(8));

</script>
```

**Output:** 

```
The probability of reaching 2 at time 100 
after starting from 4 is 0.284992
```

**时间复杂度**:O(N<sup>2</sup>* T)
T5】空间复杂度 : O(N * T)