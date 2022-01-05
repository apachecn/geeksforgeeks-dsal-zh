# 计算完整图形中边总数的程序

> 原文:[https://www . geeksforgeeks . org/program-to-find-完整图中的总边数/](https://www.geeksforgeeks.org/program-to-find-total-number-of-edges-in-a-complete-graph/)

给定图的 N 个顶点。任务是找到一个由 N 个顶点组成的*完整图*中可能的边的总数。
**完全图:**完全图是每对顶点都由一条边连接的图。
**示例** :

```
Input : N = 3
Output : Edges = 3

Input : N = 5
Output : Edges = 10
```

由 N 个顶点组成的完整图中可能的边的总数可以表示为，

> **由 N 个顶点组成的完整图的边总数**=(N *(N-1))/2

**例 1:** 下面是一个 N = 5 个顶点的完全图。

![](img/d25ffc569c864782538221a3cdd2ac22.png)

上述完全图的边总数= 10 = (5)*(5-1)/2。
以下是上述思路的实现:

## C++

```
// C++ implementation to find the
// number of edges in a complete graph

#include <bits/stdc++.h>
using namespace std;

// Function to find the total number of
// edges in a complete graph with N vertices
int totEdge(int n)
{
    int result = 0;

    result = (n * (n - 1)) / 2;

    return result;
}

// Driver Code
int main()
{
    int n = 6;

    cout << totEdge(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// number of edges in a complete graph

class GFG {

// Function to find the total number of
// edges in a complete graph with N vertices
static int totEdge(int n)
{
    int result = 0;

    result = (n * (n - 1)) / 2;

    return result;
}

    // Driver Code
    public static void main(String []args)
    {
        int n = 6;
        System.out.println(totEdge(n));
    }

}
```

## 蟒蛇 3

```
# Python 3 implementation to 
# find the number of edges
# in a complete graph

# Function to find the total
# number of edges in a complete
# graph with N vertices
def totEdge(n) :

    result = (n * (n - 1)) // 2

    return result

# Driver Code
if __name__ == "__main__" :

    n = 6

    print(totEdge(n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# implementation to find
// the number of edges in a
// complete graph
using System;

class GFG
{

// Function to find the total
// number of edges in a complete
// graph with N vertices
static int totEdge(int n)
{
    int result = 0;

    result = (n * (n - 1)) / 2;

    return result;
}

// Driver Code
public static void Main()
{
    int n = 6;
    Console.Write(totEdge(n));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the number of edges in a
// complete graph

// Function to find the total
// number of edges in a complete
// graph with N vertices
function totEdge($n)
{
    $result = 0;

    $result = ($n * ($n - 1)) / 2;

    return $result;
}

// Driver Code
$n = 6;
echo totEdge($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// number of edges in a complete graph

// Function to find the total number of
// edges in a complete graph with N vertices
function totEdge(n)
{
    var result = 0;

    result = (n * (n - 1)) / 2;

    return result;
}

// Driver Code
var n = 6;
document.write( totEdge(n));

</script>
```

**Output:** 

```
15
```