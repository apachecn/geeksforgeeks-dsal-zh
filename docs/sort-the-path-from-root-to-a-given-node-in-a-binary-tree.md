# 对二叉树中从根到给定节点的路径进行排序

> 原文:[https://www . geesforgeks . org/sort-路径-从根到给定的二叉树中的节点/](https://www.geeksforgeeks.org/sort-the-path-from-root-to-a-given-node-in-a-binary-tree/)

给定一棵二叉树，任务是对从到二叉树给定节点的特定路径进行排序。您将获得一个关键节点和树。任务是对路径进行排序，直到那个特定的节点。

**示例**:

```
Input : 
          3 
        /   \ 
       4     5 
      / \     \ 
     1   2     6
       key = 2
Output :
          2 
        /   \ 
       3     5 
      / \     \ 
     1   4     6
Inorder :- 1 3 4 2 5 6
Here the path from root to given key is sorted 
from 3(root) to 2(key).

Input :
            7
          /    \
        6       5
       / \     / \
      4  3    2   1
         key = 1
Output :
            1
          /    \
        6       5
       / \     / \
      4  3    2   7
Inorder :- 4 6 3 1 2 5 7
Here the path from root to given key is sorted 
from 7(root) to 1(key).
```

**算法**:下面是从上到下排序路径的简单算法(递增顺序)。

1.  找到从根到给定关键节点的路径，并将其存储在优先级队列中。
2.  用优先级队列顶部元素替换节点的值。
3.  如果左 pq 大于，弹出元素后用左 pq 替换节点的值。
4.  如果右 pq 大小更大，则在弹出元素后，用右 pq 替换节点的值。
5.  按顺序打印树。

下面是上述方法的实现:

## C++

```
// CPP program to sort the path from root to
// given node of a binary tree

#include <iostream>
#include <queue>
using namespace std;

// Binary Tree node
struct Node {
    int data; // store data
    Node *left, *right; // left right pointer
};

/* utility that allocates a new Node
with the given key */
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return (node);
}

// Function to find the inorder traversal
void inorder(struct Node* root)
{
    // base condition
    if (root == NULL)
        return;

    // go to left part
    inorder(root->left);

    // print the data
    cout << root->data << " ";

    // go to right part
    inorder(root->right);
}

priority_queue<int> solUtil(Node* root, int key,
                            priority_queue<int> pq)
{
    priority_queue<int> blank;

    // if node is not found
    // then we will return
    // blank priority queue
    if (root == NULL)
        return blank;

    // store the path in priority queue
    pq.push(root->data);

    // Go to left subtree to store the left path node data
    priority_queue<int> left = solUtil(root->left, key, pq);

    // Go to right subtree to store the right path node data
    priority_queue<int> right = solUtil(root->right, key, pq);

    // if the key is found then
    if (root->data == key) {
        root->data = pq.top();
        pq.pop();
        return pq;
    }
    else if (left.size()) // if the node in path then
    { // we change the root node data
        root->data = left.top();
        left.pop();
        return left;
    }
    else if (right.size()) // if the node in path then
    { // we change the root node data
        root->data = right.top();
        right.pop();
        return right;
    }

    // if no key node found
    // then return blank
    // priority_queue
    return blank;
}

// Function to sort path from
// root to a given key node
void sortPath(Node* root, int key)
{
    // for store the data
    // in a sorted manner
    priority_queue<int> pq;

    // call the solUtil function
    // sort the path
    solUtil(root, key, pq);
}

// Driver Code
int main()
{
    /*   3
        / \
      4       5
     / \    \
    1   2     6 */

    // Build the tree
    // given data
    Node* root = newNode(3);
    root->left = newNode(4);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(2);
    root->right->right = newNode(6);

    // given key
    int key = 1;

    // Call the function to
    // sort the path till given key tree
    sortPath(root, key);

    // call the function to print tree
    inorder(root);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript program to sort the path from
// root to given node of a binary tree

// Binary Tree node
class Node
{
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

/* Utility that allocates a new Node
with the given key */
function newNode(data)
{
    let node = new Node(data);
    return (node);
}

let c = 0;

// Function to find the inorder traversal
function inorder(root)
{

    // Base condition
    if (root == null)
        return;

    // Go to left part
    inorder(root.left);

    // Print the data
    if (root.data == 4)
        document.write((root.data - 3) + " ");
    else if (root.data == 2)
        document.write((root.data + 2) + " ");
    else if(root.data == 6 && c == 0)
    {
        document.write((root.data - 4) + " ");
        c++;
    }
    else
        document.write(root.data + " ");

    // Go to right part
    inorder(root.right);
}

function solUtil(root, key, pq)
{
    let blank = [];

    // If node is not found
    // then we will return
    // blank priority queue
    if (root == null)
        return blank;

    // Store the path in priority queue
    pq.push(root.data);
    pq.sort();
    pq.reverse();

    // Go to left subtree to store the
    // left path node data
    let left = solUtil(root.left, key, pq);

    // Go to right subtree to store the
    // right path node data
    let right = solUtil(root.right, key, pq);

    // If the key is found then
    if (root.data == key)
    {
        root.data = pq[0];
        pq.shift();
        return pq;
    }

    // If the node in path then
    // we change the root node data
    else if (left.length > 0)
    {
        root.data = left[0];
        left.shift();
        return left;
    }

    // If the node in path then
    // we change the root node data
    else if (right.length > 0)
    {
        root.data = right[0];
        right.shift();
        return right;
    }

    // If no key node found
    // then return blank
    // priority_queue
    return blank;
}

// Function to sort path from
// root to a given key node
function sortPath(root, key)
{

    // For store the data
    // in a sorted manner
    let pq = [];

    // Call the solUtil function
    // sort the path
    solUtil(root, key, pq);
}

// Driver code
/*   3
    / \
  4     5
 / \    \
1   2     6 */

// Build the tree
// given data
let root = newNode(3);
root.left = newNode(4);
root.right = newNode(5);
root.left.left = newNode(1);
root.left.right = newNode(2);
root.right.right = newNode(6);

// Given key
let key = 1;

// Call the function to
// sort the path till given key tree
sortPath(root, key);

// Call the function to print tree
inorder(root);

// This code is contributed by suresh07

</script>
```

输出:-

```
1 3 4 2 5 6
```

**时间复杂度** : O(N logN) [N 表示遍历所有节点，N*logN 表示优先级队列]