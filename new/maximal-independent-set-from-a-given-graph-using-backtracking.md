# 使用回溯

从给定图获得的最大独立集

> 原文： [https://www.geeksforgeeks.org/maximal-independent-set-from-a-given-graph-using-backtracking/](https://www.geeksforgeeks.org/maximal-independent-set-from-a-given-graph-using-backtracking/)

给定具有`V`顶点和`E`边的**无向图**，任务是打印所有**独立集**并找到 **最大独立集**。

> **[独立集](https://www.geeksforgeeks.org/mathematics-independent-sets-covering-and-matching/)** 是一组顶点，因此该组中的任何两个顶点之间都没有直接的边。

> **[最大独立集](https://www.geeksforgeeks.org/largest-independent-set-problem-dp-26/)** 是顶点数最多的独立集。

**注意**：对于一个给定的图形，可以有多个独立和最大独立集。

**示例**：

> **输入**：
> V = 3，E = 0
> 图：
> ![](img/fbfbd47a09dd9db832129c27a4d723b5.png)
> **输出**：
> {} {1} {1 2} {1 2 3} {1 3} {2} {2 3} {3}
> {1 2 3}
> **说明**：
> 第一行代表所有可能 给定图的独立集合。 第二行具有给定图可能的最大独立集。
> 
> **输入**：
> V = 4，E = 4
> 图：
> ![](img/e702ad1cb17be9b5c95d5c5ee728c0ac.png)
> **输出**：
> {} {1} {1 3} {2} {2 4} {3} {4}
> {1 3} {2 4}

**方法**：
的想法是使用[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)解决该问题。 在每一步中，我们都需要检查当前节点是否具有与我们独立集中已存在的任何节点的直接边缘。 如果没有，我们可以将其添加到我们的独立集中，然后对所有节点递归地重复相同的过程。

> **插图**：
> 第一个示例的递归树：
> ![](img/bd06f707d21cacfdb7f99a795e5d2882.png)
> 在上面的回溯树中，我们将仅选择在添加**安全节点[[** 将集合保持为独立集合。

下面是上述方法的实现：

## CPP

```

// C++ Program to print the 
// independent sets and 
// maximal independent sets 
// of the given graph 

#include <bits/stdc++.h> 
using namespace std; 

// To store all the independent 
// sets of the graph 
set<set<int> > independentSets; 

// To store all maximal independent 
// sets in the graph 
set<set<int> > maximalIndependentSets; 

map<pair<int, int>, int> edges; 
vector<int> vertices; 

// Function to print all independent sets 
void printAllIndependentSets() 
{ 
    for (auto iter : independentSets) { 
        cout << "{ "; 
        for (auto iter2 : iter) { 
            cout << iter2 << " "; 
        } 
        cout << "}"; 
    } 
    cout << endl; 
} 

// Function to extract all 
// maximal independent sets 
void printMaximalIndependentSets() 
{ 
    int maxCount = 0; 
    int localCount = 0; 
    for (auto iter : independentSets) { 

        localCount = 0; 
        for (auto iter2 : iter) { 
            localCount++; 
        } 
        if (localCount > maxCount) 
            maxCount = localCount; 
    } 
    for (auto iter : independentSets) { 

        localCount = 0; 
        set<int> tempMaximalSet; 

        for (auto iter2 : iter) { 
            localCount++; 
            tempMaximalSet.insert(iter2); 
        } 
        if (localCount == maxCount) 
            maximalIndependentSets 
                .insert(tempMaximalSet); 
    } 
    for (auto iter : maximalIndependentSets) { 
        cout << "{ "; 
        for (auto iter2 : iter) { 
            cout << iter2 << " "; 
        } 
        cout << "}"; 
    } 
    cout << endl; 
} 

// Function to check if a 
// node is safe node. 
bool isSafeForIndependentSet( 
    int vertex, 
    set<int> tempSolutionSet) 
{ 
    for (auto iter : tempSolutionSet) { 
        if (edges[make_pair(iter, vertex)]) { 
            return false; 
        } 
    } 
    return true; 
} 

// Recursive function to find 
// all independent sets 
void findAllIndependentSets( 
    int currV, 
    int setSize, 
    set<int> tempSolutionSet) 
{ 
    for (int i = currV; i <= setSize; i++) { 
        if (isSafeForIndependentSet( 
                vertices[i - 1], 
                tempSolutionSet)) { 
            tempSolutionSet 
                .insert(vertices[i - 1]); 
            findAllIndependentSets( 
                i + 1, 
                setSize, 
                tempSolutionSet); 
            tempSolutionSet 
                .erase(vertices[i - 1]); 
        } 
    } 
    independentSets 
        .insert(tempSolutionSet); 
} 

// Driver Program 
int main() 
{ 
    int V = 3, E = 0; 

    for (int i = 1; i <= V; i++) 
        vertices.push_back(i); 

    vector<pair<int, int> > inputEdges; 

    pair<int, int> edge; 
    int x, y; 
    for (int i = 0; i < E; i++) { 
        edge.first = inputEdges[i].first; 
        edge.second = inputEdges[i].second; 
        edges[edge] = 1; 
        int t = edge.first; 
        edge.first = edge.second; 
        edge.second = t; 
        edges[edge] = 1; 
    } 

    set<int> tempSolutionSet; 

    findAllIndependentSets(1, 
                           V, 
                           tempSolutionSet); 

    printAllIndependentSets(); 

    printMaximalIndependentSets(); 

    return 0; 
} 

```

**Output:**

```
{ }{ 1 }{ 1 2 }{ 1 2 3 }{ 1 3 }{ 2 }{ 2 3 }{ 3 }
{ 1 2 3 }

```

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。