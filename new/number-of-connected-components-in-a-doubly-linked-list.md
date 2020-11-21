# 双链表

> 原文：[https://www.geeksforgeeks.org/number-of-connected-components-in-a-doubly-linked-list/](https://www.geeksforgeeks.org/number-of-connected-components-in-a-doubly-linked-list/)

中已连接组件的数量

给定一个双向链表“ L”和一个指向双向链表“ L”的节点的引用数组“ refArr”。 数组'refArr'**不包含任何重复的引用**，并且这些引用不是 **ORDERED** 。

m < =总编号 双向链表中的节点数，其中 m =参考数组的大小。

该任务是在链表“ L”中找到已连接组件的总数。

链表“ L”中的“ **连接组件**”被定义为列表中的一组节点，其引用存储在数组“ refArr”中，并且**在其中彼此相邻** 名单。

**示例**：

> **输入**：L = 5 <-> 2 <-> 10 <-> 1 <-> 3，refArr [] = {5 ，，10，3，1}
> **输出**：2
> 两个连接的组件分别是 5 和 10 <-> 1 <-> 3\.
> 2 不包含在参考数组中，这使 5 与其余元素断开连接。
> 
> **输入**：L = 1 <-> 7 <-> 10 <-> 5 <-> 4 <-> 2，refArr [] = {5，2，7，1}
> **输出**：连接的组件总数为 3

**说明**：

> 让我们将双重链表“ L”作为{N1 N2 N3 N4 N5 N6}
> ，将数组“ refArr”作为[ref_to_nodeN1，ref_to_nodeN4，ref_to_nodeN6，ref_to_nodeN2]。
> 
> **输出**：
> 这组数组'refArr'和链表'L'包含 **3 个连接的组件**，它们是{[N1，N2]，[N4]，[N6 ]}。
> 这是因为节点 N1 和 N2 的引用存在于数组“ refArr”中，并且在列表“ L”中彼此相邻，而 N4 和 N6 不与 N1，N2 彼此相邻。 因此，它们形成了单独的组件。
> 
> 现在，将数组“ refArr”修改为[ref_to_nodeN4，ref_to_nodeN6，ref_to_nodeN5]。
> 
> **输出**：
> 这组数组'refArr'和链表'L'包含 **1 个连接的组件**，即{[N4，N5，N6]}。
> 这是因为节点 N4，N5 和 N6 的引用存在于数组“ refArr”中，并且在列表“ L”中彼此相邻。 因此，我们一起形成 1 个连接的组件。

**朴素的方法**：它涉及遍历喜欢列表“ L”的每个节点的数组“ refArr”，并检查该元素是否存在于数组中。 同样，维护一个布尔变量，该变量跟踪链表中的前一个节点是否在数组中。 取一个变量“ cc”，它初始化为 0，并表示 no。 链表中已连接组件的数量。

现在，让我们考虑遍历时发生的多种情况：

*   **情况 1**：如果前一个节点在数组中，并且当前遍历的当前节点也在数组中，则布尔变量将保持为 1，表示当前节点在数组中，但不增加变量' cc'，因为当前节点构成了先前节点已经存在的组件的一部分。

*   **情况 2**：如果上一个节点不在数组中，而当前遍历的节点在数组中，则将布尔变量更新为标记“ 1”，这意味着当前节点在数组中并递增 变量“ cc”加 1，因为当前节点形成一个新组件。

*   **情况 3**：如果前一个节点在数组中，而当前遍历的节点不在数组中，则将布尔变量更新为 0，表示当前节点不在数组中，并且不 因为当前节点不是任何组件的一部分，所以增加变量“ cc”。

*   **情况 4**：如果上一个节点不在数组中，并且当前遍历的节点也在数组中，则布尔变量将保持为 0，表示当前节点不在数组中并且不递增 变量“ cc”，因为当前节点不是任何组件的一部分。

现在，在执行 4 种情况之一之后，移至链表中的下一个节点，并对该节点也执行相同的操作。

**时间复杂度**：O（n * m），其中 n =链表“ L”的大小，并且 m =参考数组“ refArr”的大小。

**空间复杂度：`O(1)`**

**更好的方法**：该方法涉及 **unordered_set** 的使用。 使用变量“ connectedComponents”，该变量已初始化为 0。 **connectedComponents 表示链表中已连接组件的数量。**

现在，对于参考数组“ refArr”中的每个元素：

1.  将存储在数组中的引用添加到 unordered_set“ refSet”。

下面是上述方法的实现：

```

// A C++ program to find number  
// of Connected Components in a doubly linked list. 
#include <bits/stdc++.h> 
using namespace std; 

// Node of the doubly linked list 
struct Node { 
    int data; 
    struct Node* next; 
    struct Node* prev; 
}; 

// Function to find number of connected 
// components using a doubly linked list 
// and a reference array 
int func_connComp(struct Node** head_ref, 
                  vector<struct Node*> refArr, int n) 
{ 
    // Base case when the doubly 
    // linked list is empty 
    if (head_ref == NULL) { 
        return 0; 
    } 

    // Initialise connectedComponents to zero 
    int connectedComponents = 0; 

    // Initialise an unordered set 
    unordered_set<struct Node*> refSet; 

    // Push the first element of the 
    // refArr in the refSet and 
    // set the connectedComponents to 1 
    refSet.insert(refArr[0]); 
    connectedComponents++; 

    // Loop over all the elements of the refArr 
    for (int i = 1; i < n; i++) { 

        // insert each reference node to the refSet 
        refSet.insert(refArr[i]); 

        // If the reference node is the head of the linked list 
        if (refArr[i]->prev == NULL) { 

            // when next sibling of the head node is 
            // not in the refSet 
            if (refSet.find(refArr[i]->next) == refSet.end()) { 
                connectedComponents++; 
            } 
        } 

        // If the reference node is the 
        // last node of the linked list*/ 
        else if (refArr[i]->next == NULL) { 

            // when previous sibling of the 
            // node is not in the refSet 
            if (refSet.find(refArr[i]->next) == refSet.end()) { 
                connectedComponents++; 
            } 
        } 

        // the case when both previous and 
        // next siblings of the current node 
        // are in the refSet 
        else if (refSet.find(refArr[i]->prev) != refSet.end() 
                 && refSet.find(refArr[i]->next) != refSet.end()) { 
            connectedComponents--; 
        } 

        /*the case when previous and next  
        // siblings of the current node  
        // are not in the refSet*/
        else if (refSet.find(refArr[i]->prev) == refSet.end() 
                 && refSet.find(refArr[i]->next) == refSet.end()) { 
            connectedComponents++; 
        } 
    } 
    return connectedComponents; 
} 

// Function to insert a node at the 
// beginging of the Doubly Linked List 
Node* push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    struct Node* current_node = new_node; 
    /* put in the data */
    new_node->data = new_data; 

    /* since we are adding at the beginning,  
    prev is always NULL */
    new_node->prev = NULL; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* change prev of head node to new node */
    if ((*head_ref) != NULL) 
        (*head_ref)->prev = new_node; 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 

    return current_node; 
} 

// Function to print nodes in a given 
// doubly linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// Driver code 
int main() 
{ 

    // Start with the empty list 
    struct Node* head = NULL; 

    // Let us create a linked list to test 
    // the functions so as to find number 
    // of Connected Components Created a 
    // doubly linked list: 1 <-> 7 <-> 10 <-> 5 <-> 4 <-> 2 
    struct Node* ref_to_nodeN2 = push(&head, 2); 
    struct Node* ref_to_nodeN4 = push(&head, 4); 
    struct Node* ref_to_nodeN5 = push(&head, 5); 
    struct Node* ref_to_nodeN10 = push(&head, 10); 
    struct Node* ref_to_nodeN7 = push(&head, 7); 
    struct Node* ref_to_nodeN1 = push(&head, 1); 

    vector<struct Node*> refArr{ ref_to_nodeN5, 
                                         ref_to_nodeN2, ref_to_nodeN7, ref_to_nodeN1 }; 

    // This function will return the number 
    // of connected components of doubly linked list 
    int connectedComponents = func_connComp(&head, refArr, 4); 

    cout << "Total number of connected components are "
         << connectedComponents << endl; 

    return 0; 
} 

```

**输出**：

```
Total number of connected components are 3

```

**时间复杂度**：O（m）

**空间复杂度**：O（m）其中，m =参考数组“ refArr”的大小

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。