# 跳转指针算法

> 原文:[https://www.geeksforgeeks.org/jump-pointer-algorithm/](https://www.geeksforgeeks.org/jump-pointer-algorithm/)

**跳转指针算法**是对指针结构(如数组或链表)进行操作的并行算法的设计技术。该算法通常用于确定有根树的根。

在跳转指针算法中，我们对一棵树进行预处理，这样就可以在时间复杂度为 **O(log n)** 的情况下回答查询，找到树中任意节点的任意父节点。

跳转指针算法将高达 **log <sub>2</sub> n** 的指针关联到树的每个顶点。**这些指针被称为跳转指针，因为它们沿着树向上跳向树的根节点。**对于处理树的任何节点，算法存储长度为 **l** 的跳线数组，其中 **l = log2(深度(v))** 。这个数组的第 I 个元素指向节点 **v** 的第 2 个父节点。这种数据结构帮助我们从任何给定的节点跳到树的一半。当算法被要求处理一个查询以找到树中任何节点的任何父节点时，我们使用这些指针重复地向上跳树。跳转次数最多为 **log n** ，因此在 **O(log n)** 时间复杂度中可以回答任何寻找树中任意节点父节点的问题。
在跳转指针中，有一个从节点 N 到 N 的第 j 个父节点的指针，对于
j = 1，2，4，8，…等等。所以我们用每个节点的父节点存储 2 <sup>。</sup>

跳转指针算法基本上在**动态编程的方法上工作，在该方法中，我们使用预先计算的结果来找到下一个结果**。通过做一些简单的计算，我们可以计算出这样的数学公式:对于任意节点 **k，k 的第 2 个 <sup>j</sup> 母节点等于 k 的第 2 个 <sup>j-1</sup> 母节点和第 2 个 <sup>j-1</sup> 母节点。**

这个公式的简要解释在下面的算法部分给出。

这种算法最常见的用途是解决我们需要在 O(log n)时间复杂度中找到任意节点的祖先的查询。

**实现跳转指针算法的图形:**

![](img/82f58a270049395b8259d5486d16355c.png)

**存储所有节点的第 2^i 父节点的跳转数组的表示:**

![](img/54839ed5b0c157d823066bb0f6d509c1.png)

**示例:**

```
Input: 0th parent of node 2 
Output: 0th parent of node 2 is = 2

Input: 2th parent of node 4
Output: 2th parent of node 4 is = 2

Input: 3rd parent of node 8 
Output: 3rd parent of node 8 is = 1
```

**<u>算法</u> :**
下面是实现跳转指针算法来查找图中任意节点的任意父节点的算法。我们使用**动态编程**来确定跳转矩阵。这里，我们将根节点表示为 **R** ，并且最初假设**根节点的父节点为 0，这意味着该节点没有父节点**。现在看图，数组如上图所示，我们很容易理解上面的公式来确定每个节点的第 2 个 <sup>i</sup> 父节点。如果我们查看值为 8 的节点，我们可以看到它的第 **2 <sup>0</sup> 父节点是 10** ， 现在要找到它的第 2 个 <sup>1</sup> 父节点，我们看到它的第 2 个 <sup>1</sup> 父节点是值为 10 的节点的第 2 个 <sup>0</sup> 父节点，这里的 10 是 8 **的第 2 个 <sup>0</sup> 父节点的意思是节点 8 的第 2 个 <sup>1</sup> 父节点是节点 8 的第 2 个 <sup>0</sup> 父节点 8 的第 2 个 <sup>0</sup> 父节点 8** 同样，我们也可以看到节点 8 的第 2 个 <sup>2</sup> 父节点是 5，也就是节点 8 的第 2 个 **2 <sup>1</sup> 父节点，也就是值为 9** 的节点的第 2 个 <sup>1</sup> 父节点。
这样，我们可以计算所有节点的跳转指针数组，以存储它们的第 2 个 <sup>i</sup> 父节点。

下面是计算跳转指针矩阵的伪代码，该矩阵存储了树中所有节点的第 2 个 <sup>i</sup> 父节点。

```
jump[k][j] =   it points 2^jth parent of k    
             =  2^j-1th parent of (2^j-1th parent of k)       
             =  jump[jump[i][j-1][j-1] 
```

**<u>实现</u> :** 下面是实现上述算法的代码，以寻找 O( logn)时间复杂度中任意节点的任意父节点。

## C++

```
// C++ program to implement Jump pointer algorithm
#include <bits/stdc++.h>
using namespace std;

int R = 0;
// n -> it represent total number of nodes
// len -> it is the maximum length of array
// to hold parent of each node.
// In worst case, the highest value of
// parent a node can have is n-1.
// 2 ^ len <= n-1
// len = O(log2n)
int getLen(int n)
{
    int len = (int)(log(n) / log(2)) + 1;
    return len;
}

// jump represent 2D matrix to hold parent of node in jump matrix
// here we pass reference of 2D matrix so that the change made
// occur directly to the original matrix
// len is same as defined above
// n is total nodes in graph
void set_jump_pointer(vector<vector<int> >& jump,
                      vector<int> node, int len, int n)
{
    for (int j = 1; j <= len; j++)
        for (int i = 0; i < n; i++)
            jump[ node[i] ][j] = jump[jump[node[i] ][j - 1] ][j - 1];
}

// c -> it represent child
// p -> it represent parent
// i -> it represent node number
// p=0 means the node is root node
// here also we pass reference of 2D matrix
// and depth vector so that the change made
// occur directly to the original matrix and original vector
void constructGraph(vector<vector<int> >& jump,
                    vector<int>& node, vector<int>& isNode, int c, int p, int i)
{
    // enter the node in node array
    // it stores all the nodes in the graph
    node[i] = c;

    // to confirm that no child node have 2 parents
    if (isNode == 0) {
        isNode = 1;
        // make parent of x as y
        jump[0] = p;
    }
    return;
}

// function to jump to Lth parent of any node
void jumpPointer(vector<vector<int> >& jump,
                 vector<int> isNode, int x, int L, int n)
{
    int j = 0, curr = x, k = L;

    // to check if node is present in graph or not
    if (x > n || isNode[x] == 0) {
        cout << "Node is not present in graph " << endl;
        return;
    }

    // in this loop we decrease the value of L by L/2 and
    // increment j by 1 after each iteration, and check for set bit
    // if we get set bit then we update x with jth parent of x
    // as L becomes less than or equal to zero means
    // we have jumped to Lth parent of node x
    while (L > 0) {
        // to check if last bit is 1 or not
        if (L & 1)
            x = jump[x][j];

        // use of shift operator to make
        // L = L/2 after every iteration
        L = L >> 1;
        j++;
    }

    cout << k << "th parent of node " << curr
                   << " is = " << x << endl;

    return;
}

// Driver code
int main()
{
    // n represent number of nodes
    int n = 11;

    // function to calculate len
    // len -> it is the maximum length of
    // array to hold parent of each node.
    int len = getLen(n);

    // initialization of parent matrix
    vector<vector<int> > jump(n+1, vector<int>(len+1));

    // node array is used to store all nodes
    vector<int> node(n+1);

    // isNode is an array to check whether
    // a node is present in graph or not
    vector<int> isNode(n+1,0);

    // R stores root node
    R = 2;

    // construction of graph
    // here 0 represent that the node is root node
    constructGraph(jump, node, isNode, 2, 0, 0);
    constructGraph(jump, node, isNode, 5, 2, 1);
    constructGraph(jump, node, isNode, 3, 5, 2);
    constructGraph(jump, node, isNode, 4, 5, 3);
    constructGraph(jump, node, isNode, 1, 5, 4);
    constructGraph(jump, node, isNode, 7, 1, 5);
    constructGraph(jump, node, isNode, 9, 1, 6);
    constructGraph(jump, node, isNode, 10, 9, 7);
    constructGraph(jump, node, isNode, 11, 10, 8);
    constructGraph(jump, node, isNode, 6, 10, 9);
    constructGraph(jump, node, isNode, 8, 10, 10);

    // function to pre compute jump matrix
    set_jump_pointer(jump, node, len, n);

    // query to jump to parent using jump pointers
    // query to jump to 1st parent of node 2
    jumpPointer(jump, isNode, 2, 0, n);

    // query to jump to 2nd parent of node 4
    jumpPointer(jump, isNode, 4, 2, n);

    // query to jump to 3rd parent of node 8
    jumpPointer(jump, isNode, 8, 3, n);

    // query to jump to 5th parent of node 20
    jumpPointer(jump, isNode, 20, 5, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to implement
# Jump pointer algorithm
import math

# Initialization of parent matrix
# suppose max range of a node is
# up to 1000 if there are 1000 nodes
#  than also length of jump matrix
# will not exceed 10
jump = [[0 for j in range(10)]
           for i in range(1000)]

# Node array is used to store all nodes
node = [0 for i in range(1000)]

# isNode is an array to check whether
# a node is present in graph or not
isNode = [0 for i in range(1000)]

# n -> it represent total number of nodes
# len -> it is the maximum length of array
# to hold parent of each node.
# In worst case, the highest value of
# parent a node can have is n-1.
# 2 ^ len <= n-1
# len = O(log2n)
def getLen(n):

    len = int((math.log(n)) //
              (math.log(2))) + 1
    return len

# jump represent 2D matrix to hold parent
# of node in jump matrix here we pass
# reference of 2D matrix so that the
# change made occur directly to the
# original matrix len is same as
# defined above n is total nodes
# in graph
def set_jump_pointer(len, n):

    global jump, node
    for j in range(1,len + 1):
        for i in range(0, n):
            jump[node[i]][j] = jump[jump[node[i]][j - 1]][j - 1]

# c -> it represent child
# p -> it represent parent
# i -> it represent node number
# p=0 means the node is root node
# here also we pass reference of
# 2D matrix and depth vector so
# that the change made occur
# directly to the original matrix
# and original vector
def constructGraph(c, p, i):

    global jump, node, isNode

    # Enter the node in node array
    # it stores all the nodes in the graph
    node[i] = c

    # To confirm that no child node
    # have 2 parents
    if (isNode == 0):
        isNode = 1

        # Make parent of x as y
        jump[0] = p

    return

# function to jump to Lth parent
# of any node
def jumpPointer(x, L):

    j = 0
    n = x
    k = L

    global jump, isNode

    # To check if node is present in
    # graph or not
    if (isNode[x] == 0):
        print("Node is not present in graph ")
        return

    # In this loop we decrease the value
    # of L by L/2 and increment j by 1
    # after each iteration, and check
    # for set bit if we get set bit
    # then we update x with jth parent
    # of x as L becomes less than or
    # equal to zero means we have
    # jumped to Lth parent of node x
    while (L > 0):

        # To check if last bit is 1 or not
        if ((L & 1)!=0):
            x = jump[x][j]

        # Use of shift operator to make
        # L = L/2 after every iteration
        L = L >> 1
        j += 1

    print(str(k) + "th parent of node " +
          str(n) + " is = " + str(x))  

    return

# Driver code
if __name__=="__main__":

    # n represent number of nodes
    n = 11

    # Function to calculate len
    # len -> it is the maximum length of
    # array to hold parent of each node.
    len = getLen(n)

    # R stores root node
    R = 2

    # Construction of graph
    # here 0 represent that
    # the node is root node
    constructGraph(2, 0, 0)
    constructGraph(5, 2, 1)
    constructGraph(3, 5, 2)
    constructGraph(4, 5, 3)
    constructGraph(1, 5, 4)
    constructGraph(7, 1, 5)
    constructGraph(9, 1, 6)
    constructGraph(10, 9, 7)
    constructGraph(11, 10, 8)
    constructGraph(6, 10, 9)
    constructGraph(8, 10, 10)

    # Function to pre compute jump matrix
    set_jump_pointer(len, n)

    # Query to jump to parent using jump pointers
    # query to jump to 1st parent of node 2
    jumpPointer(2, 0)

    # Query to jump to 2nd parent of node 4
    jumpPointer(4, 2)

    # Query to jump to 3rd parent of node 8
    jumpPointer(8, 3)

    # Query to jump to 5th parent of node 20
    jumpPointer(20, 5)

# This code is contributed by rutvik_56
```

**Output:** 

```
0th parent of node 2 is = 2
2th parent of node 4 is = 2
3th parent of node 8 is = 1
Node is not present in graph
```

**时间复杂度:**每查询 O(logN)
T3】辅助空间: O(N * logN)