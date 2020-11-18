# 检查链接列表中的元素是否成对存在

> 原文：[https://www.geeksforgeeks.org/check-if-elements-of-linked-list-are-present-in-pair/](https://www.geeksforgeeks.org/check-if-elements-of-linked-list-are-present-in-pair/)

给定一个整数的单链表。 任务是检查链接列表中的每个元素是否成对出现，即所有元素是否出现。 的时间。

**示例**：

```
Input: 1 -> 2 -> 3 -> 3 -> 1 -> 2
Output: Yes

Input: 10 -> 20 -> 30 -> 20
Output: No

```

**方法**：

*   初始化指向*头*的*临时*节点。

*   取一个变量来计算所有元素的 *XOR* 。

*   开始遍历链表，并继续使用 node-> data 计算 XOR。

*   如果 XOR 为 0，则返回 true，否则返回 false。

下面是上述方法的实现：

## C++

```cpp

// C++ program to check if elements of 
// linked lists are present in pair 
#include <bits/stdc++.h> 

using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to check if elements of 
// linked list are present in pair 
bool isPair(struct Node* head) 
{ 

    int xxor = 0; 

    struct Node* temp = head; 

    while (temp != NULL) { 
        xxor ^= temp->data; 
        temp = temp->next; 
    } 

    return xxor; 
} 

// Function to add a node at the 
// beginning of Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* first = NULL; 

    /* First constructed linked list is:  
    10 -> 34 -> 1 -> 10 -> 34 -> 1 */
    push(&first, 1); 
    push(&first, 34); 
    push(&first, 10); 
    push(&first, 1); 
    push(&first, 34); 
    push(&first, 10); 

    // Calling function to check pair elements 
    if (!isPair(first)) { 
        cout << "Yes" << endl; 
    } 
    else { 
        cout << "No" << endl; 
    } 

    return 0; 
} 

```

## Java

```java

// Java program to check if elements of  
// linked lists are present in pair  

// Node Class  
class Node 
{ 
    int data; 
    Node next; 

    // Constructor to create a new node 
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

class SLL  
{ 

    // function to insert a node at the beginning 
    // of the Singly Linked List 
    static Node push(Node head, int data)  
    { 
        Node newNode = new Node(data); 
        newNode.next = head; 
        head = newNode; 
        return head; 
    } 

    // Function to check if elements of 
    // linked list are present in pair 
    static boolean isPair(Node head) 
    { 
        int xxor = 0; 
        Node temp = head; 
        while (temp != null) 
        { 
            xxor ^= temp.data; 
            temp = temp.next; 
        } 
        return xxor != 0; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        Node head = null; 

        // First constructed linked list 
        // 10 -> 34 -> 1 -> 10 -> 34 -> 1 

        head = push(head, 1); 
        head = push(head, 34); 
        head = push(head, 10); 
        head = push(head, 1); 
        head = push(head, 34); 
        head = push(head, 10); 

        // Calling function to check pair elements 
        if (!isPair(head)) 
        { 
            System.out.println("Yes"); 
        }  
        else
        { 
            System.out.println("No"); 
        } 
    } 
} 

// This code is contributed by Vivekkumar Singh 

```

## Python3

```py

# Python3 program to check if elements of 
# linked lists are present in pair 

# A linked list node 
class Node: 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to check if elements of 
# linked list are present in pair 
def isPair( head): 
    xxor = 0
    temp = head 

    while (temp != None) : 
        xxor = xxor ^ temp.data 
        temp = temp.next

    return xxor 

# Function to add a node at the 
# beginning of Linked List 
def push( head_ref, new_data): 

    # allocate node  
    new_node = Node() 

    # put in the data  
    new_node.data = new_data 

    # link the old list off the new node  
    new_node.next = (head_ref) 

    # move the head to point to the new node  
    (head_ref) = new_node 

    return head_ref 

# Driver code 

first = None

# First constructed linked list is:  
# 10 . 34 . 1 . 10 . 34 . 1  
first = push(first, 1) 
first = push(first, 34) 
first = push(first, 10) 
first = push(first, 1) 
first = push(first, 34) 
first = push(first, 10) 

# Calling function to check pair elements 
if (not isPair(first)):  
    print( "Yes" ) 

else : 
    print( "No" ) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to check if elements of  
// linked lists are present in pair  
using System; 

// Node Class  
public class Node 
{ 
    public int data; 
    public Node next; 

    // Constructor to create a new node 
    public Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

public class SLL  
{ 

    // function to insert a node at the beginning 
    // of the Singly Linked List 
    static Node push(Node head, int data)  
    { 
        Node newNode = new Node(data); 
        newNode.next = head; 
        head = newNode; 
        return head; 
    } 

    // Function to check if elements of 
    // linked list are present in pair 
    static Boolean isPair(Node head) 
    { 
        int xxor = 0; 
        Node temp = head; 
        while (temp != null) 
        { 
            xxor ^= temp.data; 
            temp = temp.next; 
        } 
        return xxor != 0; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        Node head = null; 

        // First constructed linked list 
        // 10 -> 34 -> 1 -> 10 -> 34 -> 1 

        head = push(head, 1); 
        head = push(head, 34); 
        head = push(head, 10); 
        head = push(head, 1); 
        head = push(head, 34); 
        head = push(head, 10); 

        // Calling function to check pair elements 
        if (!isPair(head)) 
        { 
            Console.WriteLine("Yes"); 
        }  
        else
        { 
            Console.WriteLine("No"); 
        } 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Yes

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。