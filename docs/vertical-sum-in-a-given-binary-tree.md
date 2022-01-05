# 给定二叉树中的垂直和|集合 1

> 原文:[https://www . geesforgeks . org/垂直给定二叉树求和/](https://www.geeksforgeeks.org/vertical-sum-in-a-given-binary-tree/)

给定一棵二叉树，求在同一条垂直线上的节点的垂直和。通过不同的垂直线打印所有总和。
**例:**

```
      1
    /   \
  2      3
 / \    / \
4   5  6   7
```

树有 5 条竖线
竖线-1 只有一个节点 4 = >竖线和为 4
竖线-2:只有一个节点 2= >竖线和为 2
竖线-3:有三个节点:1，5，6 = >竖线和为 1+5+6 = 12
竖线-4:只有一个节点 3 = >竖线和为 3
竖线-5:只有一个节点 7 = >

我们需要检查所有节点到根的水平距离。如果两个节点具有相同的水平距离，则它们位于同一条垂直线上。高清的想法很简单。根的 HD 为 0，右边缘(连接到右子树的边缘)被认为是+1 水平距离，左边缘被认为是-1 水平距离。例如，在上面的树中，节点 4 的高清为-2，节点 2 的高清为-1，节点 5 和 6 的高清为 0，节点 7 的高清为+2。
我们可以对给定的二叉树进行有序遍历。遍历树时，我们可以递归计算 HDs。我们最初将水平距离作为根的 0。对于左子树，我们将水平距离作为根的水平距离减 1。对于右子树，我们将水平距离作为根的水平距离加 1。
下面是相同的 Java 实现。HashMap 用于存储不同水平距离的垂直和。感谢 Nages 提出这个方法。

## C++

```
// C++ program to find Vertical Sum in
// a given Binary Tree
#include<bits/stdc++.h>
using namespace std;

struct Node
{
    int data;
    struct Node *left, *right;
};

// A utility function to create a new
// Binary Tree node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Traverses the tree in in-order form and
// populates a hashMap that contains the
// vertical sum
void verticalSumUtil(Node *node, int hd,
                     map<int, int> &Map)
{
    // Base case
    if (node == NULL) return;

    // Recur for left subtree
    verticalSumUtil(node->left, hd-1, Map);

    // Add val of current node to
    // map entry of corresponding hd
    Map[hd] += node->data;

    // Recur for right subtree
    verticalSumUtil(node->right, hd+1, Map);
}

// Function to find vertical sum
void verticalSum(Node *root)
{
    // a map to store sum of nodes for each 
    // horizontal distance
    map < int, int> Map;
    map < int, int> :: iterator it;

    // populate the map
    verticalSumUtil(root, 0, Map);

    // Prints the values stored by VerticalSumUtil()
    for (it = Map.begin(); it != Map.end(); ++it)
    {
        cout << it->first << ": "
             << it->second << endl;
    }
}

// Driver program to test above functions
int main()
{
    // Create binary tree as shown in above figure
    Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);
    root->right->right->right = newNode(9);

    cout << "Following are the values of vertical"
            " sums with the positions of the "
            "columns with respect to root\n";
    verticalSum(root);

    return 0;
}
// This code is contributed by Aditi Sharma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.TreeMap;

// Class for a tree node
class TreeNode {

    // data members
    private int key;
    private TreeNode left;
    private TreeNode right;

    // Accessor methods
    public int key()        { return key; }
    public TreeNode left()  { return left; }
    public TreeNode right() { return right; }

    // Constructor
    public TreeNode(int key)
   { this.key = key; left = null; right = null; }

    // Methods to set left and right subtrees
    public void setLeft(TreeNode left)   { this.left = left; }
    public void setRight(TreeNode right) { this.right = right; }
}

// Class for a Binary Tree
class Tree {

    private TreeNode root;

    // Constructors
    public Tree() { root = null; }
    public Tree(TreeNode n) { root = n; }

    // Method to be called by the consumer classes 
    // like Main class
    public void VerticalSumMain() { VerticalSum(root); }

    // A wrapper over VerticalSumUtil()
    private void VerticalSum(TreeNode root) {

        // base case
        if (root == null) { return; }

        // Creates an empty TreeMap hM
        TreeMap<Integer, Integer> hM =
                   new TreeMap<Integer, Integer>();

        // Calls the VerticalSumUtil() to store the 
        // vertical sum values in hM
        VerticalSumUtil(root, 0, hM);

        // Prints the values stored by VerticalSumUtil()
        if (hM != null) {
            System.out.println(hM.entrySet());
        }
    }

    // Traverses the tree in in-order form and builds
    // a hashMap hM that contains the vertical sum
    private void VerticalSumUtil(TreeNode root, int hD,
                         TreeMap<Integer, Integer> hM) {

        // base case
        if (root == null) {  return; }

        // Store the values in hM for left subtree
        VerticalSumUtil(root.left(), hD - 1, hM);

        // Update vertical sum for hD of this node
        int prevSum = (hM.get(hD) == null) ? 0 : hM.get(hD);
        hM.put(hD, prevSum + root.key());

        // Store the values in hM for right subtree
        VerticalSumUtil(root.right(), hD + 1, hM);
    }
}

// Driver class to test the verticalSum methods
public class Main {

    public static void main(String[] args) {
        /* Create the following Binary Tree
              1
            /    \
          2        3
         / \      / \
        4   5    6   7

        */
        TreeNode root = new TreeNode(1);
        root.setLeft(new TreeNode(2));
        root.setRight(new TreeNode(3));
        root.left().setLeft(new TreeNode(4));
        root.left().setRight(new TreeNode(5));
        root.right().setLeft(new TreeNode(6));
        root.right().setRight(new TreeNode(7));
        Tree t = new Tree(root);

        System.out.println("Following are the values of" + 
                           " vertical sums with the positions" +
                        " of the columns with respect to root ");
        t.VerticalSumMain();
    }
}
```

## 蟒蛇 3

```
# Python3 program to find Vertical Sum in 
# a given Binary Tree 

# Node definition 
class newNode: 

    def __init__(self, data): 

        self.left = None
        self.right = None
        self.data = data 

# Traverses the tree in in-order form and 
# populates a hashMap that contains the 
# vertical sum 
def verticalSumUtil(root, hd, Map): 

    # Base case 
    if(root == None):
        return

    # Recur for left subtree 
    verticalSumUtil(root.left, hd - 1, Map) 

    # Add val of current node to 
    # map entry of corresponding hd 
    if(hd in Map.keys()):
        Map[hd] = Map[hd] + root.data
    else:
        Map[hd] = root.data

    # Recur for right subtree 
    verticalSumUtil(root.right, hd + 1, Map)

# Function to find vertical_sum 
def verticalSum(root): 

    # a dictionary to store sum of
    # nodes for each horizontal distance 
    Map = {}

    # Populate the dictionary
    verticalSumUtil(root, 0, Map); 

    # Prints the values stored
    # by VerticalSumUtil() 
    for i,j in Map.items():
        print(i, "=", j, end = ", ")

# Driver Code 
if __name__ == "__main__": 

    '''      Create the following Binary Tree
              1
            /    \
          2        3
         / \      / \
        4   5    6   7 
    '''
    root = newNode(1) 
    root.left = newNode(2) 
    root.right = newNode(3) 
    root.left.left = newNode(4) 
    root.left.right = newNode(5) 
    root.right.left = newNode(6) 
    root.right.right = newNode(7)

    print("Following are the values of vertical "
          "sums with the positions of the "
          "columns with respect to root")

    verticalSum(root)

# This code is contributed by vipinyadav15799
```

## C#

```
// C# program to find Vertical Sum in
// a given Binary Tree
using System;
using System.Collections.Generic;

// Class for a tree node
class TreeNode 
{

    // data members
    public int key;
    public TreeNode left;
    public TreeNode right;

    // Accessor methods
    public int Key()
    { 
        return key; 
    }
    public TreeNode Left() { return left; }
    public TreeNode Right() { return right; }

    // Constructor
    public TreeNode(int key)
    { 
        this.key = key; 
        left = null;
        right = null; 
    }

    // Methods to set left and right subtrees
    public void setLeft(TreeNode left) 
    { 
        this.left = left; 
    }
    public void setRight(TreeNode right) 
    { 
        this.right = right; 
    }
}

// Class for a Binary Tree
class Tree 
{
    private TreeNode root;

    // Constructors
    public Tree() { root = null; }
    public Tree(TreeNode n) { root = n; }

    // Method to be called by the consumer classes 
    // like Main class
    public void VerticalSumMain() 
    { 
        VerticalSum(root); 
    }

    // A wrapper over VerticalSumUtil()
    private void VerticalSum(TreeNode root)
    {

        // base case
        if (root == null) { return; }

        // Creates an empty hashMap hM
        Dictionary<int, 
                   int> hM = new Dictionary<int, 
                                            int>();

        // Calls the VerticalSumUtil() to store the 
        // vertical sum values in hM
        VerticalSumUtil(root, 0, hM);

        // Prints the values stored by VerticalSumUtil()
        if (hM != null) 
        {
            Console.Write("[");
            foreach(KeyValuePair<int, int> entry in hM)
            {
                Console.Write(entry.Key + " = " + 
                              entry.Value + ", ");
            }
            Console.Write("]");
        }
    }

    // Traverses the tree in in-order form and builds
    // a hashMap hM that contains the vertical sum
    private void VerticalSumUtil(TreeNode root, int hD,
                                 Dictionary<int, int> hM)
    {

        // base case
        if (root == null) { return; }

        // Store the values in hM for left subtree
        VerticalSumUtil(root.Left(), hD - 1, hM);

        // Update vertical sum for hD of this node
        int prevSum = 0;
        if(hM.ContainsKey(hD))
        {
            prevSum = hM[hD];
            hM[hD] = prevSum + root.Key();
        }
        else
            hM.Add(hD, prevSum + root.Key());

        // Store the values in hM for right subtree
        VerticalSumUtil(root.Right(), hD + 1, hM);
    }
}

// Driver Code
public class GFG
{
    public static void Main(String[] args) 
    {
        /* Create the following Binary Tree
            1
            / \
        2     3
        / \     / \
        4 5 6 7

        */
        TreeNode root = new TreeNode(1);
        root.setLeft(new TreeNode(2));
        root.setRight(new TreeNode(3));
        root.Left().setLeft(new TreeNode(4));
        root.Left().setRight(new TreeNode(5));
        root.Right().setLeft(new TreeNode(6));
        root.Right().setRight(new TreeNode(7));
        Tree t = new Tree(root);

        Console.WriteLine("Following are the values of" + 
                          " vertical sums with the positions" +
                          " of the columns with respect to root ");
        t.VerticalSumMain();
    }
}

// This code is contributed by Rajput-Ji
```

**Output**

```
Following are the values of vertical sums with the positions of the columns with respect to root
-2: 4
-1: 2
0: 12
1: 11
2: 7
3: 9

```

[二叉树中的垂直和|集合 2(空间优化)](https://www.geeksforgeeks.org/vertical-sum-in-binary-tree-set-space-optimized/)
时间复杂度:O(nlogn)
如果发现有不正确的地方，或者想分享更多以上讨论话题的信息，请写评论。