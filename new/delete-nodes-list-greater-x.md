# 从列表中删除所有大于x的节点

给定一个链表，问题在于从列表中删除所有大于指定值 **x** 的节点。

例子：

```
Input : list: 7->3->4->8->5->1
        x = 6
Output : 3->4->5->1

Input : list: 1->8->7->3->7->10
        x = 7
Output : 1->7->3->7

```

**来源：** [Microsoft面试经验| 设定169。](https://www.geeksforgeeks.org/microsoft-interview-experience-set-169/)

**方法：**这主要是帖子的一种变体，其中[删除了首次出现的给定密钥。](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)

我们需要首先检查头节点上所有大于“ x”的事件，将其删除并适当地更改头节点。 然后，我们需要检查循环中所有出现的事件，并将它们一一删除。

```

// C++ implementation to delete all the nodes from the list 
// that are greater than the specified value x 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    Node* newNode = new Node; 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to delete all the nodes from the list 
// that are greater than the specified value x 
void deleteGreaterNodes(Node** head_ref, int x) 
{ 
    Node *temp = *head_ref, *prev; 

    // If head node itself holds the value greater than 'x' 
    if (temp != NULL && temp->data > x) { 
        *head_ref = temp->next; // Changed head 
        free(temp); // free old head 
        temp = *head_ref; // Change temp 
    } 

    // Delete occurrences other than head 
    while (temp != NULL) { 

        // Search for the node to be deleted,  
        // keep track of the previous node as we  
        // need to change 'prev->next' 
        while (temp != NULL && temp->data <= x) { 
            prev = temp; 
            temp = temp->next; 
        } 

        // If required value node was not present 
        // in linked list 
        if (temp == NULL) 
            return; 

        // Unlink the node from linked list 
        prev->next = temp->next; 

        delete temp; // Free memory 

        // Update Temp for next iteration of  
        // outer loop 
        temp = prev->next; 
    } 
} 

// function to a print a linked list 
void printList(Node* head) 
{ 
    while (head) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Create list: 7->3->4->8->5->1 
    Node* head = getNode(7); 
    head->next = getNode(3); 
    head->next->next = getNode(4); 
    head->next->next->next = getNode(8); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(1); 

    int x = 6; 

    cout << "Original List: "; 
    printList(head); 

    deleteGreaterNodes(&head, x); 

    cout << "\nModified List: "; 
    printList(head); 

    return 0; 
} 

```

输出：

```
Original List: 7 3 4 8 5 1 
Modified List: 3 4 5 1

```

时间复杂度：O（n）。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。