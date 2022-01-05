# 不求高度打印完美二叉树中层

> 原文:[https://www . geeksforgeeks . org/print-中层-完美-二叉树-不求高/](https://www.geeksforgeeks.org/print-middle-level-perfect-binary-tree-without-finding-height/)

给定一棵[完美二叉树](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)，打印中层节点，不计算其高度。完美二叉树是所有内部节点都有两个子节点，所有叶子都有相同深度或相同层次的二叉树。

![](img/ab9fda089880b51dc36ca0cace7ce5a7.png)

**输出:** 4 5 6 7

思路类似于[求单链表](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)中间的方法 2。
在树的每条路线上使用快速和慢速(或乌龟)指针。

1.  将快速指针向叶子前进 2。
2.  将慢速指针向前移动 1。
3.  如果快速指针到达慢速指针处的叶打印值
4.  检查快->左->左是否存在，然后递归地将慢指针移动一步，将快指针移动两步。
5.  如果 fast->left->left 不存在(在偶数层的情况下)，则将两个指针移动一步。

## C++

```
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has key, pointer to left
   child and a pointer to right child */
struct Node {
    int key;
    struct Node *left, *right;
};

/* To create a newNode of tree and return pointer */
struct Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Takes two parameters - same initially and
// calls recursively
void printMiddleLevelUtil(Node* a, Node* b)
{
    // Base case e
    if (a == NULL || b == NULL)
        return;

    // Fast pointer has reached the leaf so print
    // value at slow pointer
    if ((b->left == NULL) && (b->right == NULL)) {
        cout << a->key << " ";
        return;
    }

    // Recursive call
    // root.left.left and root.left.right will
    // print same value
    // root.right.left and root.right.right
    // will print same value
    // So we use any one of the condition
    if (b->left->left) {
        printMiddleLevelUtil(a->left, b->left->left);
        printMiddleLevelUtil(a->right, b->left->left);
    }
    else {
        printMiddleLevelUtil(a->left, b->left);
        printMiddleLevelUtil(a->right, b->left);
    }
}

// Main printing method that take a Tree as input
void printMiddleLevel(Node* node)
{
    printMiddleLevelUtil(node, node);
}

// Driver program to test above functions
int main()
{

    Node* n1 = newNode(1);
    Node* n2 = newNode(2);
    Node* n3 = newNode(3);
    Node* n4 = newNode(4);
    Node* n5 = newNode(5);
    Node* n6 = newNode(6);
    Node* n7 = newNode(7);

    n2->left = n4;
    n2->right = n5;
    n3->left = n6;
    n3->right = n7;
    n1->left = n2;
    n1->right = n3;

    printMiddleLevel(n1);
}

// This code is contributed by Prasad Kshirsagar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Tree node definition
class Node {
    public int key;
    public Node left;
    public Node right;
    public Node(int val)
    {
        this.left = null;
        this.right = null;
        this.key = val;
    }
}

public class PrintMiddle
{
    // Takes two parameters - same initially and
    // calls recursively
    private static void printMiddleLevelUtil(Node a, Node b)
    {
        // Base case e
        if (a == null || b == null)
            return;

        // Fast pointer has reached the leaf so print
        // value at slow pointer
        if ((b.left == null) && (b.right == null))
        {
            System.out.print(a.key + " ");
            return;
        }

        // Recursive call
        // root.left.left and root.left.right will
        // print same value
        // root.right.left and root.right.right
        // will print same value
        // So we use any one of the condition
        if (b.left.left!=null)
        {
            printMiddleLevelUtil(a.left, b.left.left);
            printMiddleLevelUtil(a.right, b.left.left);
        }
        else
        {
            printMiddleLevelUtil(a.left, b.left);
            printMiddleLevelUtil(a.right, b.left);
        }
    }

    // Main printing method that take a Tree as input
    public static void printMiddleLevel(Node node)
    {
        printMiddleLevelUtil(node, node);
    }

    // Driver code
    public static void main(String[] args)
    {
        Node n1 = new Node(1);
        Node n2 = new Node(2);
        Node n3 = new Node(3);
        Node n4 = new Node(4);
        Node n5 = new Node(5);
        Node n6 = new Node(6);
        Node n7 = new Node(7);

        n2.left = n4;
        n2.right = n5;
        n3.left = n6;
        n3.right = n7;
        n1.left = n2;
        n1.right = n3;

        printMiddleLevel(n1);
    }
}
```

## 蟒蛇 3

```
''' A binary tree node has key, pointer to left
   child and a pointer to right child '''

class Node:

    def __init__(self, key):

        self.key=key
        self.left = None
        self.right = None

# To create a newNode of tree and return pointer
def newNode(key):

    temp = Node(key)
    return temp

# Takes two parameters - same initially and
# calls recursively
def  printMiddleLevelUtil(a, b):

    # Base case e
    if (a == None or b == None):
        return;

    # Fast pointer has reached the leaf so print
    # value at slow pointer
    if ((b.left == None) and (b.right == None)):
        print(a.key, end=' ')

        return;

    # Recursive call
    # root.left.left and root.left.right will
    # print same value
    # root.right.left and root.right.right
    # will print same value
    # So we use any one of the condition
    if (b.left.left):
        printMiddleLevelUtil(a.left, b.left.left);
        printMiddleLevelUtil(a.right, b.left.left);

    else:
        printMiddleLevelUtil(a.left, b.left);
        printMiddleLevelUtil(a.right, b.left);

# Main printing method that take a Tree as input
def printMiddleLevel(node):

    printMiddleLevelUtil(node, node);

# Driver program to test above functions
if __name__=='__main__':

    n1 = newNode(1);
    n2 = newNode(2);
    n3 = newNode(3);
    n4 = newNode(4);
    n5 = newNode(5);
    n6 = newNode(6);
    n7 = newNode(7);

    n2.left = n4;
    n2.right = n5;
    n3.left = n6;
    n3.right = n7;
    n1.left = n2;
    n1.right = n3;

    printMiddleLevel(n1);

# This code is contributed by rutvik_56
```

## C#

```
using System;
// Tree node definition
public class Node {
    public int key;
    public Node left;
    public Node right;
    public Node(int val)
    {
        this.left = null;
        this.right = null;
        this.key = val;
    }
}

public class PrintMiddle
{
    // Takes two parameters - same initially and
    // calls recursively
    private static void printMiddleLevelUtil(Node a, Node b)
    {
        // Base case e
        if (a == null || b == null)
            return;

        // Fast pointer has reached the leaf so print
        // value at slow pointer
        if ((b.left == null) && (b.right == null))
        {
            Console.Write(a.key + " ");
            return;
        }

        // Recursive call
        // root.left.left and root.left.right will
        // print same value
        // root.right.left and root.right.right
        // will print same value
        // So we use any one of the condition
        if (b.left.left!=null)
        {
            printMiddleLevelUtil(a.left, b.left.left);
            printMiddleLevelUtil(a.right, b.left.left);
        }
        else
        {
            printMiddleLevelUtil(a.left, b.left);
            printMiddleLevelUtil(a.right, b.left);
        }
    }

    // Main printing method that take a Tree as input
    public static void printMiddleLevel(Node node)
    {
        printMiddleLevelUtil(node, node);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node n1 = new Node(1);
        Node n2 = new Node(2);
        Node n3 = new Node(3);
        Node n4 = new Node(4);
        Node n5 = new Node(5);
        Node n6 = new Node(6);
        Node n7 = new Node(7);

        n2.left = n4;
        n2.right = n5;
        n3.left = n6;
        n3.right = n7;
        n1.left = n2;
        n1.right = n3;

        printMiddleLevel(n1);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Tree node definition

    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.key = val;
        }
    }

    // Takes two parameters - same initially and
    // calls recursively
    function printMiddleLevelUtil(a, b)
    {

        // Base case e
        if (a == null || b == null)
            return;

        // Fast pointer has reached the leaf so print
        // value at slow pointer
        if ((b.left == null) && (b.right == null))
        {
            document.write(a.key + " ");
            return;
        }

        // Recursive call
        // root.left.left and root.left.right will
        // print same value
        // root.right.left and root.right.right
        // will print same value
        // So we use any one of the condition
        if (b.left.left != null)
        {
            printMiddleLevelUtil(a.left, b.left.left);
            printMiddleLevelUtil(a.right, b.left.left);
        }
        else
        {
            printMiddleLevelUtil(a.left, b.left);
            printMiddleLevelUtil(a.right, b.left);
        }
    }

    // Main printing method that take a Tree as input
    function printMiddleLevel(node)
    {
        printMiddleLevelUtil(node, node);
    }

    let n1 = new Node(1);
    let n2 = new Node(2);
    let n3 = new Node(3);
    let n4 = new Node(4);
    let n5 = new Node(5);
    let n6 = new Node(6);
    let n7 = new Node(7);

    n2.left = n4;
    n2.right = n5;
    n3.left = n6;
    n3.right = n7;
    n1.left = n2;
    n1.right = n3;

    printMiddleLevel(n1);

    // This code is contributed by suresh07.
</script>
```

**Output**

```
2 3
```

https://youtu.be/gy_XfE9eVfc
本文由**巴尔基山**供稿。你可以给我发一封电子邮件——kishan020696@gmail.com 如果你喜欢极客博客并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章，或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。