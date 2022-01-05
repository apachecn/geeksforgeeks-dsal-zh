# 检查二叉树的每个节点是自身还是其任何近邻都有值 K

> 原文:[https://www . geesforgeks . org/check-二叉树的每个节点是自身有值 k 还是其任意近邻/](https://www.geeksforgeeks.org/check-whether-every-node-of-binary-tree-has-a-value-k-on-itself-or-its-any-immediate-neighbours/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和值 **K** ，任务是检查二叉树的每个节点是将该节点的值作为 K，还是至少其一个相邻的连接节点具有值 K

**示例:**

```
Input:
                     1
                   /   \
                  0     0
                /   \     \
               1     0     1
              /     /  \    \
             2     1    0    5
                  /    /
                 3    0
                     /
                    0
K = 0
Output: False
Explanation: 
We can observe that some leaf nodes
are having value other than 0 and
are not connected with any
adjacent node whose value is 0\. 

Input:
                    0
                   / \
                  2   1
                       \
                        0
K = 0  
Output: True
Explanation: 
Since, all nodes of the tree
are either having value 0 or
connected with adjacent node
having value 0.
```

**进场:**

1.  其思想是简单执行[前序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，递归传递父节点的引用。
2.  t 为每个节点旅行时，检查以下条件:
    *   如果节点的值是 K 或，
    *   如果其父节点值为 K 或，
    *   如果其任何子节点值为 k
3.  如果树的任何节点不满足给定的三个条件中的任何一个，则返回假，否则返回真。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

// Defining tree node
struct node {
    int value;
    struct node *right, *left;
};

// Utility function to create
// a new node
struct node* newnode(int key)
{
    struct node* temp = new node;
    temp->value = key;
    temp->right = NULL;
    temp->left = NULL;

    return temp;
}

// Function to check binary
// tree whether its every node
// has value K or, it is
// connected with node having
// value K
bool connectedK(node* root,
                node* parent,
                int K,
                bool flag)
{
    // checking node value
    if (root->value != K) {

        // checking the left
        // child value
        if (root->left == NULL
            || root->left->value != K) {

            // checking the right
            // child value
            if (root->right == NULL
                || root->right->value != K) {

                // checking the parent value
                if (parent == NULL
                    || parent->value != K) {
                    flag = false;
                    return flag;
                }
            }
        }
    }

    // Traversing to the left subtree
    if (root->left != NULL) {
        if (flag == true) {
            flag
                = connectedK(root->left,
                            root, K, flag);
        }
    }

    // Traversing to the right subtree
    if (root->right != NULL) {
        if (flag == true) {
            flag
                = connectedK(root->right,
                            root, K, flag);
        }
    }
    return flag;
}

// Driver code
int main()
{

    // Input Binary tree
    struct node* root = newnode(0);
    root->right = newnode(1);
    root->right->right = newnode(0);
    root->left = newnode(0);

    int K = 0;

    // Function call to check
    // binary tree
    bool result
        = connectedK(root, NULL,
                    K, true);

    if (result == false)
        cout << "False\n";
    else
        cout << "True\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Defining tree node
static class node
{
    int value;
    node right, left;
};

// Utility function to create
// a new node
static node newnode(int key)
{
    node temp = new node();
    temp.value = key;
    temp.right = null;
    temp.left = null;

    return temp;
}

// Function to check binary
// tree whether its every node
// has value K or, it is
// connected with node having
// value K
static boolean connectedK(node root,
                          node parent,
                          int K,
                          boolean flag)
{
    // Checking node value
    if (root.value != K)
    {

        // Checking the left
        // child value
        if (root.left == null ||
            root.left.value != K)
        {

            // Checking the right
            // child value
            if (root.right == null ||
                root.right.value != K)
            {

                // Checking the parent value
                if (parent == null ||
                    parent.value != K)
                {
                    flag = false;
                    return flag;
                }
            }
        }
    }

    // Traversing to the left subtree
    if (root.left != null)
    {
        if (flag == true)
        {
            flag = connectedK(root.left,
                              root, K, flag);
        }
    }

    // Traversing to the right subtree
    if (root.right != null)
    {
        if (flag == true)
        {
            flag = connectedK(root.right,
                              root, K, flag);
        }
    }
    return flag;
}

// Driver code
public static void main(String[] args)
{

    // Input Binary tree
    node root = newnode(0);
    root.right = newnode(1);
    root.right.right = newnode(0);
    root.left = newnode(0);

    int K = 0;

    // Function call to check
    // binary tree
    boolean result = connectedK(root, null,
                                   K, true);

    if (result == false)
        System.out.print("False\n");
    else
        System.out.print("True\n");
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Defining tree node
class Node:
    def __init__(self,key):

        self.value = key
        self.left = None
        self.right = None

# Function to check binary
# tree whether its every node
# has value K or, it is
# connected with node having
# value K
def connectedK(root, parent, K, flag):

    # Checking node value
    if root.value != K:

        # Checking the left
        # child value
        if (root.left == None or
            root.left.value != K):

            # Checking the right
            # child value
            if (root.right == None or
                root.right.value != K):

                # Checking the parent value
                if (parent == None or
                    parent.value != K):
                    flag = False
                    return flag

    # Traversing to the left subtree
    if root.left != None:
        if flag == True:
            flag = connectedK(root.left,
                              root, K, flag)

    # Traversing to the right subtree
    if root.right != None:
        if flag == True:
            flag = connectedK(root.right,
                              root, K, flag)

    return flag

# Driver code
root = Node(0)
root.right = Node(1)
root.right.right = Node(0)
root.left = Node(0)

K = 0

# Function call to check
# binary tree
result = connectedK(root, None, K, True)

if result == False:
    print("False")
else:
    print("True")

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Defining tree node
class node
{
    public int value;
    public node right, left;
};

// Utility function to create
// a new node
static node newnode(int key)
{
    node temp = new node();
    temp.value = key;
    temp.right = null;
    temp.left = null;

    return temp;
}

// Function to check binary
// tree whether its every node
// has value K or, it is
// connected with node having
// value K
static bool connectedK(node root,
                       node parent,
                       int K,
                       bool flag)
{

    // Checking node value
    if (root.value != K)
    {

        // checking the left
        // child value
        if (root.left == null ||
            root.left.value != K)
        {

            // Checking the right
            // child value
            if (root.right == null ||
                root.right.value != K)
            {

                // Checking the parent value
                if (parent == null ||
                    parent.value != K)
                {
                    flag = false;
                    return flag;
                }
            }
        }
    }

    // Traversing to the left subtree
    if (root.left != null)
    {
        if (flag == true)
        {
            flag = connectedK(root.left,
                              root, K, flag);
        }
    }

    // Traversing to the right subtree
    if (root.right != null)
    {
        if (flag == true)
        {
            flag = connectedK(root.right,
                              root, K, flag);
        }
    }
    return flag;
}

// Driver code
public static void Main(String[] args)
{

    // Input Binary tree
    node root = newnode(0);
    root.right = newnode(1);
    root.right.right = newnode(0);
    root.left = newnode(0);

    int K = 0;

    // Function call to check
    // binary tree
    bool result = connectedK(root, null,
                                K, true);

    if (result == false)
        Console.Write("False\n");
    else
        Console.Write("True\n");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Defining tree node
    class node
    {
        constructor(key) {
           this.value = key;
           this.left = this.right = null;
        }
    }

    // Utility function to create
    // a new node
    function newnode(key)
    {
        let temp = new node(key);
        return temp;
    }

    // Function to check binary
    // tree whether its every node
    // has value K or, it is
    // connected with node having
    // value K
    function connectedK(root, parent, K, flag)
    {
        // Checking node value
        if (root.value != K)
        {

            // Checking the left
            // child value
            if (root.left == null ||
                root.left.value != K)
            {

                // Checking the right
                // child value
                if (root.right == null ||
                    root.right.value != K)
                {

                    // Checking the parent value
                    if (parent == null ||
                        parent.value != K)
                    {
                        flag = false;
                        return flag;
                    }
                }
            }
        }

        // Traversing to the left subtree
        if (root.left != null)
        {
            if (flag == true)
            {
                flag = connectedK(root.left, root, K, flag);
            }
        }

        // Traversing to the right subtree
        if (root.right != null)
        {
            if (flag == true)
            {
                flag = connectedK(root.right, root, K, flag);
            }
        }
        return flag;
    }

    // Input Binary tree
    let root = newnode(0);
    root.right = newnode(1);
    root.right.right = newnode(0);
    root.left = newnode(0);

    let K = 0;

    // Function call to check
    // binary tree
    let result = connectedK(root, null, K, true);

    if (result == false)
        document.write("False");
    else
        document.write("True");

</script>
```

**输出:**

```
True
```

**时间复杂度:** O(N)，N 为树的节点数。
**辅助空间:** O(1)