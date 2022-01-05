# 用右边最少最大的元素替换每个元素

> 原文:[https://www . geeksforgeeks . org/用右边最少的元素替换每个元素/](https://www.geeksforgeeks.org/replace-every-element-with-the-least-greater-element-on-its-right/)

给定一个整数数组，用数组中右边最少的元素替换每个元素。如果右侧没有更大的元素，将其替换为-1。

示例:

```
Input: [8, 58, 71, 18, 31, 32, 63, 92, 
         43, 3, 91, 93, 25, 80, 28]
Output: [18, 63, 80, 25, 32, 43, 80, 93, 
         80, 25, 93, -1, 28, -1, -1]
```

一个简单的方法是运行两个循环。外部循环将从左到右逐一挑选数组元素。内部循环将在右侧找到比拾取元素大的最小元素。最后，外部循环将用内部循环找到的元素替换拾取的元素。该方法的时间复杂度为 O(n <sup>2</sup> )。

一个棘手的解决方案是使用二分搜索法树。我们开始从右向左扫描数组，并将每个元素插入到 BST 中。对于每个插入的元素，我们用它在 BST 中的有序后继替换它。如果插入的元素是目前为止的最大值(即它的后续元素不存在)，我们用-1 替换它。

下面是上述思路的实现–

## c++

```
// C++ program to replace every element with the
// least greater element on its right
#include <bits/stdc++.h>
using namespace std;

// A binary Tree node
struct Node {
    int data;
    Node *left, *right;
};

// A utility function to create a new BST node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;

    return temp;
}

/* A utility function to insert a new node with
   given data in BST and find its successor */
Node* insert(Node* node, int data, Node*& succ)
{

    /* If the tree is empty, return a new node */
    if (node == NULL)
        return node = newNode(data);

    // If key is smaller than root's key, go to left
    // subtree and set successor as current node
    if (data < node->data) {
        succ = node;
        node->left = insert(node->left, data, succ);
    }

    // go to right subtree
    else if (data > node->data)
        node->right = insert(node->right, data, succ);
    return node;
}

// Function to replace every element with the
// least greater element on its right
void replace(int arr[], int n)
{
    Node* root = NULL;

    // start from right to left
    for (int i = n - 1; i >= 0; i--) {
        Node* succ = NULL;

        // insert current element into BST and
        // find its inorder successor
        root = insert(root, arr[i], succ);

        // replace element by its inorder
        // successor in BST
        if (succ)
            arr[i] = succ->data;
        else // No inorder successor
            arr[i] = -1;
    }
}

// Driver Program to test above functions
int main()
{
    int arr[] = { 8,  58, 71, 18, 31, 32, 63, 92,
                  43, 3,  91, 93, 25, 80, 28 };
    int n = sizeof(arr) / sizeof(arr[0]);

    replace(arr, n);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    return 0;
}
```

## Java

```
// Java program to replace every element with
// the least greater element on its right
import java.io.*;

class BinarySearchTree{

// A binary Tree node
class Node
{
    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

// Root of BST
static Node root;
static Node succ;

// Constructor
BinarySearchTree()
{
    root = null;
    succ = null;
}

// A utility function to insert a new node with
// given data in BST and find its successor
Node insert(Node node, int data)
{

    // If the tree is empty, return a new node
    if (node == null)
    {
        node = new Node(data);
    }

    // If key is smaller than root's key,
    // go to left subtree and set successor
    // as current node
    if (data < node.data)
    {
        succ = node;
        node.left = insert(node.left, data);
    }

    // Go to right subtree
    else if (data > node.data)
        node.right = insert(node.right, data);

    return node;
}

// Function to replace every element with the
// least greater element on its right
static void replace(int arr[], int n)
{
    BinarySearchTree tree = new BinarySearchTree();

    // start from right to left
    for(int i = n - 1; i >= 0; i--)
    {
        succ = null;

        // Insert current element into BST and
        // find its inorder successor
        root = tree.insert(root, arr[i]);

        // Replace element by its inorder
        // successor in BST
        if (succ != null)
            arr[i] = succ.data;

        // No inorder successor
        else
            arr[i] = -1;
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = new int[] { 8, 58, 71, 18, 31,
                            32, 63, 92, 43, 3,
                            91, 93, 25, 80, 28 };
    int n = arr.length;

    replace(arr, n);

    for(int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// The code is contributed by Tushar Bansal
```

## python 3

```
# Python3 program to replace every element
# with the least greater element on its right

# A binary Tree node
class Node:

    def __init__(self, d):

        self.data = d
        self.left = None
        self.right = None

# A utility function to insert a new node with
# given data in BST and find its successor
def insert(node, data):

    global succ

    # If the tree is empty, return a new node
    root = node

    if (node == None):
        return Node(data)

    # If key is smaller than root's key, go to left
    # subtree and set successor as current node
    if (data < node.data):

        #print("1")
        succ = node
        root.left = insert(node.left, data)

    # Go to right subtree
    elif (data > node.data):
        root.right = insert(node.right, data)

    return root

# Function to replace every element with the
# least greater element on its right
def replace(arr, n):

    global succ
    root = None

    # Start from right to left
    for i in range(n - 1, -1, -1):
        succ = None

        # Insert current element into BST and
        # find its inorder successor
        root = insert(root, arr[i])

        # Replace element by its inorder
        # successor in BST
        if (succ):
            arr[i] = succ.data

        # No inorder successor
        else:  
            arr[i] = -1

    return arr

# Driver code
if __name__ == '__main__':

    arr = [ 8, 58, 71, 18, 31, 32, 63,
            92, 43, 3, 91, 93, 25, 80, 28 ]
    n = len(arr)
    succ = None

    arr = replace(arr, n)

    print(*arr)

# This code is contributed by mohit kumar 29
```

T19】c#

```
// C# program to replace every element with
// the least greater element on its right
using System;

class BinarySearchTree{

// A binary Tree node
public class Node
{
    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

// Root of BST
public static Node root;
public static Node succ;

// Constructor
public BinarySearchTree()
{
    root = null;
    succ = null;
}

// A utility function to insert a new node with
// given data in BST and find its successor
public static Node insert(Node node, int data)
{

    // If the tree is empty, return a new node
    if (node == null)
    {
        node = new Node(data);
    }

    // If key is smaller than root's key,
    // go to left subtree and set successor
    // as current node
    if (data < node.data)
    {
        succ = node;
        node.left = insert(node.left, data);
    }

    // Go to right subtree
    else if (data > node.data)
    {
        node.right = insert(node.right, data);
    }
    return node;
}

// Function to replace every element with the
// least greater element on its right
public static void replace(int[] arr, int n)
{
    //BinarySearchTree tree = new BinarySearchTree();
    // Start from right to left
    for(int i = n - 1; i >= 0; i--)
    {
        succ = null;

        // Insert current element into BST and
        // find its inorder successor
        root = BinarySearchTree.insert(root, arr[i]);

        // Replace element by its inorder
        // successor in BST
        if (succ != null)
        {
            arr[i] = succ.data;
        }

        // No inorder successor
        else
        {
            arr[i] = -1;
        }
    }
}

// Driver code
static public void Main()
{
    int[] arr = { 8, 58, 71, 18, 31,
                  32, 63, 92, 43, 3,
                  91, 93, 25, 80, 28 };
    int n = arr.Length;

    replace(arr, n);

    for(int i = 0; i < n; i++)
    {
        Console.Write(arr[i]+" ");
    }
}
}

// This code is contributed by rag2127
```

## Javascript

```
<script>

// Javascript program to
// replace every element with
// the least greater element
// on its right

    // A binary Tree node
    class Node{
        constructor(d)
        {
            this.data=d;
            this.left=this.right=null;
        }
    }

    // Root of BST
    let root=null;
    let succ=null;

    // A utility function to insert a new node with
    // given data in BST and find its successor
    function insert(node,data)
    {
        // If the tree is empty, return a new node
    if (node == null)
    {
        node = new Node(data);
    }

    // If key is smaller than root's key,
    // go to left subtree and set successor
    // as current node
    if (data < node.data)
    {
        succ = node;
        node.left = insert(node.left, data);
    }

    // Go to right subtree
    else if (data > node.data)
        node.right = insert(node.right, data);

    return node;
    }

    // Function to replace every element with the
    // least greater element on its right
    function replace(arr,n)
    {
        // start from right to left
    for(let i = n - 1; i >= 0; i--)
    {
        succ = null;

        // Insert current element into BST and
        // find its inorder successor
        root = insert(root, arr[i]);

        // Replace element by its inorder
        // successor in BST
        if (succ != null)
            arr[i] = succ.data;

        // No inorder successor
        else
            arr[i] = -1;
    }
    }

    // Driver code
    let arr=[8, 58, 71, 18, 31,
             32, 63, 92, 43, 3,
             91, 93, 25, 80, 28 ];
       let n = arr.length;
    replace(arr, n);
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");

// This code is contributed by unknown2108

</script>
```

**输出**

上述解决方案的**最坏情况时间复杂度**也是 O(n)<sup>2</sup>，因为它使用的是 BST。当数组按升序或降序排序时，会出现最坏的情况。通过使用像红黑树这样的平衡树，复杂性可以很容易地降低到 0(nlogn)。

**另一种方法:**

我们可以使用 [**下一个更大的元素使用堆栈**](https://www.geeksforgeeks.org/next-greater-element/) 算法在 **O(Nlog(N))** 时间和 **O(N)** 空间中解决这个问题。

算法:

> 1.  首先，我们取一个名为 temp 的数组对，在这个数组中存储每个元素及其索引，即 **Temp [I]将存储{arr[i]，I}** 。
> 2.  [**根据阵元对阵**](https://www.geeksforgeeks.org/sorting-algorithms/) 进行排序。
> 3.  现在，通过使用 [**【下一个更大的元素】**](https://www.geeksforgeeks.org/next-greater-element/) ，使用堆栈获取数组中临时数组的每个索引的下一个更大的索引，即索引。
> 4.  现在索引[i]存储元素 temp[i]的下一个最小和最大元素的索引。首先，如果 index[i]为-1，则表示元素 temp[i]中没有最大的元素。右边第二个。
> 5.  现在取一个结果数组，其中结果[i]将等于**a[indexes[temp[I]。Second]]** 如果索引[i]不是-1，结果[i]将等于-1。

下面是上述方法的实现

## c++

T0T6T8】输出 T10】

```
Least Greater elements on the right side are 
18 63 80 25 32 43 80 93 80 25 93 -1 28 -1 -1 
```