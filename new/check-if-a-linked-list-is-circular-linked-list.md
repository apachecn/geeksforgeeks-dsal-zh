# 检查链接列表是否为循环链接列表

给定单个链接列表，请查找链接列表是否为[圆形](http://geeksquiz.com/circular-linked-list/)。 如果链表不是以 NULL 结尾的，并且所有节点都以循环的形式连接，则称为循环表。 以下是循环链表的示例。

[![](img/edcbce05d23f3327116de91a2c124f5e.png)](https://media.geeksforgeeks.org/wp-content/uploads/Circular-Linked-List-Diagram.png)

空链表被认为是循环的。
请注意，此问题与[周期检测问题](https://practice.geeksforgeeks.org/problem-page.php?pid=700099)不同，此处所有节点都必须是周期的一部分。

这个想法是存储链表的头并遍历它。 如果达到 NULL，则链表不是循环的。 如果再次到达头部，则链表为圆形。

## C++

```cpp

// C++ program to check if linked list is circular 
#include<bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

/* This function returns true if given linked 
   list is circular, else false. */
bool isCircular(struct Node *head) 
{ 
    // An empty linked list is circular 
    if (head == NULL) 
       return true; 

    // Next of head 
    struct Node *node = head->next; 

    // This loop would stop in both cases (1) If 
    // Circular (2) Not circular 
    while (node != NULL && node != head) 
       node = node->next; 

    // If loop stopped because of circular 
    // condition 
    return (node == head); 
} 

// Utility function to create a new node. 
Node *newNode(int data) 
{ 
    struct Node *temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 

    isCircular(head)? cout << "Yes\n" : 
                      cout << "No\n" ; 

    // Making linked list circular 
    head->next->next->next->next = head; 

    isCircular(head)? cout << "Yes\n" : 
                      cout << "No\n" ; 

    return 0; 
} 

```

## Java

```java

// Java program to check if  
// linked list is circular 
import java.util.*; 

class GFG 
{ 

/* Link list Node */
static class Node 
{ 
    int data; 
    Node next; 
} 

/*This function returns true if given linked 
list is circular, else false. */
static boolean isCircular( Node head) 
{ 
    // An empty linked list is circular 
    if (head == null) 
    return true; 

    // Next of head 
    Node node = head.next; 

    // This loop would stop in both cases (1) If 
    // Circular (2) Not circular 
    while (node != null && node != head) 
    node = node.next; 

    // If loop stopped because of circular 
    // condition 
    return (node == head); 
} 

// Utility function to create a new node. 
static Node newNode(int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 
    return temp; 
} 

/* Driver code*/
public static void main(String args[]) 
{ 
    /* Start with the empty list */
    Node head = newNode(1); 
    head.next = newNode(2); 
    head.next.next = newNode(3); 
    head.next.next.next = newNode(4); 

    System.out.print(isCircular(head)? "Yes\n" : 
                    "No\n" ); 

    // Making linked list circular 
    head.next.next.next.next = head; 

    System.out.print(isCircular(head)? "Yes\n" : 
                    "No\n" ); 

} 
} 

// This code contributed by Arnab Kundu 

```

## Python3

```py

# A simple Python program to check if a linked list is circular 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data # Assign data  
        self.next = None # Initialize next as null  

# Linked List class contains a Node object  
class LinkedList:  

    # Function to initialize head  
    def __init__(self):  
        self.head = None

def Circular(head): 
    if head==None: 
        return True

    # Next of head 
    node = head.next
    i = 0

    # This loop would stop in both cases (1) If 
    # Circular (2) Not circular 
    while((node is not None) and (node is not head)): 
        i = i + 1
        node = node.next

    return(node==head) 

# Code execution starts here  
if __name__=='__main__': 
    llist = LinkedList()  
    llist.head = Node(1) 
    second = Node(2) 
    third = Node(3)  
    fourth = Node(4) 

    llist.head.next = second; 
    second.next = third; 
    third.next = fourth 

    if (Circular(llist.head)): 
        print('Yes') 
    else: 
        print('No') 

    fourth.next = llist.head 

    if (Circular(llist.head)): 
        print('Yes') 
    else: 
        print('No') 

# This code is contributed by Sanket Badhe 

```

## C#

```cs

// C# program to check if  
// linked list is circular  
using System; 
public class GFG  
{  

/* Link list Node */
public class Node  
{  
    public int data;  
    public Node next;  
}  

/*This function returns true if given linked  
list is circular, else false. */
static bool isCircular( Node head)  
{  
    // An empty linked list is circular  
    if (head == null)  
    return true;  

    // Next of head  
    Node node = head.next;  

    // This loop would stop in both cases (1) If  
    // Circular (2) Not circular  
    while (node != null && node != head)  
    node = node.next;  

    // If loop stopped because of circular  
    // condition  
    return (node == head);  
}  

// Utility function to create a new node.  
static Node newNode(int data)  
{  
    Node temp = new Node();  
    temp.data = data;  
    temp.next = null;  
    return temp;  
}  

/* Driver code*/
public static void Main(String []args)  
{  
    /* Start with the empty list */
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  

    Console.Write(isCircular(head)? "Yes\n" :  
                    "No\n" );  

    // Making linked list circular  
    head.next.next.next.next = head;  

    Console.Write(isCircular(head)? "Yes\n" :  
                    "No\n" );  

}  
}  
// This code has been contributed by 29AjayKumar 

```

**输出：**

```
No
Yes

```

本文由 **Shivam Gupta** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，那么您也可以写一篇文章，然后将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

