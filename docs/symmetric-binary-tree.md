# 对称二叉树

> 原文:[https://www.geeksforgeeks.org/symmetric-binary-tree/](https://www.geeksforgeeks.org/symmetric-binary-tree/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，检查它是否是自身的镜像。

**例:**

```
Input:
      5
    /   \
   3     3
  / \   / \
 8   9 9   8

Output: Symmetric

Input:
     5
   /   \
  8     7
   \     \
   4      3
Output: Not Symmetric   
```

**方法:**想法是使用[莫里斯遍历](https://www.geeksforgeeks.org/morris-traversal-for-preorder/)和[反向莫里斯遍历](https://www.geeksforgeeks.org/reverse-morris-traversal-using-threaded-binary-tree/)遍历树，遍历给定的二叉树，并在每一步检查当前节点的数据在两次遍历中是否相等。如果在任何步骤中节点的数据不同。那么，给定的树不是对称二叉树。

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// if Tree is symmetric or not

#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;

    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};

// Function to check if the given
// binary tree is Symmetric or not
bool isSymmetric(struct Node* root)
{
    Node *curr1 = root, *curr2 = root;

    // Loop to traverse the tree in
    // Morris Traversal and
    // Reverse Morris Traversal
    while (curr1 != NULL
           && curr2 != NULL) {

        if (curr1->left == NULL
            && curr2->right == NULL) {

            if (curr1->data != curr2->data)
                return false;

            curr1 = curr1->right;
            curr2 = curr2->left;
        }

        else if (curr1->left != NULL
                 && curr2->right != NULL) {

            Node* pre1 = curr1->left;
            Node* pre2 = curr2->right;

            while (pre1->right != NULL
                   && pre1->right != curr1
                   && pre2->left != NULL
                   && pre2->left != curr2) {
                pre1 = pre1->right;
                pre2 = pre2->left;
            }

            if (pre1->right == NULL
                && pre2->left == NULL) {

                // Here, we are threading the Node
                pre1->right = curr1;
                pre2->left = curr2;
                curr1 = curr1->left;
                curr2 = curr2->right;
            }

            else if (pre1->right == curr1
                     && pre2->left == curr2) {

                // Unthreading the nodes
                pre1->right = NULL;
                pre2->left = NULL;

                if (curr1->data != curr2->data)
                    return false;
                curr1 = curr1->right;
                curr2 = curr2->left;
            }
            else
                return false;
        }
        else
            return false;
    }

    if (curr1 != curr2)
        return false;

    return true;
}

// Driver Code
int main()
{
    /*
         5
       /   \
      3     3
     / \   / \
    8   9 9   8    */

    // Creation of Binary tree
    Node* root = new Node(5);
    root->left = new Node(3);
    root->right = new Node(3);
    root->left->left = new Node(8);
    root->left->right = new Node(9);
    root->right->left = new Node(9);
    root->right->right = new Node(8);

    if (isSymmetric(root))
        cout << "Symmetric";
    else
        cout << "Not Symmetric";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if Tree is symmetric or not
class GFG{

// A Binary Tree Node
static class Node
{
    int data;
    Node left;
    Node right;

    Node(int val)
    {
        data = val;
        left = right = null;
    }
};

// Function to check if the given
// binary tree is Symmetric or not
static boolean isSymmetric(Node root)
{
    Node curr1 = root, curr2 = root;

    // Loop to traverse the tree in
    // Morris Traversal and
    // Reverse Morris Traversal
    while (curr1 != null &&
           curr2 != null)
    {

        if (curr1.left == null &&
            curr2.right == null)
        {

            if (curr1.data != curr2.data)
                return false;

            curr1 = curr1.right;
            curr2 = curr2.left;
        }

        else if (curr1.left != null &&
                 curr2.right != null)
        {
            Node pre1 = curr1.left;
            Node pre2 = curr2.right;

            while (pre1.right != null &&
                   pre1.right != curr1 &&
                   pre2.left != null &&
                   pre2.left != curr2)
            {
                pre1 = pre1.right;
                pre2 = pre2.left;
            }

            if (pre1.right == null &&
                pre2.left == null)
            {

                // Here, we are threading the Node
                pre1.right = curr1;
                pre2.left = curr2;
                curr1 = curr1.left;
                curr2 = curr2.right;
            }

            else if (pre1.right == curr1 &&
                     pre2.left == curr2)
            {

                // Unthreading the nodes
                pre1.right = null;
                pre2.left = null;

                if (curr1.data != curr2.data)
                    return false;
                curr1 = curr1.right;
                curr2 = curr2.left;
            }
            else
                return false;
        }
        else
            return false;
    }

    if (curr1 != curr2)
        return false;

    return true;
}

// Driver Code
public static void main(String[] args)
{
    /*
         5
       /   \
      3     3
     / \   / \
    8   9 9   8    */

    // Creation of Binary tree
    Node root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(3);
    root.left.left = new Node(8);
    root.left.right = new Node(9);
    root.right.left = new Node(9);
    root.right.right = new Node(8);

    if (isSymmetric(root))
        System.out.print("Symmetric");
    else
        System.out.print("Not Symmetric");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to check
# if Tree is symmetric or not

# A Binary Tree Node
class Node:
    def __init__(self, val):

        self.data = val
        self.left = self.right = None

# Function to check if the given
# binary tree is Symmetric or not
def isSymmetric(root):
    curr1 = root
    curr2 = root

    # Loop to traverse the tree in
    # Morris Traversal and
    # Reverse Morris Traversal
    while curr1 != None and curr2 != None:

        if (curr1.left == None and
            curr2.right == None):

            if curr1.data != curr2.data:
                return False

            curr1 = curr1.right
            curr2 = curr2.left

        elif curr1 != None and curr2 != None:
            pre1 = curr1.left
            pre2 = curr2.right

            while (pre1.right != None and
                   pre1.right != curr1 and
                   pre2.left != None and
                   pre2.left != curr2):
                pre1 = pre1.right
                pre2 = pre2.left

            if pre1.right == None and pre2.left == None:

                # Here, we are threading the Node
                pre1.right = curr1
                pre2.left = curr2
                curr1 = curr1.left
                curr2 = curr2.right

            elif (pre1.right == curr1 and
                  pre2.left == curr2):

                # Unthreading the nodes
                pre1.right = None
                pre2.left = None

                if curr1.data != curr2.data:
                    return False

                curr1 = curr1.right
                curr2 = curr2.left
            else:
                return False

        else:
            return False

    if curr1 != curr2:
        return False

    return True

# Driver code
def main():

    #
    #      5
    #     / \
    #  3     3
    # / \   / \
    #8   9 9   8

    # Creation of Binary tree
    root = Node(5)
    root.left = Node(3)
    root.right = Node(3)
    root.left.left = Node(8)
    root.left.right = Node(9)
    root.right.left = Node(9)
    root.right.right = Node(8)

    if isSymmetric(root):
        print("Symmetric")
    else:
        print("Not Symmetric")
main()

# This code is contributed by Stuti Pathak
```

## C#

```
// C# implementation to check
// if Tree is symmetric or not
using System;

class GFG{

// A Binary Tree Node
class Node
{
    public int data;
    public Node left;
    public Node right;

    public Node(int val)
    {
        data = val;
        left = right = null;
    }
};

// Function to check if the given
// binary tree is Symmetric or not
static bool isSymmetric(Node root)
{
    Node curr1 = root, curr2 = root;

    // Loop to traverse the tree in
    // Morris Traversal and
    // Reverse Morris Traversal
    while (curr1 != null &&
           curr2 != null)
    {
        if (curr1.left == null &&
           curr2.right == null)
        {
            if (curr1.data != curr2.data)
                return false;

            curr1 = curr1.right;
            curr2 = curr2.left;
        }

        else if (curr1.left != null &&
                curr2.right != null)
        {
            Node pre1 = curr1.left;
            Node pre2 = curr2.right;

            while (pre1.right != null &&
                   pre1.right != curr1 &&
                    pre2.left != null &&
                    pre2.left != curr2)
            {
                pre1 = pre1.right;
                pre2 = pre2.left;
            }

            if (pre1.right == null &&
                 pre2.left == null)
            {

                // Here, we are threading the Node
                pre1.right = curr1;
                pre2.left = curr2;
                curr1 = curr1.left;
                curr2 = curr2.right;
            }

            else if (pre1.right == curr1 &&
                      pre2.left == curr2)
            {

                // Unthreading the nodes
                pre1.right = null;
                pre2.left = null;

                if (curr1.data != curr2.data)
                    return false;

                curr1 = curr1.right;
                curr2 = curr2.left;
            }
            else
                return false;
        }
        else
            return false;
    }

    if (curr1 != curr2)
        return false;

    return true;
}

// Driver Code
public static void Main(String[] args)
{
    /*
         5
       /   \
      3        3
     / \   / \
    8   9 9   8 */

    // Creation of Binary tree
    Node root = new Node(5);
    root.left = new Node(3);
    root.right = new Node(3);
    root.left.left = new Node(8);
    root.left.right = new Node(9);
    root.right.left = new Node(9);
    root.right.right = new Node(8);

    if (isSymmetric(root))
        Console.Write("Symmetric");
    else
        Console.Write("Not Symmetric");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation to check
    // if Tree is symmetric or not

    // A Binary Tree Node
    class Node
    {
        constructor(val) {
           this.left = null;
           this.right = null;
           this.data = val;
        }
    }

    // Function to check if the given
    // binary tree is Symmetric or not
    function isSymmetric(root)
    {
        let curr1 = root, curr2 = root;

        // Loop to traverse the tree in
        // Morris Traversal and
        // Reverse Morris Traversal
        while (curr1 != null &&
               curr2 != null)
        {
            if (curr1.left == null &&
               curr2.right == null)
            {
                if (curr1.data != curr2.data)
                    return false;

                curr1 = curr1.right;
                curr2 = curr2.left;
            }

            else if (curr1.left != null &&
                    curr2.right != null)
            {
                let pre1 = curr1.left;
                let pre2 = curr2.right;

                while (pre1.right != null &&
                       pre1.right != curr1 &&
                        pre2.left != null &&
                        pre2.left != curr2)
                {
                    pre1 = pre1.right;
                    pre2 = pre2.left;
                }

                if (pre1.right == null &&
                     pre2.left == null)
                {

                    // Here, we are threading the Node
                    pre1.right = curr1;
                    pre2.left = curr2;
                    curr1 = curr1.left;
                    curr2 = curr2.right;
                }

                else if (pre1.right == curr1 &&
                          pre2.left == curr2)
                {

                    // Unthreading the nodes
                    pre1.right = null;
                    pre2.left = null;

                    if (curr1.data != curr2.data)
                        return false;

                    curr1 = curr1.right;
                    curr2 = curr2.left;
                }
                else
                    return false;
            }
            else
                return false;
        }

        if (curr1 != curr2)
            return false;

        return true;
    }

    /*
         5
       /   \
      3        3
     / \   / \
    8   9 9   8 */

  // Creation of Binary tree
  let root = new Node(5);
  root.left = new Node(3);
  root.right = new Node(3);
  root.left.left = new Node(8);
  root.left.right = new Node(9);
  root.right.left = new Node(9);
  root.right.right = new Node(8);

  if (isSymmetric(root))
    document.write("Symmetric");
  else
    document.write("Not Symmetric");

</script>
```

**输出:**

```
Symmetric
```

**时间复杂度:**由于树的每条边最多被遍历两次，这与 Morris 遍历的情况完全一样，在最坏的情况下，创建和移除相同数量的额外边(作为输入树)。因此，这种方法的时间复杂度为 **O(N)** 。

**辅助空间:** O(1)