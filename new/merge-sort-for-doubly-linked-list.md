# 合并双链表

的排序

给定一个双向链表，编写一个函数使用合并排序以递增顺序对双向链表进行排序。

例如，以下双向链接列表应更改为24810

![](img/61dcfe5f15a4317c70a1bea6d144f1b2.png)

[单链表](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)的合并排序已经讨论过。 此处的重要更改是在合并两个列表时还要修改先前的指针。

以下是双向链表的合并排序的实现。

## C ++

```

// C++ program for merge sort on doubly linked list  
#include <bits/stdc++.h> 
using namespace std; 
class Node  
{  
    public: 
    int data;  
    Node *next, *prev;  
};  

Node *split(Node *head);  

// Function to merge two linked lists  
Node *merge(Node *first, Node *second)  
{  
    // If first linked list is empty  
    if (!first)  
        return second;  

    // If second linked list is empty  
    if (!second)  
        return first;  

    // Pick the smaller value  
    if (first->data < second->data)  
    {  
        first->next = merge(first->next,second);  
        first->next->prev = first;  
        first->prev = NULL;  
        return first;  
    }  
    else
    {  
        second->next = merge(first,second->next);  
        second->next->prev = second;  
        second->prev = NULL;  
        return second;  
    }  
}  

// Function to do merge sort  
Node *mergeSort(Node *head)  
{  
    if (!head || !head->next)  
        return head;  
    Node *second = split(head);  

    // Recur for left and right halves  
    head = mergeSort(head);  
    second = mergeSort(second);  

    // Merge the two sorted halves  
    return merge(head,second);  
}  

// A utility function to insert a new node at the  
// beginning of doubly linked list  
void insert(Node **head, int data)  
{  
    Node *temp = new Node(); 
    temp->data = data;  
    temp->next = temp->prev = NULL;  
    if (!(*head))  
        (*head) = temp;  
    else
    {  
        temp->next = *head;  
        (*head)->prev = temp;  
        (*head) = temp;  
    }  
}  

// A utility function to print a doubly linked list in  
// both forward and backward directions  
void print(Node *head)  
{  
    Node *temp = head;  
    cout<<"Forward Traversal using next poitner\n";  
    while (head)  
    {  
        cout << head->data << " ";  
        temp = head;  
        head = head->next;  
    }  
    cout  << "\nBackward Traversal using prev pointer\n";  
    while (temp)  
    {  
        cout << temp->data << " ";  
        temp = temp->prev;  
    }  
}  

// Utility function to swap two integers  
void swap(int *A, int *B)  
{  
    int temp = *A;  
    *A = *B;  
    *B = temp;  
}  

// Split a doubly linked list (DLL) into 2 DLLs of  
// half sizes  
Node *split(Node *head)  
{  
    Node *fast = head,*slow = head;  
    while (fast->next && fast->next->next)  
    {  
        fast = fast->next->next;  
        slow = slow->next;  
    }  
    Node *temp = slow->next;  
    slow->next = NULL;  
    return temp;  
}  

// Driver program  
int main(void)  
{  
    Node *head = NULL;  
    insert(&head, 5);  
    insert(&head, 20);  
    insert(&head, 4);  
    insert(&head, 3);  
    insert(&head, 30);  
    insert(&head, 10);  
    head = mergeSort(head);  
    cout << "Linked List after sorting\n";  
    print(head);  
    return 0;  
} 

// This is code is contributed by rathbhupendra 

```

## C

```

// C program for merge sort on doubly linked list 
#include<stdio.h> 
#include<stdlib.h> 
struct Node 
{ 
    int data; 
    struct Node *next, *prev; 
}; 

struct Node *split(struct Node *head); 

// Function to merge two linked lists 
struct Node *merge(struct Node *first, struct Node *second) 
{ 
    // If first linked list is empty 
    if (!first) 
        return second; 

    // If second linked list is empty 
    if (!second) 
        return first; 

    // Pick the smaller value 
    if (first->data < second->data) 
    { 
        first->next = merge(first->next,second); 
        first->next->prev = first; 
        first->prev = NULL; 
        return first; 
    } 
    else
    { 
        second->next = merge(first,second->next); 
        second->next->prev = second; 
        second->prev = NULL; 
        return second; 
    } 
} 

// Function to do merge sort 
struct Node *mergeSort(struct Node *head) 
{ 
    if (!head || !head->next) 
        return head; 
    struct Node *second = split(head); 

    // Recur for left and right halves 
    head = mergeSort(head); 
    second = mergeSort(second); 

    // Merge the two sorted halves 
    return merge(head,second); 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node **head, int data) 
{ 
    struct Node *temp = 
        (struct Node *)malloc(sizeof(struct Node)); 
    temp->data = data; 
    temp->next = temp->prev = NULL; 
    if (!(*head)) 
        (*head) = temp; 
    else
    { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// A utility function to print a doubly linked list in 
// both forward and backward directions 
void print(struct Node *head) 
{ 
    struct Node *temp = head; 
    printf("Forward Traversal using next poitner\n"); 
    while (head) 
    { 
        printf("%d ",head->data); 
        temp = head; 
        head = head->next; 
    } 
    printf("\nBackward Traversal using prev pointer\n"); 
    while (temp) 
    { 
        printf("%d ", temp->data); 
        temp = temp->prev; 
    } 
} 

// Utility function to swap two integers 
void swap(int *A, int *B) 
{ 
    int temp = *A; 
    *A = *B; 
    *B = temp; 
} 

// Split a doubly linked list (DLL) into 2 DLLs of 
// half sizes 
struct Node *split(struct Node *head) 
{ 
    struct Node *fast = head,*slow = head; 
    while (fast->next && fast->next->next) 
    { 
        fast = fast->next->next; 
        slow = slow->next; 
    } 
    struct Node *temp = slow->next; 
    slow->next = NULL; 
    return temp; 
} 

// Driver program 
int main(void) 
{ 
    struct Node *head = NULL; 
    insert(&head,5); 
    insert(&head,20); 
    insert(&head,4); 
    insert(&head,3); 
    insert(&head,30); 
    insert(&head,10); 
    head = mergeSort(head); 
    printf("\n\nLinked List after sorting\n"); 
    print(head); 
    return 0; 
}

```

## 爪哇

```

// Java program to implement merge sort in singly linked list 

// Linked List Class 
class LinkedList { 

    static Node head;  // head of list 

    /* Node Class */
    static class Node { 

        int data; 
        Node next, prev; 

        // Constructor to create a new node 
        Node(int d) { 
            data = d; 
            next = prev = null; 
        } 
    } 

    void print(Node node) { 
        Node temp = node; 
        System.out.println("Forward Traversal using next pointer"); 
        while (node != null) { 
            System.out.print(node.data + " "); 
            temp = node; 
            node = node.next; 
        } 
        System.out.println("\nBackward Traversal using prev pointer"); 
        while (temp != null) { 
            System.out.print(temp.data + " "); 
            temp = temp.prev; 
        } 
    } 

    // Split a doubly linked list (DLL) into 2 DLLs of 
    // half sizes 
    Node split(Node head) { 
        Node fast = head, slow = head; 
        while (fast.next != null && fast.next.next != null) { 
            fast = fast.next.next; 
            slow = slow.next; 
        } 
        Node temp = slow.next; 
        slow.next = null; 
        return temp; 
    } 

    Node mergeSort(Node node) { 
        if (node == null || node.next == null) { 
            return node; 
        } 
        Node second = split(node); 

        // Recur for left and right halves 
        node = mergeSort(node); 
        second = mergeSort(second); 

        // Merge the two sorted halves 
        return merge(node, second); 
    } 

    // Function to merge two linked lists 
    Node merge(Node first, Node second) { 
        // If first linked list is empty 
        if (first == null) { 
            return second; 
        } 

        // If second linked list is empty 
        if (second == null) { 
            return first; 
        } 

        // Pick the smaller value 
        if (first.data < second.data) { 
            first.next = merge(first.next, second); 
            first.next.prev = first; 
            first.prev = null; 
            return first; 
        } else { 
            second.next = merge(first, second.next); 
            second.next.prev = second; 
            second.prev = null; 
            return second; 
        } 
    } 

    // Driver program to test above functions 
    public static void main(String[] args) { 

        LinkedList list = new LinkedList(); 
        list.head = new Node(10); 
        list.head.next = new Node(30); 
        list.head.next.next = new Node(3); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(20); 
        list.head.next.next.next.next.next = new Node(5); 

        Node node = null; 
        node = list.mergeSort(head); 
        System.out.println("Linked list after sorting :"); 
        list.print(node); 

    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

## 蟒蛇

```

# Program for merge sort on doubly linked list 

# A node of the doublly linked list 
class Node: 

    # Constructor to create a new node 
    def __init__(self, data): 
        self.data = data  
        self.next = None
        self.prev = None

class DoublyLinkedList: 

     # Constructor for empty Doubly Linked List 
    def __init__(self): 
        self.head = None

    # Function to merge two linked list 
    def merge(self, first, second): 

        # If first linked list is empty 
        if first is None: 
            return second  

        # If secon linked list is empty  
        if second is None: 
            return first 

        # Pick the smaller value 
        if first.data < second.data: 
            first.next = self.merge(first.next, second) 
            first.next.prev = first 
            first.prev = None   
            return first 
        else: 
            second.next = self.merge(first, second.next) 
            second.next.prev = second 
            second.prev = None
            return second 

    # Function to do merge sort 
    def mergeSort(self, tempHead): 
        if tempHead is None:  
            return tempHead 
        if tempHead.next is None: 
            return tempHead 

        second = self.split(tempHead) 

        # Recur for left and righ halves 
        tempHead = self.mergeSort(tempHead) 
        second = self.mergeSort(second) 

        # Merge the two sorted halves 
        return self.merge(tempHead, second) 

    # Split the doubly linked list (DLL) into two DLLs 
    # of half sizes 
    def split(self, tempHead): 
        fast = slow =  tempHead 
        while(True): 
            if fast.next is None: 
                break
            if fast.next.next is None: 
                break
            fast = fast.next.next 
            slow = slow.next

        temp = slow.next
        slow.next = None
        return temp 

    # Given a reference to the head of a list and an 
    # integer,inserts a new node on the front of list 
    def push(self, new_data): 

        # 1\. Allocates node 
        # 2\. Put the data in it 
        new_node = Node(new_data) 

        # 3\. Make next of new node as head and 
        # previous as None (already None) 
        new_node.next = self.head 

        # 4\. change prev of head node to new_node 
        if self.head is not None: 
            self.head.prev = new_node 

        # 5\. move the head to point to the new node 
        self.head = new_node 

    def printList(self, node): 
        temp = node 
        print "Forward Traversal using next poitner"
        while(node is not None): 
            print node.data, 
            temp = node 
            node = node.next
        print "\nBackward Traversal using prev pointer"
        while(temp): 
            print temp.data, 
            temp = temp.prev 

# Driver program to test the above functions 
dll = DoublyLinkedList() 
dll.push(5) 
dll.push(20); 
dll.push(4); 
dll.push(3); 
dll.push(30) 
dll.push(10); 
dll.head = dll.mergeSort(dll.head)    
print "Linked List after sorting"
dll.printList(dll.head) 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C＃

```

// C# program to implement merge  
// sort in singly linked list  

using System;  

// Linked List Class  
public class LinkedList  
{  

    Node head; // head of list  

    /* Node Class */
    class Node  
    {  

        public int data;  
        public Node next, prev;  

        // Constructor to create a new node  
        public Node(int d)  
        {  
            data = d;  
            next = prev = null;  
        }  
    }  

    void print(Node node) 
    {  
        Node temp = node;  
        Console.WriteLine("Forward Traversal" +  
                          "using next pointer");  
        while (node != null)  
        {  
            Console.Write(node.data + " ");  
            temp = node;  
            node = node.next;  
        }  
        Console.WriteLine("\nBackward Traversal" + 
                            "using prev pointer");  
        while (temp != null)  
        {  
            Console.Write(temp.data + " ");  
            temp = temp.prev;  
        }  
    }  

    // Split a doubly linked list (DLL)  
    //  into 2 DLLs of half sizes  
    Node split(Node head) 
    {  
        Node fast = head, slow = head;  
        while (fast.next != null &&  
                fast.next.next != null)  
        {  
            fast = fast.next.next;  
            slow = slow.next;  
        }  
        Node temp = slow.next;  
        slow.next = null;  
        return temp;  
    }  

    Node mergeSort(Node node) 
    {  
        if (node == null || node.next == null)  
        {  
            return node;  
        }  
        Node second = split(node);  

        // Recur for left and right halves  
        node = mergeSort(node);  
        second = mergeSort(second);  

        // Merge the two sorted halves  
        return merge(node, second);  
    }  

    // Function to merge two linked lists  
    Node merge(Node first, Node second)  
    {  
        // If first linked list is empty  
        if (first == null) {  
            return second;  
        }  

        // If second linked list is empty  
        if (second == null)  
        {  
            return first;  
        }  

        // Pick the smaller value  
        if (first.data < second.data)  
        {  
            first.next = merge(first.next, second);  
            first.next.prev = first;  
            first.prev = null;  
            return first;  
        }  
        else
        {  
            second.next = merge(first, second.next);  
            second.next.prev = second;  
            second.prev = null;  
            return second;  
        }  
    }  

    // Driver code 
    public static void Main(String[] args)  
    {  

        LinkedList list = new LinkedList();  
        list.head = new Node(10);  
        list.head.next = new Node(30);  
        list.head.next.next = new Node(3);  
        list.head.next.next.next = new Node(4);  
        list.head.next.next.next.next = new Node(20);  
        list.head.next.next.next.next.next = new Node(5);  

        Node node = null;  
        node = list.mergeSort(list.head);  
        Console.WriteLine("Linked list after sorting :");  
        list.print(node);  
    }  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
Linked List after sorting
Forward Traversal using next pointer
3 4 5 10 20 30
Backward Traversal using prev pointer
30 20 10 5 4 3
```

感谢Goku在此处的注释[中提供了上述实现。](https://www.geeksforgeeks.org/quicksort-for-linked-list/)

**时间复杂度：**上述实现的时间复杂度与数组的 [MergeSort的时间复杂度相同。 这需要Θ（nLogn）时间。](http://geeksquiz.com/merge-sort/)

您可能还想看到[快速排序以获取双向链接列表](https://www.geeksforgeeks.org/quicksort-for-linked-list/)

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。