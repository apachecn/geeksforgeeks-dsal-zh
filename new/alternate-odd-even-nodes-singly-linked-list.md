# 单链表中的备用奇偶节点

> 原文：[https://www.geeksforgeeks.org/alternate-odd-even-nodes-singly-linked-list/](https://www.geeksforgeeks.org/alternate-odd-even-nodes-singly-linked-list/)

给定一个单链列表，请重新排列该列表，以使偶数和奇数节点在列表中交替出现。

这种重新排列有两种可能的形式。 如果第一个数据为奇数，则第二个节点必须为偶数。 第三个节点必须是奇数，依此类推。 请注意，在第一个节点为偶数，第二个奇数，第三个偶数等的情况下，还有另一种安排。

**示例**：

```
Input : 11 -> 20 -> 40 -> 55 -> 77 -> 80 -> NULL
Output : 11 -> 20 -> 55 -> 40 -> 77 -> 80 -> NULL
20, 40, 80 occur in even positions and 11, 55, 77
occur in odd positions.

Input : 10 -> 1 -> 2 -> 3 -> 5 -> 6 -> 7 -> 8 -> NULL
Output : 1 -> 10 -> 3 -> 2 -> 5 -> 6 -> 7 -> 8 -> NULL
1, 3, 5, 7 occur in odd positions and 10, 2, 6, 8 occur
at even positions in the list

```

**方法 1（简单）**

在此方法中，我们创建两个栈-奇数和偶数。 我们遍历该列表，当我们在奇数位置遇到偶数节点时，便将该节点的地址压入偶数栈。 如果我们在偶数位置遇到一个奇数节点，则将该节点的地址压入奇数栈。

遍历列表后，我们只需弹出两个栈顶部的节点并交换它们的数据即可。 我们一直重复此步骤，直到栈变空。

> 步骤 1：创建两个栈，奇数和偶数。 这些栈会存储指向列表中的节点的指针。
>
> 步骤 2：使用变量`current`从头到尾遍历列表。 重复以下步骤 3-4
>
> 步骤 3：如果当前节点是偶数并且出现在奇数位置，则将该节点的地址压入栈偶数
>
> 步骤 4：如果当前节点是奇数并且出现在偶数位置 ，将该节点的地址压入栈奇数。
>
> [遍历结束]
>
> 步骤 5：两个栈的大小将相同。 当两个栈都不为空时，交换两个栈顶部的节点，并从各自的栈弹出两个节点。
>
> 步骤 6：现在重新排列了列表。 停止。

## C++

```cpp

// CPP program to rearrange nodes 
// as alternate odd even nodes in 
// a Singly Linked List 
#include <bits/stdc++.h> 
using namespace std; 

// Structure node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// A utility function to print 
// linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
    cout << endl; 
} 

// Function to create newNode 
// in a linkedlist 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Function to insert at beginning 
Node* insertBeg(Node* head, int val) 
{ 
    Node* temp = newNode(val); 
    temp->next = head; 
    head = temp; 
    return head; 
} 

// Function to rearrange the 
// odd and even nodes 
void rearrangeOddEven(Node* head) 
{ 
    stack<Node*> odd; 
    stack<Node*> even; 
    int i = 1; 

    while (head != nullptr) { 

        if (head->data % 2 != 0 && i % 2 == 0) { 

            // Odd Value in Even Position 
            // Add pointer to current node 
            // in odd stack 
            odd.push(head); 
        } 

        else if (head->data % 2 == 0 && i % 2 != 0) { 

            // Even Value in Odd Position 
            // Add pointer to current node 
            // in even stack 
            even.push(head); 
        } 

        head = head->next; 
        i++; 
    } 

    while (!odd.empty() && !even.empty()) { 

        // Swap Data at the top of two stacks 
        swap(odd.top()->data, even.top()->data); 
        odd.pop(); 
        even.pop(); 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = newNode(8); 
    head = insertBeg(head, 7); 
    head = insertBeg(head, 6); 
    head = insertBeg(head, 5); 
    head = insertBeg(head, 3); 
    head = insertBeg(head, 2); 
    head = insertBeg(head, 1); 

    cout << "Linked List:" << endl; 
    printList(head); 
    rearrangeOddEven(head); 

    cout << "Linked List after "
         << "Rearranging:" << endl; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to rearrange nodes  
// as alternate odd even nodes in  
// a Singly Linked List 
import java.util.*; 

class GFG 
{ 

// class node  
static class Node 
{  
    int data;  
    Node next;  
} 

// A utility function to print  
// linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data +" ");  
        node = node.next;  
    }  
    System.out.println(); 
}  

// Function to create newNode  
// in a linkedlist  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Function to insert at beginning  
static Node insertBeg(Node head, int val)  
{  
    Node temp = newNode(val);  
    temp.next = head;  
    head = temp;  
    return head;  
}  

// Function to rearrange the  
// odd and even nodes  
static void rearrangeOddEven(Node head)  
{  
    Stack<Node> odd=new Stack<Node>();  
    Stack<Node> even=new Stack<Node>();  
    int i = 1;  

    while (head != null) {  

        if (head.data % 2 != 0 && i % 2 == 0)  
        {  

            // Odd Value in Even Position  
            // Add pointer to current node  
            // in odd stack  
            odd.push(head);  
        }  

        else if (head.data % 2 == 0 && i % 2 != 0)  
        {  

            // Even Value in Odd Position  
            // Add pointer to current node  
            // in even stack  
            even.push(head);  
        }  

        head = head.next;  
        i++;  
    }  

    while (odd.size() > 0 && even.size() > 0) 
    {  

        // Swap Data at the top of two stacks  
        int k=odd.peek().data; 
        odd.peek().data=even.peek().data;  
        even.peek().data=k; 
        odd.pop();  
        even.pop();  
    }  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = newNode(8);  
    head = insertBeg(head, 7);  
    head = insertBeg(head, 6);  
    head = insertBeg(head, 5);  
    head = insertBeg(head, 3);  
    head = insertBeg(head, 2);  
    head = insertBeg(head, 1);  

    System.out.println( "Linked List:" );  
    printList(head);  
    rearrangeOddEven(head);  

    System.out.println( "Linked List after "+ 
                        "Rearranging:" );  
    printList(head);  
}  
} 

// This contributed by Arnab Kundu 

```

## Python

```py

# Python program to rearrange nodes 
# as alternate odd even nodes in 
# a Singly Linked List 

# Link list node  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.next = next

# A utility function to print 
# linked list 
def printList( node): 

    while (node != None) : 
        print(node.data , end=" ") 
        node = node.next

    print("\n") 

# Function to create newNode 
# in a linkedlist 
def newNode(key): 

    temp = Node(0) 
    temp.data = key 
    temp.next = None
    return temp 

# Function to insert at beginning 
def insertBeg(head, val): 

    temp = newNode(val) 
    temp.next = head 
    head = temp 
    return head 

# Function to rearrange the 
# odd and even nodes 
def rearrangeOddEven( head): 

    odd = [] 
    even = [] 
    i = 1

    while (head != None):  

        if (head.data % 2 != 0 and i % 2 == 0):  

            # Odd Value in Even Position 
            # Add pointer to current node 
            # in odd stack 
            odd.append(head) 

        elif (head.data % 2 == 0 and i % 2 != 0):  

            # Even Value in Odd Position 
            # Add pointer to current node 
            # in even stack 
            even.append(head) 

        head = head.next
        i = i + 1

    while (len(odd) != 0 and len(even) != 0) : 

        # Swap Data at the top of two stacks 
        odd[-1].data, even[-1].data = even[-1].data, odd[-1].data 
        odd.pop() 
        even.pop() 

    return head 

# Driver code 

head = newNode(8) 
head = insertBeg(head, 7) 
head = insertBeg(head, 6) 
head = insertBeg(head, 5) 
head = insertBeg(head, 3) 
head = insertBeg(head, 2) 
head = insertBeg(head, 1) 

print( "Linked List:" ) 
printList(head) 
rearrangeOddEven(head) 

print( "Linked List after ", "Rearranging:" ) 
printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to rearrange nodes  
// as alternate odd even nodes in  
// a Singly Linked List 
using System; 
using System.Collections.Generic;  

class GFG 
{ 

// class node  
public class Node 
{  
    public int data;  
    public Node next;  
} 

// A utility function to print  
// linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(node.data +" ");  
        node = node.next;  
    }  
    Console.WriteLine(); 
}  

// Function to create newNode  
// in a linkedlist  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Function to insert at beginning  
static Node insertBeg(Node head, int val)  
{  
    Node temp = newNode(val);  
    temp.next = head;  
    head = temp;  
    return head;  
}  

// Function to rearrange the  
// odd and even nodes  
static void rearrangeOddEven(Node head)  
{  
    Stack<Node> odd = new Stack<Node>();  
    Stack<Node> even = new Stack<Node>();  
    int i = 1;  

    while (head != null) 
    {  

        if (head.data % 2 != 0 && i % 2 == 0)  
        {  

            // Odd Value in Even Position  
            // Add pointer to current node  
            // in odd stack  
            odd.Push(head);  
        }  

        else if (head.data % 2 == 0 && i % 2 != 0)  
        {  

            // Even Value in Odd Position  
            // Add pointer to current node  
            // in even stack  
            even.Push(head);  
        }  

        head = head.next;  
        i++;  
    }  

    while (odd.Count > 0 && even.Count > 0) 
    {  

        // Swap Data at the top of two stacks  
        int k=odd.Peek().data; 
        odd.Peek().data=even.Peek().data;  
        even.Peek().data=k; 
        odd.Pop();  
        even.Pop();  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = newNode(8);  
    head = insertBeg(head, 7);  
    head = insertBeg(head, 6);  
    head = insertBeg(head, 5);  
    head = insertBeg(head, 3);  
    head = insertBeg(head, 2);  
    head = insertBeg(head, 1);  

    Console.WriteLine( "Linked List:" );  
    printList(head);  
    rearrangeOddEven(head);  

    Console.WriteLine( "Linked List after "+ 
                        "Rearranging:" );  
    printList(head);  
}  
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Linked List:
1 2 3 5 6 7 8 
Linked List after Rearranging:
1 2 3 6 5 8 7

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`

**方法 2（有效）**

1.  隔离列表中的奇数和偶数值。 此后，所有奇数值将一起出现，随后是所有偶数值。

2.  将列表分为两个列表，奇数和偶数。

3.  将偶数列表合并为奇数列表

```
REARRANGE (HEAD)
Step 1: Traverse the list using NODE TEMP. 
           If TEMP is odd
               Add TEMP to the beginning of the List
           [END OF IF]
        [END OF TRAVERSAL]
Step 2: Set TEMP to 2nd element of LIST.
Step 3: Set PREV_TEMP to 1st element of List
Step 4: Traverse using node TEMP as long as an even
        node is not encountered.
            PREV_TEMP = TEMP, TEMP = TEMP->NEXT
        [END OF TRAVERSAL]
Step 5: Set EVEN to TEMP. Set PREV_TEMP->NEXT to NULL
Step 6: I = HEAD, J = EVEN
Step 7: Repeat while I != NULL and J != NULL
            Store next nodes of I and J in K and L
            K = I->NEXT, L = J->NEXT
            I->NEXT = J, J->NEXT = K, PTR = J
            I = K and J = L 
       [END OF LOOP]
Step 8: if I == NULL 
            PTR->NEXT = J
        [END of IF]
Step 8: Return HEAD.
Step 9: End

```

## C++

```cpp

// Cpp program to rearrange nodes 
// as alternate odd even nodes in 
// a Singly Linked List 
#include <bits/stdc++.h> 
using namespace std; 

// Structure node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// A utility function to print 
// linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
    cout << endl; 
} 

// Function to create newNode 
// in a linkedlist 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Function to insert at beginning 
Node* insertBeg(Node* head, int val) 
{ 
    Node* temp = newNode(val); 
    temp->next = head; 
    head = temp; 
    return head; 
} 

// Function to rearrange the 
// odd and even nodes 
void rearrange(Node** head) 
{ 
    // Step 1: Segregate even and odd nodes 
    // Step 2: Split odd and even lists 
    // Step 3: Merge even list into odd list 
    Node* even; 
    Node *temp, *prev_temp; 
    Node *i, *j, *k, *l, *ptr; 

    // Step 1: Segregate Odd and Even Nodes 
    temp = (*head)->next; 
    prev_temp = *head; 

    while (temp != nullptr) { 

        // Backup next pointer of temp 
        Node* x = temp->next; 

        // If temp is odd move the node 
        // to beginning of list 
        if (temp->data % 2 != 0) { 
            prev_temp->next = x; 
            temp->next = (*head); 
            (*head) = temp; 
        } 
        else { 
            prev_temp = temp; 
        } 

        // Advance Temp Pointer 
        temp = x; 
    } 

    // Step 2 
    // Split the List into Odd and even 
    temp = (*head)->next; 
    prev_temp = (*head); 

    while (temp != nullptr && temp->data % 2 != 0) { 
        prev_temp = temp; 
        temp = temp->next; 
    } 

    even = temp; 

    // End the odd List (Make last node null) 
    prev_temp->next = nullptr; 

    // Step 3: 
    // Merge Even List into odd 
    i = *head; 
    j = even; 

    while (j != nullptr && i != nullptr) { 

        // While both lists are not 
        // exhausted Backup next 
        // pointers of i and j 
        k = i->next; 
        l = j->next; 

        i->next = j; 
        j->next = k; 

        // ptr points to the latest node added 
        ptr = j; 

        // Advance i and j pointers 
        i = k; 
        j = l; 
    } 

    if (i == nullptr) { 

        // Odd list exhausts before even, 
        // append remainder of even list to odd. 
        ptr->next = j; 
    } 

    // The case where even list exhausts before 
    // odd list is automatically handled since we 
    // merge the even list into the odd list 
} 

// Driver Code 
int main() 
{ 
    Node* head = newNode(8); 
    head = insertBeg(head, 7); 
    head = insertBeg(head, 6); 
    head = insertBeg(head, 3); 
    head = insertBeg(head, 5); 
    head = insertBeg(head, 1); 
    head = insertBeg(head, 2); 
    head = insertBeg(head, 10); 

    cout << "Linked List:" << endl; 
    printList(head); 
    cout << "Rearranged List" << endl; 
    rearrange(&head); 
    printList(head); 
} 

```

## Java

```java

// Java program to rearrange nodes  
// as alternate odd even nodes in  
// a Singly Linked List  
class GFG 
{ 

// Structure node  
static class Node  
{  
    int data;  
    Node next;  
};  

// A utility function to print  
// linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data + " ");  
        node = node.next;  
    }  
    System.out.println(); 
}  

// Function to create newNode  
// in a linkedlist  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Function to insert at beginning  
static Node insertBeg(Node head, int val)  
{  
    Node temp = newNode(val);  
    temp.next = head;  
    head = temp;  
    return head;  
}  

// Function to rearrange the  
// odd and even nodes  
static Node rearrange(Node head)  
{  
    // Step 1: Segregate even and odd nodes  
    // Step 2: Split odd and even lists  
    // Step 3: Merge even list into odd list  
    Node even;  
    Node temp, prev_temp;  
    Node i, j, k, l, ptr=null;  

    // Step 1: Segregate Odd and Even Nodes  
    temp = (head).next;  
    prev_temp = head;  

    while (temp != null)  
    {  

        // Backup next pointer of temp  
        Node x = temp.next;  

        // If temp is odd move the node  
        // to beginning of list  
        if (temp.data % 2 != 0)  
        {  
            prev_temp.next = x;  
            temp.next = (head);  
            (head) = temp;  
        }  
        else 
        {  
            prev_temp = temp;  
        }  

        // Advance Temp Pointer  
        temp = x;  
    }  

    // Step 2  
    // Split the List into Odd and even  
    temp = (head).next;  
    prev_temp = (head);  

    while (temp != null && temp.data % 2 != 0)  
    {  
        prev_temp = temp;  
        temp = temp.next;  
    }  

    even = temp;  

    // End the odd List (Make last node null)  
    prev_temp.next = null;  

    // Step 3:  
    // Merge Even List into odd  
    i = head;  
    j = even;  

    while (j != null && i != null) 
    {  

        // While both lists are not  
        // exhausted Backup next  
        // pointers of i and j  
        k = i.next;  
        l = j.next;  

        i.next = j;  
        j.next = k;  

        // ptr points to the latest node added  
        ptr = j;  

        // Advance i and j pointers  
        i = k;  
        j = l;  
    }  

    if (i == null) 
    {  

        // Odd list exhausts before even,  
        // append remainder of even list to odd.  
        ptr.next = j;  
    }  

    // The case where even list exhausts before  
    // odd list is automatically handled since we  
    // merge the even list into the odd list  
    return head; 
}  

// Driver Code  
public static void main(String args[]) 
{  
    Node head = newNode(8);  
    head = insertBeg(head, 7);  
    head = insertBeg(head, 6);  
    head = insertBeg(head, 3);  
    head = insertBeg(head, 5);  
    head = insertBeg(head, 1);  
    head = insertBeg(head, 2);  
    head = insertBeg(head, 10);  

    System.out.println("Linked List:" );  
    printList(head);  
    System.out.println("Rearranged List" );  
    head=rearrange(head);  
    printList(head);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to rearrange nodes  
# as alternate odd even nodes in  
# a Singly Linked List  

# Structure node  
class Node : 

    def __init__(self): 
        self.data = 0
        self.next = None

# A utility function to print  
# linked list  
def printList(node) : 
    while (node != None) : 
        print(node.data, end = " ")  
        node = node.next

    print(" ") 

# Function to create newNode  
# in a linkedlist  
def newNode( key) : 
    temp = Node()  
    temp.data = key  
    temp.next = None
    return temp  

# Function to insert at beginning  
def insertBeg( head, val) : 
    temp = newNode(val)  
    temp.next = head  
    head = temp  
    return head  

# Function to rearrange the  
# odd and even nodes  
def rearrange(head) : 

    # Step 1: Segregate even and odd nodes  
    # Step 2: Split odd and even lists  
    # Step 3: Merge even list into odd list  
    even = None
    temp = None
    prev_temp = None
    i = None
    j = None
    k = None
    l = None
    ptr = None

    # Step 1: Segregate Odd and Even Nodes  
    temp = (head).next
    prev_temp = head  

    while (temp != None) : 

        # Backup next pointer of temp  
        x = temp.next

        # If temp is odd move the node  
        # to beginning of list  
        if (temp.data % 2 != 0) : 

            prev_temp.next = x  
            temp.next = (head)  
            (head) = temp  

        else: 

            prev_temp = temp  

        # Advance Temp Pointer  
        temp = x  

    # Step 2  
    # Split the List into Odd and even  
    temp = (head).next
    prev_temp = (head)  

    while (temp != None and temp.data % 2 != 0) : 
        prev_temp = temp  
        temp = temp.next

    even = temp  

    # End the odd List (Make last node None)  
    prev_temp.next = None

    # Step 3:  
    # Merge Even List into odd  
    i = head  
    j = even  

    while (j != None and i != None): 

        # While both lists are not  
        # exhausted Backup next  
        # pointers of i and j  
        k = i.next
        l = j.next

        i.next = j  
        j.next = k  

        # ptr points to the latest node added  
        ptr = j  

        # Advance i and j pointers  
        i = k  
        j = l  

    if (i == None): 

        # Odd list exhausts before even,  
        # append remainder of even list to odd.  
        ptr.next = j  

    # The case where even list exhausts before  
    # odd list is automatically handled since we  
    # merge the even list into the odd list  
    return head 

# Driver Code  
head = newNode(8)  
head = insertBeg(head, 7)  
head = insertBeg(head, 6)  
head = insertBeg(head, 3)  
head = insertBeg(head, 5)  
head = insertBeg(head, 1)  
head = insertBeg(head, 2)  
head = insertBeg(head, 10)  

print("Linked List:" )  
printList(head)  
print("Rearranged List" )  
head = rearrange(head)  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to rearrange nodes  
// as alternate odd even nodes in  
// a Singly Linked List  
using System; 

class GFG  
{  

// Structure node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// A utility function to print  
// linked list  
static void printList(Node node)  
{  
    while (node != null)  
    {  
        Console.Write(node.data + " ");  
        node = node.next;  
    }  
    Console.WriteLine();  
}  

// Function to create newNode  
// in a linkedlist  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Function to insert at beginning  
static Node insertBeg(Node head, int val)  
{  
    Node temp = newNode(val);  
    temp.next = head;  
    head = temp;  
    return head;  
}  

// Function to rearrange the  
// odd and even nodes  
static Node rearrange(Node head)  
{  
    // Step 1: Segregate even and odd nodes  
    // Step 2: Split odd and even lists  
    // Step 3: Merge even list into odd list  
    Node even;  
    Node temp, prev_temp;  
    Node i, j, k, l, ptr=null;  

    // Step 1: Segregate Odd and Even Nodes  
    temp = (head).next;  
    prev_temp = head;  

    while (temp != null)  
    {  

        // Backup next pointer of temp  
        Node x = temp.next;  

        // If temp is odd move the node  
        // to beginning of list  
        if (temp.data % 2 != 0)  
        {  
            prev_temp.next = x;  
            temp.next = (head);  
            (head) = temp;  
        }  
        else
        {  
            prev_temp = temp;  
        }  

        // Advance Temp Pointer  
        temp = x;  
    }  

    // Step 2  
    // Split the List into Odd and even  
    temp = (head).next;  
    prev_temp = (head);  

    while (temp != null && temp.data % 2 != 0)  
    {  
        prev_temp = temp;  
        temp = temp.next;  
    }  

    even = temp;  

    // End the odd List (Make last node null)  
    prev_temp.next = null;  

    // Step 3:  
    // Merge Even List into odd  
    i = head;  
    j = even;  

    while (j != null && i != null)  
    {  

        // While both lists are not  
        // exhausted Backup next  
        // pointers of i and j  
        k = i.next;  
        l = j.next;  

        i.next = j;  
        j.next = k;  

        // ptr points to the latest node added  
        ptr = j;  

        // Advance i and j pointers  
        i = k;  
        j = l;  
    }  

    if (i == null)  
    {  

        // Odd list exhausts before even,  
        // append remainder of even list to odd.  
        ptr.next = j;  
    }  

    // The case where even list exhausts before  
    // odd list is automatically handled since we  
    // merge the even list into the odd list  
    return head;  
}  

// Driver Code  
public static void Main(String []args)  
{  
    Node head = newNode(8);  
    head = insertBeg(head, 7);  
    head = insertBeg(head, 6);  
    head = insertBeg(head, 3);  
    head = insertBeg(head, 5);  
    head = insertBeg(head, 1);  
    head = insertBeg(head, 2);  
    head = insertBeg(head, 10);  

    Console.WriteLine("Linked List:" );  
    printList(head);  
    Console.WriteLine("Rearranged List" );  
    head=rearrange(head);  
    printList(head);  
}  
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Linked List:
10 2 1 5 3 6 7 8 
Rearranged List
7 10 3 2 5 6 1 8

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。