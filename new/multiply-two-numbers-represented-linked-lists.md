# 将两个数字乘以链表

> 原文：[https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists/](https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists/)

给定两个由链表表示的数字，编写一个函数返回两个链表的乘积。

**示例**：

```
Input : 9->4->6
        8->4
Output : 79464

Input : 3->2->1
        1->2
Output : 3852

```

**解决方案**：

遍历两个列表并生成要相乘的所需数字，然后返回两个数字的相乘值。

从链表表示中生成数字的算法：

```
1) Initialize a variable to zero
2) Start traversing the linked list
3) Add the value of first node to this variable
4) From the second node, multiply the variable by 10
   first and then add the value of the node to this 
   variable.
5) Repeat step 4 until we reach the last node of the list. 

```

将上述算法与两个链表一起使用以生成数字。

下面是将两个数字相乘的程序，它们表示为链表：

## C/C++ 

```cpp

// C program to Multiply two numbers 
// represented as linked lists 
#include<stdio.h> 
#include<stdlib.h> 

// Linked list node 
struct node 
{ 
    int data; 
    struct node* next; 
}; 

// Function to create a new node  
// with given data 
struct node *newNode(int data) 
{ 
    struct node *new_node = (struct node *) malloc(sizeof(struct node)); 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Function to insert a node at the  
// beginning of the Linked List 
void push(struct node** head_ref, int new_data) 
{ 
    // allocate node  
    struct node* new_node = newNode(new_data); 

    // link the old list off the new node  
    new_node->next = (*head_ref); 

    // move the head to point to the new node  
    (*head_ref) = new_node; 
} 

// Multiply contents of two linked lists 
long multiplyTwoLists (struct node* first, struct node* second) 
{ 
    int num1 = 0, num2 = 0; 

    // Generate numbers from linked lists 
    while (first || second) 
    { 
        if (first) 
        { 
            num1 = num1*10 + first->data; 
            first = first->next; 
        } 
        if (second) 
        { 
            num2 = num2*10 + second->data; 
            second = second->next; 
        } 
    } 

    // Return multiplication of  
    // two numbers 
    return num1*num2; 
} 

// A utility function to print a linked list 
void printList(struct node *node) 
{ 
    while(node != NULL) 
    { 
        printf("%d", node->data); 
        if(node->next) 
            printf("->"); 
        node = node->next; 
    } 
    printf("\n"); 
} 

// Driver program to test above function 
int main(void) 
{ 
    struct node* first = NULL; 
    struct node* second = NULL; 

    // create first list 9->4->6 
    push(&first, 6); 
    push(&first, 4); 
    push(&first, 9); 
    printf("First List is: "); 
    printList(first); 

    // create second list 8->4 
    push(&second, 4); 
    push(&second, 8); 
    printf("Second List is: "); 
    printList(second); 

    // Multiply the two lists and see result 
    printf("Result is: "); 
    printf("%ld", multiplyTwoLists(first, second)); 

    return 0; 
} 

```

## Java

```java

// Java program to Multiply two numbers  
// represented as linked lists  
class GFG 
{ 

// Linked list node  
static class node  
{  
    int data;  
    node next;  
};  

// Function to create a new node  
// with given data  
static node newNode(int data)  
{  
    node new_node = new node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to insert a node at the  
// beginning of the Linked List  
static node push( node head_ref, int new_data)  
{  
    // allocate node  
    node new_node = newNode(new_data);  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Multiply contents of two linked lists  
static long multiplyTwoLists ( node first, node second)  
{  
    int num1 = 0, num2 = 0;  

    // Generate numbers from linked lists  
    while (first != null || second != null)  
    {  
        if (first != null)  
        {  
            num1 = num1*10 + first.data;  
            first = first.next;  
        }  
        if (second != null)  
        {  
            num2 = num2*10 + second.data;  
            second = second.next;  
        }  
    }  

    // Return multiplication of  
    // two numbers  
    return num1*num2;  
}  

// A utility function to print a linked list  
static void printList( node node)  
{  
    while(node != null)  
    {  
        System.out.printf("%d", node.data);  
        if(node.next != null)  
            System.out.printf("->");  
        node = node.next;  
    }  
    System.out.printf("\n");  
}  

// Driver code  
public static void main(String args[]) 
{  
    node first = null;  
    node second = null;  

    // create first list 9.4.6  
    first = push(first, 6);  
    first = push(first, 4);  
    first = push(first, 9);  
    System.out.printf("First List is: ");  
    printList(first);  

    // create second list 8.4  
    second = push(second, 4);  
    second = push(second, 8);  
    System.out.printf("Second List is: ");  
    printList(second);  

    // Multiply the two lists and see result  
    System.out.printf("Result is: ");  
    System.out.println(multiplyTwoLists(first, second));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python program to Multiply 
# two linkedlists 

# Linked List Node 
class Node(): 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Linked List class 
class singly_linked_list(): 
    def __init__(self): 
        self.head = None

    def add(self, node): 

        '''Add a node to the linked list'''
        if not self.head: 

            # If no nodes exist, assign the 
            # new node to the head node. 
            self.head = node 
        else: 

            # Link the old stuff  
            # to the new node 
            node.next = self.head 

            # Move the head node to 
            # point to the new node 
            self.head = node 

    def __repr__(self): 

        '''Returns a string object containing 
           a representation of the linked list.'''
        next = self.head 
        str_repr = "" 
        while(next): 
            str_repr += str(next.data) 
            if next.next: str_repr += "->"
            next = next.next
        return str_repr 

def multiply_linked_lists(list1, list2): 

    '''Generates the numberic representation 
       of 2 linked lists and returns their product.'''
    first_number = 0
    second_number = 0

    # Generate the first number 
    next = list1.head 
    while next: 
        first_number = (first_number * 
                        10 + next.data) 
        next = next.next

    # Generate the second number 
    next = list2.head 
    while next: 
        second_number = (second_number *
                         10 + next.data) 
        next = next.next

    # Return the product 
    return first_number * second_number 

# Driver Code 

# Instantiate 2 linked lists 
l_list1 = singly_linked_list() 
l_list2 = singly_linked_list() 

# Create first list 
l_list1.add(Node(6)) 
l_list1.add(Node(4)) 
l_list1.add(Node(9)) 

# Create second list 
l_list2.add(Node(4)) 
l_list2.add(Node(8)) 

print("First list is: ", l_list1) 
print("Second list is: ", l_list2) 

print("Results is: ",  
       multiply_linked_lists(l_list1, l_list2)) 

# This code is contributed  
# by harishkumar88 

```

## C#

```cs

// C# program to Multiply two numbers  
// represented as linked lists 
using System; 
public class GFG  
{  

// Linked list node  
public class node  
{  
    public int data;  
    public node next;  
};  

// Function to create a new node  
// with given data  
static node newNode(int data)  
{  
    node new_node = new node();  
    new_node.data = data;  
    new_node.next = null;  
    return new_node;  
}  

// Function to insert a node at the  
// beginning of the Linked List  
static node push( node head_ref, int new_data)  
{  
    // allocate node  
    node new_node = newNode(new_data);  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref;  
}  

// Multiply contents of two linked lists  
static long multiplyTwoLists ( node first, node second)  
{  
    int num1 = 0, num2 = 0;  

    // Generate numbers from linked lists  
    while (first != null || second != null)  
    {  
        if (first != null)  
        {  
            num1 = num1*10 + first.data;  
            first = first.next;  
        }  
        if (second != null)  
        {  
            num2 = num2*10 + second.data;  
            second = second.next;  
        }  
    }  

    // Return multiplication of  
    // two numbers  
    return num1*num2;  
}  

// A utility function to print a linked list  
static void printList( node node)  
{  
    while(node != null)  
    {  
        Console.Write("{0}", node.data);  
        if(node.next != null)  
            Console.Write("->");  
        node = node.next;  
    }  
    Console.Write("\n");  
}  

// Driver code  
public static void Main(String []args)  
{  
    node first = null;  
    node second = null;  

    // create first list 9.4.6  
    first = push(first, 6);  
    first = push(first, 4);  
    first = push(first, 9);  
    Console.Write("First List is: ");  
    printList(first);  

    // create second list 8.4  
    second = push(second, 4);  
    second = push(second, 8);  
    Console.Write("Second List is: ");  
    printList(second);  

    // Multiply the two lists and see result  
    Console.Write("Result is: ");  
    Console.Write(multiplyTwoLists(first, second));  
}  
}  

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
First List is: 9->4->6
Second List is: 8->4
Result is: 79464

```

### 询问：[亚马逊](https://practice.geeksforgeeks.org/company/Amazon/)

本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

