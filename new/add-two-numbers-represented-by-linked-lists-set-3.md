# 添加两个由链接列表表示的数字| 套装 3

给定两个链接列表表示的两个数字，编写一个返回和列表的函数。 总计列表是两个输入数字相加的链接列表表示。 预期空间复杂度 O（1）。

**示例：**

> **输入：**
> L1 = 5-> 6-> 3->空
> L2 = 8-> 4-> 2->空
> **输出：** 1-> 4-> 0-> 5-> NULL
> 
> **输入：**
> L1 = 1-> 0-> 0->空
> L2 = 9-> 1->空
> **输出：** 1-> 9-> 1-> NULL

**方法：**我们在此处讨论了一种解决方案 [](https://www.geeksforgeeks.org/sum-of-two-linked-lists/) ，在该解决方案中，我们使用递归达到列表中的最小有效数字，但是由于堆栈的参与，解决方案的空间复杂性 变成 O（N）

这里的目标是就地求和，并返回修改后的和列表。

我们的想法是首先反转两个链表，因此链表的新标题指向最低有效数字，我们可以按[此处](https://www.geeksforgeeks.org/?p=15194/)的说明开始添加，而不是创建新列表，而是修改现有的列表 并返回修改后列表的头。

步骤如下：

1.  反向清单 L1。

2.  反向清单 L2。

3.  迭代添加两个列表的节点。

4.  反转结果列表并返回其头部。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

class LinkedList; 

// Node class for the linked list 
class Node { 
    int data; 
    Node* next; 

    friend LinkedList; 

public: 
    Node(); 
    Node(int x); 
}; 

Node::Node() 
{ 
    data = 0; 
    next = NULL; 
} 

// Function to initialise 
// a node with value x 
Node::Node(int x) 
{ 
    data = x; 
    next = NULL; 
} 

// Linkedlist class with helper functions 
class LinkedList { 
public: 
    Node* head; 

    LinkedList(); 

    void insert(int x); 
    void reverse(); 
    void traverse(); 

    void sum(LinkedList*); 
}; 

LinkedList::LinkedList() 
{ 
    head = NULL; 
} 

// Function to insert a node at 
// the head of the list 
void LinkedList::insert(int x) 
{ 
    Node* node = new Node(); 
    node->data = x; 

    if (head == NULL) 
        head = node; 
    else { 
        node->next = head; 
        head = node; 
    } 
} 

// Function to reverse the linked list 
void LinkedList::reverse() 
{ 
    Node *prev = NULL, *curr = head; 

    while (curr) { 
        Node* temp = curr->next; 
        curr->next = prev; 
        prev = curr; 
        curr = temp; 
    } 
    head = prev; 
} 

// Function to traverse and print the list 
void LinkedList::traverse() 
{ 

    Node* temp = head; 

    while (temp) { 
        cout << temp->data << " -> "; 
        temp = temp->next; 
    } 
    cout << "NULL"; 
} 

// Function to add two numbers 
// represented as linked lists 
void LinkedList::sum(LinkedList* l2) 
{ 
    reverse(); 
    l2->reverse(); 

    Node *start1 = head, *start2 = l2->head; 

    Node* prev = NULL; 
    int carry = 0; 

    // While both lists exist 
    while (start1 && start2) { 

        // Current sum 
        int temp = start1->data + start2->data + carry; 

        // Handle carry 
        start1->data = temp % 10; 
        carry = temp / 10; 
        prev = start1; 

        // Get to next nodes 
        start1 = start1->next; 
        start2 = start2->next; 
    } 

    // If there are reamining digits 
    // in any one of the lists 
    if (start1 || start2) { 

        if (start2) 
            prev->next = start2; 

        start1 = prev->next; 

        // While first list has digits remaining 
        while (start1) { 
            int temp = start1->data + carry; 
            start1->data = temp % 10; 
            carry = temp / 10; 
            prev = start1; 
            start1 = start1->next; 
        } 
    } 

    // If a new node needs to be 
    // created due to carry 
    if (carry > 0) { 
        prev->next = new Node(carry); 
    } 

    // Reverse the resultant list 
    reverse(); 
} 

// Driver code 
int main() 
{ 

    // Create first list 
    LinkedList* l1 = new LinkedList(); 
    l1->insert(3); 
    l1->insert(6); 
    l1->insert(5); 

    // Create second list 
    LinkedList* l2 = new LinkedList(); 
    l2->insert(2); 
    l2->insert(4); 
    l2->insert(8); 

    // Add the lists 
    l1->sum(l2); 

    // Print the resultant list 
    l1->traverse(); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class Node  
{ 
    int data; 
    Node next; 

    // constructor 
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
}// Node closes 

class LinkedList 
{ 
    Node head; 

    // Helper function to traverse 
    void traverse(Node head)  
    { 
        while(head != null) 
        { 
            System.out.print(head.data + "->"); 
            head = head.next; 
        } 
    } 

    // Helper function to insert data in linked list 
    void insert(int x) 
    { 
        Node temp = new Node(x); 
        if(head == null) head = temp; 
        else
        { 
            temp.next = head; 
            head = temp; 
        } 
    } 

    // Helper function to reverse the list 
    public static Node reverse(Node head) 
    { 
        if(head == null || head.next == null) return head; 

        Node prev = null; 
        Node curr = head; 
        while(curr != null) 
        { 
            Node temp = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = temp; 
        } 
        head = prev; 
        return head; 
    } 

    // Function to add two lists 
    public static Node sum(Node l1, Node l2) 
    { 
        if(l2 == null) return l1; 
        if(l1 == null) return l2; 

        // reverse l1 list 
        l1 = reverse(l1); 

        // reverse l2 list 
        l2 = reverse(l2); 

        // storing head whose reverse is to be returned 
        // This is where which will be final node 
        Node head = l1; 
        Node prev = null; 
        int c = 0,sum; 
        while(l1 != null && l2 != null) 
        { 
            sum = c + l1.data + l2.data; 
            l1.data = sum % 10; 
            c = sum / 10; 
            prev = l1; 
            l1 = l1.next; 
            l2 = l2.next; 
        } 

        if(l1 != null||l2 != null) 
        { 
            if(l2 != null) prev.next = l2; 
            l1 = prev.next; 
            while(l1 != null) 
            { 
                sum = c + l1.data; 
                l1.data = sum % 10; 
                c = sum / 10; 
                prev = l1; 
                l1 = l1.next; 
            } 
        } 
        if(c > 0) prev.next = new Node(c); 
        return reverse(head); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        LinkedList l1 = new LinkedList(); 
        l1.insert(3); 
        l1.insert(6); 
        l1.insert(5); 
        LinkedList l2 = new LinkedList(); 
        l2.insert(2); 
        l2.insert(4); 
        l2.insert(8); 
        LinkedList l3 = new LinkedList(); 
        Node head = sum(l1.head, l2.head); 
        l3.traverse(head); 
        System.out.print("Null"); 
    } 
} 

// This code is contributed  
// by Devarshi Singh 

```

## Python3

```py

# Python3 implementation of the approach 

# Linked List Node 
class Node: 

    def __init__(self, data): 

        self.data = data 
        self.next = None

# Handle list operations 
class LinkedList: 

    def __init__(self): 

        self.head = None

    # Method to traverse list and 
    # return it in a format 
    def traverse(self): 

        linkedListStr = "" 
        temp = self.head 

        while temp: 
            linkedListStr += str(temp.data) + " -> "
            temp = temp.next

        return linkedListStr + "NULL"

    # Method to insert data in linked list 
    def insert(self, data): 

        newNode = Node(data) 

        if self.head is None: 
            self.head = newNode 
        else: 
            newNode.next = self.head 
            self.head = newNode 

# Helper function to reverse the list 
def reverse(Head): 

    if (Head is None and 
        Head.next is None): 
        return Head 

    prev = None
    curr = Head 

    while curr: 
        temp = curr.next
        curr.next = prev 
        prev = curr 
        curr = temp 

    Head = prev 
    return Head 

# Function to add two lists 
def listSum(l1, l2): 

    if l1 is None: 
        return l1 
    if l2 is None: 
        return l2 

    # Reverse first list 
    l1 = reverse(l1) 

    # Reverse second list 
    l2 = reverse(l2) 

    # Storing head whose reverse  
    # is to be returned This is  
    # where which will be final node 
    head = l1 
    prev = None
    c = 0
    sum = 0

    while l1 is not None and l2 is not None: 
        sum = c + l1.data + l2.data 
        l1.data = sum % 10
        c = int(sum / 10) 
        prev = l1 
        l1 = l1.next
        l2 = l2.next

    if l1 is not None or l2 is not None: 
        if l2 is not None: 
            prev.next = l2 
        l1 = prev.next

        while l1 is not None: 
            sum = c + l1.data 
            l1.data = sum % 10
            c = int(sum / 10) 
            prev = l1 
            l1 = l1.next

    if c > 0: 
        prev.next = Node(c) 

    return reverse(head) 

# Driver code 
linkedList1 = LinkedList() 
linkedList1.insert(3) 
linkedList1.insert(6) 
linkedList1.insert(5) 

linkedList2 = LinkedList() 
linkedList2.insert(2) 
linkedList2.insert(4) 
linkedList2.insert(8) 

linkedList3 = LinkedList() 
linkedList3.head = listSum(linkedList1.head, 
                           linkedList2.head) 

print(linkedList3.traverse()) 

# This code is contributed by Debidutta Rath 

```

## C#

```cs

// C# implementation of the above approach 
using System; 

public class Node  
{ 
    public int data; 
    public Node next; 

    // constructor 
    public Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

// Node closes 
public class LinkedList 
{ 
    Node head; 

    // Helper function to traverse 
    void traverse(Node head)  
    { 
        while(head != null) 
        { 
            Console.Write(head.data + "->"); 
            head = head.next; 
        } 
    } 

    // Helper function to insert data in linked list 
    void insert(int x) 
    { 
        Node temp = new Node(x); 
        if(head == null) head = temp; 
        else
        { 
            temp.next = head; 
            head = temp; 
        } 
    } 

    // Helper function to reverse the list 
    public static Node reverse(Node head) 
    { 
        if(head == null ||  
           head.next == null) return head; 

        Node prev = null; 
        Node curr = head; 
        while(curr != null) 
        { 
            Node temp = curr.next; 
            curr.next = prev; 
            prev = curr; 
            curr = temp; 
        } 
        head = prev; 
        return head; 
    } 

    // Function to add two lists 
    public static Node sum(Node l1, Node l2) 
    { 
        if(l2 == null) return l1; 
        if(l1 == null) return l2; 

        // reverse l1 list 
        l1 = reverse(l1); 

        // reverse l2 list 
        l2 = reverse(l2); 

        // storing head whose reverse is  
        // to be returned. This is where  
        // which will be final node 
        Node head = l1; 
        Node prev = null; 
        int c = 0,sum; 
        while(l1 != null && l2 != null) 
        { 
            sum = c + l1.data + l2.data; 
            l1.data = sum % 10; 
            c = sum / 10; 
            prev = l1; 
            l1 = l1.next; 
            l2 = l2.next; 
        } 

        if(l1 != null||l2 != null) 
        { 
            if(l2 != null) prev.next = l2; 
            l1 = prev.next; 
            while(l1 != null) 
            { 
                sum = c + l1.data; 
                l1.data = sum % 10; 
                c = sum / 10; 
                prev = l1; 
                l1 = l1.next; 
            } 
        } 
        if(c > 0) prev.next = new Node(c); 
        return reverse(head); 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        LinkedList l1 = new LinkedList(); 
        l1.insert(3); 
        l1.insert(6); 
        l1.insert(5); 
        LinkedList l2 = new LinkedList(); 
        l2.insert(2); 
        l2.insert(4); 
        l2.insert(8); 
        LinkedList l3 = new LinkedList(); 
        Node head = sum(l1.head, l2.head); 
        l3.traverse(head); 
        Console.Write("Null"); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
1 -> 4 -> 0 -> 5 -> NULL

```

**时间复杂度：** O（max（m，n）），其中 m 和 n 分别是列表 l1 和列表 l2 中的节点数。

**空间复杂度：** O（1）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。