# 将第一个元素移到给定链接列表

的末尾

编写一个C函数，该函数将第一个元素移到给定的单链列表中。 例如，如果给定的链接列表为1-> 2-> 3-> 4-> 5，则该函数应将列表更改为2-> 3-> 4-> 5-> 1。

算法：
遍历列表直到最后一个节点。 使用两个指针：一个用于存储最后一个节点（last）的地址，另一个用于存储第一个节点（first）的地址。 循环结束后，请执行以下操作。
i）将head作为第二个节点（* head_ref = first- >接下来）。
ii）将first of next设置为NULL（first- > next = NULL）。
iii）将倒数第二个设为第一（倒数->下一个=第一）

## C ++

```

/* C++ Program to move first element to end  
   in a given linked list */
#include <stdio.h> 
#include <stdlib.h> 

/* A linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* We are using a double pointer head_ref  
   here because we change head of the linked  
   list inside this function.*/
void moveToEnd(struct Node** head_ref) 
{ 
    /* If linked list is empty, or it contains  
       only one node, then nothing needs to be  
       done, simply return */
    if (*head_ref == NULL || (*head_ref)->next == NULL) 
        return; 

    /* Initialize first and last pointers */
    struct Node* first = *head_ref; 
    struct Node* last = *head_ref; 

    /*After this loop last contains address  
    of last node in Linked List */
    while (last->next != NULL) { 
        last = last->next; 
    } 

    /* Change the head pointer to point  
       to second node now */
    *head_ref = first->next; 

    /* Set the next of first as NULL */
    first->next = NULL; 

    /* Set the next of last as first */
    last->next = first; 
} 

/* UTILITY FUNCTIONS */
/* Function to add a node at the beginning  
   of Linked List */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

/* Driver program to test above function */
int main() 
{ 
    struct Node* start = NULL; 

    /* The constructed linked list is: 
     1->2->3->4->5 */
    push(&start, 5); 
    push(&start, 4); 
    push(&start, 3); 
    push(&start, 2); 
    push(&start, 1); 

    printf("\n Linked list before moving first to end\n"); 
    printList(start); 

    moveToEnd(&start); 

    printf("\n Linked list after moving first to end\n"); 
    printList(start); 

    return 0; 
} 

```

## 爪哇

```

/* Java Program to move first element to end  
in a given linked list */
class Sol 
{ 

/* A linked list node */
static class Node 
{  
    int data;  
    Node next;  
};  

/* We are using a double pointer head_ref  
here because we change head of the linked  
list inside this function.*/
static Node moveToEnd( Node head_ref)  
{  
    /* If linked list is empty, or it contains  
    only one node, then nothing needs to be  
    done, simply return */
    if (head_ref == null || (head_ref).next == null)  
        return null;  

    /* Initialize first and last pointers */
    Node first = head_ref;  
    Node last = head_ref;  

    /*After this loop last contains address  
    of last node in Linked List */
    while (last.next != null)  
    {  
        last = last.next;  
    }  

    /* Change the head pointer to point  
    to second node now */
    head_ref = first.next;  

    /* Set the next of first as null */
    first.next = null;  

    /* Set the next of last as first */
    last.next = first;  
    return head_ref; 
}  

/* UTILITY FUNCTIONS */
/* Function to add a node at the beginning  
of Linked List */
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

/* Function to print nodes in a given linked list */
static void printList( Node node)  
{  
    while (node != null) 
    {  
        System.out.printf("%d ", node.data);  
        node = node.next;  
    }  
}  

/* Driver code */
public static void main(String args[]) 
{  
    Node start = null;  

    /* The constructed linked list is:  
    1.2.3.4.5 */
    start = push(start, 5);  
    start = push(start, 4);  
    start = push(start, 3);  
    start = push(start, 2);  
    start = push(start, 1);  

    System.out.printf("\n Linked list before moving first to end\n");  
    printList(start);  

    start = moveToEnd(start);  

    System.out.printf("\n Linked list after moving first to end\n");  
    printList(start);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## C＃

```

/* C# Program to move first element to end  
in a given linked list */
using System; 

class GFG 
{ 

/* A linked list node */
public class Node 
{  
    public int data;  
    public Node next;  
};  

/* We are using a double pointer head_ref  
here because we change head of the linked  
list inside this function.*/
static Node moveToEnd( Node head_ref)  
{  
    /* If linked list is empty, or it contains  
    only one node, then nothing needs to be  
    done, simply return */
    if (head_ref == null || (head_ref).next == null)  
        return null;  

    /* Initialize first and last pointers */
    Node first = head_ref;  
    Node last = head_ref;  

    /*After this loop last contains address  
    of last node in Linked List */
    while (last.next != null)  
    {  
        last = last.next;  
    }  

    /* Change the head pointer to point  
    to second node now */
    head_ref = first.next;  

    /* Set the next of first as null */
    first.next = null;  

    /* Set the next of last as first */
    last.next = first;  
    return head_ref; 
}  

/* UTILITY FUNCTIONS */
/* Function to add a node at the beginning  
of Linked List */
static Node push( Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node; 
    return head_ref; 
}  

/* Function to print nodes in a given linked list */
static void printList( Node node)  
{  
    while (node != null) 
    {  
        Console.Write("{0} ", node.data);  
        node = node.next;  
    }  
}  

/* Driver code */
public static void Main(String []args) 
{  
    Node start = null;  

    /* The constructed linked list is:  
    1.2.3.4.5 */
    start = push(start, 5);  
    start = push(start, 4);  
    start = push(start, 3);  
    start = push(start, 2);  
    start = push(start, 1);  

    Console.Write("\n Linked list before moving first to end\n");  
    printList(start);  

    start = moveToEnd(start);  

    Console.Write("\n Linked list after moving first to end\n");  
    printList(start);  
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```

# Python3 Program to move first element to end  
# in a given linked list  

# A linked list node  
class Node: 
    def __init__(self): 
        self.data = 0
        self.next = None

# We are using a double pointer head_ref  
# here because we change head of the linked  
# list inside this function. 
def moveToEnd( head_ref) : 

    # If linked list is empty, or it contains  
    # only one node, then nothing needs to be  
    # done, simply return  
    if (head_ref == None or (head_ref).next == None) : 
        return None

    # Initialize first and last pointers  
    first = head_ref  
    last = head_ref  

    # After this loop last contains address  
    # of last node in Linked List  
    while (last.next != None) : 

        last = last.next

    # Change the head pointer to point  
    # to second node now  
    head_ref = first.next

    # Set the next of first as None  
    first.next = None

    # Set the next of last as first  
    last.next = first  
    return head_ref 

# UTILITY FUNCTIONS  
# Function to add a node at the beginning  
# of Linked List  
def push( head_ref, new_data) : 

    new_node = Node()  
    new_node.data = new_data  
    new_node.next = (head_ref)  
    (head_ref) = new_node 
    return head_ref 

# Function to print nodes in a given linked list  
def printList(node) : 

    while (node != None): 

        print(node.data, end = " ")  
        node = node.next

# Driver code  

start = None

# The constructed linked list is:  
#1.2.3.4.5  
start = push(start, 5)  
start = push(start, 4)  
start = push(start, 3)  
start = push(start, 2)  
start = push(start, 1)  

print("\n Linked list before moving first to end")  
printList(start)  

start = moveToEnd(start)  

print("\n Linked list after moving first to end")  
printList(start)  

# This code is contributed by Arnab Kundu 

```

**Output:**

```
Linked list before moving first to end
1 2 3 4 5 
 Linked list after moving first to end
2 3 4 5 1

```

**时间复杂度：** O（n），其中n是给定链接列表中的节点数。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。