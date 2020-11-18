# 删除链接列表的中间部分

给定一个单链表，请删除链表的中间。 例如，如果给定的链表为1-> 2-> 3-> 4-> 5，则链表应修改为1-> 2-> 4-> 5

如果有偶数节点，那么将有两个中间节点，我们需要删除第二个中间元素。 例如，如果给定的链表是1-> 2-> 3-> 4-> 5-> 6，则应将其修改为1-> 2-> 3-> 5-> 6。

如果输入的链表为NULL，则应保持NULL。

如果输入的链表有1个节点，则应删除该节点并返回新的头。

**简单解决方案：**这个想法是先计算链接列表中的节点数，然后使用简单的删除过程删除第n / 2个节点。

```

// C++ program to delete middle 
// of a linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node { 
    int data; 
    struct Node* next; 
}; 
// count of nodes 
int countOfNodes(struct Node* head) 
{ 
    int count = 0; 
    while (head != NULL) { 
        head = head->next; 
        count++; 
    } 
    return count; 
} 

// Deletes middle node and returns 
// head of the modified list 
struct Node* deleteMid(struct Node* head) 
{ 
    // Base cases 
    if (head == NULL) 
        return NULL; 
    if (head->next == NULL) { 
        delete head; 
        return NULL; 
    } 
    struct Node* copyHead = head; 

    // Find the count of nodes 
    int count = countOfNodes(head); 

    // Find the middle node 
    int mid = count / 2; 

    // Delete the middle node 
    while (mid-- > 1) { 
        head = head->next; 
    } 

    // Delete the middle node 
    head->next = head->next->next; 

    return copyHead; 
} 

// A utility function to print 
// a given linked list 
void printList(struct Node* ptr) 
{ 
    while (ptr != NULL) { 
        cout << ptr->data << "->"; 
        ptr = ptr->next; 
    } 
    cout << "NULL\n"; 
} 

// Utility function to create a new node. 
Node* newNode(int data) 
{ 
    struct Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

/* Drier program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 

    cout << "Gven Linked List\n"; 
    printList(head); 

    head = deleteMid(head); 

    cout << "Linked List after deletion of middle\n"; 
    printList(head); 

    return 0; 
} 

```

**Output:**

```
Gven Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL

```

**复杂度分析：**

*   **时间复杂度：** O（n）。
    只需遍历链接列表
*   **辅助空间：** O（1）。
    不需要多余的空间。

<u>**有效解决方案：**</u>
**方法：**上述解决方案需要对链表进行两次遍历。 中间节点可以使用一个遍历删除。 这个想法是使用两个指针，slow_ptr和fast_ptr。 两个指针都从列表的开头开始。 当fast_ptr到达末尾时，slow_ptr到达中间。 此想法与帖子的[方法2中使用的想法相同。 这篇文章中的另一件事是跟踪中间节点的先前位置，以便可以删除中间节点。](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)

下面是实现。

## C ++

```

// C++ program to delete middle 
// of a linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Deletes middle node and returns  
// head of the modified list 
struct Node* deleteMid(struct Node* head) 
{ 
    // Base cases 
    if (head == NULL) 
        return NULL; 
    if (head->next == NULL) { 
        delete head; 
        return NULL; 
    } 

    // Initialize slow and fast pointers 
    // to reach middle of linked list 
    struct Node* slow_ptr = head; 
    struct Node* fast_ptr = head; 

    // Find the middle and previous of middle. 
// To store previous of slow_ptr     
struct Node* prev;  
    while (fast_ptr != NULL  
&& fast_ptr->next != NULL) { 
        fast_ptr = fast_ptr->next->next; 
        prev = slow_ptr; 
        slow_ptr = slow_ptr->next; 
    } 

    // Delete the middle node 
    prev->next = slow_ptr->next; 
    delete slow_ptr; 

    return head; 
} 

// A utility function to print  
// a given linked list 
void printList(struct Node* ptr) 
{ 
    while (ptr != NULL) { 
        cout << ptr->data << "->"; 
        ptr = ptr->next; 
    } 
    cout << "NULL\n"; 
} 

// Utility function to create a new node. 
Node* newNode(int data) 
{ 
    struct Node* temp = new Node; 
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

    cout << "Gven Linked List\n"; 
    printList(head); 

    head = deleteMid(head); 

    cout << "Linked List after deletion of middle\n"; 
    printList(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to delete the  
// middle of a linked list 
class GfG { 

    /* Link list Node */
    static class Node { 
        int data; 
        Node next; 
    } 

    // Deletes middle node and returns 
    // head of the modified list 
    static Node deleteMid(Node head) 
    { 
        // Base cases 
        if (head == null) 
            return null; 
        if (head.next == null) { 
            return null; 
        } 

        // Initialize slow and fast pointers  
        // to reach middle of linked list 
        Node slow_ptr = head; 
        Node fast_ptr = head; 

        // Find the middle and previous of middle. 
        Node prev = null; 

        // To store previous of slow_ptr 
        while (fast_ptr != null 
&& fast_ptr.next != null) { 
            fast_ptr = fast_ptr.next.next; 
            prev = slow_ptr; 
            slow_ptr = slow_ptr.next; 
        } 

        // Delete the middle node 
        prev.next = slow_ptr.next; 

        return head; 
    } 

    // A utility function to print  
// a given linked list 
    static void printList(Node ptr) 
    { 
        while (ptr != null) { 
            System.out.print(ptr.data + "->"); 
            ptr = ptr.next; 
        } 
        System.out.println("NULL"); 
    } 

    // Utility function to create a new node. 
    static Node newNode(int data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = null; 
        return temp; 
    } 

    /* Drier code*/
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        Node head = newNode(1); 
        head.next = newNode(2); 
        head.next.next = newNode(3); 
        head.next.next.next = newNode(4); 

        System.out.println("Gven Linked List"); 
        printList(head); 

        head = deleteMid(head); 

        System.out.println("Linked List after deletion of middle"); 
        printList(head); 
    } 
} 

// This code is contributed by Prerna saini. 

```

## Python3

```

# Python3 program to delete the 
# middle of a linked list 

# Linked List Node 
class Node: 

    def __init__(self, data): 

        self.data = data 
        self.next = None

# Create and handle list operations 
class LinkedList: 

    def __init__(self): 

        # Head of the list 
        self.head = None 

    # Add new node to the list end 
    def addToList(self, data): 

        newNode = Node(data) 
        if self.head is None: 
            self.head = newNode 
            return

        last = self.head 

        while last.next: 
            last = last.next

        last.next = newNode 

    # Returns the list in string format 
    def __str__(self): 

        linkedListStr = "" 
        temp = self.head 

        while temp: 
            linkedListStr += str(temp.data) + "->"
            temp = temp.next

        return linkedListStr + "NULL"

    # Method deletes middle node 
    def deleteMid(self): 

        # Base cases 
        if (self.head is None or 
            self.head.next is None): 
            return

        # Initialize slow and fast pointers 
        # to reach middle of linked list 
        slow_Ptr = self.head 
        fast_Ptr = self.head 

        # Find the middle and previous of middle 
        prev = None

        # To store previous of slow pointer 
        while (fast_Ptr is not None and 
               fast_Ptr.next is not None): 
            fast_Ptr = fast_Ptr.next.next
            prev = slow_Ptr 
            slow_Ptr = slow_Ptr.next

        # Delete the middle node 
        prev.next = slow_Ptr.next

# Driver code 
linkedList = LinkedList() 

linkedList.addToList(1) 
linkedList.addToList(2) 
linkedList.addToList(3) 
linkedList.addToList(4) 

print("Given Linked List") 
print(linkedList) 

linkedList.deleteMid() 

print("Linked List after deletion of middle") 
print(linkedList) 

# This code is contributed by Debidutta Rath 

```

## C＃

```

// C# program to delete middle of a linked list 
using System; 

class GfG { 

    /* Link list Node */
    class Node { 
        public int data; 
        public Node next; 
    } 

    // Deletes middle node and returns 
    // head of the modified list 
    static Node deleteMid(Node head) 
    { 
        // Base cases 
        if (head == null) 
            return null; 
        if (head.next == null) { 
            return null; 
        } 

        // Initialize slow and fast pointers 
        // to reach middle of linked list 
        Node slow_ptr = head; 
        Node fast_ptr = head; 

        // Find the middle and previous of middle. 
        Node prev = null; 

        // To store previous of slow_ptr 
        while (fast_ptr != null && fast_ptr.next != null) { 
            fast_ptr = fast_ptr.next.next; 
            prev = slow_ptr; 
            slow_ptr = slow_ptr.next; 
        } 

        // Delete the middle node 
        prev.next = slow_ptr.next; 

        return head; 
    } 

    // A utility function to print 
    // a given linked list 
    static void printList(Node ptr) 
    { 
        while (ptr != null) { 
            Console.Write(ptr.data + "->"); 
            ptr = ptr.next; 
        } 
        Console.WriteLine("NULL"); 
    } 

    // Utility function to create a new node. 
    static Node newNode(int data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = null; 
        return temp; 
    } 

    /* Drier code*/
    public static void Main(String[] args) 
    { 
        /* Start with the empty list */
        Node head = newNode(1); 
        head.next = newNode(2); 
        head.next.next = newNode(3); 
        head.next.next.next = newNode(4); 

        Console.WriteLine("Gven Linked List"); 
        printList(head); 

        head = deleteMid(head); 

        Console.WriteLine("Linked List after"
                          + "deletion of middle"); 
        printList(head); 
    } 
} 

/* This code is contributed by 29AjayKumar */

```

**Output:**

```
Gven Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL

```

**复杂度分析：**

*   **时间复杂度：** O（n）。
    只需遍历链接列表
*   **辅助空间：** O（1）。
    由于不需要额外的空间。

本文由 **Piyush Gupta** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，那么您也可以写一篇文章，然后将您的文章邮寄到contribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。