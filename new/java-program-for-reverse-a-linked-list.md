# 反向链表的 Java 程序

> 原文：[https://www.geeksforgeeks.org/java-program-for-reverse-a-linked-list/](https://www.geeksforgeeks.org/java-program-for-reverse-a-linked-list/)

给定指向链表头节点的指针，任务是反转链表。 我们需要通过更改节点之间的链接来反转列表。

例子：

```
Input : Head of following linked list  
       1->2->3->4->NULL
Output : Linked list should be changed to,
       4->3->2->1->NULL

Input : Head of following linked list  
       1->2->3->4->5->NULL
Output : Linked list should be changed to,
       5->4->3->2->1->NULL

Input : NULL
Output : NULL

Input  : 1->NULL
Output : 1->NULL

```

**迭代方法**

## Java

```java

// Java program for reversing the linked list 

class LinkedList { 

    static Node head; 

    static class Node { 

        int data; 
        Node next; 

        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    /* Function to reverse the linked list */
    Node reverse(Node node) { 
        Node prev = null; 
        Node current = node; 
        Node next = null; 
        while (current != null) { 
            next = current.next; 
            current.next = prev; 
            prev = current; 
            current = next; 
        } 
        node = prev; 
        return node; 
    } 

    // prints content of double linked list 
    void printList(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(85); 
        list.head.next = new Node(15); 
        list.head.next.next = new Node(4); 
        list.head.next.next.next = new Node(20); 

        System.out.println("Given Linked list"); 
        list.printList(head); 
        head = list.reverse(head); 
        System.out.println(""); 
        System.out.println("Reversed linked list "); 
        list.printList(head); 
    } 
} 

// This code has been contributed by Mayank Jaiswal 

```

**递归方法**：

```

void recursiveReverse(struct Node** head_ref) 
{ 
    struct Node* first; 
    struct Node* rest; 

    /* empty list */
    if (*head_ref == NULL) 
       return;    

    /* suppose first = {1, 2, 3}, rest = {2, 3} */
    first = *head_ref;   
    rest  = first->next; 

    /* List has only one node */
    if (rest == NULL) 
       return;    

    /* reverse the rest list and put the first element at the end */
    recursiveReverse(&rest); 
    first->next->next  = first;   

    /* tricky step -- see the diagram */
    first->next  = NULL;           

    /* fix the head pointer */
    *head_ref = rest;               
} 

```

**一种更简单且尾部递归的方法**

## Java

```java

// Java program for reversing the Linked list 

class LinkedList { 

    static Node head; 

    static class Node { 

        int data; 
        Node next; 

        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    // A simple and tail recursive function to reverse 
    // a linked list.  prev is passed as NULL initially. 
    Node reverseUtil(Node curr, Node prev) { 

        /* If last node mark it head*/
        if (curr.next == null) { 
            head = curr; 

            /* Update next to prev node */
            curr.next = prev; 
            return null; 
        } 

        /* Save curr->next node for recursive call */
        Node next1 = curr.next; 

        /* and update next ..*/
        curr.next = prev; 

        reverseUtil(next1, curr); 
        return head; 
    } 

    // prints content of double linked list 
    void printList(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(1); 
        list.head.next = new Node(2); 
        list.head.next.next = new Node(3); 
        list.head.next.next.next = new Node(4); 
        list.head.next.next.next.next = new Node(5); 
        list.head.next.next.next.next.next = new Node(6); 
        list.head.next.next.next.next.next.next = new Node(7); 
        list.head.next.next.next.next.next.next.next = new Node(8); 

        System.out.println("Original Linked list "); 
        list.printList(head); 
        Node res = list.reverseUtil(head, null); 
        System.out.println(""); 
        System.out.println(""); 
        System.out.println("Reversed linked list "); 
        list.printList(res); 
    } 
} 
// This code has been contributed by Mayank Jaiswal 

```

请参阅[的完整文章反向链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)，以了解更多详细信息！

