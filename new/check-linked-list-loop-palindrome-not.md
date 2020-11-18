# 检查带有循环的链表是否为回文

> 原文：[https://www.geeksforgeeks.org/check-linked-list-loop-palindrome-not/](https://www.geeksforgeeks.org/check-linked-list-loop-palindrome-not/)

给定一个带有循环的链表，任务是查找它是否是回文。 您无权删除循环。

![](img/de522899e01a1322ab2808eeff1ad73e.png)

例子：

```
Input : 1 -> 2 -> 3 -> 2
             /|\      \|/
               ------- 1  
Output: Palindrome
Linked list is 1 2 3 2 1 which is a 
palindrome.

Input : 1 -> 2 -> 3 -> 4
             /|\      \|/
               ------- 1  
Output: Not Palindrome
Linked list is 1 2 3 4 1 which is a 
not palindrome.

```

算法：

1.  使用弗洛伊德循环检测算法检测环路。

2.  然后按照[和](https://www.geeksforgeeks.org/detect-and-remove-loop-in-a-linked-list/)中的讨论找到循环的起始节点

3.  如[和](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)中所述，检查链表是否是回文

下面是实现。

## C++

```cpp

// C++ program to check if a linked list with 
// loop is palindrome or not. 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node 
{ 
    int data; 
    struct Node * next; 
}; 

/* Function to find loop starting node. 
loop_node --> Pointer to one of the loop nodes 
head --> Pointer to the start node of the linked list */
Node* getLoopstart(Node *loop_node, Node *head) 
{ 
    Node *ptr1 = loop_node; 
    Node *ptr2 = loop_node; 

    // Count the number of nodes in loop 
    unsigned int k = 1, i; 
    while (ptr1->next != ptr2) 
    { 
        ptr1 = ptr1->next; 
        k++; 
    } 

    // Fix one pointer to head 
    ptr1 = head; 

    // And the other pointer to k nodes after head 
    ptr2 = head; 
    for (i = 0; i < k; i++) 
        ptr2 = ptr2->next; 

    /* Move both pointers at the same pace, 
    they will meet at loop starting node */
    while (ptr2 != ptr1) 
    { 
        ptr1 = ptr1->next; 
        ptr2 = ptr2->next; 
    } 
    return ptr1; 
} 

/* This function detects and find loop starting 
  node  in the list*/
Node* detectAndgetLoopstarting(Node *head) 
{ 
    Node *slow_p = head, *fast_p = head,*loop_start; 

    //Start traversing list and detect loop 
    while (slow_p && fast_p && fast_p->next) 
    { 
        slow_p = slow_p->next; 
        fast_p = fast_p->next->next; 

        /* If slow_p and fast_p meet then find 
           the loop starting node*/
        if (slow_p == fast_p) 
        { 
            loop_start = getLoopstart(slow_p, head); 
            break; 
        } 
    } 

    // Return starting node of loop 
    return loop_start; 
} 

// Utility function to check if a linked list with loop 
// is palindrome with given starting point. 
bool isPalindromeUtil(Node *head, Node* loop_start) 
{ 
    Node *ptr = head; 
    stack<int> s; 

    // Traverse linked list until last node is equal 
    // to loop_start and store the elements till start 
    // in a stack 
    int count = 0; 
    while (ptr != loop_start || count != 1) 
    { 
        s.push(ptr->data); 
        if (ptr == loop_start) 
            count = 1; 
        ptr = ptr->next; 
    } 
    ptr = head; 
    count = 0; 

    // Traverse linked list until last node is 
    // equal to loop_start second time 
    while (ptr != loop_start || count != 1) 
    { 
        // Compare data of node with the top of stack 
        // If equal then continue 
        if (ptr->data == s.top()) 
            s.pop(); 

        // Else return false 
        else
            return false; 

        if (ptr == loop_start) 
            count = 1; 
        ptr = ptr->next; 
    } 

    // Return true if linked list is palindrome 
    return true; 
} 

// Function to find if linked list is palindrome or not 
bool isPalindrome(Node* head) 
{ 
    // Find the loop starting node 
    Node* loop_start = detectAndgetLoopstarting(head); 

    // Check if linked list is palindrome 
    return isPalindromeUtil(head, loop_start); 
} 

Node *newNode(int key) 
{ 
    Node *temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above function*/
int main() 
{ 
    Node *head = newNode(50); 
    head->next = newNode(20); 
    head->next->next = newNode(15); 
    head->next->next->next = newNode(20); 
    head->next->next->next->next = newNode(50); 

    /* Create a loop for testing */
    head->next->next->next->next->next = head->next->next; 

    isPalindrome(head)? cout << "\nPalindrome"
                     : cout << "\nNot Palindrome"; 

    return 0; 
} 

```

## Java

```java

// Java program to check if a linked list 
// with loop is palindrome or not. 
import java.util.*; 

class GfG  
{ 

/* Link list node */
static class Node  
{  
    int data;  
    Node next;  
} 

/* Function to find loop starting node.  
loop_node --> Pointer to one of  
the loop nodes head --> Pointer to  
the start node of the linked list */
static Node getLoopstart(Node loop_node,  
                            Node head)  
{  
    Node ptr1 = loop_node;  
    Node ptr2 = loop_node;  

    // Count the number of nodes in loop  
    int k = 1, i;  
    while (ptr1.next != ptr2)  
    {  
        ptr1 = ptr1.next;  
        k++;  
    }  

    // Fix one pointer to head  
    ptr1 = head;  

    // And the other pointer to k  
    // nodes after head  
    ptr2 = head;  
    for (i = 0; i < k; i++)  
        ptr2 = ptr2.next;  

    /* Move both pointers at the same pace,  
    they will meet at loop starting node */
    while (ptr2 != ptr1)  
    {  
        ptr1 = ptr1.next;  
        ptr2 = ptr2.next;  
    }  
    return ptr1;  
}  

/* This function detects and find  
loop starting node in the list*/
static Node detectAndgetLoopstarting(Node head)  
{  
    Node slow_p = head, fast_p = head,loop_start = null;  

    //Start traversing list and detect loop  
    while (slow_p != null && fast_p != null &&  
            fast_p.next != null)  
    {  
        slow_p = slow_p.next;  
        fast_p = fast_p.next.next;  

        /* If slow_p and fast_p meet then find  
        the loop starting node*/
        if (slow_p == fast_p)  
        {  
            loop_start = getLoopstart(slow_p, head);  
            break;  
        }  
    }  

    // Return starting node of loop  
    return loop_start;  
}  

// Utility function to check if   
// a linked list with loop is  
// palindrome with given starting point.  
static boolean isPalindromeUtil(Node head, 
                            Node loop_start)  
{  
    Node ptr = head;  
    Stack<Integer> s = new Stack<Integer> ();  

    // Traverse linked list until last node   
    // is equal to loop_start and store the   
    // elements till start in a stack  
    int count = 0;  
    while (ptr != loop_start || count != 1)  
    {  
        s.push(ptr.data);  
        if (ptr == loop_start)  
            count = 1;  
        ptr = ptr.next;  
    }  
    ptr = head;  
    count = 0;  

    // Traverse linked list until last node is  
    // equal to loop_start second time  
    while (ptr != loop_start || count != 1)  
    {  
        // Compare data of node with the top of stack  
        // If equal then continue  
        if (ptr.data == s.peek())  
            s.pop();  

        // Else return false  
        else
            return false;  

        if (ptr == loop_start)  
            count = 1;  
        ptr = ptr.next;  
    }  

    // Return true if linked list is palindrome  
    return true;  
}  

// Function to find if linked list 
// is palindrome or not  
static boolean isPalindrome(Node head)  
{  
    // Find the loop starting node  
    Node loop_start = detectAndgetLoopstarting(head);  

    // Check if linked list is palindrome  
    return isPalindromeUtil(head, loop_start);  
}  

static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

/* Driver code*/
public static void main(String[] args)  
{  
    Node head = newNode(50);  
    head.next = newNode(20);  
    head.next.next = newNode(15);  
    head.next.next.next = newNode(20);  
    head.next.next.next.next = newNode(50);  

    /* Create a loop for testing */
    head.next.next.next.next.next = head.next.next;  

    if(isPalindrome(head) == true) 
        System.out.println("Palindrome"); 
    else
        System.out.println("Not Palindrome");  

} 
}  

// This code is contributed by prerna saini 

```

## Python

```py

# Python3 program to check if a linked list 
# with loop is palindrome or not. 

# Node class  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to find loop starting node.  
# loop_node -. Pointer to one of  
# the loop nodes head -. Pointer to  
# the start node of the linked list 
def getLoopstart(loop_node,head):  

    ptr1 = loop_node  
    ptr2 = loop_node  

    # Count the number of nodes in loop  
    k = 1
    i = 0
    while (ptr1.next != ptr2):  

        ptr1 = ptr1.next
        k = k + 1

    # Fix one pointer to head  
    ptr1 = head  

    # And the other pointer to k  
    # nodes after head  
    ptr2 = head 
    i = 0
    while ( i < k ) : 
        ptr2 = ptr2.next
        i = i + 1

    # Move both pointers at the same pace,  
    #they will meet at loop starting node */ 
    while (ptr2 != ptr1):  

        ptr1 = ptr1.next
        ptr2 = ptr2.next

    return ptr1  

# This function detects and find  
# loop starting node in the list 
def detectAndgetLoopstarting(head):  

    slow_p = head 
    fast_p = head 
    loop_start = None

    # Start traversing list and detect loop  
    while (slow_p != None and fast_p != None and
            fast_p.next != None) : 

        slow_p = slow_p.next
        fast_p = fast_p.next.next

        # If slow_p and fast_p meet then find  
        # the loop starting node 
        if (slow_p == fast_p) : 

            loop_start = getLoopstart(slow_p, head)  
            break

    # Return starting node of loop  
    return loop_start  

# Utility function to check if  
# a linked list with loop is  
# palindrome with given starting point.  
def isPalindromeUtil(head, loop_start):  

    ptr = head  
    s = []  

    # Traverse linked list until last node  
    # is equal to loop_start and store the  
    # elements till start in a stack  
    count = 0
    while (ptr != loop_start or count != 1):  

        s.append(ptr.data)  
        if (ptr == loop_start) : 
            count = 1
        ptr = ptr.next

    ptr = head  
    count = 0

    # Traverse linked list until last node is  
    # equal to loop_start second time  
    while (ptr != loop_start or count != 1):  

        # Compare data of node with the top of stack  
        # If equal then continue  
        if (ptr.data == s[-1]):  
            s.pop()  

        # Else return False  
        else: 
            return False

        if (ptr == loop_start) : 
            count = 1
        ptr = ptr.next

    # Return True if linked list is palindrome  
    return True

# Function to find if linked list 
# is palindrome or not  
def isPalindrome(head) : 

    # Find the loop starting node  
    loop_start = detectAndgetLoopstarting(head)  

    # Check if linked list is palindrome  
    return isPalindromeUtil(head, loop_start)  

def newNode(key) : 

    temp = Node(0)  
    temp.data = key  
    temp.next = None
    return temp  

# Driver code 
head = newNode(50)  
head.next = newNode(20)  
head.next.next = newNode(15)  
head.next.next.next = newNode(20)  
head.next.next.next.next = newNode(50)  

# Create a loop for testing  
head.next.next.next.next.next = head.next.next

if(isPalindrome(head) == True): 
    print("Palindrome") 
else: 
    print("Not Palindrome")  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to check if a linked list 
// with loop is palindrome or not. 
using System; 
using System.Collections.Generic;  

class GfG  
{ 

/* Link list node */
class Node  
{  
    public int data;  
    public Node next;  
} 

/* Function to find loop starting node.  
loop_node --> Pointer to one of  
the loop nodes head --> Pointer to  
the start node of the linked list */
static Node getLoopstart(Node loop_node,  
                            Node head)  
{  
    Node ptr1 = loop_node;  
    Node ptr2 = loop_node;  

    // Count the number of nodes in loop  
    int k = 1, i;  
    while (ptr1.next != ptr2)  
    {  
        ptr1 = ptr1.next;  
        k++;  
    }  

    // Fix one pointer to head  
    ptr1 = head;  

    // And the other pointer to k  
    // nodes after head  
    ptr2 = head;  
    for (i = 0; i < k; i++)  
        ptr2 = ptr2.next;  

    /* Move both pointers at the same pace,  
    they will meet at loop starting node */
    while (ptr2 != ptr1)  
    {  
        ptr1 = ptr1.next;  
        ptr2 = ptr2.next;  
    }  
    return ptr1;  
}  

/* This function detects and find  
loop starting node in the list*/
static Node detectAndgetLoopstarting(Node head)  
{  
    Node slow_p = head, fast_p = head,loop_start = null;  

    //Start traversing list and detect loop  
    while (slow_p != null && fast_p != null &&  
            fast_p.next != null)  
    {  
        slow_p = slow_p.next;  
        fast_p = fast_p.next.next;  

        /* If slow_p and fast_p meet then find  
        the loop starting node*/
        if (slow_p == fast_p)  
        {  
            loop_start = getLoopstart(slow_p, head);  
            break;  
        }  
    }  

    // Return starting node of loop  
    return loop_start;  
}  

// Utility function to check if  
// a linked list with loop is  
// palindrome with given starting point.  
static bool isPalindromeUtil(Node head, 
                            Node loop_start)  
{  
    Node ptr = head;  
    Stack<int> s = new Stack<int> ();  

    // Traverse linked list until last node  
    // is equal to loop_start and store the  
    // elements till start in a stack  
    int count = 0;  
    while (ptr != loop_start || count != 1)  
    {  
        s.Push(ptr.data);  
        if (ptr == loop_start)  
            count = 1;  
        ptr = ptr.next;  
    }  
    ptr = head;  
    count = 0;  

    // Traverse linked list until last node is  
    // equal to loop_start second time  
    while (ptr != loop_start || count != 1)  
    {  
        // Compare data of node with the top of stack  
        // If equal then continue  
        if (ptr.data == s.Peek())  
            s.Pop();  

        // Else return false  
        else
            return false;  

        if (ptr == loop_start)  
            count = 1;  
        ptr = ptr.next;  
    }  

    // Return true if linked list is palindrome  
    return true;  
}  

// Function to find if linked list 
// is palindrome or not  
static bool isPalindrome(Node head)  
{  
    // Find the loop starting node  
    Node loop_start = detectAndgetLoopstarting(head);  

    // Check if linked list is palindrome  
    return isPalindromeUtil(head, loop_start);  
}  

static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

/* Driver code*/
public static void Main(String[] args)  
{  
    Node head = newNode(50);  
    head.next = newNode(20);  
    head.next.next = newNode(15);  
    head.next.next.next = newNode(20);  
    head.next.next.next.next = newNode(50);  

    /* Create a loop for testing */
    head.next.next.next.next.next = head.next.next;  

    if(isPalindrome(head) == true) 
        Console.WriteLine("Palindrome"); 
    else
        Console.WriteLine("Not Palindrome");  
} 
} 

/* This code is contributed by 29AjayKumar */

```

**Output:**

```
Palindrome

```

本文由 [**Sahil Chhabra（akku）**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

