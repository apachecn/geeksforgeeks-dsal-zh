# 从给定的父数组表示构建二叉树|迭代方法

> 原文:[https://www . geeksforgeeks . org/construct-二叉树-从给定-父-数组-表示-迭代-方法/](https://www.geeksforgeeks.org/construct-binary-tree-from-given-parent-array-representation-iterative-approach/)

给定一个表示树的数组，数组索引是树节点中的值，数组值给出该特定索引(或节点)的父节点。根节点索引的值总是-1，因为根没有父节点。从这个给定的表示构造给定二叉树的标准链接表示。
**例:**

```
Input: parent[] = {1, 5, 5, 2, 2, -1, 3}
Output:
Inorder Traversal of constructed tree
0 1 5 6 3 2 4
          5
        /  \
       1    2
      /    / \
     0    3   4
         /
        6 
Index of -1 is 5\. So 5 is root.  
5 is present at indexes 1 and 2\.  So 1 and 2 are
children of 5\.  
1 is present at index 0, so 0 is child of 1.
2 is present at indexes 3 and 4\.  So 3 and 4 are
children of 2\.  
3 is present at index 6, so 6 is child of 3.

Input: parent[] = {-1, 0, 0, 1, 1, 3, 5}
Output:
Inorder Traversal of constructed tree
6 5 3 1 4 0 2
         0
       /   \
      1     2
     / \
    3   4
   /
  5 
 /
6
```

**方法:**这个问题的递归方法在这里[讨论](https://www.geeksforgeeks.org/construct-a-binary-tree-from-parent-array-representation/)。
以下是迭代方法:

```
1. Create a map with key as the array index and its 
   value as the node for that index.
2. Start traversing the given parent array.
3. For all elements of the given array:
   (a) Search the map for the current index.
       (i) If the current index does not exist in the map:
           .. Create a node for the current index
           .. Map the newly created node with its key by m[i]=node
       (ii) If the key exists in the map:
            .. it means that the node is already created
            .. Do nothing
   (b) If the parent of the current index is -1, it implies it is
       the root of the tree
       .. Make root=m[i]
       Else search for the parent in the map
       (i) If the parent does not exist:
           .. Create the parent node.
           .. Assign the current node as its left child 
           .. Map the parent node(as in Step 3.(a).(i))
       (ii) If the parent exists:
           .. If the left child of the parent does not exist
              -> Assign the node as its left child
           .. Else (i.e. right child of the parent does not exist)
              -> Assign the node as its right child
```

即使节点没有按顺序排列，这种方法也是有效的。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A tree node
struct Node {
    int key;
    struct Node *left, *right;
};

// Utility function to create new Node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->left = temp->right = NULL;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
void inorder(Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// Function to construct a Binary Tree from parent array
Node* createTree(int parent[], int n)
{
    // A map to keep track of all the nodes created.
    // Key: node value; Value: Pointer to that Node
    map<int, Node*> m;
    Node *root, *temp;
    int i;

    // Iterate for all elements of the parent array.
    for (i = 0; i < n; i++) {

        // Node i does not exist in the map
        if (m.find(i) == m.end()) {

            // Create a new node for the current index
            temp = newNode(i);

            // Entry of the node in the map with
            // key as i and value as temp
            m[i] = temp;
        }

        // If parent is -1
        // Current node i is the root
        // So mark it as the root of the tree
        if (parent[i] == -1)
            root = m[i];

        // Current node is not root and parent
        // of that node is not created yet
        else if (m.find(parent[i]) == m.end()) {

            // Create the parent
            temp = newNode(parent[i]);

            // Assign the node as the
            // left child of the parent
            temp->left = m[i];

            // Entry of parent in map
            m[parent[i]] = temp;
        }

        // Current node is not root and parent
        // of that node is already created
        else {

            // Left child of the parent doesn't exist
            if (!m[parent[i]]->left)
                m[parent[i]]->left = m[i];

            // Right child of the parent doesn't exist
            else
                m[parent[i]]->right = m[i];
        }
    }
    return root;
}

// Driver code
int main()
{
    int parent[] = { -1, 0, 0, 1, 1, 3, 5 };
    int n = sizeof parent / sizeof parent[0];
    Node* root = createTree(parent, n);
    cout << "Inorder Traversal of constructed tree\n";
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// A tree node
static class Node
{
    int key;
    Node left, right;
};

// Utility function to create new Node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print( root.key + " ");
        inorder(root.right);
    }
}

// Function to construct a Binary Tree from parent array
static Node createTree(int parent[], int n)
{
    // A map to keep track of all the nodes created.
    // Key: node value; Value: Pointer to that Node
    HashMap<Integer, Node> m=new HashMap<>();
    Node root=new Node(), temp=new Node();
    int i;

    // Iterate for all elements of the parent array.
    for (i = 0; i < n; i++)
    {

        // Node i does not exist in the map
        if (m.get(i) == null)
        {

            // Create a new node for the current index
            temp = newNode(i);

            // Entry of the node in the map with
            // key as i and value as temp
            m.put(i, temp);
        }

        // If parent is -1
        // Current node i is the root
        // So mark it as the root of the tree
        if (parent[i] == -1)
            root = m.get(i);

        // Current node is not root and parent
        // of that node is not created yet
        else if (m.get(parent[i]) == null)
        {

            // Create the parent
            temp = newNode(parent[i]);

            // Assign the node as the
            // left child of the parent
            temp.left = m.get(i);

            // Entry of parent in map
            m.put(parent[i],temp);
        }

        // Current node is not root and parent
        // of that node is already created
        else
        {

            // Left child of the parent doesn't exist
            if (m.get(parent[i]).left == null)
                m.get(parent[i]).left = m.get(i);

            // Right child of the parent doesn't exist
            else
                m.get(parent[i]).right = m.get(i);
        }
    }
    return root;
}

// Driver code
public static void main(String args[])
{
    int parent[] = { -1, 0, 0, 1, 1, 3, 5 };
    int n = parent.length;
    Node root = createTree(parent, n);
    System.out.print( "Inorder Traversal of constructed tree\n");
    inorder(root);

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach

# A tree node
class Node:
    def __init__(self):
        self.key = 0
        self.left = None
        self.right = None

# Utility function to create new Node
def newNode(key: int) -> Node:
    temp = Node()
    temp.key = key
    temp.left = None
    temp.right = None
    return temp

# Utility function to perform
# inorder traversal of the tree
def inorder(root: Node):
    if root is not None:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

# Function to construct a Binary Tree from parent array
def createTree(parent: list, n: int) -> Node:

    # A map to keep track of all the nodes created.
    # Key: node value; Value: Pointer to that Node
    m = dict()
    root = Node()

    # Iterate for all elements of the parent array.
    for i in range(n):

        # Node i does not exist in the map
        if i not in m:

            # Create a new node for the current index
            temp = newNode(i)

            # Entry of the node in the map with
            # key as i and value as temp
            m[i] = temp

        # If parent is -1
        # Current node i is the root
        # So mark it as the root of the tree
        if parent[i] == -1:
            root = m[i]

        # Current node is not root and parent
        # of that node is not created yet
        elif parent[i] not in m:

            # Create the parent
            temp = newNode(parent[i])

            # Assign the node as the
            # left child of the parent
            temp.left = m[i]

            # Entry of parent in map
            m[parent[i]] = temp

        # Current node is not root and parent
        # of that node is already created
        else:

            # Left child of the parent doesn't exist
            if m[parent[i]].left is None:
                m[parent[i]].left = m[i]

            # Right child of the parent doesn't exist
            else:
                m[parent[i]].right = m[i]
    return root

# Driver Code
if __name__ == "__main__":
    parent = [-1, 0, 0, 1, 1, 3, 5]
    n = len(parent)
    root = createTree(parent, n)
    print("Inorder Traversal of constructed tree")
    inorder(root)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// A tree node
class Node
{
    public int key;
    public Node left, right;
};

// Utility function to create new Node
static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.left = temp.right = null;
    return (temp);
}

// Utility function to perform
// inorder traversal of the tree
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        Console.Write( root.key + " ");
        inorder(root.right);
    }
}

// Function to construct a Binary Tree from parent array
static Node createTree(int []parent, int n)
{
    // A map to keep track of all the nodes created.
    // Key: node value; Value: Pointer to that Node
    Dictionary<int, Node> m = new Dictionary<int, Node>();
    Node root = new Node(), temp = new Node();
    int i;

    // Iterate for all elements of the parent array.
    for (i = 0; i < n; i++)
    {

        // Node i does not exist in the map
        if (!m.ContainsKey(i))
        {

            // Create a new node for the current index
            temp = newNode(i);

            // Entry of the node in the map with
            // key as i and value as temp
            m.Add(i, temp);
        }

        // If parent is -1
        // Current node i is the root
        // So mark it as the root of the tree
        if (parent[i] == -1)
            root = m[i];

        // Current node is not root and parent
        // of that node is not created yet
        else if (!m.ContainsKey(parent[i]))
        {

            // Create the parent
            temp = newNode(parent[i]);

            // Assign the node as the
            // left child of the parent
            temp.left = m[i];

            // Entry of parent in map
            m.Add(parent[i], temp);
        }

        // Current node is not root and parent
        // of that node is already created
        else
        {

            // Left child of the parent doesn't exist
            if (m[parent[i]].left == null)
                m[parent[i]].left = m[i];

            // Right child of the parent doesn't exist
            else
                m[parent[i]].right = m[i];
        }
    }
    return root;
}

// Driver code
public static void Main(String []args)
{
    int []parent = { -1, 0, 0, 1, 1, 3, 5 };
    int n = parent.Length;
    Node root = createTree(parent, n);
    Console.Write("Inorder Traversal of constructed tree\n");
    inorder(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // A tree node
class Node {
    constructor(val) {
        this.key = val;
        this.left = null;
        this.right = null;
    }
}

    // Utility function to create new Node
    function newNode(key) {
var temp = new Node();
        temp.key = key;
        temp.left = temp.right = null;
        return (temp);
    }

    // Utility function to perform
    // inorder traversal of the tree
    function inorder(root) {
        if (root != null) {
            inorder(root.left);
            document.write(root.key + " ");
            inorder(root.right);
        }
    }

    // Function to construct a Binary Tree from parent array
    function createTree(parent , n) {
        // A map to keep track of all the nodes created.
        // Key: node value; Value: Pointer to that Node
        var m = new Map();
var root = new Node(), temp = new Node();
        var i;

        // Iterate for all elements of the parent array.
        for (i = 0; i < n; i++) {

            // Node i does not exist in the map
            if (m.get(i) == null) {

                // Create a new node for the current index
                temp = newNode(i);

                // Entry of the node in the map with
                // key as i and value as temp
                m.set(i, temp);
            }

            // If parent is -1
            // Current node i is the root
            // So mark it as the root of the tree
            if (parent[i] == -1)
                root = m.get(i);

            // Current node is not root and parent
            // of that node is not created yet
            else if (m.get(parent[i]) == null) {

                // Create the parent
                temp = newNode(parent[i]);

                // Assign the node as the
                // left child of the parent
                temp.left = m.get(i);

                // Entry of parent in map
                m.set(parent[i], temp);
            }

            // Current node is not root and parent
            // of that node is already created
            else {

                // Left child of the parent doesn't exist
                if (m.get(parent[i]).left == null)
                    m.get(parent[i]).left = m.get(i);

                // Right child of the parent doesn't exist
                else
                    m.get(parent[i]).right = m.get(i);
            }
        }
        return root;
    }

    // Driver code

        var parent = [ -1, 0, 0, 1, 1, 3, 5 ];
        var n = parent.length;
var root = createTree(parent, n);
        document.write("Inorder Traversal of constructed tree<br/>");
        inorder(root);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
Inorder Traversal of constructed tree
6 5 3 1 4 0 2
```