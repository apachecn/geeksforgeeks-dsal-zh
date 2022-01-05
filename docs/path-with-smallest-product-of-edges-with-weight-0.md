# 边与权重乘积最小的路径> 0

> 原文:[https://www . geeksforgeeks . org/权重为 0 的最小边积路径/](https://www.geeksforgeeks.org/path-with-smallest-product-of-edges-with-weight-0/)

给定一个具有 **N** 个节点和 **E** 条边的有向图，其中每条边的权重为 **> 0** ，同时给定一个源 **S** 和一个目的地 **D** 。任务是找到从 **S** 到 **D** 边积最小的路径。如果 **S** 到 **D** 之间没有路径，则打印 **-1** 。

**示例:**

> **输入:** N = 3，E = 3，边= {{1，2}，0.5}，{ { 1，3}，1.9}，{{2，3}，3}}，S = 1，D = 3
> **输出:** 1.5
> **解释:**
> 最短路径为 1- > 2- > 3
> 取值 0.5*3 = 1.5
> 
> **输入:** N = 3，E = 3，边= { { 1，2}，0.5}，{{2，3}，0.5}，{{3，1}，0.5}}，S = 1，D = 3
> **输出:**检测到循环

**方法:**想法是使用[贝尔曼福特算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)。这是因为[迪克斯特拉算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/)不能在这里使用，因为它只适用于非负边。这是因为当值在[0-1]之间相乘时，乘积无限减小，最终返回 0。
此外，需要检测周期，因为如果存在一个周期，则该周期的乘积将无限期地将乘积减小到 0，并且乘积将趋于 0。为了简单起见，我们将报告这样的周期。
可以按照以下步骤计算结果:

1.  初始化数组， **dis[]** ，初始值为“inf”，dis[S]为 1。
2.  从 1–N-1 运行一个循环。对于图中的每条边:
    *   dis[edge . second]= min(dis[edge . second]，dis[edge . first]*权重(edge))
3.  对图中的每条边运行另一个循环，如果任何边以(dis[edge . second]> dis[edge . first]* weight(edge))退出，则检测到循环。
4.  如果距离[d]在无穷大，返回 **-1** ，否则返回**距离[d]** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach.
#include <bits/stdc++.h>
using namespace std;

double inf = std::
    numeric_limits<double>::infinity();

// Function to return the smallest
// product of edges
double bellman(int s, int d,
               vector<pair<pair<int, int>,
                           double> >
                   ed,
               int n)
{
    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Array to store distances
    double dis[n + 1];

    // Initialising the array
    for (int i = 1; i <= n; i++)
        dis[i] = inf;
    dis[s] = 1;

    // Bellman ford algorithm
    for (int i = 0; i < n - 1; i++)
        for (auto it : ed)
            dis[it.first.second] = min(dis[it.first.second],
                                       dis[it.first.first]
                                           * it.second);

    // Loop to detect cycle
    for (auto it : ed) {
        if (dis[it.first.second]
            > dis[it.first.first] * it.second)
            return -2;
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
int main()
{

    int n = 3;
    vector<pair<pair<int, int>, double> > ed;

    // Input edges
    ed = { { { 1, 2 }, 0.5 },
           { { 1, 3 }, 1.9 },
           { { 2, 3 }, 3 } };

    // Source and Destination
    int s = 1, d = 3;

    // Bellman ford
    double get = bellman(s, d, ed, n);

    if (get == -2)
        cout << "Cycle Detected";
    else
        cout << get;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.ArrayList;
import java.util.Arrays;
import java.util.PriorityQueue;

class Pair<K, V>
{
    K first;
    V second;

    public Pair(K first, V second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG{

static final float inf = Float.POSITIVE_INFINITY;

// Function to return the smallest
// product of edges
static float bellman(int s, int d,
                     ArrayList<Pair<Pair<Integer,
                                         Integer>, Float>> ed,
                     int n)
{

    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Array to store distances
    float[] dis = new float[n + 1];

    // Initialising the array
    Arrays.fill(dis, inf);
    dis[s] = 1;

    // Bellman ford algorithm
    for(int i = 0; i < n - 1; i++)
        for(Pair<Pair<Integer, Integer>, Float> it : ed)
            dis[it.first.second] = Math.min(dis[it.first.second],
                                            dis[it.first.first] *
                                                it.second);

    // Loop to detect cycle
    for(Pair<Pair<Integer, Integer>, Float> it : ed)
    {
        if (dis[it.first.second] >
            dis[it.first.first] *
                it.second)
            return -2;
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    // Input edges
    ArrayList<Pair<Pair<Integer,
                        Integer>, Float>> ed = new ArrayList<>(
            Arrays.asList(
                      new Pair<Pair<Integer, Integer>, Float>(
                           new Pair<Integer, Integer>(1, 2), 0.5f),
                    new Pair<Pair<Integer, Integer>, Float>(
                         new Pair<Integer, Integer>(1, 3), 1.9f),
                    new Pair<Pair<Integer, Integer>, Float>(
                         new Pair<Integer, Integer>(2, 3), 3f)));

    // Source and Destination
    int s = 1, d = 3;

    // Bellman ford
    float get = bellman(s, d, ed, n);

    if (get == -2)
        System.out.println("Cycle Detected");
    else
        System.out.println(get);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach.
import sys

inf = sys.maxsize;

# Function to return the smallest
# product of edges
def bellman(s, d, ed, n) :

    # If the source is equal
    # to the destination
    if (s == d) :
        return 0;

    # Array to store distances
    dis = [0]*(n + 1);

    # Initialising the array
    for i in range(1, n + 1) :
        dis[i] = inf;

    dis[s] = 1;

    # Bellman ford algorithm
    for i in range(n - 1) :
        for it in ed :
            dis[it[1]] = min(dis[it[1]], dis[it[0]] * ed[it]);

    # Loop to detect cycle
    for it in ed :
        if (dis[it[1]] > dis[it[0]] * ed[it]) :
            return -2;

    # Returning final answer
    if (dis[d] == inf) :
        return -1;
    else :
        return dis[d];

# Driver code
if __name__ == "__main__" :

    n = 3;

    # Input edges
    ed = { ( 1, 2 ) : 0.5 ,
        ( 1, 3 ) : 1.9 ,
        ( 2, 3 ) : 3 };

    # Source and Destination
    s = 1; d = 3;

    # Bellman ford
    get = bellman(s, d, ed, n);

    if (get == -2) :
        print("Cycle Detected");
    else :
        print(get);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;
using System.Collections.Generic;

public class GFG{

public static float inf = 1000000000;

// Function to return the smallest
// product of edges
public static float bellman(int s, int d,
                     List<KeyValuePair<KeyValuePair<int,
                                         int>, float>> ed,
                     int n)
{

    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Array to store distances
    float[] dis = Enumerable.Repeat(inf, n+1).ToArray();

    dis[s] = 1;

    // Bellman ford algorithm
    for(int i = 0; i < n - 1; i++)
        foreach(KeyValuePair<KeyValuePair<int, int>, float> it in ed)
            dis[it.Key.Value] = Math.Min(dis[it.Key.Value],
                                            dis[it.Key.Key] *
                                                it.Value);

    // Loop to detect cycle
    foreach(KeyValuePair<KeyValuePair<int, int>, float> it in ed)
    {
        if (dis[it.Key.Value] >
            dis[it.Key.Key] *
                it.Value)
            return -2;
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
public static void Main(string[] args)
{
    int n = 3;

    // Input edges
    List<KeyValuePair<KeyValuePair<int,
                        int>, float>> ed = new List<KeyValuePair<KeyValuePair<int,
                        int>, float>>(){
                      new KeyValuePair<KeyValuePair<int, int>, float>(
                           new KeyValuePair<int, int>(1, 2), 0.5f),
                    new KeyValuePair<KeyValuePair<int, int>, float>(
                         new KeyValuePair<int, int>(1, 3), 1.9f),
                    new KeyValuePair<KeyValuePair<int, int>, float>(
                         new KeyValuePair<int, int>(2, 3), 3f)};

    // Source and Destination
    int s = 1, d = 3;

    // Bellman ford
    float get = bellman(s, d, ed, n);

    if (get == -2)
        Console.Write("Cycle Detected");
    else
        Console.Write(get);
}
}

// This code is contributed by rrrtnx.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach.

var inf = 1000000000;

// Function to return the smallest
// product of edges
function bellman(s, d, ed, n)
{
    // If the source is equal
    // to the destination
    if (s == d)
        return 0;

    // Array to store distances
    var dis = Array(n+1).fill(inf);

    dis[s] = 1;

    // Bellman ford algorithm
    for (var i = 0; i < n - 1; i++)
    {
        for(var j =0 ; j< ed.length; j++)
        {
            dis[ed[j][0][1]] = Math.min(dis[ed[j][0][1]],
                                       dis[ed[j][0][0]]
                                           * ed[j][1]);
        }
    }

    // Loop to detect cycle
    for (var it in ed) {

        if (dis[it[0][1]]
            > dis[it[0][0]] * it[1])
            return -2;
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
var n = 3;
var ed;
// Input edges
ed = [ [ [ 1, 2 ], 0.5 ],
       [ [ 1, 3 ], 1.9 ],
       [ [ 2, 3 ], 3 ] ];
// Source and Destination
var s = 1, d = 3;
// Bellman ford
var get = bellman(s, d, ed, n);
if (get == -2)
    document.write( "Cycle Detected");
else
    document.write( get);

</script>
```

**Output:** 

```
1.5
```

**时间复杂度:**O(E * V)
T3】辅助空间 : O(V)。