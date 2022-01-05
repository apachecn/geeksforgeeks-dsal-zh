# 在给定的二叉树中找到最大乘积兄弟的父节点

> 原文:[https://www . geesforgeks . org/find-给定二叉树中最大乘积的父节点/](https://www.geeksforgeeks.org/find-the-parent-node-of-maximum-product-siblings-in-given-binary-tree/)

给定一个**二叉树**，任务是在给定的二叉树中找到子节点具有最大同辈积的节点。如果有多个这样的节点，则返回具有最大值的节点。

**示例:**

> **输入:**树:
> **4
> /\
> 5 2
> /\
> 3 1
> /\
> 6 12
> **输出:** 3
> **说明:**对于上面的树，对于作为节点 3 的子节点的节点 6 和 12，形成了兄弟的最大乘积。**
> 
> ****输入:**树:
> **1
> /\
> 3 5
> /\
> 6 9 4 8
> **输出:** 3
> **说明:**对于上面的树，对于作为节点 5 的子节点的节点 6 和 9，形成了兄弟节点的最大乘积。****

******方法:**要解决这个问题，可以使用二叉树的 [**级序遍历**](https://www.geeksforgeeks.org/level-order-tree-traversal/) 来寻找兄弟姐妹的最大和。请遵循以下步骤:****

*   ****从树根开始**级顺序遍历**树。****
*   ****对于每个节点，检查它是否有两个子节点。

    *   如果是，则找到子代乘积最大的节点，并将该节点值存储在引用变量中。
    *   如果发现任何节点具有更大的子代乘积，则更新引用变量中的节点值。**** 
*   ****如果当前节点**没有**两个**子节点，**则跳过该节点****
*   ****返回引用变量中的节点值，因为它包含子节点乘积最大的节点，或者子节点乘积最大的父节点。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ code to find the Parent Node
// of maximum product Siblings
// in given Binary Tree

#include <bits/stdc++.h>
using namespace std;

// Structure for Node
struct Node {
    int data;
    Node *left, *right;
};

// Function to get a new node
Node* getNode(int data)
{
    // Allocate space
    Node* newNode
      = (Node*)malloc(sizeof(Node));

    // Put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Function to get the parent
// of siblings with maximum product
int maxproduct(Node* root)
{
    int mproduct = INT_MIN;
    int ans = 0;

    // Checking base case
    if (root == NULL
        || (root->left == NULL
            && root->right == NULL))
        return 0;

    // Declaration of queue to run
    // level order traversal
    queue<Node*> q;
    q.push(root);

    // Loop to implement level order traversal
    while (!q.empty()) {
        Node* temp = q.front();
        q.pop();

        // If both the siblings are present
        // then take their product
        if (temp->right && temp->left) {
            int curr_max
                = temp->right->data
              * temp->left->data;
            if (mproduct < curr_max) {
                mproduct = curr_max;
                ans = temp->data;
            }
            else if (mproduct == curr_max) {

                // if max product is equal to
                // curr_max then consider node
                // which has maximum value
                ans = max(ans, temp->data);
            }
        }

        // pushing childs in the queue
        if (temp->right) {
            q.push(temp->right);
        }
        if (temp->left) {
            q.push(temp->left);
        }
    }
    return ans;
}

// Driver Code
int main()
{
    /* Binary tree creation
              1
            /   \
           3     5
          / \   / \
         6   9 4   8
      */
    Node* root = getNode(1);
    root->left = getNode(3);
    root->right = getNode(5);
    root->left->left = getNode(6);
    root->left->right = getNode(9);
    root->right->left = getNode(4);
    root->right->right = getNode(8);

    cout << maxproduct(root) << endl;
    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java code to find the Parent Node
// of maximum product Siblings
// in given Binary Tree
import java.util.LinkedList;
import java.util.Queue;

class GFG {

    // Structure for Node
    static class Node {
        int data;
        Node left;
        Node right;

        public Node(int data) {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Function to get a new node
    public static Node getNode(int data) {
        // Allocate space
        Node newNode = new Node(data);

        // Put in the data
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
    }

    // Function to get the parent
    // of siblings with maximum product
    public static int maxproduct(Node root) {
        int mproduct = Integer.MIN_VALUE;
        int ans = 0;

        // Checking base case
        if (root == null
                || (root.left == null
                        && root.right == null))
            return 0;

        // Declaration of queue to run
        // level order traversal
        Queue<Node> q = new LinkedList<Node>();

        q.add(root);

        // Loop to implement level order traversal
        while (!q.isEmpty()) {
            Node temp = q.peek();
            q.remove();

            // If both the siblings are present
            // then take their product
            if (temp.right != null && temp.left != null) {
                int curr_max = temp.right.data
                        * temp.left.data;
                if (mproduct < curr_max) {
                    mproduct = curr_max;
                    ans = temp.data;
                } else if (mproduct == curr_max) {

                    // if max product is equal to
                    // curr_max then consider node
                    // which has maximum value
                    ans = Math.max(ans, temp.data);
                }
            }

            // pushing childs in the queue
            if (temp.right != null) {
                q.add(temp.right);
            }
            if (temp.left != null) {
                q.add(temp.left);
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {
        /*
         * Binary tree creation
         * 1
         * / \
         * 3 5
         * / \ / \
         * 6 9 4 8
         */
        Node root = getNode(1);
        root.left = getNode(3);
        root.right = getNode(5);
        root.left.left = getNode(6);
        root.left.right = getNode(9);
        root.right.left = getNode(4);
        root.right.right = getNode(8);

        System.out.println(maxproduct(root));
    }
}

// This code is contributed by gfgking.**
```

## ****蟒蛇 3****

```
**# Python Program to implement
# the above approach

# Structure of a node of binary tree
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to get a new node
def getNode(data):

    # Allocate space
    newNode = Node(data)
    return newNode

# Function to get the parent
# of siblings with maximum product
def maxproduct(root):
    mproduct = 10 ** -9
    ans = 0;

    # Checking base case
    if (root == None or (root.left == None and root.right == None)):
        return 0;

    # Declaration of queue to run
    # level order traversal
    q = [];
    q.append(root);

    # Loop to implement level order traversal
    while (len(q)):
        temp = q[0];
        q.pop(0);

        # If both the siblings are present
        # then take their product
        if (temp.right and temp.left):
            curr_max = temp.right.data * temp.left.data;
            if (mproduct < curr_max):
                mproduct = curr_max
                ans = temp.data
            elif (mproduct == curr_max):

                # if max product is equal to
                # curr_max then consider node
                # which has maximum value
                ans = max(ans, temp.data)

        # pushing childs in the queue
        if (temp.right):
            q.append(temp.right)
        if (temp.left):
            q.append(temp.left)

    return ans

# Driver Code

""" Binary tree creation
            1
        /   \
        3     5
        / \   / \
        6   9 4   8
"""
root = getNode(1);
root.left = getNode(3);
root.right = getNode(5);
root.left.left = getNode(6);
root.left.right = getNode(9);
root.right.left = getNode(4);
root.right.right = getNode(8);

print(maxproduct(root));

# This code is contributed by gfgking**
```

## ****C#****

```
**// C# code to find the Parent Node
// of maximum product Siblings
// in given Binary Tree
using System;
using System.Collections.Generic;

public class GFG {

    // Structure for Node
    class Node {
        public int data;
        public Node left;
        public Node right;

        public Node(int data) {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    };

    // Function to get a new node
    static Node getNode(int data) {
        // Allocate space
        Node newNode = new Node(data);

        // Put in the data
        newNode.data = data;
        newNode.left = newNode.right = null;
        return newNode;
    }

    // Function to get the parent
    // of siblings with maximum product
    static int maxproduct(Node root) {
        int mproduct = int.MinValue;
        int ans = 0;

        // Checking base case
        if (root == null
                || (root.left == null
                        && root.right == null))
            return 0;

        // Declaration of queue to run
        // level order traversal
        Queue<Node> q = new Queue<Node>();

        q.Enqueue(root);

        // Loop to implement level order traversal
        while (q.Count!=0) {
            Node temp = q.Peek();
            q.Dequeue();

            // If both the siblings are present
            // then take their product
            if (temp.right != null && temp.left != null) {
                int curr_max = temp.right.data
                        * temp.left.data;
                if (mproduct < curr_max) {
                    mproduct = curr_max;
                    ans = temp.data;
                } else if (mproduct == curr_max) {

                    // if max product is equal to
                    // curr_max then consider node
                    // which has maximum value
                    ans = Math.Max(ans, temp.data);
                }
            }

            // pushing childs in the queue
            if (temp.right != null) {
                q.Enqueue(temp.right);
            }
            if (temp.left != null) {
                q.Enqueue(temp.left);
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main(String []args) {
        /*
         * Binary tree creation
         * 1
         * / \
         * 3 5
         * / \ / \
         * 6 9 4 8
         */
        Node root = getNode(1);
        root.left = getNode(3);
        root.right = getNode(5);
        root.left.left = getNode(6);
        root.left.right = getNode(9);
        root.right.left = getNode(4);
        root.right.right = getNode(8);

        Console.WriteLine(maxproduct(root));
    }
}

// This code is contributed by shikhasingrajput**
```

## ****java 描述语言****

```
**<script>

        // JavaScript Program to implement
        // the above approach

        // Structure of a node of binary tree
        class Node {
            constructor(data) {
                this.data = data;
                this.left = null;
                this.right = null;
            }
        };

        // Function to get a new node
        function getNode(data)
        {

            // Allocate space
            let newNode
                = new Node(data);
            return newNode;
        }

        // Function to get the parent
        // of siblings with maximum product
        function maxproduct(root) {
            let mproduct = Number.MIN_VALUE;
            let ans = 0;

            // Checking base case
            if (root == null
                || (root.left == null
                    && root.right == null))
                return 0;

            // Declaration of queue to run
            // level order traversal
            let q = [];
            q.push(root);

            // Loop to implement level order traversal
            while (!q.length == 0) {
                let temp = q[0];
                q.shift();

                // If both the siblings are present
                // then take their product
                if (temp.right && temp.left) {
                    let curr_max
                        = temp.right.data
                        * temp.left.data;
                    if (mproduct < curr_max) {
                        mproduct = curr_max;
                        ans = temp.data;
                    }
                    else if (mproduct == curr_max) {

                        // if max product is equal to
                        // curr_max then consider node
                        // which has maximum value
                        ans = Math.max(ans, temp.data);
                    }
                }

                // pushing childs in the queue
                if (temp.right) {
                    q.push(temp.right);
                }
                if (temp.left) {
                    q.push(temp.left);
                }
            }
            return ans;
        }

        // Driver Code

        /* Binary tree creation
                  1
                /   \
               3     5
              / \   / \
             6   9 4   8
          */
        let root = getNode(1);
        root.left = getNode(3);
        root.right = getNode(5);
        root.left.left = getNode(6);
        root.left.right = getNode(9);
        root.right.left = getNode(4);
        root.right.right = getNode(8);

        document.write(maxproduct(root) + "<br>");

    // This code is contributed by Potta Lokesh
    </script>**
```

******Output**

```
3
```**** 

******时间复杂度:** O(V)，其中 V 是树中的节点数。
**辅助空间:** O(V)。****