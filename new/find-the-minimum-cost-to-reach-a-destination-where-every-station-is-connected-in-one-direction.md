# 查找使用火车到达目的地的最低费用

> 原文： [https://www.geeksforgeeks.org/find-the-minimum-cost-to-reach-a-destination-where-every-station-is-connected-in-one-direction/](https://www.geeksforgeeks.org/find-the-minimum-cost-to-reach-a-destination-where-every-station-is-connected-in-one-direction/)

火车路线上有 N 个车站。 火车从车站 0 到 N-1。 在 j 大于 i 的情况下，给出所有一对车站（i，j）的车票成本。 找到到达目的地的最低费用。

考虑以下示例：

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

从 0 到 N-1 的最小成本可以递归写成：

```
minCost(0, N-1) = MIN { cost[0][n-1],  
                        cost[0][1] + minCost(1, N-1),  
                        minCost(0, 2) + minCost(2, N-1), 
                        ........, 
                        minCost(0, N-2) + cost[N-2][n-1] } 
```

以下是上述递归公式的实现。

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

```cs

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

// This code is contributed by Sam007\. 

```

## 的 PHP

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

**输出**：

```
The Minimum cost to reach station 4 is 65
```

上述实现的时间复杂度是指数的，因为它尝试了从 0 到 N-1 的所有可能路径。 上述解决方案多次解决了相同的 subrpoblems（可以通过为 minCostPathRec（0，5）绘制递归树来看到。
由于此问题具有动态编程问题的两个属性（（请参见[此](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[ 与其他典型的[动态编程（DP）问题一样，通过存储子问题的解决方案并以自下而上的方式解决问题，可以避免相同子问题的](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)重新计算。

一种动态编程解决方案是创建 2D 表并使用上述给定的递归公式填充表。 该解决方案所需的额外空间为 O（N <sup>2</sup> ），时间复杂度为 O（N <sup>3</sup> ）

我们可以使用 O（N）个额外空间和 O（N <sup>2</sup> ）时间来解决此问题。 该想法基于以下事实：给定的输入矩阵是有向无环图（DAG）。 DAG 中的最短路径可以使用以下文章中讨论的方法来计算。

[有向无环图](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/)中的最短路径

与上面提到的帖子相比，我们在这里需要做的工作更少，因为我们知道该图的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。 此处顶点的拓扑排序为 0、1，...，N-1。 一旦知道了拓扑排序，以下就是这个想法。

以下代码中的想法是首先计算站点 1 的最低成本，然后计算站点 2 的最低成本，依此类推。 这些成本存储在数组 dist [0…N-1]中。

1）站点 0 的最低成本为 0，即 dist [0] = 0

2）站点 1 的最低成本为 cost [0] [1]，即 di​​st [1] = cost [0] [1]

3）站点 2 的最低成本是以下两个中的最小值。
a）dist [0] + cost [0] [2]
b）dist [1] + cost [1] [2]

3）站点 3 的最低成本是以下三个的最小值。
a）dist [0] + cost [0] [3]
b）dist [1] + cost [1] [3]
c）dist [2] + cost [2] [3 ]

类似地，计算 dist [4]，dist [5]，…dist [N-1]。

以下是上述想法的实现。

## C++

```cpp

// A Dynamic Programming based solution to find min cost 
// to reach station N-1 from station 0\. 
#include<iostream> 
#include<climits> 
using namespace std; 

#define INF INT_MAX 
#define N 4 

// This function returns the smallest possible cost to 
// reach station N-1 from station 0\. 
int minCost(int cost[][N]) 
{ 
    // dist[i] stores minimum cost to reach station i 
    // from station 0\. 
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