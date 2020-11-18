# 链表

的迭代合并排序

给定一个整数的单链列表，任务是使用迭代合并排序对其进行排序。

![](img/30e3fe49cc11f92ab4b7277b9fee727d.png)

合并排序通常是对链表进行排序的首选。 这里在中讨论[。 但是，上面讨论的方法使用堆栈来存储递归调用。 如果要排序的链表太大，可能会占用大量内存。 因此，本文讨论了一种用于合并排序的纯迭代方法，无需递归调用。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

在这篇文章中，我们使用合并排序的自底向上方法。 我们知道合并排序首先合并两个项目，然后合并四个项目，依此类推。 想法是使用整数变量存储间隙，以找到需要对链表进行排序的中点。 因此问题减少到合并在中讨论的两个排序的链表。 但是，我们不使用其他列表来保留合并列表。 相反，我们将列表合并到自身中。 间隔在每次迭代中按指数递增2，然后重复该过程。

## C ++

```

// Iterative C++ program to do merge sort on  
// linked list 
#include <iostream> 
using namespace std; 

/* Structure of the Node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to calculate length of linked list */
int length(struct Node* current) 
{ 
    int count = 0; 
    while (current != NULL) { 
        current = current->next; 
        count++; 
    } 
    return count; 
} 

/* Merge function of Merge Sort to Merge the two sorted parts 
   of the Linked List. We compare the next value of start1 and  
   current value of start2 and insert start2 after start1 if  
   it's smaller than next value of start1\. We do this until 
   start1 or start2 end. If start1 ends, then we assign next  
   of start1 to start2 because start2 may have some elements 
   left out which are greater than the last value of start1.  
   If start2 ends then we assign end2 to end1\. This is necessary 
   because we use end2 in another function (mergeSort function)  
   to determine the next start1 (i.e) start1 for next 
   iteration = end2->next */
void merge(struct Node** start1, struct Node** end1,  
          struct Node** start2, struct Node** end2) 
{ 

    // Making sure that first node of second 
    // list is higher. 
    struct Node* temp = NULL; 
    if ((*start1)->data > (*start2)->data) { 
        swap(*start1, *start2); 
        swap(*end1, *end2); 
    } 

    // Merging remaining nodes 
    struct Node* astart = *start1, *aend = *end1; 
    struct Node* bstart = *start2, *bend = *end2; 
    struct Node* bendnext = (*end2)->next; 
    while (astart != aend && bstart != bendnext) { 
        if (astart->next->data > bstart->data) { 
            temp = bstart->next; 
            bstart->next = astart->next; 
            astart->next = bstart; 
            bstart = temp; 
        } 
        astart = astart->next; 
    } 
    if (astart == aend) 
        astart->next = bstart; 
    else
        *end2 = *end1; 
} 

/* MergeSort of Linked List 
   The gap is initially 1\. It is incremented as  
   2, 4, 8, .. until it reaches the length of the  
   linked list. For each gap, the linked list is  
   sorted around the gap.  
   The prevend stores the address of the last node after 
   sorting a part of linked list so that it's next node 
   can be assigned after sorting the succeeding list.  
   temp is used to store the next start1 because after  
   sorting, the last node will be different. So it  
   is necessary to store the address of start1 before  
   sorting. We select the start1, end1, start2, end2 for  
   sorting. start1 - end1 may be considered as a list  
   and start2 - end2 may be considered as another list  
   and we are merging these two sorted list in merge  
   function and assigning the starting address to the  
   previous end address. */
void mergeSort(struct Node** head) 
{ 
    if (*head == NULL) 
        return; 
    struct Node* start1 = NULL, *end1 = NULL; 
    struct Node* start2 = NULL, *end2 = NULL; 
    struct Node* prevend = NULL; 
    int len = length(*head); 

    for (int gap = 1; gap < len; gap = gap*2) { 
        start1 = *head; 
        while (start1) { 

            // If this is first iteration 
            bool isFirstIter = 0; 
            if (start1 == *head) 
                isFirstIter = 1; 

            // First part for merging 
            int counter = gap; 
            end1 = start1; 
            while (--counter && end1->next) 
                end1 = end1->next; 

            // Second part for merging 
            start2 = end1->next; 
            if (!start2) 
                break; 
            counter = gap; 
            end2 = start2; 
            while (--counter && end2->next) 
                end2 = end2->next; 

            // To store for next iteration. 
            Node *temp = end2->next; 

            // Merging two parts. 
            merge(&start1, &end1, &start2, &end2); 

            // Update head for first iteration, else 
            // append after previous list 
            if (isFirstIter) 
                *head = start1; 
            else
                prevend->next = start1; 

            prevend = end2; 
            start1 = temp; 
        } 
        prevend->next = start1; 
    } 
} 

/* Function to print the Linked List */
void print(struct Node** head) 
{ 
    if ((*head) == NULL) 
        return; 
    struct Node* temp = *head; 
    while (temp != NULL) { 
        printf("%d ", temp->data); 
        temp = temp->next; 
    } 
    printf("\n"); 
} 

/* Given a reference (pointer to    
   pointer) to the head of a list   
   and an int, push a new node on   
   the front of the list. */
void push(struct Node** head_ref,  
          int new_data)  
{  
    struct Node* new_node = new Node;  
    new_node->data = new_data;  
    new_node->next = (*head_ref);  
    (*head_ref) = new_node;  
}    

int main() 
{ 
    // start with empty list  
    struct Node* head = NULL;  

    // create linked list  
    // 1->2->3->4->5->6->7  
    push(&head, 7);  
    push(&head, 6);  
    push(&head, 5);  
    push(&head, 4);  
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 1);  

    mergeSort(&head); 

    print(&head); 
} 

```

## 爪哇

```

// Iterative Java program to do merge sort on  
// linked list 
class GFG 
{ 

/* Structure of the Node */
static class Node 
{ 
    int data; 
    Node next; 
}; 

/* Function to calculate length of linked list */
static int length(Node current) 
{ 
    int count = 0; 
    while (current != null) 
    { 
        current = current.next; 
        count++; 
    } 
    return count; 
} 

/* Merge function of Merge Sort to Merge the two sorted parts 
of the Linked List. We compare the next value of start1 and  
current value of start2 and insert start2 after start1 if  
it's smaller than next value of start1\. We do this until 
start1 or start2 end. If start1 ends, then we assign next  
of start1 to start2 because start2 may have some elements 
left out which are greater than the last value of start1.  
If start2 ends then we assign end2 to end1\. This is necessary 
because we use end2 in another function (mergeSort function)  
to determine the next start1 (i.e) start1 for next 
iteration = end2.next */
static Node merge(Node start1, Node end1,  
        Node start2, Node end2) 
{ 

    // Making sure that first node of second 
    // list is higher. 
    Node temp = null; 
    if ((start1).data > (start2).data)  
    { 
        Node t = start1; 
        start1 = start2; 
        start2 = t; 
        t = end1; 
        end1 = end2; 
        end2 = t; 
    } 

    // Merging remaining nodes 
    Node astart = start1, aend = end1; 
    Node bstart = start2, bend = end2; 
    Node bendnext = (end2).next; 
    while (astart != aend && bstart != bendnext) 
    { 
        if (astart.next.data > bstart.data) 
        { 
            temp = bstart.next; 
            bstart.next = astart.next; 
            astart.next = bstart; 
            bstart = temp; 
        } 
        astart = astart.next; 
    } 
    if (astart == aend) 
        astart.next = bstart; 
    else
        end2 = end1; 

        return start1; 
} 

/* MergeSort of Linked List 
The gap is initially 1\. It is incremented as  
2, 4, 8, .. until it reaches the length of the  
linked list. For each gap, the linked list is  
sorted around the gap.  
The prevend stores the address of the last node after 
sorting a part of linked list so that it's next node 
can be assigned after sorting the succeeding list.  
temp is used to store the next start1 because after  
sorting, the last node will be different. So it  
is necessary to store the address of start1 before  
sorting. We select the start1, end1, start2, end2 for  
sorting. start1 - end1 may be considered as a list  
and start2 - end2 may be considered as another list  
and we are merging these two sorted list in merge  
function and assigning the starting address to the  
previous end address. */
static Node mergeSort(Node head) 
{ 
    if (head == null) 
        return head; 
    Node start1 = null, end1 = null; 
    Node start2 = null, end2 = null; 
    Node prevend = null; 
    int len = length(head); 

    for (int gap = 1; gap < len; gap = gap*2)  
    { 
        start1 = head; 
        while (start1 != null)  
        { 

            // If this is first iteration 
            boolean isFirstIter = false; 
            if (start1 == head) 
                isFirstIter = true; 

            // First part for merging 
            int counter = gap; 
            end1 = start1; 
            while (--counter > 0 && end1.next != null) 
                end1 = end1.next; 

            // Second part for merging 
            start2 = end1.next; 
            if (start2 == null) 
                break; 
            counter = gap; 
            end2 = start2; 
            while (--counter > 0 && end2.next != null) 
                end2 = end2.next; 

            // To store for next iteration. 
            Node temp = end2.next; 

            // Merging two parts. 
            merge(start1, end1, start2, end2); 

            // Update head for first iteration, else 
            // append after previous list 
            if (isFirstIter) 
                head = start1; 
            else
                prevend.next = start1; 

            prevend = end2; 
            start1 = temp; 
        } 
        prevend.next = start1; 
    } 
    return head; 
} 

/* Function to print the Linked List */
static void print(Node head) 
{ 
    if ((head) == null) 
        return; 
    Node temp = head; 
    while (temp != null)  
    { 
        System.out.printf("%d ", temp.data); 
        temp = temp.next; 
    } 
    System.out.printf("\n"); 
} 

/* Given a reference (pointer to  
pointer) to the head of a list  
and an int, push a new node on  
the front of the list. */
static Node push( Node head_ref,  
        int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

public static void main(String args[]) 
{ 
    // start with empty list  
    Node head = null;  

    // create linked list  
    // 1.2.3.4.5.6.7  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    head = mergeSort(head); 

    print(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## C＃

```

// Iterative C# program to do merge sort on  
// linked list 
using System; 
class GFG 
{ 

/* Structure of the Node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

/* Function to calculate length of linked list */
static int length(Node current) 
{ 
    int count = 0; 
    while (current != null) 
    { 
        current = current.next; 
        count++; 
    } 
    return count; 
} 

/* Merge function of Merge Sort to Merge the two sorted parts 
of the Linked List. We compare the next value of start1 and  
current value of start2 and insert start2 after start1 if  
it's smaller than next value of start1\. We do this until 
start1 or start2 end. If start1 ends, then we assign next  
of start1 to start2 because start2 may have some elements 
left out which are greater than the last value of start1.  
If start2 ends then we assign end2 to end1\. This is necessary 
because we use end2 in another function (mergeSort function)  
to determine the next start1 (i.e) start1 for next 
iteration = end2.next */
static Node merge(Node start1, Node end1,  
        Node start2, Node end2) 
{ 

    // Making sure that first node of second 
    // list is higher. 
    Node temp = null; 
    if ((start1).data > (start2).data)  
    { 
        Node t = start1; 
        start1 = start2; 
        start2 = t; 
        t = end1; 
        end1 = end2; 
        end2 = t; 
    } 

    // Merging remaining nodes 
    Node astart = start1, aend = end1; 
    Node bstart = start2, bend = end2; 
    Node bendnext = (end2).next; 
    while (astart != aend && bstart != bendnext) 
    { 
        if (astart.next.data > bstart.data) 
        { 
            temp = bstart.next; 
            bstart.next = astart.next; 
            astart.next = bstart; 
            bstart = temp; 
        } 
        astart = astart.next; 
    } 
    if (astart == aend) 
        astart.next = bstart; 
    else
        end2 = end1; 

        return start1; 
} 

/* MergeSort of Linked List 
The gap is initially 1\. It is incremented as  
2, 4, 8, .. until it reaches the length of the  
linked list. For each gap, the linked list is  
sorted around the gap.  
The prevend stores the address of the last node after 
sorting a part of linked list so that it's next node 
can be assigned after sorting the succeeding list.  
temp is used to store the next start1 because after  
sorting, the last node will be different. So it  
is necessary to store the address of start1 before  
sorting. We select the start1, end1, start2, end2 for  
sorting. start1 - end1 may be considered as a list  
and start2 - end2 may be considered as another list  
and we are merging these two sorted list in merge  
function and assigning the starting address to the  
previous end address. */
static Node mergeSort(Node head) 
{ 
    if (head == null) 
        return head; 
    Node start1 = null, end1 = null; 
    Node start2 = null, end2 = null; 
    Node prevend = null; 
    int len = length(head); 

    for (int gap = 1; gap < len; gap = gap*2)  
    { 
        start1 = head; 
        while (start1 != null)  
        { 

            // If this is first iteration 
            Boolean isFirstIter = false; 
            if (start1 == head) 
                isFirstIter = true; 

            // First part for merging 
            int counter = gap; 
            end1 = start1; 
            while (--counter > 0 && end1.next != null) 
                end1 = end1.next; 

            // Second part for merging 
            start2 = end1.next; 
            if (start2 == null) 
                break; 
            counter = gap; 
            end2 = start2; 
            while (--counter > 0 && end2.next != null) 
                end2 = end2.next; 

            // To store for next iteration. 
            Node temp = end2.next; 

            // Merging two parts. 
            merge(start1, end1, start2, end2); 

            // Update head for first iteration, else 
            // append after previous list 
            if (isFirstIter) 
                head = start1; 
            else
                prevend.next = start1; 

            prevend = end2; 
            start1 = temp; 
        } 
        prevend.next = start1; 
    } 
    return head; 
} 

/* Function to print the Linked List */
static void print(Node head) 
{ 
    if ((head) == null) 
        return; 
    Node temp = head; 
    while (temp != null)  
    { 
        Console.Write( temp.data + " "); 
        temp = temp.next; 
    } 
    Console.Write("\n"); 
} 

/* Given a reference (pointer to  
pointer) to the head of a list  
and an int, push a new node on  
the front of the list. */
static Node push( Node head_ref,  
                    int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

// Driver code 
public static void Main(String []args) 
{ 
    // start with empty list  
    Node head = null;  

    // create linked list  
    // 1.2.3.4.5.6.7  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 5);  
    head = push(head, 4);  
    head = push(head, 3);  
    head = push(head, 2);  
    head = push(head, 1);  

    head = mergeSort(head); 

    print(head); 
} 
} 

// This code is contributed by Arnab Kundu 

```

**Output:**

```
1 2 3 4 5 6 7

```

**时间复杂度：** O（n Log n）
**辅助空间：** O（1）

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。