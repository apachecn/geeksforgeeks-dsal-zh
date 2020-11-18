# 将最后一个元素移到给定链接列表的前面 | 系列 2

给定一个单链表和一个整数 **K** 。 任务是将链表的最后 **K** 个元素附加到前面。

**示例**：

> **输入**：1-> 2-> 3-> 4-> 5-> 6，k = 3
> **输出**：4 -> 5-> 6-> 1-> 2-> 3
> 
> **输入**：1-> 2-> 3-> 4-> 5-> 6，k = 7
> **输出**：6 -> 1-> 2-> 3-> 4-> 5

**先决条件**：[将最后一个元素移到给定链接列表](https://www.geeksforgeeks.org/move-last-element-to-front-of-a-given-linked-list/)的前面

**方法**：

*   循环（k％n）次，其中 n 是链接列表中元素的数量。

*   每次，从链接列表的末尾删除一个节点。

*   同时在链表的开头插入该已删除的节点。

下面是上述方法的实现：

```

// CPP Program to move k last elements  
// to front in a given linked list  
#include<iostream> 
using namespace std; 

// A linked list node  
class Node 
{ 
    public: 

    int data; 
    Node* next; 
    Node(int d) { 
        data = d; 
        next = NULL; 
    } 
}; 

// Function to add a new node at the 
// end/tail of Linked List  
void insertAtTail(Node*& head, Node*& tail, int d ) { 
    Node* newnode = new Node(d); 
    if(tail == NULL) { 
        tail = head = newnode; 
        return; 
    } 

    tail->next = newnode; 
    tail = newnode; 
} 

// Function to add a node at the 
// beginning of Linked List  
void insertAtHead(Node*& head, Node*& tail,  
                           Node*& deletedNode)  
{ 
    if(head == NULL) { 
        head = tail = deletedNode; 
        return; 
    } 
    deletedNode->next = head; 
    head = deletedNode; 
    return; 
} 

// Function to add a node at the beginning of Linked List  
Node* deleteAtTail(Node*& head, Node*& tail) { 
    Node* deleted = tail; 
    Node* temp = head; 

    while(temp->next->next != NULL) { 
        temp = temp->next; 
    } 

    temp->next = NULL; 
    tail = temp; 
    return deleted; 
} 

// k can be more than n, so this function takes the modulus  
// of k with n and delete nodes from end k  
// times and simultaneously insert it in front 
void appendAtFront(Node*& head, Node*& tail, int n, int k)  
{ 
    k = k % n; 
    while(k != 0) { 
        Node* deleted = deleteAtTail(head, tail); 
        insertAtHead(head, tail, deleted); 
        k--; 
    } 
} 

// Function to print nodes in a given linked list  
void printLinkedList(Node* head) { 
    while(head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

// Driver Code  
int main()  
{ 
    // Pointer to the start of the linked list 
    Node* head = NULL; 

    // Pointer to the end of the linked list 
    Node* tail = NULL;  

    // Number of elements in the linked list 
    int n = 6;  

    // Building linked list 
    insertAtTail(head, tail, 1); 
    insertAtTail(head, tail, 2); 
    insertAtTail(head, tail, 3); 
    insertAtTail(head, tail, 4); 
    insertAtTail(head, tail, 5); 
    insertAtTail(head, tail, 6); 

    // Printing linked list before  
    // appending the linked list 
    cout << "Linked List before appending: "; 
    printLinkedList(head); 

    // Number of elements to be appended 
    int k = 7; 

    // Function call 
    appendAtFront(head, tail, n, k);  

    // Printing linked list after appending the list 
    cout << "Linked List after appending "<<k<<" elements: "; 
    printLinkedList(head);  
} 

```

**Output:**

```
Linked List before appending: 1 2 3 4 5 6 
Linked List after appending 7 elements: 6 1 2 3 4 5 

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。