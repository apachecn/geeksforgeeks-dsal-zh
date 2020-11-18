# 通过更改指针|配对交换链表的相邻节点| 设置2

给定一个单链表，编写一个函数以成对交换元素。

```
Input : 1->2->3->4->5->6->7
Output : 2->1->4->3->6->5->7,

Input : 1->2->3->4->5->6 
Output : 2->1->4->3->6->5
```

已经讨论了一种解决方案 [set 1](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/) 。 这里讨论一个更简单的解决方案。 我们显式地更改前两个节点的指针，然后修复其余的节点。

## C ++

```

/* This program swaps the nodes of linked list  
   rather than swapping the field from the nodes. 
   Imagine a case where a node contains many  
   fields, there will be plenty of unnecessary  
   swap calls. */
#include<bits/stdc++.h> 
using namespace std; 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* Function to pairwise swap elements of a 
   linked list */
Node *pairWiseSwap(Node *head) 
{ 
    // If linked list is empty or there is only 
    // one node in list 
    if (head == NULL || head->next == NULL) 
        return head; 

    // Fix the head and its next explicitly to 
    // avoid many if else in while loop 
    Node *curr = head->next->next; 
    Node *prev = head; 
    head = head->next; 
    head->next = prev; 

    // Fix remaining nodes 
    while (curr != NULL && curr->next != NULL) 
    { 
        prev->next = curr->next; 
        prev = curr; 
        Node *next = curr->next->next; 
        curr->next->next = curr; 
        curr = next; 
    } 

    prev->next = curr; 

    return head; 
} 

/* Function to add a node at the beginning of  
   Linked List */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Druver program to test above function */
int main() 
{ 
    struct Node *start = NULL; 

    /* The constructed linked list is: 
    1->2->3->4->5->6->7 */
    push(&start, 7); 
    push(&start, 6); 
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2);  
    push(&start, 1); 

    printf("\n Linked list before calling pairWiseSwap() "); 
    printList(start); 

    start = pairWiseSwap(start); 

    printf("\n Linked list after calling pairWiseSwap() "); 
    printList(start); 

    return 0; 
} 

```

## 爪哇

```

/* This program swaps the nodes of linked list  
rather than swapping the field from the nodes.  
Imagine a case where a node contains many  
fields, there will be plenty of unnecessary  
swap calls. */
class GfG  
{  

/* A linked list node */
static class Node  
{  
    int data;  
    Node next;  
} 
static Node head = null; 

/* Function to pairwise swap elements of a  
linked list */
static Node pairWiseSwap(Node head)  
{  

    // If linked list is empty or there is only  
    // one node in list  
    if (head == null || head.next == null)  
        return head;  

    // Fix the head and its next explicitly to  
    // avoid many if else in while loop  
    Node curr = head.next.next;  
    Node prev = head;  
    head = head.next;  
    head.next = prev;  

    // Fix remaining nodes  
    while (curr != null && curr.next != null)  
    {  
        prev.next = curr.next;  
        prev = curr;  
        Node next = curr.next.next;  
        curr.next.next = curr;  
        curr = next;  
    }  

    prev.next = curr;  

    return head;  
}  

/* Function to add a node at the  
beginning of Linked List */
static void push(int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head);  
    (head) = new_node;  
}  

/* Function to print nodes in a given linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data + " ");  
        node = node.next;  
    }  
}  

/* Driver code */
public static void main(String[] args)  
{  
    //Node head = null;  

    /* The constructed linked list is:  
    1->2->3->4->5->6->7 */
    push( 7);  
    push( 6);  
    push( 5);  
    push( 4);  
    push(3);  
    push( 2);  
    push( 1);  

    System.out.print("\n Linked list before calling pairWiseSwap() ");  
    printList(head);  

    Node start = pairWiseSwap(head);  

    System.out.print("\n Linked list after calling pairWiseSwap() ");  
    printList(start);  
} 
}  

// This code is contributed by Prerna Saini. 

```

## C＃

```

/* This program swaps the nodes of linked list  
rather than swapping the field from the nodes.  
Imagine a case where a node contains many  
fields, there will be plenty of unnecessary  
swap calls. */
using System; 

class GfG  
{  

/* A linked list node */
class Node  
{  
    public int data;  
    public Node next;  
} 
static Node head = null; 

/* Function to pairwise swap   
elements of a linked list */
static Node pairWiseSwap(Node head)  
{  

    // If linked list is empty or there  
    //  is only one node in list  
    if (head == null || head.next == null)  
        return head;  

    // Fix the head and its next explicitly to  
    // avoid many if else in while loop  
    Node curr = head.next.next;  
    Node prev = head;  
    head = head.next;  
    head.next = prev;  

    // Fix remaining nodes  
    while (curr != null && curr.next != null)  
    {  
        prev.next = curr.next;  
        prev = curr;  
        Node next = curr.next.next;  
        curr.next.next = curr;  
        curr = next;  
    }  

    prev.next = curr;  
    return head;  
}  

/* Function to add a node at the  
beginning of Linked List */
static void push(int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head);  
    (head) = new_node;  
}  

/* Function to print nodes 
in a given linked list */
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(node.data + " ");  
        node = node.next;  
    }  
}  

/* Driver code */
public static void Main()  
{  
    //Node head = null;  

    /* The constructed linked list is:  
    1->2->3->4->5->6->7 */
    push( 7);  
    push( 6);  
    push( 5);  
    push( 4);  
    push(3);  
    push( 2);  
    push( 1);  

    Console.Write("\n Linked list before" + 
                "calling pairWiseSwap() ");  
    printList(head);  

    Node start = pairWiseSwap(head);  

    Console.Write("\n Linked list after" +  
                "calling pairWiseSwap() ");  
    printList(start);  
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Linked list before calling pairWiseSwap() 1 2 3 4 5 6 7 
 Linked list after calling pairWiseSwap() 2 1 4 3 6 5 7

```

另一种方法：

这里的方法是使用双指针，这样我们就不需要在交换期间单独更新头指针。

```

#include <stdio.h>  
#include <stdlib.h>  

// A nexted list node  
struct Node  
{  
    int data;  
    struct Node *next;  
};  

/* Function to insert a node at the beginning */
void push(struct Node ** head_ref, int new_data)  
{  
    struct Node* new_node =  
        (struct Node*) malloc(sizeof(struct Node));  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}  

/* Utility function to print a singly linked list */
void printList(struct Node *head)  
{  
    struct Node *temp = head;  
    while (temp != NULL)  
    {  
        printf("%d ", temp->data);  
        temp = temp->next;  
    }  
    printf("\n");  
}  

// Function to swap adjacent nodes  
void swapPairs(struct Node **head)  
{  
    //Loop until we reach the last node 
    while(*head && (*head)->next)  
    { 
        struct Node *one = *head; 

        struct Node *two = one->next->next; 

        *head = one->next; 

        one->next->next = one; 

        one->next = two; 

        head = &one->next; 
    } 
}  

// Driver program to test above functions  
int main()  
{  
    struct Node *head = NULL;  
    push(&head, 6);  
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3); 
    push(&head, 2);  
    push(&head, 1); 

    printf("Actual List:\n");  
    printList(head);  

    swapPairs(&head);  

    printf("ModifiedLinked List:\n");  
    printList(head);  

    getchar();  
    return 0;  
} 

```

**Output:**

```
Actual List:
1 2 3 4 5 6 
ModifiedLinked List:
2 1 4 3 6 5 

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。