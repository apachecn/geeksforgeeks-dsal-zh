# 检查两个二叉树是否同构的迭代方法

> 原文:[https://www . geeksforgeeks . org/迭代方法检查两个二叉树是否同构/](https://www.geeksforgeeks.org/iterative-approach-to-check-if-two-binary-trees-are-isomorphic-or-not/)

给定**两个二叉树**，我们必须检测这两个树是否**同构**。如果可以通过一系列翻转(即交换多个节点的左右子节点)从另一个树获得其中一个树，则这两个树称为同构。任何级别的任何数量的节点都可以交换其子节点。

*注:两个空树同构。*

例如，以下两个树与以下翻转的子树同构:2 和 3、空和 6、7 和 8。

![](img/8b50bd9e6a390f4f7cf6fbf53a44c539.png)

**方法:**
为了解决上述问题，我们使用级别顺序遍历迭代遍历两个树，并将级别存储在队列数据结构中。每个级别有以下两个条件:

*   节点的值必须相同。
*   每个级别的节点数量应该相同。

检查队列的大小以匹配上面提到的第二个条件。将第一棵树的每一级的节点存储为带有值的关键字，对于第二棵树，我们将在一个向量中存储一级的所有节点。如果找到了密钥，我们将减少该值，以跟踪在一个级别上存在多少个具有相同值的节点。如果该值变为零，这意味着第一棵树只有这么多节点，我们将把它作为一个键删除。在每个级别的末尾，我们将遍历数组，检查每个值是否存在于地图上。会有三个条件:

*   如果找不到关键字，则第一棵树不包含在同一级别的第二棵树中找到的节点。
*   如果找到了关键字，但该值变为负值，则第二棵树具有更多与第一棵树具有相同值的节点。
*   如果地图大小不为零，这意味着还剩下一些键，这意味着第一棵树的节点与第二棵树中的任何节点都不匹配。

下面是上述方法的实现:

## C++

```
// C++ program to find two
// Binary Tree are Isomorphic or not

#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left and right children */
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* function to return if
   tree are isomorphic or not*/
bool isIsomorphic(node* root1, node* root2)
{
    // if Both roots are null
    // then tree is isomorphic
    if (root1 == NULL and root2 == NULL)
        return true;

    // check if one node is false
    else if (root1 == NULL or root2 == NULL)
        return false;

    queue<node *> q1, q2;

    // enqueue roots
    q1.push(root1);
    q2.push(root2);

    int level = 0;
    int size;

    vector<int> v2;

    unordered_map<int, int> mp;

    while (!q1.empty() and !q2.empty()) {

        // check if no. of nodes are
        // not same at a given level
        if (q1.size() != q2.size())
            return false;

        size = q1.size();

        level++;

        v2.clear();
        mp.clear();

        while (size--) {

            node* temp1 = q1.front();
            node* temp2 = q2.front();

            // dequeue the nodes
            q1.pop();
            q2.pop();

            // check if value
            // exists in the map
            if (mp.find(temp1->data) == mp.end())
                mp[temp1->data] = 1;

            else
                mp[temp1->data]++;

            v2.push_back(temp2->data);

            // enqueue the child nodes
            if (temp1->left)
                q1.push(temp1->left);

            if (temp1->right)
                q1.push(temp1->right);

            if (temp2->left)
                q2.push(temp2->left);

            if (temp2->right)
                q2.push(temp2->right);
        }

        // Iterate through each node at a level
        // to check whether it exists or not.
        for (auto i : v2) {

            if (mp.find(i) == mp.end())
                return false;

            else {
                mp[i]--;

                if (mp[i] < 0)
                    return false;

                else if (mp[i] == 0)
                    mp.erase(i);
            }
        }

        // check if the key remain
        if (mp.size() != 0)
            return false;
    }
    return true;
}

/* function that allocates a new node with the
given data and NULL left and right pointers. */
node* newnode(int data)
{
    node* temp = new node;
    temp->data = data;
    temp->left = NULL;
    temp->right = NULL;

    return (temp);
}

/* Driver program*/

int main()
{
    // create tree
    struct node* n1 = newnode(1);
    n1->left = newnode(2);
    n1->right = newnode(3);
    n1->left->left = newnode(4);
    n1->left->right = newnode(5);
    n1->right->left = newnode(6);
    n1->left->right->left = newnode(7);
    n1->left->right->right = newnode(8);

    struct node* n2 = newnode(1);
    n2->left = newnode(3);
    n2->right = newnode(2);
    n2->right->left = newnode(4);
    n2->right->right = newnode(5);
    n2->left->right = newnode(6);
    n2->right->right->left = newnode(8);
    n2->right->right->right = newnode(7);

    if (isIsomorphic(n1, n2) == true)
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find two
// Binary Tree are Isomorphic or not
import java.util.ArrayList;
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// A binary tree node has data,
// pointer to left and right children
static class Node
{
  int data;
  Node left, right;
  public Node(int data)
  {
    this.data = data;
    this.left = this.right = null;
  }
};

// Function to return if tree
// are isomorphic or not
static boolean isIsomorphic(Node root1,
                            Node root2)
{
  // If Both roots are null
  // then tree is isomorphic
  if (root1 == null &&
      root2 == null)
    return true;

  // Check if one node
  // is false
  else if (root1 == null ||
           root2 == null)
    return false;

  Queue<Node> q1 =
        new LinkedList<>(),
              q2 = new LinkedList<>();

  // Enqueue roots
  q1.add(root1);
  q2.add(root2);

  int level = 0;
  int size;

  ArrayList<Integer> v2 =
            new ArrayList<>();
  HashMap<Integer,
          Integer> mp = new HashMap<>();

  while (!q1.isEmpty() &&
         !q2.isEmpty())
  {
    // check if no. of nodes are
    // not same at a given level
    if (q1.size() != q2.size())
      return false;

    size = q1.size();
    level++;
    v2.clear();
    mp.clear();

    while (size-- > 0)
    {
      // Dequeue the nodes
      Node temp1 = q1.poll();
      Node temp2 = q2.poll();

      // Check if value
      // exists in the map
      if (!mp.containsKey(temp1.data))
        mp.put(temp1.data, 1);
      else
        mp.put(temp1.data,
               mp.get(temp1.data) + 1);

      v2.add(temp2.data);

      // Enqueue the child nodes
      if (temp1.left != null)
        q1.add(temp1.left);

      if (temp1.right != null)
        q1.add(temp1.right);

      if (temp2.left != null)
        q2.add(temp2.left);

      if (temp2.right != null)
        q2.add(temp2.right);
    }

    // Iterate through each node
    // at a level to check whether
    // it exists or not.
    for (Integer i : v2)
    {
      if (!mp.containsKey(i))
        return false;
      else
      {
        mp.put(i, mp.get(i) - 1);

        if (mp.get(i) < 0)
          return false;
        else if (mp.get(i) == 0)
          mp.remove(i);
      }
    }

    // Check if the key remain
    if (mp.size() != 0)
      return false;
  }
  return true;
}

// Driver program
public static void main(String[] args)
{
  // Create tree
  Node n1 = new Node(1);
  n1.left = new Node(2);
  n1.right = new Node(3);
  n1.left.left = new Node(4);
  n1.left.right = new Node(5);
  n1.right.left = new Node(6);
  n1.left.right.left = new Node(7);
  n1.left.right.right = new Node(8);

  Node n2 = new Node(1);
  n2.left = new Node(3);
  n2.right = new Node(2);
  n2.right.left = new Node(4);
  n2.right.right = new Node(5);
  n2.left.right = new Node(6);
  n2.right.right.left = new Node(8);
  n2.right.right.right = new Node(7);

  if (isIsomorphic(n1, n2))
    System.out.println("Yes");
  else
    System.out.println("No");
}   
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find two
# Binary Tree are Isomorphic or not
from collections import deque

class node:

    def __init__(self, x):

        self.data = x
        self.left = None
        self.right = None

# Function to return if tree are
# isomorphic or not
def isIsomorphic(root1, root2):

    # If Both roots are null
    # then tree is isomorphic
    if (root1 == None and root2 == None):
        return True

    # Check if one node is false
    elif (root1 == None or root2 == None):
        return False

    q1 = deque()
    q2 = deque()

    # enqueue roots
    q1.append(root1)
    q2.append(root2)

    level = 0
    size = 0

    v1 = []
    m2 = {}

    while (len(q1) > 0 and len(q2) > 0):

        # Check if no. of nodes are
        # not same at a given level
        if (len(q1) != len(q2)):
            return False

        size = len(q1)
        level += 1

        v2 = []
        mp = {}

        while (size):
            temp1 = q1.popleft()
            temp2 = q2.popleft()

            # Check if value
            # exists in the map
            mp[temp1.data] = mp.get(temp1.data, 0) + 1

            v2.append(temp2.data)

            # enqueue the child nodes
            if (temp1.left):
                q1.append(temp1.left)

            if (temp1.right):
                q1.append(temp1.right)

            if (temp2.left):
                q2.append(temp2.left)

            if (temp2.right):
                q2.append(temp2.right)

            v1 = v2
            m2 = mp
            size -= 1

        # Iterate through each node at a level
        # to check whether it exists or not.
        for i in v1:

            if i in m2:
                return True
            else:
                m2[i] -= 1

                if (m2[i] < 0):
                    return False
                elif (m2[i] == 0):
                    del m2[i]

        # Check if the key remain
        if (len(m2) == 0):
            return False

    return True

# Driver code
if __name__ == '__main__':

    # Create tree
    n1 = node(1)
    n1.left = node(2)
    n1.right = node(3)
    n1.left.left = node(4)
    n1.left.right = node(5)
    n1.right.left = node(6)
    n1.left.right.left = node(7)
    n1.left.right.right = node(8)

    n2 = node(1)
    n2.left = node(3)
    n2.right = node(2)
    n2.right.left = node(4)
    n2.right.right = node(5)
    n2.left.right = node(6)
    n2.right.right.left = node(8)
    n2.right.right.right = node(7)

    if (isIsomorphic(n1, n2) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find two
// Binary Tree are Isomorphic or not
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// A binary tree node has data,
// pointer to left and right children
class Node
{
  public int data;
  public Node left, right;
  public Node(int data)
  {
    this.data = data;
    this.left = this.right = null;
  }
};

// Function to return if tree
// are isomorphic or not
static bool isIsomorphic(Node root1,
                            Node root2)
{
  // If Both roots are null
  // then tree is isomorphic
  if (root1 == null &&
      root2 == null)
    return true;

  // Check if one node
  // is false
  else if (root1 == null ||
           root2 == null)
    return false;

  Queue q1 = new Queue();
  Queue q2 = new Queue();

  //  roots
  q1.Enqueue(root1);
  q2.Enqueue(root2);

  int level = 0;
  int size;

  ArrayList v2 =  new ArrayList();
  Dictionary<int,int> mp = new Dictionary<int,int>();

  while (q1.Count != 0 &&  q2.Count != 0)
  {
    // check if no. of nodes are
    // not same at a given level
    if (q1.Count != q2.Count)
      return false;

    size = q1.Count;
    level++;
    v2.Clear();
    mp.Clear();

    while (size-- > 0)
    {
      // Dequeue the nodes
      Node temp1 = (Node)q1.Dequeue();
      Node temp2 = (Node)q2.Dequeue();

      // Check if value
      // exists in the map
      if (!mp.ContainsKey(temp1.data))
        mp[temp1.data] = 1;
      else
        mp[temp1.data]++;

      v2.Add(temp2.data);

      //  the child nodes
      if (temp1.left != null)
        q1.Enqueue(temp1.left);

      if (temp1.right != null)
        q1.Enqueue(temp1.right);

      if (temp2.left != null)
        q2.Enqueue(temp2.left);

      if (temp2.right != null)
        q2.Enqueue(temp2.right);
    }

    // Iterate through each node
    // at a level to check whether
    // it exists or not.
    foreach (int i in v2)
    {
      if (!mp.ContainsKey(i))
        return false;
      else
      {
        mp[i]--;

        if (mp[i] < 0)
          return false;
        else if (mp[i] == 0)
          mp.Remove(i);
      }
    }

    // Check if the key remain
    if (mp.Count != 0)
      return false;
  }
  return true;
}

// Driver program
public static void Main(string[] args)
{

  // Create tree
  Node n1 = new Node(1);
  n1.left = new Node(2);
  n1.right = new Node(3);
  n1.left.left = new Node(4);
  n1.left.right = new Node(5);
  n1.right.left = new Node(6);
  n1.left.right.left = new Node(7);
  n1.left.right.right = new Node(8);

  Node n2 = new Node(1);
  n2.left = new Node(3);
  n2.right = new Node(2);
  n2.right.left = new Node(4);
  n2.right.right = new Node(5);
  n2.left.right = new Node(6);
  n2.right.right.left = new Node(8);
  n2.right.right.right = new Node(7);

  if (isIsomorphic(n1, n2))
    Console.WriteLine("Yes");
  else
    Console.WriteLine("No");
}   
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to find two
// Binary Tree are Isomorphic or not

// A binary tree node has data,
// pointer to left and right children
class Node
{

    // Utility function to
    // create a new node
    constructor(key)
    {
        this.data = key;
        this.left = this.right = null;
    }
}

// Function to return if tree
// are isomorphic or not
function isIsomorphic(root1, root2)
{

    // If Both roots are null
    // then tree is isomorphic
    if (root1 == null &&
        root2 == null)
        return true;

    // Check if one node
    // is false
    else if (root1 == null ||
             root2 == null)
        return false;

    let q1 =[],
    q2 = [];

    // Enqueue roots
    q1.push(root1);
    q2.push(root2);

    let level = 0;
    let size;

    let v2 = [];
    let mp = new Map();

    while (q1.length != 0 &&
           q2.length != 0)
    {

        // Check if no. of nodes are
        // not same at a given level
        if (q1.length != q2.length)
            return false;

        size = q1.length;
        level++;
        v2 = [];

        while (size-- > 0)
        {

            // Dequeue the nodes
            let temp1 = q1.shift();
            let temp2 = q2.shift();

            // Check if value
            // exists in the map
            if (!mp.has(temp1.data))
                mp.set(temp1.data, 1);
            else
                mp.set(temp1.data,
                mp.get(temp1.data) + 1);

            v2.push(temp2.data);

            // Enqueue the child nodes
            if (temp1.left != null)
                q1.push(temp1.left);

            if (temp1.right != null)
                q1.push(temp1.right);

            if (temp2.left != null)
                q2.push(temp2.left);

            if (temp2.right != null)
                q2.push(temp2.right);
        }

        // Iterate through each node
        // at a level to check whether
        // it exists or not.
        for(let i = 0; i < v2.length; i++)
        {
            if (!mp.has(v2[i]))
                return false;
            else
            {
                mp.set(v2[i], mp.get(v2[i]) - 1);

                if (mp.get(v2[i]) < 0)
                    return false;
                else if (mp.get(v2[i]) == 0)
                    mp.delete(v2[i]);
            }
        }

        // Check if the key remain
        if (mp.size != 0)
            return false;
    }
    return true;
}

// Driver code

// Create tree
let n1 = new Node(1);
n1.left = new Node(2);
n1.right = new Node(3);
n1.left.left = new Node(4);
n1.left.right = new Node(5);
n1.right.left = new Node(6);
n1.left.right.left = new Node(7);
n1.left.right.right = new Node(8);

let n2 = new Node(1);
n2.left = new Node(3);
n2.right = new Node(2);
n2.right.left = new Node(4);
n2.right.right = new Node(5);
n2.left.right = new Node(6);
n2.right.right.left = new Node(8);
n2.right.right.right = new Node(7);

if (isIsomorphic(n1, n2))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)