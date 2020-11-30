# 从包含斐波那契数字

> 原文：[https://www.geeksforgeeks.org/remove-all-nodes-from-a-doubly-linked-list-containing-fibonacci-numbers/](https://www.geeksforgeeks.org/remove-all-nodes-from-a-doubly-linked-list-containing-fibonacci-numbers/)

的双链表中删除所有节点

给定一个包含`N`个节点的[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，任务是从包含[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的列表中删除所有节点。

**示例**：

> **输入**：`DLL = 15 <=> 16 <=> 8 <=> 7 <=> 13`
>
> **输出**：`15 <=> 16 <=> 7`
>
> **说明**：
>
> 链表包含两个斐波那契数 8 和 13。
>
> 因此 ，这些节点已被删除。
> 
> **输入**：`DLL = 5 <=> 3 <=> 4 <=> 2 <=> 9`
>
> **输出**：`4 <=> 9`
>
> **说明**：
>
> 链表包含三个斐波那契数 5、3 和 2。
>
> 因此，这些节点已删除。

**方法**：这个想法是使用散列来存储和检查[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)。

1.  遍历整个[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，并获得列表中的最大值。

2.  现在，为了检查斐波那契数，建立一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于链表中最大值的斐波那契数。

3.  最后，一遍遍双链表的节点，然后[删除包含斐波纳契数作为其数据值的节点](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)。

下面是上述方法的实现：

```

// C++ implementation to delete all 
// Fibonacci nodes from the 
// doubly linked list 

#include <bits/stdc++.h> 

using namespace std; 

// Node of the doubly linked list 
struct Node { 
    int data; 
    Node *prev, *next; 
}; 

// Function to insert a node at the beginning 
// of the Doubly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // Allocate the node 
    Node* new_node 
        = (Node*)malloc(sizeof(struct Node)); 

    // Insert the data 
    new_node->data = new_data; 

    // Since we are adding at the beginning, 
    // prev is always NULL 
    new_node->prev = NULL; 

    // Link the old list off the new node 
    new_node->next = (*head_ref); 

    // Change the prev of head node to new node 
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    // Move the head to point to the new node 
    (*head_ref) = new_node; 
} 

// Function to find the largest 
// nodes in the Doubly Linked List 
int LargestInDLL(struct Node** head_ref) 
{ 
    struct Node *max, *temp; 

    // Initialize two-pointer temp 
    // and max on the head node 
    temp = max = *head_ref; 

    // Traverse the whole doubly linked list 
    while (temp != NULL) { 

        // If temp's data is greater than 
        // the max's data, then max = temp 
        // and return max->data 
        if (temp->data > max->data) 
            max = temp; 

        temp = temp->next; 
    } 
    return max->data; 
} 

// Function to create hash table to 
// check Fibonacci numbers 
void createHash(set<int>& hash, int maxElement) 
{ 
    int prev = 0, curr = 1; 
    hash.insert(prev); 
    hash.insert(curr); 

    // Inserting the Fibonacci numbers 
    // until the maximum element in the 
    // Linked List 
    while (curr <= maxElement) { 
        int temp = curr + prev; 
        hash.insert(temp); 
        prev = curr; 
        curr = temp; 
    } 
} 

// Function to delete a node 
// in a Doubly Linked List. 
// head_ref --> pointer to head node pointer. 
// del --> pointer to node to be deleted 
void deleteNode(Node** head_ref, Node* del) 
{ 
    // Base case 
    if (*head_ref == NULL || del == NULL) 
        return; 

    // If the node to be deleted is head node 
    if (*head_ref == del) 
        *head_ref = del->next; 

    // Change next only if node to be 
    // deleted is not the last node 
    if (del->next != NULL) 
        del->next->prev = del->prev; 

    // Change prev only if node to be 
    // deleted is not the first node 
    if (del->prev != NULL) 
        del->prev->next = del->next; 

    // Finally, free the memory 
    // occupied by del 
    free(del); 

    return; 
} 

// Function to delete all fibonacci nodes 
// from the doubly linked list 
void deleteFibonacciNodes(Node** head_ref) 
{ 
    // Find the largest node value 
    // in Doubly Linked List 
    int maxEle = LargestInDLL(head_ref); 

    // Creating a set containing 
    // all the fibonacci numbers 
    // upto the maximum data value 
    // in the Doubly Linked List 
    set<int> hash; 
    createHash(hash, maxEle); 

    Node* ptr = *head_ref; 
    Node* next; 

    // Iterating through the linked list 
    while (ptr != NULL) { 
        next = ptr->next; 

        // If node's data is fibonacci, 
        // delete node 'ptr' 
        if (hash.find(ptr->data) != hash.end()) 
            deleteNode(head_ref, ptr); 

        ptr = next; 
    } 
} 

// Function to print nodes in a 
// given doubly linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program 
int main() 
{ 

    Node* head = NULL; 

    // Create the doubly linked list 
    // 15 <-> 16 <-> 8 <-> 6 <-> 13 
    push(&head, 13); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 16); 
    push(&head, 15); 

    cout << "Original List: "; 
    printList(head); 

    deleteFibonacciNodes(&head); 

    cout << "\nModified List: "; 
    printList(head); 
} 

```

**输出**：

```
Original List: 15 16 8 6 13 
Modified List: 15 16 6

```

**时间复杂度**：`O(n)`，其中`N`是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。