# 在排序和旋转的链表

中计算旋转次数

给定n个节点的链表，该链表首先进行排序，然后旋转k个元素。 找出k的值。

![](img/ed860d112cdefec07c0ee0dcd93c5313.png)

想法是遍历单链表以检查条件，当前节点值是否大于下一个节点的值。 如果给定条件为真，则中断循环。 否则增加计数器变量，并通过node-> next增加节点。 下面是此方法的实现。

```

// Program for count number of rotations in 
// sorted linked list. 
#include <bits/stdc++.h> 
using namespace std; 
/* Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function that count number of 
// rotation in singly linked list. 
int countRotation(struct Node* head) 
{ 
    // declare count variable and assign it 1\. 
    int count = 0; 

    // declare a min variable and assign to 
    // data of head node. 
    int min = head->data; 

    // check that while head not equal to NULL. 
    while (head != NULL) { 

        // if min value is greater then head->data 
        // then it breaks the while loop and 
        // return the value of count. 
        if (min > head->data) 
            break; 

        count++; 

        // head assign the next value of head. 
        head = head->next; 
    } 
    return count; 
} 

// Function to push element in linked list. 
void push(struct Node** head, int data) 
{ 
    // Allocate dynamic memory for newNode. 
    struct Node* newNode = new Node; 

    // Assign the data into newNode. 
    newNode->data = data; 

    // newNode->next assign the address of 
    // head node. 
    newNode->next = (*head); 

    // newNode become the headNode. 
    (*head) = newNode; 
} 

// Display linked list. 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// Driver functions 
int main() 
{ 
    // Create a node and initialize with NULL 
    struct Node* head = NULL; 

    // push() insert node in linked list. 
    // 15 -> 18 -> 5 -> 8 -> 11 -> 12 
    push(&head, 12); 
    push(&head, 11); 
    push(&head, 8); 
    push(&head, 5); 
    push(&head, 18); 
    push(&head, 15); 

    printList(head); 
    cout << endl; 
    cout << "Linked list rotated elements: "; 

    // Function call countRotation() 
    cout << countRotation(head) << endl; 

    return 0; 
} 

```

输出：

```
Linked List:
15 18 5 8 11 12
Linked list rotated elements: 2

```

本文由 **Dharmendra Kumar** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

