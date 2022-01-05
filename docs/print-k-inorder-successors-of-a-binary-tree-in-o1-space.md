# 在 O(1)空间打印二叉树的 K 个有序后继

> 原文:[https://www . geeksforgeeks . org/print-k-inorder-后继者-一棵 o1-space 中的二叉树/](https://www.geeksforgeeks.org/print-k-inorder-successors-of-a-binary-tree-in-o1-space/)

给定一个**二叉树**和两个数字 **P** 和 **K** ，任务是在常数空间中从二叉树打印给定数字 **P** 的**K**T8】以便后继者。
**示例:**

> **输入:**树:
> 
> ```
>           1
>         /   \
>       12      11
>      /       /   \
>     3       4     13
>             \      /
>             15    9
> ```
> 
> P = 12，K = 4
> **输出:** 1 4 15 11
> **解释:**
> 有序遍历:3 12 1 4 15 11 9 13
> 节点 12 的 4 个有序后继节点是{1，4，15，11}
> **输入:**树:
> 
> ```
>                   5
>                 /   \
>               21    77
>              /  \      \
>             61   16    36
>                   \     /
>                    10  3
>                   /
>                  23
> ```
> 
> P = 23，K = 3
> **输出:** 10 5 77
> **解释:**
> 有序遍历:61 21 16 23 10 5 77 3 36
> 节点 23 的 3 个有序后继节点是{10，5，77}。

**方法:**
为了解决这个问题，我们使用 [Morris Inorder 遍历二叉树](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)来避免使用任何额外的空间。在生成有序序列时搜索节点“P”。找到后，按顺序打印下一个出现的 **K** 节点。
以下是上述方法的实施:

## C++

```
// C++ implementation to print K Inorder
// Successor of the Binary Tree
// without using extra space

#include <bits/stdc++.h>
using namespace std;

/* A binary tree Node has data,
  a pointer to left child 
  and a pointer to right child */
struct tNode {
    int data;
    struct tNode* left;
    struct tNode* right;
};

/* Function to traverse the 
  binary tree without recursion and 
  without stack */
void MorrisTraversal(struct tNode* root,
                     int p, int k)
{
    struct tNode *current, *pre;

    if (root == NULL)
        return;

    bool flag = false;

    current = root;

    while (current != NULL) {

        // Check if the left child exists
        if (current->left == NULL) {

            if (flag == true) {
                cout << current->data
                     << " ";
                k--;
            }
            if (current->data == p)
                flag = true;

            // Check if K is 0
            if (k == 0)
                flag = false;

            // Move current to its right
            current = current->right;
        }
        else {

            // Find the inorder predecessor
            // of current
            pre = current->left;
            while (pre->right != NULL
                   && pre->right != current)
                pre = pre->right;

            /* Make current as the right
               child of its inorder 
                  predecessor */
            if (pre->right == NULL) {
                pre->right = current;
                current = current->left;
            }

            /* Revert the changes made in the
               'if' part to restore the original 
               tree i.e., fix the right child 
                 of predecessor */
            else {
                pre->right = NULL;
                if (flag == true) {
                    cout << current->data
                         << " ";
                    k--;
                }
                if (current->data == p)
                    flag = true;

                if (k == 0)
                    flag = false;

                current = current->right;
            }
        }
    }
}

/* Function that allocates
   a new Node with the 
   given data and NULL left
   and right pointers. */
struct tNode* newtNode(int data)
{
    struct tNode* node = new tNode;
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return (node);
}

/* Driver code*/
int main()
{

    struct tNode* root = newtNode(1);

    root->left = newtNode(12);
    root->right = newtNode(11);
    root->left->left = newtNode(3);
    root->right->left = newtNode(4);
    root->right->right = newtNode(13);

    root->right->left->right = newtNode(15);
    root->right->right->left = newtNode(9);

    int p = 12;
    int k = 4;

    MorrisTraversal(root, p, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print K Inorder 
// Successor of the Binary Tree 
// without using extra space 

// A binary tree tNode has data, 
// a pointer to left child 
// and a pointer to right child 
class tNode 
{ 
    int data; 
    tNode left, right; 

    tNode(int item) 
    { 
        data = item; 
        left = right = null; 
    } 
} 

class BinaryTree{

tNode root; 

// Function to traverse a binary tree
// without recursion and without stack 
void MorrisTraversal(tNode root, int p, int k) 
{ 
    tNode current, pre; 

    if (root == null) 
        return; 

    boolean flag = false;
    current = root; 

    while (current != null) 
    { 
        if (current.left == null)
        { 
            if (flag == true) 
            {
                System.out.print(current.data + " "); 
                k--;
            }
            if (current.data == p)
            {
                flag = true;
            }
            if (k == 0) 
            {
                flag = false;
            }
            current = current.right; 
        } 
        else 
        {

            // Find the inorder predecessor
            // of current 
            pre = current.left; 
            while (pre.right != null && 
                   pre.right != current) 
                pre = pre.right; 

            // Make current as right child of
            // its inorder predecessor 
            if (pre.right == null) 
            { 
                pre.right = current; 
                current = current.left; 
            } 

            // Revert the changes made in the
            // 'if' part to restore the original
            // tree i.e., fix the right child of
            // predecessor
            else 
            { 
                pre.right = null; 
                if (flag == true)
                {
                    System.out.print(current.data + " "); 
                    k--;
                }
                if (current.data == p)
                {
                    flag = true;
                }
                if (k == 0) 
                {
                    flag = false;
                }
                current = current.right; 
            } 
        } 
    } 
} 

// Driver code
public static void main(String args[]) 
{ 
    BinaryTree tree = new BinaryTree(); 

    tree.root = new tNode(1); 
    tree.root.left = new tNode(12); 
    tree.root.right = new tNode(11); 
    tree.root.left.left = new tNode(3); 
    tree.root.right.left = new tNode(4); 
    tree.root.right.right = new tNode(13); 

    tree.root.right.left.right = new tNode(15); 
    tree.root.right.right.left = new tNode(9); 

    int p = 12;
    int k = 4;

    tree.MorrisTraversal(tree.root, p, k); 
} 
} 

// This code is contributed by MOHAMMAD MUDASSIR 
```

## 蟒蛇 3

```
# Python3 implementation to print K Inorder
# Successor of the Binary Tree
# without using extra space

''' A binary tree Node has data,
  a pointer to left child 
  and a pointer to right child '''
class tNode:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

''' Function to traverse the 
  binary tree without recursion and 
  without stack '''
def MorrisTraversal(root, p, k):

    current = None
    pre = None

    if (root == None):
        return;

    flag = False;

    current = root;

    while (current != None):

        # Check if the left child exists
        if (current.left == None):

            if (flag == True):
                print(current.data, end = ' ')

                k -= 1

            if (current.data == p):
                flag = True;

            # Check if K is 0
            if (k == 0):
                flag = False;

            # Move current to its right
            current = current.right;

        else:

            # Find the inorder predecessor
            # of current
            pre = current.left

            while (pre.right != None and pre.right != current):
                pre = pre.right;

            # Make current as the right
            #child of its inorder predecessor
            if(pre.right == None):
                pre.right = current;
                current = current.left;

            # Revert the changes made in the
            # 'if' part to restore the original 
            # tree i.e., fix the right child 
            # of predecessor 
            else:
                pre.right = None;
                if (flag == True):
                    print(current.data, end = ' ')

                    k -= 1

                if (current.data == p):
                    flag = True;

                if (k == 0):
                    flag = False;

                current = current.right;

''' Function that allocates
   a new Node with the 
   given data and None left
   and right pointers. '''
def newtNode(data):

    node = tNode(data);
    return (node);

# Driver code
if __name__=='__main__':

    root = newtNode(1);

    root.left = newtNode(12);
    root.right = newtNode(11);
    root.left.left = newtNode(3);
    root.right.left = newtNode(4);
    root.right.right = newtNode(13);

    root.right.left.right = newtNode(15);
    root.right.right.left = newtNode(9);

    p = 12;
    k = 4;

    MorrisTraversal(root, p, k);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print inorder traversal 
// without recursion and stack 
using System; 

// A binary tree tNode has data, 
// pointer to left child and a 
// pointer to right child 
class BinaryTree{

tNode root; 

public class tNode 
{ 
    public int data; 
    public tNode left, right; 

    public tNode(int item) 
    { 
        data = item; 
        left = right = null; 
    } 
} 

// Function to traverse binary tree without 
// recursion and without stack 
void MorrisTraversal(tNode root, int p, int k) 
{ 
    tNode current, pre; 

    if (root == null) 
        return; 

    current = root; 
    bool flag = false;
    while (current != null) 
    { 
        if (current.left == null) 
        { 
            if (flag == true) 
            {
                Console.Write(current.data + " "); 
                k--;
            }
            if (current.data == p)
            {
                flag = true;
            }
            if (k == 0)
            {
                flag = false;
            }
            current = current.right; 
        } 
        else
        { 

            // Find the inorder predecessor
            // of current 
            pre = current.left; 
            while (pre.right != null && 
                   pre.right != current) 
                pre = pre.right; 

            // Make current as right child 
            // of its inorder predecessor 
            if (pre.right == null) 
            { 
                pre.right = current; 
                current = current.left; 
            } 

            // Revert the changes made in 
            // if part to restore the original 
            // tree i.e., fix the right child 
            // of predecessor
            else
            { 
                pre.right = null; 
                if (flag == true) 
                {
                    Console.Write(current.data + " "); 
                    k--;
                }
                if (current.data == p)
                {
                    flag = true;
                }
                if (k == 0) 
                {
                    flag = false;
                }
                current = current.right; 
            }
        } 
    }
} 

// Driver code 
public static void Main(String []args) 
{ 
    BinaryTree tree = new BinaryTree(); 

    tree.root = new tNode(1); 
    tree.root.left = new tNode(12); 
    tree.root.right = new tNode(11); 
    tree.root.left.left = new tNode(3); 
    tree.root.right.left = new tNode(4); 
    tree.root.right.right = new tNode(13); 

    tree.root.right.left.right = new tNode(15); 
    tree.root.right.right.left = new tNode(9); 

    int p = 12;
    int k = 4;

    tree.MorrisTraversal(tree.root, p, k); 
} 
} 

// This code is contributed by MOHAMMAD MUDASSIR
```

## java 描述语言

```
<script>
    // Javascript implementation to print K Inorder
    // Successor of the Binary Tree
    // without using extra space

    // A binary tree tNode has data,
    // a pointer to left child
    // and a pointer to right child
    class tNode
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.data = item;
        }
    }

    let root;

    // Function to traverse a binary tree
    // without recursion and without stack
    function MorrisTraversal(root, p, k)
    {
        let current, pre;

        if (root == null)
            return;

        let flag = false;
        current = root;

        while (current != null)
        {
            if (current.left == null)
            {
                if (flag == true)
                {
                    document.write(current.data + " ");
                    k--;
                }
                if (current.data == p)
                {
                    flag = true;
                }
                if (k == 0)
                {
                    flag = false;
                }
                current = current.right;
            }
            else
            {

                // Find the inorder predecessor
                // of current
                pre = current.left;
                while (pre.right != null &&
                       pre.right != current)
                    pre = pre.right;

                // Make current as right child of
                // its inorder predecessor
                if (pre.right == null)
                {
                    pre.right = current;
                    current = current.left;
                }

                // Revert the changes made in the
                // 'if' part to restore the original
                // tree i.e., fix the right child of
                // predecessor
                else
                {
                    pre.right = null;
                    if (flag == true)
                    {
                        document.write(current.data + " ");
                        k--;
                    }
                    if (current.data == p)
                    {
                        flag = true;
                    }
                    if (k == 0)
                    {
                        flag = false;
                    }
                    current = current.right;
                }
            }
        }
    }

    root = new tNode(1);
    root.left = new tNode(12);
    root.right = new tNode(11);
    root.left.left = new tNode(3);
    root.right.left = new tNode(4);
    root.right.right = new tNode(13);

    root.right.left.right = new tNode(15);
    root.right.right.left = new tNode(9);

    let p = 12;
    let k = 4;

    MorrisTraversal(root, p, k);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
1 4 15 11
```