# 在没有额外空间的单链接中查找给定总和的对

给定一个排序的单链列表和一个值x，任务是找到总和等于x的对。 我们不允许使用任何额外的空间，并且预期的时间复杂度为O（n）。

例子：

```
Input : head = 3-->6-->7-->8-->9-->10-->11 , x=17
Output: (6, 11), (7, 10), (8, 9)

```

提示：我们可以修改原始链表

针对此问题的**简单解决方案**是一个个地取每个元素，并向前遍历其余列表以找到总和等于给定值x的第二个元素。 该方法的时间复杂度将为O（n <sup>2</sup> ）。

针对此问题的**有效解决方案**基于以下文章中讨论的思想。
[在双向链表中查找对：](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)我们使用从两端遍历链表的相同算法。
[XOR链表](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)：在单链表中，我们只能沿向前方向遍历列表。 我们使用XOR概念将单链列表转换为双链列表。

以下是步骤：

*   首先，我们需要将单链列表转换为双链列表。 在这里，我们给出了单链列表结构节点，该节点仅具有**下一个**指针，而没有**上一页**指针，因此，为了将单链列表转换为双链列表，我们使用[内存高效双链 列表（异或链接列表）](https://www.geeksforgeeks.org/xor-linked-list-a-memory-efficient-doubly-linked-list-set-2/)。
*   在XOR链接列表中，单链接列表的每个**下一个**指针都包含**下一个**和 **prev** 指针的XOR。
*   将单链列表转换为双链列表后，我们初始化两个指针变量以在排序的双链列表中找到候选元素。 首先以双向链表的开头初始化；即 **first = head** ，然后用双向链表的最后一个节点初始化**第二**；即 **second = last_node** 。
*   这里我们没有随机访问权限，因此要初始化指针，我们遍历列表直到最后一个节点，并将最后一个节点分配给第二个。
*   如果当前**首先**和**第二**的当前总和小于x，则我们将**首先**向前移动。 如果**第一个**和**第二个**元素的当前总和大于x，则我们将**第二个**向后移动。
*   循环终止条件也与阵列不同。 当两个指针中的任何一个变为NULL或它们彼此交叉（第一个= next_node），或者它们变为相同（第一个==第二个）时，循环终止。

```

// C++ program to find pair with given sum in a singly 
// linked list in O(n) time and no extra space. 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node 
{ 
    int data; 

    /* also constains XOR of next and 
    previous node after conversion*/
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
    of a list and an int, push a new node on the front 
    of the list. */
void insert(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* returns XORed value of the node addresses */
struct Node* XOR (struct Node *a, struct Node *b) 
{ 
    return (struct Node*) ((uintptr_t) (a) ^ (uintptr_t) (b)); 
} 

// Utility function to convert singly linked list 
// into XOR doubly linked list 
void convert(struct Node *head) 
{ 
    // first we store address of next node in it 
    // then take XOR of next node and previous node 
    // and store it in next pointer 
    struct Node *next_node; 

    // prev node stores the address of previously 
    // visited node 
    struct Node *prev = NULL; 

    // traverse list and store xor of address of 
    // next_node and prev node in next pointer of node 
    while (head != NULL) 
    { 
        // address of next node 
        next_node = head->next; 

        // xor of next_node and prev node 
        head->next = XOR(next_node, prev); 

        // update previous node 
        prev = head; 

        // move head forward 
        head = next_node; 
    } 
} 

// function to Find pair whose sum is equal to 
// given value x 
void pairSum(struct Node *head, int x) 
{ 
    // initialize first 
    struct Node *first = head; 

    // next_node and prev node to calculate xor again 
    // and find next and prev node while moving forward 
    // and backward direction from both the corners 
    struct Node *next_node = NULL, *prev = NULL; 

    // traverse list to initialize second pointer 
    // here we need to move in forward direction so to 
    // calculate next address we have to take xor 
    // with prev pointer because (a^b)^b = a 
    struct Node *second = head; 
    while (second->next != prev) 
    { 
        struct Node *temp = second; 
        second = XOR(second->next, prev); 
        prev = temp; 
    } 

    // now traverse from both the corners 
    next_node = NULL; 
    prev = NULL; 

    // here if we want to move forward then we must 
    // know the prev address to calculate next node 
    // and if we want to move backward then we must 
    // know the next_node address to calculate prev node 
    bool flag = false; 
    while (first != NULL && second != NULL && 
            first != second && first != next_node) 
    { 
        if ((first->data + second->data)==x) 
        { 
            cout << "(" << first->data << ","
                 << second->data << ")" << endl; 

            flag = true; 

            // move first in forward 
            struct Node *temp = first; 
            first = XOR(first->next,prev); 
            prev = temp; 

            // move second in backward 
            temp = second; 
            second = XOR(second->next, next_node); 
            next_node = temp; 
        } 
        else
        { 
            if ((first->data + second->data) < x) 
            { 
                // move first in forward 
                struct Node *temp = first; 
                first = XOR(first->next,prev); 
                prev = temp; 
            } 
            else
            { 
                // move second in backward 
                struct Node *temp = second; 
                second = XOR(second->next, next_node); 
                next_node = temp; 
            } 
        } 
    } 
    if (flag == false) 
        cout << "No pair found" << endl; 
} 

// Driver program to run the case 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 
    int x = 17; 

    /* Use insert() to construct below list 
    3-->6-->7-->8-->9-->10-->11 */
    insert(&head, 11); 
    insert(&head, 10); 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 7); 
    insert(&head, 6); 
    insert(&head, 3); 

    // convert singly linked list into XOR doubly 
    // linked list 
    convert(head); 
    pairSum(head,x); 
    return 0; 
} 

```

输出：

```
(6,11) , (7,10) , (8,9)

```

时间复杂度：O（n）

如果未对链接列表进行排序，那么我们可以将列表作为第一步进行排序。 但是在那种情况下，整体时间复杂度将变为O（n Log n）。 如果没有多余的空间，我们可以在这种情况下使用哈希。 基于哈希的解决方案与方法2 [在此处](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)相同。

本文由 **[Shashank Mishra（Gullu）](https://www.facebook.com/shashank.mishra.92167)** 贡献。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

