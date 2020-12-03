# 等级祖先问题

> 原文： [https://www.geeksforgeeks.org/level-ancestor-problem/](https://www.geeksforgeeks.org/level-ancestor-problem/)

[级祖先问题](https://en.wikipedia.org/wiki/Level_ancestor_problem)是将给定的根树 T 预处理为数据结构的问题，该数据结构可以确定从树根到给定深度的给定节点的祖先。 这里，树中任何节点的**深度**是从树的根部到节点的最短路径上的边数。

给定树表示为具有 n 个节点和 **n-1 个边**的**无向连通图**。

解决上述查询的想法是使用**跳转指针算法**并在 **O（n log n）**时间和答案级别祖先查询中对树进行预处理。 logn）时间。 在跳转指针中，有一个从节点 N 到第 N 个第 j 个祖先的指针，对于

j = 1、2、4、8，...，依此类推。 我们将这些指针称为跳转 <sub>N</sub> [i]，其中

跳转 <sub>u</sub> [i] = LA（N，depth（N）– 2 <sup>i</sup> ）。

当要求算法处理查询时，我们使用这些跳转指针反复跳转树。 跳转次数最多为 log n，因此可以在 O（logn）时间内回答查询。

因此，我们存储每个节点的 **2 <sup>i</sup> 祖先**，并且还从树的根中找到每个节点的深度。

现在我们的任务简化为找到节点 N 的第（depth（N）– 2 <sup>i</sup> ）个祖先。让我们将 X 表示为（depth（N）– 2 <sup>i</sup> ）并让[ X 的`b`位是由 s1，s2，s3，... sb 表示的**设置位**（1）。

**X = 2 <sup>（s1）</sup> + 2 <sup>（s2）</sup> +…+ 2 <sup>（sb）</sup>**

现在的问题是如何从树的根中找到每个节点的 2 个 <sup>j</sup> 祖先以及每个节点的深度？

最初，我们知道每个节点的第 2 <sup>0</sup> 个祖先是其父节点。 我们可以递归计算第 2 个 <sup>j</sup> 个祖先。 我们知道第 2 个 <sup>j</sup> 祖先是第 2 个 <sup>j-1</sup> 祖先。 为了计算每个节点的深度，我们使用祖先矩阵。 如果我们发现第 k 个元素的根节点在第 j 个索引处存在，则该节点的深度仅为 2 <sup>j</sup> ，但如果第 k 个元素的祖先数组中不存在根节点 第 k 个元素的深度为 2 <sup>（第 k 行的最后一个非零祖先的索引）</sup> +第 k 行的最后索引处的祖先的深度。

以下是使用动态编程填充每个节点的祖先矩阵和深度的算法。 在这里，我们将根节点表示为`R`，并最初假定根节点的祖先为`0`。 我们还使用 **-1 初始化深度数组。**表示未设置当前节点的深度，我们需要找到其深度。 如果当前节点的深度不等于-1，则意味着我们已经计算出其深度。

```

we know the first ancestor of each node so we take j>=1,
For j>=1

ancstr[k][j] =  2jth ancestor of k    
             =  2j-1th ancestor of (2j-1th ancestor of k)       
             =  ancstr[ancstr[i][j-1][j-1]
                if ancstr[k][j] == R && depth[k] == -1
                   depth[k] = 2j
                else if ancstr[k][j] == -1 && depth[k] == -1
                   depth[k] = 2(j-1) + depth[ ancstr[k][j-1] ]

```

让我们通过下图了解这种算法。

![](img/f2161df24c8afd4b3ae317d895f2d1e6.png)

在给定图中，我们需要计算值为`8`的节点的第一级祖先。 首先，我们创建祖先矩阵，该矩阵存储 2 个<sup>节点的第</sup>个祖先。 现在，节点`8`的 **2 <sup>0</sup>** 的祖先是 **10** 和类似的 **2 <sup>0</sup>** 节点 **10** 的祖先是`9`，节点`9`的祖先是`1`，节点`1`的祖先是[`5`。 基于上述算法，节点 8 的第一级祖先是节点 8 的**（depth（8）-1）祖先**。我们已经预先计算了每个节点的深度，深度 8 为 5，所以我们最终需要 找到**（5-1）=节点 8 的第 4 个**祖先，它等于节点[2 <sup>1 的</sup>个祖先的 **2 <sup>1</sup> 个祖先 ]** 和 **2 <sup>1</sup> 的祖先是 **2 <sup>0</sup> 的祖先是[2 <sup>0</sup> 节点 8]。** 因此，节点[8]的[2 <sup>0</sup> 的祖先的 **2 0 的祖先**是值为`9`和[ 节点 9 的 HTG56] 2 <sup>1</sup> 祖先**是值为`5`的节点。 因此，通过这种方式，我们可以以 O（logn）时间复杂度来计算所有查询。

```

// CPP program to implement Level Ancestor Algorithm 
#include <bits/stdc++.h> 
using namespace std; 
int R = 0; 

// n -> it represent total number of nodes 
// len -> it is the maximum length of array to hold  
//          ancestor of each node. In worst case,  
// the highest value of ancestor a node can have is n-1\. 
// 2 ^ len <= n-1 
// len = O(log2n) 
int getLen(int n) 
{ 
    return (int)(log(n) / log(2)) + 1; 
} 

// ancstr represents 2D matrix to hold ancestor of node. 
// Here we pass reference of 2D matrix so that the change 
// made occur directly  to the original matrix 
// depth[] stores depth of each node 
// len is same as defined above 
// n is total nodes in graph 
// R represent root node 
void setancestor(vector<vector<int> >& ancstr, 
           vector<int>& depth, int* node, int len, int n) 
{ 
    // depth of root node is set to 0 
    depth[R] = 0; 

    // if depth of a node is -1 it means its depth  
    // is not set otherwise we have computed its depth 
    for (int j = 1; j <= len; j++) { 
        for (int i = 0; i < n; i++) { 
            ancstr[node[i]][j] = ancstr[ancstr[node[i]][j - 1]][j - 1]; 

            // if ancestor of current node is R its height is 
            //  previously not set, then its height is  2^j 
            if (ancstr[node[i]][j] == R && depth[node[i]] == -1) { 

                // set the depth of ith node 
                depth[node[i]] = pow(2, j); 
            } 

            // if ancestor of current node is 0 means it  
            // does not have root node at its 2th power  
            // on its path so its depth is 2^(index of  
            // last non zero ancestor means j-1) + depth  
            // of 2^(j-1) th ancestor 
            else if (ancstr[node[i]][j] == 0 &&  
                     node[i] != R && depth[node[i]] == -1) { 
                depth[node[i]] = pow(2, j - 1) +  
                                 depth[ancstr[node[i]][j - 1]]; 
            } 
        } 
    } 
} 

// c -> it represent child 
// p -> it represent ancestor 
// i -> it represent node number 
// p=0 means the node is root node 
// R represent root node 
// here also we pass reference of 2D matrix and depth 
// vector so that the change made occur directly to 
// the original matrix and original vector 
void constructGraph(vector<vector<int> >& ancstr, 
            int* node, vector<int>& depth, int* isNode, 
                                   int c, int p, int i) 
{ 
    // enter the node in node array 
    // it stores all the nodes in the graph 
    node[i] = c; 

    // to confirm that no child node have 2 ancestors 
    if (isNode == 0) { 
        isNode = 1; 

        // make ancestor of x as y 
        ancstr[0] = p; 

        // ifits first ancestor is root than its depth is 1 
        if (R == p) { 
            depth = 1; 
        } 
    } 
    return; 
} 

// this function will delete leaf node 
// x is node to be deleted 
void removeNode(vector<vector<int> >& ancstr,  
                    int* isNode, int len, int x) 
{ 
    if (isNode[x] == 0) 
        cout << "node does not present in graph " << endl; 
    else { 
        isNode[x] = 0; 

        // make all ancestor of node x as 0 
        for (int j = 0; j <= len; j++) { 
            ancstr[x][j] = 0; 
        } 
    } 
    return; 
} 

// x -> it represent new node to be inserted 
// p -> it represent ancestor of new node 
void addNode(vector<vector<int> >& ancstr, 
      vector<int>& depth, int* isNode, int len,  
                                 int x, int p) 
{ 
    if (isNode[x] == 1) { 
        cout << " Node is already present in array " << endl; 
        return; 
    } 
    if (isNode[p] == 0) { 
        cout << " ancestor not does not present in an array " << endl; 
        return; 
    } 

    isNode[x] = 1; 
    ancstr[x][0] = p; 

    // depth of new node is 1 + depth of its ancestor 
    depth[x] = depth[p] + 1; 
    int j = 0; 

    // while we don't reach root node 
    while (ancstr[x][j] != 0) { 
        ancstr[x][j + 1] = ancstr[ancstr[x][j]][j]; 
        j++; 
    } 

    // remaining array will fill with 0 after  
    // we find root of tree 
    while (j <= len) { 
        ancstr[x][j] = 0; 
        j++; 
    } 
    return; 
} 

// LA function to find Lth level ancestor of node x 
void LA(vector<vector<int> >& ancstr, vector<int> depth,  
                              int* isNode, int x, int L) 
{ 
    int j = 0; 
    int temp = x; 

    // to check if node is present in graph or not 
    if (isNode[x] == 0) { 
        cout << "Node is not present in graph " << endl; 
        return; 
    } 

    // we change L as depth of node x - 
    int k = depth[x] - L; 
    // int q = k; 
    // in this loop we decrease the value of k by k/2 and 
    // increment j by 1 after each iteration, and check for set bit 
    // if we get set bit then we update x with jth ancestor of x 
    // as k becomes less than or equal to zero means we 
    // reach to kth level ancestor 
    while (k > 0) { 

        // to check if last bit is 1 or not 
        if (k & 1) { 
            x = ancstr[x][j]; 
        } 

        // use of shift operator to make k = k/2  
        // after every iteration 
        k = k >> 1; 
        j++; 
    } 
    cout << L << "th level acestor of node "
               << temp << " is = " << x << endl; 

    return; 
} 

int main() 
{ 
    // n represent number of nodes 
    int n = 12; 

    // initialization of ancestor matrix 
    // suppose max range of node is up to 1000 
    // if there are 1000 nodes than also length  
    // of ancestor matrix will not exceed 10 
    vector<vector<int> > ancestor(1000, vector<int>(10)); 

    // this vector is used to store depth of each node. 
    vector<int> depth(1000); 

    // fill function is used to initialize depth with -1 
    fill(depth.begin(), depth.end(), -1); 

    // node array is used to store all nodes 
    int* node = new int[1000]; 

    // isNode is an array to check whether a 
    // node is present in graph or not 
    int* isNode = new int[1000]; 

    // memset function to initialize isNode array with 0 
    memset(isNode, 0, 1000 * sizeof(int)); 

    // function to calculate len 
    // len -> it is the maximum length of array to  
    // hold ancestor of each node. 
    int len = getLen(n); 

    // R stores root node 
    R = 2; 

    // construction of graph 
    // here 0 represent that the node is root node 
    constructGraph(ancestor, node, depth, isNode, 2, 0, 0); 
    constructGraph(ancestor, node, depth, isNode, 5, 2, 1); 
    constructGraph(ancestor, node, depth, isNode, 3, 5, 2); 
    constructGraph(ancestor, node, depth, isNode, 4, 5, 3); 
    constructGraph(ancestor, node, depth, isNode, 1, 5, 4); 
    constructGraph(ancestor, node, depth, isNode, 7, 1, 5); 
    constructGraph(ancestor, node, depth, isNode, 9, 1, 6); 
    constructGraph(ancestor, node, depth, isNode, 10, 9, 7); 
    constructGraph(ancestor, node, depth, isNode, 11, 10, 8); 
    constructGraph(ancestor, node, depth, isNode, 6, 10, 9); 
    constructGraph(ancestor, node, depth, isNode, 8, 10, 10); 

    // function to pre compute ancestor matrix 
    setancestor(ancestor, depth, node, len, n); 

    // query to get 1st level ancestor of node 8 
    LA(ancestor, depth, isNode, 8, 1); 

    // add node 12 and its ancestor is 8 
    addNode(ancestor, depth, isNode, len, 12, 8); 

    // query to get 2nd level ancestor of node 12 
    LA(ancestor, depth, isNode, 12, 2); 

    // delete node 12 
    removeNode(ancestor, isNode, len, 12); 

    // query to get 5th level ancestor of node 
    // 12 after deletion of node 
    LA(ancestor, depth, isNode, 12, 1); 

    return 0; 
} 

```

**Output:**

```
1th level acestor of node 8 is = 5
2th level acestor of node 12 is = 1
Node is not present in graph

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。