# BST 中大于或等于 N 的最小数(迭代方法)

> 原文:[https://www . geesforgeks . org/BST 中的最小数大于或等于 n 的迭代方法/](https://www.geeksforgeeks.org/smallest-number-in-bst-which-is-greater-than-or-equal-to-n-iterative-approach/)

给定一个二叉查找树和一个数字 N，任务是找到二叉查找树中大于或等于 N 的最小数字

**示例:**

```
Input: N = 5   
              8
            /   \
           7     10
         /      /   \
        2      9     13

Output: 7
As 7 is the smallest number in BST which is greater than N = 5.

Input: N = 10 
           8
         /   \
        5    11
      /  \
     2    7
      \
       3

Output: 11
As 11 is the smallest number in BST which is greater than N = 10.
```

这个问题的递归解决方案已经在[帖子](https://www.geeksforgeeks.org/smallest-number-in-bst-which-is-greater-than-or-equal-to-n/)中讨论过了。下面是这个问题的迭代方法:

使用 [Morris 遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/)可以在常数空间中求解上述问题。找到目标的下一任。保留两个指针，一个指向当前节点，一个用于存储答案。

下面是上述方法的实现:

## C++

```
// C++ code to find the smallest value greater
// than or equal to N
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int key;
    Node *left, *right;
};

// To create new BST Node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// To insert a new node in BST
Node* insert(Node* node, int key)
{
    // if tree is empty return new node
    if (node == NULL)
        return newNode(key);

    // if key is less then or greater then
    // node value then recur down the tree
    if (key < node->key)
        node->left = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);

    // return the (unchanged) node pointer
    return node;
}

// Returns smallest value greater than or
// equal to key.
int findFloor(Node* root, int key)
{
    Node *curr = root, *ans = NULL;

    // traverse in the tree
    while (curr) {

        // if the node is smaller than N,
        // move right.
        if (curr->key > key) {
            ans = curr;
            curr = curr->left;
        }      

        // if it is equal to N, then it will be
        // the answer
        else if (curr->key == key) {
            ans = curr;
            break;
        }

        else // move to the right of the tree
            curr = curr->right;
    }

    if (ans != NULL)
       return ans->key;

    return -1;
}

// Driver code
int main()
{
    int N = 13;

    Node* root = insert(root, 19);
    insert(root, 2);
    insert(root, 1);
    insert(root, 3);
    insert(root, 12);
    insert(root, 9);
    insert(root, 21);
    insert(root, 25);

    printf("%d", findFloor(root, 15));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the smallest value greater
// than or equal to N
class GFG
{
    static class Node
    {
        int key;
        Node left, right;
    };

    // To create new BST Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.key = item;
        temp.left = temp.right = null;
        return temp;
    }

    // To insert a new node in BST
    static Node insert(Node node, int key)
    {
        // if tree is empty return new node
        if (node == null)
        {
            return newNode(key);
        }

        // if key is less then or greater then
        // node value then recur down the tree
        if (key < node.key)
        {
            node.left = insert(node.left, key);
        }
        else if (key > node.key)
        {
            node.right = insert(node.right, key);
        }

        // return the (unchanged) node pointer
        return node;
    }

    // Returns smallest value greater than or
    // equal to key.
    static int findFloor(Node root, int key)
    {
        Node curr = root, ans = null;

        // traverse in the tree
        while (curr != null)
        {

            // if the node is smaller than N,
            // move right.
            if (curr.key > key)
            {
                ans = curr;
                curr = curr.left;
            }

            // if it is equal to N, then it will be
            // the answer
            else if (curr.key == key)
            {
                ans = curr;
                break;
            }
            else // move to the right of the tree
            {
                curr = curr.right;
            }
        }

        if (ans != null)
        {
            return ans.key;
        }  
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 13;

        Node root = new Node();
        insert(root, 19);
        insert(root, 2);
        insert(root, 1);
        insert(root, 3);
        insert(root, 12);
        insert(root, 9);
        insert(root, 21);
        insert(root, 25);

        System.out.printf("%d", findFloor(root, 15));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to find the smallest
# value greater than or equal to N
class Node:

    def __init__(self, key):

        self.key = key
        self.left = None
        self.right = None

# To insert a new node in BST
def insert(node: Node, key: int) -> Node:

    # If tree is empty return new node
    if (node is None):
        return Node(key)

    # If key is less then or greater then
    # node value then recur down the tree
    if (key < node.key):
        node.left = insert(node.left, key)
    elif (key > node.key):
        node.right = insert(node.right, key)

    # Return the (unchanged) node pointer
    return node

# Returns smallest value greater than or
# equal to key.
def findFloor(root: Node, key: int) -> int:

    curr = root
    ans = None

    # Traverse in the tree
    while (curr):

        # If the node is smaller than N,
        # move right.
        if (curr.key > key):
            ans = curr
            curr = curr.left

        # If it is equal to N, then
        # it will be the answer
        elif (curr.key == key):
            ans = curr
            break

        else:  # Move to the right of the tree
            curr = curr.right

    if (ans != None):
        return ans.key

    return -1

# Driver code
if __name__ == "__main__":

    N = 13

    root = None
    root = insert(root, 19)
    insert(root, 2)
    insert(root, 1)
    insert(root, 3)
    insert(root, 12)
    insert(root, 9)
    insert(root, 21)
    insert(root, 25)

    print(findFloor(root, 15))

# This code is contributed by sanjeev2552
```

## C#

```
// C# code to find the smallest value greater
// than or equal to N
using System;
using System.Collections.Generic;

class GFG
{
    class Node
    {
        public int key;
        public Node left, right;
    };

    // To create new BST Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.key = item;
        temp.left = temp.right = null;
        return temp;
    }

    // To insert a new node in BST
    static Node insert(Node node, int key)
    {
        // if tree is empty return new node
        if (node == null)
        {
            return newNode(key);
        }

        // if key is less then or greater then
        // node value then recur down the tree
        if (key < node.key)
        {
            node.left = insert(node.left, key);
        }
        else if (key > node.key)
        {
            node.right = insert(node.right, key);
        }

        // return the (unchanged) node pointer
        return node;
    }

    // Returns smallest value greater than or
    // equal to key.
    static int findFloor(Node root, int key)
    {
        Node curr = root, ans = null;

        // traverse in the tree
        while (curr != null)
        {

            // if the node is smaller than N,
            // move right.
            if (curr.key > key)
            {
                ans = curr;
                curr = curr.left;
            }

            // if it is equal to N, then it will be
            // the answer
            else if (curr.key == key)
            {
                ans = curr;
                break;
            }
            else // move to the right of the tree
            {
                curr = curr.right;
            }
        }

        if (ans != null)
        {
            return ans.key;
        }
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {

        Node root = new Node();
        insert(root, 19);
        insert(root, 2);
        insert(root, 1);
        insert(root, 3);
        insert(root, 12);
        insert(root, 9);
        insert(root, 21);
        insert(root, 25);

        Console.Write("{0}", findFloor(root, 15));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript code to find the smallest
// value greater than or equal to N
class Node
{
    constructor()
    {
        this.key = 0;
        this.left = null;
        this.right = null;
    }
};

// To create new BST Node
function newNode(item)
{
    var temp = new Node();
    temp.key = item;
    temp.left = temp.right = null;
    return temp;
}

// To insert a new node in BST
function insert(node, key)
{

    // If tree is empty return new node
    if (node == null)
    {
        return newNode(key);
    }

    // If key is less then or greater then
    // node value then recur down the tree
    if (key < node.key)
    {
        node.left = insert(node.left, key);
    }
    else if (key > node.key)
    {
        node.right = insert(node.right, key);
    }

    // Return the (unchanged) node pointer
    return node;
}

// Returns smallest value greater than or
// equal to key.
function findFloor(root, key)
{
    var curr = root, ans = null;

    // Traverse in the tree
    while (curr != null)
    {

        // If the node is smaller than N,
        // move right.
        if (curr.key > key)
        {
            ans = curr;
            curr = curr.left;
        }

        // If it is equal to N, then it will be
        // the answer
        else if (curr.key == key)
        {
            ans = curr;
            break;
        }

        // Move to the right of the tree
        else
        {
            curr = curr.right;
        }
    }
    if (ans != null)
    {
        return ans.key;
    }
    return -1;
}

// Driver code
var root = new Node();
insert(root, 19);
insert(root, 2);
insert(root, 1);
insert(root, 3);
insert(root, 12);
insert(root, 9);
insert(root, 21);
insert(root, 25);

document.write(findFloor(root, 15));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
19
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)