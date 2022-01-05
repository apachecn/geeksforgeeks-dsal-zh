# 从给定的前序遍历|集合 1

构建 BST

> 原文:[https://www . geesforgeks . org/construct-BST-from-given-preorder-traversa/](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)

给定二叉查找树的前序遍历，构造 BST。

**例如**，如果给定的遍历是{10，5，1，7，40，50}，那么输出应该是下面树的根。

```
     10
   /   \
  5     40
 /  \      \
1    7      50
```

**方法 1 ( O(n <sup>2</sup> )时间复杂度)**
前序遍历的第一个元素永远是根。我们首先构造根。然后我们找到大于根的第一个元素的索引。让索引为“I”。根和“I”之间的值将是左子树的一部分，“I”(包括)和“n-1”之间的值将是右子树的一部分。在索引“I”处划分给定的 pre[]并对左右子树重复。

**例如**在{10，5，1，7，40，50}中，10 是第一个元素，所以我们把它做成 root。现在我们寻找大于 10 的第一个元素，我们找到 40。所以我们知道 BST 的结构如下。

```
             10
           /    \
          /      \
  {5, 1, 7}       {40, 50}
```

对于子阵列{5，1，7}和{40，50}，我们递归地遵循上述步骤，并获得完整的树。

## C++

```
/* A O(n^2) program for construction of BST from preorder
 * traversal */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node {
public:
    int data;
    node* left;
    node* right;
};

// A utility function to create a node
node* newNode(int data)
{
    node* temp = new node();

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct Full from pre[].
// preIndex is used to keep track of index in pre[].
node* constructTreeUtil(int pre[], int* preIndex, int low,
                        int high, int size)
{
    // Base case
    if (*preIndex >= size || low > high)
        return NULL;

    // The first node in preorder traversal is root. So take
    // the node at preIndex from pre[] and make it root, and
    // increment preIndex
    node* root = newNode(pre[*preIndex]);
    *preIndex = *preIndex + 1;

    // If the current subarray has only one element, no need
    // to recur
    if (low == high)
        return root;

    // Search for the first element greater than root
    int i;
    for (i = low; i <= high; ++i)
        if (pre[i] > root->data)
            break;

    // Use the index of element found in preorder to divide
    // preorder array in two parts. Left subtree and right
    // subtree
    root->left = constructTreeUtil(pre, preIndex, *preIndex,
                                   i - 1, size);
    root->right
        = constructTreeUtil(pre, preIndex, i, high, size);

    return root;
}

// The main function to construct BST from given preorder
// traversal. This function mainly uses constructTreeUtil()
node* constructTree(int pre[], int size)
{
    int preIndex = 0;
    return constructTreeUtil(pre, &preIndex, 0, size - 1,
                             size);
}

// A utility function to print inorder traversal of a Binary
// Tree
void printInorder(node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

// Driver code
int main()
{
    int pre[] = { 10, 5, 1, 7, 40, 50 };
    int size = sizeof(pre) / sizeof(pre[0]);

    node* root = constructTree(pre, size);

    cout << "Inorder traversal of the constructed tree: \n";
    printInorder(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
/* A O(n^2) program for construction of BST from preorder
 * traversal */
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// A utility function to create a node
struct node* newNode(int data)
{
    struct node* temp
        = (struct node*)malloc(sizeof(struct node));

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct Full from pre[].
// preIndex is used to keep track of index in pre[].
struct node* constructTreeUtil(int pre[], int* preIndex,
                               int low, int high, int size)
{
    // Base case
    if (*preIndex >= size || low > high)
        return NULL;

    // The first node in preorder traversal is root. So take
    // the node at preIndex from pre[] and make it root, and
    // increment preIndex
    struct node* root = newNode(pre[*preIndex]);
    *preIndex = *preIndex + 1;

    // If the current subarray has only one element, no need
    // to recur
    if (low == high)
        return root;

    // Search for the first element greater than root
    int i;
    for (i = low; i <= high; ++i)
        if (pre[i] > root->data)
            break;

    // Use the index of element found in preorder to divide
    // preorder array in two parts. Left subtree and right
    // subtree
    root->left = constructTreeUtil(pre, preIndex, *preIndex,
                                   i - 1, size);
    root->right
        = constructTreeUtil(pre, preIndex, i, high, size);

    return root;
}

// The main function to construct BST from given preorder
// traversal. This function mainly uses constructTreeUtil()
struct node* constructTree(int pre[], int size)
{
    int preIndex = 0;
    return constructTreeUtil(pre, &preIndex, 0, size - 1,
                             size);
}

// A utility function to print inorder traversal of a Binary
// Tree
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

// Driver code
int main()
{
    int pre[] = { 10, 5, 1, 7, 40, 50 };
    int size = sizeof(pre) / sizeof(pre[0]);

    struct node* root = constructTree(pre, size);

    printf("Inorder traversal of the constructed tree: \n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct BST from given preorder
// traversal

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class Index {

    int index = 0;
}

class BinaryTree {

    Index index = new Index();

    // A recursive function to construct Full from pre[].
    // preIndex is used to keep track of index in pre[].
    Node constructTreeUtil(int pre[], Index preIndex,
                           int low, int high, int size)
    {

        // Base case
        if (preIndex.index >= size || low > high) {
            return null;
        }

        // The first node in preorder traversal is root. So
        // take the node at preIndex from pre[] and make it
        // root, and increment preIndex
        Node root = new Node(pre[preIndex.index]);
        preIndex.index = preIndex.index + 1;

        // If the current subarray has only one element, no
        // need to recur
        if (low == high) {
            return root;
        }

        // Search for the first element greater than root
        int i;
        for (i = low; i <= high; ++i) {
            if (pre[i] > root.data) {
                break;
            }
        }

        // Use the index of element found in preorder to
        // divide preorder array in two parts. Left subtree
        // and right subtree
        root.left = constructTreeUtil(
            pre, preIndex, preIndex.index, i - 1, size);
        root.right = constructTreeUtil(pre, preIndex, i,
                                       high, size);

        return root;
    }

    // The main function to construct BST from given
    // preorder traversal. This function mainly uses
    // constructTreeUtil()
    Node constructTree(int pre[], int size)
    {
        return constructTreeUtil(pre, index, 0, size - 1,
                                 size);
    }

    // A utility function to print inorder traversal of a
    // Binary Tree
    void printInorder(Node node)
    {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[] { 10, 5, 1, 7, 40, 50 };
        int size = pre.length;
        Node root = tree.constructTree(pre, size);
        System.out.println(
            "Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# A O(n^2) Python3 program for
# construction of BST from preorder traversal

# A binary tree node

class Node():

    # A constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# constructTreeUtil.preIndex is a static variable of
# function constructTreeUtil

# Function to get the value of static variable
# constructTreeUtil.preIndex
def getPreIndex():
    return constructTreeUtil.preIndex

# Function to increment the value of static variable
# constructTreeUtil.preIndex

def incrementPreIndex():
    constructTreeUtil.preIndex += 1

# A recurseive function to construct Full from pre[].
# preIndex is used to keep track of index in pre[[].

def constructTreeUtil(pre, low, high):

        # Base Case
    if(low > high):
        return None

    # The first node in preorder traversal is root. So take
    # the node at preIndex from pre[] and make it root,
    # and increment preIndex
    root = Node(pre[getPreIndex()])
    incrementPreIndex()

    # If the current subarray has onlye one element,
    # no need to recur
    if low == high:
        return root

    r_root = -1

    # Search for the first element greater than root
    for i in range(low, high+1):
        if (pre[i] > root.data):
            r_root = i
            break

    # If no elements are greater than the current root,
    # all elements are left children
    # so assign root appropriately
    if r_root == -1:
        r_root = getPreIndex() + (high - low)

    # Use the index of element found in preorder to divide
    # preorder array in two parts. Left subtree and right
    # subtree
    root.left = constructTreeUtil(pre, getPreIndex(), r_root-1)

    root.right = constructTreeUtil(pre, r_root, high)

    return root

# The main function to construct BST from given preorder
# traversal. This function mailny uses constructTreeUtil()

def constructTree(pre):
    size = len(pre)
    constructTreeUtil.preIndex = 0
    return constructTreeUtil(pre, 0, size-1)

def printInorder(root):
    if root is None:
        return
    printInorder(root.left)
    print root.data,
    printInorder(root.right)

# Driver code
pre = [10, 5, 1, 7, 40, 50]

root = constructTree(pre)
print "Inorder traversal of the constructed tree:"
printInorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) and Rhys Compton
```

## C#

```
using System;

// C# program to construct BST from given preorder traversal
// A binary tree node
public class Node {

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class Index {

    public int index = 0;
}

public class BinaryTree {

    public Index index = new Index();

    // A recursive function to construct Full from pre[].
    // preIndex is used to keep track of index in pre[].
    public virtual Node constructTreeUtil(int[] pre,
                                          Index preIndex,
                                          int low, int high,
                                          int size)
    {

        // Base case
        if (preIndex.index >= size || low > high) {
            return null;
        }

        // The first node in preorder traversal is root. So
        // take the node at preIndex from pre[] and make it
        // root, and increment preIndex
        Node root = new Node(pre[preIndex.index]);
        preIndex.index = preIndex.index + 1;

        // If the current subarray has only one element, no
        // need to recur
        if (low == high) {
            return root;
        }

        // Search for the first element greater than root
        int i;
        for (i = low; i <= high; ++i) {
            if (pre[i] > root.data) {
                break;
            }
        }

        // Use the index of element found in preorder to
        // divide preorder array in two parts. Left subtree
        // and right subtree
        root.left = constructTreeUtil(
            pre, preIndex, preIndex.index, i - 1, size);
        root.right = constructTreeUtil(pre, preIndex, i,
                                       high, size);

        return root;
    }

    // The main function to construct BST from given
    // preorder traversal. This function mainly uses
    // constructTreeUtil()
    public virtual Node constructTree(int[] pre, int size)
    {
        return constructTreeUtil(pre, index, 0, size - 1,
                                 size);
    }

    // A utility function to print inorder traversal of a
    // Binary Tree
    public virtual void printInorder(Node node)
    {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int[] pre = new int[] { 10, 5, 1, 7, 40, 50 };
        int size = pre.Length;
        Node root = tree.constructTree(pre, size);
        Console.WriteLine(
            "Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

// This code is contributed by Shrikant13
```

**Output**

```
Inorder traversal of the constructed tree: 
1 5 7 10 40 50 
```

**时间复杂度:** O(n <sup>2</sup>

**方法 2 ( O(n)时间复杂度)**
这里使用的思路是受到[这个](https://www.geeksforgeeks.org/archives/3042)帖子的方法 3 的启发。诀窍是设置一个范围{min..最大值)。将范围初始化为{INT_MIN..INT_MAX}。第一个节点肯定在范围内，所以创建一个根节点。要构建左子树，请将范围设置为{INT_MIN …root- > data}。如果值在{ INT _ MIN 范围内..root- > data}，值是左子树的一部分。要构建右子树，请将范围设置为{根- >数据..最大..INT_MAX}。

下面是上述想法的实现:

## C++

```
/* A O(n) program for construction
of BST from preorder traversal */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class node {
public:
    int data;
    node* left;
    node* right;
};

// A utility function to create a node
node* newNode(int data)
{
    node* temp = new node();

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct
// BST from pre[]. preIndex is used
// to keep track of index in pre[].
node* constructTreeUtil(int pre[], int* preIndex, int key,
                        int min, int max, int size)
{
    // Base case
    if (*preIndex >= size)
        return NULL;

    node* root = NULL;

    // If current element of pre[] is in range, then
    // only it is part of current subtree
    if (key > min && key < max) {
        // Allocate memory for root of this
        // subtree and increment *preIndex
        root = newNode(key);
        *preIndex = *preIndex + 1;

        if (*preIndex < size) {
            // Construct the subtree under root
            // All nodes which are in range
            // {min .. key} will go in left
            // subtree, and first such node
            // will be root of left subtree.
            root->left = constructTreeUtil(pre, preIndex,
                                           pre[*preIndex],
                                           min, key, size);
        }
        if (*preIndex < size) {
            // All nodes which are in range
            // {key..max} will go in right
            // subtree, and first such node
            // will be root of right subtree.
            root->right = constructTreeUtil(pre, preIndex,
                                            pre[*preIndex],
                                            key, max, size);
        }
    }

    return root;
}

// The main function to construct BST
// from given preorder traversal.
// This function mainly uses constructTreeUtil()
node* constructTree(int pre[], int size)
{
    int preIndex = 0;
    return constructTreeUtil(pre, &preIndex, pre[0],
                             INT_MIN, INT_MAX, size);
}

// A utility function to print inorder
// traversal of a Binary Tree
void printInorder(node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

// Driver code
int main()
{
    int pre[] = { 10, 5, 1, 7, 40, 50 };
    int size = sizeof(pre) / sizeof(pre[0]);

    // Function call
    node* root = constructTree(pre, size);

    cout << "Inorder traversal of the constructed tree: \n";
    printInorder(root);

    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
/* A O(n) program for construction of BST from preorder
 * traversal */
#include <limits.h>
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

// A utility function to create a node
struct node* newNode(int data)
{
    struct node* temp
        = (struct node*)malloc(sizeof(struct node));

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// A recursive function to construct BST from pre[].
// preIndex is used to keep track of index in pre[].
struct node* constructTreeUtil(int pre[], int* preIndex,
                               int key, int min, int max,
                               int size)
{
    // Base case
    if (*preIndex >= size)
        return NULL;

    struct node* root = NULL;

    // If current element of pre[] is in range, then
    // only it is part of current subtree
    if (key > min && key < max) {
        // Allocate memory for root of this subtree and
        // increment *preIndex
        root = newNode(key);
        *preIndex = *preIndex + 1;

        if (*preIndex < size) {
            // Construct the subtree under root
            // All nodes which are in range {min .. key}
            // will go in left subtree, and first such node
            // will be root of left subtree.
            root->left = constructTreeUtil(pre, preIndex,
                                           pre[*preIndex],
                                           min, key, size);
        }
        if (*preIndex < size) {
            // All nodes which are in range {key..max} will
            // go in right subtree, and first such node will
            // be root of right subtree.
            root->right = constructTreeUtil(pre, preIndex,
                                            pre[*preIndex],
                                            key, max, size);
        }
    }

    return root;
}

// The main function to construct BST from given preorder
// traversal. This function mainly uses constructTreeUtil()
struct node* constructTree(int pre[], int size)
{
    int preIndex = 0;
    return constructTreeUtil(pre, &preIndex, pre[0],
                             INT_MIN, INT_MAX, size);
}

// A utility function to print inorder traversal of a Binary
// Tree
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->data);
    printInorder(node->right);
}

// Driver code
int main()
{
    int pre[] = { 10, 5, 1, 7, 40, 50 };
    int size = sizeof(pre) / sizeof(pre[0]);

    // function call
    struct node* root = constructTree(pre, size);

    printf("Inorder traversal of the constructed tree: \n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct BST from given preorder
// traversal

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class Index {

    int index = 0;
}

class BinaryTree {

    Index index = new Index();

    // A recursive function to construct BST from pre[].
    // preIndex is used to keep track of index in pre[].
    Node constructTreeUtil(int pre[], Index preIndex,
                           int key, int min, int max,
                           int size)
    {

        // Base case
        if (preIndex.index >= size) {
            return null;
        }

        Node root = null;

        // If current element of pre[] is in range, then
        // only it is part of current subtree
        if (key > min && key < max) {

            // Allocate memory for root of this
            // subtree and increment *preIndex
            root = new Node(key);
            preIndex.index = preIndex.index + 1;

            if (preIndex.index < size) {

                // Construct the subtree under root
                // All nodes which are in range {min .. key}
                // will go in left subtree, and first such
                // node will be root of left subtree.
                root.left = constructTreeUtil(
                    pre, preIndex, pre[preIndex.index], min,
                    key, size);
            }
            if (preIndex.index < size) {
                // All nodes which are in range {key..max}
                // will go in right subtree, and first such
                // node will be root of right subtree.
                root.right = constructTreeUtil(
                    pre, preIndex, pre[preIndex.index], key,
                    max, size);
            }
        }

        return root;
    }

    // The main function to construct BST from given
    // preorder traversal. This function mainly uses
    // constructTreeUtil()
    Node constructTree(int pre[], int size)
    {
        int preIndex = 0;
        return constructTreeUtil(pre, index, pre[0],
                                 Integer.MIN_VALUE,
                                 Integer.MAX_VALUE, size);
    }

    // A utility function to print inorder traversal of a
    // Binary Tree
    void printInorder(Node node)
    {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        int pre[] = new int[] { 10, 5, 1, 7, 40, 50 };
        int size = pre.length;

        // Function call
        Node root = tree.constructTree(pre, size);
        System.out.println(
            "Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# A O(n) program for construction of BST from preorder traversal

INT_MIN = float("-infinity")
INT_MAX = float("infinity")

# A Binary tree node

class Node:

    # Constructor to created a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Methods to get and set the value of static variable
# constructTreeUtil.preIndex for function construcTreeUtil()

def getPreIndex():
    return constructTreeUtil.preIndex

def incrementPreIndex():
    constructTreeUtil.preIndex += 1

# A recursive function to construct BST from pre[].
# preIndex is used to keep track of index in pre[]

def constructTreeUtil(pre, key, mini, maxi, size):

    # Base Case
    if(getPreIndex() >= size):
        return None

    root = None

    # If current element of pre[] is in range, then
    # only it is part of current subtree
    if(key > mini and key < maxi):

        # Allocate memory for root of this subtree
        # and increment constructTreeUtil.preIndex
        root = Node(key)
        incrementPreIndex()

        if(getPreIndex() < size):

            # Construct the subtree under root
            # All nodes which are in range {min.. key} will
            # go in left subtree, and first such node will
            # be root of left subtree
            root.left = constructTreeUtil(pre,
                                          pre[getPreIndex()],
                                          mini, key, size)
        if(getPreindex() < size):

            # All nodes which are in range{key..max} will
            # go to right subtree, and first such node will
            # be root of right subtree
            root.right = constructTreeUtil(pre,
                                           pre[getPreIndex()],
                                           key, maxi, size)

    return root

# This is the main function to construct BST from given
# preorder traversal. This function mainly uses
# constructTreeUtil()

def constructTree(pre):
    constructTreeUtil.preIndex = 0
    size = len(pre)
    return constructTreeUtil(pre, pre[0], INT_MIN, INT_MAX, size)

# A utility function to print inorder traversal of Binary Tree
def printInorder(node):

    if node is None:
        return
    printInorder(node.left)
    print node.data,
    printInorder(node.right)

# Driver code
pre = [10, 5, 1, 7, 40, 50]

# Function call
root = constructTree(pre)

print "Inorder traversal of the constructed tree: "
printInorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to construct BST from given preorder traversal
using System;

// A binary tree node
public class Node {

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class Index {
    public int index = 0;
}

public class BinaryTree {

    public Index index = new Index();

    // A recursive function to construct BST from pre[].
    // preIndex is used to keep track of index in pre[].
    public virtual Node constructTreeUtil(int[] pre,
                                          Index preIndex,
                                          int key, int min,
                                          int max, int size)
    {

        // Base case
        if (preIndex.index >= size) {
            return null;
        }

        Node root = null;

        // If current element of pre[] is in range, then
        // only it is part of current subtree
        if (key > min && key < max) {

            // Allocate memory for root of this subtree
            // and increment *preIndex
            root = new Node(key);
            preIndex.index = preIndex.index + 1;

            if (preIndex.index < size) {

                // Construct the subtree under root
                // All nodes which are in range
                // {min .. key} will go in left
                // subtree, and first such node will
                // be root of left subtree.
                root.left = constructTreeUtil(
                    pre, preIndex, pre[preIndex.index], min,
                    key, size);
            }
            if (preIndex.index < size) {
                // All nodes which are in range
                // {key..max} will go in right
                // subtree, and first such node
                // will be root of right subtree.
                root.right = constructTreeUtil(
                    pre, preIndex, pre[preIndex.index], key,
                    max, size);
            }
        }

        return root;
    }

    // The main function to construct BST from given
    // preorder traversal. This function mainly uses
    // constructTreeUtil()
    public virtual Node constructTree(int[] pre, int size)
    {

        return constructTreeUtil(pre, index, pre[0],
                                 int.MinValue, int.MaxValue,
                                 size);
    }

    // A utility function to print inorder traversal of a
    // Binary Tree
    public virtual void printInorder(Node node)
    {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        int[] pre = new int[] { 10, 5, 1, 7, 40, 50 };
        int size = pre.Length;

        // Function call
        Node root = tree.constructTree(pre, size);
        Console.WriteLine(
            "Inorder traversal of the constructed tree is ");
        tree.printInorder(root);
    }
}

// This code is contributed by Shrikant13
```

**Output**

```
Inorder traversal of the constructed tree: 
1 5 7 10 40 50 
```

**时间复杂度:** O(n)

我们将很快发布一个 O(n)迭代解作为单独的帖子。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。

**方法 3(O(n)<sup>2</sup>时间复杂度:**

只需使用递归概念并迭代给定元素的数组，如下所示。

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*Construct a BST from given pre-order traversal
for example if the given traversal is {10, 5, 1, 7, 40, 50},
then the output should be the root of the following tree.
     10
   /   \
  5     40
 /  \      \
1    7      50 */

class Node {
    int data;
    Node left, right;
    Node(int data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

class CreateBSTFromPreorder {
    private static Node node;

    // This will create the BST
    public static Node createNode(Node node, int data)
    {
        if (node == null)
            node = new Node(data);

        if (node.data > data)
            node.left = createNode(node.left, data);
        if (node.data < data)
            node.right = createNode(node.right, data);

        return node;
    }

    // A wrapper function of createNode
    public static void create(int data)
    {
        node = createNode(node, data);
    }
    // A function to print BST in inorder
    public static void inorderRec(Node root)
    {
        if (root != null) {
            inorderRec(root.left);
            System.out.println(root.data);
            inorderRec(root.right);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] nodeData = { 10, 5, 1, 7, 40, 50 };

        for (int i = 0; i < nodeData.length; i++) {
            create(nodeData[i]);
        }
        inorderRec(node);
    }
}
```

## C#

```
/*Construct a BST from given pre-order traversal
for example if the given traversal is {10, 5, 1, 7, 40, 50},
then the output should be the root of the following tree.
     10
   /   \
  5     40
 /  \      \
1    7      50 */
using System;
public class Node {
    public int data;
    public Node left, right;
    public Node(int data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

public class CreateBSTFromPreorder {
    private static Node node;

    // This will create the BST
    public static Node createNode(Node node, int data)
    {
        if (node == null)
            node = new Node(data);

        if (node.data > data)
            node.left = createNode(node.left, data);
        if (node.data < data)
            node.right = createNode(node.right, data);

        return node;
    }

    // A wrapper function of createNode
    public static void create(int data)
    {
        node = createNode(node, data);
    }

    // A function to print BST in inorder
    public static void inorderRec(Node root)
    {
        if (root != null) {
            inorderRec(root.left);
            Console.WriteLine(root.data);
            inorderRec(root.right);
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] nodeData = { 10, 5, 1, 7, 40, 50 };
        for (int i = 0; i < nodeData.Length; i++) {
            create(nodeData[i]);
        }
        inorderRec(node);
    }
}

// This code is contributed by Rajput-Ji
```

**Output**

```
1
5
7
10
40
50
```