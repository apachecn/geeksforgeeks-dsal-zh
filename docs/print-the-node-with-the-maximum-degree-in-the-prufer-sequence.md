# 打印 prufer 序列中度数最大的节点

> 原文:[https://www . geesforgeks . org/print-the-node-with-the-the-the-the-the-the-node-with-the-the-the-the-the-the-the-the-the-the-the-node-the-the-the-the-the-the-the-the-the-the-the](https://www.geeksforgeeks.org/print-the-node-with-the-maximum-degree-in-the-prufer-sequence/)

给定一个树的 [Prufer 序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是打印给定 Prufer 序列的树中具有最大度的节点。如果最大度数的节点很多，打印最小度数的节点。
**例:**

```
Input: a[] = {4, 1, 3, 4} 
Output: 4
The tree is:
2----4----3----1----5
     |
     6 

Input: a[] = {1, 2, 2} 
Output: 2
```

一种**简单的方法**是使用普鲁夫序列创建树，然后找到所有节点的度，然后找到其中的最大值。
**高效方法:**创建一个大小为 2 的**度【】**数组，大于普鲁弗序列的长度，因为如果 **N** 是节点数，普鲁弗序列的长度是**N–2**。首先，用 **1** 填充度数数组。迭代普鲁弗序列，增加每个元素在度表中的出现频率。这种方法之所以有效，是因为普鲁弗序列中一个节点的频率比树中的度数少一个。现在迭代度数组，找到最大频率的节点，这就是我们的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the node with
// the maximum degree in the tree
// whose Prufer sequence is given
int findMaxDegreeNode(int prufer[], int n)
{
    int nodes = n + 2;

    // Hash-table to mark the
    // degree of every node
    int degree[n + 2 + 1];

    // Initially let all the degrees be 1
    for (int i = 1; i <= nodes; i++)
        degree[i] = 1;

    // Increase the count of the degree
    for (int i = 0; i < n; i++)
        degree[prufer[i]]++;

    int maxDegree = 0;
    int node = 0;

    // Find the node with maximum degree
    for (int i = 1; i <= nodes; i++) {
        if (degree[i] > maxDegree) {
            maxDegree = degree[i];
            node = i;
        }
    }

    return node;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findMaxDegreeNode(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

    // Function to return the node with
    // the maximum degree in the tree
    // whose Prufer sequence is given
    static int findMaxDegreeNode(int prufer[], int n)
    {
        int nodes = n + 2;

        // Hash-table to mark the
        // degree of every node
        int []degree = new int[n + 2 + 1];

        // Initially let all the degrees be 1
        for (int i = 1; i <= nodes; i++)
            degree[i] = 1;

        // Increase the count of the degree
        for (int i = 0; i < n; i++)
            degree[prufer[i]]++;

        int maxDegree = 0;
        int node = 0;

        // Find the node with maximum degree
        for (int i = 1; i <= nodes; i++)
        {
            if (degree[i] > maxDegree)
            {
                maxDegree = degree[i];
                node = i;
            }
        }

        return node;
    }

    // Driver code
    public static void main (String[] args)
    {

        int []a = { 1, 2, 2 };
        int n = a.length;
        System.out.println(findMaxDegreeNode(a, n));
    }
}

// This code is contributed by ajit_00023
```

## 蟒蛇 3

```

# Python implementation of the approach

# Function to return the node with
# the maximum degree in the tree
# whose Prufer sequence is given
def findMaxDegreeNode(prufer, n):
    nodes = n + 2;

    # Hash-table to mark the
    # degree of every node
    degree = [0]*(n + 2 + 1);

    # Initially let all the degrees be 1
    for i in range(1,nodes+1):
        degree[i] = 1;

    # Increase the count of the degree
    for i in range(n):
        degree[prufer[i]]+=1;

    maxDegree = 0;
    node = 0;

    # Find the node with maximum degree
    for i in range(1,nodes+1):
        if (degree[i] > maxDegree):
            maxDegree = degree[i];
            node = i;

    return node;

# Driver code
a = [ 1, 2, 2 ];
n = len(a);
print(findMaxDegreeNode(a, n));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the node with
    // the maximum degree in the tree
    // whose Prufer sequence is given
    static int findMaxDegreeNode(int []prufer, int n)
    {
        int nodes = n + 2;

        // Hash-table to mark the
        // degree of every node
        int []degree = new int[n + 2 + 1];

        // Initially let all the degrees be 1
        for (int i = 1; i <= nodes; i++)
            degree[i] = 1;

        // Increase the count of the degree
        for (int i = 0; i < n; i++)
            degree[prufer[i]]++;

        int maxDegree = 0;
        int node = 0;

        // Find the node with maximum degree
        for (int i = 1; i <= nodes; i++)
        {
            if (degree[i] > maxDegree)
            {
                maxDegree = degree[i];
                node = i;
            }
        }

        return node;
    }

    // Driver code
    static public void Main ()
    {
        int []a = { 1, 2, 2 };
        int n = a.Length;

        Console.WriteLine(findMaxDegreeNode(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the node with
    // the maximum degree in the tree
    // whose Prufer sequence is given
    function findMaxDegreeNode(prufer, n)
    {
        let nodes = n + 2;

        // Hash-table to mark the
        // degree of every node
        let degree = new Array(n + 2 + 1);
        degree.fill(0);

        // Initially let all the degrees be 1
        for (let i = 1; i <= nodes; i++)
            degree[i] = 1;

        // Increase the count of the degree
        for (let i = 0; i < n; i++)
            degree[prufer[i]]++;

        let maxDegree = 0;
        let node = 0;

        // Find the node with maximum degree
        for (let i = 1; i <= nodes; i++)
        {
            if (degree[i] > maxDegree)
            {
                maxDegree = degree[i];
                node = i;
            }
        }

        return node;
    }

    let a = [ 1, 2, 2 ];
    let n = a.length;
    document.write(findMaxDegreeNode(a, n));

</script>
```

**Output:** 

```
2
```