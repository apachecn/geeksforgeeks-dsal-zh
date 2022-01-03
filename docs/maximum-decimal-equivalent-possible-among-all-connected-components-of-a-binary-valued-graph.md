# 二进制值图

的所有连通组件之间可能的最大十进制等效项

> 原文： [https://www.geeksforgeeks.org/maximum-decimal-equivalent-possible-among-all-connected-components-of-a-binary-valued-graph/](https://www.geeksforgeeks.org/maximum-decimal-equivalent-possible-among-all-connected-components-of-a-binary-valued-graph/)

给定**二进制值** [无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，并带有`V`顶点和`E`边，任务是在所有 图的连通组件。 可以将二进制值图视为仅将二进制数**（0 或 1）**作为顶点值。

**示例**：

> **输入**：E = 4，V = 7
> 
> ![](img/fb50e4ce31778dd68a347b016976fde7.png)
> 
> **输出**：3
> **说明**：
> 所连通组件的十进制当量如下：
> [0，1]：最大可能的十进制当量= 2 [（ 10） <sub>2</sub> ]
> [0，0，0]：最大可能的十进制当量= 2
> [1，1]：最大可能的十进制当量= 3
> 因此，最大十进制当量 所有组件的总和= 3
> 
> **输入**：E = 6，V = 10
> 
> ![](img/83927206790a724c02078daf19b731bf.png)
> 
> **输出**：8
> **说明**：
> 连通组件和十进制等效项如下：
> [1]：最大可能的十进制等效项= 2
> [0 ，0，1，0]：最大可能的十进制等效值= 8 [（1000） <sub>2</sub> ]
> [1，1，0]：最大可能的十进制等效值= 6
> [1，0 ]：最大可能的十进制等效值= 2
> 因此，所有组件的最大十进制等效值= 8

**方法**：

*   这个想法是使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来跟踪无向图中的连通组件，如[此](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)文章中所述。

*   对于每个连通组件，将存储二进制字符串并计算等效的十进制值。

*   设置一个全局最大值，该最大值与每次迭代后获得的最大十进制等效值进行比较以获得最终结果。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to find
// maximum decimal equivalent among
// all connected components

#include <bits/stdc++.h>

using namespace std;

// Function to traverse the undirected
// graph using the Depth first traversal
void depthFirst(int v, vector<int> graph[],
                vector<bool>& visited,
                vector<int>& storeChain)
{
    // Marking the visited
    // vertex as true
    visited[v] = true;

    // Store the connected chain
    storeChain.push_back(v);

    for (auto i : graph[v]) {
        if (visited[i] == false) {

            // Recursive call to
            // the DFS algorithm
            depthFirst(i, graph,
                       visited, storeChain);
        }
    }
}

// Function to return decimal
// equivalent of each connected
// component
int decimal(int arr[], int n)
{
    int zeros = 0, ones = 0;

    // Storing the respective
    // counts of 1's and 0's
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0)
            zeros++;
        else
            ones++;
    }

    // If all are zero then
    // maximum decimal equivalent
    // is also zero
    if (zeros == n)
        return 0;

    int temp = n - ones;
    int dec = 0;

    // For all the 1's, calculate
    // the decimal equivalent by
    // appropriate multiplication
    // of power of 2's
    while (ones--) {
        dec += pow(2, temp);
        temp++;
    }
    return dec;
}

// Function to find the maximum
// decimal equivalent among all
// connected components
void decimalValue(
    vector<int> graph[], int vertices,
    vector<int> values)
{
    // Initializing boolean array
    // to mark visited vertices
    vector<bool> visited(10001, false);

    // maxDeci stores the
    // maximum decimal value
    int maxDeci = INT_MIN;

    // Following loop invokes
    // DFS algorithm
    for (int i = 1; i <= vertices; i++) {
        if (visited[i] == false) {

            // Variable to hold
            // temporary length
            int sizeChain;

            // Variable to hold temporary
            // Decimal values
            int tempDeci;

            // Container to store
            // each chain
            vector<int> storeChain;

            // DFS algorithm
            depthFirst(i, graph, visited,
                       storeChain);

            // Variable to hold each
            // chain size
            sizeChain = storeChain.size();

            // Container to store values
            // of vertices of individual
            // chains
            int chainValues[sizeChain + 1];

            // Storing the values of
            // each chain
            for (int i = 0; i < sizeChain; i++) {
                int temp = values[storeChain[i] - 1];
                chainValues[i] = temp;
            }

            // Function call to find
            // decimal equivalent
            tempDeci = decimal(chainValues,
                               sizeChain);

            // Conditional to store maximum
            // value of decimal equivalent
            if (tempDeci > maxDeci) {
                maxDeci = tempDeci;
            }
        }
    }

    // Printing the decimal result
    // (global maxima)

    cout << maxDeci;
}

// Driver code
int main()
{
    // Initializing graph in the
    // form of adjacency list
    vector<int> graph[1001];

    // Defining the number of
    // edges and vertices
    int E, V;
    E = 4;
    V = 7;

    // Assigning the values
    // for each vertex of the
    // undirected graph
    vector<int> values;
    values.push_back(0);
    values.push_back(1);
    values.push_back(0);
    values.push_back(0);
    values.push_back(0);
    values.push_back(1);
    values.push_back(1);

    // Constructing the
    // undirected graph
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[4].push_back(5);
    graph[5].push_back(4);
    graph[6].push_back(7);
    graph[7].push_back(6);

    decimalValue(graph, V, values);
    return 0;
}

```

## Java

```java

// Java program to find maximum 
// decimal equivalent among all 
// connected components
import java.io.*;
import java.util.*;

class GFG{

// Function to traverse the undirected
// graph using the Depth first traversal
static void depthFirst(int v,
                       List<List<Integer>> graph,
                       boolean[] visited,
                       List<Integer> storeChain)
{

    // Marking the visited
    // vertex as true
    visited[v] = true;

    // Store the connected chain
    storeChain.add(v);

    for(int i : graph.get(v)) 
    {
        if (visited[i] == false)
        {

            // Recursive call to
            // the DFS algorithm
            depthFirst(i, graph, visited,
                       storeChain);
        }
    }
}

// Function to return decimal
// equivalent of each connected
// component
static int decimal(int arr[], int n)
{
    int zeros = 0, ones = 0;

    // Storing the respective
    // counts of 1's and 0's
    for(int i = 0; i < n; i++)
    {
        if (arr[i] == 0)
            zeros++;
        else
            ones++;
    }

    // If all are zero then maximum
    // decimal equivalent is also zero
    if (zeros == n)
        return 0;

    int temp = n - ones;
    int dec = 0;

    // For all the 1's, calculate
    // the decimal equivalent by
    // appropriate multiplication
    // of power of 2's
    while (ones > 0) 
    {
        dec += Math.pow(2, temp);
        temp++;
        ones--;
    }
    return dec;
}

// Function to find the maximum
// decimal equivalent among all
// connected components
static void decimalValue(List<List<Integer>> graph,
                         int vertices,
                         List<Integer> values)
{

    // Initializing boolean array
    // to mark visited vertices
    boolean[] visited = new boolean[10001];

    // maxDeci stores the
    // maximum decimal value
    int maxDeci = Integer.MIN_VALUE;

    // Following loop invokes
    // DFS algorithm
    for(int i = 1; i <= vertices; i++) 
    {
        if (visited[i] == false) 
        {

            // Variable to hold
            // temporary length
            int sizeChain;

            // Variable to hold temporary
            // Decimal values
            int tempDeci;

            // Container to store
            // each chain
            List<Integer> storeChain = new ArrayList<Integer>();

            // DFS algorithm
            depthFirst(i, graph, visited,
                       storeChain);

            // Variable to hold each
            // chain size
            sizeChain = storeChain.size();

            // Container to store values
            // of vertices of individual
            // chains
            int[] chainValues = new int[sizeChain + 1];

            // Storing the values of
            // each chain
            for(int j = 0; j < sizeChain; j++)
            {
                int temp = values.get(
                    storeChain.get(j) - 1);
                chainValues[j] = temp;
            }

            // Function call to find
            // decimal equivalent
            tempDeci = decimal(chainValues, 
                               sizeChain);

            // Conditional to store maximum
            // value of decimal equivalent
            if (tempDeci > maxDeci)
            {
                maxDeci = tempDeci;
            }
        }
    }

    // Printing the decimal result
    // (global maxima)
    System.out.println(maxDeci);
}

// Driver code
public static void main(String[] args)
{

    // Initializing graph in the
    // form of adjacency list
    @SuppressWarnings("unchecked")
    List<List<Integer>> graph = new ArrayList();

    for(int i = 0; i < 1001; i++)
        graph.add(new ArrayList<Integer>());

    // Defining the number
    // of edges and vertices
    int E = 4, V = 7;

    // Assigning the values for each
    // vertex of the undirected graph
    List<Integer> values = new ArrayList<Integer>();
    values.add(0);
    values.add(1);
    values.add(0);
    values.add(0);
    values.add(0);
    values.add(1);
    values.add(1);

    // Constructing the
    // undirected graph
    graph.get(1).add(2);
    graph.get(2).add(1);
    graph.get(3).add(4);
    graph.get(4).add(3);
    graph.get(4).add(5);
    graph.get(5).add(4);
    graph.get(6).add(7);
    graph.get(7).add(6);

    decimalValue(graph, V, values);
}
}

// This code is contributed by jithin

```

## Python

```py

# Python3 Program to find
# maximum decimal equivalent among
# all connected components
import sys

# Function to traverse the 
# undirected graph using 
# the Depth first traversal
def depthFirst(v, graph, 
               visited, 
               storeChain):

    # Marking the visited
    # vertex as true
    visited[v] = True;

    # Store the connected chain
    storeChain.append(v);

    for i in graph[v]:
        if (visited[i] == False):

            # Recursive call to
            # the DFS algorithm
            depthFirst(i, graph,
                       visited, 
                       storeChain);        

# Function to return decimal
# equivalent of each connected
# component
def decimal(arr, n):

    zeros = 0
    ones = 0

    # Storing the respective
    # counts of 1's and 0's
    for i in range(n):

        if (arr[i] == 0):
            zeros+=1;
        else:
            ones += 1;    

    # If all are zero then
    # maximum decimal equivalent
    # is also zero
    if (zeros == n):
        return 0;

    temp = n - ones;
    dec = 0;

    # For all the 1's, calculate
    # the decimal equivalent by
    # appropriate multiplication
    # of power of 2's
    while (ones != 0):
        ones -= 1
        dec += pow(2, temp);
        temp += 1;

    return dec;

# Function to find the maximum
# decimal equivalent among all
# connected components
def decimalValue(graph, 
                 vertices, values):

    # Initializing boolean array
    # to mark visited vertices
    visited = [False for i in range(10001)]

    # maxDeci stores the
    # maximum decimal value
    maxDeci = -sys.maxsize;

    # Following loop invokes
    # DFS algorithm
    for i in range(vertices + 1):

        if (visited[i] == False):

            # Variable to hold
            # temporary length
            sizeChain = 0;

            # Variable to hold 
            # temporary Decimal values
            tempDeci = 0;

            # Container to store
            # each chain
            storeChain = [];

            # DFS algorithm
            depthFirst(i, graph, 
                       visited,
                       storeChain);

            # Variable to hold each
            # chain size
            sizeChain = len(storeChain)

            # Container to store values
            # of vertices of individual
            # chains
            chainValues = [0 for i in range(sizeChain + 1)]

            # Storing the values of
            # each chain
            for i in range(sizeChain):            
                temp = values[storeChain[i] - 1];
                chainValues[i] = temp;            

            # Function call to find
            # decimal equivalent
            tempDeci = decimal(chainValues,
                               sizeChain);

            # Conditional to store maximum
            # value of decimal equivalent
            if (tempDeci > maxDeci):
                maxDeci = tempDeci;            

    # Printing the decimal result
    # (global maxima) 
    print(maxDeci)

if __name__ == "__main__":

    # Initializing graph in the
    # form of adjacency list
    graph = [[] for i in range(1001)]

    # Defining the number
    # of edges and vertices
    E = 4;
    V = 7;

    # Assigning the values 
    # for each vertex of 
    # the undirected graph
    values = [];
    values.append(0);
    values.append(1);
    values.append(0);
    values.append(0);
    values.append(0);
    values.append(1);
    values.append(1);

    # Constructing the 
    # undirected graph
    graph[1].append(2);
    graph[2].append(1);
    graph[3].append(4);
    graph[4].append(3);
    graph[4].append(5);
    graph[5].append(4);
    graph[6].append(7);
    graph[7].append(6);

    decimalValue(graph, V, values);

# This code is contributed by rutvik_56

```

**Output:** 

```
3

```

**复杂度分析**：

**时间复杂度**：O（V <sup>2</sup> ）

DFS 算法需要`O(V + E)`时间来运行，其中 V，E 是无向图的顶点和边。 此外，在每次迭代中都会找到十进制等效项，这需要额外的`O(V)`来计算并返回结果。 因此，整体复杂度为 **O（V <sup>2</sup> ）**

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。