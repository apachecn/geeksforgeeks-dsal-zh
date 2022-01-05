# 完全二叉树的迭代边界遍历

> 原文:[https://www . geeksforgeeks . org/迭代-边界-遍历-完全-二叉树/](https://www.geeksforgeeks.org/iterative-boundary-traversal-of-complete-binary-tree/)

给定一个完整的二叉树，遍历它，使得所有的边界节点从根开始以逆时针顺序被访问。
**例:**

```
Input:
               18
           /       \  
         15         30  
        /  \        /  \
      40    50    100   20
Output: 18 15 40 50 100 20 30
```

**进场:**

*   从上到下遍历树的最左侧节点。(左边界)
*   从左到右遍历树的最底层。(叶节点)
*   自下而上遍历树的最右侧节点。(右边界)

在 while 循环的帮助下，我们可以非常容易地遍历左边界，该循环检查节点何时没有剩余的子节点。类似地，在 while 循环的帮助下，我们可以非常容易地遍历正确的边界，该循环检查节点何时没有任何正确的子节点。
这里的主要挑战是按照从左到右的顺序遍历树的最后一级。要逐级遍历，有 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) ，从左到右的顺序可以通过首先推送队列中的左节点来处理。所以现在唯一剩下的就是确定是最后一关。只需检查节点是否有任何子节点，并且只包含它们。
我们必须特别注意拐角情况，即相同的节点不会再次遍历。在上面的例子中，40 是左边界和叶节点的一部分。类似地，20 是右边界和叶节点的一部分。
所以在这种情况下，我们只需要遍历到两个边界的第二个最后节点。还要记住，我们不应该再次遍历根。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer
   to left child and a pointer to right
   child */
struct Node {
    int data;
    struct Node *left, *right;
};

/* Helper function that allocates a new
   node with the given data and NULL left
   and right pointers. */
struct Node* newNode(int data)
{
    Node* temp = new Node;

    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Function to print the nodes of a complete
// binary tree in boundary traversal order
void boundaryTraversal(Node* root)
{
    if (root) {

        // If there is only 1 node print it
        // and return
        if (!(root->left) && !(root->right)) {
            cout << root->data << endl;
            return;
        }

        // List to store order of traversed
        // nodes
        vector<Node*> list;
        list.push_back(root);

        // Traverse left boundary without root
        // and last node
        Node* L = root->left;
        while (L->left) {
            list.push_back(L);
            L = L->left;
        }

        // BFS designed to only include leaf nodes
        queue<Node*> q;
        q.push(root);
        while (!q.empty()) {
            Node* temp = q.front();
            q.pop();
            if (!(temp->left) && !(temp->right)) {
                list.push_back(temp);
            }
            if (temp->left) {
                q.push(temp->left);
            }
            if (temp->right) {
                q.push(temp->right);
            }
        }

        // Traverse right boundary without root
        // and last node
        vector<Node*> list_r;
        Node* R = root->right;
        while (R->right) {
            list_r.push_back(R);
            R = R->right;
        }

        // Reversing the order
        reverse(list_r.begin(), list_r.end());

        // Concatenating the two lists
        list.insert(list.end(), list_r.begin(),
                                 list_r.end());

        // Printing the node's data from the list
        for (auto i : list) {
            cout << i->data << " ";
        }
        cout << endl;
        return;
    }
}

// Driver code
int main()
{

    // Root node of the tree
    Node* root = newNode(20);

    root->left = newNode(8);
    root->right = newNode(22);

    root->left->left = newNode(4);
    root->left->right = newNode(12);

    root->right->left = newNode(10);
    root->right->right = newNode(25);

    boundaryTraversal(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

/* A binary tree node has data, pointer
   to left child and a pointer to right
   child */
static class Node {
    int data;
    Node left, right;
};

/* Helper function that allocates a new
   node with the given data and null left
   and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();

    temp.data = data;
    temp.left = temp.right = null;

    return temp;
}

// Function to print the nodes of a complete
// binary tree in boundary traversal order
static void boundaryTraversal(Node root)
{
    if (root != null) {

        // If there is only 1 node print it
        // and return
        if ((root.left == null) && (root.right == null)) {
            System.out.print(root.data +"\n");
            return;
        }

        // List to store order of traversed
        // nodes
        Vector<Node> list = new Vector<Node>();
        list.add(root);

        // Traverse left boundary without root
        // and last node
        Node L = root.left;
        while (L.left != null) {
            list.add(L);
            L = L.left;
        }

        // BFS designed to only include leaf nodes
        Queue<Node> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()) {
            Node temp = q.peek();
            q.remove();
            if ((temp.left == null) && (temp.right == null)) {
                list.add(temp);
            }
            if (temp.left != null) {
                q.add(temp.left);
            }
            if (temp.right != null) {
                q.add(temp.right);
            }
        }

        // Traverse right boundary without root
        // and last node
        Vector<Node> list_r = new Vector<Node>();
        Node R = root.right;
        while (R.right != null) {
            list_r.add(R);
            R = R.right;
        }

        // Reversing the order
        Collections.reverse(list_r);

        // Concatenating the two lists
        list.addAll(list_r);

        // Printing the node's data from the list
        for (Node i : list) {
            System.out.print(i.data + " ");
        }
        System.out.println();
        return;
    }
}

// Driver code
public static void main(String[] args)
{

    // Root node of the tree
    Node root = newNode(20);

    root.left = newNode(8);
    root.right = newNode(22);

    root.left.left = newNode(4);
    root.left.right = newNode(12);

    root.right.left = newNode(10);
    root.right.right = newNode(25);

    boundaryTraversal(root);
}
}

// This code is contributed by Princi Singh
```

## 计算机编程语言

```
# Python implementation of the approach
from collections import deque

# A binary tree node
class Node:

    # A constructor for making a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to print the nodes of a complete
# binary tree in boundary traversal order
def boundaryTraversal(root):
    # If there is only 1 node print it and return
    if root:
        if not root.left and not root.right:
            print (root.data)
            return

        # List to store order of traversed nodes
        list = []
        list.append(root)

        # Traverse left boundary without root
        # and last node
        temp = root.left
        while temp.left:
            list.append(temp)
            temp = temp.left

        # BFS designed to only include leaf nodes
        q = deque()
        q.append(root)
        while len(q) != 0:
            x = q.pop()
            if not x.left and not x.right:
                list.append(x)
            if x.right:
                q.append(x.right)
            if x.left:
                q.append(x.left)

        # Traverse right boundary without root
        # and last node
        list_r = []
        temp = root.right
        while temp.right:
            list.append(temp)
            temp = temp.right

        # Reversing the order
        list_r = list_r[::-1]

        # Concatenating the two lists
        list += list_r

        # Printing the node's data from the list
        print (" ".join([str(i.data) for i in list]))
    return

# Root node of the tree

root = Node(20)

root.left = Node(8)
root.right = Node(22)

root.left.left = Node(4)
root.left.right = Node(12)

root.right.left = Node(10)
root.right.right = Node(25)

boundaryTraversal(root)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

/* A binary tree node has data, pointer
   to left child and a pointer to right
   child */
class Node
{
    public int data;
    public Node left, right;
};

/* Helper function that allocates a new
   node with the given data and null left
   and right pointers. */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = temp.right = null;
    return temp;
}

// Function to print the nodes of a complete
// binary tree in boundary traversal order
static void boundaryTraversal(Node root)
{
    if (root != null)
    {

        // If there is only 1 node print it
        // and return
        if ((root.left == null) &&
            (root.right == null))
        {
            Console.Write(root.data + "\n");
            return;
        }

        // List to store order of traversed
        // nodes
        List<Node> list = new List<Node>();
        list.Add(root);

        // Traverse left boundary without root
        // and last node
        Node L = root.left;
        while (L.left != null)
        {
            list.Add(L);
            L = L.left;
        }

        // BFS designed to only include leaf nodes
        Queue<Node> q = new Queue<Node>();
        q.Enqueue(root);
        while (q.Count != 0)
        {
            Node temp = q.Peek();
            q.Dequeue();
            if ((temp.left == null) &&
                (temp.right == null))
            {
                list.Add(temp);
            }
            if (temp.left != null)
            {
                q.Enqueue(temp.left);
            }
            if (temp.right != null)
            {
                q.Enqueue(temp.right);
            }
        }

        // Traverse right boundary without root
        // and last node
        List<Node> list_r = new List<Node>();
        Node R = root.right;
        while (R.right != null)
        {
            list_r.Add(R);
            R = R.right;
        }

        // Reversing the order
        list_r.Reverse();

        // Concatenating the two lists
        list.InsertRange(list.Count-1, list_r);

        // Printing the node's data from the list
        foreach (Node i in list)
        {
            Console.Write(i.data + " ");
        }
        Console.WriteLine();
        return;
    }
}

// Driver code
public static void Main(String[] args)
{

    // Root node of the tree
    Node root = newNode(20);
    root.left = newNode(8);
    root.right = newNode(22);
    root.left.left = newNode(4);
    root.left.right = newNode(12);
    root.right.left = newNode(10);
    root.right.right = newNode(25);
    boundaryTraversal(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

      /* A binary tree node has data, pointer
    to left child and a pointer to right
    child */
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    /* Helper function that allocates a new
   node with the given data and null left
   and right pointers. */
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Function to print the nodes of a complete
    // binary tree in boundary traversal order
    function boundaryTraversal(root)
    {
        if (root != null) {

            // If there is only 1 node print it
            // and return
            if ((root.left == null) && (root.right == null)) {
                document.write(root.data +"</br>");
                return;
            }

            // List to store order of traversed
            // nodes
            let list = [];
            list.push(root);

            // Traverse left boundary without root
            // and last node
            let L = root.left;
            while (L.left != null) {
                list.push(L);
                L = L.left;
            }

            // BFS designed to only include leaf nodes
            let q = [];
            q.push(root);
            while (q.length > 0) {
                let temp = q[0];
                q.shift();
                if ((temp.left == null) && (temp.right == null)) {
                    list.push(temp);
                }
                if (temp.left != null) {
                    q.push(temp.left);
                }
                if (temp.right != null) {
                    q.push(temp.right);
                }
            }

            // Traverse right boundary without root
            // and last node
            let list_r = [];
            let R = root.right;
            while (R.right != null) {
                list_r.push(R);
                R = R.right;
            }

            // Reversing the order
            list_r.reverse();

            // Concatenating the two lists
            for(let i = 0; i < list_r.length; i++)
            {
                list.push(list_r[i]);
            }

            // Printing the node's data from the list
            for (let i = 0; i < list.length; i++) {
                document.write(list[i].data + " ");
            }
            document.write("</br>");
            return;
        }
    }

    // Root node of the tree
    let root = newNode(20);

    root.left = newNode(8);
    root.right = newNode(22);

    root.left.left = newNode(4);
    root.left.right = newNode(12);

    root.right.left = newNode(10);
    root.right.right = newNode(25);

    boundaryTraversal(root);

</script>
```

**Output:** 

```
20 8 4 12 10 25 22
```