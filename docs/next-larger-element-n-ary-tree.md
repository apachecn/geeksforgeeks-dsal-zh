# n 元树中的下一个较大元素

> 原文:[https://www . geesforgeks . org/next-biger-element-n-ary-tree/](https://www.geeksforgeeks.org/next-larger-element-n-ary-tree/)

给定一个类属树和一个整数 x。查找并返回树中下一个较大元素的节点，即查找仅大于 x 的节点。如果不存在值大于 x 的节点，则返回 NULL。
例如，在给定的树中

![](img/c7c9487b3a4f153afdb7453d43220fa1.png)

x = 10，只是更大的节点值是 12

想法是维护一个节点指针 **res** ，它将包含最终的结果节点。
遍历树并检查根数据是否大于 x。如果是，则将根数据与 res 数据进行比较。
如果根数据大于 n 且小于 res 数据，更新 RES

## C++

```
// CPP program to find next larger element
// in an n-ary tree.
#include <bits/stdc++.h>
using namespace std;

// Structure of a node of an n-ary tree
struct Node {
    int key;
    vector<Node*> child;
};

// Utility function to create a new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    return temp;
}

void nextLargerElementUtil(Node* root, int x, Node** res)
{
    if (root == NULL)
        return;

    // if root is less than res but greater than
    // x update res
    if (root->key > x)
        if (!(*res) || (*res)->key > root->key)
            *res = root;   

    // Number of children of root
    int numChildren = root->child.size();

    // Recur calling for every child
    for (int i = 0; i < numChildren; i++)
        nextLargerElementUtil(root->child[i], x, res);

    return;
}

// Function to find next Greater element of x in tree
Node* nextLargerElement(Node* root, int x)
{
    // resultant node
    Node* res = NULL;

    // calling helper function
    nextLargerElementUtil(root, x, &res);

    return res;
}

// Driver program
int main()
{
    /*   Let us create below tree
   *             5
   *         /   |  \
   *         1   2   3
   *        /   / \   \
   *       15  4   5   6
   */

    Node* root = newNode(5);
    (root->child).push_back(newNode(1));
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(3));
    (root->child[0]->child).push_back(newNode(15));
    (root->child[1]->child).push_back(newNode(4));
    (root->child[1]->child).push_back(newNode(5));
    (root->child[2]->child).push_back(newNode(6));

    int x = 5;

    cout << "Next larger element of " << x << " is ";
    cout << nextLargerElement(root, x)->key << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next larger element
// in an n-ary tree.
import java.util.*;

class GFG
{

// Structure of a node of an n-ary tree
static class Node
{
    int key;
    Vector<Node> child;
};
static Node res;

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.child = new Vector<>();
    return temp;
}

static void nextLargerElementUtil(Node root, int x)
{
    if (root == null)
        return;

    // if root is less than res but
    // greater than x, update res
    if (root.key > x)
        if ((res == null || (res).key > root.key))
            res = root;

    // Number of children of root
    int numChildren = root.child.size();

    // Recur calling for every child
    for (int i = 0; i < numChildren; i++)
        nextLargerElementUtil(root.child.get(i), x);

    return;
}

// Function to find next Greater element
// of x in tree
static Node nextLargerElement(Node root, int x)
{
    // resultant node
    res = null;

    // calling helper function
    nextLargerElementUtil(root, x);

    return res;
}

// Driver Code
public static void main(String[] args)
{
    /* Let us create below tree
    *             5
    *         / | \
    *         1 2 3
    *     / / \ \
    *     15 4 5 6
    */
    Node root = newNode(5);
    (root.child).add(newNode(1));
    (root.child).add(newNode(2));
    (root.child).add(newNode(3));
    (root.child.get(0).child).add(newNode(15));
    (root.child.get(1).child).add(newNode(4));
    (root.child.get(1).child).add(newNode(5));
    (root.child.get(2).child).add(newNode(6));

    int x = 5;

    System.out.print("Next larger element of " +
                                    x + " is ");
    System.out.print(nextLargerElement(root, x).key + "\n");

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find next larger element
# in an n-ary tree.
class Node:

# Structure of a node of an n-ary tree
    def __init__(self):
        self.key = 0
        self.child = []

# Utility function to create a new tree node
def newNode(key):
    temp = Node()
    temp.key = key
    temp.child = []
    return temp

res = None;   
def nextLargerElementUtil(root,x):
    global res
    if (root == None):
        return;

     # if root is less than res but
    # greater than x, update res
    if (root.key > x):
        if ((res == None or (res).key > root.key)):
            res = root;

    # Number of children of root
    numChildren = len(root.child)

     # Recur calling for every child
    for i in range(numChildren):
        nextLargerElementUtil(root.child[i], x)
    return

  # Function to find next Greater element
# of x in tree
def nextLargerElement(root,x):

   # resultant node
    global res
    res=None

    # Calling helper function
    nextLargerElementUtil(root, x)

    return res

    # Driver code
root = newNode(5)
(root.child).append(newNode(1))
(root.child).append(newNode(2))
(root.child).append(newNode(3))
(root.child[0].child).append(newNode(15))
(root.child[1].child).append(newNode(4))
(root.child[1].child).append(newNode(5))
(root.child[2].child).append(newNode(6))

x = 5
print("Next larger element of " , x , " is ",end='')
print(nextLargerElement(root, x).key)

# This code is contributed by rag2127.
```

## C#

```
// C# program to find next larger element
// in an n-ary tree.
using System;
using System.Collections.Generic;

class GFG
{

// Structure of a node of an n-ary tree
class Node
{
    public int key;
    public List<Node> child;
};
static Node res;

// Utility function to create a new tree node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.child = new List<Node>();
    return temp;
}

static void nextLargerElementUtil(Node root,
                                  int x)
{
    if (root == null)
        return;

    // if root is less than res but
    // greater than x, update res
    if (root.key > x)
        if ((res == null ||
            (res).key > root.key))
            res = root;

    // Number of children of root
    int numChildren = root.child.Count;

    // Recur calling for every child
    for (int i = 0; i < numChildren; i++)
        nextLargerElementUtil(root.child[i], x);

    return;
}

// Function to find next Greater element
// of x in tree
static Node nextLargerElement(Node root,   
                                  int x)
{
    // resultant node
    res = null;

    // calling helper function
    nextLargerElementUtil(root, x);

    return res;
}

// Driver Code
public static void Main(String[] args)
{
    /* Let us create below tree
    *             5
    *         / | \
    *         1 2 3
    *     / / \ \
    *     15 4 5 6
    */
    Node root = newNode(5);
    (root.child).Add(newNode(1));
    (root.child).Add(newNode(2));
    (root.child).Add(newNode(3));
    (root.child[0].child).Add(newNode(15));
    (root.child[1].child).Add(newNode(4));
    (root.child[1].child).Add(newNode(5));
    (root.child[2].child).Add(newNode(6));

    int x = 5;

    Console.Write("Next larger element of " +
                                 x + " is ");
    Console.Write(nextLargerElement(root, x).key + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find next larger element
// in an n-ary tree.

// Structure of a node of an n-ary tree
class Node
{
    constructor()
    {
        this.key = 0;
        this.child = [];
    }
};

var res = null;

// Utility function to create a new tree node
function newNode(key)
{
    var temp = new Node();
    temp.key = key;
    temp.child = [];
    return temp;
}

function nextLargerElementUtil(root, x)
{
    if (root == null)
        return;

    // if root is less than res but
    // greater than x, update res
    if (root.key > x)
        if ((res == null ||
            (res).key > root.key))
            res = root;

    // Number of children of root
    var numChildren = root.child.length;

    // Recur calling for every child
    for (var i = 0; i < numChildren; i++)
        nextLargerElementUtil(root.child[i], x);

    return;
}

// Function to find next Greater element
// of x in tree
function nextLargerElement(root,  x)
{
    // resultant node
    res = null;

    // calling helper function
    nextLargerElementUtil(root, x);

    return res;
}

// Driver Code
/* Let us create below tree
*             5
*         / | \
*         1 2 3
*     / / \ \
*     15 4 5 6
*/
var root = newNode(5);
(root.child).push(newNode(1));
(root.child).push(newNode(2));
(root.child).push(newNode(3));
(root.child[0].child).push(newNode(15));
(root.child[1].child).push(newNode(4));
(root.child[1].child).push(newNode(5));
(root.child[2].child).push(newNode(6));
var x = 5;
document.write("Next larger element of " +
                             x + " is ");
document.write(nextLargerElement(root, x).key + "<br>");

</script>
```

**输出:**

```
Next larger element of 5 is 6
```

本文由 [**查哈维**](https://auth.geeksforgeeks.org/profile.php?user=chhavi saini 1&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。