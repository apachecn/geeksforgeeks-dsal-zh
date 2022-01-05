# 计数阵列中的反转|集合 2(使用自平衡 BST)

> 原文:[https://www . geesforgeks . org/count-inversion-in-a-in-a-set-2-use-self-balancing-BST/](https://www.geeksforgeeks.org/count-inversions-in-an-array-set-2-using-self-balancing-bst/)

数组的反转计数表示数组离排序有多远(或多近)。如果一个数组已经排序，那么反转计数为 0。如果一个数组是按逆序排序的，那么逆序计数就是最大值。
如果 a[i] > a[j]和 i < j，则两个元素 a[i]和 a[j]形成反转，为了简单起见，我们可以假设所有元素都是唯一的。
**例:**

```
Input: arr[] = {8, 4, 2, 1}
Output: 6

Explanation: Given array has six inversions:
(8,4), (4,2),(8,2), (8,1), (4,1), (2,1).

Input: arr[] = {3, 1, 2}
Output: 2

Explanation:Given array has two inversions:
(3, 1), (3, 2)      
```

我们已经讨论了[朴素方法和基于合并排序的倒计数方法](https://www.geeksforgeeks.org/counting-inversions/)。
**上述帖子中解决方案的复杂性分析:**
**朴素方法的时间复杂性**是 O(n <sup>2</sup> )
**基于合并排序的方法的时间复杂性**是 O(n Log n)。
阅读本文前请先浏览 [AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)。
有一个更有效的方法来解决这个问题。
**方法:**思路是像[红黑树](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)[AVL 树](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)等一样使用自平衡二叉查找树，并对其进行扩充，使每个节点也能跟踪右子树中的节点数。因此，每个节点将包含其右子树中的节点数，即大于该数的节点数。所以可以看到，当有一对 *(a，b)* 时，计数增加，其中 a 出现在数组中的 b 之前， *a > b* 所以当数组从头到尾遍历时，将元素添加到 AVL 树中，新插入的节点在其右子树中的节点计数将是计数增加或对的数量 *(a，b)* 其中 b 是当前元素。
**算法:**

1.  创建一个 *AVL 树*，其属性是每个节点将包含其子树的大小。
2.  从头到尾遍历数组。
3.  对于每个元素，在 **AVL** 树中插入元素
4.  大于当前元素的节点数可以通过检查其右子树的大小来找到，因此可以保证当前节点右子树中的元素的索引小于当前元素，并且它们的值大于当前元素。所以这些元素符合标准。
5.  所以根据当前插入节点的右子树的大小来增加计数。
6.  显示计数。

**实施:**

## C++

```
// An AVL Tree based C++ program to count
// inversion in an array
#include<bits/stdc++.h>
using namespace std;

// An AVL tree node
struct Node
{
    int key, height;
    struct Node *left, *right;

// size of the tree rooted with this Node
    int size;
};

// A utility function to get the height of
// the tree rooted with N
int height(struct Node *N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// A utility function to size of the
// tree of rooted with N
int size(struct Node *N)
{
    if (N == NULL)
        return 0;
    return N->size;
}

/* Helper function that allocates a new Node with
the given key and NULL left and right pointers. */
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->key   = key;
    node->left   = node->right  = NULL;
    node->height = node->size = 1;
    return(node);
}

// A utility function to right rotate
// subtree rooted with y
struct Node *rightRotate(struct Node *y)
{
    struct Node *x = y->left;
    struct Node *T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left),
 height(y->right))+1;
    x->height = max(height(x->left),
 height(x->right))+1;

    // Update sizes
    y->size = size(y->left) + size(y->right) + 1;
    x->size = size(x->left) + size(x->right) + 1;

    // Return new root
    return x;
}

// A utility function to left rotate
// subtree rooted with x
struct Node *leftRotate(struct Node *x)
{
    struct Node *y = x->right;
    struct Node *T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    //  Update heights
    x->height = max(height(x->left), height(x->right))+1;
    y->height = max(height(y->left), height(y->right))+1;

    // Update sizes
    x->size = size(x->left) + size(x->right) + 1;
    y->size = size(y->left) + size(y->right) + 1;

    // Return new root
    return y;
}

// Get Balance factor of Node N
int getBalance(struct Node *N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

// Inserts a new key to the tree rotted with Node. Also, updates
// *result (inversion count)
struct Node* insert(struct Node* node, int key, int *result)
{
    /* 1.  Perform the normal BST rotation */
    if (node == NULL)
        return(newNode(key));

    if (key < node->key)
    {
        node->left  = insert(node->left, key, result);

        // UPDATE COUNT OF GREATE ELEMENTS FOR KEY
        *result = *result + size(node->right) + 1;
    }
    else
        node->right = insert(node->right, key, result);

    /* 2\. Update height and size of this ancestor node */
    node->height = max(height(node->left),
                       height(node->right)) + 1;
    node->size = size(node->left) + size(node->right) + 1;

    /* 3\. Get the balance factor of this ancestor node to
          check whether this node became unbalanced */
    int balance = getBalance(node);

    // If this node becomes unbalanced, then there are
    // 4 cases

    // Left Left Case
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node->left->key)
    {
        node->left =  leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node->right->key)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    /* return the (unchanged) node pointer */
    return node;
}

// The following function returns inversion count in arr[]
int getInvCount(int arr[], int n)
{
  struct Node *root = NULL;  // Create empty AVL Tree

  int result = 0;   // Initialize result

  // Starting from first element, insert all elements one by
  // one in an AVL tree.
  for (int i=0; i<n; i++)

     // Note that address of result is passed as insert
     // operation updates result by adding count of elements
     // greater than arr[i] on left of arr[i]
     root = insert(root, arr[i], &result);

  return result;
}

// Driver program to test above
int main()
{
    int arr[] = {8, 4, 2, 1};
    int n = sizeof(arr)/sizeof(int);
    cout << "Number of inversions count are : "
         << getInvCount(arr,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// AVL Tree based Java program to count
// inversion in an array
import java.util.*;

class GfG{

// Initialize result
static int result = 0;

// An AVL tree node
static class Node
{
    int key, height;
    Node left, right;

    // Size of the tree rooted
    // with this Node
    int size;
}

// A utility function to get the height of
// the tree rooted with N
static int height(Node N)
{
    if (N == null)
        return 0;

    return N.height;
}

// A utility function to size of the
// tree of rooted with N
static int size(Node N)
{
    if (N == null)
        return 0;

    return N.size;
}

// A utility function to create a new node
static Node newNode(int ele)
{
    Node temp = new Node();
    temp.key = ele;
    temp.left = null;
    temp.right = null;
    temp.height = 1;
    temp.size = 1;
    return temp;
}

// A utility function to right rotate
// subtree rooted with y
static Node rightRotate(Node y)
{
    Node x = y.left;
    Node T2 = x.right;

    // Perform rotation
    x.right = y;
    y.left = T2;

    // Update heights
    y.height = Math.max(height(y.left),
                        height(y.right)) + 1;
    x.height = Math.max(height(x.left),
                        height(x.right)) + 1;

    // Update sizes
    y.size = size(y.left) + size(y.right) + 1;
    x.size = size(x.left) + size(x.right) + 1;

    // Return new root
    return x;
}

// A utility function to left rotate
// subtree rooted with x
static Node leftRotate(Node x)
{
    Node y = x.right;
    Node T2 = y.left;

    // Perform rotation
    y.left = x;
    x.right = T2;

    // Update heights
    x.height = Math.max(height(x.left),
                        height(x.right)) + 1;
    y.height = Math.max(height(y.left),
                        height(y.right)) + 1;

    // Update sizes
    x.size = size(x.left) + size(x.right) + 1;
    y.size = size(y.left) + size(y.right) + 1;

    // Return new root
    return y;
}

// Get Balance factor of Node N
static int getBalance(Node N)
{
    if (N == null)
        return 0;

    return height(N.left) - height(N.right);
}

// Inserts a new key to the tree rotted
// with Node. Also, updates *result
// (inversion count)
static Node insert(Node node, int key)
{

    // 1\. Perform the normal BST rotation
    if (node == null)
        return (newNode(key));

    if (key < node.key)
    {
        node.left = insert(node.left, key);

        // UPDATE COUNT OF GREATE ELEMENTS FOR KEY
        result = result + size(node.right) + 1;
    }
    else
        node.right = insert(node.right, key);

    // 2\. Update height and size of
    // this ancestor node
    node.height = Math.max(height(node.left),
                           height(node.right)) + 1;
    node.size = size(node.left) +
                size(node.right) + 1;

    // 3\. Get the balance factor of this
    // ancestor node to check whether this
    // node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced,
    // then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node.left.key)
        return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node.right.key)
        return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node.left.key)
    {
        node.left = leftRotate(node.left);
        return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node.right.key)
    {
        node.right = rightRotate(node.right);
        return leftRotate(node);
    }

    // Return the (unchanged) node pointer
    return node;
}

// The following function returns inversion
// count in arr[]
static void getInvCount(int arr[], int n)
{

    // Create empty AVL Tree
    Node root = null;

    // Starting from first element,
    // insert all elements one by
    // one in an AVL tree.
    for(int i = 0; i < n; i++)

        // Note that address of result
        // is passed as insert operation
        // updates result by adding count
        // of elements greater than arr[i]
        // on left of arr[i]
        root = insert(root, arr[i]);
}

// Driver code
public static void main(String[] args)
{
    int[] arr = new int[] { 8, 4, 2, 1 };
    int n = arr.length;
    getInvCount(arr, n);

    System.out.print("Number of inversions " +
                     "count are : " + result);
}
}

// This code is contributed by tushar_bansal
```

## 蟒蛇 3

```
# An AVL Tree based Python program to
# count inversion in an array

# A utility function to get height of
# the tree rooted with N
def height(N):
    if N == None:
        return 0
    return N.height

# A utility function to size of the
# tree of rooted with N
def size(N):
    if N == None:
        return 0
    return N.size

# Helper function that allocates a new
# Node with the given key and NULL left
# and right pointers.
class newNode:
    def __init__(self, key):
        self.key = key
        self.left = self.right = None
        self.height = self.size = 1

# A utility function to right rotate
# subtree rooted with y
def rightRotate(y):
    x = y.left
    T2 = x.right

    # Perform rotation
    x.right = y
    y.left = T2

    # Update heights
    y.height = max(height(y.left),
                   height(y.right)) + 1
    x.height = max(height(x.left),
                   height(x.right)) + 1

    # Update sizes
    y.size = size(y.left) + size(y.right) + 1
    x.size = size(x.left) + size(x.right) + 1

    # Return new root
    return x

# A utility function to left rotate
# subtree rooted with x
def leftRotate(x):
    y = x.right
    T2 = y.left

    # Perform rotation
    y.left = x
    x.right = T2

    # Update heights
    x.height = max(height(x.left),
                   height(x.right)) + 1
    y.height = max(height(y.left),
                   height(y.right)) + 1

    # Update sizes
    x.size = size(x.left) + size(x.right) + 1
    y.size = size(y.left) + size(y.right) + 1

    # Return new root
    return y

# Get Balance factor of Node N
def getBalance(N):
    if N == None:
        return 0
    return height(N.left) - height(N.right)

# Inserts a new key to the tree rotted
# with Node. Also, updates *result (inversion count)
def insert(node, key, result):

    # 1\. Perform the normal BST rotation
    if node == None:
        return newNode(key)

    if key < node.key:
        node.left = insert(node.left, key, result)

        # UPDATE COUNT OF GREATE ELEMENTS FOR KEY
        result[0] = result[0] + size(node.right) + 1
    else:
        node.right = insert(node.right, key, result)

    # 2\. Update height and size of this ancestor node
    node.height = max(height(node.left),   
                      height(node.right)) + 1
    node.size = size(node.left) + size(node.right) + 1

    # 3\. Get the balance factor of this ancestor
    #     node to check whether this node became
    #    unbalanced
    balance = getBalance(node)

    # If this node becomes unbalanced, 
    # then there are 4 cases

    # Left Left Case
    if (balance > 1 and key < node.left.key):
        return rightRotate(node)

    # Right Right Case
    if (balance < -1 and key > node.right.key):
        return leftRotate(node)

    # Left Right Case
    if balance > 1 and key > node.left.key:
        node.left = leftRotate(node.left)
        return rightRotate(node)

    # Right Left Case
    if balance < -1 and key < node.right.key:
        node.right = rightRotate(node.right)
        return leftRotate(node)

    # return the (unchanged) node pointer
    return node

# The following function returns
# inversion count in arr[]
def getInvCount(arr, n):
    root = None # Create empty AVL Tree

    result = [0] # Initialize result

    # Starting from first element, insert all
    # elements one by one in an AVL tree.
    for i in range(n):

        # Note that address of result is passed
        # as insert operation updates result by
        # adding count of elements greater than
        # arr[i] on left of arr[i]
        root = insert(root, arr[i], result)

    return result[0]

# Driver Code
if __name__ == '__main__':
    arr = [8, 4, 2, 1]
    n = len(arr)
    print("Number of inversions count are :",
                         getInvCount(arr, n))

# This code is contributed by PranchalK
```

## C#

```
// AVL Tree based C# program to count
// inversion in an array
using System;
class GfG
{

  // Initialize result
  static int result = 0;

  // An AVL tree node
  public
    class Node
    {
      public
        int key, height;
      public
        Node left, right;

      // Size of the tree rooted
      // with this Node
      public
        int size;
    }

  // A utility function to get the height of
  // the tree rooted with N
  static int height(Node N)
  {
    if (N == null)
      return 0; 
    return N.height;
  }

  // A utility function to size of the
  // tree of rooted with N
  static int size(Node N)
  {
    if (N == null)
      return 0;      
    return N.size;
  }

  // A utility function to create a new node
  static Node newNode(int ele)
  {
    Node temp = new Node();
    temp.key = ele;
    temp.left = null;
    temp.right = null;
    temp.height = 1;
    temp.size = 1;
    return temp;
  }

  // A utility function to right rotate
  // subtree rooted with y
  static Node rightRotate(Node y)
  {
    Node x = y.left;
    Node T2 = x.right;

    // Perform rotation
    x.right = y;
    y.left = T2;

    // Update heights
    y.height = Math.Max(height(y.left),
                        height(y.right)) + 1;
    x.height = Math.Max(height(x.left),
                        height(x.right)) + 1;

    // Update sizes
    y.size = size(y.left) + size(y.right) + 1;
    x.size = size(x.left) + size(x.right) + 1;

    // Return new root
    return x;
  }

  // A utility function to left rotate
  // subtree rooted with x
  static Node leftRotate(Node x)
  {
    Node y = x.right;
    Node T2 = y.left;

    // Perform rotation
    y.left = x;
    x.right = T2;

    // Update heights
    x.height = Math.Max(height(x.left),
                        height(x.right)) + 1;
    y.height = Math.Max(height(y.left),
                        height(y.right)) + 1;

    // Update sizes
    x.size = size(x.left) + size(x.right) + 1;
    y.size = size(y.left) + size(y.right) + 1;

    // Return new root
    return y;
  }

  // Get Balance factor of Node N
  static int getBalance(Node N)
  {
    if (N == null)
      return 0;    
    return height(N.left) - height(N.right);
  }

  // Inserts a new key to the tree rotted
  // with Node. Also, updates *result
  // (inversion count)
  static Node insert(Node node, int key)
  {

    // 1\. Perform the normal BST rotation
    if (node == null)
      return (newNode(key));
    if (key < node.key)
    {
      node.left = insert(node.left, key);

      // UPDATE COUNT OF GREATE ELEMENTS FOR KEY
      result = result + size(node.right) + 1;
    }
    else
      node.right = insert(node.right, key);

    // 2\. Update height and size of
    // this ancestor node
    node.height = Math.Max(height(node.left),
                           height(node.right)) + 1;
    node.size = size(node.left) +
      size(node.right) + 1;

    // 3\. Get the balance factor of this
    // ancestor node to check whether this
    // node became unbalanced
    int balance = getBalance(node);

    // If this node becomes unbalanced,
    // then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < node.left.key)
      return rightRotate(node);

    // Right Right Case
    if (balance < -1 && key > node.right.key)
      return leftRotate(node);

    // Left Right Case
    if (balance > 1 && key > node.left.key)
    {
      node.left = leftRotate(node.left);
      return rightRotate(node);
    }

    // Right Left Case
    if (balance < -1 && key < node.right.key)
    {
      node.right = rightRotate(node.right);
      return leftRotate(node);
    }

    // Return the (unchanged) node pointer
    return node;
  }

  // The following function returns inversion
  // count in []arr
  static void getInvCount(int []arr, int n)
  {

    // Create empty AVL Tree
    Node root = null;

    // Starting from first element,
    // insert all elements one by
    // one in an AVL tree.
    for(int i = 0; i < n; i++)

      // Note that address of result
      // is passed as insert operation
      // updates result by adding count
      // of elements greater than arr[i]
      // on left of arr[i]
      root = insert(root, arr[i]);
  }

  // Driver code
  public static void Main(String[] args)
  {
    int[] arr = new int[] { 8, 4, 2, 1 };
    int n = arr.Length;
    getInvCount(arr, n);

    Console.Write("Number of inversions " +
                  "count are : " + result);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// AVL Tree based javascript program to count
// inversion in an

    // Initialize result
    var result = 0;

    // An AVL tree node
     class Node {
     constructor(){
         this.key = 0, this.height = 0;
         this.left = null, this.right = null;

        // Size of the tree rooted
        // with this Node
        this.size = 0;
        }
    }

    // A utility function to get the height of
    // the tree rooted with N
    function height(N) {
        if (N == null)
            return 0;

        return N.height;
    }

    // A utility function to size of the
    // tree of rooted with N
    function size(N) {
        if (N == null)
            return 0;

        return N.size;
    }

    // A utility function to create a new node
    function newNode(ele) {
    var temp = new Node();
        temp.key = ele;
        temp.left = null;
        temp.right = null;
        temp.height = 1;
        temp.size = 1;
        return temp;
    }

    // A utility function to right rotate
    // subtree rooted with y
    function rightRotate(y) {
    var x = y.left;
    var T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = Math.max(height(y.left),
        height(y.right)) + 1;
        x.height = Math.max(height(x.left),
        height(x.right)) + 1;

        // Update sizes
        y.size = size(y.left) + size(y.right) + 1;
        x.size = size(x.left) + size(x.right) + 1;

        // Return new root
        return x;
    }

    // A utility function to left rotate
    // subtree rooted with x
    function leftRotate(x) {
     var y = x.right;
     var T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = Math.max(height(x.left),
        height(x.right)) + 1;
        y.height = Math.max(height(y.left),
        height(y.right)) + 1;

        // Update sizes
        x.size = size(x.left) + size(x.right) + 1;
        y.size = size(y.left) + size(y.right) + 1;

        // Return new root
        return y;
    }

    // Get Balance factor of Node N
    function getBalance(N) {
        if (N == null)
            return 0;

        return height(N.left) - height(N.right);
    }

    // Inserts a new key to the tree rotted
    // with Node. Also, updates *result
    // (inversion count)
    function insert(node , key) {

        // 1\. Perform the normal BST rotation
        if (node == null)
            return (newNode(key));

        if (key < node.key) {
            node.left = insert(node.left, key);

            // UPDATE COUNT OF GREATE ELEMENTS FOR KEY
            result = result + size(node.right) + 1;
        } else
            node.right = insert(node.right, key);

        // 2\. Update height and size of
        // this ancestor node
        node.height = Math.max(height(node.left),
        height(node.right)) + 1;
        node.size = size(node.left) +
         size(node.right) + 1;

        // 3\. Get the balance factor of this
        // ancestor node to check whether this
        // node became unbalanced
        var balance = getBalance(node);

        // If this node becomes unbalanced,
        // then there are 4 cases

        // Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        // Return the (unchanged) node pointer
        return node;
    }

    // The following function returns inversion
    // count in arr
    function getInvCount(arr , n) {

        // Create empty AVL Tree
       var root = null;

        // Starting from first element,
        // insert all elements one by
        // one in an AVL tree.
        for (i = 0; i < n; i++)

            // Note that address of result
            // is passed as insert operation
            // updates result by adding count
            // of elements greater than arr[i]
            // on left of arr[i]
            root = insert(root, arr[i]);
    }

    // Driver code

        var arr = [ 8, 4, 2, 1 ];
        var n = arr.length;
        getInvCount(arr, n);

        document.write("Number of inversions " +
        "count are : " + result);

// This code contributed by aashish1995

</script>
```

**输出:**

```
Number of inversions count are: 6
```

**复杂度分析:**

*   **时间复杂度:** O(n Log n)。
    在 AVL 插入中的插入需要 O(log n)时间，并且 n 个元素被插入到树中，因此时间复杂度为 O(n log n)。
*   **空间复杂度:** O(n)。
    要创建一个最多有 n 个节点的 AVL 树，需要 O(n)个额外空间。

[用 C++ STL 中的 Set 计算逆序。](http://geeksquiz.com/counting-inversions-using-set-in-c-stl/)
我们将很快讨论[基于二进制索引树](https://www.geeksforgeeks.org/binary-indexed-tree-or-fenwick-tree-2/)的方法。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息