# 检查移除边是否可以将二叉树分成两半

> 原文:[https://www . geesforgeks . org/check-if-remove-an-edge-can-divide-a-二叉树两半/](https://www.geeksforgeeks.org/check-if-removing-an-edge-can-divide-a-binary-tree-in-two-halves/)

给定一棵二叉树，找出是否存在一条边，它的移除会创建两个大小相等的树。

**示例:**

```
Input : root of following tree
           5
         /   \
       1      6    
      /      /  \
     3      7    4
Output : true
Removing edge 5-6 creates two trees of equal size

Input : root of following tree
           5
         /   \
       1      6    
            /  \
           7    4
         /  \    \
        3    2    8
Output : false
There is no edge whose removal creates two trees
of equal size.
```

来源- Kshitij IIT KGP

**方法 1(简单)**
首先统计整棵树的节点数。让所有节点的计数为 n。现在遍历树，对于每个节点，找到以该节点为根的子树的大小。如果 n-s 等于 s，则返回 true，否则返回 false。

## C++

```
// C++ program to check if there exist an edge whose
// removal creates two trees of same size
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node* left, *right;
};

// utility function to create a new node
struct Node* newNode(int x)
{
    struct Node* temp = new Node;
    temp->data = x;
    temp->left = temp->right = NULL;
    return temp;
};

// To calculate size of tree with given root
int count(Node* root)
{
    if (root==NULL)
        return 0;
    return count(root->left) + count(root->right) + 1;
}

// This function returns true if there is an edge
// whose removal can divide the tree in two halves
// n is size of tree
bool checkRec(Node* root, int n)
{
    // Base cases
    if (root ==NULL)
       return false;

    // Check for root
    if (count(root) == n-count(root))
        return true;

    // Check for rest of the nodes
    return checkRec(root->left, n) ||
           checkRec(root->right, n);
}

// This function mainly uses checkRec()
bool check(Node *root)
{
    // Count total nodes in given tree
    int n = count(root);

    // Now recursively check all nodes
    return checkRec(root, n);
}

// Driver code
int main()
{
    struct Node* root = newNode(5);
    root->left = newNode(1);
    root->right = newNode(6);
    root->left->left = newNode(3);
    root->right->left = newNode(7);
    root->right->right = newNode(4);

    check(root)?  printf("YES") : printf("NO");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there exist an edge whose
// removal creates two trees of same size

class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // To calculate size of tree with given root
    int count(Node node)
    {
        if (node == null)
            return 0;

        return count(node.left) + count(node.right) + 1;
    }

    // This function returns true if there is an edge
    // whose removal can divide the tree in two halves
    // n is size of tree
    boolean checkRec(Node node, int n)
    {
        // Base cases
        if (node == null)
            return false;

        // Check for root
        if (count(node) == n - count(node))
            return true;

        // Check for rest of the nodes
        return checkRec(node.left, n)
                || checkRec(node.right, n);
    }

    // This function mainly uses checkRec()
    boolean check(Node node)
    {
        // Count total nodes in given tree
        int n = count(node);

        // Now recursively check all nodes
        return checkRec(node, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(1);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(3);
        tree.root.right.left = new Node(7);
        tree.root.right.right = new Node(4);
        if(tree.check(tree.root)==true)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to check if there
# exist an edge whose removal creates
# two trees of same size

# utility function to create a new node
class newNode:
    def __init__(self, x):
        self.data = x
        self.left = self.right = None

# To calculate size of tree
# with given root
def count(root):
    if (root == None):
        return 0
    return (count(root.left) +
            count(root.right) + 1)

# This function returns true if there
# is an edge whose removal can divide
# the tree in two halves n is size of tree
def checkRec(root, n):

    # Base cases
    if (root == None):
        return False

    # Check for root
    if (count(root) == n - count(root)):
        return True

    # Check for rest of the nodes
    return (checkRec(root.left, n) or
            checkRec(root.right, n))

# This function mainly uses checkRec()
def check(root):

    # Count total nodes in given tree
    n = count(root)

    # Now recursively check all nodes
    return checkRec(root, n)

# Driver code
if __name__ == '__main__':
    root = newNode(5)
    root.left = newNode(1)
    root.right = newNode(6)
    root.left.left = newNode(3)
    root.right.left = newNode(7)
    root.right.right = newNode(4)

    if check(root):
        print("YES")
    else:
        print("NO")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check if there exist
// an edge whose removal creates two
// trees of same size
using System;

public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class GFG
{
public Node root;

// To calculate size of tree with given root
public virtual int count(Node node)
{
    if (node == null)
    {
        return 0;
    }

    return count(node.left) +
           count(node.right) + 1;
}

// This function returns true if there
// is an edge whose removal can divide
// the tree in two halves n is size of tree
public virtual bool checkRec(Node node, int n)
{
    // Base cases
    if (node == null)
    {
        return false;
    }

    // Check for root
    if (count(node) == n - count(node))
    {
        return true;
    }

    // Check for rest of the nodes
    return checkRec(node.left, n) ||
           checkRec(node.right, n);
}

// This function mainly uses checkRec()
public virtual bool check(Node node)
{
    // Count total nodes in given tree
    int n = count(node);

    // Now recursively check all nodes
    return checkRec(node, n);
}

// Driver code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(5);
    tree.root.left = new Node(1);
    tree.root.right = new Node(6);
    tree.root.left.left = new Node(3);
    tree.root.right.left = new Node(7);
    tree.root.right.right = new Node(4);
    if (tree.check(tree.root) == true)
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to check if
// there exist an edge whose
// removal creates two trees of same size

    class Node
    {
        constructor(key)
        {
            this.key=key;
            this.left=this.right=null;
        }
    }

    // To calculate size of tree
    // with given root
    function count(node)
    {
        if (node == null)
            return 0;

        return count(node.left) +
        count(node.right) + 1;
    }

    // This function returns true
    // if there is an edge
    // whose removal can divide the
    // tree in two halves
    // n is size of tree
    function checkRec(node,n)
    {
        // Base cases
        if (node == null)
            return false;

        // Check for root
        if (count(node) == n - count(node))
            return true;

        // Check for rest of the nodes
        return checkRec(node.left, n)
                || checkRec(node.right, n);
    }

    // This function mainly uses checkRec()
    function check(node)
    {
        // Count total nodes in given tree
        let n = count(node);

        // Now recursively check all nodes
        return checkRec(node, n);
    }

    // Driver code
    let root = new Node(5);
    root.left = new Node(1);
    root.right = new Node(6);
    root.left.left = new Node(3);
    root.right.left = new Node(7);
    root.right.right = new Node(4);
    if(check(root)==true)
        document.write("YES");
    else
        document.write("NO");

    // This code is contributed by unknown2108

</script>
```

**输出:**

```
YES
```

上述解的时间复杂度为 O(n <sup>2</sup> )，其中 n 是给定二叉树中的节点数。

**方法 2(高效)**
我们可以在 O(n)时间内找到解。其思想是以自下而上的方式遍历树，并在遍历时不断更新大小，并不断检查是否有符合所需属性的节点。

以下是上述想法的实现。

## C++

```
// C++ program to check if there exist an edge whose
// removal creates two trees of same size
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node* left, *right;
};

// utility function to create a new node
struct Node* newNode(int x)
{
    struct Node* temp = new Node;
    temp->data = x;
    temp->left = temp->right = NULL;
    return temp;
};

// To calculate size of tree with given root
int count(Node* root)
{
    if (root==NULL)
        return 0;
    return count(root->left) + count(root->right) + 1;
}

// This function returns size of tree rooted with given
// root. It also set "res" as true if there is an edge
// whose removal divides tree in two halves.
// n is size of tree
int checkRec(Node* root, int n, bool &res)
{
    // Base case
    if (root == NULL)
       return 0;

    // Compute sizes of left and right children
    int c = checkRec(root->left, n, res) + 1 +
            checkRec(root->right, n, res);

    // If required property is true for current node
    // set "res" as true
    if (c == n-c)
        res = true;

    // Return size
    return c;
}

// This function mainly uses checkRec()
bool check(Node *root)
{
    // Count total nodes in given tree
    int n = count(root);

    // Initialize result and recursively check all nodes
    bool res = false;
    checkRec(root, n,  res);

    return res;
}

// Driver code
int main()
{
    struct Node* root = newNode(5);
    root->left = newNode(1);
    root->right = newNode(6);
    root->left->left = newNode(3);
    root->right->left = newNode(7);
    root->right->right = newNode(4);

    check(root)?  printf("YES") : printf("NO");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if there exist an edge whose
// removal creates two trees of same size

class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class Res
{
    boolean res = false;
}

class BinaryTree
{
    Node root;

    // To calculate size of tree with given root
    int count(Node node)
    {
        if (node == null)
            return 0;

        return count(node.left) + count(node.right) + 1;
    }

    // This function returns size of tree rooted with given
    // root. It also set "res" as true if there is an edge
    // whose removal divides tree in two halves.
    // n is size of tree
    int checkRec(Node root, int n, Res res)
    {
        // Base case
        if (root == null)
            return 0;

        // Compute sizes of left and right children
        int c = checkRec(root.left, n, res) + 1
                + checkRec(root.right, n, res);

        // If required property is true for current node
        // set "res" as true
        if (c == n - c)
            res.res = true;

        // Return size
        return c;
    }

    // This function mainly uses checkRec()
    boolean check(Node root)
    {
        // Count total nodes in given tree
        int n = count(root);

        // Initialize result and recursively check all nodes
        Res res = new Res();
        checkRec(root, n, res);

        return res.res;
    }

    // Driver code
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(1);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(3);
        tree.root.right.left = new Node(7);
        tree.root.right.right = new Node(4);
        if (tree.check(tree.root) == true)
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to check if there exist
# an edge whose removal creates two trees
# of same size
class Node:

    def __init__(self, x):

        self.key = x
        self.left = None
        self.right = None

# To calculate size of tree with
# given root
def count(node):

    if (node == None):
        return 0

    return (count(node.left) +
            count(node.right) + 1)

# This function returns size of tree rooted
# with given root. It also set "res" as true
# if there is an edge whose removal divides
# tree in two halves.n is size of tree
def checkRec(root, n):

    global res

    # Base case
    if (root == None):
       return 0

    # Compute sizes of left and right children
    c = (checkRec(root.left, n) + 1 +
         checkRec(root.right, n))

    # If required property is true for
    # current node set "res" as true
    if (c == n - c):
        res = True

    # Return size
    return c

# This function mainly uses checkRec()
def check(root):

    # Count total nodes in given tree
    n = count(root)

    # Initialize result and recursively
    # check all nodes
    # bool res = false;
    checkRec(root, n)

# Driver code
if __name__ == '__main__':

    res = False
    root = Node(5)
    root.left = Node(1)
    root.right = Node(6)
    root.left.left = Node(3)
    root.right.left = Node(7)
    root.right.right = Node(4)

    check(root)

    if res:
        print("YES")
    else:
        print("NO")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if there exist an edge whose
// removal creates two trees of same size
using System;

public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

public class Res
{
    public bool res = false;
}

public class BinaryTree
{
    public Node root;

    // To calculate size of tree with given root
    public virtual int count(Node node)
    {
        if (node == null)
        {
            return 0;
        }

        return count(node.left) + count(node.right) + 1;
    }

    // This function returns size of tree rooted with given
    // root. It also set "res" as true if there is an edge
    // whose removal divides tree in two halves.
    // n is size of tree
    public virtual int checkRec(Node root, int n, Res res)
    {
        // Base case
        if (root == null)
        {
            return 0;
        }

        // Compute sizes of left and right children
        int c = checkRec(root.left, n, res) + 1 + checkRec(root.right, n, res);

        // If required property is true for current node
        // set "res" as true
        if (c == n - c)
        {
            res.res = true;
        }

        // Return size
        return c;
    }

    // This function mainly uses checkRec()
    public virtual bool check(Node root)
    {
        // Count total nodes in given tree
        int n = count(root);

        // Initialize result and recursively check all nodes
        Res res = new Res();
        checkRec(root, n, res);

        return res.res;
    }

    // Driver code
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(1);
        tree.root.right = new Node(6);
        tree.root.left.left = new Node(3);
        tree.root.right.left = new Node(7);
        tree.root.right.right = new Node(4);
        if (tree.check(tree.root) == true)
        {
            Console.WriteLine("YES");
        }
        else
        {
            Console.WriteLine("NO");
        }
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// javascript program to check if there exist an edge whose
// removal creates two trees of same size

class Node {

    constructor(key) {
        this.key = key;
        this.left = this.right = null;
    }
}

class Res {
constructor(){
     this.res = false;
    }
}

    var root;

    // To calculate size of tree with given root
    function count( node) {
        if (node == null)
            return 0;

        return count(node.left) + count(node.right) + 1;
    }

    // This function returns size of tree rooted with given
    // root. It also set "res" as true if there is an edge
    // whose removal divides tree in two halves.
    // n is size of tree
    function checkRec( root , n,  res) {
        // Base case
        if (root == null)
            return 0;

        // Compute sizes of left and right children
        var c = checkRec(root.left, n, res) + 1 + checkRec(root.right, n, res);

        // If required property is true for current node
        // set "res" as true
        if (c == n - c)
            res.res = true;

        // Return size
        return c;
    }

    // This function mainly uses checkRec()
    function check( root) {
        // Count total nodes in given tree
        var n = count(root);

        // Initialize result and recursively check all nodes
         res = new Res();
        checkRec(root, n, res);

        return res.res;
    }

    // Driver code

        root = new Node(5);
        root.left = new Node(1);
        root.right = new Node(6);
        root.left.left = new Node(3);
        root.right.left = new Node(7);
        root.right.right = new Node(4);
        if (check(root) == true)
            document.write("YES");
        else
            document.write("NO");

// This code contributed by umadevi9616
</script>
```

**输出:**

```
YES
```

本文由**阿萨德·阿克兰**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息