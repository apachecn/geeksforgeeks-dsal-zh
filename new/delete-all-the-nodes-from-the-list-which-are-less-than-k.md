# 从列表中删除所有小于 K 的节点

> 原文：[https://www.geeksforgeeks.org/delete-all-the-nodes-from-the-list-which-are-less-than-k/](https://www.geeksforgeeks.org/delete-all-the-nodes-from-the-list-which-are-less-than-k/)

给定一个链表和一个密钥 K。任务是编写一个程序，从列表中删除所有小于密钥 K 的节点。

**示例**：

```
Input :12->15->9->11->5->6
        K = 9
Output : 12 -> 15 -> 9 -> 11

Input : 13->4->16->9->22->45->5->16->6
        K = 10
Output : 13 -> 16 -> 22 -> 45 -> 16

```

**方法**：该方法类似于[从列表中删除大于给定密钥](https://www.geeksforgeeks.org/delete-nodes-list-greater-x/)的所有节点。

有两种可能的情况：

1.  头节点的值小于 K：首先检查头节点上所有小于“ K”的事件，然后删除它们并适当地更改头节点。

2.  一些中间节点的值小于 k：从头开始遍历，检查当前节点的值是否小于 K。如果是，则[删除该节点](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)并在列表中前进。

下面是上述方法的实现：

```

// C++ program to delete all the nodes from the list 
// that are lesser than the specified value K 
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
// that are lesser than the specified value K 
void deleteLesserNodes(Node** head_ref, int K) 
{ 
    Node *temp = *head_ref, *prev; 

    // If head node itself holds the value lessser than 'K' 
    while (temp != NULL && temp->data < K) { 
        *head_ref = temp->next; // Changed head 
        free(temp); // free old head 
        temp = *head_ref; // Change temp 
    } 

    // Delete occurrences other than head 
    while (temp != NULL) { 

        // Search for the node to be deleted, 
        // keep track of the previous node as we 
        // need to change 'prev->next' 
        while (temp != NULL && temp->data >= K) { 
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

// Driver code 
int main() 
{ 
    // Create list: 12->15->9->11->5->6 
    Node* head = getNode(12); 
    head->next = getNode(15); 
    head->next->next = getNode(9); 
    head->next->next->next = getNode(11); 
    head->next->next->next->next = getNode(5); 
    head->next->next->next->next->next = getNode(6); 

    int K = 9; 

    cout << "Initial List: "; 
    printList(head); 

    deleteLesserNodes(&head, K); 

    cout << "\nFinal List: "; 
    printList(head); 

    return 0; 
} 

```

**Output:**

```
Initial List: 12 15 9 11 5 6 
Final List: 12 15 9 11

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。