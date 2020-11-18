# 单链接列表

> 原文：[https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/](https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)

上的快速排序

[双链表](https://www.geeksforgeeks.org/quicksort-for-linked-list/)上的 QuickSort 在此处进行了讨论。 练习了单链接列表上的 QuickSort。 以下是相同的 C++实现。 关于实现的重要事项是，它更改指针而不是交换数据，并且时间复杂度与“双链表”的实现相同。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

在 **partition（）**中，我们将最后一个元素视为枢纽。 我们遍历当前列表，如果节点的值大于枢轴，则将其移到尾部之后。 如果节点的值较小，我们将其保持在当前位置。

在 **QuickSortRecur（）**中，我们首先调用 partition（），它将枢轴放置在正确的位置并返回枢轴。 将透视图放置在正确的位置后，我们找到左侧的尾节点（透视图之前的列表）并递归到左侧列表。 最后，我们再次列出正确的清单。

## C++

```cpp

// C++ program for Quick Sort on Singly Linled List 
#include <iostream> 
#include <cstdio> 
using namespace std; 

/* a node of the singly linked list */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

/* A utility function to insert a node at the beginning of linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = new Node; 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* A utility function to print linked list */
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
    printf("\n"); 
} 

// Returns the last node of the list 
struct Node *getTail(struct Node *cur) 
{ 
    while (cur != NULL && cur->next != NULL) 
        cur = cur->next; 
    return cur; 
} 

// Partitions the list taking the last element as the pivot 
struct Node *partition(struct Node *head, struct Node *end, 
                    struct Node **newHead, struct Node **newEnd) 
{ 
    struct Node *pivot = end; 
    struct Node *prev = NULL, *cur = head, *tail = pivot; 

    // During partition, both the head and end of the list might change 
    // which is updated in the newHead and newEnd variables 
    while (cur != pivot) 
    { 
        if (cur->data < pivot->data) 
        { 
            // First node that has a value less than the pivot - becomes 
            // the new head 
            if ((*newHead) == NULL) 
                (*newHead) = cur; 

            prev = cur;  
            cur = cur->next; 
        } 
        else // If cur node is greater than pivot 
        { 
            // Move cur node to next of tail, and change tail 
            if (prev) 
                prev->next = cur->next; 
            struct Node *tmp = cur->next; 
            cur->next = NULL; 
            tail->next = cur; 
            tail = cur; 
            cur = tmp; 
        } 
    } 

    // If the pivot data is the smallest element in the current list, 
    // pivot becomes the head 
    if ((*newHead) == NULL) 
        (*newHead) = pivot; 

    // Update newEnd to the current last node 
    (*newEnd) = tail; 

    // Return the pivot node 
    return pivot; 
} 

//here the sorting happens exclusive of the end node 
struct Node *quickSortRecur(struct Node *head, struct Node *end) 
{ 
    // base condition 
    if (!head || head == end) 
        return head; 

    Node *newHead = NULL, *newEnd = NULL; 

    // Partition the list, newHead and newEnd will be updated 
    // by the partition function 
    struct Node *pivot = partition(head, end, &newHead, &newEnd); 

    // If pivot is the smallest element - no need to recur for 
    // the left part. 
    if (newHead != pivot) 
    { 
        // Set the node before the pivot node as NULL 
        struct Node *tmp = newHead; 
        while (tmp->next != pivot) 
            tmp = tmp->next; 
        tmp->next = NULL; 

        // Recur for the list before pivot 
        newHead = quickSortRecur(newHead, tmp); 

        // Change next of last node of the left half to pivot 
        tmp = getTail(newHead); 
        tmp->next = pivot; 
    } 

    // Recur for the list after the pivot element 
    pivot->next = quickSortRecur(pivot->next, newEnd); 

    return newHead; 
} 

// The main function for quick sort. This is a wrapper over recursive 
// function quickSortRecur() 
void quickSort(struct Node **headRef) 
{ 
    (*headRef) = quickSortRecur(*headRef, getTail(*headRef)); 
    return; 
} 

// Driver program to test above functions 
int main() 
{ 
    struct Node *a = NULL; 
    push(&a, 5); 
    push(&a, 20); 
    push(&a, 4); 
    push(&a, 3); 
    push(&a, 30); 

    cout << "Linked List before sorting \n"; 
    printList(a); 

    quickSort(&a); 

    cout << "Linked List after sorting \n"; 
    printList(a); 

    return 0; 
} 

```

## Java

```java

// Java program for Quick Sort on Singly Linled List 

/*sort a linked list using quick sort*/
public class QuickSortLinkedList  
{ 
static class Node 
{ 
    int data; 
    Node next; 

    Node(int d) 
    { 
        this.data = d; 
        this.next= null; 
    } 
} 

Node head; 

void addNode(int data) 
{ 
    if(head == null) 
    { 
        head = new Node(data); 
        return; 
    } 

    Node curr = head; 
    while(curr.next != null) 
        curr = curr.next; 

    Node newNode = new Node(data); 
    curr.next = newNode; 
} 

void printList(Node n) 
{ 
    while(n != null) 
    { 
        System.out.print(n.data); 
        System.out.print(" "); 
        n = n.next; 
    } 
} 

// takes first and last node, 
// but do not break any links in  
// the whole linked list 
Node paritionLast(Node start, Node end) 
{ 
    if(start == end ||  
       start == null || end == null) 
        return start; 

    Node pivot_prev = start; 
    Node curr = start;  
    int pivot = end.data;  

    // iterate till one before the end,  
    // no need to iterate till the end  
    // because end is pivot 
    while(start != end ) 
    { 
        if(start.data < pivot) 
        {  
            // keep tracks of last modified item 
            pivot_prev = curr;  
            int temp = curr.data;  
            curr.data = start.data;  
            start.data = temp;  
            curr = curr.next;  
        } 
        start = start.next;  
    } 

    // swap the position of curr i.e. 
    // next suitable index and pivot 
    int temp = curr.data;  
    curr.data = pivot;  
    end.data = temp;  

    // return one previous to current 
    // because current is now pointing to pivot 
    return pivot_prev; 
} 

void sort(Node start, Node end) 
{ 
    if(start == end ) 
        return; 

    // split list and partion recurse 
    Node pivot_prev = paritionLast(start, end); 
    sort(start, pivot_prev); 

    // if pivot is picked and moved to the start, 
    // that means start and pivot is same  
    // so pick from next of pivot 
    if( pivot_prev != null &&  
        pivot_prev == start ) 
        sort(pivot_prev.next, end); 

    // if pivot is in between of the list, 
    // start from next of pivot,  
    // since we have pivot_prev, so we move two nodes 
    else if(pivot_prev != null &&  
            pivot_prev.next != null) 
        sort(pivot_prev.next.next, end); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    QuickSortLinkedList list = new QuickSortLinkedList(); 
    list.addNode(30); 
    list.addNode(3); 
    list.addNode(4); 
    list.addNode(20); 
    list.addNode(5); 

    Node n = list.head; 
    while(n.next != null) 
        n= n.next; 

    System.out.println("Linked List before sorting"); 
    list.printList(list.head); 

    list.sort(list.head , n); 

    System.out.println("\nLinked List after sorting"); 
    list.printList(list.head); 
} 
} 

// This code is contributed by trinadumca 

```

## C#

```cs

// C# program for Quick Sort on  
// Singly Linled List 
using System; 

/*sort a linked list using quick sort*/
class GFG  
{ 
public class Node 
{ 
    public int data; 
    public Node next; 

    public Node(int d) 
    { 
        this.data = d; 
        this.next = null; 
    } 
} 

Node head; 

void addNode(int data) 
{ 
    if(head == null) 
    { 
        head = new Node(data); 
        return; 
    } 

    Node curr = head; 
    while(curr.next != null) 
        curr = curr.next; 

    Node newNode = new Node(data); 
    curr.next = newNode; 
} 

void printList(Node n) 
{ 
    while(n != null) 
    { 
        Console.Write(n.data); 
        Console.Write(" "); 
        n = n.next; 
    } 
} 

// takes first and last node, 
// but do not break any links in  
// the whole linked list 
Node paritionLast(Node start, Node end) 
{ 
    if(start == end ||  
       start == null || end == null) 
        return start; 

    Node pivot_prev = start; 
    Node curr = start;  
    int pivot = end.data;  

    // iterate till one before the end,  
    // no need to iterate till the end  
    // because end is pivot 
    int temp; 
    while(start != end ) 
    { 

        if(start.data < pivot) 
        {  
            // keep tracks of last modified item 
            pivot_prev = curr;  
            temp = curr.data;  
            curr.data = start.data;  
            start.data = temp;  
            curr = curr.next;  
        } 
        start = start.next;  
    } 

    // swap the position of curr i.e. 
    // next suitable index and pivot 
    temp = curr.data;  
    curr.data = pivot;  
    end.data = temp;  

    // return one previous to current 
    // because current is now pointing to pivot 
    return pivot_prev; 
} 

void sort(Node start, Node end) 
{ 
    if(start == end ) 
        return; 

    // split list and partion recurse 
    Node pivot_prev = paritionLast(start, end); 
    sort(start, pivot_prev); 

    // if pivot is picked and moved to the start, 
    // that means start and pivot is same  
    // so pick from next of pivot 
    if( pivot_prev != null &&  
        pivot_prev == start ) 
        sort(pivot_prev.next, end); 

    // if pivot is in between of the list, 
    // start from next of pivot,  
    // since we have pivot_prev, so we move two nodes 
    else if(pivot_prev != null &&  
            pivot_prev.next != null) 
        sort(pivot_prev.next.next, end); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    GFG list = new GFG(); 
    list.addNode(30); 
    list.addNode(3); 
    list.addNode(4); 
    list.addNode(20); 
    list.addNode(5); 

    Node n = list.head; 
    while(n.next != null) 
        n = n.next; 

    Console.WriteLine("Linked List before sorting"); 
    list.printList(list.head); 

    list.sort(list.head , n); 

    Console.WriteLine("\nLinked List after sorting"); 
    list.printList(list.head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Linked List before sorting
30 3 4 20 5 
Linked List after sorting
3 4 5 20 30

```

本文由 [**Balasubramanian.N**](http://in.linkedin.com/pub/balasubramanian-nagasundaram/3a/361/97b) 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

