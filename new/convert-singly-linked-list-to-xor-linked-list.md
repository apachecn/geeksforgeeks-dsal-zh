# 将单链接列表转换为 XOR 链接列表

**前提条件**：

*   [XOR 链表–内存有效的双链表 | 系列 1](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-1/)

*   [XOR 链表–内存有效的双链表 | 系列 2](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)

**XOR 链接列表**是一种内存有效的双向链接列表，其中每个节点的下一个指针存储上一个和下一个节点的地址的 XOR。

给定一个单链表，任务是将给定的单链表转换为 XOR 链表。

**方法**：由于在 **XOR** 链表中，每个下一个指针都存储**上一个**的 **XOR** 和下一个节点的**。 因此，想法是遍历给定的单链表，并在指针 *prev* 中跟踪先前的节点。**

现在，遍历列表时，将每个节点的下一个指针更改为：

```
current -> next = XOR(prev, current->next) 

```

**打印 XOR 链接列表**：

在打印 XOR 链接列表时，我们每次必须找到下一个节点的确切地址。 正如我们在上面看到的，每个节点的下一个指针存储 prev 与下一个节点的地址的 XOR 值。 因此，可以通过在 XOR 链接列表中找到 prev 的 XOR 和当前节点的 next 指针来获得下一个节点的地址。

因此，要打印 XOR 链接列表，请通过维护存储上一个节点地址的 prev 指针来遍历它，并找到下一个节点，计算 prev 与当前节点的下一个 XOR。

下面是上述方法的实现：

```

// C++ program to Convert a Singly Linked 
// List to XOR Linked List 

#include <bits/stdc++.h> 

using namespace std; 

// Linked List node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Utiltity function to create new node 
Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 

    return temp; 
} 

// Print singly linked list before conversion 
void print(Node* head) 
{ 
    while (head) { 

        // print current node 
        cout << head->data << " "; 
        head = head->next; 
    } 

    cout << endl; 
} 

// Function to find XORed value of 
// the node addresses 
Node* XOR(Node* a, Node* b) 
{ 
    return (Node*)((uintptr_t)(a) ^ (uintptr_t)(b)); 
} 

// Function to convert singly linked 
// list to XOR linked list 
void convert(Node* head) 
{ 
    Node* curr = head; 
    Node* prev = NULL; 
    Node* next = curr->next; 

    while (curr) { 

        // store curr->next in next 
        next = curr->next; 

        // cahnge curr->next to XOR of prev and next 
        curr->next = XOR(prev, next); 

        // prev wil change to curr for next iteration 
        prev = curr; 

        // curr is now pointing to next for next iteration 
        curr = next; 
    } 
} 

// Function to print XORed liked list 
void printXOR(Node* head) 
{ 
    Node* curr = head; 
    Node* prev = NULL; 

    while (curr) { 

        // print current node 
        cout << curr->data << " "; 

        Node* temp = curr; 

        /* compute curr as prev^curr->next as 
           it is previously set as prev^curr->next so 
           this time curr would be prev^prev^curr->next  
           which is curr->next */
        curr = XOR(prev, curr->next); 

        prev = temp; 
    } 

    cout << endl; 
} 

// Driver Code 
int main() 
{ 
    // Create following singly linked list 
    // 1->2->3->4 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 

    cout << "Before Conversion : " << endl; 
    print(head); 

    convert(head); 
    cout << "After Conversion : " << endl; 
    printXOR(head); 

    return 0; 
} 

```

**Output:**

```
Before Conversion : 
1 2 3 4 
After Conversion : 
1 2 3 4

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。