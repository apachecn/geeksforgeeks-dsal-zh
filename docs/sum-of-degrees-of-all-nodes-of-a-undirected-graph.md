# 无向图所有节点的度之和

> 原文:[https://www . geesforgeks . org/无向图所有节点的度数总和/](https://www.geeksforgeeks.org/sum-of-degrees-of-all-nodes-of-a-undirected-graph/)

给定一个图的边列表，我们必须找到无向图所有节点的度之和。
**例**

![](img/b2088932180352eba20c13c87009b183.png)

**例:**

```
Input : edge list : (1, 2), (2, 3), (1, 4), (2, 4)  
Output : sum= 8
```

**蛮力逼近**
我们将把图中每个节点的度数相加，打印总和。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// returns the sum of degree of all
// the nodes in a undirected graph
int count(int edges[][2], int len, int n)
{
    int degree[n + 1] = { 0 };

    // compute the degree of each node
    for (int i = 0; i < len; i++) {

        // increase the degree of the
        // nodes
        degree[edges[i][0]]++;
        degree[edges[i][1]]++;
    }

    // calculate the sum of degree
    int sum = 0;
    for (int i = 1; i <= n; i++)
        sum += degree[i];

    return sum;
}

// main function
int main()
{
    // the edge list
    int edges[][2] = { { 1, 2 },
                       { 2, 3 },
                       { 1, 4 },
                       { 2, 4 } };
    int len = sizeof(edges) / (sizeof(int) * 2), n = 4;

    // display the result
    cout << "sum = " << count(edges, len, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // returns the sum of degree of all
    // the nodes in a undirected graph
    static int count(int edges[][], int len, int n)
    {
        int degree[] = new int[n + 1];

        // compute the degree of each node
        for (int i = 0; i < len; i++) {

            // increase the degree of the
            // nodes
            degree[edges[i][0]]++;
            degree[edges[i][1]]++;
        }

        // calculate the sum of degree
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += degree[i];

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        // the edge list
        int edges[][] = { { 1, 2 },
                          { 2, 3 },
                          { 1, 4 },
                          { 2, 4 } };
        int len = edges.length, n = 4;

        // display the result
        System.out.println("sum = " + count(edges, len, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# returns the sum of degree of all
# the nodes in a undirected graph
def count(edges, len1, n):
    degree = [0 for i in range(n + 1)]

    # compute the degree of each node
    for i in range(len1):
        # increase the degree of the
        # nodes
        degree[edges[i][0]] += 1
        degree[edges[i][1]] += 1

    # calculate the sum of degree
    sum = 0
    for i in range(1, n + 1, 1):
        sum += degree[i]

    return sum

# main function
if __name__ == '__main__':
    # the edge list
    edges = [[1, 2], [2, 3], [1, 4], [2, 4]]
    len1 = len(edges)
    n = 4

    # display the result
    print("sum =", count(edges, len1, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // returns the sum of degree of all
    // the nodes in a undirected graph
    static int count(int[][] edges, int len, int n)
    {
        int[] degree = new int[n + 1];

        // compute the degree of each node
        for (int i = 0; i < len; i++) {

            // increase the degree of the
            // nodes
            degree[edges[i][0]]++;
            degree[edges[i][1]]++;
        }

        // calculate the sum of degree
        int sum = 0;
        for (int i = 1; i <= n; i++)
            sum += degree[i];

        return sum;
    }

    // Driver code
    public static void Main()
    {
        // the edge list
        int[][] edges = new int[][] { new int[] { 1, 2 },
                                      new int[] { 2, 3 },
                                      new int[] { 1, 4 },
                                      new int[] { 2, 4 } };
        int len = edges.Length, n = 4;

        // display the result
        Console.WriteLine("sum = " + count(edges, len, n));
    }
}

// This code has been contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Returns the sum of degree of all
// the nodes in a undirected graph
function count1($edges, $len, $n)
{
    $degree = array_fill(0, $n + 1, 0);

    // compute the degree of each node
    for ($i = 0; $i < $len; $i++)
    {

        // increase the degree of the
        // nodes
        $degree[$edges[$i][0]]++;
        $degree[$edges[$i][1]]++;
    }

    // calculate the sum of degree
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum += $degree[$i];

    return $sum;
}

// Driver Code

// the edge list
$edges = array(array(1, 2),
               array(2, 3),
               array(1, 4),
               array(2, 4));
$len = count($edges);
$n = 4;

// display the result
echo "sum = " . count1($edges, $len, $n) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// returns the sum of degree of all
// the nodes in a undirected graph
function count(edges, len, n)
{
    var degree = Array(n+1).fill(0);

    // compute the degree of each node
    for (var i = 0; i < len; i++) {

        // increase the degree of the
        // nodes
        degree[edges[i][0]]++;
        degree[edges[i][1]]++;
    }

    // calculate the sum of degree
    var sum = 0;
    for (var i = 1; i <= n; i++)
        sum += degree[i];

    return sum;
}

// main function
// the edge list
var edges = [ [ 1, 2 ],
                   [ 2, 3 ],
                   [ 1, 4 ],
                   [ 2, 4 ] ];
var len = edges.length, n = 4;

// display the result
document.write( "sum = " + count(edges, len, n));

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
sum = 8
```

**有效方法**
如果我们得到一个有向图的边的个数，那么我们就可以找到这个图的度的和。让我们考虑一个没有边的图。如果我们添加一条边，我们将图的两个节点的度增加 1，因此在添加每条边后，节点的度之和增加 2，因此度之和是 2*e.

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// returns the sum of degree of all
// the nodes in a undirected graph
int count(int edges[][2], int len)
{
    return 2 * len;
}

// main function
int main()
{
    // the edge list
    int edges[][2] = { { 1, 2 },
                       { 2, 3 },
                       { 1, 4 },
                       { 2, 4 } };
    int len = sizeof(edges) / (sizeof(int) * 2);

    // display the result
    cout << "sum = " << count(edges, len) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for above approach
class GFG {

    // returns the sum of degree of all
    // the nodes in a undirected graph
    static int count(int edges[][], int len)
    {
        return 2 * len;
    }

    // Driver code
    public static void main(String[] args)
    {
        // the edge list
        int edges[][] = { { 1, 2 },
                          { 2, 3 },
                          { 1, 4 },
                          { 2, 4 } };
        int len = edges.length;

        // display the result
        System.out.println("sum = " + count(edges, len));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# returns the sum of degree of all
# the nodes in a undirected graph
def count(edges, length) :

    return 2 * length;

# Driver Code
if __name__ == "__main__" :

    # the edge list
    edges = [[ 1, 2 ],
             [ 2, 3 ],
             [ 1, 4 ],
             [ 2, 4 ]];
    length = len(edges);

    # display the result
    print("sum = ", count(edges, length));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation for above approach
using System;

class GFG {

    // returns the sum of degree of all
    // the nodes in a undirected graph
    static int count(int[, ] edges, int len)
    {
        return 2 * len;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // the edge list
        int[, ] edges = { { 1, 2 },
                          { 2, 3 },
                          { 1, 4 },
                          { 2, 4 } };
        int len = edges.GetLength(0);

        // display the result
        Console.WriteLine("sum = " + count(edges, len));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// returns the sum of degree of all
// the nodes in a undirected graph
function count1($edges, $len)
{
    return 2 * $len;
}

// Driver Code

// the edge list
$edges = array(array(1, 2),
               array(2, 3),
               array(1, 4),
               array(2, 4));
$len = sizeof($edges);

// display the result
echo "sum = " . count1($edges, $len) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// returns the sum of degree of all
// the nodes in a undirected graph
function count(edges, len)
{
    return 2 * len;
}

// main function
// the edge list
var edges = [ [ 1, 2 ],
                   [ 2, 3 ],
                   [ 1, 4 ],
                   [ 2, 4 ] ];
var len = edges.length;
// display the result
document.write( "sum = " + count(edges, len));

</script>   
```

**输出:**

```
sum = 8
```