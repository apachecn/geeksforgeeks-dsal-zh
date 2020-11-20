# 从未排序的链表中删除重复项

> 原文：[https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/](https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/)

编写一个 removeDuplicates（）函数，该函数获取一个列表并从列表中删除所有重复的节点。 该列表未排序。

例如，如果链表是 12- > 11- > 12- > 21- > 41- > 43- > 21，则 removeDuplicates（）应该将列表转换为 12- > 11- > 21- > 41- > 43。

**方法 1（使用两个循环）**

这是使用两个循环的简单方法。 外循环用于一个接一个地拾取元素，内循环将拾取的元素与其余元素进行比较。

感谢 Gaurav Saxena 在编写此代码方面的帮助。

## C++

```cpp

/* Program to remove duplicates in an unsorted 
   linked list */
#include<bits/stdc++.h> 
using namespace std; 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

// Utility function to create a new Node 
struct Node *newNode(int data) 
{ 
   Node *temp = new Node; 
   temp->data = data; 
   temp->next = NULL; 
   return temp; 
} 

/* Function to remove duplicates from a 
   unsorted linked list */
void removeDuplicates(struct Node *start) 
{ 
    struct Node *ptr1, *ptr2, *dup; 
    ptr1 = start; 

    /* Pick elements one by one */
    while (ptr1 != NULL && ptr1->next != NULL) 
    { 
        ptr2 = ptr1; 

        /* Compare the picked element with rest 
           of the elements */
        while (ptr2->next != NULL) 
        { 
            /* If duplicate then delete it */
            if (ptr1->data == ptr2->next->data) 
            { 
                /* sequence of steps is important here */
                dup = ptr2->next; 
                ptr2->next = ptr2->next->next; 
                delete(dup); 
            } 
            else /* This is tricky */
                ptr2 = ptr2->next; 
        } 
        ptr1 = ptr1->next; 
    } 
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
    /* The constructed linked list is: 
     10->12->11->11->12->11->10*/
    struct Node *start = newNode(10); 
    start->next = newNode(12); 
    start->next->next = newNode(11); 
    start->next->next->next = newNode(11); 
    start->next->next->next->next = newNode(12); 
    start->next->next->next->next->next = 
                                    newNode(11); 
    start->next->next->next->next->next->next = 
                                    newNode(10); 

    printf("Linked list before removing duplicates "); 
    printList(start); 

    removeDuplicates(start); 

    printf("\nLinked list after removing duplicates "); 
    printList(start); 

    return 0; 
}

```

## Java

```java

// Java program to remove duplicates from unsorted  
// linked list 

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

    /* Function to remove duplicates from an 
       unsorted linked list */
    void remove_duplicates() { 
        Node ptr1 = null, ptr2 = null, dup = null; 
        ptr1 = head; 

        /* Pick elements one by one */
        while (ptr1 != null && ptr1.next != null) { 
            ptr2 = ptr1; 

            /* Compare the picked element with rest 
                of the elements */
            while (ptr2.next != null) { 

                /* If duplicate then delete it */
                if (ptr1.data == ptr2.next.data) { 

                    /* sequence of steps is important here */
                    dup = ptr2.next; 
                    ptr2.next = ptr2.next.next; 
                    System.gc(); 
                } else /* This is tricky */ { 
                    ptr2 = ptr2.next; 
                } 
            } 
            ptr1 = ptr1.next; 
        } 
    } 

    void printList(Node node) { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    public static void main(String[] args) { 
        LinkedList list = new LinkedList(); 
        list.head = new Node(10); 
        list.head.next = new Node(12); 
        list.head.next.next = new Node(11); 
        list.head.next.next.next = new Node(11); 
        list.head.next.next.next.next = new Node(12); 
        list.head.next.next.next.next.next = new Node(11); 
        list.head.next.next.next.next.next.next = new Node(10); 

        System.out.println("Linked List before removing duplicates : \n "); 
        list.printList(head); 

        list.remove_duplicates(); 
        System.out.println(""); 
        System.out.println("Linked List after removing duplicates : \n "); 
        list.printList(head); 
    } 
} 
// This code has been contributed by Mayank Jaiswal 

```

## C#

```cs

// C# program to remove duplicates from unsorted  
// linked list 
using System; 
class List_{ 

  Node head; 

  class Node{ 

    public
      int data; 
    public
      Node next; 

    public

    Node(int d)  
    { 
      data = d; 
      next = null; 
    } 
  } 

  /* Function to remove duplicates from an 
       unsorted linked list */
  void remove_duplicates()  
  { 
    Node ptr1 = null, ptr2 = null, dup = null; 
    ptr1 = head; 

    /* Pick elements one by one */
    while (ptr1 != null &&  
           ptr1.next != null) 
    { 
      ptr2 = ptr1; 

      /* Compare the picked element with rest 
                of the elements */
      while (ptr2.next != null)  
      { 

        /* If duplicate then delete it */
        if (ptr1.data == ptr2.next.data)  
        { 

          /* sequence of steps is important here */
          dup = ptr2.next; 
          ptr2.next = ptr2.next.next; 

        } 
        else /* This is tricky */ 
        { 
          ptr2 = ptr2.next; 
        } 
      } 
      ptr1 = ptr1.next; 
    } 
  } 

  void printList(Node node) 
  { 
    while (node != null)  
    { 
      Console.Write(node.data + " "); 
      node = node.next; 
    } 
  } 

  // Driver Code 
  public static void Main(String[] args)  
  { 
    List_ list = new List_(); 
    list.head = new Node(10); 
    list.head.next = new Node(12); 
    list.head.next.next = new Node(11); 
    list.head.next.next.next = new Node(11); 
    list.head.next.next.next.next = new Node(12); 
    list.head.next.next.next.next.next = new Node(11); 
    list.head.next.next.next.next.next.next = new Node(10); 

    Console.WriteLine("Linked List_ before removing duplicates : \n "); 
    list.printList(list.head); 

    list.remove_duplicates(); 
    Console.WriteLine(""); 
    Console.WriteLine("Linked List_ after removing duplicates : \n "); 
    list.printList(list.head); 
  } 
} 

// This code is contributed by gauravrajput1

```

**输出**：

```
Linked list before removing duplicates:
 10 12 11 11 12 11 10 
Linked list after removing duplicates:
 10 12 11 

```

时间复杂度：`O(N ^ 2)`

**方法 2（使用排序）**

通常，合并排序是最有效地对链表进行排序的最合适的排序算法。

1.  使用合并排序对元素进行排序。 我们很快将写一篇有关对链表进行排序的文章。 O（nLogn）

2.  使用[算法在线性时间内删除重复项，该算法用于删除已排序的链表中的重复项。`O(n)`](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)

请注意，此方法不会保留元素的原始顺序。

时间复杂度：O（nLogn）

**方法 3（使用散列）**

我们从头到尾遍历链表。 对于每个新遇到的元素，我们检查它是否在哈希表中：如果是，则将其删除；否则，将其删除。 否则我们将其放在哈希表中。

## C++

```cpp

/* Program to remove duplicates in an unsorted 
   linked list */
#include<bits/stdc++.h> 
using namespace std; 

/* A linked list node */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

// Utility function to create a new Node 
struct Node *newNode(int data) 
{ 
   Node *temp = new Node; 
   temp->data = data; 
   temp->next = NULL; 
   return temp; 
} 

/* Function to remove duplicates from a 
   unsorted linked list */
void removeDuplicates(struct Node *start) 
{ 
    // Hash to store seen values 
    unordered_set<int> seen; 

    /* Pick elements one by one */
    struct Node *curr = start; 
    struct Node *prev = NULL; 
    while (curr != NULL) 
    { 
        // If current value is seen before 
        if (seen.find(curr->data) != seen.end()) 
        { 
           prev->next = curr->next; 
           delete (curr); 
        } 
        else
        { 
           seen.insert(curr->data); 
           prev = curr; 
        } 
        curr = prev->next; 
    } 
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

/* Driver program to test above function */
int main() 
{ 
    /* The constructed linked list is: 
     10->12->11->11->12->11->10*/
    struct Node *start = newNode(10); 
    start->next = newNode(12); 
    start->next->next = newNode(11); 
    start->next->next->next = newNode(11); 
    start->next->next->next->next = newNode(12); 
    start->next->next->next->next->next = 
                                    newNode(11); 
    start->next->next->next->next->next->next = 
                                    newNode(10); 

    printf("Linked list before removing duplicates : \n"); 
    printList(start); 

    removeDuplicates(start); 

    printf("\nLinked list after removing duplicates : \n"); 
    printList(start); 

    return 0; 
} 

```

## Java

```java

// Java program to remove duplicates 
// from unsorted linkedlist 

import java.util.HashSet; 

public class removeDuplicates  
{ 
    static class node  
    { 
        int val; 
        node next; 

        public node(int val)  
        { 
            this.val = val; 
        } 
    } 

    /* Function to remove duplicates from a 
       unsorted linked list */
    static void removeDuplicate(node head)  
    { 
        // Hash to store seen values 
        HashSet<Integer> hs = new HashSet<>(); 

        /* Pick elements one by one */
        node current = head; 
        node prev = null; 
        while (current != null)  
        { 
            int curval = current.val; 

             // If current value is seen before 
            if (hs.contains(curval)) { 
                prev.next = current.next; 
            } else { 
                hs.add(curval); 
                prev = current; 
            } 
            current = current.next; 
        } 

    } 

    /* Function to print nodes in a given linked list */
    static void printList(node head)  
    { 
        while (head != null)  
        { 
            System.out.print(head.val + " "); 
            head = head.next; 
        } 
    } 

    public static void main(String[] args)  
    { 
        /* The constructed linked list is: 
         10->12->11->11->12->11->10*/
        node start = new node(10); 
        start.next = new node(12); 
        start.next.next = new node(11); 
        start.next.next.next = new node(11); 
        start.next.next.next.next = new node(12); 
        start.next.next.next.next.next = new node(11); 
        start.next.next.next.next.next.next = new node(10); 

        System.out.println("Linked list before removing duplicates :"); 
        printList(start); 

        removeDuplicate(start); 

        System.out.println("\nLinked list after removing duplicates :"); 
        printList(start); 
    } 
} 

// This code is contributed by Rishabh Mahrsee 

```

## C#

```cs

// C# program to remove duplicates 
// from unsorted linkedlist 
using System; 
using System.Collections.Generic; 

class removeDuplicates{ 
class node  
{ 
    public int val; 
    public node next; 

    public node(int val)  
    { 
        this.val = val; 
    } 
} 

// Function to remove duplicates from a 
// unsorted linked list  
static void removeDuplicate(node head)  
{ 

    // Hash to store seen values 
    HashSet<int> hs = new HashSet<int>(); 

    // Pick elements one by one  
    node current = head; 
    node prev = null; 
    while (current != null)  
    { 
        int curval = current.val; 

        // If current value is seen before 
        if (hs.Contains(curval)) 
        { 
            prev.next = current.next; 
        } 
        else 
        { 
            hs.Add(curval); 
            prev = current; 
        } 
        current = current.next; 
    } 
} 

// Function to print nodes in a  
// given linked list  
static void printList(node head)  
{ 
    while (head != null)  
    { 
        Console.Write(head.val + " "); 
        head = head.next; 
    } 
} 

// Driver code 
public static void Main(String[] args)  
{ 

    // The constructed linked list is: 
    // 10->12->11->11->12->11->10 
    node start = new node(10); 
    start.next = new node(12); 
    start.next.next = new node(11); 
    start.next.next.next = new node(11); 
    start.next.next.next.next = new node(12); 
    start.next.next.next.next.next = new node(11); 
    start.next.next.next.next.next.next = new node(10); 

    Console.WriteLine("Linked list before removing " + 
                      "duplicates :"); 
    printList(start); 

    removeDuplicate(start); 

    Console.WriteLine("\nLinked list after removing " +  
                      "duplicates :"); 
    printList(start); 
} 
} 

// This code is contributed by amal kumar choubey 

```

**输出**：

```
Linked list before removing duplicates:
 10 12 11 11 12 11 10 
Linked list after removing duplicates:
 10 12 11 

```

感谢 bearwang 建议这种方法。

时间复杂度：平均为`O(n)`（假设哈希表访问时间平均为`O(1)`）。

如果您发现上述任何解释/算法不正确，或者是解决同一问题的更好方法，请写评论。

