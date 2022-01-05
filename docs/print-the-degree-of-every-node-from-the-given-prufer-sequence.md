# 打印给定普鲁弗序列中每个节点的度数

> 原文:[https://www . geeksforgeeks . org/print-给定 prufer 序列中每个节点的度数/](https://www.geeksforgeeks.org/print-the-degree-of-every-node-from-the-given-prufer-sequence/)

给定一个[普鲁弗序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是找出普鲁弗序列所构成的树的所有节点的度。
**例:**

```
Input: arr[] = {4, 1, 3, 4} 
Output: 2 1 2 3 1 1

The tree is:
2----4----3----1----5
     |
     6 

Input: arr[] = {1, 2, 2} 
Output: 2 3 1 1 1
```

一种简单的方法是使用普鲁夫序列创建树，然后找到所有节点的度。
**高效方法:**创建一个大小为 2 的**度【】**数组，大于 prufer 序列的长度，因为如果 **N** 是节点数，那么 prufer 序列的长度就是**N–2**。首先，用 **1** 填充度数数组。迭代普鲁弗序列，增加每个元素在度表中的出现频率。这种方法之所以有效，是因为普鲁弗序列中一个节点的频率比树中的度数少一个。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the degrees of every
// node in the tree made by
// the given Prufer sequence
void printDegree(int prufer[], int n)
{
    int node = n + 2;

    // Hash-table to mark the
    // degree of every node
    int degree[n + 2 + 1];

    // Initially let all the degrees be 1
    for (int i = 1; i <= node; i++)
        degree[i] = 1;

    // Increase the count of the degree
    for (int i = 0; i < n; i++)
        degree[prufer[i]]++;

    // Print the degree of every node
    for (int i = 1; i <= node; i++) {
        cout << degree[i] << " ";
    }
}

// Driver code
int main()
{
    int a[] = { 4, 1, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    printDegree(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to print the degrees of every
    // node in the tree made by
    // the given Prufer sequence
    static void printDegree(int prufer[], int n)
    {
        int node = n + 2;

        // Hash-table to mark the
        // degree of every node
        int[] degree = new int[n + 2 + 1];

        // Initially let all the degrees be 1
        for (int i = 1; i <= node; i++)
        {
            degree[i] = 1;
        }

        // Increase the count of the degree
        for (int i = 0; i < n; i++)
        {
            degree[prufer[i]]++;
        }

        // Print the degree of every node
        for (int i = 1; i <= node; i++)
        {
            System.out.print(degree[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {4, 1, 3, 4};
        int n = a.length;
        printDegree(a, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the degrees of
# every node in the tree made by
# the given Prufer sequence
def printDegree(prufer, n):

    node = n + 2

    # Hash-table to mark the
    # degree of every node
    degree = [1] * (n + 2 + 1)

    # Increase the count of the degree
    for i in range(0, n):
        degree[prufer[i]] += 1

    # Print the degree of every node
    for i in range(1, node+1): 
        print(degree[i], end = " ")

# Driver code
if __name__ == "__main__":

    a = [4, 1, 3, 4]
    n = len(a)
    printDegree(a, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the degrees of every
// node in the tree made by
// the given Prufer sequence
static void printDegree(int []prufer, int n)
{
    int node = n + 2;

    // Hash-table to mark the
    // degree of every node
    int[] degree = new int[n + 2 + 1];

    // Initially let all the degrees be 1
    for (int i = 1; i <= node; i++)
    {
        degree[i] = 1;
    }

    // Increase the count of the degree
    for (int i = 0; i < n; i++)
    {
        degree[prufer[i]]++;
    }

    // Print the degree of every node
    for (int i = 1; i <= node; i++)
    {
        Console.Write(degree[i] + " ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int []a = {4, 1, 3, 4};
    int n = a.Length;
    printDegree(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to print the degrees of every
    // node in the tree made by
    // the given Prufer sequence
    function printDegree(prufer , n)
    {
        var node = n + 2;

        // Hash-table to mark the
        // degree of every node
        var degree = Array(n + 2 + 1).fill(0);

        // Initially let all the degrees be 1
        for (i = 1; i <= node; i++) {
            degree[i] = 1;
        }

        // Increase the count of the degree
        for (i = 0; i < n; i++) {
            degree[prufer[i]]++;
        }

        // Print the degree of every node
        for (i = 1; i <= node; i++) {
            document.write(degree[i] + " ");
        }
    }

    // Driver code

        var a = [ 4, 1, 3, 4 ];
        var n = a.length;
        printDegree(a, n);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
2 1 2 3 1 1
```