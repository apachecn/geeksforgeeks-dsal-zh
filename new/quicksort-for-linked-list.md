# 双链接列表

上的快速排序

以下是数组的 [QuickSort](http://en.wikipedia.org/wiki/Quicksort) 的典型递归实现。 该实现使用last元素作为枢轴。

```

/* A typical recursive implementation of Quicksort for array*/

/* This function takes last element as pivot, places the pivot element at its 
   correct position in sorted array, and places all smaller (smaller than  
   pivot) to left of pivot and all greater elements to right of pivot */
int partition (int arr[], int l, int h) 
{ 
    int x = arr[h]; 
    int i = (l - 1); 

    for (int j = l; j <= h- 1; j++) 
    { 
        if (arr[j] <= x) 
        { 
            i++; 
            swap (&arr[i], &arr[j]); 
        } 
    } 
    swap (&arr[i + 1], &arr[h]); 
    return (i + 1); 
} 

/* A[] --> Array to be sorted, l  --> Starting index, h  --> Ending index */
void quickSort(int A[], int l, int h) 
{ 
    if (l < h) 
    {         
        int p = partition(A, l, h); /* Partitioning index */
        quickSort(A, l, p - 1);   
        quickSort(A, p + 1, h); 
    } 
} 

```

**我们可以对链表使用相同的算法吗？**
以下是双向链表的C++实现。 这个想法很简单，我们首先找出指向最后一个节点的指针。 一旦有了指向最后一个节点的指针，就可以使用指向链表的第一个和最后一个节点的指针对链表进行递归排序，类似于上面的递归函数，其中传递了第一个和最后一个数组元素的索引。 链表的分区功能也类似于数组的分区。 代替返回枢轴元素的索引，它返回指向枢轴元素的指针。 在以下实现中，quickSort（）只是一个包装函数，主要的递归函数是_quickSort（），类似于数组实现的quickSort（）。

![](img/907e6783a6130c711cfa83c52cb7210e.png)

## C++

```cpp

// A C++ program to sort a linked list using Quicksort  
#include <bits/stdc++.h> 
using namespace std; 

/* a node of the doubly linked list */
class Node  
{  
    public: 
    int data;  
    Node *next;  
    Node *prev;  
};  

/* A utility function to swap two elements */
void swap ( int* a, int* b )  
{ int t = *a; *a = *b; *b = t; }  

// A utility function to find 
// last node of linked list  
Node *lastNode(Node *root)  
{  
    while (root && root->next)  
        root = root->next;  
    return root;  
}  

/* Considers last element as pivot,  
places the pivot element at its  
correct position in sorted array,  
and places all smaller (smaller than  
pivot) to left of pivot and all greater 
elements to right of pivot */
Node* partition(Node *l, Node *h)  
{  
    // set pivot as h element  
    int x = h->data;  

    // similar to i = l-1 for array implementation  
    Node *i = l->prev;  

    // Similar to "for (int j = l; j <= h- 1; j++)"  
    for (Node *j = l; j != h; j = j->next)  
    {  
        if (j->data <= x)  
        {  
            // Similar to i++ for array  
            i = (i == NULL)? l : i->next;  

            swap(&(i->data), &(j->data));  
        }  
    }  
    i = (i == NULL)? l : i->next; // Similar to i++  
    swap(&(i->data), &(h->data));  
    return i;  
}  

/* A recursive implementation  
of quicksort for linked list */
void _quickSort(Node* l, Node *h)  
{  
    if (h != NULL && l != h && l != h->next)  
    {  
        Node *p = partition(l, h);  
        _quickSort(l, p->prev);  
        _quickSort(p->next, h);  
    }  
}  

// The main function to sort a linked list. 
// It mainly calls _quickSort()  
void quickSort(Node *head)  
{  
    // Find last node  
    Node *h = lastNode(head);  

    // Call the recursive QuickSort  
    _quickSort(head, h);  
}  

// A utility function to print contents of arr  
void printList(Node *head)  
{  
    while (head)  
    {  
        cout << head->data << " ";  
        head = head->next;  
    }  
    cout << endl;  
}  

/* Function to insert a node at the  
beginging of the Doubly Linked List */
void push(Node** head_ref, int new_data)  
{  
    Node* new_node = new Node; /* allocate node */
    new_node->data = new_data;  

    /* since we are adding at the 
    beginning, prev is always NULL */
    new_node->prev = NULL;  

    /* link the old list off the new node */
    new_node->next = (*head_ref);  

    /* change prev of head node to new node */
    if ((*head_ref) != NULL) (*head_ref)->prev = new_node ;  

    /* move the head to point to the new node */
    (*head_ref) = new_node;  
}  

/* Driver code */
int main()  
{  
    Node *a = NULL;  
    push(&a, 5);  
    push(&a, 20);  
    push(&a, 4);  
    push(&a, 3);  
    push(&a, 30);  

    cout << "Linked List before sorting \n";  
    printList(a);  

    quickSort(a);  

    cout << "Linked List after sorting \n";  
    printList(a);  

    return 0;  
}  

// This code is contributed by rathbhupendra 

```

## C

```c

// C program to sort a linked list using Quicksort 
#include <stdio.h> 
#include <stdlib.h> 

/* a node of the doubly linked list */
struct Node 
{ 
    int data; 
    struct Node *next; 
    struct Node *prev; 
}; 

/* A utility function to swap two elements */
void swap ( int* a, int* b ) 
{ int t = *a; *a = *b; *b = t; } 

// A utility function to find last node of linked list 
struct Node *lastNode(struct Node *root) 
{ 
    while (root && root->next) 
        root = root->next; 
    return root; 
} 

/* Considers last element as pivot, places the  
pivot element at its correct position in sorted array,  
and places all smaller (smaller than pivot) to left 
of pivot and all greater elements to right of pivot */
struct Node* partition(struct Node *l, struct Node *h) 
{ 
    // set pivot as h element 
    int x = h->data; 

    // similar to i = l-1 for array implementation 
    struct Node *i = l->prev; 

    // Similar to "for (int j = l; j <= h- 1; j++)" 
    for (struct Node *j = l; j != h; j = j->next) 
    { 
        if (j->data <= x) 
        { 
            // Similar to i++ for array 
            i = (i == NULL) ? l : i->next; 

            swap(&(i->data), &(j->data)); 
        } 
    } 
    i = (i == NULL) ? l : i->next; // Similar to i++ 
    swap(&(i->data), &(h->data)); 
    return i; 
} 

/* A recursive implementation of quicksort for linked list */
void _quickSort(struct Node* l, struct Node *h) 
{ 
    if (h != NULL && l != h && l != h->next) 
    { 
        struct Node *p = partition(l, h); 
        _quickSort(l, p->prev); 
        _quickSort(p->next, h); 
    } 
} 

// The main function to sort a linked list. 
// It mainly calls _quickSort() 
void quickSort(struct Node *head) 
{ 
    // Find last node 
    struct Node *h = lastNode(head); 

    // Call the recursive QuickSort 
    _quickSort(head, h); 
} 

// A utility function to print contents of arr 
void printList(struct Node *head) 
{ 
    while (head) 
    { 
        printf("%d ", head->data); 
        head = head->next; 
    } 
    printf("\n"); 
} 

/* Function to insert a node at the  
beginning of the Doubly Linked List */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = (struct Node*)  
               malloc(sizeof(struct Node)); /* allocate node */
    new_node->data = new_data; 

    /* since we are adding at the beginning, 
    prev is always NULL */
    new_node->prev = NULL; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* change prev of head node to new node */
    if ((*head_ref) != NULL) (*head_ref)->prev = new_node ; 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Driver Code 
int main(int argc, char **argv) 
{ 
    struct Node *a = NULL; 
    push(&a, 5); 
    push(&a, 20); 
    push(&a, 4); 
    push(&a, 3); 
    push(&a, 30); 

    printf("Linked List before sorting \n"); 
    printList(a); 

    quickSort(a); 

    printf("Linked List after sorting \n"); 
    printList(a); 

    return 0; 
} 

```

## Java

```java

// A Java program to sort a linked list using Quicksort 
class QuickSort_using_Doubly_LinkedList{ 
    Node head; 

/* a node of the doubly linked list */  
    static class Node{ 
        private int data; 
        private Node next; 
        private Node prev; 

        Node(int d){ 
            data = d; 
            next = null; 
            prev = null; 
        } 
    } 

// A utility function to find last node of linked list     
    Node lastNode(Node node){ 
        while(node.next!=null) 
            node = node.next; 
        return node; 
    } 

/* Considers last element as pivot, places the pivot element at its 
   correct position in sorted array, and places all smaller (smaller than 
   pivot) to left of pivot and all greater elements to right of pivot */
    Node partition(Node l,Node h) 
    { 
       // set pivot as h element 
        int x = h.data; 

        // similar to i = l-1 for array implementation 
        Node i = l.prev; 

        // Similar to "for (int j = l; j <= h- 1; j++)" 
        for(Node j=l; j!=h; j=j.next) 
        { 
            if(j.data <= x) 
            { 
                // Similar to i++ for array 
                i = (i==null) ? l : i.next; 
                int temp = i.data; 
                i.data = j.data; 
                j.data = temp; 
            } 
        } 
        i = (i==null) ? l : i.next;  // Similar to i++ 
        int temp = i.data; 
        i.data = h.data; 
        h.data = temp; 
        return i; 
    } 

    /* A recursive implementation of quicksort for linked list */
    void _quickSort(Node l,Node h) 
    { 
        if(h!=null && l!=h && l!=h.next){ 
            Node temp = partition(l,h); 
            _quickSort(l,temp.prev); 
            _quickSort(temp.next,h); 
        } 
    } 

    // The main function to sort a linked list. It mainly calls _quickSort() 
    public void quickSort(Node node) 
    { 
        // Find last node 
        Node head = lastNode(node); 

        // Call the recursive QuickSort 
        _quickSort(node,head); 
    } 

     // A utility function to print contents of arr 
     public void printList(Node head) 
     { 
        while(head!=null){ 
            System.out.print(head.data+" "); 
            head = head.next; 
        } 
    } 

    /* Function to insert a node at the beginning of the Doubly Linked List */
    void push(int new_Data) 
    { 
        Node new_Node = new Node(new_Data);     /* allocate node */

        // if head is null, head = new_Node 
        if(head==null){ 
            head = new_Node; 
            return; 
        } 

        /* link the old list off the new node */
        new_Node.next = head; 

        /* change prev of head node to new node */
        head.prev = new_Node; 

        /* since we are adding at the beginning, prev is always NULL */
        new_Node.prev = null; 

        /* move the head to point to the new node */
        head = new_Node; 
    } 

    /* Driver program to test above function */
    public static void main(String[] args){ 
            QuickSort_using_Doubly_LinkedList list = new QuickSort_using_Doubly_LinkedList(); 

            list.push(5); 
            list.push(20); 
            list.push(4); 
            list.push(3); 
            list.push(30); 

            System.out.println("Linked List before sorting "); 
            list.printList(list.head); 
            System.out.println("\nLinked List after sorting"); 
            list.quickSort(list.head); 
            list.printList(list.head); 

    } 
} 

// This code has been contributed by Amit Khandelwal 

```

## C#

```cs

// A C# program to sort a linked list using Quicksort  
using System;  

public class QuickSort_using_Doubly_LinkedList 
{  
    Node head;  

/* a node of the doubly linked list */
    public class Node{  
        public int data;  
        public Node next;  
        public Node prev;  

        public Node(int d){  
            data = d;  
            next = null;  
            prev = null;  
        }  
    }  

// A utility function to find the last node of linked list  
    Node lastNode(Node node) 
    {  
        while(node.next!=null)  
            node = node.next;  
        return node;  
    }  

/* Considers last element as pivot, 
places the pivot element at its  
correct position in a sorted array, 
and places all smaller (smaller than  
pivot) to left of pivot and all  
greater elements to right of pivot */
    Node partition(Node l,Node h)  
    {  
        // set pivot as h element  
        int x = h.data;  

        // similar to i = l-1 for array implementation  
        Node i = l.prev;  
        int temp; 

        // Similar to "for (int j = l; j <= h- 1; j++)"  
        for(Node j=l; j!=h; j=j.next)  
        {  
            if(j.data <= x)  
            {  
                // Similar to i++ for array  
                i = (i==null) ? l : i.next;  
                temp = i.data;  
                i.data = j.data;  
                j.data = temp;  
            }  
        }  
        i = (i == null) ? l : i.next; // Similar to i++  
        temp = i.data;  
        i.data = h.data;  
        h.data = temp;  
        return i;  
    }  

    /* A recursive implementation of  
    quicksort for linked list */
    void _quickSort(Node l,Node h)  
    {  
        if(h!=null && l!=h && l!=h.next){  
            Node temp = partition(l,h);  
            _quickSort(l,temp.prev);  
            _quickSort(temp.next,h);  
        }  
    }  

    // The main function to sort a linked list. 
    // It mainly calls _quickSort()  
    public void quickSort(Node node)  
    {  
        // Find last node  
        Node head = lastNode(node);  

        // Call the recursive QuickSort  
        _quickSort(node,head);  
    }  

    // A utility function to print contents of arr  
    public void printList(Node head)  
    {  
        while(head!=null){  
            Console.Write(head.data+" ");  
            head = head.next;  
        }  
    }  

    /* Function to insert a node at the  
    beginging of the Doubly Linked List */
    void push(int new_Data)  
    {  
        Node new_Node = new Node(new_Data); /* allocate node */

        // if head is null, head = new_Node  
        if(head==null) 
        {  
            head = new_Node;  
            return;  
        }  

        /* link the old list off the new node */
        new_Node.next = head;  

        /* change prev of head node to new node */
        head.prev = new_Node;  

        /* since we are adding at the 
        beginning, prev is always NULL */
        new_Node.prev = null;  

        /* move the head to point to the new node */
        head = new_Node;  
    }  

    /* Driver code */
    public static void Main(String[] args){  
            QuickSort_using_Doubly_LinkedList list = new QuickSort_using_Doubly_LinkedList();  

            list.push(5);  
            list.push(20);  
            list.push(4);  
            list.push(3);  
            list.push(30);  

            Console.WriteLine("Linked List before sorting ");  
            list.printList(list.head);  
            Console.WriteLine("\nLinked List after sorting");  
            list.quickSort(list.head);  
            list.printList(list.head);  
    }  
}  

// This code is contributed by 29AjayKumar 

```

**输出：**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

**时间复杂度：**上述实现的时间复杂度与数组的QuickSort（）的时间复杂度相同。 在最坏的情况下需要O（n ^ 2）时间，在平均和最好的情况下需要O（nLogn）。 最坏的情况是链表已经排序。

我们可以对链接列表实施随机快速排序吗？
仅当我们可以选择一个固定点作为枢轴时（如上述实现中的最后一个元素），才能为链接列表实现Quicksort。 通过选择随机数据透视表，不能有效地为链接列表实现随机QuickSort。

**练习：**
上面的实现适用于双链表。 修改它为单链列表。 请注意，单链接列表中没有上一个指针。
请参阅单链接列表上的[快速排序。](https://www.geeksforgeeks.org/quicksort-on-singly-linked-list/)

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

