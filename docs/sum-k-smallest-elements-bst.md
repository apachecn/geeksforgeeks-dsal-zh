# BST 中 k 个最小元素之和

> 原文:[https://www.geeksforgeeks.org/sum-k-smallest-elements-bst/](https://www.geeksforgeeks.org/sum-k-smallest-elements-bst/)

鉴于[二叉查找树](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。任务是找出小于等于 Kth 最小元素的所有元素的和。
**例:**

```
Input :  K = 3
              8
            /   \
           7     10
         /      /   \
        2      9     13
Output : 17
Explanation : Kth smallest element is 8 so sum of all
              element smaller then or equal to 8 are
              2 + 7 + 8

Input : K = 5
           8
         /   \
        5    11
      /  \
     2    7
      \
       3
Output :  25
```

**方法 1(不改变 BST 节点结构)**
思路是在有序遍历中遍历 BST。请注意，BST 的有序遍历以排序(或递增)的顺序访问元素。遍历时，我们跟踪访问节点的计数，并不断添加节点，直到计数变为 k 为止

## C++

```
// c++ program to find Sum Of All Elements smaller
// than or equal to Kth Smallest Element In BST
#include <bits/stdc++.h>
using namespace std;

/* Binary tree Node */
struct Node
{
    int data;
    Node* left, * right;
};

// utility function new Node of BST
struct Node *createNode(int data)
{
    Node * new_Node = new Node;
    new_Node->left = NULL;
    new_Node->right = NULL;
    new_Node->data = data;
    return new_Node;
}

// A utility function to insert a new Node
//  with given key in BST and also maintain lcount ,Sum
struct Node * insert(Node *root, int key)
{
    // If the tree is empty, return a new Node
    if (root == NULL)
        return createNode(key);

    // Otherwise, recur down the tree
    if (root->data > key)
        root->left = insert(root->left, key);

    else if (root->data < key)
        root->right = insert(root->right, key);

    // return the (unchanged) Node pointer
    return root;
}

// function return sum of all element smaller than
// and equal to Kth smallest element
int ksmallestElementSumRec(Node *root, int k, int &count)
{
    // Base cases
    if (root == NULL)
        return 0;
    if (count > k)
        return 0;

    // Compute sum of elements in left subtree
    int res = ksmallestElementSumRec(root->left, k, count);
    if (count >= k)
        return res;

    // Add root's data
    res += root->data;

    // Add current Node
    count++;
    if (count >= k)
      return res;

    // If count is less than k, return right subtree Nodes
    return res + ksmallestElementSumRec(root->right, k, count);
}

// Wrapper over ksmallestElementSumRec()
int ksmallestElementSum(struct Node *root, int k)
{
   int count = 0;
   ksmallestElementSumRec(root, k, count);
}

/* Driver program to test above functions */
int main()
{

    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node *root = NULL;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    int k = 3;
    cout <<  ksmallestElementSum(root, k) <<endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum Of All Elements smaller
// than or equal to Kth Smallest Element In BST
import java.util.*;
class GFG
{

  /* Binary tree Node */
  static class Node
  {
    int data;
    Node left,  right;
  };

  // utility function new Node of BST
  static Node createNode(int data)
  {
    Node  new_Node = new Node();
    new_Node.left = null;
    new_Node.right = null;
    new_Node.data = data;
    return new_Node;
  }

  // A utility function to insert a new Node
  //  with given key in BST and also maintain lcount ,Sum
  static Node  insert(Node root, int key)
  {

    // If the tree is empty, return a new Node
    if (root == null)
      return createNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
      root.left = insert(root.left, key);
    else if (root.data < key)
      root.right = insert(root.right, key);

    // return the (unchanged) Node pointer
    return root;
  }

  static int count = 0;

  // function return sum of all element smaller than
  // and equal to Kth smallest element
  static int ksmallestElementSumRec(Node root, int k)
  {

    // Base cases
    if (root == null)
      return 0;
    if (count > k)
      return 0;

    // Compute sum of elements in left subtree
    int res = ksmallestElementSumRec(root.left, k);
    if (count >= k)
      return res;

    // Add root's data
    res += root.data;

    // Add current Node
    count++;
    if (count >= k)
      return res;

    // If count is less than k, return right subtree Nodes
    return res + ksmallestElementSumRec(root.right, k);
  }

  // Wrapper over ksmallestElementSumRec()
  static int ksmallestElementSum(Node root, int k)
  {

    int res = ksmallestElementSumRec(root, k);
    return res;
  }

  /* Driver program to test above functions */
  public static void main(String[] args)
  {

    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node root = null;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    int k = 3;
    int count = ksmallestElementSum(root, k);
    System.out.println(count);
  }
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to find Sum Of All
# Elements smaller than or equal to
# Kth Smallest Element In BST

INT_MAX = 2147483647

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class createNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# A utility function to insert a new
# Node with given key in BST and also
# maintain lcount ,Sum
def insert(root, key) :

    # If the tree is empty, return a new Node
    if (root == None) :
        return createNode(key)

    # Otherwise, recur down the tree
    if (root.data > key) :
        root.left = insert(root.left, key)

    elif (root.data < key):
        root.right = insert(root.right, key)

    # return the (unchanged) Node pointer
    return root

# function return sum of all element smaller
# than and equal to Kth smallest element
def ksmallestElementSumRec(root, k, count) :

    # Base cases
    if (root == None) :
        return 0
    if (count[0] > k[0]) :
        return 0

    # Compute sum of elements in left subtree
    res = ksmallestElementSumRec(root.left, k, count)
    if (count[0] >= k[0]) :
        return res

    # Add root's data
    res += root.data

    # Add current Node
    count[0] += 1
    if (count[0] >= k[0]) :
        return res

    # If count is less than k, return
    # right subtree Nodes
    return res + ksmallestElementSumRec(root.right,
                                        k, count)

# Wrapper over ksmallestElementSumRec()
def ksmallestElementSum(root, k):
    count = [0]
    return ksmallestElementSumRec(root, k, count)

# Driver Code
if __name__ == '__main__':

    """ 20
        / \
    8 22
    / \
    4 12
        / \
        10 14
        """
    root = None
    root = insert(root, 20)
    root = insert(root, 8)
    root = insert(root, 4)
    root = insert(root, 12)
    root = insert(root, 10)
    root = insert(root, 14)
    root = insert(root, 22)

    k = [3]
    print(ksmallestElementSum(root, k))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find Sum Of All Elements smaller
// than or equal to Kth Smallest Element In BST
using System;

public class GFG
{

  /* Binary tree Node */
  public class Node
  {
    public int data;
    public Node left,  right;
  };

  // utility function new Node of BST
  static Node createNode(int data)
  {
    Node  new_Node = new Node();
    new_Node.left = null;
    new_Node.right = null;
    new_Node.data = data;
    return new_Node;
  }

  // A utility function to insert a new Node
  //  with given key in BST and also maintain lcount ,Sum
  static Node  insert(Node root, int key)
  {

    // If the tree is empty, return a new Node
    if (root == null)
      return createNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
      root.left = insert(root.left, key);
    else if (root.data < key)
      root.right = insert(root.right, key);

    // return the (unchanged) Node pointer
    return root;
  }
  static int count = 0;

  // function return sum of all element smaller than
  // and equal to Kth smallest element
  static int ksmallestElementSumRec(Node root, int k)
  {

    // Base cases
    if (root == null)
      return 0;
    if (count > k)
      return 0;

    // Compute sum of elements in left subtree
    int res = ksmallestElementSumRec(root.left, k);
    if (count >= k)
      return res;

    // Add root's data
    res += root.data;

    // Add current Node
    count++;
    if (count >= k)
      return res;

    // If count is less than k, return right subtree Nodes
    return res + ksmallestElementSumRec(root.right, k);
  }

  // Wrapper over ksmallestElementSumRec()
  static int ksmallestElementSum(Node root, int k)
  {

    int res = ksmallestElementSumRec(root, k);
    return res;
  }

  /* Driver program to test above functions */
  public static void Main(String[] args)
  {

    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node root = null;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);
    int k = 3;
    int count = ksmallestElementSum(root, k);
    Console.WriteLine(count);
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to find
// Sum Of All Elements smaller
// than or equal to Kth Smallest Element In BST
 /* Binary tree Node */
class Node {
    constructor() {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

  // utility function new Node of BST
  function createNode(data)
  {
    var  new_Node = new Node();
    new_Node.left = null;
    new_Node.right = null;
    new_Node.data = data;
    return new_Node;
  }

  // A utility function to insert a new Node
  //  with given key in BST and also maintain lcount ,Sum
  function  insert(root , key)
  {

    // If the tree is empty, return a new Node
    if (root == null)
      return createNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
      root.left = insert(root.left, key);
    else if (root.data < key)
      root.right = insert(root.right, key);

    // return the (unchanged) Node pointer
    return root;
  }
  var count = 0;

  // function return sum of all element smaller than
  // and equal to Kth smallest element
  function ksmallestElementSumRec(root , k)
  {

    // Base cases
    if (root == null)
      return 0;
    if (count > k)
      return 0;

    // Compute sum of elements in left subtree
    var res = ksmallestElementSumRec(root.left, k);
    if (count >= k)
      return res;

    // Add root's data
    res += root.data;

    // Add current Node
    count++;
    if (count >= k)
      return res;

    // If count is less than k, return right subtree Nodes
    return res + ksmallestElementSumRec(root.right, k);
  }

  // Wrapper over ksmallestElementSumRec()
  function ksmallestElementSum(root , k)
  {

    var res = ksmallestElementSumRec(root, k);
    return res;
  }

  /* Driver program to test above functions */

    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    var root = null;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    var k = 3;
    var count = ksmallestElementSum(root, k);
    document.write(count);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
22
```

**时间复杂度:** O(k)

**方法 2(有效并改变 BST 的结构)**
我们可以在 O(h)时间内找到所需的和，其中 h 是 BST 的高度。想法类似于[BST](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-bst-order-statistics-in-bst/)中的第 k 个最小元素。这里我们使用增广树数据结构在 O(h)时间内有效地解决了这个问题[ h 是 BST 的高度]。
算法:

```
BST Node contain to extra fields : Lcount , Sum

For each Node of BST
lCount : store how many left child it has
Sum     : store sum of all left child it has

Find Kth smallest element
[ temp_sum store sum of all element less than equal to K ]

ksmallestElementSumRec(root, K, temp_sum)

  IF root -> lCount == K + 1
      temp_sum += root->data + root->sum;
      break;
  ELSE
     IF k > root->lCount   // Goto right sub-tree
        temp_sum += root->data + root-> sum;
        ksmallestElementSumRec(root->right, K-root->lcount+1, temp_sum)
     ELSE
        // Goto left sun-tree
        ksmallestElementSumRec( root->left, K, temp_sum)
```

以下是上述算法的实现:

## C++

```
// C++ program to find Sum Of All Elements smaller
// than or equal t Kth Smallest Element In BST
#include <bits/stdc++.h>
using namespace std;

/* Binary tree Node */
struct Node
{
    int data;
    int lCount;
    int Sum ;
    Node* left;
    Node* right;
};

//utility function new Node of BST
struct Node *createNode(int data)
{
    Node * new_Node = new Node;
    new_Node->left = NULL;
    new_Node->right = NULL;
    new_Node->data = data;
    new_Node->lCount = 0 ;
    new_Node->Sum = 0;
    return new_Node;
}

// A utility function to insert a new Node with
// given key in BST and also maintain lcount ,Sum
struct Node * insert(Node *root, int key)
{
    // If the tree is empty, return a new Node
    if (root == NULL)
        return createNode(key);

    // Otherwise, recur down the tree
    if (root->data > key)
    {
        // increment lCount of current Node
        root->lCount++;

        // increment current Node sum by adding
        // key into it
        root->Sum += key;

        root->left= insert(root->left , key);
    }
    else if (root->data < key )
        root->right= insert (root->right , key );

    // return the (unchanged) Node pointer
    return root;
}

// function return sum of all element smaller than and equal
// to Kth smallest element
void ksmallestElementSumRec(Node *root, int k , int &temp_sum)
{
    if (root == NULL)
        return ;

    // if we fount k smallest element then break the function
    if ((root->lCount + 1) == k)
    {
        temp_sum += root->data + root->Sum ;
        return ;
    }

    else if (k > root->lCount)
    {
        // store sum of all element smaller than current root ;
        temp_sum += root->data + root->Sum;

        // decremented k and call right sub-tree
        k = k -( root->lCount + 1);
        ksmallestElementSumRec(root->right , k , temp_sum);
    }
    else // call left sub-tree
        ksmallestElementSumRec(root->left , k , temp_sum );
}

// Wrapper over ksmallestElementSumRec()
int ksmallestElementSum(struct Node *root, int k)
{
    int sum = 0;
    ksmallestElementSumRec(root, k, sum);
    return sum;
}

/* Driver program to test above functions */
int main()
{
    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node *root = NULL;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    int k = 3;
    cout <<  ksmallestElementSum(root, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Sum Of All Elements smaller
// than or equal t Kth Smallest Element In BST

import java.util.*;

class GFG{

/* Binary tree Node */
static class Node
{
    int data;
    int lCount;
    int Sum ;
    Node left;
    Node right;
};

//utility function new Node of BST
static Node createNode(int data)
{
    Node  new_Node = new Node();
    new_Node.left = null;
    new_Node.right = null;
    new_Node.data = data;
    new_Node.lCount = 0 ;
    new_Node.Sum = 0;
    return new_Node;
}

// A utility function to insert a new Node with
// given key in BST and also maintain lcount ,Sum
static Node  insert(Node root, int key)
{
    // If the tree is empty, return a new Node
    if (root == null)
        return createNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
    {
        // increment lCount of current Node
        root.lCount++;

        // increment current Node sum by adding
        // key into it
        root.Sum += key;

        root.left= insert(root.left , key);
    }
    else if (root.data < key )
        root.right= insert (root.right , key );

    // return the (unchanged) Node pointer
    return root;
}

static int temp_sum;
// function return sum of all element smaller than and equal
// to Kth smallest element
static void ksmallestElementSumRec(Node root, int k )
{
    if (root == null)
        return ;

    // if we fount k smallest element then break the function
    if ((root.lCount + 1) == k)
    {
        temp_sum += root.data + root.Sum ;
        return ;
    }

    else if (k > root.lCount)
    {
        // store sum of all element smaller than current root ;
        temp_sum += root.data + root.Sum;

        // decremented k and call right sub-tree
        k = k -( root.lCount + 1);
        ksmallestElementSumRec(root.right , k );
    }
    else // call left sub-tree
        ksmallestElementSumRec(root.left , k );
}

// Wrapper over ksmallestElementSumRec()
static void ksmallestElementSum(Node root, int k)
{
    temp_sum = 0;
    ksmallestElementSumRec(root, k);
}

/* Driver program to test above functions */
public static void main(String[] args)
{
    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node root = null;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    int k = 3;
     ksmallestElementSum(root, k);
     System.out.println(temp_sum);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to find Sum Of All Elements
# smaller than or equal t Kth Smallest Element In BST

# utility function new Node of BST
class createNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.lCount = 0
        self.Sum = 0
        self.left = None
        self.right = None

# A utility function to insert a new Node with
# given key in BST and also maintain lcount ,Sum
def insert(root, key):

    # If the tree is empty, return a new Node
    if root == None:
        return createNode(key)

    # Otherwise, recur down the tree
    if root.data > key:

        # increment lCount of current Node
        root.lCount += 1

        # increment current Node sum by
        # adding key into it
        root.Sum += key

        root.left= insert(root.left , key)
    elif root.data < key:
        root.right= insert (root.right , key)

    # return the (unchanged) Node pointer
    return root

# function return sum of all element smaller
# than and equal to Kth smallest element
def ksmallestElementSumRec(root, k , temp_sum):
    if root == None:
        return

    # if we fount k smallest element
    # then break the function
    if (root.lCount + 1) == k:
        temp_sum[0] += root.data + root.Sum
        return

    elif k > root.lCount:

        # store sum of all element smaller
        # than current root ;
        temp_sum[0] += root.data + root.Sum

        # decremented k and call right sub-tree
        k = k -( root.lCount + 1)
        ksmallestElementSumRec(root.right,
                               k, temp_sum)
    else: # call left sub-tree
        ksmallestElementSumRec(root.left,
                               k, temp_sum)

# Wrapper over ksmallestElementSumRec()
def ksmallestElementSum(root, k):
    Sum = [0]
    ksmallestElementSumRec(root, k, Sum)
    return Sum[0]

# Driver Code
if __name__ == '__main__':

    # 20
    # / \
    # 8     22
    # / \
    #4     12
    #     / \
    # 10 14
    #    
    root = None
    root = insert(root, 20)
    root = insert(root, 8)
    root = insert(root, 4)
    root = insert(root, 12)
    root = insert(root, 10)
    root = insert(root, 14)
    root = insert(root, 22)

    k = 3
    print(ksmallestElementSum(root, k))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find Sum Of All Elements smaller
// than or equal t Kth Smallest Element In BST
using System;
public class GFG
{

/* Binary tree Node */
public class Node
{
   public int data;
   public int lCount;
   public int Sum ;
   public Node left;
   public Node right;
};

// utility function new Node of BST
static Node createNode(int data)
{
    Node  new_Node = new Node();
    new_Node.left = null;
    new_Node.right = null;
    new_Node.data = data;
    new_Node.lCount = 0 ;
    new_Node.Sum = 0;
    return new_Node;
}

// A utility function to insert a new Node with
// given key in BST and also maintain lcount ,Sum
static Node  insert(Node root, int key)
{

    // If the tree is empty, return a new Node
    if (root == null)
        return createNode(key);

    // Otherwise, recur down the tree
    if (root.data > key)
    {

        // increment lCount of current Node
        root.lCount++;

        // increment current Node sum by adding
        // key into it
        root.Sum += key;
        root.left = insert(root.left , key);
    }
    else if (root.data < key )
        root.right = insert (root.right , key );

    // return the (unchanged) Node pointer
    return root;
}

static int temp_sum;

// function return sum of all element smaller than and equal
// to Kth smallest element
static void ksmallestElementSumRec(Node root, int k )
{
    if (root == null)
        return ;

    // if we fount k smallest element then break the function
    if ((root.lCount + 1) == k)
    {
        temp_sum += root.data + root.Sum ;
        return ;
    }

    else if (k > root.lCount)
    {

        // store sum of all element smaller than current root ;
        temp_sum += root.data + root.Sum;

        // decremented k and call right sub-tree
        k = k -( root.lCount + 1);
        ksmallestElementSumRec(root.right , k );
    }
    else // call left sub-tree
        ksmallestElementSumRec(root.left , k );
}

// Wrapper over ksmallestElementSumRec()
static void ksmallestElementSum(Node root, int k)
{
    temp_sum = 0;
    ksmallestElementSumRec(root, k);
}

/* Driver program to test above functions */
public static void Main(String[] args)
{
    /*    20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
    Node root = null;
    root = insert(root, 20);
    root = insert(root, 8);
    root = insert(root, 4);
    root = insert(root, 12);
    root = insert(root, 10);
    root = insert(root, 14);
    root = insert(root, 22);

    int k = 3;
     ksmallestElementSum(root, k);
     Console.WriteLine(temp_sum);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

      // JavaScript program to find Sum Of All Elements smaller
      // than or equal t Kth Smallest Element In BST
      /* Binary tree Node */
      class Node {
        constructor() {
          this.data = 0;
          this.lCount = 0;
          this.Sum = 0;
          this.left = null;
          this.right = null;
        }
      }

      // utility function new Node of BST
      function createNode(data) {
        var new_Node = new Node();
        new_Node.left = null;
        new_Node.right = null;
        new_Node.data = data;
        new_Node.lCount = 0;
        new_Node.Sum = 0;
        return new_Node;
      }

      // A utility function to insert a new Node with
      // given key in BST and also maintain lcount ,Sum
      function insert(root, key) {
        // If the tree is empty, return a new Node
        if (root == null) return createNode(key);

        // Otherwise, recur down the tree
        if (root.data > key) {
          // increment lCount of current Node
          root.lCount++;

          // increment current Node sum by adding
          // key into it
          root.Sum += key;
          root.left = insert(root.left, key);
        } else if (root.data < key)
        root.right = insert(root.right, key);

        // return the (unchanged) Node pointer
        return root;
      }

      var temp_sum = 0;

      // function return sum of all element smaller than and equal
      // to Kth smallest element
      function ksmallestElementSumRec(root, k) {
        if (root == null) return;

        // if we fount k smallest element then break the function
        if (root.lCount + 1 == k) {
          temp_sum += root.data + root.Sum;
          return;
        } else if (k > root.lCount) {
          // store sum of all element smaller than current root ;
          temp_sum += root.data + root.Sum;

          // decremented k and call right sub-tree
          k = k - (root.lCount + 1);
          ksmallestElementSumRec(root.right, k);
        } // call left sub-tree
        else ksmallestElementSumRec(root.left, k);
      }

      // Wrapper over ksmallestElementSumRec()
      function ksmallestElementSum(root, k) {
        temp_sum = 0;
        ksmallestElementSumRec(root, k);
      }

      /* Driver program to test above functions */
      /*  20
        /    \
       8     22
     /   \
    4     12
         /   \
        10    14
          */
      var root = null;
      root = insert(root, 20);
      root = insert(root, 8);
      root = insert(root, 4);
      root = insert(root, 12);
      root = insert(root, 10);
      root = insert(root, 14);
      root = insert(root, 22);

      var k = 3;
      ksmallestElementSum(root, k);
      document.write(temp_sum);

</script>
```

**输出:**

```
22
```

**时间复杂度:** O(h)，其中 h 为树高。

本文由 [**尼尚·辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。