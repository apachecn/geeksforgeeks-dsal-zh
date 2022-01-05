# 在 BST |迭代方法

中为给定的键指定前置和后续

> 原文:[https://www . geeksforgeeks . org/in order-preference-and-后继-for-a-给定-key-in-BST-iterative-approach/](https://www.geeksforgeeks.org/inorder-predecessor-and-successor-for-a-given-key-in-bst-iterative-approach/)

给定一个 BST 和一把钥匙。任务是找到给定键的顺序后继和前置。在这种情况下，如果前任或继任者都不存在，则打印-1。
**例:**

```
Input:          50
               /  \
              /    \
            30     70
           / \     / \
          /   \   /   \
         20   40 60   80
            key = 65
Output: Predecessor : 60
        Successor : 70

Input:          50
               /  \
              /    \
            30     70
           / \     / \
          /   \   /   \
         20   40 60   80
            key = 100
Output: predecessor : 80
        successor : -1
Explanation: As no node in BST has key value greater 
than 100 so -1 is printed for successor.
```

在[之前的](https://www.geeksforgeeks.org/inorder-predecessor-successor-given-key-bst/)帖子中，已经讨论了递归解决方案。这个问题可以用迭代的方法来解决。为了解决这个问题，必须处理搜索密钥时的三种情况，如下所述:

1.  **根是给定的键**:这种情况下，如果左子树不为 NULL，那么前置是左子树中最右边的节点，如果右子树不为 NULL，那么后继是右子树中最左边的节点。
2.  **根大于键**:这种情况下，键出现在根的左子树中。因此，通过设置 root = root- > left 来搜索左子树中的键。请注意，root 可能是给定密钥的后续。如果键没有正确的子树，根将是它的后继。
3.  **根小于键**:这种情况下，键出现在根的右子树中。因此，通过设置 root = root- > right 来搜索右子树中的键。请注意，根可以是给定键的更高级的前身。如果键没有左子树，根将是它的前身。

下面是上述方法的实现:

## C++

```
// C++ program to find predecessor
// and successor in a BST
#include <bits/stdc++.h>
using namespace std;

// BST Node
struct Node {
    int key;
    struct Node *left, *right;
};

// Function that finds predecessor and successor of key in BST.
void findPreSuc(Node* root, Node*& pre, Node*& suc, int key)
{
    if (root == NULL)
        return;

    // Search for given key in BST.
    while (root != NULL) {

        // If root is given key.
        if (root->key == key) {

            // the minimum value in right subtree
            // is predecessor.
            if (root->right) {
                suc = root->right;
                while (suc->left)
                    suc = suc->left;
            }

            // the maximum value in left subtree
            // is successor.
            if (root->left) {
                pre = root->left;
                while (pre->right)
                    pre = pre->right;
            }

            return;
        }

        // If key is greater than root, then
        // key lies in right subtree. Root
        // could be predecessor if left
        // subtree of key is null.
        else if (root->key < key) {
            pre = root;
            root = root->right;
        }

        // If key is smaller than root, then
        // key lies in left subtree. Root
        // could be successor if right
        // subtree of key is null.
        else {
            suc = root;
            root = root->left;
        }
    }
}

// A utility function to create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to insert
// a new node with given key in BST
Node* insert(Node* node, int key)
{
    if (node == NULL)
        return newNode(key);
    if (key < node->key)
        node->left = insert(node->left, key);
    else
        node->right = insert(node->right, key);
    return node;
}

// Driver program to test above function
int main()
{
    int key = 65; // Key to be searched in BST

    /* Let us create following BST
                 50
                /  \
               /    \
              30     70
             / \     / \
            /   \   /   \
           20   40 60   80
*/
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    Node *pre = NULL, *suc = NULL;

    findPreSuc(root, pre, suc, key);
    if (pre != NULL)
        cout << "Predecessor is " << pre->key << endl;
    else
        cout << "-1";

    if (suc != NULL)
        cout << "Successor is " << suc->key;
    else
        cout << "-1";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find predecessor
// and successor in a BST
import java.util.*;
class GFG
{

// BST Node
static class Node
{
    int key;
    Node left, right;
};
static Node pre;
static Node suc;

// Function that finds predecessor
// and successor of key in BST.
static void findPreSuc(Node root, int key)
{
    if (root == null)
        return;

    // Search for given key in BST.
    while (root != null)
    {

        // If root is given key.
        if (root.key == key)
        {

            // the minimum value in right subtree
            // is successor.
            if (root.right != null)
            {
                suc = root.right;
                while (suc.left != null)
                    suc = suc.left;
            }

            // the maximum value in left subtree
            // is predecessor.
            if (root.left != null)
            {
                pre = root.left;
                while (pre.right != null)
                    pre = pre.right;
            }
            return;
        }

        // If key is greater than root, then
        // key lies in right subtree. Root
        // could be predecessor if left
        // subtree of key is null.
        else if (root.key < key)
        {
            pre = root;
            root = root.right;
        }

        // If key is smaller than root, then
        // key lies in left subtree. Root
        // could be successor if right
        // subtree of key is null.
        else
        {
            suc = root;
            root = root.left;
        }
    }
}

// A utility function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert
// a new node with given key in BST
static Node insert(Node node, int key)
{
    if (node == null)
        return newNode(key);
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);
    return node;
}

// Driver Code
public static void main(String[] args)
{
    int key = 65; // Key to be searched in BST

    /* Let us create following BST
                50
                / \
            / \
            30     70
            / \     / \
            / \ / \
        20 40 60 80
    */
    Node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    findPreSuc(root, key);
    if (pre != null)
        System.out.println("Predecessor is " +
                                     pre.key);
    else
        System.out.print("-1");

    if (suc != null)
        System.out.print("Successor is " + suc.key);
    else
        System.out.print("-1");
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find predecessor
# and successor in a BST

# A utility function to create a
# new BST node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# Function that finds predecessor and
# successor of key in BST.
def findPreSuc(root, pre, suc, key):
    if root == None:
        return

    # Search for given key in BST.
    while root != None:

        # If root is given key.
        if root.key == key:

            # the minimum value in right
            # subtree is predecessor.
            if root.right:
                suc[0] = root.right
                while suc[0].left:
                    suc[0] = suc[0].left

            # the maximum value in left
            # subtree is successor.
            if root.left:
                pre[0] = root.left
                while pre[0].right:
                    pre[0] = pre[0].right

            return

        # If key is greater than root, then
        # key lies in right subtree. Root
        # could be predecessor if left
        # subtree of key is null.
        elif root.key < key:
            pre[0] = root
            root = root.right

        # If key is smaller than root, then
        # key lies in left subtree. Root
        # could be successor if right
        # subtree of key is null.
        else:
            suc[0] = root
            root = root.left

# A utility function to insert
# a new node with given key in BST
def insert(node, key):
    if node == None:
        return newNode(key)
    if key < node.key:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)
    return node

# Driver Code
if __name__ == '__main__':
    key = 65 # Key to be searched in BST

    # Let us create following BST
    #             50
    #         / \
    #         / \
    #         30     70
    #         / \     / \
    #     / \ / \
    #     20 40 60 80

    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)

    pre, suc = [None], [None]

    findPreSuc(root, pre, suc, key)
    if pre[0] != None:
        print("Predecessor is", pre[0].key)
    else:
        print("-1")

    if suc[0] != None:
        print("Successor is", suc[0].key)
    else:
        print("-1")

# This code is contributed by PranchalK
```

## C#

```
// C# program to find predecessor
// and successor in a BST
using System;

class GFG
{

// BST Node
class Node
{
    public int key;
    public Node left, right;
};
static Node pre;
static Node suc;

// Function that finds predecessor
// and successor of key in BST.
static void findPreSuc(Node root, int key)
{
    if (root == null)
        return;

    // Search for given key in BST.
    while (root != null)
    {

        // If root is given key.
        if (root.key == key)
        {

            // the minimum value in right subtree
            // is predecessor.
            if (root.right != null)
            {
                suc = root.right;
                while (suc.left != null)
                    suc = suc.left;
            }

            // the maximum value in left subtree
            // is successor.
            if (root.left != null)
            {
                pre = root.left;
                while (pre.right != null)
                    pre = pre.right;
            }
            return;
        }

        // If key is greater than root, then
        // key lies in right subtree. Root
        // could be predecessor if left
        // subtree of key is null.
        else if (root.key < key)
        {
            pre = root;
            root = root.right;
        }

        // If key is smaller than root, then
        // key lies in left subtree. Root
        // could be successor if right
        // subtree of key is null.
        else
        {
            suc = root;
            root = root.left;
        }
    }
}

// A utility function to create a new BST node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert
// a new node with given key in BST
static Node insert(Node node, int key)
{
    if (node == null)
        return newNode(key);
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);
    return node;
}

// Driver Code
public static void Main(String[] args)
{
    int key = 65; // Key to be searched in BST

    /* Let us create following BST
                50
                / \
            / \
            30     70
            / \     / \
            / \ / \
        20 40 60 80
    */
    Node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    findPreSuc(root, key);
    if (pre != null)
        Console.WriteLine("Predecessor is " +
                                    pre.key);
    else
        Console.Write("-1");

    if (suc != null)
        Console.Write("Successor is " + suc.key);
    else
        Console.Write("-1");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to find predecessor
// and successor in a BST

// BST Node
class Node {
    constructor(val) {
        this.key = val;
        this.left = null;
        this.right = null;
    }
}
var pre;
var suc;

// Function that finds predecessor
// and successor of key in BST.
function findPreSuc(root , key)
{
    if (root == null)
        return;

    // Search for given key in BST.
    while (root != null)
    {

        // If root is given key.
        if (root.key == key)
        {

            // the minimum value in right subtree
            // is successor.
            if (root.right != null)
            {
                suc = root.right;
                while (suc.left != null)
                    suc = suc.left;
            }

            // the maximum value in left subtree
            // is predecessor.
            if (root.left != null)
            {
                pre = root.left;
                while (pre.right != null)
                    pre = pre.right;
            }
            return;
        }

        // If key is greater than root, then
        // key lies in right subtree. Root
        // could be predecessor if left
        // subtree of key is null.
        else if (root.key < key)
        {
            pre = root;
            root = root.right;
        }

        // If key is smaller than root, then
        // key lies in left subtree. Root
        // could be successor if right
        // subtree of key is null.
        else
        {
            suc = root;
            root = root.left;
        }
    }
}

// A utility function to create a new BST node
function newNode(item)
{
    var temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert
// a new node with given key in BST
function insert(node , key)
{
    if (node == null)
        return newNode(key);
    if (key < node.key)
        node.left = insert(node.left, key);
    else
        node.right = insert(node.right, key);
    return node;
}

// Driver Code

    var key = 65; // Key to be searched in BST

    /* Let us create following BST
                50
                / \
            / \
            30     70
            / \     / \
            / \ / \
        20 40 60 80
    */
    var root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    findPreSuc(root, key);
    if (pre != null)
        document.write("Predecessor is " +
                                     pre.key+"<br/>");
    else
        document.write("-1<br/>");

    if (suc != null)
        document.write("Successor is " + suc.key);
    else
        document.write("-1");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Predecessor is 60
Successor is 70
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
**相关文章**:[https://www . geekes forgeeks . org/inoder-previous-后继-given-key-bst/](https://www.geeksforgeeks.org/inorder-predecessor-successor-given-key-bst/)