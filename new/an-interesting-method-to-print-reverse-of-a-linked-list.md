# 一种有趣的打印反向链表的方法

> 原文：[https://www.geeksforgeeks.org/an-interesting-method-to-print-reverse-of-a-linked-list/](https://www.geeksforgeeks.org/an-interesting-method-to-print-reverse-of-a-linked-list/)

我们得到了一个链表，我们需要以相反的顺序打印链表。

例子：

```
Input : list : 5-> 15-> 20-> 25 
Output : Reversed Linked list : 25-> 20-> 15-> 5

Input : list : 85-> 15-> 4-> 20 
Output : Reversed Linked list : 20-> 4-> 15-> 85

Input : list : 85
Output : Reversed Linked list : 85

```

对于以相反顺序打印列表，我们已经讨论了[反向迭代和递归](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)的方法。

在本文中，我们讨论了一种有趣的方法，该方法不需要递归，也不需要修改列表。 该功能也只访问链表的每个节点一次。

**技巧**：以反向顺序打印列表而没有任何递归功能或循环的想法是使用[回车符](https://en.wikipedia.org/wiki/Carriage_return)（`"r"`）。 为此，我们应该了解列表的长度。 现在，我们应该打印`n-1`个空白字符，然后打印第一个元素，然后打印`"r"`，再打印`n-2`个空白字符，再打印第二个节点，然后打印`"r"`，依此类推。

**回车（`\n`）**：它命令打印机（光标或系统控制台的显示屏）将光标的位置移至同一行的第一个位置。

## C/C++ 

```cpp

// C program to print reverse of list 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to reverse the linked list */
void printReverse(struct Node** head_ref, int n) 
{ 
    int j = 0; 
    struct Node* current = *head_ref; 
    while (current != NULL) { 

        // For each node, print proper number 
        // of spaces before printing it 
        for (int i = 0; i < 2 * (n - j); i++) 
            printf(" "); 

        // use of carriage return to move back 
        // and print. 
        printf("%d\r", current->data); 

        current = current->next; 
        j++; 
    } 
} 

/* Function to push a node */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node =  
          (struct Node*)malloc(sizeof(struct Node)); 

    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print linked list and find its 
   length */
int printList(struct Node* head) 
{ 
    // i for finding length of list 
    int i = 0; 
    struct Node* temp = head; 
    while (temp != NULL) { 
        printf("%d  ", temp->data); 
        temp = temp->next; 
        i++; 
    } 
    return i; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 
    // list nodes are as 6 5 4 3 2 1 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 3); 
    push(&head, 4); 
    push(&head, 5); 
    push(&head, 6); 

    printf("Given linked list:\n"); 
    // printlist print the list and 
    // return the size of list 
    int n = printList(head); 

    // print reverse list with help 
    // of carriage return function 
    printf("\nReversed Linked list:\n"); 
    printReverse(&head, n); 
    printf("\n"); 
    return 0; 
} 

```

## Java

```java

// Java program to print reverse of list 
import java.io.*; 
import java.util.*; 

// Represents node of a linkedlist 
class Node { 
      int data; 
      Node next; 
      Node(int val) 
      { 
          data = val; 
          next = null; 
      } 
} 

public class GFG  
{ 

   /* Function to reverse the linked list */
   static void printReverse(Node head, int n) 
   { 
          int j = 0; 
          Node current = head; 
          while (current != null) { 

             // For each node, print proper number  
             // of spaces before printing it  
             for (int i = 0; i < 2 * (n - j); i++) 
                  System.out.print(" "); 

             // use of carriage return to move back  
             // and print. 
             System.out.print("\r" + current.data); 

             current = current.next; 
             j++;  
          } 
   } 

   /* Function to push a node */
   static Node push(Node head, int data)  
   { 
          Node new_node = new Node(data); 
          new_node.next = head; 
          head = new_node; 

          return head; 
   } 

   /* Function to print linked list and find its  
   length */
   static int printList(Node head) 
   { 
          // i for finding length of list  
          int i = 0; 
          Node temp = head; 
          while (temp != null) 
          { 
                 System.out.print(temp.data + " "); 
                 temp = temp.next; 
                 i++; 
          } 

          return i; 
   } 

   // Driver code 
   public static void main(String args[]) 
   { 
          /* Start with the empty list */
          Node head = null; 

          // list nodes are as 6 5 4 3 2 1 
          head = push(head, 1); 
          head = push(head, 2); 
          head = push(head, 3); 
          head = push(head, 4); 
          head = push(head, 5); 
          head = push(head, 6); 

          System.out.println("Given linked list: "); 

          // printlist print the list and  
          // return the size of list  
          int n = printList(head);  

          // print reverse list with help  
          // of carriage return function 
          System.out.println("Reversed Linked list: "); 
          printReverse(head, n);  
          System.out.println(); 

   } 
} 

// This code is contributed by rachana soma 

```

## C#

```cs

// C# program to print reverse of list 
using System; 

// Represents node of a linkedlist 
public class Node { 
      public int data; 
      public Node next; 
      public Node(int val) 
      { 
          data = val; 
          next = null; 
      } 
} 

public class GFG 
{ 

   /* Function to reverse the linked list */
   static void printReverse(Node head, int n) 
   { 
          int j = 0; 
          Node current = head; 
          while (current != null) { 

             // For each node, print proper number  
             // of spaces before printing it  
             for (int i = 0; i < 2 * (n - j); i++) 
                  Console.Write(" "); 

             // use of carriage return to move back  
             // and print. 
             Console.Write("\r" + current.data); 

             current = current.next; 
             j++;  
          } 
   } 

   /* Function to push a node */
   static Node push(Node head, int data)  
   { 
          Node new_node = new Node(data); 
          new_node.next = head; 
          head = new_node; 

          return head; 
   } 

   /* Function to print linked list and find its  
   length */
   static int printList(Node head) 
   { 
          // i for finding length of list  
          int i = 0; 
          Node temp = head; 
          while (temp != null) 
          { 
                 Console.Write(temp.data + " "); 
                 temp = temp.next; 
                 i++; 
          } 

          return i; 
   } 

   // Driver code 
   public static void Main(String []args) 
   { 
      /* Start with the empty list */
      Node head = null; 

      // list nodes are as 6 5 4 3 2 1 
      head = push(head, 1); 
      head = push(head, 2); 
      head = push(head, 3); 
      head = push(head, 4); 
      head = push(head, 5); 
      head = push(head, 6); 

      Console.WriteLine("Given linked list: "); 
      // printlist print the list and  
      // return the size of list  
      int n = printList(head);  

      // print reverse list with help  
      // of carriage return function 
      Console.WriteLine("Reversed Linked list: "); 
      printReverse(head, n);  
      Console.WriteLine(); 
   } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to print reverse of list 

# Link list node  
class Node: 
    def __init__(self): 
        self.data=  0
        self.next=None

# Function to reverse the linked list  
def printReverse( head_ref, n): 

    j = 0
    current = head_ref 
    while (current != None):  
        i = 0

        # For each node, print proper number 
        # of spaces before printing it 
        while ( i < 2 * (n - j) ): 
            print(end=" ") 
            i = i + 1

        # use of carriage return to move back 
        # and print. 
        print( current.data, end = "\r") 

        current = current.next
        j = j + 1

 # Function to push a node  
def push( head_ref, new_data): 

    new_node = Node()  

    new_node.data = new_data 
    new_node.next = (head_ref) 
    (head_ref) = new_node 
    return head_ref; 

# Function to print linked list and find its 
#  length  
def printList( head): 

    # i for finding length of list 
    i = 0
    temp = head 
    while (temp != None):  
        print( temp.data,end = " ") 
        temp = temp.next
        i = i + 1

    return i 

# Driver program to test above function 

# Start with the empty list  
head = None

# list nodes are as 6 5 4 3 2 1 
head = push(head, 1) 
head = push(head, 2) 
head = push(head, 3) 
head = push(head, 4) 
head = push(head, 5) 
head = push(head, 6) 

print("Given linked list:") 

# printlist print the list and 
# return the size of list 
n = printList(head) 

# print reverse list with help 
# of carriage return function 
print("\nReversed Linked list:") 
printReverse(head, n) 
print() 

# This code is contributed by Arnab Kundu 

```

**输出**：

```
Given linked list:
6 5 4 3 2 1
Reversed Linked List:
1 2 3 4 5 6

```

**输入和输出图示**：

```
输入：     6 5 4 3 2 1
第一次迭代：_ _ _ _ _ 6
第二次迭代：_ _ _ _ 5 6
第三次迭代：_ _ _ 4 5 6
第四次迭代：_ _ 3 4 5 6
第五次迭代：_ 2 3 4 5 6
最终输出：  1 2 3 4 5 6
```

**注意**： 上面的程序可能无法在在线编译器上运行，因为它们不支持控制台上的回车之类的操作。

**参考**：

[栈溢出/回车](https://stackoverflow.com/questions/7372918/whats-the-use-of-r-escape-sequence)

本文由 [**Shivam Pradhan(anuj_charm)**](https://www.facebook.com/anuj.charm) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

