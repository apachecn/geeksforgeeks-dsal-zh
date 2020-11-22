# 反转双链表 | 系列 4（交换数据）

> 原文：[https://www.geeksforgeeks.org/reverse-doubly-linked-list-set-4-swapping-data/](https://www.geeksforgeeks.org/reverse-doubly-linked-list-set-4-swapping-data/)

给定一个双向链表，我们被要求在不使用任何额外空间的情况下原地反转该列表。

**示例**：

```
Input : 1 <--> 2 <--> 5 <--> 6 <--> 7
Output : 7 <--> 6 <--> 5 <--> 2 <--> 1

Input : 11 <--> 22 <--> 33 <--> 22 <--> 1
Output : 1 <--> 22 <--> 33 <--> 22 <--> 11

```

我们已经讨论了三种方法来反向双向链表：[反向双向链表](https://www.geeksforgeeks.org/reverse-a-doubly-linked-list/)，[反向双向链表（组 2）](https://www.geeksforgeeks.org/reverse-doubly-linked-list-set-2//)和[反向双向链表使用 递归](https://www.geeksforgeeks.org/reverse-doubly-linked-list-using-recursion/)。

前两种方法的工作时间为`O(n)`，并且不需要额外的空间。 第一种方法通过交换每个节点的下一个和上一个指针来工作。 第二种方法从列表中取出每个节点，并将其添加到列表的开头。

还有另一种方法更直观，但也更昂贵。

此方法类似于反转数组。 要反转数组，我们将两个指针放在一个位置：一个放在列表的开头，另一个放在列表的结尾。 然后，我们交换两个指针的数据，并使两个指针彼此相对。 当两个指针相遇或彼此交叉时，我们将停止。 我们恰好执行 n / 2 个交换，并且时间复杂度也是`O(n)`。

双链表同时具有上一个指针和下一个指针，这意味着我们可以在列表中向前和向后移动。 因此，如果我们在列表的开头放置一个指针（例如，左指针），在列表的末尾放置另一个右指针，则可以通过使左指针前进和后退右指针来使这些指针彼此相对。

**算法**

```
Step 1: Set LEFT to head of list
Step 2: Traverse the list and set RIGHT to end of the list 
Step 3: Repeat following steps while LEFT != RIGHT and 
        LEFT->PREV != RIGHT
Step 4: Swap LEFT->DATA and RIGHT->DATA
Step 5: Advance LEFT pointer by one, LEFT = LEFT->NEXT
Step 6: Recede RIGHT pointer by one, i.e RIGHT = RIGHT->PREV
        [END OF LOOP]
Step 7: End

```

**关于三种方法**的比较效率的注释

必须提到几件事。 此方法易于实现，但与指针交换方法相比，它的成本也更高。 这是因为我们交换数据而不是指针。 如果节点是具有多个数据成员的大型复杂数据类型，则交换数据的成本可能更高。 相反，指向节点的指针将始终是更简单的数据类型，并且为 4 或 8 个字节。

下面是该算法的实现。

## C++

```cpp

// Cpp Program to Reverse a List using Data Swapping 

#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    struct Node *prev, *next; 
}; 

Node* newNode(int val) 
{ 
    Node* temp = new Node; 
    temp->data = val; 
    temp->prev = temp->next = nullptr; 
    return temp; 
} 

void printList(Node* head) 
{ 
    while (head->next != nullptr) { 
        cout << head->data << " <--> "; 
        head = head->next; 
    } 
    cout << head->data << endl; 
} 

// Insert a new node at the head of the list 
void insert(Node** head, int val) 
{ 
    Node* temp = newNode(val); 
    temp->next = *head; 
    (*head)->prev = temp; 
    (*head) = temp; 
} 

// Function to reverse the list 
void reverseList(Node** head) 
{ 
    Node* left = *head, * right = *head; 

    // Traverse the list and set right pointer to 
    // end of list 
    while (right->next != nullptr) 
        right = right->next; 

    // Swap data of left and right pointer and move 
    // them towards each other until they meet or  
    // cross each other 
    while (left != right && left->prev != right) { 

        // Swap data of left and right pointer 
        swap(left->data, right->data); 

        // Advance left pointer 
        left = left->next; 

        // Advance right pointer 
        right = right->prev; 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = newNode(5); 
    insert(&head, 4); 
    insert(&head, 3); 
    insert(&head, 2); 
    insert(&head, 1); 

    printList(head); 
    cout << "List After Reversing" << endl; 
    reverseList(&head); 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java Program to Reverse a List using Data Swapping  
class GFG 
{ 
static class Node 
{  
    int data;  
    Node prev, next;  
};  

static Node newNode(int val)  
{  
    Node temp = new Node();  
    temp.data = val;  
    temp.prev = temp.next = null;  
    return temp;  
}  

static void printList(Node head)  
{  
    while (head.next != null) 
    {  
        System.out.print(head.data+ " <-> ");  
        head = head.next;  
    }  
    System.out.println( head.data );  
}  

// Insert a new node at the head of the list  
static Node insert(Node head, int val)  
{  
    Node temp = newNode(val);  
    temp.next = head;  
    (head).prev = temp;  
    (head) = temp; 
    return head; 
}  

// Function to reverse the list  
static Node reverseList(Node head)  
{  
    Node left = head, right = head;  

    // Traverse the list and set right pointer to  
    // end of list  
    while (right.next != null)  
        right = right.next;  

    // Swap data of left and right pointer and move  
    // them towards each other until they meet or  
    // cross each other  
    while (left != right && left.prev != right) 
    {  

        // Swap data of left and right pointer  
        int t = left.data; 
        left.data = right.data; 
        right.data = t; 

        // Advance left pointer  
        left = left.next;  

        // Advance right pointer  
        right = right.prev;  
    }  
    return head; 
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = newNode(5);  
    head = insert(head, 4);  
    head = insert(head, 3);  
    head = insert(head, 2);  
    head = insert(head, 1);  

    printList(head);  
    System.out.println("List After Reversing");  
    head=reverseList(head);  
    printList(head);  

} 
} 

// This code is contributed by Arnab Kundu  

```

## Python3

```py

# Python3 Program to Reverse a List  
# using Data Swapping 
import math 

class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

def newNode(val): 
    temp = Node(val) 
    temp.data = val 
    temp.prev =None
    temp.next = None
    return temp 

def printList( head): 
    while (head.next != None): 
        print(head.data, end = "<-->") 
        head = head.next

    print(head.data) 

# Insert a new node at the head of the list 
def insert(head, val): 
    temp = newNode(val) 
    temp.next = head 
    (head).prev = temp 
    (head) = temp 
    return head 

# Function to reverse the list 
def reverseList( head): 
    left = head 
    right = head 

    # Traverse the list and set right  
    # pointer to end of list 
    while (right.next != None): 
        right = right.next

    # Swap data of left and right pointer  
    # and move them towards each other  
    # until they meet or cross each other 
    while (left != right and left.prev != right): 

        # Swap data of left and right pointer 
        t = left.data 
        left.data = right.data 
        right.data = t 

        # Advance left pointer 
        left = left.next

        # Advance right pointer 
        right = right.prev 

    return head 

# Driver code 
if __name__=='__main__':  

    head = newNode(5) 
    head = insert(head, 4) 
    head = insert(head, 3) 
    head = insert(head, 2) 
    head = insert(head, 1) 

    printList(head) 
    print("List After Reversing") 
    head = reverseList(head) 
    printList(head) 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# Program to Reverse a List using Data Swapping  
using System; 

class GFG 
{ 

    public class Node 
    {  
        public int data;  
        public Node prev, next;  
    };  

    static Node newNode(int val)  
    {  
        Node temp = new Node();  
        temp.data = val;  
        temp.prev = temp.next = null;  
        return temp;  
    }  

    static void printList(Node head)  
    {  
        while (head.next != null) 
        {  
            Console.Write(head.data+ " <-> ");  
            head = head.next;  
        }  
        Console.WriteLine( head.data );  
    }  

    // Insert a new node at the head of the list  
    static Node insert(Node head, int val)  
    {  
        Node temp = newNode(val);  
        temp.next = head;  
        (head).prev = temp;  
        (head) = temp; 
        return head; 
    }  

    // Function to reverse the list  
    static Node reverseList(Node head)  
    {  
        Node left = head, right = head;  

        // Traverse the list and set right pointer to  
        // end of list  
        while (right.next != null)  
            right = right.next;  

        // Swap data of left and right pointer and move  
        // them towards each other until they meet or  
        // cross each other  
        while (left != right && left.prev != right) 
        {  

            // Swap data of left and right pointer  
            int t = left.data; 
            left.data = right.data; 
            right.data = t; 

            // Advance left pointer  
            left = left.next;  

            // Advance right pointer  
            right = right.prev;  
        }  
        return head; 
    }  

    // Driver code  
    public static void Main(String []args) 
    {  
        Node head = newNode(5);  
        head = insert(head, 4);  
        head = insert(head, 3);  
        head = insert(head, 2);  
        head = insert(head, 1);  

        printList(head);  
        Console.WriteLine("List After Reversing");  
        head=reverseList(head);  
        printList(head);  

    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
1 <--> 2 <--> 3 <--> 4 <--> 5
List After Reversing
5 <--> 4 <--> 3 <--> 2 <--> 1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。