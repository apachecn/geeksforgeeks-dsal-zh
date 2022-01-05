# 将 X 转换为 Y 所需的最小步骤，其中二进制矩阵表示可能的转换

> 原文:[https://www . geesforgeks . org/convert-x-to-y-其中二进制矩阵表示可能的转换/](https://www.geeksforgeeks.org/minimum-steps-required-to-convert-x-to-y-where-a-binary-matrix-represents-the-possible-conversions/)

给定大小为 NxN 的二进制矩阵，其中 1 表示数字 I 可以转换为 j，0 表示它不能转换为。还给出了两个数字 X( <n y="" the="" task="" is="" to="" find="" minimum="" number="" of="" steps="" required="" convert="" x="" y.="" if="" there="" no="" such="" way="" possible="" print="">**)示例:**</n> 

```
Input: 
{{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 1, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1}
{ 0, 0, 0, 1, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 1, 0, 0, 0, 0, 0, 0, 0, 0}
{ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1}}

X = 2, Y = 3 
Output: 2 
Convert 2 -> 4 -> 3, which is the minimum way possible. 

Input:
{{ 0, 0, 0, 0}
{ 0, 0, 0, 1}
{ 0, 0, 0, 0}
{ 0, 1, 0, 0}}

X = 1, Y = 2
Output: -1 
```

**方法:**这个问题是 [Floyd-warshall 算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)的一个变种，在 I 和 j 之间有一个权重为 1 的边，即 **mat[i][j]==1** ，否则它们没有边，我们可以像在 Floyd-warshall 中那样给边赋值为无穷大。求解矩阵，如果不是无穷大，则返回 **dp[i][j]** 。如果无限，返回 **-1** ，这意味着它们之间没有可能的路径。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define INF 99999
#define size 10

int findMinimumSteps(int mat[size][size], int x, int y, int n)
{
    // dist[][] will be the output matrix that
    // will finally have the shortest
    // distances between every pair of numbers
    int dist[n][n], i, j, k;

    // Initially same as mat
    for (i = 0; i < n; i++) {
        for (j = 0; j < n; j++) {
            if (mat[i][j] == 0)
                dist[i][j] = INF;
            else
                dist[i][j] = 1;

            if (i == j)
                dist[i][j] = 1;
        }
    }

    // Add all numbers one by one to the set
    // of intermediate numbers. Before start of
    // an iteration, we have shortest distances
    // between all pairs of numbers such that the
    // shortest distances consider only the numbers
    // in set {0, 1, 2, .. k-1} as intermediate numbers.
    // After the end of an iteration, vertex no. k is
    // added to the set of intermediate numbers and
    // the set becomes {0, 1, 2, .. k}
    for (k = 0; k < n; k++) {

        // Pick all numbers as source one by one
        for (i = 0; i < n; i++) {

            // Pick all numbers as destination for the
            // above picked source
            for (j = 0; j < n; j++) {

                // If number k is on the shortest path from
                // i to j, then update the value of dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    // If no path
    if (dist[x][y] < INF)
        return dist[x][y];
    else
        return -1;
}

// Driver Code
int main()
{

    int mat[size][size] = { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                            { 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 },
                            { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 } };

    int x = 2, y = 3;

    cout << findMinimumSteps(mat, x, y, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    static int INF=99999;

    static int findMinimumSteps(int mat[][], int x, int y, int n)
    {
        // dist[][] will be the output matrix that
        // will finally have the shortest
        // distances between every pair of numbers
        int i, j, k;
        int [][] dist= new int[n][n];

        // Initially same as mat
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (mat[i][j] == 0)
                    dist[i][j] = INF;
                else
                    dist[i][j] = 1;

                if (i == j)
                    dist[i][j] = 1;
            }
        }

        // Add all numbers one by one to the set
        // of intermediate numbers. Before start of
        // an iteration, we have shortest distances
        // between all pairs of numbers such that the
        // shortest distances consider only the numbers
        // in set {0, 1, 2, .. k-1} as intermediate numbers.
        // After the end of an iteration, vertex no. k is
        // added to the set of intermediate numbers and
        // the set becomes {0, 1, 2, .. k}
        for (k = 0; k < n; k++) {

            // Pick all numbers as source one by one
            for (i = 0; i < n; i++) {

                // Pick all numbers as destination for the
                // above picked source
                for (j = 0; j < n; j++) {

                    // If number k is on the shortest path from
                    // i to j, then update the value of dist[i][j]
                    if (dist[i][k] + dist[k][j] < dist[i][j])
                        dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }

        // If no path
        if (dist[x][y] < INF)
            return dist[x][y];
        else
            return -1;
    }

    // Driver Code
    public static void main(String []args)
    {

        int [][] mat =  { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 } };

        int x = 2, y = 3;
        int size=mat.length;

        System.out.println( findMinimumSteps(mat, x, y, size));
    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Pyton3 implementation of the above approach

INF = 99999
size = 10

def findMinimumSteps(mat, x, y, n):

    # dist[][] will be the output matrix
    # that will finally have the shortest
    # distances between every pair of numbers
    dist = [[0 for i in range(n)]
               for i in range(n)]
    i, j, k = 0, 0, 0

    # Initially same as mat
    for i in range(n):
        for j in range(n):
            if (mat[i][j] == 0):
                dist[i][j] = INF
            else:
                dist[i][j] = 1

            if (i == j):
                dist[i][j] = 1

    # Add all numbers one by one to the set
    # of intermediate numbers. Before start
    # of an iteration, we have shortest distances
    # between all pairs of numbers such that the
    # shortest distances consider only the numbers
    # in set {0, 1, 2, .. k-1} as intermediate
    # numbers. After the end of an iteration, vertex
    # no. k is added to the set of intermediate
    # numbers and the set becomes {0, 1, 2, .. k}
    for k in range(n):

        # Pick all numbers as source one by one
        for i in range(n):

            # Pick all numbers as destination
            # for the above picked source
            for j in range(n):

                # If number k is on the shortest path from
                # i to j, then update the value of dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j]):
                    dist[i][j] = dist[i][k] + dist[k][j]

    # If no path
    if (dist[x][y] < INF):
        return dist[x][y]
    else:
        return -1

# Driver Code
mat = [[ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 ],
       [ 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 ],
       [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 ]]

x, y = 2, 3

print(findMinimumSteps(mat, x, y, size))

# This code is contributed by Mohit kumar 29
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{

    static int INF=99999;

    static int findMinimumSteps(int [,]mat, int x, int y, int n)
    {
        // dist[][] will be the output matrix that
        // will finally have the shortest
        // distances between every pair of numbers
        int i, j, k;
        int [,] dist= new int[n,n];

        // Initially same as mat
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (mat[i,j] == 0)
                    dist[i,j] = INF;
                else
                    dist[i,j] = 1;

                if (i == j)
                    dist[i,j] = 1;
            }
        }

        // Add all numbers one by one to the set
        // of intermediate numbers. Before start of
        // an iteration, we have shortest distances
        // between all pairs of numbers such that the
        // shortest distances consider only the numbers
        // in set {0, 1, 2, .. k-1} as intermediate numbers.
        // After the end of an iteration, vertex no. k is
        // added to the set of intermediate numbers and
        // the set becomes {0, 1, 2, .. k}
        for (k = 0; k < n; k++) {

            // Pick all numbers as source one by one
            for (i = 0; i < n; i++) {

                // Pick all numbers as destination for the
                // above picked source
                for (j = 0; j < n; j++) {

                    // If number k is on the shortest path from
                    // i to j, then update the value of dist[i][j]
                    if (dist[i,k] + dist[k,j] < dist[i,j])
                        dist[i,j] = dist[i,k] + dist[k,j];
                }
            }
        }

        // If no path
        if (dist[x,y] < INF)
            return dist[x,y];
        else
            return -1;
    }

    // Driver Code
    public static void Main()
    {

        int [,] mat = { { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                        { 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 } };

        int x = 2, y = 3;
        int size = mat.GetLength(0) ;

        Console.WriteLine( findMinimumSteps(mat, x, y, size));
    }
    // This code is contributed by Ryuga
}
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach  
    var INF=99999;

    function findMinimumSteps(mat , x , y , n)
    {
        // dist will be the output matrix that
        // will finally have the shortest
        // distances between every pair of numbers
        var i, j, k;
        var  dist= Array(n).fill().map(()=>Array(n).fill(0));

        // Initially same as mat
        for (i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (mat[i][j] == 0)
                    dist[i][j] = INF;
                else
                    dist[i][j] = 1;

                if (i == j)
                    dist[i][j] = 1;
            }
        }

        // Add all numbers one by one to the set
        // of intermediate numbers. Before start of
        // an iteration, we have shortest distances
        // between all pairs of numbers such that the
        // shortest distances consider only the numbers
        // in set {0, 1, 2, .. k-1} as intermediate numbers.
        // After the end of an iteration, vertex no. k is
        // added to the set of intermediate numbers and
        // the set becomes {0, 1, 2, .. k}
        for (k = 0; k < n; k++) {

            // Pick all numbers as source one by one
            for (i = 0; i < n; i++) {

                // Pick all numbers as destination for the
                // above picked source
                for (j = 0; j < n; j++) {

                    // If number k is on the
                    // shortest path from
                    // i to j, then update the
                    // value of dist[i][j]
                    if (dist[i][k] + dist[k][j] < dist[i][j])
                        dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }

        // If no path
        if (dist[x][y] < INF)
            return dist[x][y];
        else
            return -1;
    }

    // Driver Code

        var  mat =  [[ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 1, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 ],
                        [ 0, 0, 0, 1, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 1, 0, 0, 0, 0, 0, 0, 0, 0 ],
                        [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 1 ] ];

        var x = 2, y = 3;
        var size=mat.length;

        document.write( findMinimumSteps(mat, x, y, size));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2
```