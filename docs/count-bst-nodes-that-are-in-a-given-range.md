# 统计位于给定范围内的 BST 节点

> 原文:[https://www . geesforgeks . org/count-BST-给定范围内的节点/](https://www.geeksforgeeks.org/count-bst-nodes-that-are-in-a-given-range/)

给定一个二叉查找树(BST)和一个范围，计算位于给定范围内的节点数。
**例:**

```
Input:
        10
      /    \
    5       50
   /       /  \
 1       40   100
Range: [5, 45]

Output:  3
There are three nodes in range, 5, 10 and 40
```

这个想法是从根开始遍历给定的二叉查找树。对于每个被访问的节点，检查该节点是否在范围内，如果是，则在结果中添加 1，并对其两个子节点重复出现。如果当前节点小于范围的低值，则右子节点重复出现，否则左子节点重复出现。
下面是上面思路的实现。

## C++

```
// C++ program to count BST nodes withing a given range
#include<bits/stdc++.h>
using namespace std;

// A BST node
struct node
{
    int data;
    struct node* left, *right;
};

// Utility function to create new node
node *newNode(int data)
{
    node *temp = new node;
    temp->data  = data;
    temp->left  = temp->right = NULL;
    return (temp);
}

// Returns count of nodes in BST in range [low, high]
int getCount(node *root, int low, int high)
{
    // Base case
    if (!root) return 0;

    // Special Optional case for improving efficiency
    if (root->data == high && root->data == low)
        return 1;

    // If current node is in range, then include it in count and
    // recur for left and right children of it
    if (root->data <= high && root->data >= low)
         return 1 + getCount(root->left, low, high) +
                    getCount(root->right, low, high);

    // If current node is smaller than low, then recur for right
    // child
    else if (root->data < low)
         return getCount(root->right, low, high);

    // Else recur for left child
    else return getCount(root->left, low, high);
}

// Driver program
int main()
{
    // Let us construct the BST shown in the above figure
    node *root        = newNode(10);
    root->left        = newNode(5);
    root->right       = newNode(50);
    root->left->left  = newNode(1);
    root->right->left = newNode(40);
    root->right->right = newNode(100);
    /* Let us constructed BST shown in above example
          10
        /    \
      5       50
     /       /  \
    1       40   100   */
    int l = 5;
    int h = 45;
    cout << "Count of nodes between [" << l << ", " << h
         << "] is " << getCount(root, l, h);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count BST nodes that
// lie in a given range
class BinarySearchTree {

    /* Class containing left and right child
    of current node and key value*/
    static class Node {
        int data;
        Node left, right;

        public Node(int item) {
            data = item;
            left = right = null;
        }
    }

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() {
        root = null;
    }

    // Returns count of nodes in BST in
    // range [low, high]
    int getCount(Node node, int low, int high)
    {
        // Base Case
        if(node == null)
            return 0;

        // If current node is in range, then
        // include it in count and recur for
        // left and right children of it
        if(node.data >= low && node.data <= high)
            return 1 + this.getCount(node.left, low, high)+
                this.getCount(node.right, low, high);

        // If current node is smaller than low,
        // then recur for right child
        else if(node.data < low)
            return this.getCount(node.right, low, high);

        // Else recur for left child
        else
            return this.getCount(node.left, low, high);    
    }

    // Driver function
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();

        tree.root = new Node(10);
        tree.root.left     = new Node(5);
        tree.root.right     = new Node(50);
        tree.root.left.left = new Node(1);
        tree.root.right.left = new Node(40);
        tree.root.right.right = new Node(100);
        /* Let us constructed BST shown in above example
          10
        /    \
      5       50
     /       /  \
    1       40   100   */
    int l=5;
    int h=45;
    System.out.println("Count of nodes between [" + l + ", "
                      + h+ "] is " + tree.getCount(tree.root,
                                                  l, h));
    }
}
// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to count BST nodes
# withing a given range

# Utility function to create new node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Returns count of nodes in BST in
# range [low, high]
def getCount(root, low, high):

    # Base case
    if root == None:
        return 0

    # Special Optional case for improving
    # efficiency
    if root.data == high and root.data == low:
        return 1

    # If current node is in range, then
    # include it in count and recur for
    # left and right children of it
    if root.data <= high and root.data >= low:
        return (1 + getCount(root.left, low, high) +
                    getCount(root.right, low, high))

    # If current node is smaller than low,
    # then recur for right child
    elif root.data < low:
        return getCount(root.right, low, high)

    # Else recur for left child
    else:
        return getCount(root.left, low, high)

# Driver Code
if __name__ == '__main__':

    # Let us construct the BST shown in
    # the above figure
    root = newNode(10)
    root.left = newNode(5)
    root.right = newNode(50)
    root.left.left = newNode(1)
    root.right.left = newNode(40)
    root.right.right = newNode(100)

    # Let us constructed BST shown in above example
    #     10
    #     / \
    # 5     50
    # /     / \
    # 1     40 100
    l = 5
    h = 45
    print("Count of nodes between [", l, ", ", h,"] is ",
                                    getCount(root, l, h))

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# code to count BST nodes that
// lie in a given range
public class BinarySearchTree
{

    /* Class containing left and right child
    of current node and key value*/
    public class Node
    {
        public int data;
        public Node left, right;

        public Node(int item)
        {
            data = item;
            left = right = null;
        }
    }

    // Root of BST
    public Node root;

    // Constructor
    public BinarySearchTree()
    {
        root = null;
    }

    // Returns count of nodes in BST in 
    // range [low, high]
    public virtual int getCount(Node node, int low, int high)
    {
        // Base Case
        if (node == null)
        {
            return 0;
        }

        // If current node is in range, then 
        // include it in count and recur for 
        // left and right children of it
        if (node.data >= low && node.data <= high)
        {
            return 1 + this.getCount(node.left, low, high) + this.getCount(node.right, low, high);
        }

        // If current node is smaller than low, 
        // then recur for right child
        else if (node.data < low)
        {
            return this.getCount(node.right, low, high);
        }

        // Else recur for left child
        else
        {
            return this.getCount(node.left, low, high);
        }
    }

    // Driver function
    public static void Main(string[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        tree.root = new Node(10);
        tree.root.left = new Node(5);
        tree.root.right = new Node(50);
        tree.root.left.left = new Node(1);
        tree.root.right.left = new Node(40);
        tree.root.right.right = new Node(100);
        /* Let us constructed BST shown in above example
          10
        /    \
      5       50
     /       /  \
    1       40   100   */
    int l = 5;
    int h = 45;
    Console.WriteLine("Count of nodes between [" + l + ", " + h + "] is " + tree.getCount(tree.root, l, h));
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript code to count BST nodes that
// lie in a given range

    /*
     * Class containing left and right child of current node and key value
     */
     class Node {
        constructor(item) {
            this.data = item;
            this.left =this.right = null;
        }
    }

    // Root of BST
    var root = null;

    // Returns count of nodes in BST in
    // range [low, high]
    function getCount( node , low , high) {
        // Base Case
        if (node == null)
            return 0;

        // If current node is in range, then
        // include it in count and recur for
        // left and right children of it
        if (node.data >= low && node.data <= high)
            return 1 + this.getCount(node.left, low, high) + this.getCount(node.right, low, high);

        // If current node is smaller than low,
        // then recur for right child
        else if (node.data < low)
            return this.getCount(node.right, low, high);

        // Else recur for left child
        else
            return this.getCount(node.left, low, high);
    }

    // Driver function

        root = new Node(10);
        root.left = new Node(5);
        root.right = new Node(50);
        root.left.left = new Node(1);
        root.right.left = new Node(40);
        root.right.right = new Node(100);
        /*
         * Let us constructed BST shown in above example 10 / \ 5 50 / / \ 1 40 100
         */
        var l = 5;
        var h = 45;
        document.write("Count of nodes between [" + l + ", " + h + "] is " + getCount(root, l, h));

// This code contributed by aashish1995
</script>
```

**输出:**

```
Count of nodes between [5, 45] is 3
```

上述程序的时间复杂度为 O(h + k)，其中 h 是 BST 的高度，k 是给定范围内的节点数。

https://youtu.be/jfk

-uX_xKK4？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
本文由[高拉夫·阿赫瓦尔](https://www.facebook.com/COOL.DUDE.BORN.NUD3?fref=ts)供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。