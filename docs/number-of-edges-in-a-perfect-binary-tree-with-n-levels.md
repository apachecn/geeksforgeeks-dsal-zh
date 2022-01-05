# N 级完美二叉树的边数

> 原文:[https://www . geesforgeks . org/n 级完美二叉树边数/](https://www.geeksforgeeks.org/number-of-edges-in-a-perfect-binary-tree-with-n-levels/)

给定一个正整数 **N** ，任务是找到一个具有 **N** 级的完美二叉树的边数。
**例:**

```
Input: N = 2
Output: 2
  1
 / \
2   3

Input: N = 3
Output: 6
     1
   /    \
  2      3
 / \    /  \
4   5  6    7
```

**方法:**可以观察到对于 **N = 1，2，3，…** 的值，将形成一个系列为 **0，2，6，14，30，62，…** ，其 **N <sup>第</sup>T9】项为**2<sup>N</sup>–2**。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of edges in an n-level
// perfect binary tree
int cntEdges(int n)
{
    int edges = pow(2, n) - 2;
    return edges;
}

// Driver code
int main()
{
    int n = 4;

    cout << cntEdges(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of edges in an n-level
// perfect binary tree
static int cntEdges(int n)
{
    int edges = (int)Math.pow(2, n) - 2;
    return edges;
}

// Driver code
public static void main(String[] args)
{
    int n = 4;

    System.out.println(cntEdges(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of edges in an n-level
# perfect binary tree
def cntEdges(n) :

    edges = 2 ** n - 2;

    return edges;

# Driver code
if __name__ == "__main__" :

    n = 4;

    print(cntEdges(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the count
// of edges in an n-level
// perfect binary tree
static int cntEdges(int n)
{
    int edges = (int)Math.Pow(2, n) - 2;
    return edges;
}

// Driver code
public static void Main(String[] args)
{
    int n = 4;

    Console.Write(cntEdges(n));
}
}

// This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of edges in an n-level
// perfect binary tree
function cntEdges(n)
{
    var edges = Math.pow(2, n) - 2;
    return edges;
}

// Driver code
var n = 4;
document.write(cntEdges(n));

</script>
```

**Output:** 

```
14
```