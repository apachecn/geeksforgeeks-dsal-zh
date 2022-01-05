# 旅行推销员问题|贪婪方法

> 原文:[https://www . geeksforgeeks . org/旅行推销员-问题-贪婪-方法/](https://www.geeksforgeeks.org/travelling-salesman-problem-greedy-approach/)

给定一个 2D 矩阵**tsp【】【】**，其中每一行都有从该索引城市到所有其他城市的距离数组， **-1** 表示这两个索引城市之间不存在路径。任务是打印 TSP 周期中的最小成本。
**例:**

> **输入:**
> tsp[][] = {{-1，10，15，20}，
> {10，-1，35，25}，
> {15，35，-1，30}，
> {20，25，30，-1 } }；
> 下图为
> 
> [![](img/f13c11b6b6abf6bde87d85db87cd09b6.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/Euler12.png)
> 
> **输出:** 80
> **说明:**
> 我们正在努力寻找成本最小的路径/路线，从而达到我们一次游览所有城市并返回源城市的目的。我们实现这一目标的途径可以表示为 1 - > 2 - > 4 - > 3 - > 1。在这里，我们从第一个城市出发，一路上同样游览了所有其他城市。我们的路径/路线的成本计算如下:
> 1->2 = 10
> 2->4 = 25
> 4->3 = 30
> 3->1 = 15
> (所有成本取自给定的 2D 数组)
> 因此，总成本= 10 + 25 + 30 + 15 = 80
> **输入:**
> tsp[[]=]
> **产量:** 50

我们在[之前的帖子](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)中介绍了[旅行推销员问题](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)，并讨论了该问题的天真和动态编程解决方案。这两个解决方案都不可行。事实上，这个问题没有多项式时间的解决方案，因为这个问题是一个已知的 NP-Hard 问题。不过，有一些近似算法可以解决这个问题。
这个问题可以和[哈密顿圈问题](https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/)联系起来，在这里我们知道图中存在一个哈密顿圈，但是我们的工作是找到代价最小的圈。此外，在一个特定的 TSP 图中，可以有许多哈密顿圈，但是我们只需要输出一个满足我们要求的问题目标的哈密顿圈。
**进场:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  创建两个主要数据持有者:
    *   根据城市间距离的输入矩阵保存城市指数的列表。
    *   结果数组，其中将有所有城市，可以显示出来的控制台，以任何方式。
2.  对所有城市的给定邻接矩阵 **tsp[][]** 执行遍历，如果从当前城市到达任何城市的成本小于当前成本，则更新成本。
3.  使用上述步骤生成最小路径周期，并以最小成本返回。

下面是上述方法的实现:

## C++

```
//  C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// cost path for all the paths
void findMinRoute(vector<vector<int> > tsp)
{
    int sum = 0;
    int counter = 0;
    int j = 0, i = 0;
    int min = INT_MAX;
    map<int, int> visitedRouteList;

    // Starting from the 0th indexed
    // city i.e., the first city
    visitedRouteList[0] = 1;
    int route[tsp.size()];

    // Traverse the adjacency
    // matrix tsp[][]
    while (i < tsp.size() && j < tsp[i].size())
    {

        // Corner of the Matrix
        if (counter >= tsp[i].size() - 1)
        {
            break;
        }

        // If this path is unvisited then
        // and if the cost is less then
        // update the cost
        if (j != i && (visitedRouteList[j] == 0))
        {
            if (tsp[i][j] < min)
            {
                min = tsp[i][j];
                route[counter] = j + 1;
            }
        }
        j++;

        // Check all paths from the
        // ith indexed city
        if (j == tsp[i].size())
        {
            sum += min;
            min = INT_MAX;
            visitedRouteList[route[counter] - 1] = 1;
            j = 0;
            i = route[counter] - 1;
            counter++;
        }
    }

    // Update the ending city in array
    // from city which was last visited
    i = route[counter - 1] - 1;

    for (j = 0; j < tsp.size(); j++)
    {

        if ((i != j) && tsp[i][j] < min)
        {
            min = tsp[i][j];
            route[counter] = j + 1;
        }
    }
    sum += min;

    // Started from the node where
    // we finished as well.
    cout << ("Minimum Cost is : ");
    cout << (sum);
}

// Driver Code
int main()
{

    // Input Matrix
    vector<vector<int> > tsp = { { -1, 10, 15, 20 },
                                 { 10, -1, 35, 25 },
                                 { 15, 35, -1, 30 },
                                 { 20, 25, 30, -1 } };

    // Function Call
    findMinRoute(tsp);
}

// This code is contributed by grand_master.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class TSPGreedy {

    // Function to find the minimum
    // cost path for all the paths
    static void findMinRoute(int[][] tsp)
    {
        int sum = 0;
        int counter = 0;
        int j = 0, i = 0;
        int min = Integer.MAX_VALUE;
        List<Integer> visitedRouteList
            = new ArrayList<>();

        // Starting from the 0th indexed
        // city i.e., the first city
        visitedRouteList.add(0);
        int[] route = new int[tsp.length];

        // Traverse the adjacency
        // matrix tsp[][]
        while (i < tsp.length
               && j < tsp[i].length) {

            // Corner of the Matrix
            if (counter >= tsp[i].length - 1) {
                break;
            }

            // If this path is unvisited then
            // and if the cost is less then
            // update the cost
            if (j != i
                && !(visitedRouteList.contains(j))) {
                if (tsp[i][j] < min) {
                    min = tsp[i][j];
                    route[counter] = j + 1;
                }
            }
            j++;

            // Check all paths from the
            // ith indexed city
            if (j == tsp[i].length) {
                sum += min;
                min = Integer.MAX_VALUE;
                visitedRouteList.add(route[counter] - 1);
                j = 0;
                i = route[counter] - 1;
                counter++;
            }
        }

        // Update the ending city in array
        // from city which was last visited
        i = route[counter - 1] - 1;

        for (j = 0; j < tsp.length; j++) {

            if ((i != j) && tsp[i][j] < min) {
                min = tsp[i][j];
                route[counter] = j + 1;
            }
        }
        sum += min;

        // Started from the node where
        // we finished as well.
        System.out.print("Minimum Cost is : ");
        System.out.println(sum);
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Input Matrix
        int[][] tsp = {
            { -1, 10, 15, 20 },
            { 10, -1, 35, 25 },
            { 15, 35, -1, 30 },
            { 20, 25, 30, -1 }
        };

        // Function Call
        findMinRoute(tsp);
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class TSPGreedy{

// Function to find the minimum
// cost path for all the paths
static void findMinRoute(int[,] tsp)
{
    int sum = 0;
    int counter = 0;
    int j = 0, i = 0;
    int min = int.MaxValue;

    List<int> visitedRouteList = new List<int>();

    // Starting from the 0th indexed
    // city i.e., the first city
    visitedRouteList.Add(0);
    int[] route = new int[tsp.Length];

    // Traverse the adjacency
    // matrix tsp[,]
    while (i < tsp.GetLength(0) &&
           j < tsp.GetLength(1))
    {

        // Corner of the Matrix
        if (counter >= tsp.GetLength(0) - 1)
        {
            break;
        }

        // If this path is unvisited then
        // and if the cost is less then
        // update the cost
        if (j != i &&
            !(visitedRouteList.Contains(j)))
        {
            if (tsp[i, j] < min)
            {
                min = tsp[i, j];
                route[counter] = j + 1;
            }
        }
        j++;

        // Check all paths from the
        // ith indexed city
        if (j == tsp.GetLength(0))
        {
            sum += min;
            min = int.MaxValue;
            visitedRouteList.Add(route[counter] - 1);

            j = 0;
            i = route[counter] - 1;
            counter++;
        }
    }

    // Update the ending city in array
    // from city which was last visited
    i = route[counter - 1] - 1;

    for(j = 0; j < tsp.GetLength(0); j++)
    {
        if ((i != j) && tsp[i, j] < min)
        {
            min = tsp[i, j];
            route[counter] = j + 1;
        }
    }
    sum += min;

    // Started from the node where
    // we finished as well.
    Console.Write("Minimum Cost is : ");
    Console.WriteLine(sum);
}

// Driver Code
public static void Main(String[] args)
{

    // Input Matrix
    int[,] tsp = { { -1, 10, 15, 20 },
                   { 10, -1, 35, 25 },
                   { 15, 35, -1, 30 },
                   { 20, 25, 30, -1 } };

    // Function call
    findMinRoute(tsp);
}
}

// This code is contributed by Amit Katiyar
```

**Output**

```
Minimum Cost is : 80
```

***时间复杂度:**O(N<sup>2</sup>* log<sub>2</sub>N)*
***辅助空间:** O(N)*