# 通过尽可能向右移动所有节点来修改二叉树

> 原文:[https://www . geesforgeks . org/通过将所有节点尽可能向右移动来修改二叉树/](https://www.geeksforgeeks.org/modify-a-binary-tree-by-shifting-all-nodes-to-as-far-right-as-possible/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是打印给定树的所有节点尽可能向右移动后得到的修改树的[有序遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)，同时保持每一级的相对顺序。
**例:**

> **输入:**下面是给定的树:
> 1
> /\
> 2 3
> /\ \
> 4 5 6
> **输出:** 2 4 1 5 3 6
> **说明:**将所有节点移到最右侧后得到的树如下:
> **1
> /\
> 2 3
> /\
> 4 5 6**
> 
> ****输入:**下面是给定的树:
> 1
> /
> 2
> /\
> 3 4
> /\
> 5 6
> T10】输出:1 3 2 5 4 6
> T13】解释:T15**T17】1
> \
> 2
> /\
> 3 4
> /\
> 5 6****

****方法:**解决给定问题的思路是使用[栈从右向左存储一个级别的节点](https://www.geeksforgeeks.org/stack-data-structure/)和使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)存储下一个级别的现有节点，并使用[级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)连接有效位置的节点。按照以下步骤解决问题:**

*   **初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/) **S** 来存储二叉树从右到左的一个[级的节点序列。](https://www.geeksforgeeks.org/get-level-of-a-node-in-a-binary-tree/)**
*   **初始化一个**队列** **Q** 来存储二叉树的一个级别的现有节点。**
*   **如果根的右子存在，[将其推入队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/) **Q** 。腾出合适的孩子。**
*   **如果根的左子存在，[将其推入队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/) **Q** 。腾出左边的孩子。**
*   **[推**根**入栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)T4。**
*   **在[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)上执行[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，并执行以下步骤:

    *   如果栈顶[节点的右子节点为空，则将队列](https://www.geeksforgeeks.org/stack-top-c-stl/)前面的[节点设置为右子节点。](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)
    *   否则，对左边的孩子重复上述步骤。从栈顶弹出节点。
    *   将队列前面节点的左右子节点添加到队列中。
    *   在堆栈中从右到左存储下一级的节点序列。** 
*   **完成以上步骤后，打印修改树的[以便遍历](https://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion/)。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a Tree node
struct TreeNode {
    int val = 0;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int x)
    {
        val = x;
        left = right = NULL;
    }
};

// Function to print Inorder
// Traversal of a Binary Tree
void printTree(TreeNode* root)
{
    if (!root)
        return;

    // Traverse left child
    printTree(root->left);

    // Print current node
    cout << root->val << " ";

    // Traverse right child
    printTree(root->right);
}

// Function to shift all nodes of the
// given Binary Tree to as far as
// right possible
TreeNode* shiftRight(TreeNode* root)
{

    // If tree is empty
    if (!root)
        return NULL;

    stack<TreeNode*> st;
    queue<TreeNode*> q;

    // If right child exists
    if (root->right)
        q.push(root->right);

    root->right = NULL;

    // If left child exists
    if (root->left)
        q.push(root->left);

    root->left = NULL;

    // Push current node into stack
    st.push(root);

    while (!q.empty()) {

        // Count valid existing nodes
        // in current level
        int n = q.size();
        stack<TreeNode*> temp;

        // Iterate existing nodes
        // in the current level
        while (n--) {

            // If no right child exists
            if (!st.top()->right)

                // Set the rightmost
                // vacant node
                st.top()->right = q.front();

            // If no left child exists
            else {

                // Set rightmost vacant node
                st.top()->left = q.front();

                // Remove the node as both
                // child nodes are occupied
                st.pop();
            }

            // If r̥ight child exist
            if (q.front()->right)

                // Push into the queue
                q.push(q.front()->right);

            // Vacate right child
            q.front()->right = NULL;

            // If left child exists
            if (q.front()->left)

                // Push into the queue
                q.push(q.front()->left);

            // Vacate left child
            q.front()->left = NULL;

            // Add the node to stack to
            // maintain sequence of nodes
            // present in the level
            temp.push(q.front());
            q.pop();
        }

        while (!st.empty())
            st.pop();

        // Add nodes of the next
        // level into the stack st
        while (!temp.empty()) {

            st.push(temp.top());
            temp.pop();
        }
    }

    // Return the root of the
    // modified Tree
    return root;
}

// Driver Code
int main()
{

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->right = new TreeNode(6);

    // Function Call
    root = shiftRight(root);

    // Print the inOrder Traversal
    printTree(root);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;
public class Main
{

    // Class containing left and
    // right child of current
    // node and key value
    static class TreeNode {

        public int val;
        public TreeNode left, right;

        public TreeNode(int x)
        {
            val = x;
            left = right = null;
        }
    }

    // Function to print Inorder
    // Traversal of a Binary Tree
    static void printTree(TreeNode root)
    {
        if (root == null)
            return;

        // Traverse left child
        printTree(root.left);

        // Print current node
        System.out.print(root.val + " ");

        // Traverse right child
        printTree(root.right);
    }

    // Function to shift all nodes of the
    // given Binary Tree to as far as
    // right possible
    static TreeNode shiftRight(TreeNode root)
    {

        // If tree is empty
        if (root == null)
            return null;

        Stack<TreeNode> st = new Stack<TreeNode>();
        Queue<TreeNode> q = new LinkedList<>();

        // If right child exists
        if (root.right != null)
            q.add(root.right);

        root.right = null;

        // If left child exists
        if (root.left != null)
            q.add(root.left);

        root.left = null;

        // Push current node into stack
        st.push(root);

        while (q.size() > 0) {

            // Count valid existing nodes
            // in current level
            int n = q.size();
            Stack<TreeNode> temp = new Stack<TreeNode>();

            // Iterate existing nodes
            // in the current level
            while (n-- > 0) {

                // If no right child exists
                if (((TreeNode)st.peek()).right == null)

                    // Set the rightmost
                    // vacant node
                    ((TreeNode)st.peek()).right = (TreeNode)q.peek();

                // If no left child exists
                else {

                    // Set rightmost vacant node
                    ((TreeNode)st.peek()).left = (TreeNode)q.peek();

                    // Remove the node as both
                    // child nodes are occupied
                    st.pop();
                }

                // If r̥ight child exist
                if (((TreeNode)q.peek()).right != null)

                    // Push into the queue
                    q.add(((TreeNode)q.peek()).right);

                // Vacate right child
                ((TreeNode)q.peek()).right = null;

                // If left child exists
                if (((TreeNode)q.peek()).left != null)

                    // Push into the queue
                    q.add(((TreeNode)q.peek()).left);

                // Vacate left child
                ((TreeNode)q.peek()).left = null;

                // Add the node to stack to
                // maintain sequence of nodes
                // present in the level
                temp.push(((TreeNode)q.peek()));
                q.remove();
            }

            while (st.size() > 0)
                st.pop();

            // Add nodes of the next
            // level into the stack st
            while (temp.size() > 0) {

                st.push(temp.peek());
                temp.pop();
            }
        }

        // Return the root of the
        // modified Tree
        return root;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(6);

        // Function Call
        root = shiftRight(root);

        // Print the inOrder Traversal
        printTree(root);
    }
}

// This code is contributed by suresh07.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Structure of a Tree node
class TreeNode:

    def __init__(self,val):
        self.val = val
        self.left = None
        self.right = None

# Function to print Inorder
# Traversal of a Binary Tree
def printTree(root):
    if (root == None):
        return

    # Traverse left child
    printTree(root.left)

    # Print current node
    print(root.val,end = " ")

    # Traverse right child
    printTree(root.right)

# Function to shift all nodes of the
# given Binary Tree to as far as
# right possible
def shiftRight(root):

    # If tree is empty
    if (root == None):
        return None

    st = []  #stack
    q = [] # queue

    # If right child exists
    if (root.right):
        q.append(root.right)

    root.right = None

    # If left child exists
    if (root.left):
        q.append(root.left)

    root.left = None

    # Push current node into stack
    st.append(root)

    while (len(q) > 0):

        # Count valid existing nodes
        # in current level
        n = len(q)
        temp = []

        # Iterate existing nodes
        # in the current level
        while (n > 0 and len(st) > 0 and len(q) > 0):

            # If no right child exists
            if (st[len(st) - 1].right == None):

                # Set the rightmost
                # vacant node
                st[len(st) - 1].right = q[0]

            # If no left child exists
            else:

                # Set rightmost vacant node
                st[len(st) - 1].left = q[0]

                # Remove the node as both
                # child nodes are occupied
                st = st[:-1]

            # If r̥ight child exist
            if (q[0].right):

                # Push into the queue
                q.append(q[0].right)

            # Vacate right child
            q[0].right = None

            # If left child exists
            if (q[0].left):

                # Push into the queue
                q.append(q[0].left)

            # Vacate left child
            q[0].left = None

            # Add the node to stack to
            # maintain sequence of nodes
            # present in the level
            temp.append(q[0])
            q = q[1:]

        while (len(st) > 0):
            st = st[:-1]

        # Add nodes of the next
        # level into the stack st
        while(len(temp)>0):
            st.append(temp[len(temp)-1])
            temp = temp[:-1]

    # Return the root of the
    # modified Tree
    return root

# Driver Code
if __name__ == '__main__':
    root = TreeNode(1)
    root.left = TreeNode(2)
    root.right = TreeNode(3)
    root.left.left = TreeNode(4)
    root.left.right = TreeNode(5)
    root.right.right = TreeNode(6)

    # Function Call
    root = shiftRight(root)

    # Print the inOrder Traversal
    printTree(root)

    # This code is contributed by SURENDRA_GANGWAR.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Class containing left and
    // right child of current
    // node and key value
    class TreeNode {

        public int val;
        public TreeNode left, right;

        public TreeNode(int x)
        {
            val = x;
            left = right = null;
        }
    }

    // Function to print Inorder
    // Traversal of a Binary Tree
    static void printTree(TreeNode root)
    {
        if (root == null)
            return;

        // Traverse left child
        printTree(root.left);

        // Print current node
        Console.Write(root.val + " ");

        // Traverse right child
        printTree(root.right);
    }

    // Function to shift all nodes of the
    // given Binary Tree to as far as
    // right possible
    static TreeNode shiftRight(TreeNode root)
    {

        // If tree is empty
        if (root == null)
            return null;

        Stack st = new Stack();
        Queue q = new Queue();

        // If right child exists
        if (root.right != null)
            q.Enqueue(root.right);

        root.right = null;

        // If left child exists
        if (root.left != null)
            q.Enqueue(root.left);

        root.left = null;

        // Push current node into stack
        st.Push(root);

        while (q.Count > 0) {

            // Count valid existing nodes
            // in current level
            int n = q.Count;
            Stack temp = new Stack();

            // Iterate existing nodes
            // in the current level
            while (n-- > 0) {

                // If no right child exists
                if (((TreeNode)st.Peek()).right == null)

                    // Set the rightmost
                    // vacant node
                    ((TreeNode)st.Peek()).right = (TreeNode)q.Peek();

                // If no left child exists
                else {

                    // Set rightmost vacant node
                    ((TreeNode)st.Peek()).left = (TreeNode)q.Peek();

                    // Remove the node as both
                    // child nodes are occupied
                    st.Pop();
                }

                // If r̥ight child exist
                if (((TreeNode)q.Peek()).right != null)

                    // Push into the queue
                    q.Enqueue(((TreeNode)q.Peek()).right);

                // Vacate right child
                ((TreeNode)q.Peek()).right = null;

                // If left child exists
                if (((TreeNode)q.Peek()).left != null)

                    // Push into the queue
                    q.Enqueue(((TreeNode)q.Peek()).left);

                // Vacate left child
                ((TreeNode)q.Peek()).left = null;

                // Add the node to stack to
                // maintain sequence of nodes
                // present in the level
                temp.Push(((TreeNode)q.Peek()));
                q.Dequeue();
            }

            while (st.Count > 0)
                st.Pop();

            // Add nodes of the next
            // level into the stack st
            while (temp.Count > 0) {

                st.Push(temp.Peek());
                temp.Pop();
            }
        }

        // Return the root of the
        // modified Tree
        return root;
    }

  static void Main() {
    TreeNode root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(5);
    root.right.right = new TreeNode(6);

    // Function Call
    root = shiftRight(root);

    // Print the inOrder Traversal
    printTree(root);
  }
}

// This code is contributed by decode2207.
```

## **java 描述语言**

```
<script>

    // JavaScript program for the above approach

    class TreeNode
    {
        constructor(x) {
           this.left = null;
           this.right = null;
           this.val = x;
        }
    }

    // Function to print Inorder
    // Traversal of a Binary Tree
    function printTree(root)
    {
        if (!root)
            return;

        // Traverse left child
        printTree(root.left);

        // Print current node
        document.write(root.val + " ");

        // Traverse right child
        printTree(root.right);
    }

    // Function to shift all nodes of the
    // given Binary Tree to as far as
    // right possible
    function shiftRight(root)
    {

        // If tree is empty
        if (root == null)
            return null;

        let st = [];
        let q = [];

        // If right child exists
        if (root.right)
            q.push(root.right);

        root.right = null;

        // If left child exists
        if (root.left != null)
            q.push(root.left);

        root.left = null;

        // Push current node into stack
        st.push(root);

        while (q.length > 0) {

            // Count valid existing nodes
            // in current level
            let n = q.length;
            let temp = [];

            // Iterate existing nodes
            // in the current level
            while (n-- > 0) {

                // If no right child exists
                if (st[st.length - 1].right == null)

                    // Set the rightmost
                    // vacant node
                    st[st.length - 1].right = q[0];

                // If no left child exists
                else {

                    // Set rightmost vacant node
                    st[st.length - 1].left = q[0];

                    // Remove the node as both
                    // child nodes are occupied
                    st.pop();
                }

                // If r̥ight child exist
                if (q[0].right != null)

                    // Push into the queue
                    q.push(q[0].right);

                // Vacate right child
                q[0].right = null;

                // If left child exists
                if (q[0].left != null)

                    // Push into the queue
                    q.push(q[0].left);

                // Vacate left child
                q[0].left = null;

                // Add the node to stack to
                // maintain sequence of nodes
                // present in the level
                temp.push(q[0]);
                q.shift();
            }

            while (st.length > 0)
                st.pop();

            // Add nodes of the next
            // level into the stack st
            while (temp.length > 0) {

                st.push(temp[temp.length - 1]);
                temp.pop();
            }
        }

        // Return the root of the
        // modified Tree
        return root;
    }

    let root = new TreeNode(1);
    root.left = new TreeNode(2);
    root.right = new TreeNode(3);
    root.left.left = new TreeNode(4);
    root.left.right = new TreeNode(5);
    root.right.right = new TreeNode(6);

    // Function Call
    root = shiftRight(root);

    // Print the inOrder Traversal
    printTree(root);

</script>
```

****Output**

```
2 4 1 5 3 6 
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**

****方法 2: (** 使用散列表)
1。存储级别和相应的树节点。
2。然后贪婪地分配节点，首先作为右子节点，然后作为左子节点，成对 2。**

## **C++**

```
// CPP program for the above approach
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Structure of a Tree node
struct TreeNode {
    int val = 0;
    TreeNode* left;
    TreeNode* right;

    // Constructor
    TreeNode(int x)
    {
        val = x;
        left = right = NULL;
    }
};

// Function to print Inorder
// Traversal of a Binary Tree
void printTree(TreeNode* root)
{
    if (!root)
        return;

    // Traverse left child
    printTree(root->left);

    // Print current node
    cout << root->val << " ";

    // Traverse right child
    printTree(root->right);
}

void dfsit(TreeNode* rt, int key,
           map<int, vector<TreeNode*> >& mp)
{
    if (!rt) {
        return;
    }
    mp[key].push_back(rt);
    dfsit(rt->right, key + 1, mp);
    dfsit(rt->left, key + 1, mp);
    rt->left = NULL;
    rt->right = NULL;
}

TreeNode* shiftRight(TreeNode* root)
{
    TreeNode* tmp = root;
    map<int, vector<TreeNode*> > mp;
    int i = 0;

    dfsit(root, 0, mp);
    int n = mp.size();
    TreeNode* cur = new TreeNode(-1);

    queue<TreeNode*> st;
    st.push(cur);

  while (i < n) {
        vector<TreeNode*> nd = mp[i];
        int j = 0;
        queue<TreeNode*> tmp;
        while (j < nd.size()) {
            auto r = st.front();
            st.pop();
            r->right = nd[j];
            tmp.push(nd[j]);
            j++;
            if (j < nd.size()) {
                r->left = nd[j];
                tmp.push(nd[j]);
                j++;
            }
        }
        st = tmp;
        i++;
    }

    return cur->right;
}

// Driver Code
int main()
{

    TreeNode* root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);
    root->right->right = new TreeNode(6);

    // Function Call
    root = shiftRight(root);

    // Print the inOrder Traversal
    printTree(root);
    return 0;
}
```

****Output**

```
2 4 1 5 3 6 
```**