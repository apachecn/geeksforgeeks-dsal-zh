# 用父指针找到二叉树的右兄弟

> 原文:[https://www . geesforgeks . org/find-right-同胞-二叉树-父指针/](https://www.geeksforgeeks.org/find-right-sibling-binary-tree-parent-pointers/)

给定一个带有父指针的二叉树，找到一个给定节点的右同级(将给出指向该节点的指针)，如果它不存在，返回 null。在 O(1)空间和 O(n)时间做？
**例:**

```
             1
            / \
           2   3
          /  \  \
         4    6  5
        /      \  \
       7        9  8
       /         \
      10         12
Input : Given above tree with parent pointer and node 10
Output : 12 
```

**方法:**思路是找出最近祖先的第一个右子，既不是当前节点，也不是当前节点的父节点，往上走的时候跟踪那些中的级别。然后，遍历该节点第一个左子节点，如果左子节点不在那里，则遍历右子节点，如果级别变为 0，则这是给定节点的下一个右兄弟节点。
在上面的例子中，如果给定的节点是 7，我们将以 6 结束，以找到没有任何孩子的正确的孩子。
在这种情况下，我们需要递归调用当前级别的正确兄弟，这样我们的 case 就达到了 8。

## C++

```
// C program to print right sibling of a node
#include <bits/stdc++.h>

// A Binary Tree Node
struct Node {
    int data;
    Node *left, *right, *parent;
};

// A utility function to create a new Binary
// Tree Node
Node* newNode(int item, Node* parent)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    temp->parent = parent;
    return temp;
}

// Method to find right sibling
Node* findRightSibling(Node* node, int level)
{
    if (node == NULL || node->parent == NULL)
        return NULL;

    // GET Parent pointer whose right child is not
    // a parent or itself of this node. There might
    // be case when parent has no right child, but,
    // current node is left child of the parent
    // (second condition is for that).
    while (node->parent->right == node
           || (node->parent->right == NULL
               && node->parent->left == node)) {
        if (node->parent == NULL
            || node->parent->parent == NULL)
            return NULL;

        node = node->parent;
        level--;
    }

    // Move to the required child, where right sibling
    // can be present
    node = node->parent->right;

    if (node == NULL)
        return NULL;
    // find right sibling in the given subtree(from current
    // node), when level will be 0
    while (level < 0) {

        // Iterate through subtree
        if (node->left != NULL)
            node = node->left;
        else if (node->right != NULL)
            node = node->right;
        else

            // if no child are there, we cannot have right
            // sibling in this path
            break;

        level++;
    }

    if (level == 0)
        return node;

    // This is the case when we reach 9 node in the tree,
    // where we need to again recursively find the right
    // sibling
    return findRightSibling(node, level);
}

// Driver Program to test above functions
int main()
{
    Node* root = newNode(1, NULL);
    root->left = newNode(2, root);
    root->right = newNode(3, root);
    root->left->left = newNode(4, root->left);
    root->left->right = newNode(6, root->left);
    root->left->left->left = newNode(7, root->left->left);
    root->left->left->left->left = newNode(10, root->left->left->left);
    root->left->right->right = newNode(9, root->left->right);
    root->right->right = newNode(5, root->right);
    root->right->right->right = newNode(8, root->right->right);
    root->right->right->right->right = newNode(12, root->right->right->right);

    // passing 10
    Node* res = findRightSibling(root->left->left->left->left, 0);
    if (res == NULL)
        printf("No right sibling");
    else
        printf("%d", res->data);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print right sibling of a node
public class Right_Sibling {

    // A Binary Tree Node
    static class Node {
        int data;
        Node left, right, parent;

        // Constructor
        public Node(int data, Node parent)
        {
            this.data = data;
            left = null;
            right = null;
            this.parent = parent;
        }
    };

    // Method to find right sibling
    static Node findRightSibling(Node node, int level)
    {
        if (node == null || node.parent == null)
            return null;

        // GET Parent pointer whose right child is not
        // a parent or itself of this node. There might
        // be case when parent has no right child, but,
        // current node is left child of the parent
        // (second condition is for that).
        while (node.parent.right == node
               || (node.parent.right == null
                   && node.parent.left == node)) {
            if (node.parent == null)
                return null;

            node = node.parent;
            level--;
        }

        // Move to the required child, where right sibling
        // can be present
        node = node.parent.right;

        // find right sibling in the given subtree(from current
        // node), when level will be 0
        while (level < 0) {

            // Iterate through subtree
            if (node.left != null)
                node = node.left;
            else if (node.right != null)
                node = node.right;
            else

                // if no child are there, we cannot have right
                // sibling in this path
                break;

            level++;
        }

        if (level == 0)
            return node;

        // This is the case when we reach 9 node in the tree,
        // where we need to again recursively find the right
        // sibling
        return findRightSibling(node, level);
    }

    // Driver Program to test above functions
    public static void main(String args[])
    {
        Node root = new Node(1, null);
        root.left = new Node(2, root);
        root.right = new Node(3, root);
        root.left.left = new Node(4, root.left);
        root.left.right = new Node(6, root.left);
        root.left.left.left = new Node(7, root.left.left);
        root.left.left.left.left = new Node(10, root.left.left.left);
        root.left.right.right = new Node(9, root.left.right);
        root.right.right = new Node(5, root.right);
        root.right.right.right = new Node(8, root.right.right);
        root.right.right.right.right = new Node(12, root.right.right.right);

        // passing 10
        System.out.println(findRightSibling(root.left.left.left.left, 0).data);
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to print right sibling
# of a node

# A class to create a new Binary
# Tree Node
class newNode:
    def __init__(self, item, parent):
        self.data = item
        self.left = self.right = None
        self.parent = parent

# Method to find right sibling
def findRightSibling(node, level):
    if (node == None or node.parent == None):
        return None   

    # GET Parent pointer whose right child is not
    # a parent or itself of this node. There might
    # be case when parent has no right child, but,
    # current node is left child of the parent
    # (second condition is for that).
    while (node.parent.right == node or
          (node.parent.right == None and
           node.parent.left == node)):
        if (node.parent == None):
            return None

        node = node.parent
        level -= 1

    # Move to the required child, where
    # right sibling can be present
    node = node.parent.right

    # find right sibling in the given subtree
    # (from current node), when level will be 0
    while (level < 0):

        # Iterate through subtree
        if (node.left != None):
            node = node.left
        elif (node.right != None):
            node = node.right
        else:

            # if no child are there, we cannot
            # have right sibling in this path
            break

        level += 1

    if (level == 0):
        return node    

    # This is the case when we reach 9 node
    # in the tree, where we need to again
    # recursively find the right sibling
    return findRightSibling(node, level)

# Driver Code
if __name__ == '__main__':
    root = newNode(1, None)
    root.left = newNode(2, root)
    root.right = newNode(3, root)
    root.left.left = newNode(4, root.left)
    root.left.right = newNode(6, root.left)
    root.left.left.left = newNode(7, root.left.left)
    root.left.left.left.left = newNode(10, root.left.left.left)
    root.left.right.right = newNode(9, root.left.right)
    root.right.right = newNode(5, root.right)
    root.right.right.right = newNode(8, root.right.right)
    root.right.right.right.right = newNode(12, root.right.right.right)

    # passing 10
    res = findRightSibling(root.left.left.left.left, 0)
    if (res == None):
        print("No right sibling")
    else:
        print(res.data)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to print right sibling of a node
public class Right_Sibling {

    // A Binary Tree Node
    public class Node {
        public int data;
        public Node left, right, parent;

        // Constructor
        public Node(int data, Node parent)
        {
            this.data = data;
            left = null;
            right = null;
            this.parent = parent;
        }
    }

    // Method to find right sibling
    public static Node findRightSibling(Node node, int level)
    {
        if (node == null || node.parent == null) {
            return null;
        }

        // GET Parent pointer whose right child is not
        // a parent or itself of this node. There might
        // be case when parent has no right child, but,
        // current node is left child of the parent
        // (second condition is for that).
        while (node.parent.right == node
               || (node.parent.right == null
                   && node.parent.left == node)) {
            if (node.parent == null
                || node.parent.parent == null) {
                return null;
            }

            node = node.parent;
            level--;
        }

        // Move to the required child, where right sibling
        // can be present
        node = node.parent.right;

        // find right sibling in the given subtree(from current
        // node), when level will be 0
        while (level < 0) {

            // Iterate through subtree
            if (node.left != null) {
                node = node.left;
            }
            else if (node.right != null) {
                node = node.right;
            }
            else {

                // if no child are there, we cannot have right
                // sibling in this path
                break;
            }

            level++;
        }

        if (level == 0) {
            return node;
        }

        // This is the case when we reach 9 node in the tree,
        // where we need to again recursively find the right
        // sibling
        return findRightSibling(node, level);
    }

    // Driver Program to test above functions
    public static void Main(string[] args)
    {
        Node root = new Node(1, null);
        root.left = new Node(2, root);
        root.right = new Node(3, root);
        root.left.left = new Node(4, root.left);
        root.left.right = new Node(6, root.left);
        root.left.left.left = new Node(7, root.left.left);
        root.left.left.left.left = new Node(10, root.left.left.left);
        root.left.right.right = new Node(9, root.left.right);
        root.right.right = new Node(5, root.right);
        root.right.right.right = new Node(8, root.right.right);
        root.right.right.right.right = new Node(12, root.right.right.right);

        // passing 10
        Console.WriteLine(findRightSibling(root.left.left.left.left, 0).data);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
    // Javascript program to print right sibling of a node

    // A Binary Tree Node
    class Node
    {
        constructor(data, parent) {
           this.left = null;
           this.right = null;
           this.data = data;
           this.parent = parent;
        }
    }

    // Method to find right sibling
    function findRightSibling(node, level)
    {
        if (node == null || node.parent == null)
            return null;

        // GET Parent pointer whose right child is not
        // a parent or itself of this node. There might
        // be case when parent has no right child, but,
        // current node is left child of the parent
        // (second condition is for that).
        while (node.parent.right == node
               || (node.parent.right == null
                   && node.parent.left == node)) {
            if (node.parent == null)
                return null;

            node = node.parent;
            level--;
        }

        // Move to the required child, where right sibling
        // can be present
        node = node.parent.right;

        // find right sibling in the given subtree(from current
        // node), when level will be 0
        while (level < 0) {

            // Iterate through subtree
            if (node.left != null)
                node = node.left;
            else if (node.right != null)
                node = node.right;
            else

                // if no child are there, we cannot have right
                // sibling in this path
                break;

            level++;
        }

        if (level == 0)
            return node;

        // This is the case when we reach 9 node in the tree,
        // where we need to again recursively find the right
        // sibling
        return findRightSibling(node, level);
    }

    let root = new Node(1, null);
    root.left = new Node(2, root);
    root.right = new Node(3, root);
    root.left.left = new Node(4, root.left);
    root.left.right = new Node(6, root.left);
    root.left.left.left = new Node(7, root.left.left);
    root.left.left.left.left = new Node(10, root.left.left.left);
    root.left.right.right = new Node(9, root.left.right);
    root.right.right = new Node(5, root.right);
    root.right.right.right = new Node(8, root.right.right);
    root.right.right.right.right = new Node(12, root.right.right.right);

    // passing 10
    document.write(findRightSibling(root.left.left.left.left, 0).data);

   // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
12
```

**时间复杂度:** O(N)

**辅助空间:** O(1)

本文由**克里希纳·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。