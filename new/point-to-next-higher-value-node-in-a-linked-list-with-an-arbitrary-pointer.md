# 使用任意指针指向链表中的下一个较高值的节点

给定单链表，每个节点都有一个额外的“任意”指针，该指针当前指向 NULL。 需要使“任意”指针指向下一个较高值的节点。

[![listwithArbit](img/8169f1fd5a3a7a6cf9da279cda5846a5.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/listwithArbit1.png)

**我们强烈建议您最小化您的浏览器，然后先尝试一下。**

一种**简单解决方案**是一个遍历所有节点，对于每个节点，查找当前节点中具有下一个更大值的节点，并更改下一个指针。 该解决方案的时间复杂度为 O（n <sup>2</sup> ）。

有效的**解决方案**的工作时间为 O（nLogn）。 这个想法是对链接列表使用[合并排序。

1）遍历输入列表，并将下一个指针复制到每个节点的仲裁指针。

2）对由仲裁指针形成的链表进行合并排序。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

以下是上述想法的实现。 所有合并排序功能均取自[这里](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)。 在此修改了采用的函数，以便它们在仲裁指针上工作，而不是在下一个指针上工作。

## C++

```cpp

// C++ program to populate arbit pointers  
// to next higher value using merge sort  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
class Node  
{  
    public: 
    int data;  
    Node* next, *arbit;  
};  

/* function prototypes */
Node* SortedMerge(Node* a, Node* b);  
void FrontBackSplit(Node* source,  
                    Node** frontRef, Node** backRef);  

/* sorts the linked list formed by arbit pointers  
(does not change next pointer or data) */
void MergeSort(Node** headRef)  
{  
    Node* head = *headRef;  
    Node* a, *b;  

    /* Base case -- length 0 or 1 */
    if ((head == NULL) || (head->arbit == NULL))  
        return;  

    /* Split head into 'a' and 'b' sublists */
    FrontBackSplit(head, &a, &b);  

    /* Recursively sort the sublists */
    MergeSort(&a);  
    MergeSort(&b);  

    /* answer = merge the two sorted lists together */
    *headRef = SortedMerge(a, b);  
}  

/* See https://www.geeksforgeeks.org/?p=3622 for   
details of this function */
Node* SortedMerge(Node* a, Node* b)  
{  
    Node* result = NULL;  

    /* Base cases */
    if (a == NULL)  
        return (b);  
    else if (b == NULL)  
        return (a);  

    /* Pick either a or b, and recur */
    if (a->data <= b->data)  
    {  
        result = a;  
        result->arbit = SortedMerge(a->arbit, b);  
    }  
    else
    {  
        result = b;  
        result->arbit = SortedMerge(a, b->arbit);  
    }  

    return (result);  
}  

/* Split the nodes of the given list into front  
and back halves, and return the two lists using  
the reference parameters. If the length is odd,  
the extra node should go in the front list.  
Uses the fast/slow pointer strategy. */
void FrontBackSplit(Node* source,  
                    Node** frontRef, Node** backRef)  
{  
    Node* fast, *slow;  

    if (source == NULL || source->arbit == NULL)  
    {  
        /* length < 2 cases */
        *frontRef = source;  
        *backRef = NULL;  
        return;  
    }  

    slow = source, fast = source->arbit;  

    /* Advance 'fast' two nodes, and  
    advance 'slow' one node */
    while (fast != NULL)  
    {  
        fast = fast->arbit;  
        if (fast != NULL)  
        {  
            slow = slow->arbit;  
            fast = fast->arbit;  
        }  
    }  

    /* 'slow' is before the midpoint in the list,  
     so split it in two at that point. */
    *frontRef = source;  
    *backRef = slow->arbit;  
    slow->arbit = NULL;  
}  

/* Function to insert a node at the 
beginging of the linked list */
void push(Node** head_ref, int new_data)  
{  
    /* allocate node */
    Node* new_node = new Node(); 

    /* put in the data */
    new_node->data = new_data;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    new_node->arbit = NULL;  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

// Utility function to print result linked list  
void printListafter(Node *node, Node *anode)  
{  
    cout<<"Traversal using Next Pointer\n";  
    while (node!=NULL)  
    {  
        cout << node->data << ", ";  
        node = node->next;  
    }  

    printf("\nTraversal using Arbit Pointer\n");  
    while (anode!=NULL)  
    {  
        cout << anode->data << ", ";  
        anode = anode->arbit;  
    }  
}  

// This function populates arbit pointer in every node to the  
// next higher value. And returns pointer to the node with  
// minimum value  
Node* populateArbit(Node *head)  
{  
    // Copy next pointers to arbit pointers  
    Node *temp = head;  
    while (temp != NULL)  
    {  
        temp->arbit = temp->next;  
        temp = temp->next;  
    }  

    // Do merge sort for arbitrary pointers  
    MergeSort(&head);  

    // Return head of arbitrary pointer linked list  
    return head;  
}  

/* Driver program to test above functions*/
int main()  
{  
    /* Start with the empty list */
    Node* head = NULL;  

    /* Let us create the list shown above */
    push(&head, 3);  
    push(&head, 2);  
    push(&head, 10);  
    push(&head, 5);  

    /* Sort the above created Linked List */
    Node *ahead = populateArbit(head);  

    cout << "Result Linked List is: \n";  
    printListafter(head, ahead);  
    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to populate arbit pointers to next higher value 
// using merge sort 
#include<stdio.h> 
#include<stdlib.h> 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node* next, *arbit; 
}; 

/* function prototypes */
struct Node* SortedMerge(struct Node* a, struct Node* b); 
void FrontBackSplit(struct Node* source, 
                    struct Node** frontRef, struct Node** backRef); 

/* sorts the linked list formed by arbit pointers 
  (does not change next pointer or data) */
void MergeSort(struct Node** headRef) 
{ 
    struct Node* head = *headRef; 
    struct Node* a, *b; 

    /* Base case -- length 0 or 1 */
    if ((head == NULL) || (head->arbit == NULL)) 
        return; 

    /* Split head into 'a' and 'b' sublists */
    FrontBackSplit(head, &a, &b); 

    /* Recursively sort the sublists */
    MergeSort(&a); 
    MergeSort(&b); 

    /* answer = merge the two sorted lists together */
    *headRef = SortedMerge(a, b); 
} 

/* See https://www.geeksforgeeks.org/?p=3622 for details of this 
   function */
struct Node* SortedMerge(struct Node* a, struct Node* b) 
{ 
    struct Node* result = NULL; 

    /* Base cases */
    if (a == NULL) 
        return (b); 
    else if (b==NULL) 
        return (a); 

    /* Pick either a or b, and recur */
    if (a->data <= b->data) 
    { 
        result = a; 
        result->arbit = SortedMerge(a->arbit, b); 
    } 
    else
    { 
        result = b; 
        result->arbit = SortedMerge(a, b->arbit); 
    } 

    return (result); 
} 

/* Split the nodes of the given list into front and back halves, 
   and return the two lists using the reference parameters. 
   If the length is odd, the extra node should go in the front list. 
   Uses the fast/slow pointer strategy.  */
void FrontBackSplit(struct Node* source, 
                    struct Node** frontRef, struct Node** backRef) 
{ 
    struct Node* fast, *slow; 

    if (source==NULL || source->arbit==NULL) 
    { 
        /* length < 2 cases */
        *frontRef = source; 
        *backRef = NULL; 
        return; 
    } 

    slow = source,  fast = source->arbit; 

    /* Advance 'fast' two nodes, and advance 'slow' one node */
    while (fast != NULL) 
    { 
        fast = fast->arbit; 
        if (fast != NULL) 
        { 
            slow = slow->arbit; 
            fast = fast->arbit; 
        } 
    } 

    /* 'slow' is before the midpoint in the list, so split it in two 
      at that point. */
    *frontRef = source; 
    *backRef = slow->arbit; 
    slow->arbit = NULL; 
} 

/* Function to insert a node at the beginging of the linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = 
        (struct Node*) malloc(sizeof(struct Node)); 

    /* put in the data  */
    new_node->data  = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    new_node->arbit = NULL; 

    /* move the head to point to the new node */
    (*head_ref)    = new_node; 
} 

// Utility function to print result linked list 
void printListafter(struct Node *node, struct Node *anode) 
{ 
    printf("Traversal using Next Pointer\n"); 
    while (node!=NULL) 
    { 
        printf("%d, ", node->data); 
        node = node->next; 
    } 

    printf("\nTraversal using Arbit Pointer\n"); 
    while (anode!=NULL) 
    { 
        printf("%d, ", anode->data); 
        anode = anode->arbit; 
    } 
} 

// This function populates arbit pointer in every node to the 
// next higher value. And returns pointer to the node with 
// minimum value 
struct Node* populateArbit(struct Node *head) 
{ 
    // Copy next pointers to arbit pointers 
    struct Node *temp = head; 
    while (temp != NULL) 
    { 
        temp->arbit = temp->next; 
        temp = temp->next; 
    } 

    // Do merge sort for arbitrary pointers 
    MergeSort(&head); 

    // Return head of arbitrary pointer linked list 
    return head; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Let us create the list shown above */
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 10); 
    push(&head, 5); 

    /* Sort the above created Linked List */
    struct Node *ahead = populateArbit(head); 

    printf("\nResult Linked List is: \n"); 
    printListafter(head, ahead); 

    getchar(); 
    return 0; 
} 

```

## Java

```java

// Java program to populate arbit pointers  
// to next higher value using merge sort 
class LinkedList 
{ 

    static Node head; 

    /* Link list node */
    static class Node 
    { 
        int data; 
        Node next, arbit; 

        Node(int data)  
        { 
            this.data = data; 
            next = null; 
            arbit = null; 
        } 
    } 

    // Utility function to print result linked list 
    void printList(Node node, Node anode) 
    { 
        System.out.println("Traversal using Next Pointer"); 
        while (node != null) 
        { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 

        System.out.println("\nTraversal using Arbit Pointer"); 
        while (anode != null) 
        { 
            System.out.print(anode.data + " "); 
            anode = anode.arbit; 
        } 
    } 

    // This function populates arbit pointer in every node to the  
    // next higher value. And returns pointer to the node with  
    // minimum value 
    private Node populateArbit(Node start) 
    { 

        Node temp = start; 

        // Copy next pointers to arbit pointers 
        while (temp != null) 
        { 
            temp.arbit = temp.next; 
            temp = temp.next; 
        } 

        // Do merge sort for arbitrary pointers and 
        // return head of arbitrary pointer linked list 
        return MergeSort(start); 
    } 

    /* sorts the linked list formed by arbit pointers  
    (does not change next pointer or data) */
    private Node MergeSort(Node start) 
    { 

        /* Base case -- length 0 or 1 */
        if (start == null || start.arbit == null) 
        { 
            return start; 
        } 

        /* Split head into 'middle' and 'nextofmiddle' sublists */
        Node middle = getMiddle(start); 
        Node nextofmiddle = middle.arbit; 

        middle.arbit = null; 

        /* Recursively sort the sublists */
        Node left = MergeSort(start); 
        Node right = MergeSort(nextofmiddle); 

        /* answer = merge the two sorted lists together */
        Node sortedlist = SortedMerge(left, right); 

        return sortedlist; 
    } 

    // Utility function to get the middle of the linked list 
    private Node getMiddle(Node source) 
    { 
        // Base case 
        if (source == null) 
            return source; 
        Node fastptr = source.arbit; 
        Node slowptr = source; 

        // Move fastptr by two and slow ptr by one  
        // Finally slowptr will point to middle node 
        while (fastptr != null) 
        { 
            fastptr = fastptr.arbit; 
            if (fastptr != null) 
            { 
                slowptr = slowptr.arbit; 
                fastptr = fastptr.arbit; 
            } 
        } 
        return slowptr; 
    } 

    private Node SortedMerge(Node a, Node b) 
    { 
        Node result = null; 

        /* Base cases */
        if (a == null) 
            return b; 
        else if (b == null) 
            return a; 

        /* Pick either a or b, and recur */
        if (a.data <= b.data) 
        { 
            result = a; 
            result.arbit = SortedMerge(a.arbit, b); 
        } 
        else
        { 
            result = b; 
            result.arbit = SortedMerge(a, b.arbit); 
        } 

        return result; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        LinkedList list = new LinkedList(); 

        /* Let us create the list shown above */
        list.head = new Node(5); 
        list.head.next = new Node(10); 
        list.head.next.next = new Node(2); 
        list.head.next.next.next = new Node(3); 

        /* Sort the above created Linked List */
        Node ahead = list.populateArbit(head); 

        System.out.println("Result Linked List is:"); 
        list.printList(head, ahead); 
    } 
} 

// This code is contributed by shubham96301     

```

## C#

```cs

// C# program to populate arbit pointers  
// to next higher value using merge sort 
using System; 
public class LinkedList 
{ 

    public Node head; 

    /* Link list node */
    public class Node 
    { 
        public int data; 
        public Node next, arbit; 

        public Node(int data)  
        { 
            this.data = data; 
            next = null; 
            arbit = null; 
        } 
    } 

    // Utility function to print result linked list 
    void printList(Node node, Node anode) 
    { 
        Console.WriteLine("Traversal using Next Pointer"); 
        while (node != null) 
        { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 

        Console.WriteLine("\nTraversal using Arbit Pointer"); 
        while (anode != null) 
        { 
            Console.Write(anode.data + " "); 
            anode = anode.arbit; 
        } 
    } 

    // This function populates arbit pointer in every node to the  
    // next higher value. And returns pointer to the node with  
    // minimum value 
    private Node populateArbit(Node start) 
    { 

        Node temp = start; 

        // Copy next pointers to arbit pointers 
        while (temp != null) 
        { 
            temp.arbit = temp.next; 
            temp = temp.next; 
        } 

        // Do merge sort for arbitrary pointers and 
        // return head of arbitrary pointer linked list 
        return MergeSort(start); 
    } 

    /* sorts the linked list formed by arbit pointers  
    (does not change next pointer or data) */
    private Node MergeSort(Node start) 
    { 

        /* Base case -- length 0 or 1 */
        if (start == null || start.arbit == null) 
        { 
            return start; 
        } 

        /* Split head into 'middle' and 'nextofmiddle' sublists */
        Node middle = getMiddle(start); 
        Node nextofmiddle = middle.arbit; 

        middle.arbit = null; 

        /* Recursively sort the sublists */
        Node left = MergeSort(start); 
        Node right = MergeSort(nextofmiddle); 

        /* answer = merge the two sorted lists together */
        Node sortedlist = SortedMerge(left, right); 

        return sortedlist; 
    } 

    // Utility function to get the middle of the linked list 
    private Node getMiddle(Node source) 
    { 
        // Base case 
        if (source == null) 
            return source; 
        Node fastptr = source.arbit; 
        Node slowptr = source; 

        // Move fastptr by two and slow ptr by one  
        // Finally slowptr will point to middle node 
        while (fastptr != null) 
        { 
            fastptr = fastptr.arbit; 
            if (fastptr != null) 
            { 
                slowptr = slowptr.arbit; 
                fastptr = fastptr.arbit; 
            } 
        } 
        return slowptr; 
    } 

    private Node SortedMerge(Node a, Node b) 
    { 
        Node result = null; 

        /* Base cases */
        if (a == null) 
            return b; 
        else if (b == null) 
            return a; 

        /* Pick either a or b, and recur */
        if (a.data <= b.data) 
        { 
            result = a; 
            result.arbit = SortedMerge(a.arbit, b); 
        } 
        else
        { 
            result = b; 
            result.arbit = SortedMerge(a, b.arbit); 
        } 

        return result; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        LinkedList list = new LinkedList(); 

        /* Let us create the list shown above */
        list.head = new Node(5); 
        list.head.next = new Node(10); 
        list.head.next.next = new Node(2); 
        list.head.next.next.next = new Node(3); 

        /* Sort the above created Linked List */
        Node ahead = list.populateArbit(list.head); 

        Console.WriteLine("Result Linked List is:"); 
        list.printList(list.head, ahead); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Result Linked List is:
Traversal using Next Pointer
5, 10, 2, 3,
Traversal using Arbit Pointer
2, 3, 5, 10,
```

本文由 **Saurabh Bansal** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

