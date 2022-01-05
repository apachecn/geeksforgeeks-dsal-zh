# 检查两个 BST 是否包含相同的元素组

> 原文:[https://www . geesforgeks . org/check-two-bsts-contain-set-elements/](https://www.geeksforgeeks.org/check-two-bsts-contain-set-elements/)

给定两个由唯一正元素组成的二分搜索法树，我们必须检查这两个 BST 是否包含相同的集合或元素。
**注**:给定的两个 BST 结构可以不同。
例如

![9 (5)](img/c01ba3ee5ab227dbbcc3d31578851364.png)

以上两个 BST 包含相同的元素集{5，10，12，15，20，25}

**方法 1** :最简单的方法是遍历第一棵树，并将其元素存储在列表或数组中。现在，遍历第二棵树，同时检查当前元素是否在列表中。如果是，则将列表中的元素标记为负，并检查其他元素；否则，如果不是，则立即终止遍历并打印“否”。如果列表中存在第二棵树的所有元素并标记为负，则最后遍历列表以检查是否还有任何非负元素。如果是，那么这意味着第一个树有一些额外的元素，否则这两个树包含相同的元素集。
时间复杂度:O( n * n)，其中 n 为 BST 中的节点数。
辅助空间:O( n)。
**方法二**:该方法是上述方法的优化。如果我们仔细观察，我们会发现在上面的方法中，在列表中搜索元素需要线性时间。我们可以使用 hashmap 而不是 list 来优化这个在恒定时间内完成的操作。我们在不同的散列集中插入两棵树的元素。最后，我们比较两个哈希集是否包含相同的元素。
以下是上述方法的完整实现:

## C++

```
// CPP program to check if two BSTs contains
// same set of elements
#include<bits/stdc++.h>
using namespace std;

// BST Node
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create new Node
Node* newNode(int val)
{
    Node* temp = new Node;
    temp->data = val;
    temp->left = temp->right = NULL;
    return temp;
}

// function to insert elements of the
// tree to map m
void insertToHash(Node* root, unordered_set<int> &s)
{
    if (!root)
        return;
    insertToHash(root->left, s);
    s.insert(root->data);
    insertToHash(root->right, s);
}

// function to check if the two BSTs contain
// same set  of elements
bool checkBSTs(Node* root1, Node* root2)
{
    // Base cases
    if (!root1 && !root2)
        return true;
    if ((root1 && !root2) || (!root1 && root2))
        return false;

    // Create two hash sets and store
    // elements both BSTs in them.
    unordered_set<int> s1, s2;
    insertToHash(root1, s1);
    insertToHash(root2, s2);

    // Return true if both hash sets
    // contain same elements.
    return (s1 == s2);
}

// Driver program to check above functions
int main()
{
    // First BST
    Node* root1 = newNode(15);
    root1->left = newNode(10);
    root1->right = newNode(20);
    root1->left->left = newNode(5);
    root1->left->right = newNode(12);
    root1->right->right = newNode(25);

    // Second BST
    Node* root2 = newNode(15);
    root2->left = newNode(12);
    root2->right = newNode(20);
    root2->left->left = newNode(5);
    root2->left->left->right = newNode(10);
    root2->right->right = newNode(25);

    // check if two BSTs have same set of elements
    if (checkBSTs(root1, root2))
        cout << "YES";
    else
        cout << "NO";
    return 0;       
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if two BSTs contains
// same set of elements
import java.util.*;

class GFG
{

// BST Node
static class Node
{
    int data;
    Node left;
    Node right;
};

// Utility function to create new Node
static Node newNode(int val)
{
    Node temp = new Node();
    temp.data = val;
    temp.left = temp.right = null;
    return temp;
}

// function to insert elements of the
// tree to map m
static void insertToHash(Node root, HashSet<Integer> s)
{
    if (root == null)
        return;
    insertToHash(root.left, s);
    s.add(root.data);
    insertToHash(root.right, s);
}

// function to check if the two BSTs contain
// same set of elements
static boolean checkBSTs(Node root1, Node root2)
{
    // Base cases
    if (root1 != null && root2 != null)
        return true;
    if ((root1 == null && root2 != null) || (root1 != null && root2 == null))
        return false;

    // Create two hash sets and store
    // elements both BSTs in them.
    HashSet<Integer> s1 = new HashSet<Integer>();
    HashSet<Integer> s2 = new HashSet<Integer>();
    insertToHash(root1, s1);
    insertToHash(root2, s2);

    // Return true if both hash sets
    // contain same elements.
    return (s1.equals(s2));
}

// Driver program to check above functions
public static void main(String[] args)
{
    // First BST
    Node root1 = newNode(15);
    root1.left = newNode(10);
    root1.right = newNode(20);
    root1.left.left = newNode(5);
    root1.left.right = newNode(12);
    root1.right.right = newNode(25);

    // Second BST
    Node root2 = newNode(15);
    root2.left = newNode(12);
    root2.right = newNode(20);
    root2.left.left = newNode(5);
    root2.left.left.right = newNode(10);
    root2.right.right = newNode(25);

    // check if two BSTs have same set of elements
    if (checkBSTs(root1, root2))
        System.out.print("YES");
    else
        System.out.print("NO");
}    
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if two BSTs contains
# same set of elements

# BST Node
class Node:
    def __init__(self):
        self.val = 0
        self.left = None
        self.right = None

# Utility function to create Node
def Node_(val1):

    temp = Node()
    temp.val = val1
    temp.left = temp.right = None
    return temp

s = {}

# function to insert elements of the
# tree to map m
def insertToHash(root):

    if (root == None):
        return
    insertToHash(root.left)
    s.add(root.data)
    insertToHash(root.right)

# function to check if the two BSTs contain
# same set of elements
def checkBSTs(root1, root2):

    # Base cases
    if (root1 != None and root2 != None) :
        return True
    if ((root1 == None and root2 != None) or
        (root1 != None and root2 == None)):
        return False

    # Create two hash sets and store
    # elements both BSTs in them.
    s1 = {}
    s2 = {}
    s = s1
    insertToHash(root1)
    s1 = s
    s = s2
    insertToHash(root2)
    s2 = s

    # Return True if both hash sets
    # contain same elements.
    return (s1 == (s2))

# Driver code

# First BST
root1 = Node_(15)
root1.left = Node_(10)
root1.right = Node_(20)
root1.left.left = Node_(5)
root1.left.right = Node_(12)
root1.right.right = Node_(25)

# Second BST
root2 = Node_(15)
root2.left = Node_(12)
root2.right = Node_(20)
root2.left.left = Node_(5)
root2.left.left.right = Node_(10)
root2.right.right = Node_(25)

# check if two BSTs have same set of elements
if (checkBSTs(root1, root2)):
    print("YES")
else:
    print("NO")

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to check if two BSTs contains
// same set of elements
using System;
using System.Collections.Generic;

class GFG
{

// BST Node
class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Utility function to create new Node
static Node newNode(int val)
{
    Node temp = new Node();
    temp.data = val;
    temp.left = temp.right = null;
    return temp;
}

// function to insert elements of the
// tree to map m
static void insertToHash(Node root,
                         HashSet<int> s)
{
    if (root == null)
        return;
    insertToHash(root.left, s);
    s.Add(root.data);
    insertToHash(root.right, s);
}

// function to check if the two BSTs contain
// same set of elements
static bool checkBSTs(Node root1, Node root2)
{
    // Base cases
    if (root1 != null && root2 != null)
        return true;
    if ((root1 == null && root2 != null) ||
        (root1 != null && root2 == null))
        return false;

    // Create two hash sets and store
    // elements both BSTs in them.
    HashSet<int> s1 = new HashSet<int>();
    HashSet<int> s2 = new HashSet<int>();
    insertToHash(root1, s1);
    insertToHash(root2, s2);

    // Return true if both hash sets
    // contain same elements.
    return (s1.Equals(s2));
}

// Driver Code
public static void Main(String[] args)
{
    // First BST
    Node root1 = newNode(15);
    root1.left = newNode(10);
    root1.right = newNode(20);
    root1.left.left = newNode(5);
    root1.left.right = newNode(12);
    root1.right.right = newNode(25);

    // Second BST
    Node root2 = newNode(15);
    root2.left = newNode(12);
    root2.right = newNode(20);
    root2.left.left = newNode(5);
    root2.left.left.right = newNode(10);
    root2.right.right = newNode(25);

    // check if two BSTs have same set of elements
    if (checkBSTs(root1, root2))
        Console.Write("YES");
    else
        Console.Write("NO");
}    
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to check if two BSTs contains
// same set of elements

// BST Node
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function to create new Node
function newNode(val)
{
    var temp = new Node();
    temp.data = val;
    temp.left = temp.right = null;
    return temp;
}

// function to insert elements of the
// tree to map m
function insertToHash(root, s)
{
    if (root == null)
        return;
    insertToHash(root.left, s);
    s.add(root.data);
    insertToHash(root.right, s);
}

// function to check if the two BSTs contain
// same set of elements
function checkBSTs(root1, root2)
{
    // Base cases
    if (root1 != null && root2 != null)
        return true;
    if ((root1 == null && root2 != null) ||
        (root1 != null && root2 == null))
        return false;

    // Create two hash sets and store
    // elements both BSTs in them.
    var s1 = new Set();
    var s2 = new Set();
    insertToHash(root1, s1);
    insertToHash(root2, s2);

    // Return true if both hash sets
    // contain same elements.
    return (s1==s2);
}

// Driver Code
// First BST
var root1 = newNode(15);
root1.left = newNode(10);
root1.right = newNode(20);
root1.left.left = newNode(5);
root1.left.right = newNode(12);
root1.right.right = newNode(25);

// Second BST
var root2 = newNode(15);
root2.left = newNode(12);
root2.right = newNode(20);
root2.left.left = newNode(5);
root2.left.left.right = newNode(10);
root2.right.right = newNode(25);

// check if two BSTs have same set of elements
if (checkBSTs(root1, root2))
    document.write("YES");
else
    document.write("NO");

</script>
```

**输出:**

```
YES
```

**时间复杂度** : O( n)，其中 n 是树中的节点数。
**辅助空间** : O( n)。
**方法 3** :我们知道了 BST 的一个有趣的特性，对 BST 的有序遍历会生成一个排序的数组。所以我们可以对两个 BST 进行多次遍历，生成两个数组，最后我们可以比较这两个数组。如果两个数组都相同，那么 BST 就有相同的元素集，否则就没有。

## C++

```
// CPP program to check if two BSTs contains
// same set of elements
#include<bits/stdc++.h>
using namespace std;

// BST Node
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create new Node
Node* newNode(int val)
{
    Node* temp = new Node;
    temp->data = val;
    temp->left = temp->right = NULL;
    return temp;
}

// function to insert elements of the
// tree to map m
void storeInorder(Node* root, vector<int> &v)
{
    if (!root)
        return;
    storeInorder(root->left, v);
    v.push_back(root->data);
    storeInorder(root->right, v);
}

// function to check if the two BSTs contain
// same set  of elements
bool checkBSTs(Node* root1, Node* root2)
{
    // Base cases
    if (!root1 && !root2)
        return true;
    if ((root1 && !root2) || (!root1 && root2))
        return false;

    // Create two vectors and store
    // inorder traversals of both BSTs
    // in them.
    vector<int> v1, v2;
    storeInorder(root1, v1);
    storeInorder(root2, v2);

    // Return true if both vectors are
    // identical
    return (v1 == v2);
}

// Driver program to check above functions
int main()
{
    // First BST
    Node* root1 = newNode(15);
    root1->left = newNode(10);
    root1->right = newNode(20);
    root1->left->left = newNode(5);
    root1->left->right = newNode(12);
    root1->right->right = newNode(25);

    // Second BST
    Node* root2 = newNode(15);
    root2->left = newNode(12);
    root2->right = newNode(20);
    root2->left->left = newNode(5);
    root2->left->left->right = newNode(10);
    root2->right->right = newNode(25);

    // check if two BSTs have same set of elements
    if (checkBSTs(root1, root2))
        cout << "YES";
    else
        cout << "NO";
    return 0;       
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two BSTs
// contain same set of elements
import java.util.*;

class GFG
{

// BST Node
static class Node
{
    int data;
    Node left;
    Node right;
};

// Utility function to create new Node
static Node newNode(int val)
{
    Node temp = new Node();
    temp.data = val;
    temp.left = temp.right = null;
    return temp;
}

// function to insert elements 
// of the tree to map m
static void storeInorder(Node root,
                         Vector<Integer> v)
{
    if (root == null)
        return;
    storeInorder(root.left, v);
    v.add(root.data);
    storeInorder(root.right, v);
}

// function to check if the two BSTs
// contain same set of elements
static boolean checkBSTs(Node root1, Node root2)
{
    // Base cases
    if (root1 != null && root2 != null)
        return true;
    if ((root1 == null && root2 != null) ||
        (root1 != null && root2 == null))
        return false;

    // Create two vectors and store
    // inorder traversals of both BSTs
    // in them.
    Vector<Integer> v1 = new Vector<Integer>();
    Vector<Integer> v2 = new Vector<Integer>();
    storeInorder(root1, v1);
    storeInorder(root2, v2);

    // Return true if both vectors are
    // identical
    return (v1 == v2);
}

// Driver Code
public static void main(String[] args)
{
    // First BST
    Node root1 = newNode(15);
    root1.left = newNode(10);
    root1.right = newNode(20);
    root1.left.left = newNode(5);
    root1.left.right = newNode(12);
    root1.right.right = newNode(25);

    // Second BST
    Node root2 = newNode(15);
    root2.left = newNode(12);
    root2.right = newNode(20);
    root2.left.left = newNode(5);
    root2.left.left.right = newNode(10);
    root2.right.right = newNode(25);

    // check if two BSTs have same set of elements
    if (checkBSTs(root1, root2))
        System.out.print("YES");
    else
        System.out.print("NO");
}    
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to check if two BSTs contains
# same set of elements

# BST Node
class Node:
    def __init__(self):
        self.val = 0
        self.left = None
        self.right = None

# Utility function to create Node
def Node_(val1):

    temp = Node()
    temp.val = val1
    temp.left = temp.right = None
    return temp

v = []

# function to insert elements of the
# tree to map m
def storeInorder(root):

    if (root == None):
        return
    storeInorder(root.left)
    v.append(root.data)
    storeInorder(root.right)

# function to check if the two BSTs contain
# same set of elements
def checkBSTs(root1, root2):

    # Base cases
    if (root1 != None and root2 != None) :
        return True
    if ((root1 == None and root2 != None) or \
        (root1 != None and root2 == None)):
        return False

    # Create two hash sets and store
    # elements both BSTs in them.
    v1 = []
    v2 = []
    v = v1
    storeInorder(root1)
    v1 = v
    v = v2
    storeInorder(root2)
    v2 = v

    # Return True if both hash sets
    # contain same elements.
    return (v1 == v2)

# Driver code

# First BST
root1 = Node_(15)
root1.left = Node_(10)
root1.right = Node_(20)
root1.left.left = Node_(5)
root1.left.right = Node_(12)
root1.right.right = Node_(25)

# Second BST
root2 = Node_(15)
root2.left = Node_(12)
root2.right = Node_(20)
root2.left.left = Node_(5)
root2.left.left.right = Node_(10)
root2.right.right = Node_(25)

# check if two BSTs have same set of elements
if (checkBSTs(root1, root2)):
    print("YES")
else:
    print("NO")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to check if two BSTs
// contain same set of elements
using System;
using System.Collections.Generic;

class GFG
{

// BST Node
class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Utility function to create new Node
static Node newNode(int val)
{
    Node temp = new Node();
    temp.data = val;
    temp.left = temp.right = null;
    return temp;
}

// function to insert elements
// of the tree to map m
static void storeInorder(Node root,
                         List<int> v)
{
    if (root == null)
        return;
    storeInorder(root.left, v);
    v.Add(root.data);
    storeInorder(root.right, v);
}

// function to check if the two BSTs
// contain same set of elements
static bool checkBSTs(Node root1,
                      Node root2)
{
    // Base cases
    if (root1 != null && root2 != null)
        return true;
    if ((root1 == null && root2 != null) ||
        (root1 != null && root2 == null))
        return false;

    // Create two vectors and store
    // inorder traversals of both BSTs
    // in them.
    List<int> v1 = new List<int>();
    List<int> v2 = new List<int>();
    storeInorder(root1, v1);
    storeInorder(root2, v2);

    // Return true if both vectors are
    // identical
    return (v1 == v2);
}

// Driver Code
public static void Main(String[] args)
{
    // First BST
    Node root1 = newNode(15);
    root1.left = newNode(10);
    root1.right = newNode(20);
    root1.left.left = newNode(5);
    root1.left.right = newNode(12);
    root1.right.right = newNode(25);

    // Second BST
    Node root2 = newNode(15);
    root2.left = newNode(12);
    root2.right = newNode(20);
    root2.left.left = newNode(5);
    root2.left.left.right = newNode(10);
    root2.right.right = newNode(25);

    // check if two BSTs have
    // same set of elements
    if (checkBSTs(root1, root2))
        Console.Write("YES");
    else
        Console.Write("NO");
}    
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to check if two BSTs
// contain same set of elements

    // BST Node
class Node {
    constructor() {
        this.data = 0;
        this.prev = null;
        this.next = null;
    }
}

    // Utility function to create new Node
    function newNode(val)
    {
        var temp = new Node();
        temp.data = val;
        temp.left = temp.right = null;
        return temp;
    }

    // function to insert elements
    // of the tree to map m
    function storeInorder(root, v) {
        if (root == null)
            return;
        storeInorder(root.left, v);
        v.push(root.data);
        storeInorder(root.right, v);
    }

    // function to check if the two BSTs
    // contain same set of elements
    function checkBSTs(root1,  root2)
    {
        // Base cases
        if (root1 != null && root2 != null)
            return true;
        if ((root1 == null && root2 != null) ||
            (root1 != null && root2 == null))
            return false;

        // Create two vectors and store
        // inorder traversals of both BSTs
        // in them.
        var v1 = [];
        var v2 = [];
        storeInorder(root1, v1);
        storeInorder(root2, v2);

        // Return true if both vectors are
        // identical
        return (v1 == v2);
    }

    // Driver Code

        // First BST
        var root1 = newNode(15);
        root1.left = newNode(10);
        root1.right = newNode(20);
        root1.left.left = newNode(5);
        root1.left.right = newNode(12);
        root1.right.right = newNode(25);

        // Second BST
        var root2 = newNode(15);
        root2.left = newNode(12);
        root2.right = newNode(20);
        root2.left.left = newNode(5);
        root2.left.left.right = newNode(10);
        root2.right.right = newNode(25);

        // check if two BSTs have same set of elements
        if (checkBSTs(root1, root2))
            document.write("YES");
        else
            document.write("NO");

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
YES
```

**时间复杂度** : O( n)。
**辅助空间** : O( n)。

本文由 [**哈什·阿加瓦尔**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。