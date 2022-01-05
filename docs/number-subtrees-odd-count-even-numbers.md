# 奇数计数为偶数的子树数

> 原文:[https://www . geesforgeks . org/number-subtrees-奇数-计数-偶数/](https://www.geeksforgeeks.org/number-subtrees-odd-count-even-numbers/)

给定一棵二叉树，找出奇数计数为偶数的子树的数目。

**示例:**

```
Input :         2             
             /     \          
           1        3            
         /   \     /  \       
        4    10   8     5     
             /                
            6      
Output : 6
The subtrees are 4, 6,    1,      8,    3
                        /   \          /  \
                        4    10       8    5
                            /
                           6

               2             
             /     \          
           1        3            
         /   \     /  \       
        4    10   8     5     
             /                
            6   
```

这个想法是递归遍历树。对于每个节点，递归计算左右子树中的偶数。如果根也是偶数，那么加上它也算。如果计数变成奇数，则递增结果。

```
count = 0 // Initialize result

int countSubtrees(root)
{
  if (root == NULL)
    return 0;

  // count even numbers in left subtree
  int c = countSubtrees(root-> left);

  // Add count of even numbers in right subtree
  c += countSubtrees(root-> right);

  // check if root data is an even number
  if (root-> data % 2 == 0)
    c += 1;

  // If total count of even numbers
  // for the subtree is odd
  if (c % 2 != 0)
    count++;

  // return total count of even
  // numbers of the subtree
  return c;
}
```

## C++

```
// C++ implementation to find number of
// subtrees having odd count of even numbers
#include <bits/stdc++.h>
using namespace std;

/* A binary tree Node */
struct Node
{
    int data;
    struct Node* left, *right;
};

/* Helper function that allocates a new Node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

// Returns count of subtrees having odd count of
// even numbers
int countRec(struct Node* root, int *pcount)
{
    // base condition
    if (root == NULL)
        return 0;

    // count even nodes in left subtree
    int c = countRec(root->left, pcount);

    // Add even nodes in right subtree
    c += countRec(root->right, pcount);

    // Check if root data is an even number
    if (root->data % 2 == 0)
        c += 1;

    // if total count of even numbers
    // for the subtree is odd
    if (c % 2 != 0)
        (*pcount)++;

    // Total count of even nodes of the subtree
    return c;
}

// A wrapper over countRec()
int countSubtrees(Node *root)
{
    int count = 0;
    int *pcount = &count;
    countRec(root, pcount);
    return count;
}

// Driver program to test above
int main()
{
    // binary tree formation
    struct Node *root = newNode(2);   /*          2         */
    root->left        = newNode(1);   /*      /     \       */
    root->right       = newNode(3);   /*     1        3        */
    root->left->left  = newNode(4);   /*   /   \     /  \    */
    root->left->right = newNode(10);  /*  4    10   8     5  */
    root->right->left  = newNode(8);  /*       /             */
    root->right->right = newNode(5);  /*     6               */
    root->left->right->left = newNode(6);

    cout<<"Count = "<< countSubtrees(root);
    return 0;
}

// This code is contributed by famously.
```

## C

```
// C implementation to find number of
// subtrees having odd count of even numbers
#include <bits/stdc++.h>

/* A binary tree Node */
struct Node
{
    int data;
    struct Node* left, *right;
};

/* Helper function that allocates a new Node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

// Returns count of subtrees having odd count of
// even numbers
int countRec(struct Node* root, int *pcount)
{
    // base condition
    if (root == NULL)
        return 0;

    // count even nodes in left subtree
    int c = countRec(root->left, pcount);

    // Add even nodes in right subtree
    c += countRec(root->right, pcount);

    // Check if root data is an even number
    if (root->data % 2 == 0)
        c += 1;

    // if total count of even numbers
    // for the subtree is odd
    if (c % 2 != 0)
        (*pcount)++;

    // Total count of even nodes of the subtree
    return c;
}

// A wrapper over countRec()
int countSubtrees(Node *root)
{
    int count = 0;
    int *pcount = &count;
    countRec(root, pcount);
    return count;
}

// Driver program to test above
int main()
{
    // binary tree formation
    struct Node *root = newNode(2);   /*          2         */
    root->left        = newNode(1);   /*      /     \       */
    root->right       = newNode(3);   /*     1        3        */
    root->left->left  = newNode(4);   /*   /   \     /  \    */
    root->left->right = newNode(10);  /*  4    10   8     5  */
    root->right->left  = newNode(8);  /*       /             */
    root->right->right = newNode(5);  /*     6               */
    root->left->right->left = newNode(6);

    printf("Count = %d", countSubtrees(root));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find number of
// subtrees having odd count of even numbers
import java.util.*;
class GfG {

/* A binary tree Node */
static class Node
{
    int data;
    Node left, right;
}

/* Helper function that allocates a new Node with the
given data and NULL left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return(node);
}

// Returns count of subtrees having odd count of
// even numbers
static class P
{
    int pcount = 0;
}
static int countRec(Node root, P p)
{
    // base condition
    if (root == null)
        return 0;

    // count even nodes in left subtree
    int c = countRec(root.left, p);

    // Add even nodes in right subtree
    c += countRec(root.right, p);

    // Check if root data is an even number
    if (root.data % 2 == 0)
        c += 1;

    // if total count of even numbers
    // for the subtree is odd
    if (c % 2 != 0)
        (p.pcount)++;

    // Total count of even nodes of the subtree
    return c;
}

// A wrapper over countRec()
static int countSubtrees(Node root)
{
    P p = new P();
    countRec(root, p);
    return p.pcount;
}

// Driver program to test above
public static void main(String[] args)
{
    // binary tree formation
     Node root = newNode(2); /*         2         */
    root.left     = newNode(1); /*     /     \     */
    root.right     = newNode(3); /*     1     3     */
    root.left.left = newNode(4); /* / \     / \ */
    root.left.right = newNode(10); /* 4 10 8     5 */
    root.right.left = newNode(8); /*     /             */
    root.right.right = newNode(5); /*     6             */
    root.left.right.left = newNode(6);

System.out.println("Count = " + countSubtrees(root));
}
}
```

## 蟒蛇 3

```
# Python3 implementation to find number of
# subtrees having odd count of even numbers

# Helper class that allocates a new Node
# with the given data and None left and
# right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Returns count of subtrees having odd
# count of even numbers
def countRec(root, pcount):

    # base condition
    if (root == None):
        return 0

    # count even nodes in left subtree
    c = countRec(root.left, pcount)

    # Add even nodes in right subtree
    c += countRec(root.right, pcount)

    # Check if root data is an even number
    if (root.data % 2 == 0):
        c += 1

    # if total count of even numbers
    # for the subtree is odd
    if c % 2 != 0:
        pcount[0] += 1

    # Total count of even nodes of
    # the subtree
    return c

# A wrapper over countRec()
def countSubtrees(root):
    count = [0]
    pcount = count
    countRec(root, pcount)
    return count[0]

# Driver Code
if __name__ == '__main__':

    # binary tree formation
    root = newNode(2) #         2        
    root.left     = newNode(1) #     /     \    
    root.right     = newNode(3) #     1     3    
    root.left.left = newNode(4) # / \     / \
    root.left.right = newNode(10) # 4 10 8     5
    root.right.left = newNode(8) #     /            
    root.right.right = newNode(5) #     6            
    root.left.right.left = newNode(6)

    print("Count = ", countSubtrees(root))

# This code is contributed by PranchalK
```

## C#

```
// C# implementation to find number of
// subtrees having odd count of even numbers
using System;

class GFG
{

/* A binary tree Node */
public class Node
{
    public int data;
    public Node left, right;
}

/* Helper function that allocates
a new Node with the given data and
NULL left and right pointers. */
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;
    return(node);
}

// Returns count of subtrees
// having odd count of even numbers
public class P
{
    public int pcount = 0;
}

static int countRec(Node root, P p)
{
    // base condition
    if (root == null)
        return 0;

    // count even nodes in left subtree
    int c = countRec(root.left, p);

    // Add even nodes in right subtree
    c += countRec(root.right, p);

    // Check if root data is an even number
    if (root.data % 2 == 0)
        c += 1;

    // if total count of even numbers
    // for the subtree is odd
    if (c % 2 != 0)
        (p.pcount)++;

    // Total count of even nodes of the subtree
    return c;
}

// A wrapper over countRec()
static int countSubtrees(Node root)
{
    P p = new P();
    countRec(root, p);
    return p.pcount;
}

// Driver Code
public static void Main(String[] args)
{
    // binary tree formation
    Node root = newNode(2); /*         2         */
    root.left     = newNode(1); /*     /     \     */
    root.right     = newNode(3); /*     1     3     */
    root.left.left = newNode(4); /* / \     / \ */
    root.left.right = newNode(10); /* 4 10 8     5 */
    root.right.left = newNode(8); /*     /             */
    root.right.right = newNode(5); /*     6             */
    root.left.right.left = newNode(6);

    Console.WriteLine("Count = " +
                       countSubtrees(root));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find number of
// subtrees having odd count of even numbers

// A binary tree Node
class Node
{

    // Helper function that allocates a new
    // Node with the given data and NULL left
    // and right pointers.
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Returns count of subtrees having odd
// count of even numbers
class P
{
    constructor()
    {
        this.pcount = 0;
    }
}

function countRec(root, p)
{

    // Base condition
    if (root == null)
        return 0;

    // Count even nodes in left subtree
    let c = countRec(root.left, p);

    // Add even nodes in right subtree
    c += countRec(root.right, p);

    // Check if root data is an even number
    if (root.data % 2 == 0)
        c += 1;

    // If total count of even numbers
    // for the subtree is odd
    if (c % 2 != 0)
        (p.pcount)++;

    // Total count of even nodes
    // of the subtree
    return c;
}

// A wrapper over countRec()
function countSubtrees(root)
{
    let p = new P();
    countRec(root, p);
    return p.pcount;
}

// Driver code

// Binary tree formation
let root = new Node(2); /*               2         */
root.left = new Node(1); /*           /     \      */
root.right = new Node(3); /*         1       3     */
root.left.left = new Node(4); /*    / \     / \    */
root.left.right = new Node(10); /* 4   10  8   5   */
root.right.left = new Node(8); /*     /            */
root.right.right = new Node(5); /*   6             */
root.left.right.left = new Node(6);

document.write("Count = " + countSubtrees(root) + "<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Count = 6
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。