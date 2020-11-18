# 展平链接列表

> 原文：[https://www.geeksforgeeks.org/flattening-a-linked-list/](https://www.geeksforgeeks.org/flattening-a-linked-list/)

给定一个链表，其中每个节点代表一个链表，并包含两个其类型的指针：

（i）指向主列表中下一个节点的指针（在下面的代码中我们称之为“正确”指针）

（ii）指向此节点为头的链接列表的指针（在下面的代码中我们称之为“向下”指针）。

所有链接列表已排序。 请参阅以下示例

```
       5 -> 10 -> 19 -> 28
       |    |     |     |
       V    V     V     V
       7    20    22    35
       |          |     |
       V          V     V
       8          50    40
       |                |
       V                V
       30               45

```

编写一个函数 flatten（）以将列表展平为单个链接列表。 展平的链表也应排序。 例如，对于上面的输入列表，输出列表应为 5-> 7-> 8-> 10-> 19-> 20-> 22-> 28-> 30-> 35-> 40-> 45-> 50 。

这个想法是对链接列表使用[合并排序的 Merge（）过程。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/) 我们使用 merge（）逐一合并列表。 我们以递归方式将当前列表与已经变平的列表合并（）。

下指针用于链接扁平化列表的节点。

以下是 C 和 Java 实现。

## C / C++

```cpp

// C program for flattening a linked list 
#include <stdio.h> 
#include <stdlib.h> 

// A Linked List Node 
typedef struct Node 
{ 
    int data; 
    struct Node *right; 
    struct Node *down; 
} Node; 

/* A utility function to insert a new node at the beginning 
   of linked list */
void push (Node** head_ref, int new_data) 
{ 
    /* allocate node */
    Node* new_node = (Node *) malloc(sizeof(Node)); 
    new_node->right = NULL; 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->down = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

/* Function to print nodes in the flattened linked list */
void printList(Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->down; 
    } 
} 

// A utility function to merge two sorted linked lists 
Node* merge( Node* a, Node* b ) 
{ 
    // If first list is empty, the second list is result 
    if (a == NULL) 
        return b; 

    // If second list is empty, the second list is result 
    if (b == NULL) 
        return a; 

    // Compare the data members of head nodes of both lists 
    // and put the smaller one in result 
    Node* result; 
    if (a->data < b->data) 
    { 
        result = a; 
        result->down = merge( a->down, b ); 
    } 
    else
    { 
        result = b; 
        result->down = merge( a, b->down ); 
    } 

    result->right = NULL; 
    return result; 
} 

// The main function that flattens a given linked list 
Node* flatten (Node* root) 
{ 
    // Base cases 
    if (root == NULL || root->right == NULL) 
        return root; 

    // Merge this list with the list on right side 
    return merge( root, flatten(root->right) ); 
} 

// Driver program to test above functions 
int main() 
{ 
    Node* root = NULL; 

    /* Let us create the following linked list 
       5 -> 10 -> 19 -> 28 
       |    |     |     | 
       V    V     V     V 
       7    20    22    35 
       |          |     | 
       V          V     V 
       8          50    40 
       |                | 
       V                V 
       30               45 
    */
    push( &root, 30 ); 
    push( &root, 8 ); 
    push( &root, 7 ); 
    push( &root, 5 ); 

    push( &( root->right ), 20 ); 
    push( &( root->right ), 10 ); 

    push( &( root->right->right ), 50 ); 
    push( &( root->right->right ), 22 ); 
    push( &( root->right->right ), 19 ); 

    push( &( root->right->right->right ), 45 ); 
    push( &( root->right->right->right ), 40 ); 
    push( &( root->right->right->right ), 35 ); 
    push( &( root->right->right->right ), 20 ); 

    // Let us flatten the list 
    root = flatten(root); 

    // Let us print the flatened linked list 
    printList(root); 

    return 0; 
} 

```

## Java

```java

// Java program for flattening a Linked List 
class LinkedList 
{ 
    Node head;  // head of list 

    /* Linked list Node*/
    class Node 
    { 
        int data; 
        Node right, down; 
        Node(int data) 
        { 
            this.data = data; 
            right = null; 
            down = null; 
        } 
    } 

    // An utility function to merge two sorted linked lists 
    Node merge(Node a, Node b) 
    { 
        // if first linked list is empty then second 
        // is the answer 
        if (a == null)     return b; 

        // if second linked list is empty then first 
        // is the result 
        if (b == null)      return a; 

        // compare the data members of the two linked lists 
        // and put the larger one in the result 
        Node result; 

        if (a.data < b.data) 
        { 
            result = a; 
            result.down =  merge(a.down, b); 
        } 

        else
        { 
            result = b; 
            result.down = merge(a, b.down); 
        } 

        result.right = null;  
        return result; 
    } 

    Node flatten(Node root) 
    { 
        // Base Cases 
        if (root == null || root.right == null) 
            return root; 

        // recur for list on right 
        root.right = flatten(root.right); 

        // now merge 
        root = merge(root, root.right); 

        // return the root 
        // it will be in turn merged with its left 
        return root; 
    } 

    /* Utility function to insert a node at beginning of the 
       linked list */
    Node push(Node head_ref, int data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(data); 

        /* 3\. Make next of new Node as head */
        new_node.down = head_ref; 

        /* 4\. Move the head to point to new Node */
        head_ref = new_node; 

        /*5\. return to link it back */
        return head_ref; 
    } 

    void printList() 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
            System.out.print(temp.data + " "); 
            temp = temp.down; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        LinkedList L = new LinkedList(); 

        /* Let us create the following linked list 
            5 -> 10 -> 19 -> 28 
            |    |     |     | 
            V    V     V     V 
            7    20    22    35 
            |          |     | 
            V          V     V 
            8          50    40 
            |                | 
            V                V 
            30               45 
        */

        L.head = L.push(L.head, 30); 
        L.head = L.push(L.head, 8); 
        L.head = L.push(L.head, 7); 
        L.head = L.push(L.head, 5); 

        L.head.right = L.push(L.head.right, 20); 
        L.head.right = L.push(L.head.right, 10); 

        L.head.right.right = L.push(L.head.right.right, 50); 
        L.head.right.right = L.push(L.head.right.right, 22); 
        L.head.right.right = L.push(L.head.right.right, 19); 

        L.head.right.right.right = L.push(L.head.right.right.right, 45); 
        L.head.right.right.right = L.push(L.head.right.right.right, 40); 
        L.head.right.right.right = L.push(L.head.right.right.right, 35); 
        L.head.right.right.right = L.push(L.head.right.right.right, 20); 

        // flatten the list 
        L.head = L.flatten(L.head); 

        L.printList(); 
    } 
} /* This code is contributed by Rajat Mishra */

```

**Output:**

```
5 7 8 10 19 20 20 22 30 35 40 45 50

```

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

