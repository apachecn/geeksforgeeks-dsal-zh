# n 元树中的第二大元素

> 原文:[https://www . geesforgeks . org/第二大元素-n-ary-tree/](https://www.geeksforgeeks.org/second-largest-element-n-ary-tree/)

给定一个 N 元树，找到并返回给定树中具有第二大值的节点。如果不存在具有所需值的节点，则返回空值。
例如，在给定的树中

![](img/c7c9487b3a4f153afdb7453d43220fa1.png)

第二大节点是 20。

一个**简单的**解决方案是遍历数组两次。在第一次遍历中找到最大值节点。在第二次遍历中，找到比第一次遍历中获得的元素少的最大元素节点。这个解的时间复杂度是 O(n)。
一个**高效的**解决方案可以是在单次遍历中找到第二大元素。
下面是完成此操作的完整算法:

```
1) Initialize two nodes first and second to NULL as,
   first = second = NULL
2) Start traversing the tree,
   a) If the current node data say root->key is greater
      than first->key then update first and second as,
      second = first
      first = root
   b) If the current node data is in between first and 
      second, then update second to store the value
      of current node as
        second = root
3) Return the node stored in second.
```

## C++

```
// CPP program to find second largest node
// in an n-ary tree.
#include <bits/stdc++.h>
using namespace std;

// Structure of a node of an n-ary tree
struct Node {
    int key;
    vector<Node*> child;
};

// Utility function to create a new tree node
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    return temp;
}

void secondLargestUtil(Node* root, Node** first,
                       Node** second)
{
    if (root == NULL)
        return;

    // If first is NULL, make root equal to first
    if (!(*first))
        *first = root;

    // if root is greater than first then second
    // will become first and update first equal
    // to root
    else if (root->key > (*first)->key) {
        *second = *first;
        *first = root;
    }
    // if second is null, then
    // update first only if root is less than first
    else if (!(*second)) {
        if (root->key < (*first)->key) {
            *second = root;
        }
    }
    // If root is less than first but greater than second
    else if (root->key < (*first)->key && root->key > (*second)->key)
        *second = root;

    // number of children of root
    int numChildren = root->child.size();

    // recursively calling for every child
    for (int i = 0; i < numChildren; i++)
        secondLargestUtil(root->child[i], first, second);
}

Node* secondLargest(Node* root)
{
    // second will store the second highest value
    Node* second = NULL;

    // first will store the largest value in the tree
    Node* first = NULL;

    // calling the helper function
    secondLargestUtil(root, &first, &second);

    if (second == NULL)
        return NULL;

    // return the second largest element
    return second;
}

// Driver program
int main()
{
    /*   Let us create below tree
   *             5
   *         /   |  \
   *         1   2   3
   *        /   / \   \
   *       15  4   5   6
   */

    Node* root = newNode(5);
    (root->child).push_back(newNode(1));
    (root->child).push_back(newNode(2));
    (root->child).push_back(newNode(3));
    (root->child[0]->child).push_back(newNode(15));
    (root->child[1]->child).push_back(newNode(4));
    (root->child[1]->child).push_back(newNode(5));
    (root->child[2]->child).push_back(newNode(6));

    if (secondLargest(root) != NULL)
        cout << "Second largest element is : " << secondLargest(root)->key << endl;
    else
        cout << "Second largest element not found\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Class for the node of the tree
    static class Node
    {
        int data;

        // List of children
        Node children[];

        Node(int n, int data)
        {
            children = new Node[n];
            this.data = data;
        }
    }

    // Pointers to store the largest and second largest node
    public static Node largest;
    public static Node secondLargest;

    // Helper Function to find the second largest node of the n-ary tree
    public static void findSecondLargestHelper(Node root)
    {

        // Base Case
        if (root == null) {
            return;
        }

        // Check if root's data is larger than current largest node's data
        if (root.data > largest.data) {
            secondLargest = largest;
            largest = root;
        } else if (root.data > secondLargest.data && root.data != largest.data)
            secondLargest = root;

        // recursively find second largest in children
        for (Node child: root.children)
            findSecondLargestHelper(child);
    }

    // Function to find the second largest node of the n-ary tree
    public static Node findSecondLargest(Node root)
    {

        // Initialising the pointers to a node with value negative infinity
        largest = new Node(0, Integer.MIN_VALUE);
        secondLargest = largest;

        findSecondLargestHelper(root);
        return secondLargest;
    }

    // Driver code
    public static void main(String[] args)
    {

        /* Create the following tree
                   1
                /  |  \
               2   3   4
             / | \
            5  6  7
        */
        int n = 3;
        Node root = new Node(n, 1);
        root.children[0] = new Node(n, 2);
        root.children[1] = new Node(n, 3);
        root.children[2] = new Node(n, 4);
        root.children[0].children[0] = new Node(n, 5);
        root.children[0].children[1] = new Node(n, 6);
        root.children[0].children[2] = new Node(n, 7);

        findSecondLargest(root);

        System.out.print("Second Largest Node is: ");
        System.out.println(secondLargest.data);
    }
}

// This code is contributed by Amitava Mitra
```

**Output:** 

```
Second largest element is : 6
```

本文由 [**查哈维**](https://auth.geeksforgeeks.org/profile.php?user=chhavi saini 1&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。