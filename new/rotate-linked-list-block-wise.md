# 明智地旋转链接列表

给定长度为n和块长度为**的链表，k** 循环向每个块右/左旋转 **d** 。 如果 **d** 为正，则向右旋转，否则向左旋转。

**示例：**

```
Input: 1->2->3->4->5->6->7->8->9->NULL, 
        k = 3 
        d = 1
Output: 3->1->2->6->4->5->9->7->8->NULL
Explanation: Here blocks of size 3 are
rotated towards right(as d is positive) 
by 1.

Input: 1->2->3->4->5->6->7->8->9->10->
               11->12->13->14->15->NULL, 
        k = 4 
        d = -1
Output: 2->3->4->1->6->7->8->5->10->11
             ->12->9->14->15->13->NULL
Explanation: Here, at the end of linked 
list, remaining nodes are less than k, i.e.
only three nodes are left while k is 4\. 
Rotate those 3 nodes also by d.

```

先决条件：[旋转链接列表](https://www.geeksforgeeks.org/rotate-a-linked-list/)

这个想法是，如果d的绝对值大于k的值，则将链接列表旋转d％k次。 如果d为0，则根本不需要旋转链表。

## C++

```cpp

// C++ program to rotate a linked list block wise  
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

// Recursive function to rotate one block  
Node* rotateHelper(Node* blockHead,  
                        Node* blockTail,  
                        int d, Node** tail,  
                        int k)  
{  
    if (d == 0)  
        return blockHead;  

    // Rotate Clockwise  
    if (d > 0)  
    {  
        Node* temp = blockHead;  
        for (int i = 1; temp->next->next &&  
                        i < k - 1; i++)  
            temp = temp->next;  
        blockTail->next = blockHead;  
        *tail = temp;  
        return rotateHelper(blockTail, temp,  
                            d - 1, tail, k);  
    }  

    // Rotate anti-Clockwise  
    if (d < 0)  
    {  
        blockTail->next = blockHead;  
        *tail = blockHead;  
        return rotateHelper(blockHead->next,  
                blockHead, d + 1, tail, k);  
    }  
}  

// Function to rotate the linked list block wise  
Node* rotateByBlocks(Node* head,  
                                int k, int d)  
{  
    // If length is 0 or 1 return head  
    if (!head || !head->next)  
        return head;  

    // if degree of rotation is 0, return head  
    if (d == 0)  
        return head;  

    Node* temp = head, *tail = NULL;  

    // Traverse upto last element of this block  
    int i;  
    for (i = 1; temp->next && i < k; i++)  
        temp = temp->next;  

    // storing the first node of next block  
    Node* nextBlock = temp->next;  

    // If nodes of this block are less than k.  
    // Rotate this block also  
    if (i < k)  
        head = rotateHelper(head, temp, d % k,  
                                    &tail, i);  
    else
        head = rotateHelper(head, temp, d % k,  
                                    &tail, k);  

    // Append the new head of next block to  
    // the tail of this block  
    tail->next = rotateByBlocks(nextBlock, k,  
                                    d % k);  

    // return head of updated Linked List  
    return head;  
}  

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(Node** head_ref, int new_data)  
{  
    Node* new_node = new Node;  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

/* Function to print linked list */
void printList(Node* node)  
{  
    while (node != NULL)  
    {  
        cout << node->data << " ";  
        node = node->next;  
    }  
}  

/* Driver code*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    // create a list 1->2->3->4->5->  
    // 6->7->8->9->NULL  
    for (int i = 9; i > 0; i -= 1)  
        push(&head, i);  

    cout<<"Given linked list \n";  
    printList(head);  

    // k is block size and d is number of  
    // rotations in every block.  
    int k = 3, d = 2;  
    head = rotateByBlocks(head, k, d);  

    cout << "\nRotated by blocks Linked list \n";  
    printList(head);  

    return (0);  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to rotate a linked list block wise 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Recursive function to rotate one block 
struct Node* rotateHelper(struct Node* blockHead, 
                          struct Node* blockTail, 
                          int d, struct Node** tail, 
                          int k) 
{ 
    if (d == 0) 
        return blockHead; 

    // Rotate Clockwise 
    if (d > 0) { 
        struct Node* temp = blockHead; 
        for (int i = 1; temp->next->next && 
                        i < k - 1; i++) 
            temp = temp->next; 
        blockTail->next = blockHead; 
        *tail = temp; 
        return rotateHelper(blockTail, temp, 
                            d - 1, tail, k); 
    } 

    // Rotate anti-Clockwise 
    if (d < 0) { 
        blockTail->next = blockHead; 
        *tail = blockHead; 
        return rotateHelper(blockHead->next, 
                blockHead, d + 1, tail, k); 
    } 
} 

// Function to rotate the linked list block wise 
struct Node* rotateByBlocks(struct Node* head, 
                                 int k, int d) 
{ 
    // If length is 0 or 1 return head 
    if (!head || !head->next) 
        return head; 

    // if degree of rotation is 0, return head 
    if (d == 0) 
        return head; 

    struct Node* temp = head, *tail = NULL; 

    // Traverse upto last element of this block 
    int i; 
    for (i = 1; temp->next && i < k; i++) 
        temp = temp->next; 

    // storing the first node of next block 
    struct Node* nextBlock = temp->next; 

    // If nodes of this block are less than k. 
    // Rotate this block also 
    if (i < k) 
        head = rotateHelper(head, temp, d % k, 
                                    &tail, i); 
    else
        head = rotateHelper(head, temp, d % k, 
                                    &tail, k); 

    // Append the new head of next block to 
    // the tail of this block 
    tail->next = rotateByBlocks(nextBlock, k, 
                                      d % k); 

    // return head of updated Linked List 
    return head; 
} 

/* UTILITY FUNCTIONS */
/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    // create a list 1->2->3->4->5-> 
    // 6->7->8->9->NULL 
    for (int i = 9; i > 0; i -= 1) 
        push(&head, i); 

    printf("Given linked list \n"); 
    printList(head); 

    // k is block size and d is number of 
    // rotations in every block. 
    int k = 3, d = 2; 
    head = rotateByBlocks(head, k, d); 

    printf("\nRotated by blocks Linked list \n"); 
    printList(head); 

    return (0); 
} 

```

**Output:**

```
Given linked list 
1 2 3 4 5 6 7 8 9 
Rotated by blocks Linked list 
2 3 1 5 6 4 8 9 7 

```

本文由 **Chhavi** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

