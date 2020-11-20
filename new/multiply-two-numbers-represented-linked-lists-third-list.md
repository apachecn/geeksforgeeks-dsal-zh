# 将表示为链表的两个数字乘以第三个列表

> 原文：[https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists-third-list/](https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists-third-list/)

给定两个由链表表示的数字，编写一个函数，该函数返回新链表的开头，该头表示这些数字乘积的数字。

示例：

```
Input : 9->4->6
        8->4
Output : 7->9->4->6->4

Input : 9->9->9->4->6->9
        9->9->8->4->9
Output : 9->9->7->9->5->9->8->0->1->8->1

```

我们已经在下面的文章中讨论了一个解决方案。

[乘以链表表示的两个数字](https://www.geeksforgeeks.org/multiply-two-numbers-represented-linked-lists/)

上面讨论的解决方案将结果存储为整数。 她将结果存储在第三个列表中，以便可以处理大量数字。

还记得旧式乘法吗？ 我们模仿这个过程。 在纸上，我们将数字的最后一位乘以第二个数字，然后得出乘积。 现在离开最后一列，以同样的方式将一个数字的每个数字与另一个数字的每个数字相乘，并在每次写入结果时都离开最后一列。 然后添加这些构成数字的列。 现在，假设这些列为结果链表的节点。 我们以相反的方式生成结果链表。

**算法** [

```
Reverse both linked lists
Make a linked list of maximum result size (m + n + 1)
For each node of one list
  For each node of second list
   a) Multiply nodes
   b) Add digit in result LL at corresponding 
      position
   c) Now resultant node itself can be higher
      than one digit
   d) Make carry for next node
  Leave one last column means next time start
From next node in result list
Reverse the resulted linked list

```

## C++

```cpp

// C++ program to Multiply two numbers  
// represented as linked lists  
#include <bits/stdc++.h>  
using namespace std; 

// Linked list Node  
struct Node {  
    int data;  
    struct Node* next;  
};  

// Function to create a new Node  
// with given data  
struct Node* newNode(int data)  
{  
    struct Node* new_node =  
        (struct Node*)malloc(sizeof(struct Node));  
    new_node->data = data;  
    new_node->next = NULL;  
    return new_node;  
}  

// Function to insert a Node at the  
// beginning of the Linked List  
void push(struct Node** head_ref, int new_data)  
{  
    // allocate Node  
    struct Node* new_node = newNode(new_data);  

    // link the old list off the new Node  
    new_node->next = (*head_ref);  

    // move the head to point to the new Node  
    (*head_ref) = new_node;  
}  

// Function to reverse the linked list and return  
// its length  
int reverse(struct Node** head_ref)  
{  
    struct Node* prev = NULL;  
    struct Node* current = *head_ref;  
    struct Node* next;  
    int len = 0;  
    while (current != NULL) {  
        len++;  
        next = current->next;  
        current->next = prev;  
        prev = current;  
        current = next;  
    }  
    *head_ref = prev;  
    return len;  
}  

// Function to make an empty linked list of  
// given size  
struct Node* make_empty_list(int size)  
{  
    struct Node* head = NULL;  
    while (size--)  
        push(&head, 0);  
    return head;  
}  

// Multiply contents of two linked lists => store  
// in another list and return its head  
struct Node* multiplyTwoLists(struct Node* first,  
                        struct Node* second)  
{  
    // reverse the lists to muliply from end  
    // m and n lengths of linked lists to make  
    // and empty list  
    int m = reverse(&first), n = reverse(&second);  

    // make a list that will contain the result  
    // of multiplication.  
    // m+n+1 can be max size of the list  
    struct Node* result = make_empty_list(m + n + 1);  

    // pointers for traverse linked lists and also  
    // to reverse them after  
    struct Node *second_ptr = second,  
        *result_ptr1 = result, *result_ptr2, *first_ptr;  

    // multiply each Node of second list with first  
    while (second_ptr) {  

        int carry = 0;  

        // each time we start from the next of Node  
        // from which we started last time  
        result_ptr2 = result_ptr1;  

        first_ptr = first;  

        while (first_ptr) {  

            // multiply a first list's digit with a  
            // current second list's digit  
            int mul = first_ptr->data * second_ptr->data  
                    + carry;  

            // Assigne the product to corresponding Node  
            // of result  
            result_ptr2->data += mul % 10;  

            // now resultant Node itself can have more  
            // than 1 digit  
            carry = mul / 10 + result_ptr2->data / 10;  
            result_ptr2->data = result_ptr2->data % 10;  

            first_ptr = first_ptr->next;  
            result_ptr2 = result_ptr2->next;  
        }  

        // if carry is remaining from last multiplication  
        if (carry > 0) {  
            result_ptr2->data += carry;  
        }  

        result_ptr1 = result_ptr1->next;  
        second_ptr = second_ptr->next;  
    }  

    // reverse the result_list as it was populated  
    // from last Node  
    reverse(&result);  
    reverse(&first);  
    reverse(&second);  

    // remove if there are zeros at starting  
    while (result->data == 0) {  
        struct Node* temp = result;  
        result = result->next;  
        free(temp);  
    }  

    // Return head of multiplication list  
    return result;  
}  

// A utility function to print a linked list  
void printList(struct Node* Node)  
{  
    while (Node != NULL) {  
        cout << Node->data;  
        if (Node->next)  
            cout<<"->";  
        Node = Node->next;  
    }  
    cout << endl;  
}  

// Driver program to test above function  
int main(void)  
{  
    struct Node* first = NULL;  
    struct Node* second = NULL;  

    // create first list 9->9->9->4->6->9  
    push(&first, 9);  
    push(&first, 6);  
    push(&first, 4);  
    push(&first, 9);  
    push(&first, 9);  
    push(&first, 9);  
    cout<<"First List is: ";  
    printList(first);  

    // create second list 9->9->8->4->9  
    push(&second, 9);  
    push(&second, 4);  
    push(&second, 8);  
    push(&second, 9);  
    push(&second, 9);  
    cout<<"Second List is: ";  
    printList(second);  

    // Multiply the two lists and see result  
    struct Node* result = multiplyTwoLists(first, second);  
    cout << "Resultant list is: ";  
    printList(result);  

    return 0;  
}  

// This code is contributed by SHUBHAMSINGH10 

```

## C

```c

// C program to Multiply two numbers 
// represented as linked lists 
#include <stdio.h> 
#include <stdlib.h> 

// Linked list Node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to create a new Node 
// with given data 
struct Node* newNode(int data) 
{ 
    struct Node* new_node = 
        (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Function to insert a Node at the 
// beginning of the Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate Node 
    struct Node* new_node = newNode(new_data); 

    // link the old list off the new Node 
    new_node->next = (*head_ref); 

    // move the head to point to the new Node 
    (*head_ref) = new_node; 
} 

// Function to reverse the linked list and return 
// its length 
int reverse(struct Node** head_ref) 
{ 
    struct Node* prev = NULL; 
    struct Node* current = *head_ref; 
    struct Node* next; 
    int len = 0; 
    while (current != NULL) { 
        len++; 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 
    *head_ref = prev; 
    return len; 
} 

// Function to make an empty linked list of 
// given size 
struct Node* make_empty_list(int size) 
{ 
    struct Node* head = NULL; 
    while (size--) 
        push(&head, 0); 
    return head; 
} 

// Multiply contents of two linked lists => store 
// in another list and return its head 
struct Node* multiplyTwoLists(struct Node* first, 
                           struct Node* second) 
{ 
    // reverse the lists to muliply from end 
    // m and n lengths of linked lists to make 
    // and empty list 
    int m = reverse(&first), n = reverse(&second); 

    // make a list that will contain the result 
    // of multiplication. 
    // m+n+1 can be max size of the list 
    struct Node* result = make_empty_list(m + n + 1); 

    // pointers for traverse linked lists and also 
    // to reverse them after 
    struct Node *second_ptr = second, 
          *result_ptr1 = result, *result_ptr2, *first_ptr; 

    // multiply each Node of second list with first 
    while (second_ptr) { 

        int carry = 0; 

        // each time we start from the next of Node 
        // from which we started last time 
        result_ptr2 = result_ptr1; 

        first_ptr = first; 

        while (first_ptr) { 

            // multiply a first list's digit with a 
            // current second list's digit 
            int mul = first_ptr->data * second_ptr->data 
                      + carry; 

            // Assigne the product to corresponding Node 
            // of result 
            result_ptr2->data += mul % 10; 

            // now resultant Node itself can have more 
            // than 1 digit 
            carry = mul / 10 + result_ptr2->data / 10; 
            result_ptr2->data = result_ptr2->data % 10; 

            first_ptr = first_ptr->next; 
            result_ptr2 = result_ptr2->next; 
        } 

        // if carry is remaining from last multiplication 
        if (carry > 0) { 
            result_ptr2->data += carry; 
        } 

        result_ptr1 = result_ptr1->next; 
        second_ptr = second_ptr->next; 
    } 

    // reverse the result_list as it was populated 
    // from last Node 
    reverse(&result); 
    reverse(&first); 
    reverse(&second); 

    // remove if there are zeros at starting 
    while (result->data == 0) { 
        struct Node* temp = result; 
        result = result->next; 
        free(temp); 
    } 

    // Return head of multiplication list 
    return result; 
} 

// A utility function to print a linked list 
void printList(struct Node* Node) 
{ 
    while (Node != NULL) { 
        printf("%d", Node->data); 
        if (Node->next) 
            printf("->"); 
        Node = Node->next; 
    } 
    printf("\n"); 
} 

// Driver program to test above function 
int main(void) 
{ 
    struct Node* first = NULL; 
    struct Node* second = NULL; 

    // create first list 9->9->9->4->6->9 
    push(&first, 9); 
    push(&first, 6); 
    push(&first, 4); 
    push(&first, 9); 
    push(&first, 9); 
    push(&first, 9); 
    printf("First List is: "); 
    printList(first); 

    // create second list 9->9->8->4->9 
    push(&second, 9); 
    push(&second, 4); 
    push(&second, 8); 
    push(&second, 9); 
    push(&second, 9); 
    printf("Second List is: "); 
    printList(second); 

    // Multiply the two lists and see result 
    struct Node* result = multiplyTwoLists(first, second); 
    printf("Resultant list is: "); 
    printList(result); 

    return 0; 
} 

```

## Python3

```py

# Python3 program to multiply two numbers  
# represented as linked lists  

# Node class  
class Node:  

    # Function to initialize the node object  
    def __init__(self, data):  

        self.data = data  
        self.next = None 

# Linked List Class 
class LinkedList: 

    # Function to initialize the 
    # LinkedList class. 
    def __init__(self): 

        # Initialize head as None 
        self.head = None

    # This function insert a new node at the  
    # beginning of the linked list  
    def push(self, new_data):  

        # Create a new Node  
        new_node = Node(new_data)  

        # Make next of new Node as head  
        new_node.next = self.head  

        # Move the head to point to new Node  
        self.head = new_node 

    # Method to print the linked list 
    def printList(self): 

        # Object to iterate 
        # the list 
        ptr = self.head 

        # Loop to iterate list 
        while(ptr != None): 
            print(ptr.data, '->', end = '') 

            # Moving the iterating object 
            # to next node 
            ptr = ptr.next

        print() 

# Function to reverse the linked 
# list and return its length 
def reverse(head_ref): 

    # Initialising prev and current 
    # at None and starting node 
    # respectively. 
    prev = None
    current = head_ref.head 

    Len = 0

    # Loop to reverse the link 
    # of each node in the list 
    while(current != None): 
        Len += 1
        Next = current.next
        current.next = prev 
        prev = current 
        current = Next

    # Assigning new starting object 
    # to main head object. 
    head_ref.head = prev 

    # Returning the lemgth of 
    # linked list. 
    return Len

# Function to define an empty 
# linked list of given size and 
# each element as zero. 
def make_empty_list(size): 

    head = LinkedList() 

    while(size): 
        head.push(0) 
        size -= 1

    # Returns the head object. 
    return head 

# Multiply contents of two linked 
# list store it in other list and 
# return its head. 
def multiplyTwoLists(first, second): 

    # Reverse the list to multiply from  
    # end m and n lengths of linked list 
    # to make and empty list 
    m = reverse(first) 
    n = reverse(second) 

    # Make a list that will contain the 
    # result of multiplication. 
    # m+n+1 can be max size of the list. 
    result = make_empty_list(m + n + 1) 

    # Objects for traverse linked list 
    # and also to reverse them after. 
    second_ptr = second.head 
    result_ptr1 = result.head 

    # Multiply each node of second 
    # list with first. 
    while(second_ptr != None): 
        carry = 0

        # Each time we start from next 
        # node from which we started last 
        # time. 
        result_ptr2 = result_ptr1 
        first_ptr = first.head 

        while(first_ptr != None): 

            # Multiply a first list's digit 
            # with a current second list's digit. 
            mul = ((first_ptr.data) * 
                  (second_ptr.data) + carry) 

            # Assign the product to corresponding 
            # node of result. 
            result_ptr2.data += mul % 10

            # Now resultant node itself can have 
            # more then one digit. 
            carry = ((mul // 10) + 
                     (result_ptr2.data // 10)) 
            result_ptr2.data = result_ptr2.data % 10

            first_ptr = first_ptr.next
            result_ptr2 = result_ptr2.next

        # If carry is remaining from 
        # last multiplication 
        if(carry > 0): 
            result_ptr2.data += carry 

        result_ptr1 = result_ptr1.next
        second_ptr = second_ptr.next

    # Reverse the result_list as it 
    # was populated from last node 
    reverse(result) 
    reverse(first) 
    reverse(second) 

    # Remove starting nodes 
    # containing zeroes. 
    start = result.head 
    while(start.data == 0): 
        result.head = start.next
        start = start.next

    # Return the resultant multiplicated 
    # linked list. 
    return result 

# Driver code 
if __name__=='__main__': 

    first = LinkedList() 
    second = LinkedList() 

    # Pushing elements at start of 
    # first linked list. 
    first.push(9) 
    first.push(6) 
    first.push(4) 
    first.push(9) 
    first.push(9) 
    first.push(9) 

    # Printing first linked list 
    print("First list is: ", end = '') 
    first.printList() 

    # Pushing elements at start of 
    # second linked list. 
    second.push(9) 
    second.push(4) 
    second.push(8) 
    second.push(9) 
    second.push(9) 

    # Printing second linked list. 
    print("Second List is: ", end = '') 
    second.printList() 

    # Multiply two linked list and 
    # print the result. 
    result = multiplyTwoLists(first, second) 
    print("Resultant list is: ", end = '') 
    result.printList() 

# This code is contributed by Amit Mangal 

```

输出：

```
First List is: 9->9->9->4->6->9
Second List is: 9->9->8->4->9
Resultant list is: 9->9->7->9->5->9->8->0->1->8->1

```

注意：我们可以照顾到结果结点，该结点在循环外可以有 1 位以上的数字，只需遍历结果列表并在反转之前将进位加到下一位数字即可。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。