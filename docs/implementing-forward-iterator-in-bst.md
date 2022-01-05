# 在 BST 中实现正向迭代器

> 原文:[https://www . geesforgeks . org/implementing-forward-iterator-in-BST/](https://www.geeksforgeeks.org/implementing-forward-iterator-in-bst/)

给定一个二叉查找树，任务是用以下函数在其上实现前向迭代器。

1.  **curr():** 返回当前元素的指针。
2.  **next():** 迭代到二叉查找树中的下一个最小元素。
3.  **isEnd():** 如果没有剩下要遍历的节点，则返回 true，否则返回 false。

迭代器按照排序顺序(递增)遍历 BST。我们将使用[栈](http://www.geeksforgeeks.org/stack-data-structure/)数据结构来实现迭代器。
T3 初始化:

> *   We will create a stack named "q" to store BST nodes.
> *   Create a variable "curr" and initialize it with a pointer to the root.
> *   And "curr" is not empty.
>     *   "curr" is pushed in stack' q'.
>     *   Set curr = curr-> left

**curr()**

> 返回堆栈顶部的值“q”。
> **注意:**如果栈是空的，可能会抛出分段错误。

**时间复杂度:** O(1)

**下一个()**

> *   Declare the pointer variable "curr" to the node.
> *   Set curr = q.top()- > right.
> *   The top element of the stack pops up.
> *   When "curr" is not empty
>     *   Push "curr" in the stack "q".
>     *   Set curr = curr-> to left.

**时间复杂度:** O(1)平均所有通话。在最坏的情况下，单次呼叫可以为 0(h)。

**isEnd（）**

> 如果堆栈“q”为空，则返回 true，否则返回 false。

**时间复杂度:** O(1)
迭代器的这个实现的最坏情况空间复杂度是 O(h)。需要注意的是
迭代器指向栈的最顶层元素。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Iterator for BST
class bstit {
private:
    // Stack to store the nodes
    // of BST
    stack<node*> q;

public:
    // Constructor for the class
    bstit(node* root)
    {
        // Initializing stack
        node* curr = root;
        while (curr != NULL)
            q.push(curr), curr = curr->left;
    }

    // Function to return
    // current element iterator
    // is pointing to
    node* curr()
    {
        return q.top();
    }

    // Function to iterate to next
    // element of BST
    void next()
    {
        node* curr = q.top()->right;
        q.pop();
        while (curr != NULL)
            q.push(curr), curr = curr->left;
    }

    // Function to check if
    // stack is empty
    bool isEnd()
    {
        return !(q.size());
    }
};

// Function to iterator to every element
// using iterator
void iterate(bstit it)
{
    while (!it.isEnd())
        cout << it.curr()->data << " ", it.next();
}

// Driver code
int main()
{
    node* root = new node(5);
    root->left = new node(3);
    root->right = new node(7);
    root->left->left = new node(2);
    root->left->right = new node(4);
    root->right->left = new node(6);
    root->right->right = new node(8);

    // Iterator to BST
    bstit it(root);

    // Function to test iterator
    iterate(it);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

// Node of the binary tree
class TreeNode
{
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x)
    {
        val = x;
    }
}

// Iterator for BST
class BSTIterator{

// Stack to store the nodes
// of BST
Stack<TreeNode> s;

// Constructor for the class
public BSTIterator(TreeNode root)
{

    // Initializing stack
    s = new Stack<>();
    TreeNode curr = root;

    while (curr != null)
    {
        s.push(curr);
        curr = curr.left;
    }
}

// Function to return
// current element iterator
// is pointing to
TreeNode curr()
{
    return s.peek();
}

// Function to iterate to next
// element of BST
public void next()
{
    TreeNode temp = s.peek().right;
    s.pop();

    while (temp != null)
    {
        s.push(temp);
        temp = temp.left;
    }
}

// Function to check if
// stack is empty
public boolean isEnd()
{
    return !s.isEmpty();
}

// Function to iterator to every element
// using iterator
void iterate()
{
    while (isEnd())
    {
        System.out.print(curr().val + " ");
        next();
    }
}
}

class BinaryTree{

TreeNode root;

// Driver code
public static void main(String args[])
{

    // Let us construct a tree shown in
    // the above figure
    BinaryTree tree = new BinaryTree();
    tree.root = new TreeNode(5);
    tree.root.left = new TreeNode(3);
    tree.root.right = new TreeNode(7);
    tree.root.left.left = new TreeNode(2);
    tree.root.left.right = new TreeNode(4);
    tree.root.right.left = new TreeNode(6);
    tree.root.right.right = new TreeNode(8);

    // Iterator to BST
    BSTIterator it = new BSTIterator(tree.root);

    // Function to test iterator
    it.iterate();
}
}

// This code is contributed by nobody_cares
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
# Node of the binary tree
class node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None

# Iterator for BST
class bstit:
    # Stack to store the nodes
    # of BST
    __stack = []
    # Constructor for the class

    def __init__(self, root):

        # Initializing stack
        curr = root
        while (curr is not None):
            self.__stack.append(curr)
            curr = curr.left

    # Function to return
    # current element iterator
    # is pointing to
    def curr(self):
        return self.__stack[-1]

    # Function to iterate to next
    # element of BST
    def next(self):

        curr = self.__stack[-1].right
        self.__stack.pop()
        while (curr is not None):
            self.__stack.append(curr)
            curr = curr.left

    # Function to check if
    # stack is empty
    def isEnd(self):
        return not len(self.__stack)

# Function to iterator to every element
# using iterator
def iterate(it):

    while (not it.isEnd()):
        print(it.curr().data,end=" ")
        it.next()

# Driver code
if __name__ == '__main__':

    root = node(5)
    root.left = node(3)
    root.right = node(7)
    root.left.left = node(2)
    root.left.right = node(4)
    root.right.left = node(6)
    root.right.right = node(8)

    # Iterator to BST
    it = bstit(root)

    # Function to test iterator
    iterate(it)
    print()
# This code is added by Amartya Ghosh
```

**Output:** 

```
2 3 4 5 6 7 8
```