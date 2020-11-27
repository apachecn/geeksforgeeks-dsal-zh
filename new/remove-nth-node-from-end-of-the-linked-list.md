# 删除距离链表的末尾的第`N`个节点

> 原文：[https://www.geeksforgeeks.org/remove-nth-node-from-end-of-the-linked-list/](https://www.geeksforgeeks.org/remove-nth-node-from-end-of-the-linked-list/)

给定一个链表。 任务是从链表的末尾删除第`N`个节点。

**示例**：

> **输入**：`1 -> 2 -> 3 -> 4 -> 5, N = 2`
>
> **输出**：`1 -> 2  -> 3 -> 5`
> 
> **输入**：`7 -> 8 -> 4 -> 3 -> 2, N = 1`
>
> **输出**：`7 -> 8  -> 4 -> 3`

**先决条件**：

1.  [从链表中删除一个节点。](https://www.geeksforgeeks.org/delete-a-linked-list-node-at-a-given-position/)

2.  [从链表的末尾找到第`n`个节点](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)

**方法**：

从最后删除`B`节点与从开始删除`length - B + 1`基本相同。 在我们的方法中，我们首先评估链表的长度，然后检查

*   如果`length = B`，则返回`head->next`

*   如果`length > B`，则意味着我们必须删除中间节点，我们将删除此节点，并使它的上一个节点指向已删除节点的下一个节点。

## C++

```cpp

// CPP program to delete nth node from last 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert node in a linked list 
struct Node* create(struct Node* head, int x) 
{ 
    struct Node *temp, *ptr = head; 
    temp = new Node(); 
    temp->data = x; 
    temp->next = NULL; 
    if (head == NULL) 
        head = temp; 
    else { 
        while (ptr->next != NULL) { 
            ptr = ptr->next; 
        } 
        ptr->next = temp; 
    } 
    return head; 
} 

// Function to remove nth node from last 
Node* removeNthFromEnd(Node* head, int B) 
{ 
    // To store length of the linked list 
    int len = 0; 
    Node* tmp = head; 
    while (tmp != NULL) { 
        len++; 
        tmp = tmp->next;  
    } 

    // B > length, then we can't remove node 
    if (B > len)  
    { 
        cout << "Length of the linked list is " << len; 
        cout  << " we can't remove "<< B << "th node from the"; 
        cout << " linked list\n"; 
        return head;  
    } 

    // We need to remove head node 
    else if (B == len) { 

        // Return head->next 
        return head->next;  

    } 
    else 
    { 
        // Remove len - B th node from starting 
        int diff = len - B;           
        Node* prev= NULL;        
        Node* curr = head;          
        for(int i = 0;i < diff;i++){ 
            prev = curr;             
            curr = curr->next;       
        } 
        prev->next = curr->next; 
        return head; 
    } 

} 

// This function prints contents of linked  
// list starting from the given node  
void dispaly(struct Node* head) 
{ 

    struct Node* temp = head; 
    while (temp != NULL) { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
    cout << endl; 
} 

// Driver code 
int main() 
{ 
    struct Node* head = NULL; 

    head = create(head, 1); 
    head = create(head, 2); 
    head = create(head, 3); 
    head = create(head, 4); 
    head = create(head, 5); 

    int n = 2; 

    cout << "Linked list before modification: \n"; 
    dispaly(head); 

    head = removeNthFromEnd(head, 2); 
    cout << "Linked list after modification: \n"; 
    dispaly(head); 

    return 0; 
} 

```

## Java

```java

// Java program to delete nth node from last 
class GFG  
{  

// Structure of node 
static class Node 
{ 
    int data; 
    Node next; 
}; 

// Function to insert node in a linked list 
static Node create(Node head, int x) 
{ 
    Node temp, ptr = head; 
    temp = new Node(); 
    temp.data = x; 
    temp.next = null; 
    if (head == null) 
        head = temp; 
    else 
    { 
        while (ptr.next != null)  
        { 
            ptr = ptr.next; 
        } 
        ptr.next = temp; 
    } 
    return head; 
} 

// Function to remove nth node from last 
static Node removeNthFromEnd(Node head, int B) 
{ 
    // To store length of the linked list 
    int len = 0; 
    Node tmp = head; 
    while (tmp != null)  
    { 
        len++; 
        tmp = tmp.next;  
    } 

    // B > length, then we can't remove node 
    if (B > len)  
    { 
        System.out.print("Length of the linked list is " + len); 
        System.out.print(" we can't remove "+ B +  
                         "th node from the"); 
        System.out.print(" linked list\n"); 
        return head;  
    } 

    // We need to remove head node 
    else if (B == len)  
    { 

        // Return head.next 
        return head.next;  

    } 
    else
    { 
        // Remove len - B th node from starting 
        int diff = len - B;          
        Node prev= null;      
        Node curr = head;          
        for(int i = 0; i < diff; i++) 
        { 
            prev = curr;          
            curr = curr.next;      
        } 
        prev.next = curr.next; 
        return head; 
    } 

} 

// This function prints contents of linked  
// list starting from the given node  
static void dispaly(Node head) 
{ 
    Node temp = head; 
    while (temp != null)  
    { 
        System.out.print(temp.data + " "); 
        temp = temp.next; 
    } 
    System.out.println(); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node head = null; 

    head = create(head, 1); 
    head = create(head, 2); 
    head = create(head, 3); 
    head = create(head, 4); 
    head = create(head, 5); 

    int n = 2; 

    System.out.print("Linked list before modification: \n"); 
    dispaly(head); 

    head = removeNthFromEnd(head, 2); 
    System.out.print("Linked list after modification: \n"); 
    dispaly(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to delete nth node from last 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None # Initialize next as null 

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Function to add node at the end 
    def create(self, x): 

        new_node = Node(x) 

        if self.head is None: 
            self.head = new_node 
            return

        last = self.head 
        while last.next: 
            last = last.next

        last.next = new_node 

    # This function prints contents of linked  
    # list starting from the given node  
    def display(self): 
        temp = self.head 

        while temp: 
            print(temp.data, end = " ") 
            temp = temp.next

# Function to remove nth node from last 
def removeNthFromEnd(head, k): 

    # the function uses two pointer method 
    first = head 
    second = head 
    count = 1
    while count <= k: 
        second = second.next
        count += 1
    if second is None: 
        head.value = head.next.value 
        head.next = head.next.next
        return
    while second.next is not None: 
        first = first.next
        second = second.next
    first.next = first.next.next

# Driver code 

# val list contains list of values 
val = [1, 2, 3, 4, 5] 
k = 2
ll = LinkedList() 
for i in val: 
    ll.create(i) 

print("Linked list before modification:"); 
ll.display() 

removeNthFromEnd(ll.head, k) 

print("\nLinked list after modification:"); 
ll.display() 

# This code is contributed by Dhinesh 

```

## C#

```cs

// C# program to delete nth node from last 
using System; 

class GFG  
{  

// Structure of node 
class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert node in a linked list 
static Node create(Node head, int x) 
{ 
    Node temp, ptr = head; 
    temp = new Node(); 
    temp.data = x; 
    temp.next = null; 
    if (head == null) 
        head = temp; 
    else
    { 
        while (ptr.next != null)  
        { 
            ptr = ptr.next; 
        } 
        ptr.next = temp; 
    } 
    return head; 
} 

// Function to remove nth node from last 
static Node removeNthFromEnd(Node head, int B) 
{ 
    // To store length of the linked list 
    int len = 0; 
    Node tmp = head; 
    while (tmp != null)  
    { 
        len++; 
        tmp = tmp.next;  
    } 

    // B > length, then we can't remove node 
    if (B > len)  
    { 
        Console.Write("Length of the linked list is " + len); 
        Console.Write(" we can't remove " + B +  
                           "th node from the"); 
        Console.Write(" linked list\n"); 
        return head;  
    } 

    // We need to remove head node 
    else if (B == len)  
    { 

        // Return head.next 
        return head.next;  

    } 
    else
    { 
        // Remove len - B th node from starting 
        int diff = len - B;          
        Node prev= null;      
        Node curr = head;          
        for(int i = 0; i < diff; i++) 
        { 
            prev = curr;          
            curr = curr.next;      
        } 
        prev.next = curr.next; 
        return head; 
    } 

} 

// This function prints contents of linked  
// list starting from the given node  
static void dispaly(Node head) 
{ 
    Node temp = head; 
    while (temp != null)  
    { 
        Console.Write(temp.data + " "); 
        temp = temp.next; 
    } 
    Console.Write("\n"); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node head = null; 

    head = create(head, 1); 
    head = create(head, 2); 
    head = create(head, 3); 
    head = create(head, 4); 
    head = create(head, 5); 

    Console.Write("Linked list before modification: \n"); 
    dispaly(head); 

    head = removeNthFromEnd(head, 2); 
    Console.Write("Linked list after modification: \n"); 
    dispaly(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Linked list before modification: 
1 2 3 4 5 
Linked list after modification: 
1 2 3 5 

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。**