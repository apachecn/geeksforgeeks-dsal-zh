# 以垂直顺序打印二叉树|设置 1

> 原文:[https://www . geesforgeks . org/print-binary-tree-vertical-order/](https://www.geeksforgeeks.org/print-binary-tree-vertical-order/)

给定一棵二叉树，垂直打印。以下示例说明了垂直顺序遍历。

```
           1
        /    \
       2      3
      / \    / \
     4   5  6   7
             \   \
              8   9 

The output of print this tree vertically will be:
4
2
1 5 6
3 8
7
9 
```

![print-binary-tree-in-vertical-order](img/cc28eedea5b4a9f78c91d1d61ee6e5ea.png)

这个想法是遍历一次树，得到相对于根的最小和最大水平距离。对于上面显示的树，最小距离为-2(对于值为 4 的节点)，最大距离为 3(对于值为 9 的节点)。
一旦我们有了离根的最大和最小距离，我们就在离根最小到最大的距离上迭代每条垂直线，对于每条垂直线遍历树并打印位于该垂直线上的节点。
**算法:**

```
// min --> Minimum horizontal distance from root
// max --> Maximum horizontal distance from root
// hd  --> Horizontal distance of current node from root 
findMinMax(tree, min, max, hd)
     if tree is NULL then return;

     if hd is less than min then
           *min = hd;
     else if hd is greater than max then
           *max = hd;

     findMinMax(tree->left, min, max, hd-1);
     findMinMax(tree->right, min, max, hd+1);

printVerticalLine(tree, line_no, hd)
     if tree is NULL then return;

     if hd is equal to line_no, then
           print(tree->data);
     printVerticalLine(tree->left, line_no, hd-1);
     printVerticalLine(tree->right, line_no, hd+1); 
```

**实现:**
以下是上述算法的实现。

## C++

```
#include <iostream>
using namespace std;

// A node of binary tree
struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new Binary Tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to find min and max distances with respect
// to root.
void findMinMax(Node *node, int *min, int *max, int hd)
{
    // Base case
    if (node == NULL) return;

    // Update min and max
    if (hd < *min)  *min = hd;
    else if (hd > *max) *max = hd;

    // Recur for left and right subtrees
    findMinMax(node->left, min, max, hd-1);
    findMinMax(node->right, min, max, hd+1);
}

// A utility function to print all nodes on a given line_no.
// hd is horizontal distance of current node with respect to root.
void printVerticalLine(Node *node, int line_no, int hd)
{
    // Base case
    if (node == NULL) return;

    // If this node is on the given line number
    if (hd == line_no)
        cout << node->data << " ";

    // Recur for left and right subtrees
    printVerticalLine(node->left, line_no, hd-1);
    printVerticalLine(node->right, line_no, hd+1);
}

// The main function that prints a given binary tree in
// vertical order
void verticalOrder(Node *root)
{
    // Find min and max distances with resepect to root
    int min = 0, max = 0;
    findMinMax(root, &min, &max, 0);

    // Iterate through all possible vertical lines starting
    // from the leftmost line and print nodes line by line
    for (int line_no = min; line_no <= max; line_no++)
    {
        printVerticalLine(root, line_no, 0);
        cout << endl;
    }
}

// Driver program to test above functions
int main()
{
    // Create binary tree shown in above figure
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);
    root->right->right->right = newNode(9);

    cout << "Vertical order traversal is \n";
    verticalOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print binary tree in reverse order

// A binary tree node
class Node
{
    int data;
    Node left, right;

    Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class Values
{
    int max, min;
}

class BinaryTree
{
    Node root;
    Values val = new Values();

    // A utility function to find min and max distances with respect
    // to root.
    void findMinMax(Node node, Values min, Values max, int hd)
    {
        // Base case
        if (node == null)
            return;

        // Update min and max
        if (hd < min.min)
            min.min = hd;
        else if (hd > max.max)
            max.max = hd;

        // Recur for left and right subtrees
        findMinMax(node.left, min, max, hd - 1);
        findMinMax(node.right, min, max, hd + 1);
    }

    // A utility function to print all nodes on a given line_no.
    // hd is horizontal distance of current node with respect to root.
    void printVerticalLine(Node node, int line_no, int hd)
    {
        // Base case
        if (node == null)
            return;

        // If this node is on the given line number
        if (hd == line_no)
            System.out.print(node.data + " ");       

        // Recur for left and right subtrees
        printVerticalLine(node.left, line_no, hd - 1);
        printVerticalLine(node.right, line_no, hd + 1);
    }

    // The main function that prints a given binary tree in
    // vertical order
    void verticalOrder(Node node)
    {
        // Find min and max distances with resepect to root
        findMinMax(node, val, val, 0);

        // Iterate through all possible vertical lines starting
        // from the leftmost line and print nodes line by line
        for (int line_no = val.min; line_no <= val.max; line_no++)
        {
            printVerticalLine(node, line_no, 0);
            System.out.println("");
        }
    }

    // Driver program to test the above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /* Let us construct the tree shown in above diagram */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);
        tree.root.right.right.right = new Node(9);

        System.out.println("vertical order traversal is :");
        tree.verticalOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Program to print binary tree in vertical order

# A binary tree
class Node:
    # Constructor to create a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# A utility function to find min and max distances with
# respect to root
def findMinMax(node, minimum, maximum, hd):

    # Base Case
    if node is None:
        return

    # Update min and max
    if hd < minimum[0] :
        minimum[0] = hd
    elif hd > maximum[0]:
        maximum[0] = hd

    # Recur for left and right subtrees
    findMinMax(node.left, minimum, maximum, hd-1)
    findMinMax(node.right, minimum, maximum, hd+1)

# A utility function to print all nodes on a given line_no
# hd is horizontal distance of current node with respect to root
def printVerticalLine(node, line_no, hd):

    # Base Case
    if node is None:
        return

    # If this node is on the given line number
    if hd == line_no:
        print node.data,

    # Recur for left and right subtrees
    printVerticalLine(node.left, line_no, hd-1)
    printVerticalLine(node.right, line_no, hd+1)

def verticalOrder(root):

    # Find min and max distances with respect to root
    minimum = [0]
    maximum = [0]
    findMinMax(root, minimum, maximum, 0)

    # Iterate through all possible lines starting
    # from the leftmost line and print nodes line by line
    for line_no in range(minimum[0], maximum[0]+1):
        printVerticalLine(root, line_no, 0)
        print

# Driver program to test above function
root = Node(1)
root.left = Node(2)
root.right = Node(3)
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)
root.right.left.right = Node(8)
root.right.right.right = Node(9)

print "Vertical order traversal is"
verticalOrder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to print binary tree in reverse order
using System;

// A binary tree node
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

class Values
{
    public int max, min;
}

public class BinaryTree
{
    Node root;
    Values val = new Values();

    // A utility function to find min and
    //  max distances with respect to root.
    void findMinMax(Node node, Values min,
                    Values max, int hd)
    {
        // Base case
        if (node == null)
            return;

        // Update min and max
        if (hd < min.min)
            min.min = hd;
        else if (hd > max.max)
            max.max = hd;

        // Recur for left and right subtrees
        findMinMax(node.left, min, max, hd - 1);
        findMinMax(node.right, min, max, hd + 1);
    }

    // A utility function to print
    // all nodes on a given line_no.
    // hd is horizontal distance of
    // current node with respect to root.
    void printVerticalLine(Node node,
                            int line_no, int hd)
    {
        // Base case
        if (node == null)
            return;

        // If this node is on the given line number
        if (hd == line_no)
            Console.Write(node.data + " ");    

        // Recur for left and right subtrees
        printVerticalLine(node.left, line_no, hd - 1);
        printVerticalLine(node.right, line_no, hd + 1);
    }

    // The main function that prints
    // a given binary tree in vertical order
    void verticalOrder(Node node)
    {
        // Find min and max distances with resepect to root
        findMinMax(node, val, val, 0);

        // Iterate through all possible
        // vertical lines starting from the
        // leftmost line and print nodes line by line
        for (int line_no = val.min; line_no <= val.max; line_no++)
        {
            printVerticalLine(node, line_no, 0);
            Console.WriteLine("");
        }
    }

    // Driver code
    public static void Main()
    {
        BinaryTree tree = new BinaryTree();

        /* Let us construct the tree
        shown in above diagram */
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);
        tree.root.right.left.right = new Node(8);
        tree.root.right.right.right = new Node(9);

        Console.WriteLine("vertical order traversal is :");
        tree.verticalOrder(tree.root);
    }
}

/* This code is contributed PrinciRaj1992 */
```

## java 描述语言

```
<script>

    // JavaScript program to print binary tree
    // in reverse order

    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root, min = 0, max = 0;

    // A utility function to find min and
    // max distances with respect
    // to root.
    function findMinMax(node, hd)
    {
        // Base case
        if (node == null)
            return;

        // Update min and max
        if (hd < min)
            min = hd;
        else if (hd > max)
            max = hd;

        // Recur for left and right subtrees
        findMinMax(node.left, hd - 1);
        findMinMax(node.right, hd + 1);
    }

    // A utility function to print all nodes on a given line_no.
    // hd is horizontal distance of
    // current node with respect to root.
    function printVerticalLine(node, line_no, hd)
    {
        // Base case
        if (node == null)
            return;

        // If this node is on the given line number
        if (hd == line_no)
            document.write(node.data + " ");       

        // Recur for left and right subtrees
        printVerticalLine(node.left, line_no, hd - 1);
        printVerticalLine(node.right, line_no, hd + 1);
    }

    // The main function that prints a given binary tree in
    // vertical order
    function verticalOrder(node)
    {
        // Find min and max distances with resepect to root
        findMinMax(node, 0);

        // Iterate through all possible vertical lines starting
        // from the leftmost line and print nodes line by line
        for (let line_no = min; line_no <= max; line_no++)
        {
            printVerticalLine(node, line_no, 0);
            document.write("</br>");
        }
    }

    /* Let us construct the tree shown in above diagram */
    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.right.left.right = new Node(8);
    root.right.right.right = new Node(9);

    document.write("Vertical order traversal is :" + "</br>");
    verticalOrder(root);

</script>
```

**输出:**

```
Vertical order traversal is
4
2
1 5 6
3 8
7
9
```

**时间复杂度:**上述算法的时间复杂度为 O(w*n)，其中 w 为二叉树的宽度，n 为二叉树中的节点数。在最坏的情况下，w 的值可以是 O(n)(例如考虑一个完整的树)，时间复杂度可以变成 O(n <sup>2</sup> )。
这个问题可以使用[这个](https://www.geeksforgeeks.org/vertical-sum-in-a-given-binary-tree/)帖子中讨论的技术更有效地解决。我们将很快讨论完整的算法和实现更有效的方法。
本文由 **Shalki Agarwal** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息