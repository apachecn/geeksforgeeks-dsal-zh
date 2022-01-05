# 如何对重复次数多的大数组进行排序？

> 原文:[https://www . geeksforgeeks . org/如何对多次重复的大数组进行排序/](https://www.geeksforgeeks.org/how-to-sort-a-big-array-with-many-repetitions/)

考虑一个大数组，其中元素来自一个小集合，并且在任何范围内，即有许多重复。如何高效排序数组？

```
Example: 
Input:  arr[] = {100, 12, 100, 1, 1, 12, 100, 1, 12, 100, 1, 1}
Output: arr[] = {1, 1, 1, 1, 1, 12, 12, 12, 100, 100, 100, 100}
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
像[合并排序](http://geeksquiz.com/merge-sort/)、[堆排序](http://geeksquiz.com/heap-sort/)这样的**基本排序**算法需要 O(nLogn)时间，其中 n 是元素数量，我们能做得更好吗？
一个**更好的解决方案**是使用自平衡二叉查找树像 [AVL](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/) 或[红黑](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)在 O(n Log m)时间排序，其中 m 是不同元素的数量。其思想是扩展树节点，使其也有键数。

```
struct Node
{
   int key;
   struct Node *left. *right;
   int count;  // Added to handle duplicates

   // Other tree node info for balancing like height in AVL
}
```

下面是使用 AVL 树的完整算法。
1)创建一个空的 AVL 树，将计数作为附加字段。
2)遍历输入数组，并对每个元素“arr[I]”
执行以下操作…..a)如果 arr[i]不在树中，则插入它并初始化计数为 1
…..b)否则增加其在树中的计数。
3)进行树的有序遍历。这样做时，请将每个键的计数次数放在 arr[]。
第 2 <sup>步和第 3 <sup>步耗时。所以整体时间复杂度为 O(n Log m)
下面是上述思想的 C++实现。</sup></sup> 

## C++

```
// C++ program to sort an array using AVL tree
#include<iostream>
using namespace std;

// An AVL tree Node
struct Node
{
    int key;
    struct Node *left, *right;
    int height, count;
};

// Function to insert a key in AVL Tree, if key is already present,
// then it increments count in key's node.
struct Node* insert(struct Node* Node, int key);

// This function puts inorder traversal of AVL Tree in arr[]
void inorder(int arr[], struct Node *root, int *index_ptr);

// An AVL tree based sorting function for sorting an array with
// duplicates
void sort(int arr[], int n)
{
  // Create an empty AVL Tree
  struct Node *root = NULL;

  // Insert all nodes one by one in AVL tree. The insert function
  // increments count if key is already present
  for (int i=0; i<n; i++)
     root = insert(root, arr[i]);

  // Do inorder traversal to put elements back in sorted order
  int index = 0;
  inorder(arr, root, &index);
}

// This function puts inorder traversal of AVL Tree in arr[]
void inorder(int arr[], struct Node *root, int *index_ptr)
{
    if (root != NULL)
    {
        // Recur for left child
        inorder(arr, root->left, index_ptr);

        // Put all occurrences of root's key in arr[]
        for (int i=0; i<root->count; i++)
        {
           arr[*index_ptr] = root->key;
           (*index_ptr)++;
        }

        // Recur for right child
        inorder(arr, root->right, index_ptr);
    }
}

// A utility function to get height of the tree
int height(struct Node *N)
{
    if (N == NULL)
        return 0;
    return N->height;
}

// Helper function that allocates a new Node
struct Node* newNode(int key)
{
    struct Node* node = new Node;
    node->key   = key;
    node->left   = node->right = NULL;
    node->height = node->count = 1;
    return(node);
}

// A utility function to right rotate subtree rooted
// with y.
struct Node *rightRotate(struct Node *y)
{
    struct Node *x = y->left;
    struct Node *T2 = x->right;

    // Perform rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right))+1;
    x->height = max(height(x->left), height(x->right))+1;

    // Return new root
    return x;
}

// A utility function to left rotate subtree rooted with x
struct Node *leftRotate(struct Node *x)
{
    struct Node *y = x->right;
    struct Node *T2 = y->left;

    // Perform rotation
    y->left = x;
    x->right = T2;

    //  Update heights
    x->height = max(height(x->left), height(x->right))+1;
    y->height = max(height(y->left), height(y->right))+1;

    // Return new root
    return y;
}

// Get Balance factor of Node N
int getBalance(struct Node *N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}

// Function to insert a key in AVL Tree, if key is already
// present, then it increments count in key's node.
struct Node* insert(struct Node* Node, int key)
{
    /* 1.  Perform the normal BST rotation */
    if (Node == NULL)
        return (newNode(key));

    // If key already exists in BST, increment count and return
    if (key == Node->key)
    {
        (Node->count)++;
        return Node;
    }

     /* Otherwise, recur down the tree */
    if (key < Node->key)
        Node->left  = insert(Node->left, key);
    else
        Node->right = insert(Node->right, key);

    /* 2\. Update height of this ancestor Node */
    Node->height = max(height(Node->left), height(Node->right)) + 1;

    /* 3\. Get the balance factor of this ancestor Node to
       check whether this Node became unbalanced */
    int balance = getBalance(Node);

    // If this Node becomes unbalanced, then there are 4 cases

    // Left Left Case
    if (balance > 1 && key < Node->left->key)
        return rightRotate(Node);

    // Right Right Case
    if (balance < -1 && key > Node->right->key)
        return leftRotate(Node);

    // Left Right Case
    if (balance > 1 && key > Node->left->key)
    {
        Node->left =  leftRotate(Node->left);
        return rightRotate(Node);
    }

    // Right Left Case
    if (balance < -1 && key < Node->right->key)
    {
        Node->right = rightRotate(Node->right);
        return leftRotate(Node);
    }

    /* return the (unchanged) Node pointer */
    return Node;
}

// A utility function to print an array
void printArr(int arr[], int n)
{
    for (int i=0; i<n; i++)
       cout << arr[i] << ", ";
    cout << endl;
}

/* Driver program to test above function*/
int main()
{
  int arr[] = {100, 12, 100, 1, 1, 12, 100, 1, 12, 100, 1, 1};
  int n = sizeof(arr)/sizeof(arr[0]);

  cout << "Input array is\n";
  printArr(arr, n);

  sort(arr, n);

  cout << "Sorted array is\n";
  printArr(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for insertion in AVL Tree
public class AvlTree
{

    static Node root = null;

    static class Node
    {
        int key, height, count;
        Node left, right;

        Node(int d)
        {
            key = d;
            height = 1;
            count = 1;
            left = right = null;
        }
    }

    // A utility function to get the height of the tree
    int height(Node N)
    {
        if (N == null)
            return 0;

            return N.height;
    }

    // A utility function to get maximum of two integers
    int max(int a, int b)
    {
        return (a > b) ? a : b;
    }

    // A utility function to right rotate subtree rooted with y
    // See the diagram given above.
    Node rightRotate(Node y)
    {
        Node x = y.left;
        Node T2 = x.right;

        // Perform rotation
        x.right = y;
        y.left = T2;

        // Update heights
        y.height = max(height(y.left), height(y.right)) + 1;
        x.height = max(height(x.left), height(x.right)) + 1;

        // Return new root
        return x;
    }

    // A utility function to left rotate subtree rooted with x
    // See the diagram given above.
    Node leftRotate(Node x)
    {
        Node y = x.right;
        Node T2 = y.left;

        // Perform rotation
        y.left = x;
        x.right = T2;

        // Update heights
        x.height = max(height(x.left), height(x.right)) + 1;
        y.height = max(height(y.left), height(y.right)) + 1;

        // Return new root
        return y;
    }

    // Get Balance factor of node N
    int getBalance(Node N)
    {
        if (N == null)
            return 0;

        return height(N.left) - height(N.right);
    }

    Node insert(Node node, int key)
    {

        /* 1\. Perform the normal BST insertion */
        if (node == null)
            return (new Node(key));

        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);

        // Duplicate keys not allowed
        else
        {
            node.count++;
            return node;
        }

        /* 2\. Update height of this ancestor node */
        node.height = 1 + max(height(node.left),
                            height(node.right));

        /* 3\. Get the balance factor of this ancestor
            node to check whether this node became
            unbalanced */
        int balance = getBalance(node);

        // If this node becomes unbalanced, then there
        // are 4 cases Left Left Case
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && key > node.left.key)
        {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && key < node.right.key)
        {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }

        /* return the (unchanged) node pointer */
        return node;
    }

    // inorder traversal in BST always give sorted
    // order. Put the sorted elements back into the array
    int inorder(Node n, int arr[], int i)
    {
        if (n != null)
        {
            i = inorder(n.left, arr, i);
            for(int j = 0; j < n.count; j++)
            {
                arr[i] = n.key;
                i++;
            }
            i = inorder(n.right, arr, i);
        }
        return i;
    }

    // Driver code
    public static void main(String[] args)
    {
        // TODO Auto-generated method stub
        int arr[] = {100, 12, 100, 1, 1, 12, 100, 1, 12, 100, 1, 1};
        System.out.println("Input array ");
        for (int i = 0; i < arr.length; i++)
        System.out.print(" "+ arr[i]);

        AvlTree at= new AvlTree();

        // insert all element in AVL tree
        for (int i = 0; i < arr.length; i++)
        root = at.insert(root, arr[i]);

        // Do inorder traversal to put
        // elements back in sorted order
        int index = 0;
        at.inorder(root, arr, index);
        System.out.println("\nOutput array ");
        for (int i = 0; i < arr.length; i++)
            System.out.print(" "+ arr[i]);
    }
}

// This code is contributed by moonishussain
```

**输出:**

```
Input array is
100, 12, 100, 1, 1, 12, 100, 1, 12, 100, 1, 1,
Sorted array is
1, 1, 1, 1, 1, 12, 12, 12, 100, 100, 100, 100,
```

我们也可以用[二进制堆](http://geeksquiz.com/binary-heap/)在 O(n Log m)时间内求解。
我们也可以使用 [**哈希**](http://geeksquiz.com/hashing-set-1-introduction/) **在 O(n + m Log m)时间**内解决上述问题。
1)创建一个空哈希表。输入数组值作为键存储，它们的计数作为值存储在哈希表中。
2)对于 arr[]的每个元素“x”，请执行以下操作
…..a)如果哈希表中存在 x ix，增加其值
…..b)否则插入值等于 1 的 x。
3)考虑哈希表的所有键并排序。
4)遍历所有排序的键，并打印每个键的值次数。
在哈希搜索和插入花费 O(1)时间的假设下，2 <sup>和</sup>步的时间复杂度为 O(n)。步骤 3 花费 0(m Log m)时间，其中 m 是输入数组中不同键的总数。第四步耗时 0(n)。所以总的时间复杂度是 O(n + m Log m)。
使用哈希表的程序实现

## C

```
// A C++ program to sort a big array with many repetitions

#include <iostream>
#include <algorithm>
#include <map>
using namespace std;

void sort(int arr[], int n)
{
   //1\. Create an empty hash table.
    map<int, int> count;

    //2\. Input array values are stores as key and their
    //counts are stored as value in hash table.
    for (int i=0; i<n; i++)
        count[arr[i]]++;

    map<int, int>::iterator it;
    int index = 0;

    //3\. Consider all keys of hash table and sort them.
    //In std::map, keys are already sorted.

    //4\. Traverse all sorted keys and print every key its value times.
    for (it=count.begin(); it!=count.end(); ++it)
    {
        while(it->second--)
        arr[index++]=it->first;
    }
}

// Utility function to print an array
void printArray(int arr[], int n)
{
    for (int i=0; i<n; i++)
        cout << arr[i] << " ";
        cout << endl;
 }

// Driver program to test above function.
int main()
{
    int arr[] = {100, 12, 100, 1, 1, 12, 100, 1, 12, 100, 1, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << "Input array is\n";
    printArray(arr, n);

    sort(arr, n);

    cout << "Sorted array is\n";
    printArray(arr, n);

    return 0;
}
// Contributed by Aditya Goel
```

输出:

```
Input array is

100 12 100 1 1 12 100 1 12 100 1 1 

Sorted array is

1 1 1 1 1 12 12 12 100 100 100 100
```

本文由 Ankur 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。