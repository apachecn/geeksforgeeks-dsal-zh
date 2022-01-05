# 检查二叉树是否包含偶数和奇数层严格递增和递减顺序的节点值

> 原文:[https://www . geeksforgeeks . org/check-if-a-二叉树-包含严格递增和递减顺序的节点值在偶数和奇数层/](https://www.geeksforgeeks.org/check-if-a-binary-tree-contains-node-values-in-strictly-increasing-and-decreasing-order-at-even-and-odd-levels/)

给定一个[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是检查它是否由节点值组成，节点值在偶数层严格递增，在奇数层严格递减(*假设根节点在级别 **0*** )。

**示例:**

> **输入:**
> 
> ```
>              2
>             / \
>            6   3
>           / \   \
>          4   7   11
>         / \   \
>        10  5   1
> ```
> 
> **输出:**是
> **说明:**
> 在 1 级(奇数)，节点值 6 和 3 是严格递减的顺序。
> 在级别 2(偶数)中，节点值 4、7 和 11 严格按递增顺序排列。
> 在级别 3(奇数)中，节点值 10、5 和 1 严格按降序排列。
> 因此，树满足给定的条件。
> 
> **输入:**
> 
> ```
>              5
>             / \
>            6   3
>           / \   \
>          4   9   2
> ```
> 
> **输出**:否

**方法:**思想是在给定的**二叉树**上执行[级序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)，对于每一级，检查它是否满足给定的条件。按照以下步骤解决问题:

*   创建一个空的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，在树的级别顺序遍历过程中逐个存储每一级的节点。
*   将根节点推入队列。
*   迭代直到队列为空，并执行以下操作:
    *   继续从队列中弹出当前级别的节点，并将其插入[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)。将其所有子节点推入**队列**。
    *   如果级别为偶数，[检查数组列表中的元素是否按升序排列](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。如果发现是真的，进入下一个级别。否则，打印**否**。
    *   同样，检查奇数层。
    *   完成树的遍历后，如果发现所有级别都满足条件，则打印**是**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int val;
    Node *left, *right;
};

struct Node* newNode(int data)
{
    struct Node* temp = (struct Node*)malloc(sizeof(struct Node));
    temp->val = data;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// Function to check if given binary
// tree satisfies the required conditions
bool checkEvenOddLevel(Node *root)
{
    if (root == NULL)
        return true;

    // Queue to store nodes
    // of each level
    queue<Node*> q;
    q.push(root);

    // Stores the current
    // level of the binary tree
    int level = 0;

    // Traverse until the
    // queue is empty
    while (q.empty())
    {
        vector<int> vec;

        // Stores the number of nodes
        // present in the current level
        int size = q.size();

        for(int i = 0; i < size; i++)
        {
            Node *node = q.front();
            vec.push_back(node->val);

            // Insert left and right child
            // of node into the queue
            if (node->left != NULL)
                q.push(node->left);

            if (node->right != NULL)
                q.push(node->right);
        }

        // If the level is even
        if (level % 2 == 0)
        {

            // If the nodes in this
            // level are in strictly
            // increasing order or not
            for(int i = 0; i < vec.size() - 1; i++)
            {
                if (vec[i + 1] > vec[i])
                    continue;

                return false;
            }
        }

        // If the level is odd
        else if (level % 2 == 1)
        {

            // If the nodes in this
            // level are in strictly
            // decreasing order or not
            for(int i = 0; i < vec.size() - 1; i++)
            {
                if (vec[i + 1] < vec[i])
                    continue;

                return false;
            }
        }

        // Increment the level count
        level++;
    }
    return true;
}

// Driver Code
int main()
{

    // Construct a Binary Tree
    Node *root = NULL;
    root = newNode(2);
    root->left = newNode(6);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(7);
    root->right->right = newNode(11);
    root->left->left->left = newNode(10);
    root->left->left->right = newNode(5);
    root->left->right->right = newNode(1);

    // Function Call
    if (checkEvenOddLevel(root))
        cout << "YES";
    else
        cout << "NO";
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG {

    // Structure of Tree node
    static class Node {
        int val;
        Node left, right;
    }

    // Function to create new Tree node
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.val = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Function to check if given binary
    // tree satisfies the required conditions
    public static boolean
    checkEvenOddLevel(Node root)
    {
        if (root == null)
            return true;

        // Queue to store nodes
        // of each level
        Queue<Node> q
            = new LinkedList<>();
        q.add(root);

        // Stores the current
        // level of the binary tree
        int level = 0;

        // Traverse until the
        // queue is empty
        while (!q.isEmpty()) {

            ArrayList<Integer> list
                = new ArrayList<>();

            // Stores the number of nodes
            // present in the current level
            int size = q.size();

            for (int i = 0; i < size; i++) {

                Node node = q.poll();
                list.add(node.val);

                // Insert left and right child
                // of node into the queue
                if (node.left != null)
                    q.add(node.left);

                if (node.right != null)
                    q.add(node.right);
            }

            // If the level is even
            if (level % 2 == 0) {

                // If the nodes in this
                // level are in strictly
                // increasing order or not
                for (int i = 0; i < list.size() - 1;
                     i++) {

                    if (list.get(i + 1) > list.get(i))
                        continue;
                    return false;
                }
            }

            // If the level is odd
            else if (level % 2 == 1) {

                // If the nodes in this
                // level are in strictly
                // decreasing order or not
                for (int i = 0; i < list.size() - 1;
                     i++) {

                    if (list.get(i + 1) < list.get(i))
                        continue;
                    return false;
                }
            }

            // Increment the level count
            level++;
        }

        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Construct a Binary Tree
        Node root = null;
        root = newNode(2);
        root.left = newNode(6);
        root.right = newNode(3);
        root.left.left = newNode(4);
        root.left.right = newNode(7);
        root.right.right = newNode(11);
        root.left.left.left = newNode(10);
        root.left.left.right = newNode(5);
        root.left.right.right = newNode(1);

        // Function Call
        if (checkEvenOddLevel(root)) {

            System.out.println("YES");
        }
        else {

            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Tree node
class Node:

    def __init__(self, data):

        self.left = None
        self.right = None
        self.val = data

# Function to return new tree node
def newNode(data):

    temp = Node(data)

    return temp

# Function to check if the
# tree is even-odd tree
def checkEvenOddLevel(root):

    if (root == None):
        return True

    q = []

    # Stores nodes of each level
    q.append(root)

    # Store the current level
    # of the binary tree
    level = 0

    # Traverse until the
    # queue is empty
    while (len(q) != 0):
        l = []

        # Stores the number of nodes
        # present in the current level
        size = len(q)

        for i in range(size):
            node = q[0]
            q.pop(0)

            # Insert left and right child
            # of node into the queue
            if (node.left != None):
                q.append(node.left);

            if (node.right != None):
                q.append(node.right);

            # If the level is even
            if (level % 2 == 0):

                # If the nodes in this
                # level are in strictly
                # increasing order or not
                for i in range(len(l) - 1):
                    if (l[i + 1] > l[i]):
                        continue

                    return False

            # If the level is odd
            elif (level % 2 == 1):

                # If the nodes in this
                # level are in strictly
                # decreasing order or not
                for i in range(len(l) - 1):
                    if (l[i + 1] < l[i]):
                        continue

                    return False

            # Increment the level count
            level += 1

        return True

# Driver code
if __name__=="__main__":

    # Construct a Binary Tree
    root = None
    root = newNode(2)
    root.left = newNode(6)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(7)
    root.right.right = newNode(11)
    root.left.left.left = newNode(10)
    root.left.left.right = newNode(5)
    root.left.right.right = newNode(1)

    # Check if the binary tree
    # is even-odd tree or not
    if (checkEvenOddLevel(root)):
        print("YES")
    else:
        print("NO")

# This code is contributed by rutvik_56
```

## C#

```
// C# Program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Structure of Tree node
public class Node
{
  public int val;
  public Node left, right;
}

// Function to create
// new Tree node
static Node newNode(int data)
{
  Node temp = new Node();
  temp.val = data;
  temp.left = null;
  temp.right = null;
  return temp;
}

// Function to check if given binary
// tree satisfies the required conditions
public static bool checkEvenOddLevel(Node root)
{
  if (root == null)
    return true;

  // Queue to store nodes
  // of each level
  Queue<Node> q =
              new Queue<Node>();
  q.Enqueue(root);

  // Stores the current
  // level of the binary tree
  int level = 0;

  // Traverse until the
  // queue is empty
  while (q.Count != 0)
  {
    List<int> list =
              new List<int>();

    // Stores the number of nodes
    // present in the current level
    int size = q.Count;

    for (int i = 0; i < size; i++)
    {
      Node node = q.Dequeue();
      list.Add(node.val);

      // Insert left and right child
      // of node into the queue
      if (node.left != null)
        q.Enqueue(node.left);

      if (node.right != null)
        q.Enqueue(node.right);
    }

    // If the level is even
    if (level % 2 == 0)
    {
      // If the nodes in this
      // level are in strictly
      // increasing order or not
      for (int i = 0;
               i < list.Count - 1; i++)
      {
        if (list[i + 1] > list[i])
          continue;
        return false;
      }
    }

    // If the level is odd
    else if (level % 2 == 1)
    {
      // If the nodes in this
      // level are in strictly
      // decreasing order or not
      for (int i = 0;
               i < list.Count - 1; i++)
      {
        if (list[i + 1] < list[i])
          continue;
        return false;
      }
    }

    // Increment the level count
    level++;
  }

  return true;
}

// Driver Code
public static void Main(String[] args)
{
  // Construct a Binary Tree
  Node root = null;
  root = newNode(2);
  root.left = newNode(6);
  root.right = newNode(3);
  root.left.left = newNode(4);
  root.left.right = newNode(7);
  root.right.right = newNode(11);
  root.left.left.left = newNode(10);
  root.left.left.right = newNode(5);
  root.left.right.right = newNode(1);

  // Function Call
  if (checkEvenOddLevel(root))
  {
    Console.WriteLine("YES");
  }
  else
  {
    Console.WriteLine("NO");
  }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Structure of Tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.val = data;
    }
}

// Function to create new Tree node
function newNode(data)
{
    let temp = new Node(data);
    return temp;
}

// Function to check if given binary
// tree satisfies the required conditions
function checkEvenOddLevel(root)
{
    if (root == null)
        return true;

    // Queue to store nodes
    // of each level
    let q = [];
    q.push(root);

    // Stores the current
    // level of the binary tree
    let level = 0;

    // Traverse until the
    // queue is empty
    while (q.length > 0)
    {
        let list = [];

        // Stores the number of nodes
        // present in the current level
        let size = q.length;

        for(let i = 0; i < size; i++)
        {
            let node = q[0];
            q.shift();
            list.push(node.val);

            // Insert left and right child
            // of node into the queue
            if (node.left != null)
                q.push(node.left);

            if (node.right != null)
                q.push(node.right);
        }

        // If the level is even
        if (level % 2 == 0)
        {

            // If the nodes in this
            // level are in strictly
            // increasing order or not
            for(let i = 0; i < list.length - 1; i++)
            {
                if (list[i + 1] > list[i])
                    continue;

                return false;
            }
        }

        // If the level is odd
        else if (level % 2 == 1)
        {

            // If the nodes in this
            // level are in strictly
            // decreasing order or not
            for(let i = 0; i < list.length - 1; i++)
            {
                if (list[i + 1] < list[i])
                    continue;

                return false;
            }
        }

        // Increment the level count
        level++;
    }
    return true;
}

// Driver code

// Construct a Binary Tree
let root = null;
root = newNode(2);
root.left = newNode(6);
root.right = newNode(3);
root.left.left = newNode(4);
root.left.right = newNode(7);
root.right.right = newNode(11);
root.left.left.left = newNode(10);
root.left.left.right = newNode(5);
root.left.right.right = newNode(1);

// Function Call
if (checkEvenOddLevel(root))
{
    document.write("YES");
}
else
{
    document.write("NO");
}

// This code is contributed by suresh07

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)