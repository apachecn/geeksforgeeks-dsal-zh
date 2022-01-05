# 用火车找到到达目的地的最小成本

> 原文:[https://www . geeksforgeeks . org/find-到达目的地的最低成本-每个站点单向连接/](https://www.geeksforgeeks.org/find-the-minimum-cost-to-reach-a-destination-where-every-station-is-connected-in-one-direction/)

一列火车的路线上有 N 个车站。火车从 0 站开往 N-1 站。给出所有车站对(I，j)的票价，其中 j 大于 I。找出到达目的地的最小费用。
考虑以下示例:

```
Input: 
cost[N][N] = { {0, 15, 80, 90},
              {INF, 0, 40, 50},
              {INF, INF, 0, 70},
              {INF, INF, INF, 0}
             };
There are 4 stations and cost[i][j] indicates cost to reach j 
from i. The entries where j < i are meaningless.

Output:
The minimum cost is 65
The minimum cost can be obtained by first going to station 1 
from 0\. Then from station 1 to station 3.
```

从 0 到 N-1 的最小代价可以递归地写成如下:

```
minCost(0, N-1) = MIN { cost[0][n-1],  
                        cost[0][1] + minCost(1, N-1),  
                        minCost(0, 2) + minCost(2, N-1), 
                        ........, 
                        minCost(0, N-2) + cost[N-2][n-1] } 
```

下面是上面递归公式的实现。

## C++

```
// A naive recursive solution to find min cost path from station 0
// to station N-1
#include<iostream>
#include<climits>
using namespace std;

// infinite value
#define INF INT_MAX

// Number of stations
#define N 4

// A C++ recursive function to find the shortest path from
// source 's' to destination 'd'.
int minCostRec(int cost[][N], int s, int d)
{
    // If source is same as destination
    // or destination is next to source
    if (s == d || s+1 == d)
      return cost[s][d];

    // Initialize min cost as direct ticket from
    // source 's' to destination 'd'.
    int min = cost[s][d];

    // Try every intermediate vertex to find minimum
    for (int i = s+1; i<d; i++)
    {
        int c = minCostRec(cost, s, i) +
                minCostRec(cost, i, d);
        if (c < min)
           min = c;
    }
    return min;
}

// This function returns the smallest possible cost to
// reach station N-1 from station 0\. This function mainly
// uses minCostRec().
int minCost(int cost[][N])
{
    return minCostRec(cost, 0, N-1);
}

// Driver program to test above function
int main()
{
    int cost[N][N] = { {0, 15, 80, 90},
                      {INF, 0, 40, 50},
                      {INF, INF, 0, 70},
                      {INF, INF, INF, 0}
                    };
    cout << "The Minimum cost to reach station "
          << N << " is " << minCost(cost);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java naive recursive solution to find min cost path from station 0
// to station N-1
class shortest_path
{

    static int INF = Integer.MAX_VALUE,N = 4;
    // A recursive function to find the shortest path from
    // source 's' to destination 'd'.
    static int minCostRec(int cost[][], int s, int d)
    {
        // If source is same as destination
        // or destination is next to source
        if (s == d || s+1 == d)
          return cost[s][d];

        // Initialize min cost as direct ticket from
        // source 's' to destination 'd'.
        int min = cost[s][d];

        // Try every intermediate vertex to find minimum
        for (int i = s+1; i<d; i++)
        {
            int c = minCostRec(cost, s, i) +
                    minCostRec(cost, i, d);
            if (c < min)
               min = c;
        }
        return min;
    }

    // This function returns the smallest possible cost to
    // reach station N-1 from station 0\. This function mainly
    // uses minCostRec().
    static int minCost(int cost[][])
    {
        return minCostRec(cost, 0, N-1);
    }

    public static void main(String args[])
    {
        int cost[][] = { {0, 15, 80, 90},
                      {INF, 0, 40, 50},
                      {INF, INF, 0, 70},
                      {INF, INF, INF, 0}
                    };
        System.out.println("The Minimum cost to reach station "+ N+
                                               " is "+minCost(cost));
    }

}/* This code is contributed by Rajat Mishra */
```

## 计算机编程语言

```
# Python program to find min cost path
# from station 0 to station N-1

global N
N = 4
def minCostRec(cost, s, d):

    if s == d or s+1 == d:
        return cost[s][d]

    min = cost[s][d]

    for i in range(s+1, d):
        c = minCostRec(cost,s, i) + minCostRec(cost, i, d)
        if c < min:
            min = c
    return min

def minCost(cost):
    return minCostRec(cost, 0, N-1)
cost = [ [0, 15, 80, 90],
         [float("inf"), 0, 40, 50],
         [float("inf"), float("inf"), 0, 70],
         [float("inf"), float("inf"), float("inf"), 0]
        ]
print "The Minimum cost to reach station %d is %d" % \
                                    (N, minCost(cost))

# This code is contributed by Divyanshu Mehta
```

## C#

```
// A C# naive recursive solution to find min
// cost path from station 0 to station N-1
using System;

class GFG {

    static int INF = int.MaxValue, N = 4;

    // A recursive function to find the
    // shortest path from source 's' to
    // destination 'd'.
    static int minCostRec(int [,]cost, int s, int d)
    {

        // If source is same as destination
        // or destination is next to source
        if (s == d || s + 1 == d)
        return cost[s,d];

        // Initialize min cost as direct
        // ticket from source 's' to
        // destination 'd'.
        int min = cost[s,d];

        // Try every intermediate vertex to
        // find minimum
        for (int i = s + 1; i < d; i++)
        {
            int c = minCostRec(cost, s, i) +
                       minCostRec(cost, i, d);

            if (c < min)
            min = c;
        }

        return min;
    }

    // This function returns the smallest
    // possible cost to reach station N-1
    // from station 0\. This function mainly
    // uses minCostRec().
    static int minCost(int [,]cost)
    {
        return minCostRec(cost, 0, N-1);
    }

    // Driver code
    public static void Main()
    {
        int [,]cost = { {0, 15, 80, 90},
                        {INF, 0, 40, 50},
                        {INF, INF, 0, 70},
                        {INF, INF, INF, 0} };
        Console.WriteLine("The Minimum cost to"
                         + " reach station "+ N
                        + " is "+minCost(cost));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP naive recursive solution to find min cost path from station 0
// to station N-1
// infinite value

$INF= PHP_INT_MAX ;

// Number of stations
 $N = 4;

// A recursive function to find the shortest path from
// source 's' to destination 'd'.
function  minCostRec($cost, $s, $d)
{
    // If source is same as destination
    // or destination is next to source
    if ($s == $d || $s+1 == $d)
    return $cost[$s][$d];

    // Initialize min cost as direct ticket from
    // source 's' to destination 'd'.
$min = $cost[$s][$d];

    // Try every intermediate vertex to find minimum
    for ($i = $s+1; $i<$d; $i++)
    {
         $c = minCostRec($cost, $s, $i) +
                minCostRec($cost, $i, $d);
        if ($c < $min)
        $min = $c;
    }
    return $min;
}

// This function returns the smallest possible cost to
// reach station N-1 from station 0\. This function mainly
// uses minCostRec().
function  minCost($cost)
{
     global $N;
    return minCostRec($cost, 0, $N-1);
}

// Driver program to test above function
    $cost = array(array(0, 15, 80, 90),
                array(INF, 0, 40, 50),
                array(INF, INF, 0, 70),
                    array(INF, INF, INF, 0)
                    );
    echo "The Minimum cost to reach station ",
        $N , " is " , minCost($cost);

?>
```

## java 描述语言

```
<script>
    // A Javascript naive recursive solution to find min cost path from station 0 to station N-1   
    let INF = Number.MAX_VALUE,N = 4;

    // A recursive function to find the shortest path from
    // source 's' to destination 'd'.
    function minCostRec(cost, s, d)
    {

        // If source is same as destination
        // or destination is next to source
        if (s == d || s+1 == d)
          return cost[s][d];

        // Initialize min cost as direct ticket from
        // source 's' to destination 'd'.
        let min = cost[s][d];

        // Try every intermediate vertex to find minimum
        for (let i = s+1; i<d; i++)
        {
            let c = minCostRec(cost, s, i) +
                    minCostRec(cost, i, d);
            if (c < min)
               min = c;
        }
        return min;
    }

    // This function returns the smallest possible cost to
    // reach station N-1 from station 0\. This function mainly
    // uses minCostRec().
    function minCost(cost)
    {
        return minCostRec(cost, 0, N-1);
    }

    let cost = [ [0, 15, 80, 90],
                  [INF, 0, 40, 50],
                  [INF, INF, 0, 70],
                  [INF, INF, INF, 0]
                  ];
    document.write("The Minimum cost to reach station "+ N+
                       " is "+minCost(cost));

// This code is contributed by decode2207.
</script>
```

**输出:**

```
The Minimum cost to reach station 4 is 65
```

上述实现的时间复杂度是指数级的，因为它尝试了从 0 到 N-1 的所有可能路径。上述解决方案多次解决了相同的子问题(可以通过绘制 minCostPathRec(0，5)的递归树看出)。
既然这个问题同时具有动态规划问题的性质((见[这个](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[这个](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。像其他典型的[动态规划(DP)问题一样，](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)通过存储子问题的解并以自下而上的方式解决问题，可以避免相同子问题的重新计算。
一种动态编程解决方案是创建一个 2D 表，并使用上面给出的递归公式填充该表。该解决方案所需的额外空间为 O(N <sup>2</sup> )，时间复杂度为 O(N <sup>3</sup> )
我们可以使用 O(N)个额外空间和 O(N <sup>2</sup> )个时间来解决这个问题。这个想法是基于这样一个事实，即给定的输入矩阵是一个有向无环图。DAG 中的最短路径可以使用下面文章中讨论的方法来计算。
[有向无环图中的最短路径](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)
与上面提到的帖子相比，我们在这里需要做的工作更少，因为我们知道图的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。这里顶点的拓扑排序是 0，1，…，N-1。以下是拓扑排序已知后的想法。
下面代码中的想法是首先计算站点 1 的最小成本，然后计算站点 2 的最小成本，依此类推。这些成本存储在数组 dist[0…N-1]中。
1)车站 0 的最小成本为 0，即 dist[0] = 0
2)车站 1 的最小成本为成本[0][1]，即 dist[1] =成本[0][1]
3)车站 2 的最小成本为以下两者中的最小值。
a)距离[0] +成本[0][2]
b)距离[1] +成本[1][2]
3)车站 3 的最小成本为以下三项中的最小值。
a) dist[0] +成本[0][3]
b) dist[1] +成本[1][3]
c) dist[2] +成本[2][3]
同样，dist[4]，dist[5]，… dist[N-1]也是这样计算的。
以下是上述思路的实现。

## C++

```
// A Dynamic Programming based solution to find min cost
// to reach station N-1 from station 0.
#include<iostream>
#include<climits>
using namespace std;

#define INF INT_MAX
#define N 4

// This function returns the smallest possible cost to
// reach station N-1 from station 0.
int minCost(int cost[][N])
{
    // dist[i] stores minimum cost to reach station i
    // from station 0.
    int dist[N];
    for (int i=0; i<N; i++)
       dist[i] = INF;
    dist[0] = 0;

    // Go through every station and check if using it
    // as an intermediate station gives better path
    for (int i=0; i<N; i++)
       for (int j=i+1; j<N; j++)
          if (dist[j] > dist[i] + cost[i][j])
             dist[j] = dist[i] + cost[i][j];

    return dist[N-1];
}

// Driver program to test above function
int main()
{
    int cost[N][N] = { {0, 15, 80, 90},
                      {INF, 0, 40, 50},
                      {INF, INF, 0, 70},
                      {INF, INF, INF, 0}
                    };
    cout << "The Minimum cost to reach station "
          << N << " is " << minCost(cost);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Dynamic Programming based solution to find min cost
// to reach station N-1 from station 0.
class shortest_path
{

    static int INF = Integer.MAX_VALUE,N = 4;
    // A recursive function to find the shortest path from
    // source 's' to destination 'd'.

    // This function returns the smallest possible cost to
    // reach station N-1 from station 0.
    static int minCost(int cost[][])
    {
        // dist[i] stores minimum cost to reach station i
        // from station 0.
        int dist[] = new int[N];
        for (int i=0; i<N; i++)
           dist[i] = INF;
        dist[0] = 0;

        // Go through every station and check if using it
        // as an intermediate station gives better path
        for (int i=0; i<N; i++)
           for (int j=i+1; j<N; j++)
              if (dist[j] > dist[i] + cost[i][j])
                 dist[j] = dist[i] + cost[i][j];

        return dist[N-1];
    }

    public static void main(String args[])
    {
        int cost[][] = { {0, 15, 80, 90},
                      {INF, 0, 40, 50},
                      {INF, INF, 0, 70},
                      {INF, INF, INF, 0}
                    };
        System.out.println("The Minimum cost to reach station "+ N+
                                              " is "+minCost(cost));
    }

}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# A Dynamic Programming based
# solution to find min cost
# to reach station N-1
# from station 0.

INF = 2147483647
N = 4

# This function returns the
# smallest possible cost to
# reach station N-1 from station 0.
def minCost(cost):

    # dist[i] stores minimum
    # cost to reach station i
    # from station 0.
    dist=[0 for i in range(N)]
    for i in range(N):
        dist[i] = INF
    dist[0] = 0

    # Go through every station
    # and check if using it
    # as an intermediate station
    # gives better path
    for i in range(N):
        for j in range(i+1,N):
            if (dist[j] > dist[i] + cost[i][j]):
                dist[j] = dist[i] + cost[i][j]

    return dist[N-1]

# Driver program to
# test above function

cost= [ [0, 15, 80, 90],
            [INF, 0, 40, 50],
            [INF, INF, 0, 70],
            [INF, INF, INF, 0]]

print("The Minimum cost to reach station ",
           N," is ",minCost(cost))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// A Dynamic Programming based solution
// to find min cost to reach station N-1
// from station 0.
using System;

class GFG {

    static int INF = int.MaxValue, N = 4;
    // A recursive function to find the
    // shortest path from source 's' to
    // destination 'd'.

    // This function returns the smallest
    // possible cost to reach station N-1
    // from station 0.
    static int minCost(int [,]cost)
    {

        // dist[i] stores minimum cost
        // to reach station i from
        // station 0.
        int []dist = new int[N];

        for (int i = 0; i < N; i++)
            dist[i] = INF;

        dist[0] = 0;

        // Go through every station and check
        // if using it as an intermediate
        // station gives better path
        for (int i = 0; i < N; i++)
            for (int j = i + 1; j < N; j++)
                if (dist[j] > dist[i] + cost[i,j])
                    dist[j] = dist[i] + cost[i,j];

        return dist[N-1];
    }

    public static void Main()
    {
        int [,]cost = { {0, 15, 80, 90},
                        {INF, 0, 40, 50},
                        {INF, INF, 0, 70},
                        {INF, INF, INF, 0} };
        Console.WriteLine("The Minimum cost to"
                        + " reach station "+ N
                       + " is "+minCost(cost));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based solution to find min cost
// to reach station N-1 from station 0.

$INF =PHP_INT_MAX;
$N = 4;

// This function returns the smallest possible cost to
// reach station N-1 from station 0.
function  minCost($cost)
{
global $INF;
global $N;

    // dist[i] stores minimum cost to reach station i
    // from station 0.
     $dist[$N]=array();
    for ($i=0; $i<$N; $i++)
    $dist[$i] = $INF;
    $dist[0] = 0;

    // Go through every station and check if using it
    // as an intermediate station gives better path
    for ($i=0; $i<$N; $i++)
    for ( $j=$i+1; $j<$N; $j++)
        if ($dist[$j] > $dist[$i] + $cost[$i][$j])
            $dist[$j] = $dist[$i] + $cost[$i][$j];

    return $dist[$N-1];
}

// Driver program to test above function

    $cost =array(array(0, 15, 80, 90),
            array(INF, 0, 40, 50),
            array(INF, INF, 0, 70),
            array(INF, INF, INF, 0));
    echo  "The Minimum cost to reach station ",
        $N , " is ",minCost($cost);

?>
```

## java 描述语言

```
<script>
    // A Dynamic Programming based solution
    // to find min cost to reach station N-1
    // from station 0.

    let INF = Number.MAX_VALUE, N = 4;
    // A recursive function to find the
    // shortest path from source 's' to
    // destination 'd'.

    // This function returns the smallest
    // possible cost to reach station N-1
    // from station 0.
    function minCost(cost)
    {

        // dist[i] stores minimum cost
        // to reach station i from
        // station 0.
        let dist = new Array(N);
        dist.fill(0);

        for (let i = 0; i < N; i++)
            dist[i] = INF;

        dist[0] = 0;

        // Go through every station and check
        // if using it as an intermediate
        // station gives better path
        for (let i = 0; i < N; i++)
            for (let j = i + 1; j < N; j++)
                if (dist[j] > dist[i] + cost[i][j])
                    dist[j] = dist[i] + cost[i][j];

        return dist[N-1];
    }

    let cost = [ [0, 15, 80, 90],
                  [INF, 0, 40, 50],
                  [INF, INF, 0, 70],
                  [INF, INF, INF, 0] ];
    document.write("The Minimum cost to"
                      + " reach station "+ N
                      + " is "+minCost(cost));

</script>
```

输出:

```
The Minimum cost to reach station 4 is 65
```

本文由 **Udit Gupta** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。