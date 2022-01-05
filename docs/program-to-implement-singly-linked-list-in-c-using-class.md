# 用类

在 C++中实现单链表的程序

> 原文:[https://www . geesforgeks . org/program-to-implement-single-link-list-in-c-use-class/](https://www.geeksforgeeks.org/program-to-implement-singly-linked-list-in-c-using-class/)

[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)将数据存储在顺序存储器中，就像[数组](https://www.geeksforgeeks.org/array-data-structure/)一样。虽然数据是按顺序存储的，但存储位置并不连续。
与数组不同，链表可以存储不同数据类型的数据。
下图为链表结构。

[![](img/d97a233bf3c89e80c46e6a3193e851d6.png)](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)

在 C++中，链表可以分别用一个类和一个 **Node** 类来表示，后者有两个成员，即数据和指向下一个节点的 **next** 指针。

**<u>插入节点</u>** :本文中[的插入是在列表](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的末尾完成的。按照步骤在链表中插入一个节点。

*   假设 **4** 要插入到已有的链表上，即 **1 - > 2 - > 3** 。生成的链表将是 **1 - > 2 - > 3 - > 4。**
*   [插入新的节点遍历，直到列表结束，直到找到空节点。](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)
*   创建一个新节点，并将该新节点链接到链表的最后一个节点。

**<u>删除节点</u>** :在本文中，[的删除是使用节点的**索引**完成的。按照以下步骤删除节点:](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)

*   如果要删除的节点是头节点，将**头**存储在**温度**变量中。然后更新**头像**为**头像- >下一个**。删除**温度**。
*   如果要删除的节点的索引大于列表的长度，则从函数返回。
*   [遍历直到要删除的节点。删除该节点，并将前一个节点链接到被删除节点的下一个节点。](https://www.geeksforgeeks.org/in-a-linked-list-given-only-a-pointer-to-a-node-to-be-deleted-in-a-singly-linked-list-how-do-you-delete-it/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Node class to represent
// a node of the linked list.
class Node {
public:
    int data;
    Node* next;

    // Default constructor
    Node()
    {
        data = 0;
        next = NULL;
    }

    // Parameterised Constructor
    Node(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};

// Linked list class to
// implement a linked list.
class Linkedlist {
    Node* head;

public:
    // Default constructor
    Linkedlist() { head = NULL; }

    // Function to insert a
    // node at the end of the
    // linked list.
    void insertNode(int);

    // Function to print the
    // linked list.
    void printList();

    // Function to delete the
    // node at given position
    void deleteNode(int);
};

// Function to delete the
// node at given position
void Linkedlist::deleteNode(int nodeOffset)
{
    Node *temp1 = head, *temp2 = NULL;
    int ListLen = 0;

    if (head == NULL) {
        cout << "List empty." << endl;
        return;
    }

    // Find length of the linked-list.
    while (temp1 != NULL) {
        temp1 = temp1->next;
        ListLen++;
    }

    // Check if the position to be
    // deleted is less than the length
    // of the linked list.
    if (ListLen < nodeOffset) {
        cout << "Index out of range"
             << endl;
        return;
    }

    // Declare temp1
    temp1 = head;

    // Deleting the head.
    if (nodeOffset == 1) {

        // Update head
        head = head->next;
        delete temp1;
        return;
    }

    // Traverse the list to
    // find the node to be deleted.
    while (nodeOffset-- > 1) {

        // Update temp2
        temp2 = temp1;

        // Update temp1
        temp1 = temp1->next;
    }

    // Change the next pointer
    // of the previous node.
    temp2->next = temp1->next;

    // Delete the node
    delete temp1;
}

// Function to insert a new node.
void Linkedlist::insertNode(int data)
{
    // Create the new Node.
    Node* newNode = new Node(data);

    // Assign to head
    if (head == NULL) {
        head = newNode;
        return;
    }

    // Traverse till end of list
    Node* temp = head;
    while (temp->next != NULL) {

        // Update temp
        temp = temp->next;
    }

    // Insert at the last.
    temp->next = newNode;
}

// Function to print the
// nodes of the linked list.
void Linkedlist::printList()
{
    Node* temp = head;

    // Check for empty list.
    if (head == NULL) {
        cout << "List empty" << endl;
        return;
    }

    // Traverse the list.
    while (temp != NULL) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Driver Code
int main()
{
    Linkedlist list;

    // Inserting nodes
    list.insertNode(1);
    list.insertNode(2);
    list.insertNode(3);
    list.insertNode(4);

    cout << "Elements of the list are: ";

    // Print the list
    list.printList();
    cout << endl;

    // Delete node at position 2.
    list.deleteNode(2);

    cout << "Elements of the list are: ";
    list.printList();
    cout << endl;
    return 0;
}
```

**Output**

```
Elements of the list are: 1 2 3 4 
Elements of the list are: 1 3 4 

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)