# 打印从根到两个给定节点的两条路径的公共路径

> 原文:[https://www . geesforgeks . org/print-path-common-two-path-root-two-given-nodes/](https://www.geeksforgeeks.org/print-path-common-two-paths-root-two-given-nodes/)

给定具有不同节点的二叉树(没有两个节点具有相同的数据值)。问题是打印从根到两个给定节点 **n1** 和 **n2** 的两条路径的公共路径。如果任一节点不存在，则打印“无公共路径”。

示例:

```
Input :          1
               /   \
              2     3
             / \   /  \
            4   5  6   7
               /    \   
              8      9

          n1 = 4, n2 = 8

Output : 1->2
Path form root to n1:
1->2->4

Path form root to n2:
1->2->5->8

Common Path:
1->2
```

**进场:**以下步骤为:

1.  找到两个节点 **n1** 和 **n2** 的 **LCA** (最低共同祖先)。参见[本](https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/)。
2.  如果**生命周期评价**退出，则打印从根到生命周期评价的路径。参见[本](https://www.geeksforgeeks.org/print-path-root-given-node-binary-tree/)。否则打印“无公共路径”。

## C++

```
// C++ implementation to print the path common to the
// two paths from the root to the two given nodes
#include <bits/stdc++.h>

using namespace std;

// structure of a node of binary tree
struct Node
{
    int data;
    Node *left, *right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* getNode(int data)
{
    struct Node *newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// This function returns pointer to LCA of two given values n1 and n2.
// v1 is set as true by this function if n1 is found
// v2 is set as true by this function if n2 is found
struct Node *findLCAUtil(struct Node* root, int n1, int n2, bool &v1, bool &v2)
{
    // Base case
    if (root == NULL) return NULL;

    // If either n1 or n2 matches with root's data, report the presence
    // by setting v1 or v2 as true and return root (Note that if a key
    // is ancestor of other, then the ancestor key becomes LCA)
    if (root->data == n1)
    {
        v1 = true;
        return root;
    }
    if (root->data == n2)
    {
        v2 = true;
        return root;
    }

    // Look for nodes in left and right subtrees
    Node *left_lca  = findLCAUtil(root->left, n1, n2, v1, v2);
    Node *right_lca = findLCAUtil(root->right, n1, n2, v1, v2);

    // If both of the above calls return Non-NULL, then one node
    // is present in one subtree and other is present in other,
    // So this current node is the LCA
    if (left_lca && right_lca)  return root;

    // Otherwise check if left subtree or right subtree is LCA
    return (left_lca != NULL)? left_lca: right_lca;
}

// Returns true if key k is present in tree rooted with root
bool find(Node *root, int k)
{
    // Base Case
    if (root == NULL)
        return false;

    // If key k is present at root, or in left subtree
    // or right subtree, return true
    if (root->data == k || find(root->left, k) ||  find(root->right, k))
        return true;

    // Else return false
    return false;
}

// This function returns LCA of n1 and n2 only if both n1 and n2
// are present in tree, otherwise returns NULL
Node *findLCA(Node *root, int n1, int n2)
{
    // Initialize n1 and n2 as not visited
    bool v1 = false, v2 = false;

    // Find lca of n1 and n2
    Node *lca = findLCAUtil(root, n1, n2, v1, v2);

    // Return LCA only if both n1 and n2 are present in tree
    if (v1 && v2 || v1 && find(lca, n2) || v2 && find(lca, n1))
        return lca;

    // Else return NULL
    return NULL;
}

// function returns true if
// there is a path from root to
// the given node. It also populates
// 'arr' with the given path
bool hasPath(Node *root, vector<int>& arr, int x)
{
    // if root is NULL
    // there is no path
    if (!root)
        return false;

    // push the node's value in 'arr'
    arr.push_back(root->data);   

    // if it is the required node
    // return true
    if (root->data == x)   
        return true;

    // else check whether there    the required node lies in the
    // left subtree or right subtree of the current node
    if (hasPath(root->left, arr, x) ||
        hasPath(root->right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from 'arr'
    // and then return false;   
    arr.pop_back();
    return false;           
}

// function to print the path common
// to the two paths from the root
// to the two given nodes if the nodes
// lie in the binary tree
void printCommonPath(Node *root, int n1, int n2)
{
    // vector to store the common path
    vector<int> arr;

    // LCA of node n1 and n2
    Node *lca = findLCA(root, n1, n2);

    // if LCA of both n1 and n2 exists
    if (lca)
    {
        // then print the path from root to
        // LCA node
        if (hasPath(root, arr, lca->data))
        {
            for (int i=0; i<arr.size()-1; i++)   
                cout << arr[i] << "->";
            cout << arr[arr.size() - 1];   
        }   
    }

    // LCA is not present in the binary tree
    // either n1 or n2 or both are not present
    else
        cout << "No Common Path";
}

// Driver program to test above
int main()
{
    // binary tree formation
    struct Node *root = getNode(1);
    root->left = getNode(2);
    root->right = getNode(3);
    root->left->left = getNode(4);
    root->left->right = getNode(5);
    root->right->left = getNode(6);
    root->right->right = getNode(7);
    root->left->right->left = getNode(8);
    root->right->left->right = getNode(9);

    int n1 = 4, n2 = 8;
    printCommonPath(root, n1, n2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the path common to the 
// two paths from the root to the two given nodes
import java.util.ArrayList;
public class PrintCommonPath {

    // Initialize n1 and n2 as not visited
    static boolean v1 = false, v2 = false;

    // This function returns pointer to LCA of two given
    // values n1 and n2\. This function assumes that n1 and
    // n2 are present in Binary Tree
    static Node findLCAUtil(Node node, int n1, int n2)
    {
        // Base case
        if (node == null)
            return null;

        //Store result in temp, in case of key match so that we can search for other key also.
        Node temp=null;

        // If either n1 or n2 matches with root's key, report the presence
        // by setting v1 or v2 as true and return root (Note that if a key
        // is ancestor of other, then the ancestor key becomes LCA)
        if (node.data == n1)
        {
            v1 = true;
            temp = node;
        }
        if (node.data == n2)
        {
            v2 = true;
            temp = node;
        }

        // Look for keys in left and right subtrees
        Node left_lca = findLCAUtil(node.left, n1, n2);
        Node right_lca = findLCAUtil(node.right, n1, n2);

        if (temp != null)
            return temp;

        // If both of the above calls return Non-NULL, then one key
        // is present in once subtree and other is present in other,
        // So this node is the LCA
        if (left_lca != null && right_lca != null)
            return node;

        // Otherwise check if left subtree or right subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

    // Returns true if key k is present in tree rooted with root
    static boolean find(Node root, int k)
    {
        // Base Case
        if (root == null)
            return false;

        // If key k is present at root, or in left subtree 
        // or right subtree, return true
        if (root.data == k || find(root.left, k) ||  find(root.right, k))
            return true;

        // Else return false
        return false;
    }

    // This function returns LCA of n1 and n2 only if both n1 and n2 
    // are present in tree, otherwise returns null
    static Node findLCA(Node root, int n1, int n2)
    {
        // Find lca of n1 and n2
        Node lca = findLCAUtil(root, n1, n2);

        // Return LCA only if both n1 and n2 are present in tree
        if (v1 && v2 || v1 && find(lca, n2) || v2 && find(lca, n1))
            return lca;

        // Else return null
        return null;
    }

    // function returns true if 
    // there is a path from root to 
    // the given node. It also populates 
    // 'arr' with the given path
    static boolean hasPath(Node root, ArrayList<Integer> arr, int x)
    {
        // if root is null
        // there is no path
        if (root==null)
            return false;

        // push the node's value in 'arr'
        arr.add(root.data);    

        // if it is the required node
        // return true
        if (root.data == x)    
            return true;

        // else check whether there    the required node lies in the
        // left subtree or right subtree of the current node
        if (hasPath(root.left, arr, x) ||
            hasPath(root.right, arr, x))
            return true;

        // required node does not lie either in the 
        // left or right subtree of the current node
        // Thus, remove current node's value from 'arr'
        // and then return false;    
        arr.remove(arr.size()-1);
        return false;            
    }

    // function to print the path common
    // to the two paths from the root 
    // to the two given nodes if the nodes 
    // lie in the binary tree
    static void printCommonPath(Node root, int n1, int n2)
    {
        // ArrayList to store the common path
        ArrayList<Integer> arr=new ArrayList<>();

        // LCA of node n1 and n2
        Node lca = findLCA(root, n1, n2);

        // if LCA of both n1 and n2 exists
        if (lca!=null)
        {  
            // then print the path from root to
            // LCA node
            if (hasPath(root, arr, lca.data))
            {
                for (int i=0; i<arr.size()-1; i++)    
                    System.out.print(arr.get(i)+"->");
                    System.out.print(arr.get(arr.size() - 1));    
            }    
        }

        // LCA is not present in the binary tree 
        // either n1 or n2 or both are not present
        else
            System.out.print("No Common Path");
    }

    public static void main(String args[])
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.right.left = new Node(8);
        root.right.left.right = new Node(9);

        int n1 = 4, n2 = 8;
        printCommonPath(root, n1, n2);
        }
}

/* Class containing left and right child of current
 node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python implementation to print the path common to the
# two paths from the root to the two given nodes

# structure of a node of binary tree
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# This function returns pointer to LCA of two given values n1 and n2.
# v1 is set as True by this function if n1 is found
# v2 is set as True by this function if n2 is found
def findLCAUtil(root: Node, n1: int, n2: int) -> Node:
    global v1, v2

    # Base case
    if (root is None):
        return None

    # If either n1 or n2 matches with root's data, report the presence
    # by setting v1 or v2 as True and return root (Note that if a key
    # is ancestor of other, then the ancestor key becomes LCA)
    if (root.data == n1):
        v1 = True
        return root

    if (root.data == n2):

        v2 = True
        return root

    # Look for nodes in left and right subtrees
    left_lca = findLCAUtil(root.left, n1, n2)
    right_lca = findLCAUtil(root.right, n1, n2)

    # If both of the above calls return Non-None, then one node
    # is present in one subtree and other is present in other,
    # So this current node is the LCA
    if (left_lca and right_lca):
        return root

    # Otherwise check if left subtree or right subtree is LCA
    return left_lca if (left_lca != None) else right_lca

# Returns True if key k is present in tree rooted with root
def find(root: Node, k: int) -> bool:

    # Base Case
    if (root == None):
        return False

    # If key k is present at root, or in left subtree
    # or right subtree, return True
    if (root.data == k or find(root.left, k) or find(root.right, k)):
        return True

    # Else return False
    return False

# This function returns LCA of n1 and n2 only if both n1 and n2
# are present in tree, otherwise returns None
def findLCA(root: Node, n1: int, n2: int) -> Node:
    global v1, v2

    # Initialize n1 and n2 as not visited
    v1 = False
    v2 = False

    # Find lca of n1 and n2
    lca = findLCAUtil(root, n1, n2)

    # Return LCA only if both n1 and n2 are present in tree
    if (v1 and v2 or v1 and find(lca, n2) or v2 and find(lca, n1)):
        return lca

    # Else return None
    return None

# function returns True if
# there is a path from root to
# the given node. It also populates
# 'arr' with the given path
def hasPath(root: Node, arr: list, x: int) -> Node:

    # if root is None
    # there is no path
    if (root is None):
        return False

    # push the node's value in 'arr'
    arr.append(root.data)

    # if it is the required node
    # return True
    if (root.data == x):
        return True

    # else check whether there    the required node lies in the
    # left subtree or right subtree of the current node
    if (hasPath(root.left, arr, x) or hasPath(root.right, arr, x)):
        return True

    # required node does not lie either in the
    # left or right subtree of the current node
    # Thus, remove current node's value from 'arr'
    # and then return False;
    arr.pop()
    return False

# function to print the path common
# to the two paths from the root
# to the two given nodes if the nodes
# lie in the binary tree
def printCommonPath(root: Node, n1: int, n2: int):

    # vector to store the common path
    arr = []

    # LCA of node n1 and n2
    lca = findLCA(root, n1, n2)

    # if LCA of both n1 and n2 exists
    if (lca):

        # then print the path from root to
        # LCA node
        if (hasPath(root, arr, lca.data)):

            for i in range(len(arr) - 1):
                print(arr[i], end="->")
            print(arr[-1])

    # LCA is not present in the binary tree
    # either n1 or n2 or both are not present
    else:
        print("No Common Path")

# Driver Code
if __name__ == "__main__":

    v1 = 0
    v2 = 0

    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.left.right.left = Node(8)
    root.right.left.right = Node(9)

    n1 = 4
    n2 = 8
    printCommonPath(root, n1, n2)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to print the path common to the
// two paths from the root to the two given nodes
using System;
using System.Collections.Generic;

public class PrintCommonPath
{

    // Initialize n1 and n2 as not visited
    static Boolean v1 = false, v2 = false;

    // This function returns pointer to LCA of two given
    // values n1 and n2\. This function assumes that n1 and
    // n2 are present in Binary Tree
    static Node findLCAUtil(Node node, int n1, int n2)
    {
        // Base case
        if (node == null)
            return null;

        //Store result in temp, in case of key
        // match so that we can search for other key also.
        Node temp=null;

        // If either n1 or n2 matches with root's key, report the presence
        // by setting v1 or v2 as true and return root (Note that if a key
        // is ancestor of other, then the ancestor key becomes LCA)
        if (node.data == n1)
        {
            v1 = true;
            temp = node;
        }
        if (node.data == n2)
        {
            v2 = true;
            temp = node;
        }

        // Look for keys in left and right subtrees
        Node left_lca = findLCAUtil(node.left, n1, n2);
        Node right_lca = findLCAUtil(node.right, n1, n2);

        if (temp != null)
            return temp;

        // If both of the above calls return Non-NULL, then one key
        // is present in once subtree and other is present in other,
        // So this node is the LCA
        if (left_lca != null && right_lca != null)
            return node;

        // Otherwise check if left subtree or right subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

    // Returns true if key k is present in tree rooted with root
    static Boolean find(Node root, int k)
    {
        // Base Case
        if (root == null)
            return false;

        // If key k is present at root, or in left subtree
        // or right subtree, return true
        if (root.data == k || find(root.left, k) || find(root.right, k))
            return true;

        // Else return false
        return false;
    }

    // This function returns LCA of n1 and n2 only if both n1 and n2
    // are present in tree, otherwise returns null
    static Node findLCA(Node root, int n1, int n2)
    {
        // Find lca of n1 and n2
        Node lca = findLCAUtil(root, n1, n2);

        // Return LCA only if both n1 and n2 are present in tree
        if (v1 && v2 || v1 && find(lca, n2) || v2 && find(lca, n1))
            return lca;

        // Else return null
        return null;
    }

    // function returns true if
    // there is a path from root to
    // the given node. It also populates
    // 'arr' with the given path
    static Boolean hasPath(Node root, List<int> arr, int x)
    {
        // if root is null
        // there is no path
        if (root == null)
            return false;

        // push the node's value in 'arr'
        arr.Add(root.data);    

        // if it is the required node
        // return true
        if (root.data == x)    
            return true;

        // else check whether there the required node lies in the
        // left subtree or right subtree of the current node
        if (hasPath(root.left, arr, x) ||
            hasPath(root.right, arr, x))
            return true;

        // required node does not lie either in the
        // left or right subtree of the current node
        // Thus, remove current node's value from 'arr'
        // and then return false;    
        arr.Remove(arr.Count-1);
        return false;            
    }

    // function to print the path common
    // to the two paths from the root
    // to the two given nodes if the nodes
    // lie in the binary tree
    static void printCommonPath(Node root, int n1, int n2)
    {
        // ArrayList to store the common path
        List<int> arr = new List<int>();

        // LCA of node n1 and n2
        Node lca = findLCA(root, n1, n2);

        // if LCA of both n1 and n2 exists
        if (lca!=null)
        {
            // then print the path from root to
            // LCA node
            if (hasPath(root, arr, lca.data))
            {
                for (int i=0; i<arr.Count-1; i++)    
                    Console.Write(arr[i]+"->");
                    Console.Write(arr[arr.Count - 1]);    
            }    
        }

        // LCA is not present in the binary tree
        // either n1 or n2 or both are not present
        else
            Console.Write("No Common Path");
    }

    // Driver code
    public static void Main(String []args)
    {
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.left.right.left = new Node(8);
        root.right.left.right = new Node(9);

        int n1 = 4, n2 = 8;
        printCommonPath(root, n1, n2);
        }
}

/* Class containing left and right child of current
node and key value*/
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to print the path
// common to the two paths from the root to the
// two given nodes
class Node
{
    constructor(d)
    {
        this.data = d;
        this.left = this.right = null;
    }
}

let v1 = false;
let v2 = false;

// This function returns pointer to LCA of two given
// values n1 and n2\. This function assumes that n1 and
// n2 are present in Binary Tree
function findLCAUtil(node, n1, n2)
{

    // Base case
    if (node == null)
        return null;

    // If either n1 or n2 matches with root's key,
    // report the presence by setting v1 or v2 as
    // true and return root (Note that if a key
    // is ancestor of other, then the ancestor
    // key becomes LCA)
    if (node.data == n1)
    {
        v1 = true;
        return node;
    }
    if (node.data == n2)
    {
        v2 = true;
        return node;
    }

    // Look for keys in left and right subtrees
    let left_lca = findLCAUtil(node.left, n1, n2);
    let right_lca = findLCAUtil(node.right, n1, n2);

    // If both of the above calls return Non-NULL,
    // then one key is present in once subtree and
    // other is present in other, So this node is the LCA
    if (left_lca != null && right_lca != null)
        return node;

    // Otherwise check if left subtree or right
    // subtree is LCA
    return (left_lca != null) ? left_lca : right_lca;
}

function find(root, k)
{

    // Base Case
    if (root == null)
        return false;

    // If key k is present at root, or in left subtree
    // or right subtree, return true
    if ((root.data == k) || find(root.left, k) ||
                            find(root.right, k))
        return true;

    // Else return false
    return false;
}

// This function returns LCA of n1 and n2 only
// if both n1 and n2 are present in tree,
// otherwise returns null
function findLCA(root, n1, n2)
{

    // Find lca of n1 and n2
    let lca = findLCAUtil(root, n1, n2);

    // Return LCA only if both n1 and n2
    // are present in tree
    if ((v1 && v2) || (v1 && find(lca, n2)) ||
                      (v2 && find(lca, n1)))
        return lca;

    // Else return null
    return null;
}

// Function returns true if
// there is a path from root to
// the given node. It also populates
// 'arr' with the given path
function hasPath(root, arr, x)
{

    // If root is null
    // there is no path
    if (root == null)
        return false;

    // Push the node's value in 'arr'
    arr.push(root.data);   

    // If it is the required node
    // return true
    if (root.data == x)   
        return true;

    // Else check whether the required node lies in the
    // left subtree or right subtree of the current node
    if (hasPath(root.left, arr, x) ||
        hasPath(root.right, arr, x))
        return true;

    // Required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from 'arr'
    // and then return false;   
    arr.pop();
    return false;          
}

// Function to print the path common
// to the two paths from the root
// to the two given nodes if the nodes
// lie in the binary tree
function printCommonPath(root, n1, n2)
{

    // ArrayList to store the common path
    let arr = [];

    // LCA of node n1 and n2
    let lca = findLCA(root, n1, n2);

    // If LCA of both n1 and n2 exists
    if (lca != null)
    { 

        // Then print the path from root to
        // LCA node
        if (hasPath(root, arr, lca.data))
        {
            for(let i = 0; i < arr.length - 1; i++)   
            {    document.write(arr[i] + "->");
                document.write(arr[arr.length - 1]);   
            }
        }   
    }

    // LCA is not present in the binary tree
    // either n1 or n2 or both are not present
    else
    {
        document.write("No Common Path");
    }
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);
root.left.right.left = new Node(8);
root.right.left.right = new Node(9);

let n1 = 4, n2 = 8;
printCommonPath(root, n1, n2);

// This code is contributed by rag2127

</script>
```

**输出:**

```
1->2
```

**时间复杂度:** O(n)，其中 n 为二叉树中的节点数。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。