# 打印具有最大和最小度数的节点

> 原文:[https://www . geesforgeks . org/print-nodes-having-max-and-minimum-degrees/](https://www.geeksforgeeks.org/print-nodes-having-maximum-and-minimum-degrees/)

给定一个有 **N** 个节点的无向图，任务是打印具有最小和最大度数的节点。
**例:**

```
Input:
1-----2
|     |
3-----4
Output:
Nodes with maximum degree : 1 2 3 4 
Nodes with minimum degree : 1 2 3 4 
Every node has a degree of 2.

Input:
    1
   / \
  2   3
 /
4
Output:
Nodes with maximum degree : 1 2 
Nodes with minimum degree : 3 4 
```

**逼近:**对于无向图来说，节点的度就是入射到它的边数，所以每个节点的度可以通过统计它在边列表中的出现频率来计算。因此，方法是使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)从边列表中计算每个顶点的频率，并使用该图找到具有最大和最小度数的节点。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the nodes having
// maximum and minimum degree
void minMax(int edges[][2], int len, int n)
{

    // Map to store the degrees of every node
    map<int, int> m;

    for (int i = 0; i < len; i++) {

        // Storing the degree for each node
        m[edges[i][0]]++;
        m[edges[i][1]]++;
    }

    // maxi and mini variables to store
    // the maximum and minimum degree
    int maxi = 0;
    int mini = n;

    for (int i = 1; i <= n; i++) {
        maxi = max(maxi, m[i]);
        mini = min(mini, m[i]);
    }

    // Printing all the nodes with maximum degree
    cout << "Nodes with maximum degree : ";
    for (int i = 1; i <= n; i++) {
        if (m[i] == maxi)
            cout << i << " ";
    }
    cout << endl;

    // Printing all the nodes with minimum degree
    cout << "Nodes with minimum degree : ";
    for (int i = 1; i <= n; i++) {
        if (m[i] == mini)
            cout << i << " ";
    }
}

// Driver code
int main()
{

    // Count of nodes and edges
    int n = 4, m = 6;

    // The edge list
    int edges[][2] = { { 1, 2 },
                       { 1, 3 },
                       { 1, 4 },
                       { 2, 3 },
                       { 2, 4 },
                       { 3, 4 } };

    minMax(edges, m, 4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to print the nodes having
// maximum and minimum degree
static void minMax(int edges[][], int len, int n)
{

    // Map to store the degrees of every node
    HashMap<Integer,
            Integer> m = new HashMap<Integer,
                                     Integer>();

    for (int i = 0; i < len; i++)
    {

        // Storing the degree for each node
        if(m.containsKey(edges[i][0]))
        {
            m.put(edges[i][0], m.get(edges[i][0]) + 1);
        }
        else
        {
            m.put(edges[i][0], 1);
        }
        if(m.containsKey(edges[i][1]))
        {
            m.put(edges[i][1], m.get(edges[i][1]) + 1);
        }
        else
        {
            m.put(edges[i][1], 1);
        }
    }

    // maxi and mini variables to store
    // the maximum and minimum degree
    int maxi = 0;
    int mini = n;

    for (int i = 1; i <= n; i++)
    {
        maxi = Math.max(maxi, m.get(i));
        mini = Math.min(mini, m.get(i));
    }

    // Printing all the nodes with maximum degree
    System.out.print("Nodes with maximum degree : ");
    for (int i = 1; i <= n; i++)
    {
        if (m.get(i) == maxi)
            System.out.print(i + " ");
    }
    System.out.println();

    // Printing all the nodes with minimum degree
    System.out.print("Nodes with minimum degree : ");
    for (int i = 1; i <= n; i++)
    {
        if (m.get(i) == mini)
            System.out.print(i + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    // Count of nodes and edges
    int n = 4, m = 6;

    // The edge list
    int edges[][] = {{ 1, 2 }, { 1, 3 },
                     { 1, 4 }, { 2, 3 },
                     { 2, 4 }, { 3, 4 }};

    minMax(edges, m, 4);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the nodes having
# maximum and minimum degree
def minMax(edges, leng, n) :

    # Map to store the degrees of every node
    m = {};

    for i in range(leng) :
        m[edges[i][0]] = 0;
        m[edges[i][1]] = 0;

    for i in range(leng) :

        # Storing the degree for each node
        m[edges[i][0]] += 1;
        m[edges[i][1]] += 1;

    # maxi and mini variables to store
    # the maximum and minimum degree
    maxi = 0;
    mini = n;

    for i in range(1, n + 1) :
        maxi = max(maxi, m[i]);
        mini = min(mini, m[i]);

    # Printing all the nodes
    # with maximum degree
    print("Nodes with maximum degree : ",
                                end = "")

    for i in range(1, n + 1) :
        if (m[i] == maxi) :
            print(i, end = " ");

    print()

    # Printing all the nodes
    # with minimum degree
    print("Nodes with minimum degree : ",
                                end = "")

    for i in range(1, n + 1) :
        if (m[i] == mini) :
            print(i, end = " ");

# Driver code
if __name__ == "__main__" :

    # Count of nodes and edges
    n = 4; m = 6;

    # The edge list
    edges = [[ 1, 2 ], [ 1, 3 ],
             [ 1, 4 ], [ 2, 3 ],
             [ 2, 4 ], [ 3, 4 ]];

    minMax(edges, m, 4);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to print the nodes having
// maximum and minimum degree
static void minMax(int [,]edges, int len, int n)
{

    // Map to store the degrees of every node
    Dictionary<int, int> m = new Dictionary<int, int>();

    for (int i = 0; i < len; i++)
    {

        // Storing the degree for each node
        if(m.ContainsKey(edges[i, 0]))
        {
            m[edges[i, 0]] = m[edges[i, 0]] + 1;
        }
        else
        {
            m.Add(edges[i, 0], 1);
        }
        if(m.ContainsKey(edges[i, 1]))
        {
            m[edges[i, 1]] = m[edges[i, 1]] + 1;
        }
        else
        {
            m.Add(edges[i, 1], 1);
        }
    }

    // maxi and mini variables to store
    // the maximum and minimum degree
    int maxi = 0;
    int mini = n;

    for (int i = 1; i <= n; i++)
    {
        maxi = Math.Max(maxi, m[i]);
        mini = Math.Min(mini, m[i]);
    }

    // Printing all the nodes with maximum degree
    Console.Write("Nodes with maximum degree : ");
    for (int i = 1; i <= n; i++)
    {
        if (m[i] == maxi)
            Console.Write(i + " ");
    }
    Console.WriteLine();

    // Printing all the nodes with minimum degree
    Console.Write("Nodes with minimum degree : ");
    for (int i = 1; i <= n; i++)
    {
        if (m[i] == mini)
            Console.Write(i + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Count of nodes and edges
    int m = 6;

    // The edge list
    int [,]edges = {{ 1, 2 }, { 1, 3 },
                    { 1, 4 }, { 2, 3 },
                    { 2, 4 }, { 3, 4 }};

    minMax(edges, m, 4);
}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
Nodes with maximum degree : 1 2 3 4 
Nodes with minimum degree : 1 2 3 4
```

**时间复杂度** : O(M*logN + N)。
**辅助空间** : O(N)。