# 二项式堆|集–2 的实现(删除()和递减键())

> 原文:[https://www . geesforgeks . org/implementation-binomial-heap-set-2/](https://www.geeksforgeeks.org/implementation-binomial-heap-set-2/)

在[上一篇文章](https://www.geeksforgeeks.org/implementation-binomial-heap/)中，即第 1 集中，我们已经讨论了实现以下功能:

1.  **插入(H，k):** 向二项式堆“H”插入一个键“k”。这个操作首先创建一个带有单个键“k”的二项式堆，然后调用 H 和新的二项式堆的并集。
2.  **getMin(H):**getMin()的一个简单方法是遍历二叉树的根列表并返回最小键。这个实现需要 O(Logn)时间。通过维护一个指向最小键根的指针，可以将其优化为 0(1)。
3.  **extractMin(H):** 该操作也使用 union()。我们首先调用 getMin()来找到最小键二叉树，然后移除该节点，并通过连接移除的最小节点的所有子树来创建一个新的二叉树堆。最后我们在 H 和新创建的二项式堆上调用 union()。此操作需要 0(Logn)时间。

示例:

```
12------------10--------------------20
             /  \                 /  | \
           15    50             70  50  40
           |                  / |    |     
           30               80  85  65 
                            |
                           100
A Binomial Heap with 13 nodes. It is a collection of 3 
Binomial Trees of orders 0, 2 and 3 from left to right. 

    10--------------------20
   /  \                 /  | \
 15    50             70  50  40
 |                  / |    |     
 30               80  85  65 
                  |
                 100

```

在这篇文章中，实现了以下功能。

1.  **delete(H):** 和二进制堆一样，delete 操作首先将键减为负无穷大，然后调用 extractMin()。
2.  **递减键(H):** 递减键()也类似于二进制堆。我们比较减少键和它的父键，如果父键更多，我们交换键并为父键重复。当我们到达一个其父节点具有较小键的节点时，或者当我们到达根节点时，我们停止。递减密钥()的时间复杂度为 0(Logn)

```
// C++ program for implementation of
// Binomial Heap and Operations on it
#include <bits/stdc++.h>
using namespace std;

// Structure of Node
struct Node
{
    int val, degree;
    Node *parent, *child, *sibling;
};

// Making root global to avoid one extra
// parameter in all functions.
Node *root = NULL;

// link two heaps by making h1 a child
// of h2.
int binomialLink(Node *h1, Node *h2)
{
    h1->parent = h2;
    h1->sibling = h2->child;
    h2->child = h1;
    h2->degree = h2->degree + 1;
}

// create a Node
Node *createNode(int n)
{
    Node *new_node = new Node;
    new_node->val = n;
    new_node->parent = NULL;
    new_node->sibling = NULL;
    new_node->child = NULL;
    new_node->degree = 0;
    return new_node;
}

// This function merge two Binomial Trees
Node *mergeBHeaps(Node *h1, Node *h2)
{
    if (h1 == NULL)
        return h2;
    if (h2 == NULL)
        return h1;

    // define a Node
    Node *res = NULL;

    // check degree of both Node i.e.
    // which is greater or smaller
    if (h1->degree <= h2->degree)
        res = h1;

    else if (h1->degree > h2->degree)
        res = h2;

    // traverse till if any of heap gets empty
    while (h1 != NULL && h2 != NULL)
    {
        // if degree of h1 is smaller, increment h1
        if (h1->degree < h2->degree)
            h1 = h1->sibling;

        // Link h1 with h2 in case of equal degree
        else if (h1->degree == h2->degree)
        {
            Node *sib = h1->sibling;
            h1->sibling = h2;
            h1 = sib;
        }

        // if h2 is greater
        else
        {
            Node *sib = h2->sibling;
            h2->sibling = h1;
            h2 = sib;
        }
    }
    return res;
}

// This function perform union operation on two
// binomial heap i.e. h1 & h2
Node *unionBHeaps(Node *h1, Node *h2)
{
    if (h1 == NULL && h2 == NULL)
       return NULL;

    Node *res = mergeBHeaps(h1, h2);

    // Traverse the merged list and set
    // values according to the degree of
    // Nodes
    Node *prev = NULL, *curr = res,
         *next = curr->sibling;
    while (next != NULL)
    {
        if ((curr->degree != next->degree) ||
                ((next->sibling != NULL) &&
                 (next->sibling)->degree ==
                 curr->degree))
        {
            prev = curr;
            curr = next;
        }

        else
        {
            if (curr->val <= next->val)
            {
                curr->sibling = next->sibling;
                binomialLink(next, curr);
            }
            else
            {
                if (prev == NULL)
                    res = next;
                else
                    prev->sibling = next;
                binomialLink(curr, next);
                curr = next;
            }
        }
        next = curr->sibling;
    }
    return res;
}

// Function to insert a Node
void binomialHeapInsert(int x)
{
    // Create a new node and do union of
    // this node with root
    root = unionBHeaps(root, createNode(x));
}

// Function to display the Nodes
void display(Node *h)
{
    while (h)
    {
        cout << h->val << " ";
        display(h->child);
        h = h->sibling;
    }
}

// Function to reverse a list
// using recursion.
int revertList(Node *h)
{
    if (h->sibling != NULL)
    {
        revertList(h->sibling);
        (h->sibling)->sibling = h;
    }
    else
        root = h;
}

// Function to extract minimum value
Node *extractMinBHeap(Node *h)
{
    if (h == NULL)
       return NULL;

    Node *min_node_prev = NULL;
    Node *min_node = h;

    // Find minimum value
    int min = h->val;
    Node *curr = h;
    while (curr->sibling != NULL)
    {
        if ((curr->sibling)->val < min)
        {
            min = (curr->sibling)->val;
            min_node_prev = curr;
            min_node = curr->sibling;
        }
        curr = curr->sibling;
    }

    // If there is a single Node
    if (min_node_prev == NULL &&
        min_node->sibling == NULL)
        h = NULL;

    else if (min_node_prev == NULL)
        h = min_node->sibling;

    // Remove min node from list
    else
        min_node_prev->sibling = min_node->sibling;

    // Set root (which is global) as children
    // list of min node
    if (min_node->child != NULL)
    {
        revertList(min_node->child);
        (min_node->child)->sibling = NULL;
    }

    // Do union of root h and children
    return unionBHeaps(h, root);
}

// Function to search for an element
Node *findNode(Node *h, int val)
{
    if (h == NULL)
      return NULL;

     // check if key is equal to the root's data
    if (h->val == val)
        return h;

    // Recur for child
    Node *res = findNode(h->child, val);
    if (res != NULL)
       return res;

    return findNode(h->sibling, val);
}

// Function to decrease the value of old_val
// to new_val
void decreaseKeyBHeap(Node *H, int old_val,
                               int new_val)
{
    // First check element present or not
    Node *node = findNode(H, old_val);

    // return if Node is not present
    if (node == NULL)
        return;

    // Reduce the value to the minimum
    node->val = new_val;
    Node *parent = node->parent;

    // Update the heap according to reduced value
    while (parent != NULL && node->val < parent->val)
    {
        swap(node->val, parent->val);
        node = parent;
        parent = parent->parent;
    }
}

// Function to delete an element
Node *binomialHeapDelete(Node *h, int val)
{
    // Check if heap is empty or not
    if (h == NULL)
        return NULL;

    // Reduce the value of element to minimum
    decreaseKeyBHeap(h, val, INT_MIN);

    // Delete the minimum element from heap
    return extractMinBHeap(h);
}

// Driver code
int main()
{
    // Note that root is global
    binomialHeapInsert(10);
    binomialHeapInsert(20);
    binomialHeapInsert(30);
    binomialHeapInsert(40);
    binomialHeapInsert(50);

    cout << "The heap is:\n";
    display(root);

    // Delete a particular element from heap
    root = binomialHeapDelete(root, 10);

    cout << "\nAfter deleing 10, the heap is:\n";

    display(root);

    return 0;
}
```

输出:

```
The heap is:
50 10 30 40 20 
After deleing 10, the heap is:
20 30 40 50 

```