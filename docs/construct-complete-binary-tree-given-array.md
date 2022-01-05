# 从给定的数组以层级顺序方式构建一个完整的二叉树

> 原文:[https://www . geesforgeks . org/construct-complete-二叉树-给定-array/](https://www.geeksforgeeks.org/construct-complete-binary-tree-given-array/)

给定一个元素数组，我们的任务是按照级别顺序从这个数组构建一个完整的二叉树。也就是说，数组中左边的元素将从 0 级开始逐级填充到树中。
**例:**

```
Input  :  arr[] = {1, 2, 3, 4, 5, 6}
Output : Root of the following tree
                  1
                 / \
                2   3
               / \ /
              4  5 6

Input: arr[] = {1, 2, 3, 4, 5, 6, 6, 6, 6, 6}
Output: Root of the following tree
                   1
                  / \
                 2   3
                / \ / \
               4  5 6  6
              / \ /
             6  6 6
```

如果我们仔细观察，我们可以看到，如果父节点在数组中的索引 I 处，那么该节点的左子节点在数组中的索引(2*i + 1)处，右子节点在数组中的索引(2*i + 2)处。
利用这个概念，我们可以通过选择其父节点来轻松插入左右节点。我们将插入数组中的第一个元素作为树中 0 级的根节点，并开始遍历数组，对于每个节点 I，我们将在树中左右插入它的子节点。
下面是做这个的递归程序:

## C++

```
// CPP program to construct binary
// tree from given array in level
// order fashion Tree Node
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
struct Node
{
    int data;
    Node* left, * right;
};

/* Helper function that allocates a
new node */
Node* newNode(int data)
{
    Node* node = (Node*)malloc(sizeof(Node));
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to insert nodes in level order
Node* insertLevelOrder(int arr[], Node* root,
                       int i, int n)
{
    // Base case for recursion
    if (i < n)
    {
        Node* temp = newNode(arr[i]);
        root = temp;

        // insert left child
        root->left = insertLevelOrder(arr,
                   root->left, 2 * i + 1, n);

        // insert right child
        root->right = insertLevelOrder(arr,
                  root->right, 2 * i + 2, n);
    }
    return root;
}

// Function to print tree nodes in
// InOrder fashion
void inOrder(Node* root)
{
    if (root != NULL)
    {
        inOrder(root->left);
        cout << root->data <<" ";
        inOrder(root->right);
    }
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 6, 6, 6 };
    int n = sizeof(arr)/sizeof(arr[0]);
    Node* root = insertLevelOrder(arr, root, 0, n);
    inOrder(root);
}

// This code is contributed by Chhavi
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct binary tree from
// given array in level order fashion

public class Tree {
    Node root;

    // Tree Node
    static class Node {
        int data;
        Node left, right;
        Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    // Function to insert nodes in level order
    public Node insertLevelOrder(int[] arr, Node root,
                                                int i)
    {
        // Base case for recursion
        if (i < arr.length) {
            Node temp = new Node(arr[i]);
            root = temp;

            // insert left child
            root.left = insertLevelOrder(arr, root.left,
                                             2 * i + 1);

            // insert right child
            root.right = insertLevelOrder(arr, root.right,
                                               2 * i + 2);
        }
        return root;
    }

    // Function to print tree nodes in InOrder fashion
    public void inOrder(Node root)
    {
        if (root != null) {
            inOrder(root.left);
            System.out.print(root.data + " ");
            inOrder(root.right);
        }
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        Tree t2 = new Tree();
        int arr[] = { 1, 2, 3, 4, 5, 6, 6, 6, 6 };
        t2.root = t2.insertLevelOrder(arr, t2.root, 0);
        t2.inOrder(t2.root);
    }
}
```

## 蟒蛇 3

```
# Python3 program to construct binary
# tree from given array in level
# order fashion Tree Node

# Helper function that allocates a
#new node
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Function to insert nodes in level order
def insertLevelOrder(arr, root, i, n):

    # Base case for recursion
    if i < n:
        temp = newNode(arr[i])
        root = temp

        # insert left child
        root.left = insertLevelOrder(arr, root.left,
                                     2 * i + 1, n)

        # insert right child
        root.right = insertLevelOrder(arr, root.right,
                                      2 * i + 2, n)
    return root

# Function to print tree nodes in
# InOrder fashion
def inOrder(root):
    if root != None:
        inOrder(root.left)
        print(root.data,end=" ")
        inOrder(root.right)

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 6, 6, 6]
    n = len(arr)
    root = None
    root = insertLevelOrder(arr, root, 0, n)
    inOrder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to construct binary tree from
// given array in level order fashion
using System;

public class Tree
{
    Node root;

    // Tree Node
    public class Node
    {
        public int data;
        public Node left, right;
        public Node(int data)
        {
            this.data = data;
            this.left = null;
            this.right = null;
        }
    }

    // Function to insert nodes in level order
    public Node insertLevelOrder(int[] arr,
                            Node root, int i)
    {
        // Base case for recursion
        if (i < arr.Length)
        {
            Node temp = new Node(arr[i]);
            root = temp;

            // insert left child
            root.left = insertLevelOrder(arr,
                            root.left, 2 * i + 1);

            // insert right child
            root.right = insertLevelOrder(arr,
                            root.right, 2 * i + 2);
        }
        return root;
    }

    // Function to print tree
    // nodes in InOrder fashion
    public void inOrder(Node root)
    {
        if (root != null)
        {
            inOrder(root.left);
            Console.Write(root.data + " ");
            inOrder(root.right);
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        Tree t2 = new Tree();
        int []arr = { 1, 2, 3, 4, 5, 6, 6, 6, 6 };
        t2.root = t2.insertLevelOrder(arr, t2.root, 0);
        t2.inOrder(t2.root);
    }
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to construct binary tree from
    // given array in level order fashion

    let root;

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // Function to insert nodes in level order
    function insertLevelOrder(arr, root, i)
    {
        // Base case for recursion
        if (i < arr.length) {
            let temp = new Node(arr[i]);
            root = temp;

            // insert left child
            root.left = insertLevelOrder(arr, root.left,
                                             2 * i + 1);

            // insert right child
            root.right = insertLevelOrder(arr, root.right,
                                               2 * i + 2);
        }
        return root;
    }

    // Function to print tree nodes in InOrder fashion
    function inOrder(root)
    {
        if (root != null) {
            inOrder(root.left);
            document.write(root.data + " ");
            inOrder(root.right);
        }
    }

    let arr = [ 1, 2, 3, 4, 5, 6, 6, 6, 6 ];
    root = insertLevelOrder(arr, root, 0);
    inOrder(root);

// This code is contributed by suresh07.
</script>
```

**输出:**

```
6 4 6 2 5 1 6 3 6 
```

**时间复杂度** : O(n)，其中 n 为树中节点总数。

本文由 [**Haribalaji R**](https://www.facebook.com/haribalaji.ravi) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。