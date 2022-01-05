# 查找根中是否有一对叶路径，其总和等于根的数据

> 原文:[https://www . geesforgeks . org/find-pair-root-leaf-path-sum-equals-root-data/](https://www.geeksforgeeks.org/find-pair-root-leaf-path-sum-equals-roots-data/)

给定一棵二叉树，找出根路径和叶路径是否有一对，使得成对的值之和等于根的数据。例如，在下面的树中，在任何根到叶路径中都没有总和等于根数据的对。

![](img/5edb5c862d1ecd4e24c00ad87e7eb4e6.png)

这个想法是基于散列和树遍历。思路类似于数组对和问题的方法 2 [。](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/) 

*   创建一个空哈希表。
*   开始以预定的方式遍历树。
*   如果我们到达一个叶节点，我们返回 false。
*   对于每个被访问的节点，检查哈希表中是否存在根节点的数据减去当前节点的数据。如果是，返回真。否则在哈希表中插入当前节点。
*   递归签入左右子树。
*   从哈希表中删除当前节点，这样它就不会出现在其他根到叶路径中。

以下是上述想法的实现。

## C++

```
// C++ program to find if there is a pair in any root
// to leaf path with sum equals to root's key.
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node
{
    int data;
    struct Node* left, *right;
};

/* utility that allocates a new node with the
given data and NULL left and right pointers. */
struct Node* newnode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right  = NULL;
    return (node);
}

// Function to print root to leaf path which satisfies the condition
bool printPathUtil(Node *node, unordered_set<int> &s, int root_data)
{
    // Base condition
    if (node == NULL)
        return false;

    // Check if current node makes a pair with any of the
    // existing elements in set.
    int rem = root_data - node->data;
    if (s.find(rem) != s.end())
        return true;

    // Insert current node in set
    s.insert(node->data);

    // If result returned by either left or right child is
    // true, return true.
    bool res = printPathUtil(node->left, s, root_data) ||
               printPathUtil(node->right, s, root_data);

    // Remove current node from hash table
    s.erase(node->data);

    return res;
}

// A wrapper over printPathUtil()
bool isPathSum(Node *root)
{
   // create an empty hash table
   unordered_set<int> s;

   // Recursively check in left and right subtrees.
   return printPathUtil(root->left, s, root->data) ||
          printPathUtil(root->right, s, root->data);
}

// Driver program to run the case
int main()
{
    struct Node *root = newnode(8);
    root->left    = newnode(5);
    root->right   = newnode(4);
    root->left->left = newnode(9);
    root->left->right = newnode(7);
    root->left->right->left = newnode(1);
    root->left->right->right = newnode(12);
    root->left->right->right->right = newnode(2);
    root->right->right = newnode(11);
    root->right->right->left = newnode(3);
    isPathSum(root)? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if there is a pair in any root
// to leaf path with sum equals to root's key.
import java.util.*;

class GFG
{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int data;
    Node left, right;
};

/* utility that allocates a new node with the
given data and null left and right pointers. */
static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print root to leaf path which satisfies the condition
static boolean printPathUtil(Node node, HashSet<Integer> s, int root_data)
{
    // Base condition
    if (node == null)
        return false;

    // Check if current node makes a pair with any of the
    // existing elements in set.
    int rem = root_data - node.data;
    if (s.contains(rem))
        return true;

    // Insert current node in set
    s.add(node.data);

    // If result returned by either left or right child is
    // true, return true.
    boolean res = printPathUtil(node.left, s, root_data) ||
            printPathUtil(node.right, s, root_data);

    // Remove current node from hash table
    s.remove(node.data);

    return res;
}

// A wrapper over printPathUtil()
static boolean isPathSum(Node root)
{

// create an empty hash table
HashSet<Integer> s = new HashSet<Integer>();

// Recursively check in left and right subtrees.
return printPathUtil(root.left, s, root.data) ||
        printPathUtil(root.right, s, root.data);
}

// Driver code
public static void main(String[] args)
{
    Node root = newnode(8);
    root.left = newnode(5);
    root.right = newnode(4);
    root.left.left = newnode(9);
    root.left.right = newnode(7);
    root.left.right.left = newnode(1);
    root.left.right.right = newnode(12);
    root.left.right.right.right = newnode(2);
    root.right.right = newnode(11);
    root.right.right.left = newnode(3);
    System.out.print(isPathSum(root)==true ?"Yes" : "No");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find if there is a
# pair in any root to leaf path with sum
# equals to root's key

# A binary tree node has data, pointer to
# left child and a pointer to right child

""" utility that allocates a new node with the
given data and None left and right pointers. """
class newnode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to prroot to leaf path which
# satisfies the condition
def printPathUtil(node, s, root_data) :

    # Base condition
    if (node == None) :
        return False

    # Check if current node makes a pair
    # with any of the existing elements in set.
    rem = root_data - node.data
    if rem in s:
        return True

    # Insert current node in set
    s.add(node.data)

    # If result returned by either left or
    # right child is True, return True.
    res = printPathUtil(node.left, s, root_data) or \
           printPathUtil(node.right, s, root_data)

    # Remove current node from hash table
    s.remove(node.data)

    return res

# A wrapper over printPathUtil()
def isPathSum(root) :

    # create an empty hash table
    s = set()

    # Recursively check in left and right subtrees.
    return printPathUtil(root.left, s, root.data) or \
           printPathUtil(root.right, s, root.data)

# Driver Code
if __name__ == '__main__':
    root = newnode(8)
    root.left = newnode(5)
    root.right = newnode(4)
    root.left.left = newnode(9)
    root.left.right = newnode(7)
    root.left.right.left = newnode(1)
    root.left.right.right = newnode(12)
    root.left.right.right.right = newnode(2)
    root.right.right = newnode(11)
    root.right.right.left = newnode(3)
    print("Yes") if (isPathSum(root)) else print("No")

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
// C# program to find if there is a pair in any root
// to leaf path with sum equals to root's key.
using System;
using System.Collections.Generic;

class GFG
{

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
public class Node
{
    public int data;
    public Node left, right;
};

/* utility that allocates a new node with the
given data and null left and right pointers. */
static Node newnode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return (node);
}

// Function to print root to leaf path
// which satisfies the condition
static bool printPathUtil(Node node,
                          HashSet<int> s,
                          int root_data)
{
    // Base condition
    if (node == null)
        return false;

    // Check if current node makes a pair
    // with any of the existing elements in set.
    int rem = root_data - node.data;
    if (s.Contains(rem))
        return true;

    // Insert current node in set
    s.Add(node.data);

    // If result returned by either left or
    // right child is true, return true.
    bool res = printPathUtil(node.left, s, root_data) ||
               printPathUtil(node.right, s, root_data);

    // Remove current node from hash table
    s.Remove(node.data);

    return res;
}

// A wrapper over printPathUtil()
static bool isPathSum(Node root)
{

    // create an empty hash table
    HashSet<int> s = new HashSet<int>();

    // Recursively check in left and right subtrees.
    return printPathUtil(root.left, s, root.data) ||
           printPathUtil(root.right, s, root.data);
}

// Driver code
public static void Main(String[] args)
{
    Node root = newnode(8);
    root.left = newnode(5);
    root.right = newnode(4);
    root.left.left = newnode(9);
    root.left.right = newnode(7);
    root.left.right.left = newnode(1);
    root.left.right.right = newnode(12);
    root.left.right.right.right = newnode(2);
    root.right.right = newnode(11);
    root.right.right.left = newnode(3);
    Console.Write(isPathSum(root) == true ?
                                    "Yes" : "No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find if there is a pair in any root
// to leaf path with sum equals to root's key.

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    /* utility that allocates a new node with the
given data and null left and right pointers. */
    constructor(data)
    {
        this.data=data;
        this.left=this.right=null;
    }
}

// Function to print root to leaf path which satisfies the condition
function printPathUtil(node,s,root_data)
{
    // Base condition
    if (node == null)
        return false;

    // Check if current node makes a pair with any of the
    // existing elements in set.
    let rem = root_data - node.data;
    if (s.has(rem))
        return true;

    // Insert current node in set
    s.add(node.data);

    // If result returned by either left or right child is
    // true, return true.
    let res = printPathUtil(node.left, s, root_data) ||
            printPathUtil(node.right, s, root_data);

    // Remove current node from hash table
    s.delete(node.data);

    return res;
}

// A wrapper over printPathUtil()
function isPathSum(root)
{
    // create an empty hash table
let s = new Set();

// Recursively check in left and right subtrees.
return printPathUtil(root.left, s, root.data) ||
        printPathUtil(root.right, s, root.data);
}

// Driver code
let root = new Node(8);
root.left = new Node(5);
root.right = new Node(4);
root.left.left = new Node(9);
root.left.right = new Node(7);
root.left.right.left = new Node(1);
root.left.right.right = new Node(12);
root.left.right.right.right = new Node(2);
root.right.right = new Node(11);
root.right.right.left = new Node(3);
document.write(isPathSum(root)==true ?"Yes" : "No");

// This code is contributed by rag2127
</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)假设哈希搜索、插入和擦除需要 O(1)个时间。
**练习:**扩展上述解决方案，打印所有根到叶路径，这些路径有一对总和等于根的数据。
本文由 [**沙莎克·米什拉(古鲁)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。