# 在 BST 中实现反向迭代器

> 原文:[https://www . geeksforgeeks . org/implementing-backward-iterator-in-BST/](https://www.geeksforgeeks.org/implementing-backward-iterator-in-bst/)

给定一个二叉查找树，任务是用以下函数在其上实现向后迭代器。

1.  **curr():** 返回当前元素的指针。
2.  **prev():** 迭代到二叉查找树上一个最大的元素。
3.  **isEnd():** 如果没有剩下要遍历的节点，则返回 true，否则返回 false。

迭代器以递减的顺序遍历 BST。我们将使用[栈](http://www.geeksforgeeks.org/stack-data-structure/)数据结构来实现迭代器。

**初始化:**

> *   We will create a stack named "q" to store BST nodes.
> *   Create a variable "curr" and initialize it with a pointer to the root.
> *   And "curr" is not empty.
>     *   "curr" is pushed in stack' q'.
>     *   Set curr = curr-> right

**curr()**

> 返回堆栈顶部的值“q”。
> **注意:**如果栈是空的，可能会抛出分段错误。

**时间复杂度:** O(1)

**预测()**

> *   Declare the pointer variable "curr" to the node.
> *   左置 curr = q.top()-> .
> *   The top element of the stack pops up.
> *   When "curr" is not empty
>     *   Push "curr" in the stack "q".
>     *   Set curr = curr-> to the right.

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
            q.push(curr), curr = curr->right;
    }

    // Function to return
    // current element iterator
    // is pointing to
    node* curr()
    {
        return q.top();
    }

    // Function to iterate to previous
    // element of BST
    void prev()
    {
        node* curr = q.top()->left;
        q.pop();
        while (curr != NULL)
            q.push(curr), curr = curr->right;
    }

    // Function to check if
    // stack is empty
    bool isEnd()
    {
        return !(q.size());
    }
};

// Function to test the iterator
void iterate(bstit it)
{
    while (!it.isEnd())
        cout << it.curr()->data << " ", it.prev();
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

    // Function call to test the iterator
    iterate(it);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of the binary tree
class node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Stack to store the nodes
// of BST
let q = [];

// Constructor for the class
function bstit(root)
{

    // Initializing stack
    let curr = root;

    while (curr != null)
    {
        q.push(curr);
        curr = curr.right;
    }
}

// Function to return
// current element iterator
// is pointing to
function curr()
{
    return q[q.length - 1];
}

// Function to iterate to previous
// element of BST
function prev()
{
    let curr = q[q.length - 1].left;
    q.pop();

    while (curr != null)
    {
        q.push(curr);
        curr = curr.right;
    }
}

// Function to check if
// stack is empty
function isEnd()
{
    return (q.length == 0);
}

// Function to test the iterator
function iterate()
{
    while (!isEnd())
    {
        document.write(curr().data + " ");
        prev();
    }
}

// Driver code
let root = new node(5);
root.left = new node(3);
root.right = new node(7);
root.left.left = new node(2);
root.left.right = new node(4);
root.right.left = new node(6);
root.right.right = new node(8);

// Iterator to BST
bstit(root);

// Function call to test the iterator
iterate();

// This code is contributed by divyeshrabadiya07

</script>
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
    # __stack to store the nodes
    # of BST
    __stack = []
    # Constructor for the class

    def __init__(self, root):

        # Initializing __stack
        curr = root
        while (curr is not None):
            self.__stack.append(curr)
            curr = curr.right

    # Function to return
    # current element iterator
    # is pointing to
    def curr(self):
        return self.__stack[-1]

    # Function to iterate to previous
    # element of BST
    def prev(self):

        curr = self.__stack[-1].left
        self.__stack.pop()
        while (curr != None):
            self.__stack.append(curr)
            curr = curr.right

    # Function to check if
    # __stack is empty
    def isEnd(self):
        return not len((self.__stack))

# Function to test the iterator
def iterate(it):
    while (not it.isEnd()):
        print(it.curr().data,end=" ")
        it.prev()

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
    it=bstit(root)

    # Function call to test the iterator
    iterate(it)
    print()
# This code is contributed by Amartya Ghosh
```

**Output:** 

```
8 7 6 5 4 3 2
```