# 二叉树的仰视图

> 原文:[https://www.geeksforgeeks.org/bottom-view-binary-tree/](https://www.geeksforgeeks.org/bottom-view-binary-tree/)

给定一个二叉树，我们需要从左到右打印底部视图。如果 x 是水平距离的最底部节点，则输出中有一个节点 x。节点 x 的左子节点的水平距离等于 x 减 1 的水平距离，右子节点的水平距离等于 x 加 1 的水平距离。

**示例:**

```
                      20
                    /    \
                  8       22
                /   \      \
              5      3      25
                    / \      
                  10    14
```

对于上面的树，输出应该是 5，10，3，14，25。
如果距离根的水平距离有多个最底部的节点，则在级别遍历中打印后面的节点。例如，在下图中，3 和 4 都是水平距离为 0 的最底部节点，我们需要打印 4。

```

                      20
                    /    \
                  8       22
                /   \    /   \
              5      3 4     25
                    / \      
                  10    14
```

对于上面的树，输出应该是 5，10，4，14，25。

**方法 1–使用队列**
以下是打印二叉树底视图的步骤。
1。我们将树节点放在队列中，进行级别顺序遍历。
2。从根节点的水平距离(hd) 0 开始，继续添加左子节点到队列，水平距离为 hd-1，右子节点为 hd+1。
3。此外，使用存储按键排序的键值对的树形图。
4。每次，我们遇到一个新的水平距离或一个现有的水平距离，把水平距离的节点数据作为关键。第一次它将添加到地图中，下次它将替换该值。这将确保该水平距离的最底部元素出现在地图中，如果您从下方看到树，您将看到该元素。

下面是上面的实现:

## C++

```
// C++ Program to print Bottom View of Binary Tree
#include<bits/stdc++.h>
using namespace std;

// Tree node class
struct Node
{
    int data; //data of the node
    int hd; //horizontal distance of the node
    Node *left, *right; //left and right references

    // Constructor of tree node
    Node(int key)
    {
        data = key;
        hd = INT_MAX;
        left = right = NULL;
    }
};

// Method that prints the bottom view.
void bottomView(Node *root)
{
    if (root == NULL)
        return;

    // Initialize a variable 'hd' with 0
    // for the root element.
    int hd = 0;

    // TreeMap which stores key value pair
    // sorted on key value
    map<int, int> m;

    // Queue to store tree nodes in level
    // order traversal
    queue<Node *> q;

    // Assign initialized horizontal distance
    // value to root node and add it to the queue.
    root->hd = hd;
    q.push(root);  // In STL, push() is used enqueue an item

    // Loop until the queue is empty (standard
    // level order loop)
    while (!q.empty())
    {
        Node *temp = q.front();
        q.pop();   // In STL, pop() is used dequeue an item

        // Extract the horizontal distance value
        // from the dequeued tree node.
        hd = temp->hd;

        // Put the dequeued tree node to TreeMap
        // having key as horizontal distance. Every
        // time we find a node having same horizontal
        // distance we need to replace the data in
        // the map.
        m[hd] = temp->data;

        // If the dequeued node has a left child, add
        // it to the queue with a horizontal distance hd-1.
        if (temp->left != NULL)
        {
            temp->left->hd = hd-1;
            q.push(temp->left);
        }

        // If the dequeued node has a right child, add
        // it to the queue with a horizontal distance
        // hd+1.
        if (temp->right != NULL)
        {
            temp->right->hd = hd+1;
            q.push(temp->right);
        }
    }

    // Traverse the map elements using the iterator.
    for (auto i = m.begin(); i != m.end(); ++i)
        cout << i->second << " ";
}

// Driver Code
int main()
{
    Node *root = new Node(20);
    root->left = new Node(8);
    root->right = new Node(22);
    root->left->left = new Node(5);
    root->left->right = new Node(3);
    root->right->left = new Node(4);
    root->right->right = new Node(25);
    root->left->right->left = new Node(10);
    root->left->right->right = new Node(14);
    cout << "Bottom view of the given binary tree :\n"
    bottomView(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print Bottom View of Binary Tree
import java.util.*;
import java.util.Map.Entry;

// Tree node class
class Node
{
    int data; //data of the node
    int hd; //horizontal distance of the node
    Node left, right; //left and right references

    // Constructor of tree node
    public Node(int key)
    {
        data = key;
        hd = Integer.MAX_VALUE;
        left = right = null;
    }
}

//Tree class
class Tree
{
    Node root; //root node of tree

    // Default constructor
    public Tree() {}

    // Parameterized tree constructor
    public Tree(Node node)
    {
        root = node;
    }

    // Method that prints the bottom view.
    public void bottomView()
    {
        if (root == null)
            return;

        // Initialize a variable 'hd' with 0 for the root element.
        int hd = 0;

        // TreeMap which stores key value pair sorted on key value
        Map<Integer, Integer> map = new TreeMap<>();

         // Queue to store tree nodes in level order traversal
        Queue<Node> queue = new LinkedList<Node>();

        // Assign initialized horizontal distance value to root
        // node and add it to the queue.
        root.hd = hd;
        queue.add(root);

        // Loop until the queue is empty (standard level order loop)
        while (!queue.isEmpty())
        {
            Node temp = queue.remove();

            // Extract the horizontal distance value from the
            // dequeued tree node.
            hd = temp.hd;

            // Put the dequeued tree node to TreeMap having key
            // as horizontal distance. Every time we find a node
            // having same horizontal distance we need to replace
            // the data in the map.
            map.put(hd, temp.data);

            // If the dequeued node has a left child add it to the
            // queue with a horizontal distance hd-1.
            if (temp.left != null)
            {
                temp.left.hd = hd-1;
                queue.add(temp.left);
            }
            // If the dequeued node has a right child add it to the
            // queue with a horizontal distance hd+1.
            if (temp.right != null)
            {
                temp.right.hd = hd+1;
                queue.add(temp.right);
            }
        }

        // Extract the entries of map into a set to traverse
        // an iterator over that.
        Set<Entry<Integer, Integer>> set = map.entrySet();

        // Make an iterator
        Iterator<Entry<Integer, Integer>> iterator = set.iterator();

        // Traverse the map elements using the iterator.
        while (iterator.hasNext())
        {
            Map.Entry<Integer, Integer> me = iterator.next();
            System.out.print(me.getValue()+" ");
        }
    }
}

// Main driver class
public class BottomView
{
    public static void main(String[] args)
    {
        Node root = new Node(20);
        root.left = new Node(8);
        root.right = new Node(22);
        root.left.left = new Node(5);
        root.left.right = new Node(3);
        root.right.left = new Node(4);
        root.right.right = new Node(25);
        root.left.right.left = new Node(10);
        root.left.right.right = new Node(14);
        Tree tree = new Tree(root);
        System.out.println("Bottom view of the given binary tree:");
        tree.bottomView();
    }
}
```

## 蟒蛇 3

```
# Python3 program to print Bottom
# View of Binary Tree

# Tree node class
class Node:

    def __init__(self, key):

        self.data = key
        self.hd = 1000000
        self.left = None
        self.right = None

# Method that prints the bottom view.
def bottomView(root):

    if (root == None):
        return

    # Initialize a variable 'hd' with 0
    # for the root element.
    hd = 0

    # TreeMap which stores key value pair
    # sorted on key value
    m = dict()

    # Queue to store tree nodes in level
    # order traversal
    q = []

    # Assign initialized horizontal distance
    # value to root node and add it to the queue.
    root.hd = hd

    # In STL, append() is used enqueue an item
    q.append(root) 

    # Loop until the queue is empty (standard
    # level order loop)
    while (len(q) != 0):
        temp = q[0]

        # In STL, pop() is used dequeue an item
        q.pop(0) 

        # Extract the horizontal distance value
        # from the dequeued tree node.
        hd = temp.hd

        # Put the dequeued tree node to TreeMap
        # having key as horizontal distance. Every
        # time we find a node having same horizontal
        # distance we need to replace the data in
        # the map.
        m[hd] = temp.data

        # If the dequeued node has a left child, add
        # it to the queue with a horizontal distance hd-1.
        if (temp.left != None):
            temp.left.hd = hd - 1
            q.append(temp.left)

        # If the dequeued node has a right child, add
        # it to the queue with a horizontal distance
        # hd+1.
        if (temp.right != None):
            temp.right.hd = hd + 1
            q.append(temp.right)

    # Traverse the map elements using the iterator.
    for i in sorted(m.keys()):
        print(m[i], end = ' ')

# Driver Code
if __name__=='__main__':

    root = Node(20)
    root.left = Node(8)
    root.right = Node(22)
    root.left.left = Node(5)
    root.left.right = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(25)
    root.left.right.left = Node(10)
    root.left.right.right = Node(14)

    print("Bottom view of the given binary tree :")

    bottomView(root)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print Bottom View of Binary Tree
using System;
using System.Collections;
using System.Collections.Generic;

// Tree node class
class Node
{

    // Data of the node
    public int data;

    // Horizontal distance of the node
    public int hd;

    // left and right references
    public Node left, right;

    // Constructor of tree node
    public Node(int key)
    {
        data = key;
        hd = 1000000;
        left = right = null;
    }
}

// Tree class
class Tree
{

    // Root node of tree
    Node root;

    // Default constructor
    public Tree(){}

    // Parameterized tree constructor
    public Tree(Node node)
    {
        root = node;
    }

    // Method that prints the bottom view.
    public void bottomView()
    {
        if (root == null)
            return;

        // Initialize a variable 'hd' with
        // 0 for the root element.
        int hd = 0;

        // TreeMap which stores key value
        // pair sorted on key value
        SortedDictionary<int,
                         int> map = new SortedDictionary<int,
                                                         int>();

        // Queue to store tree nodes in level order
        // traversal
        Queue queue = new Queue();

        // Assign initialized horizontal distance
        // value to root node and add it to the queue.
        root.hd = hd;
        queue.Enqueue(root);

        // Loop until the queue is empty
        // (standard level order loop)
        while (queue.Count != 0)
        {
            Node temp = (Node) queue.Dequeue();

            // Extract the horizontal distance value
            // from the dequeued tree node.
            hd = temp.hd;

            // Put the dequeued tree node to TreeMap
            // having key as horizontal distance.
            // Every time we find a node having same
            // horizontal distance we need to replace
            // the data in the map.
            map[hd] = temp.data;

            // If the dequeued node has a left child
            // add it to the queue with a horizontal
            // distance hd-1.
            if (temp.left != null)
            {
                temp.left.hd = hd - 1;
                queue.Enqueue(temp.left);
            }

            // If the dequeued node has a right
            // child add it to the queue with a
            // horizontal distance hd+1.
            if (temp.right != null)
            {
                temp.right.hd = hd + 1;
                queue.Enqueue(temp.right);
            }
        }

        foreach(int i in map.Values)
        {
            Console.Write(i + " ");
        }
    }
}

public class BottomView{

// Driver code
public static void Main(string[] args)
{
    Node root = new Node(20);
    root.left = new Node(8);
    root.right = new Node(22);
    root.left.left = new Node(5);
    root.left.right = new Node(3);
    root.right.left = new Node(4);
    root.right.right = new Node(25);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(14);
    Tree tree = new Tree(root);

    Console.WriteLine("Bottom view of the " +
                      "given binary tree:");

    tree.bottomView();
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

      // JavaScript program to print Bottom View of Binary Tree
      // Tree node class
      class Node {
        // Constructor of tree node
        constructor(key) {
          this.data = key; // Data of the node
          this.hd = 1000000; // Horizontal distance of the node
          this.left = null; // left and right references
          this.right = null;
        }
      }

      // Tree class
      class Tree {
        // Parameterized tree constructor
        constructor(node) {
          // Root node of tree
          this.root = node;
        }

        // Method that prints the bottom view.
        bottomView() {
          if (this.root == null) return;

          // Initialize a variable 'hd' with
          // 0 for the root element.
          var hd = 0;

          // TreeMap which stores key value
          // pair sorted on key value
          var map = {};

          // Queue to store tree nodes in level order
          // traversal
          var queue = [];

          // Assign initialized horizontal distance
          // value to root node and add it to the queue.
          this.root.hd = hd;
          queue.push(this.root);

          // Loop until the queue is empty
          // (standard level order loop)
          while (queue.length != 0) {
            var temp = queue.shift();

            // Extract the horizontal distance value
            // from the dequeued tree node.
            hd = temp.hd;

            // Put the dequeued tree node to TreeMap
            // having key as horizontal distance.
            // Every time we find a node having same
            // horizontal distance we need to replace
            // the data in the map.
            map[hd] = temp.data;

            // If the dequeued node has a left child
            // add it to the queue with a horizontal
            // distance hd-1.
            if (temp.left != null) {
              temp.left.hd = hd - 1;
              queue.push(temp.left);
            }

            // If the dequeued node has a right
            // child add it to the queue with a
            // horizontal distance hd+1.
            if (temp.right != null) {
              temp.right.hd = hd + 1;
              queue.push(temp.right);
            }
          }

          for (const [key, value] of Object.entries(map).sort(
            (a, b) => a[0] - b[0]
          )) {
            document.write(value + " ");
          }
        }
      }

      // Driver code
      var root = new Node(20);
      root.left = new Node(8);
      root.right = new Node(22);
      root.left.left = new Node(5);
      root.left.right = new Node(3);
      root.right.left = new Node(4);
      root.right.right = new Node(25);
      root.left.right.left = new Node(10);
      root.left.right.right = new Node(14);
      var tree = new Tree(root);

      document.write("Bottom view of the " + "given binary tree:<br>");

      tree.bottomView();

</script>
```

**输出:**

```
Bottom view of the given binary tree:
5 10 4 14 25
```

**方法 2-使用 HashMap()**
此方法由 [Ekta Goel](https://auth.geeksforgeeks.org/user/Ekta%20Goel/articles) 贡献。

**方法:**
创建一个类似的地图，地图中 key 是水平距离，value 是一对(a，b)，其中 a 是节点的值，b 是节点的高度。执行树的预先排序遍历。如果水平距离为 h 的当前节点是我们看到的第一个节点，请将其插入地图。否则，将该节点与地图中的现有节点进行比较，如果新节点的高度更高，则在地图中进行更新。

下面是上面的实现:

## C++

```
// C++ Program to print Bottom View of Binary Tree
#include <bits/stdc++.h>
#include <map>
using namespace std;

// Tree node class
struct Node
{
    // data of the node
    int data;

    // horizontal distance of the node
    int hd;

    //left and right references
    Node * left, * right;

    // Constructor of tree node
    Node(int key)
    {
        data = key;
        hd = INT_MAX;
        left = right = NULL;
    }
};

void printBottomViewUtil(Node * root, int curr, int hd, map <int, pair <int, int>> & m)
{
    // Base case
    if (root == NULL)
        return;

    // If node for a particular
    // horizontal distance is not
    // present, add to the map.
    if (m.find(hd) == m.end())
    {
        m[hd] = make_pair(root -> data, curr);
    }
    // Compare height for already
    // present node at similar horizontal
    // distance
    else
    {
        pair < int, int > p = m[hd];
        if (p.second <= curr)
        {
            m[hd].second = curr;
            m[hd].first = root -> data;
        }
    }

    // Recur for left subtree
    printBottomViewUtil(root -> left, curr + 1, hd - 1, m);

    // Recur for right subtree
    printBottomViewUtil(root -> right, curr + 1, hd + 1, m);
}

void printBottomView(Node * root)
{

    // Map to store Horizontal Distance,
    // Height and Data.
    map < int, pair < int, int > > m;

    printBottomViewUtil(root, 0, 0, m);

     // Prints the values stored by printBottomViewUtil()
    map < int, pair < int, int > > ::iterator it;
    for (it = m.begin(); it != m.end(); ++it)
    {
        pair < int, int > p = it -> second;
        cout << p.first << " ";
    }
}

int main()
{
    Node * root = new Node(20);
    root -> left = new Node(8);
    root -> right = new Node(22);
    root -> left -> left = new Node(5);
    root -> left -> right = new Node(3);
    root -> right -> left = new Node(4);
    root -> right -> right = new Node(25);
    root -> left -> right -> left = new Node(10);
    root -> left -> right -> right = new Node(14);
    cout << "Bottom view of the given binary tree :\n";
    printBottomView(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Bottom View of Binary Tree
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Tree node class
static class Node
{

    // Data of the node
    int data;

    // Horizontal distance of the node
    int hd;

    // Left and right references
    Node left, right;

    // Constructor of tree node
    public Node(int key)
    {
        data = key;
        hd = Integer.MAX_VALUE;
        left = right = null;
    }
}

static void printBottomViewUtil(Node root, int curr, int hd,
                                TreeMap<Integer, int[]> m)
{

    // Base case
    if (root == null)
        return;

    // If node for a particular
    // horizontal distance is not
    // present, add to the map.
    if (!m.containsKey(hd))
    {
        m.put(hd, new int[]{ root.data, curr });
    }

    // Compare height for already
    // present node at similar horizontal
    // distance
    else
    {
        int[] p = m.get(hd);
        if (p[1] <= curr)
        {
            p[1] = curr;
            p[0] = root.data;
        }
        m.put(hd, p);
    }

    // Recur for left subtree
    printBottomViewUtil(root.left, curr + 1,
                        hd - 1, m);

    // Recur for right subtree
    printBottomViewUtil(root.right, curr + 1,
                        hd + 1, m);
}

static void printBottomView(Node root)
{

    // Map to store Horizontal Distance,
    // Height and Data.
    TreeMap<Integer, int[]> m = new TreeMap<>();

    printBottomViewUtil(root, 0, 0, m);

    // Prints the values stored by printBottomViewUtil()
    for(int val[] : m.values())
    {
        System.out.print(val[0] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    Node root = new Node(20);
    root.left = new Node(8);
    root.right = new Node(22);
    root.left.left = new Node(5);
    root.left.right = new Node(3);
    root.right.left = new Node(4);
    root.right.right = new Node(25);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(14);

    System.out.println(
        "Bottom view of the given binary tree:");

    printBottomView(root);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program to print Bottom
# View of Binary Tree
class Node:

    def __init__(self, key = None,
                      left = None,
                     right = None):

        self.data = key
        self.left = left
        self.right = right

def printBottomView(root):

      # Create a dictionary where
    # key -> relative horizontal distance
    # of the node from root node and
    # value -> pair containing node's
    # value and its level
    d = dict()

    printBottomViewUtil(root, d, 0, 0)

    # Traverse the dictionary in sorted
    # order of their keys and print
    # the bottom view
    for i in sorted(d.keys()):
        print(d[i][0], end = " ")

def printBottomViewUtil(root, d, hd, level):

      # Base case
    if root is None:
        return

    # If current level is more than or equal
    # to maximum level seen so far for the
    # same horizontal distance or horizontal
    # distance is seen for the first time,
    # update the dictionary
    if hd in d:
        if level >= d[hd][1]:
            d[hd] = [root.data, level]
    else:
        d[hd] = [root.data, level]

    # recur for left subtree by decreasing
    # horizontal distance and increasing
    # level by 1
    printBottomViewUtil(root.left, d, hd - 1,
                                   level + 1)

    # recur for right subtree by increasing
    # horizontal distance and increasing
    # level by 1
    printBottomViewUtil(root.right, d, hd + 1,
                                    level + 1)

# Driver Code   
if __name__ == '__main__':

    root = Node(20)
    root.left = Node(8)
    root.right = Node(22)
    root.left.left = Node(5)
    root.left.right = Node(3)
    root.right.left = Node(4)
    root.right.right = Node(25)
    root.left.right.left = Node(10)
    root.left.right.right = Node(14)

    print("Bottom view of the given binary tree :")

    printBottomView(root)

# This code is contributed by tusharroy
```