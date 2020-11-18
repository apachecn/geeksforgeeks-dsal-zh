# 程序使用堆栈

来反向链接列表

给定一个链表。 任务是使用辅助堆栈反转链表元素的顺序。

**示例：**

```
Input : List = 3 -> 2 -> 1
Output : 1 -> 2 -> 3

Input : 9 -> 7 -> 4 -> 2
Output : 2 -> 4 -> 7 -> 9 

```

**算法**：

1.  遍历列表并将其所有节点压入堆栈。
2.  再次遍历头节点的列表，并从堆栈顶部弹出一个值，然后以相反的顺序连接它们。

下面是上述方法的实现：

## C++

```cpp

// C/C++ program to reverse linked list 
// using stack 

#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to 
   the head of a list and an int, push a new  
   node on the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 

    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to reverse linked list 
Node *reverseList(Node* head) 
{ 
    // Stack to store elements of list 
    stack<Node *> stk; 

    // Push the elements of list to stack 
    Node* ptr = head; 
    while (ptr->next != NULL) { 
        stk.push(ptr); 
        ptr = ptr->next; 
    } 

    // Pop from stack and replace 
    // current nodes value' 
    head = ptr; 
    while (!stk.empty()) { 
        ptr->next = stk.top(); 

        ptr = ptr->next; 
        stk.pop(); 
    } 

    ptr->next = NULL; 

    return head; 
} 

// Function to print the Linked list 
void printList(Node* head) 
{ 
    while (head) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver Code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct below list  
    1->2->3->4->5 */
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    head = reverseList(head); 

    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to reverse linked list  
// using stack  
import java.util.*; 
class GfG  
{  

/* Link list node */
static class Node 
{  
    int data;  
    Node next;  
} 
static Node head = null; 

/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new  
node on the front of the list. */
static void push( int new_data)  
{  
    Node new_node = new Node();  

    new_node.data = new_data;  
    new_node.next = (head);  
    (head) = new_node;  
}  

// Function to reverse linked list  
static Node reverseList(Node head)  
{  
    // Stack to store elements of list  
    Stack<Node > stk = new Stack<Node> ();  

    // Push the elements of list to stack  
    Node ptr = head;  
    while (ptr.next != null)  
    {  
        stk.push(ptr);  
        ptr = ptr.next;  
    }  

    // Pop from stack and replace  
    // current nodes value'  
    head = ptr;  
    while (!stk.isEmpty()) 
    {  
        ptr.next = stk.peek();  
        ptr = ptr.next;  
        stk.pop();  
    }  
    ptr.next = null;  

    return head;  
}  

// Function to print the Linked list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        System.out.print(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver Code  
public static void main(String[] args)  
{  
    /* Start with the empty list */
    //Node head = null;  

    /* Use push() to construct below list  
    1->2->3->4->5 */
    push( 5);  
    push( 4);  
    push( 3);  
    push( 2);  
    push( 1);  

    head = reverseList(head);  

    printList(head);  
} 
}  

// This code is contributed by Prerna Saini. 

```

## Python3

```py

# Python3 program to reverse a linked 
# list using stack  

# Link list node  
class Node: 

    def __init__(self, data, next): 
        self.data = data 
        self.next = next

class LinkedList: 

    def __init__(self): 
        self.head = None

    # Function to push a new Node in  
    # the linked list  
    def push(self, new_data):  

        new_node = Node(new_data, self.head)  
        self.head = new_node 

    # Function to reverse linked list  
    def reverseList(self):  

        # Stack to store elements of list  
        stk = [] 

        # Push the elements of list to stack  
        ptr = self.head  
        while ptr.next != None:  
            stk.append(ptr)  
            ptr = ptr.next

        # Pop from stack and replace  
        # current nodes value'  
        self.head = ptr  
        while len(stk) != 0:  
            ptr.next = stk.pop()  
            ptr = ptr.next

        ptr.next = None

    # Function to print the Linked list  
    def printList(self): 

        curr = self.head 
        while curr:  
            print(curr.data, end = " ")  
            curr = curr.next

# Driver Code  
if __name__ == "__main__": 

    # Start with the empty list 
    linkedList = LinkedList()  

    # Use push() to construct below list  
    # 1.2.3.4.5 
    linkedList.push(5)  
    linkedList.push(4)  
    linkedList.push(3)  
    linkedList.push(2)  
    linkedList.push(1)  

    linkedList.reverseList()  

    linkedList.printList()  

# This code is contributed by Rituraj Jain  

```

## C#

```cs

// C# program to reverse linked list  
// using stack  
using System; 
using System.Collections.Generic; 

class GfG  
{  

/* Link list node */
public class Node  
{  
    public int data;  
    public Node next;  
}  
static Node head = null;  

/* Given a reference (pointer to pointer) to  
the head of a list and an int, push a new  
node on the front of the list. */
static void push( int new_data)  
{  
    Node new_node = new Node();  

    new_node.data = new_data;  
    new_node.next = (head);  
    (head) = new_node;  
}  

// Function to reverse linked list  
static Node reverseList(Node head)  
{  
    // Stack to store elements of list  
    Stack<Node > stk = new Stack<Node> ();  

    // Push the elements of list to stack  
    Node ptr = head;  
    while (ptr.next != null)  
    {  
        stk.Push(ptr);  
        ptr = ptr.next;  
    }  

    // Pop from stack and replace  
    // current nodes value'  
    head = ptr;  
    while (stk.Count != 0) 
    {  
        ptr.next = stk.Peek();  
        ptr = ptr.next;  
        stk.Pop();  
    }  
    ptr.next = null;  

    return head;  
}  

// Function to print the Linked list  
static void printList(Node head)  
{  
    while (head != null)  
    {  
        Console.Write(head.data + " ");  
        head = head.next;  
    }  
}  

// Driver Code  
public static void Main(String[] args)  
{  
    /* Start with the empty list */
    //Node head = null;  

    /* Use push() to construct below list  
    1->2->3->4->5 */
    push( 5);  
    push( 4);  
    push( 3);  
    push( 2);  
    push( 1);  

    head = reverseList(head);  

    printList(head);  
}  
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
5 4 3 2 1

```

**时间复杂度：** O（n）

我们可以使用O（1）辅助空间反转链表。 请参阅[更多方法来反向链接列表](https://www.geeksforgeeks.org/reverse-a-linked-list/)。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。