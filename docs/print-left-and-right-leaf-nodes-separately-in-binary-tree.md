# 在二叉树中分别打印左右叶节点

> 原文:[https://www . geeksforgeeks . org/print-左右叶节点-二叉树中单独/](https://www.geeksforgeeks.org/print-left-and-right-leaf-nodes-separately-in-binary-tree/)

给定一棵二叉树，任务是分别打印左右叶节点。

**示例:**

```
Input:
       0
     /   \
   1      2
 /  \
3    4 
Output:
Left Leaf Nodes: 3
Right Leaf Nodes: 4 2

Input:
   0
     \
      1
       \
        2
         \
          3
Output:
Left Leaf Nodes: None
Right Leaf Nodes: 3
```

**进场:**

*   检查给定节点是否为空。如果为空，则从函数返回。
*   对于在右侧和左侧的每个遍历，使用参数**类型**发送关于子对象(左侧或右侧子对象)的信息。下降到左分支时设置 type = 0，右分支时设置 type = 1。
*   检查它是否是叶节点。如果该节点是叶节点，则将该叶节点存储在左右子节点的两个向量之一中。
*   如果节点不是叶节点，继续遍历。
*   在单节点树的情况下，它既是根节点又是叶节点。这个案子必须分开处理。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Structure for
// Binary Tree Node
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int x): data(x), left(NULL), right(NULL) {}
};

// Function for
// dfs traversal
void dfs(Node* root, int type, vector<int>& left_leaf,
         vector<int>& right_leaf)
{
    // If node is
    // null, return
    if (!root) {
        return;
    }

    // If tree consists
    // of a single node
    if (!root->left && !root->right) {
        if (type == -1) {
            cout << "Tree consists of a single node\n";
        }
        else if (type == 0) {
            left_leaf.push_back(root->data);
        }
        else {
            right_leaf.push_back(root->data);
        }

        return;
    }

    // If left child exists,
    // traverse and set type to 0
    if (root->left) {
        dfs(root->left, 0, left_leaf, right_leaf);
    }
    // If right child exists,
    // traverse and set type to 1
    if (root->right) {
        dfs(root->right, 1, left_leaf, right_leaf);
    }
}

// Function to print
// the solution
void print(vector<int>& left_leaf, vector<int>& right_leaf)
{

    if (left_leaf.size() == 0 && right_leaf.size() == 0)
        return;

    // Printing left leaf nodes
    cout << "Left leaf nodes\n";
    for (int x : left_leaf) {
        cout << x << " ";
    }
    cout << '\n';

    // Printing right leaf nodes
    cout << "Right leaf nodes\n";
    for (int x : right_leaf) {
        cout << x << " ";
    }
    cout << '\n';
}

// Driver code
int main()
{

    Node* root = new Node(0);
    root->left = new Node(1);
    root->right = new Node(2);
    root->left->left = new Node(3);
    root->left->right = new Node(4);

    vector<int> left_leaf, right_leaf;
    dfs(root, -1, left_leaf, right_leaf);

    print(left_leaf, right_leaf);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG
{

    // Structure for
    // Binary Tree Node
    static class Node
    {
        int data;
        Node left;
        Node right;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }

    };

    // Function for
    // dfs traversal
    static void dfs(Node root, int type, Vector<Integer> left_leaf,
            Vector<Integer> right_leaf)
    {
        // If node is
        // null, return
        if (root == null)
        {
            return;
        }

        // If tree consists
        // of a single node
        if (root.left == null && root.right == null)
        {
            if (type == -1)
            {
                System.out.print("Tree consists of a single node\n");
            }
            else if (type == 0)
            {
                left_leaf.add(root.data);
            }
            else
            {
                right_leaf.add(root.data);
            }

            return;
        }

        // If left child exists,
        // traverse and set type to 0
        if (root.left != null)
        {
            dfs(root.left, 0, left_leaf, right_leaf);
        }

        // If right child exists,
        // traverse and set type to 1
        if (root.right != null)
        {
            dfs(root.right, 1, left_leaf, right_leaf);
        }
    }

    // Function to print
    // the solution
    static void print(Vector<Integer> left_leaf,
                    Vector<Integer> right_leaf)
    {

        if (left_leaf.size() == 0 && right_leaf.size() == 0)
            return;

        // Printing left leaf nodes
        System.out.print("Left leaf nodes\n");
        for (int x : left_leaf)
        {
            System.out.print(x + " ");
        }
        System.out.println();

        // Printing right leaf nodes
        System.out.print("Right leaf nodes\n");
        for (int x : right_leaf)
        {
            System.out.print(x + " ");
        }
        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {

        Node root = new Node(0);
        root.left = new Node(1);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.left.right = new Node(4);

        Vector<Integer> left_leaf = new Vector<Integer>(),
                right_leaf = new Vector<Integer>();
        dfs(root, -1, left_leaf, right_leaf);

        print(left_leaf, right_leaf);

    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Structure for
# Binary Tree Node
class Node:

    def __init__(self, data):

        self.data = data
        self.left = None
        self.right = None

# Function for
# dfs traversal
def dfs(root, type_t, left_leaf,
        right_leaf):

    # If node is
    # null, return
    if (not root):
        return

    # If tree consists
    # of a single node
    if (not root.left and not root.right):
        if (type_t == -1):
            print("Tree consists of a single node")

        elif (type_t == 0):
            left_leaf.append(root.data)

        else:
            right_leaf.append(root.data)

        return

    # If left child exists,
    # traverse and set type_t to 0
    if (root.left):
        dfs(root.left, 0, left_leaf,
            right_leaf)

    # If right child exists,
    # traverse and set type_t to 1
    if (root.right):
        dfs(root.right, 1, left_leaf,
            right_leaf)

# Function to print
# the solution
def prints(left_leaf, right_leaf):

    if (len(left_leaf) == 0 and
        len(right_leaf) == 0):
        return

    # Printing left leaf nodes
    print("Left leaf nodes")

    for x in left_leaf:
        print(x, end = ' ')

    print()

    # Printing right leaf nodes
    print("Right leaf nodes")

    for x in right_leaf:
        print(x, end = ' ')

    print()

# Driver code
if __name__=='__main__':

    root = Node(0)
    root.left = Node(1)
    root.right = Node(2)
    root.left.left = Node(3)
    root.left.right = Node(4)

    left_leaf = []
    right_leaf = []
    dfs(root, -1, left_leaf, right_leaf)

    prints(left_leaf, right_leaf)

# This code is contributed by pratham76
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Structure for
    // Binary Tree Node
    public class Node
    {
        public int data;
        public Node left;
        public Node right;

        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }

    };

    // Function for
    // dfs traversal
    static void dfs(Node root, int type, List<int> left_leaf,
            List<int> right_leaf)
    {
        // If node is
        // null, return
        if (root == null)
        {
            return;
        }

        // If tree consists
        // of a single node
        if (root.left == null && root.right == null)
        {
            if (type == -1)
            {
                Console.Write("Tree consists of a single node\n");
            }
            else if (type == 0)
            {
                left_leaf.Add(root.data);
            }
            else
            {
                right_leaf.Add(root.data);
            }

            return;
        }

        // If left child exists,
        // traverse and set type to 0
        if (root.left != null)
        {
            dfs(root.left, 0, left_leaf, right_leaf);
        }

        // If right child exists,
        // traverse and set type to 1
        if (root.right != null)
        {
            dfs(root.right, 1, left_leaf, right_leaf);
        }
    }

    // Function to print
    // the solution
    static void print(List<int> left_leaf,
                    List<int> right_leaf)
    {

        if (left_leaf.Count == 0 && right_leaf.Count == 0)
            return;

        // Printing left leaf nodes
        Console.Write("Left leaf nodes\n");
        foreach (int x in left_leaf)
        {
            Console.Write(x + " ");
        }
        Console.WriteLine();

        // Printing right leaf nodes
        Console.Write("Right leaf nodes\n");
        foreach (int x in right_leaf)
        {
            Console.Write(x + " ");
        }
        Console.WriteLine();
    }

    // Driver code
    public static void Main(String[] args)
    {

        Node root = new Node(0);
        root.left = new Node(1);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.left.right = new Node(4);

        List<int> left_leaf = new List<int>(),
                right_leaf = new List<int>();
        dfs(root, -1, left_leaf, right_leaf);

        print(left_leaf, right_leaf);

    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program for the
// above approach
// Structure for
// Binary Tree Node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};
// Function for
// dfs traversal
function dfs(root, type, left_leaf, right_leaf)
{
    // If node is
    // null, return
    if (root == null)
    {
        return;
    }
    // If tree consists
    // of a single node
    if (root.left == null && root.right == null)
    {
        if (type == -1)
        {
            document.write("Tree consists of a single node<br>");
        }
        else if (type == 0)
        {
            left_leaf.push(root.data);
        }
        else
        {
            right_leaf.push(root.data);
        }
        return;
    }
    // If left child exists,
    // traverse and set type to 0
    if (root.left != null)
    {
        dfs(root.left, 0, left_leaf, right_leaf);
    }

    // If right child exists,
    // traverse and set type to 1
    if (root.right != null)
    {
        dfs(root.right, 1, left_leaf, right_leaf);
    }
}
// Function to print
// the solution
function print(left_leaf, right_leaf)
{
    if (left_leaf.Count == 0 && right_leaf.Count == 0)
        return;
    // Printing left leaf nodes
    document.write("Left leaf nodes<br>");

    for(var x of left_leaf)
    {
        document.write(x + " ");
    }
    document.write("<br>");

    // Printing right leaf nodes
    document.write("Right leaf nodes<br>");
    for(var x of right_leaf)
    {
        document.write(x + " ");
    }
    document.write("<br>");
}

// Driver code
var root = new Node(0);
root.left = new Node(1);
root.right = new Node(2);
root.left.left = new Node(3);
root.left.right = new Node(4);
var left_leaf = [];
var right_leaf = [];
dfs(root, -1, left_leaf, right_leaf);
print(left_leaf, right_leaf);

</script>
```

**Output:** 

```
Left leaf nodes
3 
Right leaf nodes
4 2
```