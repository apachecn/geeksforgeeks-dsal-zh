# 二叉树中带平衡括号的级数

> 原文:[https://www . geeksforgeeks . org/二进制树中有平衡括号的层数/](https://www.geeksforgeeks.org/number-of-levels-having-balanced-parentheses-in-a-binary-tree/)

给定仅由**(“**”和**)“**组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，如果具有括号的级别的节点从左到右平衡，则认为该级别是平衡的。任务是计算二叉树中平衡级别的总数。

**示例:**

> **输入:**(
> /\
> )(
> /\ \
> )(
> /\ \
> ((())
> 
> **输出:** 2
> **说明:**
> 2、4 级括号平衡。
> 
> **输入:**)
> /\
> ()
> /\
> ()
> /
> (
> 
> **输出:** 2
> **说明:**
> 2、3 级括号平衡。

**方法:**按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)，在给定的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)上执行[杠杆顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。
*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)检查每一级[括号是否平衡](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/)。
*   逐一遍历每个级别，并执行以下步骤:
    *   如果当前节点值为**(“**”，[将其推入堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
    *   如果当前节点值为 **')'** ，则检查[栈是否为空](https://www.geeksforgeeks.org/stack-empty-method-in-java/)。如果非空且[堆叠顶部](https://www.geeksforgeeks.org/stack-top-c-stl/)为**(**，则[将其从堆叠](https://www.geeksforgeeks.org/stack-pop-method-in-java/)中弹出。
    *   否则，得出括号不平衡的结论。
*   在遍历结束时，如果发现堆栈是空的，那么断定括号是平衡的。否则，得出括号不平衡的结论。

下面是上述方法的实现:

## C++

```
// C++ program for Number of levels having balanced
// parentheses in a Binary Tree
#include <bits/stdc++.h>
using namespace std;

// Class containing left and
// right child of current
// node and key value
struct Node {

    Node* left;
    Node* right;
    int key;

    Node(int item)
    {
        key = item;
        this->left = nullptr;
        this->right = nullptr;
    }
};

// Root of Binary Tree
Node* root = nullptr;

// Function to count levels in the
// Binary Tree having balanced parentheses
int countbal(Node* root)
{

  // Stores nodes of each level
  queue<Node*> que;
  que.push(root);

  // Stores required count of
  // levels with balanced parentheses
  int ans = 0;

  // Iterate until false
  while (true)
  {

    // Stores parentheses
    stack<char> stk;
    bool flag = true;
    int len = que.size();

    // If length is false
    if (len == 0) {
      break;
    }
    while (len > 0)
    {

      // Pop 0 from queue
      // and store it in temp
      Node* temp = que.front();
      que.pop();

      // Check if temp.key
      // is equal to '('
      if (temp->key == '(')
      {

        // push '(' into stack
        stk.push('(');
      }
      else
      {

        // If stk is not empty and the
        // last element in the stack is '(
        if (stk.size() > 0 && stk.top() == '(')
        {

          // Pop from stack
          stk.pop();
        }
        else
        {

          // Mark flag as False
          flag = false;
        }
      }

      // If tmp.left is True
      if (temp->left != nullptr)
      {

        // push temp.left into queue
        que.push(temp->left);
      }

      // If tmp.right is True
      if (temp->right != nullptr)
      {

        // push temp.right into queue
        que.push(temp->right);
      }

      // Decrement length by 1
      len--;
    }

    // If flag is True
    // and stk is False
    if (flag && stk.size() > 0)
    {
      ans += 1;
    }
  }
  return ans;
}

int main()
{
    /*create root*/
    // creating all its child
    root = new Node('(');
    root->left = new Node('(');
    root->right = new Node(')');
    root->left->left = new Node('(');
    root->left->right = new Node(')');
    root->right->right = new Node('(');
    root->left->left->left = new Node('(');
    root->left->left->right = new Node('(');
    root->right->right->left = new Node(')');
    root->right->right->right = new Node(')');

    // function call and ans print
    cout << countbal(root);

    return 0;
}

// This code is contributed by suresh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Number of levels having balanced
// parentheses in a Binary Tree
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

/* Class containing left and right child of current
node and key value*/
class Node {
  char key;
  Node left, right;

  public Node(char item)
  {
    key = item;
    left = right = null;
  }
}

// A Java program to introduce Binary Tree
class BinaryTree
{

  // Root of Binary Tree
  Node root;

  // Constructors
  BinaryTree(char key) { root = new Node(key); }

  BinaryTree() { root = null; }

  // Function to count levels in the
  // Binary Tree having balanced parentheses
  public static int countbal(Node root)
  {

    // Stores nodes of each level
    Queue<Node> que = new LinkedList<>();
    que.add(root);

    // Stores required count of
    // levels with balanced parentheses
    int ans = 0;

    // Iterate until false
    while (true)
    {

      // Stores parentheses
      Stack<Character> stk = new Stack<>();
      boolean flag = true;
      int len = que.size();

      // If length is false
      if (len == 0) {
        break;
      }
      while (len > 0)
      {

        // Pop 0 from queue
        // and store it in temp
        Node temp = que.remove();

        // Check if temp.key
        // is equal to '('
        if (temp.key == '(')
        {

          // push '(' into stack
          stk.push('(');
        }
        else
        {

          // If stk is not empty and the
          // last element in the stack is '(
          if (stk.size() > 0
              && stk.peek() == '(')
          {

            // Pop from stack
            stk.pop();
          }
          else
          {

            // Mark flag as False
            flag = false;
          }
        }

        // If tmp.left is True
        if (temp.left != null)
        {

          // push temp.left into queue
          que.add(temp.left);
        }

        // If tmp.right is True
        if (temp.right != null)
        {

          // push temp.right into queue
          que.add(temp.right);
        }

        // Decrement length by 1
        len--;
      }

      // If flag is True
      // and stk is False
      if (flag && stk.size() > 0)
      {
        ans += 1;
      }
    }
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    BinaryTree tree = new BinaryTree();

    /*create root*/
    // creating all its child
    tree.root = new Node('(');
    tree.root.left = new Node('(');
    tree.root.right = new Node(')');
    tree.root.left.left = new Node('(');
    tree.root.left.right = new Node(')');
    tree.root.right.right = new Node('(');
    tree.root.left.left.left = new Node('(');
    tree.root.left.left.right = new Node('(');
    tree.root.right.right.left = new Node(')');
    tree.root.right.right.right = new Node(')');

    // function call and ans print
    System.out.println(countbal(tree.root));
  }
}

// This code is contributed by adity7409.
```

## 蟒蛇 3

```
# Python Code for above approach

# Structure of a Tree Node
class TreeNode:
    def __init__(self, val='',
                 left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

# Function to count levels in the
# Binary Tree having balanced parentheses
def countBal(root):

    # Stores nodes of each level
    que = [root]

    # Stores required count of
    # levels with balanced parentheses
    ans = 0

    # Iterate until false
    while True:

        # Stores parentheses
        stk = []
        flag = True

        length = len(que)

        # If length is false
        if not length:
            break

        while length:

            # Pop 0 from queue
            # and store it in temp
            temp = que.pop(0)

            # Check if temp.val
            # is equal to '('
            if temp.val == '(':

                # Append '(' into stack
                stk.append('(')
            else:

                # If stk is not empty and the
                # last element in the stack is '('
                if stk and stk[-1] == '(':

                    # Pop from stack
                    stk.pop()
                else:

                    # Mark flag as False
                    flag = False

            # If tmp.left is True
            if temp.left:

                # Append temp.left into queue
                que.append(temp.left)

            # If tmp.right is True
            if temp.right:

                # Append temp.right into queue
                que.append(temp.right)

            # Decrement length by 1
            length -= 1

        # If flag is True
        # and stk is False
        if flag and not stk:
            ans += 1

    # Return ans
    return ans

# Driver Code
root = TreeNode('(')
root.left = TreeNode('(')
root.right = TreeNode(')')
root.left.left = TreeNode('(')
root.left.right = TreeNode(')')
root.right.right = TreeNode('(')
root.left.left.left = TreeNode('(')
root.left.left.right = TreeNode('(')
root.right.right.left = TreeNode(')')
root.right.right.right = TreeNode(')')

print(countBal(root))
```

## C#

```
// C# program for Number of levels having balanced
// parentheses in a Binary Tree
using System;
using System.Collections;
class GFG {

    // Class containing left and
    // right child of current
    // node and key value
    class Node {

        public int key;
        public Node left, right;

        public Node(int item)
        {
            key = item;
            left = right = null;
        }
    }

    // Root of Binary Tree
    static Node root = null;

    // Function to count levels in the
    // Binary Tree having balanced parentheses
    static int countbal(Node root)
    {

      // Stores nodes of each level
      Queue que = new Queue();
      que.Enqueue(root);

      // Stores required count of
      // levels with balanced parentheses
      int ans = 0;

      // Iterate until false
      while (true)
      {

        // Stores parentheses
        Stack stk = new Stack();
        bool flag = true;
        int len = que.Count;

        // If length is false
        if (len == 0) {
          break;
        }
        while (len > 0)
        {

          // Pop 0 from queue
          // and store it in temp
          Node temp = (Node)que.Peek();
          que.Dequeue();

          // Check if temp.key
          // is equal to '('
          if (temp.key == '(')
          {

            // push '(' into stack
            stk.Push('(');
          }
          else
          {

            // If stk is not empty and the
            // last element in the stack is '(
            if (stk.Count > 0
                && (char)stk.Peek() == '(')
            {

              // Pop from stack
              stk.Pop();
            }
            else
            {

              // Mark flag as False
              flag = false;
            }
          }

          // If tmp.left is True
          if (temp.left != null)
          {

            // push temp.left into queue
            que.Enqueue(temp.left);
          }

          // If tmp.right is True
          if (temp.right != null)
          {

            // push temp.right into queue
            que.Enqueue(temp.right);
          }

          // Decrement length by 1
          len--;
        }

        // If flag is True
        // and stk is False
        if (flag && stk.Count > 0)
        {
          ans += 1;
        }
      }
      return ans;
    }

  static void Main()
  {

    /*create root*/
    // creating all its child
    root = new Node('(');
    root.left = new Node('(');
    root.right = new Node(')');
    root.left.left = new Node('(');
    root.left.right = new Node(')');
    root.right.right = new Node('(');
    root.left.left.left = new Node('(');
    root.left.left.right = new Node('(');
    root.right.right.left = new Node(')');
    root.right.right.right = new Node(')');

    // function call and ans print
    Console.Write(countbal(root));
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>

    // JavaScript program for Number of levels having balanced
    // parentheses in a Binary Tree

    class Node
    {
        constructor(item) {
           this.left = null;
           this.right = null;
           this.key = item;
        }
    }

    // Root of Binary Tree
    let root;

    root = null;

    // Function to count levels in the
    // Binary Tree having balanced parentheses
    function countbal(root)
    {

      // Stores nodes of each level
      let que = [];
      que.push(root);

      // Stores required count of
      // levels with balanced parentheses
      let ans = 0;

      // Iterate until false
      while (true)
      {

        // Stores parentheses
        let stk = [];
        let flag = true;
        let len = que.length;

        // If length is false
        if (len == 0) {
          break;
        }
        while (len > 0)
        {

          // Pop 0 from queue
          // and store it in temp
          let temp = que.shift();

          // Check if temp.key
          // is equal to '('
          if (temp.key == '(')
          {

            // push '(' into stack
            stk.push('(');
          }
          else
          {

            // If stk is not empty and the
            // last element in the stack is '(
            if (stk.length > 0
                && stk[stk.length - 1] == '(')
            {

              // Pop from stack
              stk.pop();
            }
            else
            {

              // Mark flag as False
              flag = false;
            }
          }

          // If tmp.left is True
          if (temp.left != null)
          {

            // push temp.left into queue
            que.push(temp.left);
          }

          // If tmp.right is True
          if (temp.right != null)
          {

            // push temp.right into queue
            que.push(temp.right);
          }

          // Decrement length by 1
          len--;
        }

        // If flag is True
        // and stk is False
        if (flag && stk.length > 0)
        {
          ans += 1;
        }
      }
      return ans;
    }

    /*create root*/
    // creating all its child
    root = new Node('(');
    root.left = new Node('(');
    root.right = new Node(')');
    root.left.left = new Node('(');
    root.left.right = new Node(')');
    root.right.right = new Node('(');
    root.left.left.left = new Node('(');
    root.left.left.right = new Node('(');
    root.right.right.left = new Node(')');
    root.right.right.right = new Node(')');

    // function call and ans print
    document.write(countbal(root));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)