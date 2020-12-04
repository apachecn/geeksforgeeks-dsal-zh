# 在给定图表

中所有周期的计数，没有任何内部周期

> 原文： [https://www.geeksforgeeks.org/count-of-all-cycles-without-any-inner-cycle-in-a-given-graph/](https://www.geeksforgeeks.org/count-of-all-cycles-without-any-inner-cycle-in-a-given-graph/)

给定**无向图**，该图由编号为 **[0，N-1]** 和`E`边的`N`个顶点组成。 周期数，以使一个周期的任何顶点子集不会形成另一个周期。

**范例**：[

> **输入**：N = 2，E = 2，边沿= [{0，1}，{1，0}]
> **输出**：1
> **说明 **：。
> 两个顶点之间仅存在一个循环。
> 
> ![](img/72e78a4333147a554a50c9fe986c549c.png)
> 
> **输入**：N = 6，E = 9，边线= [{0，1}，{1，2}，{0，2}，{3，0}，{3，2}，{ 4，1}，{4，2}，{5，1}，{5，0}]]
> **输出**：4
> **说明**：
> 可能的周期如下图所示：
> 
> ![Example 2 Image](img/59f7bac8b026367b6d6801a3bc50f005.png)
> 
> 不考虑诸如 5-> 0-> 2-> 1-> 5 之类的循环，因为它包含内部循环{5-> 0-> 1}和{0-> 1-> 2}。

**方法**：

由于 V 顶点需要 V 边以形成 1 个周期，因此可以使用以下公式表示所需的周期数：

```
(Edges - Vertices) + 1

```

**插图**：，

> N = 6，E = 9，边= [{0，1}，{1，2}，{0，2}，{3，0}，{3，2}，{4，1}，{4， 2}，{5，1}，{5，0}]]
> 循环数= 9 – 6 + 1 = 4
> 图中的 4 个循环为：
> {5，0，1} ，{0，1，2}，{3，0，2}和{1，2，4}。

此公式还涵盖单个顶点可能具有自环的情况。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation for the
// above approach.

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of required cycles
int numberOfCycles(int N, int E,
                   int edges[][2])
{
    vector<int> graph[N];
    for (int i = 0; i < E; i++) {
        graph[edges[i][0]]
            .push_back(edges[i][1]);
        graph[edges[i][1]]
            .push_back(edges[i][0]);
    }

    // Return the number of cycles
    return (E - N) + 1;
}

// Driver Code
int main()
{
    int N = 6;
    int E = 9;
    int edges[][2] = { { 0, 1 },
                       { 1, 2 },
                       { 2, 0 },
                       { 5, 1 },
                       { 5, 0 },
                       { 3, 0 },
                       { 3, 2 },
                       { 4, 2 },
                       { 4, 1 } };
    int k = numberOfCycles(N, E,
                           edges);

    cout << k << endl;
    return 0;
}

```

## Java

```java

// Java implementation for the
// above approach.
import java.util.*;

class GFG{

// Function to return the
// count of required cycles
static int numberOfCycles(int N, int E,
                          int edges[][])
{
    @SuppressWarnings("unchecked")
    Vector<Integer> []graph = new Vector[N];
    for(int i = 0; i < N; i++)
        graph[i] = new Vector<Integer>();

    for(int i = 0; i < E; i++)
    {
        graph[edges[i][0]].add(edges[i][1]);
        graph[edges[i][1]].add(edges[i][0]);
    }

    // Return the number of cycles
    return (E - N) + 1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;
    int E = 9;
    int edges[][] = { { 0, 1 },
                      { 1, 2 },
                      { 2, 0 },
                      { 5, 1 },
                      { 5, 0 },
                      { 3, 0 },
                      { 3, 2 },
                      { 4, 2 },
                      { 4, 1 } };

    int k = numberOfCycles(N, E, edges);

    System.out.print(k + "\n");
}
}

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# implementation for the
// above approach.
using System;
using System.Collections.Generic;
class GFG{

// Function to return the
// count of required cycles
static int numberOfCycles(int N, int E,
                          int [,]edges)
{

    List<int> []graph = new List<int>[N];
    for(int i = 0; i < N; i++)
        graph[i] = new List<int>();

    for(int i = 0; i < E; i++)
    {
        graph[edges[i, 0]].Add(edges[i, 1]);
        graph[edges[i, 1]].Add(edges[i, 0]);
    }

    // Return the number of cycles
    return (E - N) + 1;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 6;
    int E = 9;
    int [,]edges = { { 0, 1 }, { 1, 2 },
                     { 2, 0 }, { 5, 1 },
                     { 5, 0 }, { 3, 0 },
                     { 3, 2 }, { 4, 2 },
                     { 4, 1 } };

    int k = numberOfCycles(N, E, edges);

    Console.Write(k + "\n");
}
}

// This code is contributed by Rohit_ranjan

```

**Output:** 

```
4

```

**时间复杂度**：O（E）

**辅助空间**：`O(N)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。