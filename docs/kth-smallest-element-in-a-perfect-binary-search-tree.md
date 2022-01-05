# 完美二叉查找树中的第几个最小元素

> 原文:[https://www . geesforgeks . org/kth-完美二进制搜索树中的最小元素/](https://www.geeksforgeeks.org/kth-smallest-element-in-a-perfect-binary-search-tree/)

给定一个带有 **N** 节点的 [**完美 BST**](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/) 和一个整数 **K，**的任务是找到树中存在的 **K <sup>th</sup>** 最小元素。

**示例:**

```
Input:
K = 3, N = 15
               50 
            /     \ 
          30        70 
         /  \      /  \ 
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85   
Output: 25

Explanation: 
The 3rd smallest element
in the given BST is 25

Input: 
K = 9, N = 15
              50 
           /       \ 
          30        70 
         /  \      /  \ 
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85    
Output: 55

Explanation: 
The 9th smallest element
in the given BST is 55
```

**天真方法:**在一个完美的 BST 中进行[有序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)，比如 [morris 遍历](https://www.geeksforgeeks.org/morris-traversal-for-preorder/)或者递归求解，访问每个节点，返回第 kth 个访问键。完成这项任务需要 O(N)个时间复杂度。

**高效方法:**
由于给定的 BST 是完美的，并且整个树的节点数是已知的，所以解决问题的计算复杂度可以降低到 ***log(N)*** 。按照下面给出的步骤解决问题:

*   在一个完美的 BST 树(N)中，|N|将永远是奇数在一个完美的二叉树中，任何完美的 BST 中的中位数的位置都是 floor(|N|/2) + 1。
*   通过**将**总节点数除以**楼层** (| **N| / 2)，计算出每个子树的**节点数。****
*   如果 **:** ，则**完美 BST** 的左侧子树将始终包含**第 k 个最小元素**
    *   **K <位置(中值(N))=M** 这是因为 **M** 的第几个最小元素将总是大于 **K** 的第几个最小元素，并且右子树中的每个元素都将大于 **M** 的第几个最小元素
*   如果 **:** ，则**完美 BST** 的右子树将始终包含一个 **R** 次最小元素**T5**
    *   **K >位置(中值(N))=M，**在本例中，**K–位置(中值(N))=R** 是右子树中第 **R** 个最小元素。这是因为右子树中第 **R** 个最小元素比第 **M** 个最小元素大，左子树中每个元素都比第 **M** 个最小元素小，但是第 **R** 个最小元素比它们都大。当至少 **M** 较小的可能性可以忽略时，人们可能会认为 **R** 是新的数字。 **R** 第**T21】最小元素是 **K** 当循环到右子树时的第最小元素(但是要记住 R **！=** K！).**
*   如果 **K** 是**位置(中间值(T))，**则该节点包含完美 BST 中的 **Kth** 最小元素。

下面是上述方法的实现:

## C++

```
// C++ program to find K-th
// smallest element in a
// perfect BST
#include <bits/stdc++.h>
using namespace std;

// A BST node
struct Node
{
    int key;
    Node *left, *right;
};

// A utility function to
// create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to insert a
// new node with given key in BST
Node* insert(Node* node, int key)
{
    // If the tree is empty
    if (node == NULL)
        return newNode(key);

    // Recur down the left
    // subtree for smaller values
    if (key < node->key)
        node->left = insert(node->left, key);

    // Recur down the right
    // subtree for smaller values
    else if (key > node->key)
        node->right = insert(node->right, key);

    // Return the (unchanged) node pointer
    return node;
}

// FUnction to find Kth Smallest
// element in a perfect BST
bool KSmallestPerfectBST(Node* root, int k,
                         int treeSize,
                         int& kth_smallest)
{
    if (root == NULL)
        return false;

    // Find the median
    // (division operation is floored)
    int median_loc = (treeSize / 2) + 1;

    // If the element is at
    // the median
    if (k == median_loc)
    {
        kth_smallest = root->key;
        return true;
    }

    // calculate the number of nodes in the
    // right and left sub-trees
    // (division operation is floored)
    int newTreeSize = treeSize / 2;

    // If median is located higher
    if (k < median_loc)
    {
        return KSmallestPerfectBST(
            root->left, k,
            newTreeSize, kth_smallest);
    }

    // If median is located lower
    int newK = k - median_loc;
    return KSmallestPerfectBST(root->right, newK,
                               newTreeSize,
                               kth_smallest);
}

// Driver Code
int main()
{
    /* Let us create following BST
               50
           /       \
          30        70
         /  \      /  \
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85
       */
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);
    insert(root, 14);
    insert(root, 25);
    insert(root, 35);
    insert(root, 45);
    insert(root, 55);
    insert(root, 65);
    insert(root, 75);
    insert(root, 85);

    int n = 15, k = 5;
    int ans = -1;

    // Function call
    if (KSmallestPerfectBST(root, k, n, ans)) {

        cout << ans << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find K-th
// smallest element in a
// perfect BST
import java.util.*;

class GFG{

// A BST node
 static class Node
{
    int key;
    Node left, right;
};

static int kth_smallest;

// A utility function to
// create a new BST node
public static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// A utility function to insert a
// new node with given key in BST
static Node insert(Node node, int key)
{

    // If the tree is empty
    if (node == null)
        return newNode(key);

    // Recur down the left
    // subtree for smaller values
    if (key < node.key)
        node.left = insert(node.left, key);

    // Recur down the right
    // subtree for smaller values
    else if (key > node.key)
        node.right = insert(node.right, key);

    // Return the (unchanged) node pointer
    return node;
}

// FUnction to find Kth Smallest
// element in a perfect BST
static boolean KSmallestPerfectBST(Node root, int k,
                                   int treeSize)
{
    if (root == null)
        return false;

    // Find the median
    // (division operation is floored)
    int median_loc = (treeSize / 2) + 1;

    // If the element is at
    // the median
    if (k == median_loc)
    {
        kth_smallest = root.key;
        return true;
    }

    // calculate the number of nodes in the
    // right and left sub-trees
    // (division operation is floored)
    int newTreeSize = treeSize / 2;

    // If median is located higher
    if (k < median_loc)
    {
        return KSmallestPerfectBST(
            root.left, k,
            newTreeSize);
    }

    // If median is located lower
    int newK = k - median_loc;
    return KSmallestPerfectBST(root.right, newK,
                               newTreeSize);
}

// Driver Code
public static void main(String[] args)
{
    /* Let us create following BST
               50
           /       \
          30        70
         /  \      /  \
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85
       */
    Node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);
    insert(root, 14);
    insert(root, 25);
    insert(root, 35);
    insert(root, 45);
    insert(root, 55);
    insert(root, 65);
    insert(root, 75);
    insert(root, 85);

    int n = 15, k = 5;

    // Function call
    if (KSmallestPerfectBST(root, k, n))
    {
        System.out.print(kth_smallest + " ");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find K-th
# smallest element in a perfect BST
kth_smallest = 0

# A BST node
class newNode:

    def __init__(self, item):

        self.key = item
        self.left = None
        self.right = None

# A utility function to insert a
# new node with given key in BST
def insert(node, key):

    # If the tree is empty
    if (node == None):
        return newNode(key)

    # Recur down the left
    # subtree for smaller values
    if (key < node.key):
        node.left = insert(node.left, key)

    # Recur down the right
    # subtree for smaller values
    elif(key > node.key):
        node.right = insert(node.right, key)

    # Return the (unchanged) node pointer
    return node

# FUnction to find Kth Smallest
# element in a perfect BST
def KSmallestPerfectBST(root, k, treeSize):

    global kth_smallest

    if (root == None):
        return False

    # Find the median
    # (division operation is floored)
    median_loc = (treeSize // 2) + 1

    # If the element is at
    # the median
    if (k == median_loc):
        kth_smallest = root.key
        return True

    # Calculate the number of nodes in
    # the right and left sub-trees
    # (division operation is floored)
    newTreeSize = treeSize // 2

    # If median is located higher
    if (k < median_loc):
        return KSmallestPerfectBST(root.left,
                                   k, newTreeSize)

    # If median is located lower
    newK = k - median_loc
    return KSmallestPerfectBST(root.right, newK,
                               newTreeSize)

# Driver Code
if __name__ == '__main__':

    ''' Let us create following BST
              50
           /       \
          30        70
         /  \      /  \
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85
    '''
    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)
    insert(root, 14)
    insert(root, 25)
    insert(root, 35)
    insert(root, 45)
    insert(root, 55)
    insert(root, 65)
    insert(root, 75)
    insert(root, 85)

    n = 15
    k = 5

    # Function call
    if (KSmallestPerfectBST(root, k, n)):
        print(kth_smallest, end = " ")

# This code is contributed by ipg2016107
```

## C#

```
// C# program to find K-th
// smallest element in a
// perfect BST
using System;
class GFG{

// A BST node
 public class Node
 {
   public int key;
   public Node left,
               right;
 };

static int kth_smallest;

// A utility function to
// create a new BST node
public static Node newNode(int item)
{
  Node temp = new Node();
  temp.key = item;
  temp.left = temp.right = null;
  return temp;
}

// A utility function to
// insert a new node with
// given key in BST
static Node insert(Node node,
                   int key)
{   
  // If the tree is empty
  if (node == null)
    return newNode(key);

  // Recur down the left
  // subtree for smaller values
  if (key < node.key)
    node.left = insert(node.left,
                       key);

  // Recur down the right
  // subtree for smaller values
  else if (key > node.key)
    node.right = insert(node.right,
                        key);

  // Return the (unchanged)
  // node pointer
  return node;
}

// Function to find Kth Smallest
// element in a perfect BST
static bool KSmallestPerfectBST(Node root, int k,
                                int treeSize)
{
  if (root == null)
    return false;

  // Find the median
  // (division operation is floored)
  int median_loc = (treeSize / 2) + 1;

  // If the element is at
  // the median
  if (k == median_loc)
  {
    kth_smallest = root.key;
    return true;
  }

  // calculate the number of nodes 
  // in the right and left sub-trees
  // (division operation is floored)
  int newTreeSize = treeSize / 2;

  // If median is located higher
  if (k < median_loc)
  {
    return KSmallestPerfectBST(root.left, k,
                               newTreeSize);
  }

  // If median is located lower
  int newK = k - median_loc;
  return KSmallestPerfectBST(root.right, newK,
                             newTreeSize);
}

// Driver Code
public static void Main(String[] args)
{
  /* Let us create following BST
               50
           /       \
          30        70
         /  \      /  \
       20   40    60    80
       /\   /\    /\    / \
     14 25 35 45 55 65 75  85
       */
  Node root = null;
  root = insert(root, 50);
  insert(root, 30);
  insert(root, 20);
  insert(root, 40);
  insert(root, 70);
  insert(root, 60);
  insert(root, 80);
  insert(root, 14);
  insert(root, 25);
  insert(root, 35);
  insert(root, 45);
  insert(root, 55);
  insert(root, 65);
  insert(root, 75);
  insert(root, 85);

  int n = 15, k = 5;

  // Function call
  if (KSmallestPerfectBST(root,
                          k, n))
  {
    Console.Write(kth_smallest + " ");
  }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find K-th
// smallest element in a
// perfect BST

// A BST node
 class Node
 {
     constructor()
     {
         this.key = 0;
         this.left = null;
         this.right = null;
     }
 };

var kth_smallest;

// A utility function to
// create a new BST node
function newNode(item)
{
  var temp = new Node();
  temp.key = item;
  temp.left = temp.right = null;
  return temp;
}

// A utility function to
// insert a new node with
// given key in BST
function insert( node, key)
{   
  // If the tree is empty
  if (node == null)
    return newNode(key);

  // Recur down the left
  // subtree for smaller values
  if (key < node.key)
    node.left = insert(node.left,
                       key);

  // Recur down the right
  // subtree for smaller values
  else if (key > node.key)
    node.right = insert(node.right,
                        key);

  // Return the (unchanged)
  // node pointer
  return node;
}

// Function to find Kth Smallest
// element in a perfect BST
function KSmallestPerfectBST(root, k, treeSize)
{
  if (root == null)
    return false;

  // Find the median
  // (division operation is floored)
  var median_loc = parseInt(treeSize / 2) + 1;

  // If the element is at
  // the median
  if (k == median_loc)
  {
    kth_smallest = root.key;
    return true;
  }

  // calculate the number of nodes 
  // in the right and left sub-trees
  // (division operation is floored)
  var newTreeSize = parseInt(treeSize / 2);

  // If median is located higher
  if (k < median_loc)
  {
    return KSmallestPerfectBST(root.left, k,
                               newTreeSize);
  }

  // If median is located lower
  var newK = k - median_loc;
  return KSmallestPerfectBST(root.right, newK,
                             newTreeSize);
}

// Driver Code
/* Let us create following BST
             50
         /       \
        30        70
       /  \      /  \
     20   40    60    80
     /\   /\    /\    / \
   14 25 35 45 55 65 75  85
     */
var root = null;
root = insert(root, 50);
insert(root, 30);
insert(root, 20);
insert(root, 40);
insert(root, 70);
insert(root, 60);
insert(root, 80);
insert(root, 14);
insert(root, 25);
insert(root, 35);
insert(root, 45);
insert(root, 55);
insert(root, 65);
insert(root, 75);
insert(root, 85);
var n = 15, k = 5;
// Function call
if (KSmallestPerfectBST(root,
                        k, n))
{
  document.write(kth_smallest + " ");
}

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
35 
```

**时间复杂度:**O(Log(N))
T3】辅助空间: O(Log(N))