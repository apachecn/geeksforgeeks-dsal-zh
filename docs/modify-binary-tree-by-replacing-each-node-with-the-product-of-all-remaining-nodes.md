# 通过用所有剩余节点的乘积替换每个节点来修改二叉树

> 原文:[https://www . geesforgeks . org/modify-二叉树-通过用所有剩余节点的乘积替换每个节点/](https://www.geeksforgeeks.org/modify-binary-tree-by-replacing-each-node-with-the-product-of-all-remaining-nodes/)

给定一个由 **N** 个节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是用所有剩余节点的乘积替换树的每个节点。

**示例:**

> **输入:**
> 1
> /\
> 2 3
> /\
> 4 5
> **输出:**
> 120
> /\
> 60 40
> /\
> 30 24
> 
> **输入:**
> 2
> / \
> 2 3
> **输出:**
> 6
> / \
> 6 4

**方法:**首先计算[给定树](https://www.geeksforgeeks.org/product-of-all-nodes-in-a-binary-tree/)中所有节点的乘积，然后对给定树执行[任意树遍历，并用值 **(P/(根- >值)**更新每个节点，即可解决给定问题。按照以下步骤解决问题:](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)

*   [使用](https://www.geeksforgeeks.org/product-of-all-nodes-in-a-binary-tree/)[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)找到二叉树的所有节点的乘积，并将其存储在一个变量中，比如 **P** 。
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，说**更新树(根，P)** ，执行以下步骤:
    *   如果**根**的值为**空**，则从函数返回。
    *   将根节点的当前值更新为值**(P/根- >值)**。
    *   [递归调用左右子树的](https://www.geeksforgeeks.org/recursion/)为**更新树(根- >左，P)** 和**更新树(根- >右，P)** 。
*   完成上述步骤后，打印修改后的树的[有序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// A Tree node
class Node {
public:
    int data;
    Node *left, *right;

    // Constructor
    Node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function to create a new node in
// the given Tree
Node* newNode(int value)
{
    Node* temp = new Node(value);
    return (temp);
}

// Function to find the product of
// all the nodes in the given Tree
int findProduct(Node* root)
{
    // Base Case
    if (root == NULL)
        return 1;

    // Recursively Call for the left
    // and the right subtree
    return (root->data
            * findProduct(root->left)
            * findProduct(root->right));
}

// Function to perform the Inorder
// traversal of the given tree
void display(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Recursively call for the
    // left subtree
    display(root->left);

    // Print the value
    cout << root->data << " ";

    // Recursively call for the
    // right subtree
    display(root->right);
}

// Function to convert the given tree
// to the multiplication tree
void convertTree(int product,
                 Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Divide the total product by
    // the root's data
    root->data = product / (root->data);

    // Go to the left subtree
    convertTree(product, root->left);

    // Go to the right subtree
    convertTree(product, root->right);
}

// Driver Code
int main()
{
    // Given Binary Tree
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);

    root->right->left = newNode(4);
    root->right->right = newNode(5);

    cout << "Inorder Traversal of "
         << "given Tree:\n";

    // Print the tree traversal
    display(root);

    int product = findProduct(root);

    cout << "\nInorder Traversal of "
         << "given Tree:\n";

    // Function Call
    convertTree(product, root);

    // Print the tree traversal
    display(root);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# A Tree node
class Node:

    def __init__(self, d):

        self.data = d
        self.left = None
        self.right = None

# Function to find the product of
# all the nodes in the given Tree
def findProduct(root):

    # Base Case
    if (root == None):
        return 1

    # Recursively Call for the left
    # and the right subtree
    return (root.data * findProduct(root.left) *
                        findProduct(root.right))

# Function to perform the Inorder
# traversal of the given tree
def display(root):

    # Base Case
    if (root == None):
        return

    # Recursively call for the
    # left subtree
    display(root.left)

    # Print the value
    print(root.data, end = " ")

    # Recursively call for the
    # right subtree
    display(root.right)

# Function to convert the given tree
# to the multiplication tree
def convertTree(product, root):

    # Base Case
    if (root == None):
        return

    # Divide the total product by
    # the root's data
    root.data = product // (root.data)

    # Go to the left subtree
    convertTree(product, root.left)

    # Go to the right subtree
    convertTree(product, root.right)

# Driver Code
if __name__ == '__main__':

    # Given Binary Tree
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(5)

    print("Inorder Traversal of given Tree: ")

    # Print the tree traversal
    display(root)

    product = findProduct(root)

    print("\nInorder Traversal of given Tree:")

    # Function Call
    convertTree(product, root)

    # Print the tree traversal
    display(root)

# This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {
    // TreeNode class
    static class Node {
        public int data;
        public Node left, right;
    };

    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.data = key;
        temp.left = temp.right = null;
        return temp;
    }

    // Function to find the product of
    // all the nodes in the given Tree
    static int findProduct(Node root)
    {
        // Base Case
        if (root == null)
            return 1;

        // Recursively Call for the left
        // and the right subtree
        return (root.data * findProduct(root.left)
                * findProduct(root.right));
    }

    // Function to perform the Inorder
    // traversal of the given tree
    static void display(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Recursively call for the
        // left subtree
        display(root.left);

        // Print the value
        System.out.print(root.data + " ");

        // Recursively call for the
        // right subtree
        display(root.right);
    }

    // Function to convert the given tree
    // to the multiplication tree
    static void convertTree(int product, Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Divide the total product by
        // the root's data
        root.data = product / (root.data);

        // Go to the left subtree
        convertTree(product, root.left);

        // Go to the right subtree
        convertTree(product, root.right);
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Binary Tree
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);

        root.right.left = newNode(4);
        root.right.right = newNode(5);

        System.out.println("Inorder Traversal of "
                           + "given Tree:");

        // Print the tree traversal
        display(root);

        int product = findProduct(root);

        System.out.println("\nInorder Traversal of "
                           + "given Tree:");

        // Function Call
        convertTree(product, root);

        // Print the tree traversal
        display(root);
    }
}
// This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

public class GFG {
    // TreeNode class
    class Node {
        public int data;
        public Node left, right;
    };

    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.data = key;
        temp.left = temp.right = null;
        return temp;
    }

    // Function to find the product of
    // all the nodes in the given Tree
    static int findProduct(Node root)
    {
        // Base Case
        if (root == null)
            return 1;

        // Recursively Call for the left
        // and the right subtree
        return (root.data * findProduct(root.left)
                * findProduct(root.right));
    }

    // Function to perform the Inorder
    // traversal of the given tree
    static void display(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Recursively call for the
        // left subtree
        display(root.left);

        // Print the value
        Console.Write(root.data + " ");

        // Recursively call for the
        // right subtree
        display(root.right);
    }

    // Function to convert the given tree
    // to the multiplication tree
    static void convertTree(int product, Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Divide the total product by
        // the root's data
        root.data = product / (root.data);

        // Go to the left subtree
        convertTree(product, root.left);

        // Go to the right subtree
        convertTree(product, root.right);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Given Binary Tree
        Node root = newNode(1);
        root.left = newNode(2);
        root.right = newNode(3);

        root.right.left = newNode(4);
        root.right.right = newNode(5);

        Console.WriteLine("Inorder Traversal of "
                           + "given Tree:");

        // Print the tree traversal
        display(root);

        int product = findProduct(root);

        Console.WriteLine("\nInorder Traversal of "
                           + "given Tree:");

        // Function Call
        convertTree(product, root);

        // Print the tree traversal
        display(root);
    }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // TreeNode class
      class Node {
        constructor() {
          this.data = 0;
          this.left = null;
          this.right = null;
        }
      }

      function newNode(key) {
        var temp = new Node();
        temp.data = key;
        temp.left = temp.right = null;
        return temp;
      }

      // Function to find the product of
      // all the nodes in the given Tree
      function findProduct(root) {
        // Base Case
        if (root == null) return 1;

        // Recursively Call for the left
        // and the right subtree
        return root.data * findProduct(root.left) * findProduct(root.right);
      }

      // Function to perform the Inorder
      // traversal of the given tree
      function display(root) {
        // Base Case
        if (root == null) return;

        // Recursively call for the
        // left subtree
        display(root.left);

        // Print the value
        document.write(root.data + " ");

        // Recursively call for the
        // right subtree
        display(root.right);
      }

      // Function to convert the given tree
      // to the multiplication tree
      function convertTree(product, root) {
        // Base Case
        if (root == null) return;

        // Divide the total product by
        // the root's data
        root.data = parseInt(product / root.data);

        // Go to the left subtree
        convertTree(product, root.left);

        // Go to the right subtree
        convertTree(product, root.right);
      }

      // Driver code
      // Given Binary Tree
      var root = newNode(1);
      root.left = newNode(2);
      root.right = newNode(3);

      root.right.left = newNode(4);
      root.right.right = newNode(5);

      document.write("Inorder Traversal of " + "given Tree: <br>");

      // Print the tree traversal
      display(root);

      var product = findProduct(root);

      document.write("<br>Inorder Traversal of " + "given Tree:<br>");

      // Function Call
      convertTree(product, root);

      // Print the tree traversal
      display(root);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
Inorder Traversal of given Tree:
2 1 4 3 5 
Inorder Traversal of given Tree:
60 120 30 40 24
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)