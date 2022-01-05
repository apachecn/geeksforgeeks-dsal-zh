# 打印二叉树中从根到给定节点的路径

> 原文:[https://www . geesforgeks . org/print-path-root-given-node-二叉树/](https://www.geeksforgeeks.org/print-path-root-given-node-binary-tree/)

给定具有不同节点的二叉树(没有两个节点具有相同的数据值)。问题是打印从根到给定节点 **x** 的路径。如果节点 **x** 不存在，则打印“无路径”。

**示例:**

```
Input :          1
               /   \
              2     3
             / \   /  \
            4   5  6   7

               x = 5

Output : 1->2->5
```

**方法:**创建一个递归函数，遍历二叉树中的不同路径，找到需要的节点 **x** 。如果节点 **x** 存在，则它返回真，并在某个数组**arr【】**中累积路径节点。否则返回假。
以下是遍历过程中的情况:

1.  如果**根=空**，返回假。
2.  将根的数据推入 **arr[]** 。
3.  如果**根的数据= x** ，返回真。
4.  如果节点 **x** 出现在根的左或右子树中，返回 true。
5.  否则从 **arr[]** 中移除根的数据值，并返回 false。

可以从其他函数访问该递归函数，以检查节点 **x** 是否存在，如果存在，则可以从 **arr[]** 访问路径节点。您可以全局定义 **arr[]** 或将它的引用传递给递归函数。

## C++

```
// C++ implementation to print the path from root
// to a given node in a binary tree
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
    struct Node *newNode = new Node;
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Returns true if there is a path from root
// to the given node. It also populates
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

    // else check whether the required node lies
    // in the left subtree or right subtree of
    // the current node
    if (hasPath(root->left, arr, x) ||
        hasPath(root->right, arr, x))
        return true;

    // required node does not lie either in the
    // left or right subtree of the current node
    // Thus, remove current node's value from
    // 'arr'and then return false   
    arr.pop_back();
    return false;           
}

// function to print the path from root to the
// given node if the node lies in the binary tree
void printPath(Node *root, int x)
{
    // vector to store the path
    vector<int> arr;

    // if required node 'x' is present
    // then print the path
    if (hasPath(root, arr, x))
    {
        for (int i=0; i<arr.size()-1; i++)   
            cout << arr[i] << "->";
        cout << arr[arr.size() - 1];   
    }

    // 'x' is not present in the binary tree
    else
        cout << "No Path";
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

    int x = 5;
    printPath(root, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print the path from root
// to a given node in a binary tree
import java.util.ArrayList;
public class PrintPath {

    // Returns true if there is a path from root
    // to the given node. It also populates 
    // 'arr' with the given path
    public static boolean hasPath(Node root, ArrayList<Integer> arr, int x)
    {
        // if root is NULL
        // there is no path
        if (root==null)
            return false;

        // push the node's value in 'arr'
        arr.add(root.data);    

        // if it is the required node
        // return true
        if (root.data == x)    
            return true;

        // else check whether the required node lies
        // in the left subtree or right subtree of 
        // the current node
        if (hasPath(root.left, arr, x) ||
            hasPath(root.right, arr, x))
            return true;

        // required node does not lie either in the 
        // left or right subtree of the current node
        // Thus, remove current node's value from 
        // 'arr'and then return false    
        arr.remove(arr.size()-1);
        return false;            
    }

    // function to print the path from root to the
    // given node if the node lies in the binary tree
    public static void printPath(Node root, int x)
    {
        // ArrayList to store the path
        ArrayList<Integer> arr=new ArrayList<>();

        // if required node 'x' is present
        // then print the path
        if (hasPath(root, arr, x))
        {
            for (int i=0; i<arr.size()-1; i++)    
                System.out.print(arr.get(i)+"->");
            System.out.print(arr.get(arr.size() - 1));   
        }

        // 'x' is not present in the binary tree 
        else
            System.out.print("No Path");
    }

    public static void main(String args[]) {
        Node root=new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        int x=5;
        printPath(root, x);
    }
}

// A node of binary tree
class Node
{
    int data;
    Node left, right;
    Node(int data)
    {
        this.data=data;
        left=right=null;
    }
};
//This code is contributed by Gaurav Tiwari
```

## 蟒蛇 3

```
# Python3 implementation to print the path from
# root to a given node in a binary tree

# Helper Class that allocates a new node
# with the given data and None left and
# right pointers.
class getNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Returns true if there is a path from
# root to the given node. It also
# populates 'arr' with the given path
def hasPath(root, arr, x):

    # if root is None there is no path
    if (not root):
        return False

    # push the node's value in 'arr'
    arr.append(root.data)    

    # if it is the required node
    # return true
    if (root.data == x):    
        return True

    # else check whether the required node
    # lies in the left subtree or right
    # subtree of the current node
    if (hasPath(root.left, arr, x) or
        hasPath(root.right, arr, x)):
        return True

    # required node does not lie either in
    # the left or right subtree of the current
    # node. Thus, remove current node's value 
    # from 'arr'and then return false    
    arr.pop(-1)
    return False

# function to print the path from root to
# the given node if the node lies in
# the binary tree
def printPath(root, x):

    # vector to store the path
    arr = []

    # if required node 'x' is present
    # then print the path
    if (hasPath(root, arr, x)):
        for i in range(len(arr) - 1):
            print(arr[i], end = "->")
        print(arr[len(arr) - 1])

    # 'x' is not present in the
    # binary tree
    else:
        print("No Path")

# Driver Code
if __name__ == '__main__':

    # binary tree formation
    root = getNode(1)
    root.left = getNode(2)
    root.right = getNode(3)
    root.left.left = getNode(4)
    root.left.right = getNode(5)
    root.right.left = getNode(6)
    root.right.right = getNode(7)

    x = 5
    printPath(root, x)

# This code is contributed by PranchalK
```

## C#

```
// C# implementation to print the path from root
// to a given node in a binary tree
using System;
using System.Collections;
using System.Collections.Generic;

class PrintPath
{

// A node of binary tree
public class Node
{
    public int data;
    public Node left, right;
    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

    // Returns true if there is a path from root
    // to the given node. It also populates
    // 'arr' with the given path
    public static Boolean hasPath(Node root,
                        List<int> arr, int x)
    {
        // if root is NULL
        // there is no path
        if (root == null)
            return false;

        // push the node's value in 'arr'
        arr.Add(root.data);    

        // if it is the required node
        // return true
        if (root.data == x)    
            return true;

        // else check whether the required node lies
        // in the left subtree or right subtree of
        // the current node
        if (hasPath(root.left, arr, x) ||
            hasPath(root.right, arr, x))
            return true;

        // required node does not lie either in the
        // left or right subtree of the current node
        // Thus, remove current node's value from
        // 'arr'and then return false    
        arr.RemoveAt(arr.Count - 1);
        return false;            
    }

    // function to print the path from root to the
    // given node if the node lies in the binary tree
    public static void printPath(Node root, int x)
    {
        // List to store the path
        List<int> arr = new List<int>();

        // if required node 'x' is present
        // then print the path
        if (hasPath(root, arr, x))
        {
            for (int i = 0; i < arr.Count - 1; i++)    
                Console.Write(arr[i]+"->");
            Console.Write(arr[arr.Count - 1]);
        }

        // 'x' is not present in the binary tree
        else
            Console.Write("No Path");
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
        int x=5;

        printPath(root, x);
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// Javascript implementation to print
// the path from root to a given node
// in a binary tree
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

// Returns true if there is a path from root
// to the given node. It also populates 
// 'arr' with the given path
function hasPath(root, arr, x)
{

    // If root is NULL
    // there is no path
    if (root == null)
        return false;

    // Push the node's value in 'arr'
    arr.push(root.data);    

    // If it is the required node
    // return true
    if (root.data == x)    
        return true;

    // Else check whether the required node lies
    // in the left subtree or right subtree of 
    // the current node
    if (hasPath(root.left, arr, x) ||
        hasPath(root.right, arr, x))
        return true;

    // Required node does not lie either in the 
    // left or right subtree of the current node
    // Thus, remove current node's value from 
    // 'arr'and then return false    
    arr.pop();
    return false;            
}

// Function to print the path from root to the
// given node if the node lies in the binary tree
function printPath(root, x)
{

    // ArrayList to store the path
    let arr = [];

    // If required node 'x' is present
    // then print the path
    if (hasPath(root, arr, x))
    {
        for(let i = 0; i < arr.length - 1; i++)    
            document.write(arr[i] + "->");
        document.write(arr[arr.length - 1]);   
    }

    // 'x' is not present in the binary tree 
    else
        document.write("No Path");
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);

let x = 5;
printPath(root, x);

// This code is contributed by divyeshrabadiya07

</script>
```

**输出:**

```
1->2->5
```

**时间复杂度:**最坏情况下 O(n)，其中 n 为二叉树中的节点数。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。