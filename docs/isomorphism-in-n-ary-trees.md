# N 元树中的同构

> 原文:[https://www.geeksforgeeks.org/isomorphism-in-n-ary-trees/](https://www.geeksforgeeks.org/isomorphism-in-n-ary-trees/)

给定两个分别具有 **M** 节点的 [N 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)。另外，分别给定它们的边和根。任务是检查它们是否是[同构树](https://www.geeksforgeeks.org/tree-isomorphism-problem/)。如果两棵树同构，则打印**“是”**否则打印**“否”**。
**举例:**

> **输入:** M = 9，树-1: 1 的根节点，树-2: 3 的根节点
> 树-1 的边:{ (1，3)，(3，4)，(3，5)，(1，8)，(8，9)，(1，2)，(2，6)，(2，7) }
> 树-2 的边:{ (3，1)，(1，2)，(1，5)，(3，6)，(6，7)，(3，4)，(4，8)，(4，9) }
> 
> ![](img/67d48f3fb2a81f365e5732d051d0ce30.png)
> 
> **输出:**YES
> T3】输入: M = 9，树-1 的根节点:6，树-2 的根节点:7
> 树-1 的边:{(1，3)，(1，2)，(1，8)，(3，4)，(3，5)，(8，9)，(2，6)，(2，7)}
> 树-2 的边:{(1，2)，(1，5)，(3，1)，(3，4)，(4，8)，(4，9)，(6，3)，(7，6)
> 
> ![](img/67d48f3fb2a81f365e5732d051d0ce30.png)
> 
> **输出:**否

**方法:**
想法是找出这两棵树的范式并进行比较。叶节点将使**“()”**返回到其后续的上层。
下面是一个例子，展示了寻找范式的过程。

![](img/b63a53bac2e3d73f4c4bff47f3a6b41b.png)

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To create N-ary tree
map<int, vector<int> > tree;

// Function which will accept the root
// of the tree and its parent (which
// is initially "-1") and will return
// the canonical form of the tree
string ConvertCanonical(int vertex,
                        int parent)
{
    // In this string vector we will
    // store canonical form of out
    // current node and its subtree
    vector<string> child;

    // Loop to the neighbours of
    // current vertex
    for (auto neighbour : tree[vertex]) {

        // This is to prevent us from
        // visiting the parent again
        if (neighbour == parent)
            continue;

        // DFS call neighbour of our
        // current vertex & it will
        // pushback the subtree-structure
        // of this neighbour into our
        // child vector.
        child.push_back(ConvertCanonical(
            neighbour, vertex));
    }

    // These opening and closing
    // brackets are for the
    // current node
    string str = "(";

    // Sorting function will re-order
    // the structure of subtree of
    // the current vertex in a
    // shortest-subtree-first manner.
    // Hence we can
    // now compare the two tree
    // structures effectively
    sort(child.begin(), child.end());

    for (auto j : child)
        str += j;

    // Append the subtree structure
    // and enclose it with "(" <subtree>
    // ")" the opening and closing
    // brackets of current vertex
    str += ")";

    // return the subtree-structure
    // of our Current vertex
    return str;
}

// Function to add edges
void addedge(int a, int b)
{
    tree[a].push_back(b);
    tree[b].push_back(a);
}

// Driver code
int main()
{
    // Given N-ary Tree 1
    addedge(1, 3);
    addedge(1, 2);
    addedge(1, 5);
    addedge(3, 4);
    addedge(4, 8);
    addedge(4, 9);
    addedge(3, 6);
    addedge(6, 7);

    // Function Call to convert Tree 1
    // into canonical with 3 is the root
    // and the parent of root be "-1"
    string tree1 = ConvertCanonical(3, -1);

    // Clearing our current tree
    // before taking input of
    // next tree
    tree.clear();

    // Given N-ary Tree 2
    addedge(1, 3);
    addedge(3, 4);
    addedge(3, 5);
    addedge(1, 8);
    addedge(8, 9);
    addedge(1, 2);
    addedge(2, 6);
    addedge(2, 7);

    // Function Call to convert Tree 2
    // into canonical
    string tree2 = ConvertCanonical(1, -1);

    // Check if canonical form of both
    // tree are equal or not
    if (tree1 == tree2)
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To create N-ary tree
tree=dict()

# Function which will accept the root
# of the tree and its parent (which
# is initially "-1") and will return
# the canonical form of the tree
def ConvertCanonical(vertex, parent):
    # In this string vector we will
    # store canonical form of out
    # current node and its subtree
    child=[]

    # Loop to the neighbours of
    # current vertex
    for neighbour in tree[vertex] :

        # This is to prevent us from
        # visiting the parent again
        if (neighbour == parent):
            continue

        # DFS call neighbour of our
        # current vertex & it will
        # pushback the subtree-structure
        # of this neighbour into our
        # child vector.
        child.append(ConvertCanonical(
            neighbour, vertex))

    # These opening and closing
    # brackets are for the
    # current node
    s = "("

    # Sorting function will re-order
    # the structure of subtree of
    # the current vertex in a
    # shortest-subtree-first manner.
    # Hence we can
    # now compare the two tree
    # structures effectively
    child.sort()

    for j in child:
        s += j

    # Append the subtree structure
    # and enclose it with "(" <subtree>
    # ")" the opening and closing
    # brackets of current vertex
    s += ")"

    # return the subtree-structure
    # of our Current vertex
    return s

# Function to add edges
def addedge(a, b):
    if a in tree:
        tree[a].append(b)
    else:
        tree[a]=[b,]
    if b in tree:
        tree[b].append(a)
    else:
        tree[b]=[a,]

# Driver code
if __name__=='__main__':
    # Given N-ary Tree 1
    addedge(1, 3)
    addedge(1, 2)
    addedge(1, 5)
    addedge(3, 4)
    addedge(4, 8)
    addedge(4, 9)
    addedge(3, 6)
    addedge(6, 7)

    # Function Call to convert Tree 1
    # into canonical with 3 is the root
    # and the parent of root be "-1"
    tree1 = ConvertCanonical(3, -1)

    # Clearing our current tree
    # before taking input of
    # next tree
    tree.clear()

    # Given N-ary Tree 2
    addedge(1, 3)
    addedge(3, 4)
    addedge(3, 5)
    addedge(1, 8)
    addedge(8, 9)
    addedge(1, 2)
    addedge(2, 6)
    addedge(2, 7)

    # Function Call to convert Tree 2
    # into canonical
    tree2 = ConvertCanonical(1, -1)

    # Check if canonical form of both
    # tree are equal or not
    if (tree1 == tree2):
        print("YES")
    else:
        print("NO")
```

**Output:** 

```
YES
```

**时间复杂度:** *O(E * log(E))* ，其中 E 为边数。
***辅助空间** : O(E)*