# 根据给定的前序遍历构造 BST 集合 3(朴素方法)

> 原文:[https://www . geesforgeks . org/construct-BST-from-给定-preorder-遍历-set-3-幼稚-method/](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversal-set-3-naive-method/)

给定二叉查找树的前序遍历，构造 BST。
例如，如果给定的遍历是{10，5，1，7，40，50}，那么输出应该是跟随树的根。

```
    10
   /   \
  5     40
 /  \      \
1    7      50
```

我们已经在[之前的帖子](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)中讨论了构建二叉查找树的方法。这里是另一种方法来构造二叉查找树当给定的前序遍历。

我们知道 BST 的有序遍历以非递减的方式给出元素。因此，我们可以对给定的前序遍历进行排序，以获得二叉查找树的有序遍历。

我们已经在[这篇](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)帖子中学习了当给定了前序和中序遍历时构造树的方法。我们现在将使用相同的方法来构建 BST。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// A BST node has data, pointer to left
// child and pointer to right child
struct Node {
    int data;
    Node *left, *right;
};

// A utility function to create new node
Node* getNode(int data)
{
    Node* temp = new Node();
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

/* Recursive function to construct BST
Inorder traversal in[] and Preorder traversal
pre[]. Initial values of inStart and inEnd should be
0 and n -1.*/
Node* buildBTRec(int in[], int pre[], int inStart,
            int inEnd, unordered_map<int,int>& m)
{
    static int preIdx = 0;
    if (inStart > inEnd)
        return NULL;

    // Pick current node from Preorder traversal
    // using preIndex and increment preIndex
    int curr = pre[preIdx];
    ++preIdx;

    Node* temp = getNode(curr);

    // If this node has no children then return
    if (inStart == inEnd)
        return temp;

    // Else find the index of this node in
    // inorder traversal
    int idx = m[curr];

    // Using this index construct left and right subtrees
    temp->left = buildBTRec(in, pre, inStart, idx - 1, m);
    temp->right = buildBTRec(in, pre, idx + 1, inEnd, m);

    return temp;
}

// This function mainly creates a map to store
// the indices of all items so we can quickly
// access them later.
Node* buildBST(int pre[], int n)
{
    // Copy pre[] to in[] and sort it
    int in[n];
    for (int i = 0; i < n; i++)
        in[i] = pre[i];
    sort(in, in + n);
      unordered_map<int,int> m;
      for(int i=0;i<n;i++)
    {
     m[in[i]] = i;
    }
      return buildBTRec(in, pre, 0, n-1,m);
}

// Inorder Traversal of tree

void inorderTraversal(Node* node)
{
     if(node==NULL)
      return ;
      inorderTraversal(node->left);
      cout << node->data << " ";
      inorderTraversal(node->right);
}

// Driver Program
int main()
{
    int pre[] = { 100, 20, 10, 30, 200, 150, 300 };
    int n = sizeof(pre) / sizeof(pre[0]);

    Node* root = buildBST(pre, n);

    // Let's test the built tree by printing its
    // Inorder traversal
    cout << "Inorder traversal of the tree is \n";
    inorderTraversal(root);
    return 0;
}
```

## 蟒蛇 3

```
# A BST node has data, pointer to left
# child and pointer to right child
class Node:
    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# /* Recursive function to construct BST
# Inorder traversal in[] and Preorder traversal
# pre[]. Initial values of inStart and inEnd should be
# 0 and n -1.*/
def buildBTRec(inn, pre, inStart, inEnd):
    global m, preIdx

    if (inStart > inEnd):
        return None

    # Pick current node from Preorder traversal
    # using preIndex and increment preIndex
    curr = pre[preIdx]
    preIdx += 1

    temp = Node(curr)

    # If this node has no children then return
    if (inStart == inEnd):
        return temp

    # Else find the index of this node in
    # inorder traversal
    idx = m[curr]

    # Using this index construct left and right subtrees
    temp.left = buildBTRec(inn, pre, inStart, idx - 1)
    temp.right = buildBTRec(inn, pre, idx + 1, inEnd)

    return temp

# This function mainly creates a map to store
# the indices of all items so we can quickly
# access them later.
def buildBST(pre, n):
    global m

    # Copy pre[] to in[] and sort it
    inn=[0 for i in range(n)]

    for i in range(n):
        inn[i] = pre[i]

    inn = sorted(inn)

    for i in range(n):
        m[inn[i]] = i

    return buildBTRec(inn, pre, 0, n - 1)

def inorderTraversal(root):
    if (root == None):
        return
    inorderTraversal(root.left)
    print(root.data, end = " ")
    inorderTraversal(root.right)

# Driver Program
if __name__ == '__main__':
    m,preIdx = {}, 0
    pre = [100, 20, 10, 30, 200, 150, 300]
    n = len(pre)

    root = buildBST(pre, n)

    # Let's test the built tree by printing its
    # Inorder traversal
    print("Inorder traversal of the tree is")
    inorderTraversal(root)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// A BST node has data, pointer to left
// child and pointer to right child
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

/* Recursive function to construct BST
Inorder traversal in[] and Preorder traversal
pre[]. Initial values of inStart and inEnd should be
0 and n -1.*/
function buildBTRec(In, pre, inStart, inEnd)
{
    if (inStart > inEnd)
        return null;

    // Pick current node from Preorder traversal
    // using preIndex and increment preIndex
    let curr = pre[preIdx];
    ++preIdx;

    let temp = new Node(curr);

    // If this node has no children then return
    if (inStart == inEnd)
        return temp;

    // Else find the index of this node in
    // inorder traversal
    let idx = m.get(curr);

    // Using this index construct left and right subtrees
    temp.left = buildBTRec(In, pre, inStart, idx - 1);
    temp.right = buildBTRec(In, pre, idx + 1, inEnd);

    return temp;
}

// This function mainly creates a map to store
// the indices of all items so we can quickly
// access them later.
function buildBST(pre, n)
{

    // Copy pre[] to in[] and sort it
    let In = new Array(n);
    for(let i = 0; i < n; i++)
        In[i] = pre[i];

    In.sort(function(a, b){return a - b;});

    for(let i = 0; i < n; i++)
        m.set(In[i], i);

    return buildBTRec(In, pre, 0, n - 1)
}

function inorderTraversal(root)
{
    if (root == null)
        return;

    inorderTraversal(root.left);
    document.write(root.data + " ");
    inorderTraversal(root.right);
}

// Driver code
let m = new Map();
let preIdx = 0;
let pre = [ 100, 20, 10, 30, 200, 150, 300 ];
let n = pre.length;
let root = buildBST(pre, n);

// Let's test the built tree by printing its
// Inorder traversal
document.write("Inorder traversal of the tree is <br>");

inorderTraversal(root);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Inorder traversal of the tree is 
10 20 30 100 150 200 300
```

**时间复杂度:**排序需要 O(nlogn)时间，使用前序和中序遍历进行排序和构造需要线性时间。因此，上述解决方案的总时间复杂度为 0(nlogn)。
**辅助空间:** O(n)。