# 检查二叉树顶视图中的节点是否形成回文编号

> 原文:[https://www . geeksforgeeks . org/check-if-nodes-in-top-view-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a](https://www.geeksforgeeks.org/check-if-nodes-in-top-view-of-a-binary-tree-forms-a-palindrome-number-or-not/)

给定由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，任务是检查二叉树的[顶视图中的节点是否形成](https://www.geeksforgeeks.org/print-nodes-top-view-binary-tree/)[回文号](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not/?ref=rp)。如果发现是回文，则打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:**
> **5
> /\
> 3
> /\ \
> 6 2 6
> **输出:**是
> **说明:**
> 顶视图中的节点为{6，3，5，3，6}。因此，生成的数字(= 63536)是一个回文。**
> 
> ****输入:**
> **1
> /\
> 4 2
> **输出:**否****

******方法:**要解决给定的问题，思路是使用本文[中讨论的方法](https://www.geeksforgeeks.org/print-nodes-top-view-binary-tree/)找到给定的**二叉树**的俯视图，并将其存储在数组中，比如 **arr[]** 。现在，[检查数组 **arr[]** 是否回文](https://www.geeksforgeeks.org/program-to-check-if-an-array-is-palindrome-or-not/)。如果发现为真，则打印**是**否则打印**否**。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of the node
// of a Binary Tree
struct Node {
    Node* left;
    Node* right;
    int hd;
    int data;
};

// Function to create a new node
Node* newNode(int key)
{
    Node* node = new Node();
    node->left = node->right = NULL;
    node->data = key;
    return node;
}

// Function to check if array
// is a palindrome or not
void isPalindrome(vector<int> arr)
{
    // Store the size of arr[]
    int n = arr.size();

    // Initialise flag to 0
    int flag = 0;

    // Iterate till half the array length
    for (int i = 0; i <= n / 2
                    && n != 0;
         i++) {

        // If the first and last
        // array elements are different
        if (arr[i] != arr[n - i - 1]) {
            flag = 1;
            break;
        }
    }

    // If flag is set, then print No
    if (flag == 1)
        cout << "No";
    else
        cout << "Yes";
}

// Function to find the top view
// of the given Binary Tree
void topview(Node* root)
{
    // Base Case
    if (root == NULL)
        return;

    // Stores the nodes while
    // performing tree traversal
    queue<Node*> q;

    map<int, int> m;

    int hd = 0;
    root->hd = hd;

    // Push node and horizontal
    // distance into the queue
    q.push(root);

    while (q.size()) {

        hd = root->hd;

        if (m.count(hd) == 0)
            m[hd] = root->data;

        // If root's left child exists
        if (root->left) {
            root->left->hd = hd - 1;
            q.push(root->left);
        }

        // If root's right child exists
        if (root->right) {
            root->right->hd = hd + 1;
            q.push(root->right);
        }
        q.pop();
        root = q.front();
    }

    // Store the top view in a vector
    vector<int> v;

    // Traverse the map
    for (auto i = m.begin();
         i != m.end(); i++) {

        // Insert the element in v
        v.push_back(i->second);
    }

    // Function call to check if
    // vector v is palindromic or not
    isPalindrome(v);
}

// Driver Code
int main()
{
    // Binary Tree Formation
    Node* root = newNode(5);
    root->left = newNode(3);
    root->right = newNode(3);
    root->left->left = newNode(6);
    root->left->right = newNode(2);
    root->right->right = newNode(6);

    topview(root);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

// Structure of the node
// of a Binary Tree
static class Node
{
    Node left;
    Node right;
    int hd;
    int data;
};

// Function to create a new node
static Node newNode(int key)
{
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
}

// Function to check if array
// is a palindrome or not
static void isPalindrome(Vector<Integer> arr)
{

    // Store the size of arr[]
    int n = arr.size();

    // Initialise flag to 0
    int flag = 0;

    // Iterate till half the array length
    for(int i = 0; i <= n / 2 && n != 0; i++)
    {

        // If the first and last
        // array elements are different
        if (arr.get(i) != arr.get(n - i - 1))
        {
            flag = 1;
            break;
        }
    }

    // If flag is set, then print No
    if (flag == 1)
        System.out.print("No");
    else
        System.out.print("Yes");
}

// Function to find the top view
// of the given Binary Tree
static void topview(Node root)
{

    // Base Case
    if (root == null)
        return;

    // Stores the nodes while
    // performing tree traversal
    Queue<Node> q = new LinkedList<>();

    HashMap<Integer, Integer> m = new HashMap<>();

    int hd = 0;
    root.hd = hd;

    // Push node and horizontal
    // distance into the queue
    q.add(root);

    while (q.size() > 0)
    {
        hd = root.hd;

        if (m.containsKey(hd) && m.get(hd) == 0)
            m.put(hd, root.data);

        // If root's left child exists
        if (root.left != null)
        {
            root.left.hd = hd - 1;
            q.add(root.left);
        }

        // If root's right child exists
        if (root.right != null)
        {
            root.right.hd = hd + 1;
            q.add(root.right);
        }
        q.remove();
        root = q.peek();
    }

    // Store the top view in a vector
    Vector<Integer> v = new Vector<Integer>();

    // Traverse the map
    for(Map.Entry<Integer,Integer> i : m.entrySet())
    {

        // Insert the element in v
        v.add(i.getValue());
    }

    // Function call to check if
    // vector v is palindromic or not
    isPalindrome(v);
}

// Driver Code
public static void main(String[] args)
{

    // Binary Tree Formation
    Node root = newNode(5);
    root.left = newNode(3);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.left.right = newNode(2);
    root.right.right = newNode(6);

    topview(root);
}
}

// This code is contributed by shikhasingrajput**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Structure of the node
# of a Binary Tree
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None
        self.hd = 0

# Function to check if array
# is a palindrome or not
def isPalindrome(arr):

    # Store the size of arr[]
    n = len(arr)

    # Initialise flag to 0
    flag = 0

    # Iterate till half the array length
    i = 0
    while i <= n // 2 and n != 0:

        # If the first and last
        # array elements are different
        if (arr[i] != arr[n - i - 1]):
            flag = 1
            break
        i += 1

    # If flag is set, then print No
    if (flag == 1):
        print("No")
    else:
        print("Yes")

# Function to find the top view
# of the given Binary Tree
def topview(root):

    # Base case
    if(root == None) :
        return
    q = []
    m = dict()
    hd = 0
    root.hd = hd

    # push node and horizontal
    # distance to queue
    q.append(root)
    while(len(q)) :
        root = q[0]
        hd = root.hd

        # count function returns 1 if the
        # container contains an element
        # whose key is equivalent to hd,
        # or returns zero otherwise.
        if hd not in m:
            m[hd] = root.data
        if(root.left) :        
            root.left.hd = hd - 1
            q.append(root.left)

        if(root.right):        
            root.right.hd = hd + 1
            q.append(root.right)

        q.pop(0)

    v = []

    # Traverse the map
    for i in sorted(m):

        # Insert the element in v
        v.append(m[i])

    # Function call to check if
    # vector v is palindromic or not

    isPalindrome(v)

# Driver Code

# Binary Tree Formation
root = newNode(5)
root.left = newNode(3)
root.right = newNode(3)
root.left.left = newNode(6)
root.left.right = newNode(2)
root.right.right = newNode(6)

topview(root)

# This code is contributed by rohitsingh07052.**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

  // Structure of the node
  // of a Binary Tree
  class Node
  {
    public Node left;
    public Node right;
    public int hd;
    public int data;
  };

  // Function to create a new node
  static Node newNode(int key)
  {
    Node node = new Node();
    node.left = node.right = null;
    node.data = key;
    return node;
  }

  // Function to check if array
  // is a palindrome or not
  static void isPalindrome(List<int> arr)
  {

    // Store the size of []arr
    int n = arr.Count;

    // Initialise flag to 0
    int flag = 0;

    // Iterate till half the array length
    for(int i = 0; i <= n / 2 && n != 0; i++)
    {

      // If the first and last
      // array elements are different
      if (arr[i] != arr[n - i - 1])
      {
        flag = 1;
        break;
      }
    }

    // If flag is set, then print No
    if (flag == 1)
      Console.Write("No");
    else
      Console.Write("Yes");
  }

  // Function to find the top view
  // of the given Binary Tree
  static void topview(Node root)
  {

    // Base Case
    if (root == null)
      return;

    // Stores the nodes while
    // performing tree traversal
    Queue<Node> q = new Queue<Node>();

    Dictionary<int, int> m = new Dictionary<int, int>();

    int hd = 0;
    root.hd = hd;

    // Push node and horizontal
    // distance into the queue
    q.Enqueue(root);

    while (q.Count > 0)
    {
      hd = root.hd;

      if (m.ContainsKey(hd) && m[hd] == 0)
        m[hd] = root.data;

      // If root's left child exists
      if (root.left != null)
      {
        root.left.hd = hd - 1;
        q.Enqueue(root.left);
      }

      // If root's right child exists
      if (root.right != null)
      {
        root.right.hd = hd + 1;
        q.Enqueue(root.right);
      }

      root = q.Peek();
      q.Dequeue();
    }

    // Store the top view in a vector
    List<int> v = new List<int>();

    // Traverse the map
    foreach(KeyValuePair<int,int> i in m)
    {

      // Insert the element in v
      v.Add(i.Value);
    }

    // Function call to check if
    // vector v is palindromic or not
    isPalindrome(v);
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Binary Tree Formation
    Node root = newNode(5);
    root.left = newNode(3);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.left.right = newNode(2);
    root.right.right = newNode(6);

    topview(root);
  }
}

// This code is contributed by 29AjayKumar**
```

## ****java 描述语言****

```
**<script>

    // JavaScript program for the above approach

    class Node
    {
        constructor(key) {
           this.left = null;
           this.right = null;
           this.data = key;
        }
    }

    // Function to create a new node
    function newNode(key)
    {
        let node = new Node(key);
        return node;
    }

    // Function to check if array
    // is a palindrome or not
    function isPalindrome(arr)
    {

        // Store the size of arr[]
        let n = arr.length;

        // Initialise flag to 0
        let flag = 0;

        // Iterate till half the array length
        for(let i = 0; i <= parseInt(n / 2, 10) && n != 0; i++)
        {

            // If the first and last
            // array elements are different
            if (arr[i] != arr[n - i - 1])
            {
                flag = 1;
                break;
            }
        }

        // If flag is set, then print No
        if (flag == 1)
            document.write("No");
        else
            document.write("Yes");
    }

    // Function to find the top view
    // of the given Binary Tree
    function topview(root)
    {

        // Base Case
        if (root == null)
            return;

        // Stores the nodes while
        // performing tree traversal
        let q = [];

        let m = new Map();

        let hd = 0;
        root.hd = hd;

        // Push node and horizontal
        // distance into the queue
        q.push(root);

        while (q.length > 0)
        {
            hd = root.hd;

            if (m.has(hd) && m.get(hd) == 0)
                m.set(hd, root.data);

            // If root's left child exists
            if (root.left != null)
            {
                root.left.hd = hd - 1;
                q.push(root.left);
            }

            // If root's right child exists
            if (root.right != null)
            {
                root.right.hd = hd + 1;
                q.push(root.right);
            }
            q.shift();
            root = q[0];
        }

        // Store the top view in a vector
        let v = [];

        // Traverse the map
        m.forEach((values,keys)=>{

            // Insert the element in v
            v.push(values);
        })

        // Function call to check if
        // vector v is palindromic or not
        isPalindrome(v);
    }

    // Binary Tree Formation
    let root = newNode(5);
    root.left = newNode(3);
    root.right = newNode(3);
    root.left.left = newNode(6);
    root.left.right = newNode(2);
    root.right.right = newNode(6);

    topview(root);

</script>**
```

******Output:** 

```
Yes
```**** 

******时间复杂度:O(N)**
**辅助空间:O(N)******