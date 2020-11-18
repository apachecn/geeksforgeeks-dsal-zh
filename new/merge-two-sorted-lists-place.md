# 合并两个已排序的列表（就地）

> 原文：[https://www.geeksforgeeks.org/merge-two-sorted-lists-place/](https://www.geeksforgeeks.org/merge-two-sorted-lists-place/)

给定两个排序列表，将它们合并，以生成组合的排序列表（不使用多余的空间）。

**示例**：

```
Input : head1: 5->7->9
        head2: 4->6->8 
Output : 4->5->6->7->8->9
Explanation: The output list is in sorted order.

Input : head1: 1->3->5->7
        head2: 2->4
Output : 1->2->3->4->5->7
Explanation: The output list is in sorted order.

```

 **以下文章中讨论了不同的解决方案。**

[合并两个排序的链接列表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)

 **方法 1（递归）

**方法**：如果对链表进行排序，则可以形成递归解决方案。

1.  比较两个链接列表的标题。

2.  在两个头节点中找到较小的节点。 当前元素将是两个头节点中的较小节点。

3.  这两个列表的其余元素将在此之后出现。

4.  现在运行带有参数，较小元素的下一个节点和另一个头的参数的递归函数。

5.  递归函数将返回与其余已排序元素链接的下一个较小元素。 现在将当前元素的下一个指向该元素，即 *curr_ele- > next = recursivefunction（）*

6.  处理一些角落情况。

    *   如果两个头都为 NULL，则返回 null。

    *   如果一个头为空，则返回另一个。

## C++

```cpp

// C program to merge two sorted linked lists 
// in-place. 
#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to create newNode in a linkedlist 
Node* newNode(int key) 
{ 
    struct Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// A utility function to print linked list 
void printList(Node* node) 
{ 
    while (node != NULL) { 
        printf("%d  ", node->data); 
        node = node->next; 
    } 
} 

// Merges two given lists in-place. This function 
// mainly compares head nodes and calls mergeUtil() 
Node* merge(Node* h1, Node* h2) 
{ 
    if (!h1) 
        return h2; 
    if (!h2) 
        return h1; 

    // start with the linked list 
    // whose head data is the least 
    if (h1->data < h2->data) { 
        h1->next = merge(h1->next, h2); 
        return h1; 
    } 
    else { 
        h2->next = merge(h1, h2->next); 
        return h2; 
    } 
} 

// Driver program 
int main() 
{ 
    Node* head1 = newNode(1); 
    head1->next = newNode(3); 
    head1->next->next = newNode(5); 

    // 1->3->5 LinkedList created 

    Node* head2 = newNode(0); 
    head2->next = newNode(2); 
    head2->next->next = newNode(4); 

    // 0->2->4 LinkedList created 

    Node* mergedhead = merge(head1, head2); 

    printList(mergedhead); 
    return 0; 
} 

```

## Java

```java

// Java program to merge two sorted 
// linked lists in-place. 
class GFG { 

    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to create newNode in a linkedlist 
    static Node newNode(int key) 
    { 
        Node temp = new Node(); 
        temp.data = key; 
        temp.next = null; 
        return temp; 
    } 

    // A utility function to print linked list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            System.out.printf("%d ", node.data); 
            node = node.next; 
        } 
    } 

    // Merges two given lists in-place. This function 
    // mainly compares head nodes and calls mergeUtil() 
    static Node merge(Node h1, Node h2) 
    { 
        if (h1 == null) 
            return h2; 
        if (h2 == null) 
            return h1; 

        // start with the linked list 
        // whose head data is the least 
        if (h1.data < h2.data) { 
            h1.next = merge(h1.next, h2); 
            return h1; 
        } 
        else { 
            h2.next = merge(h1, h2.next); 
            return h2; 
        } 
    } 

    // Driver program 
    public static void main(String args[]) 
    { 
        Node head1 = newNode(1); 
        head1.next = newNode(3); 
        head1.next.next = newNode(5); 

        // 1.3.5 LinkedList created 

        Node head2 = newNode(0); 
        head2.next = newNode(2); 
        head2.next.next = newNode(4); 

        // 0.2.4 LinkedList created 

        Node mergedhead = merge(head1, head2); 

        printList(mergedhead); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to merge two  
# sorted linked lists in-place. 
import math 

class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to create newNode in a linkedlist 
def newNode( key): 
    temp = Node(key) 
    temp.data = key 
    temp.next = None
    return temp 

# A utility function to print linked list 
def printList( node): 
    while (node != None): 
        print(node.data, end = " ") 
        node = node.next

# Merges two given lists in-place.  
# This function mainly compares  
# head nodes and calls mergeUtil() 
def merge( h1, h2): 
    if (h1 == None): 
        return h2 
    if (h2 == None): 
        return h1 

    # start with the linked list 
    # whose head data is the least 
    if (h1.data < h2.data): 
        h1.next = merge(h1.next, h2) 
        return h1 

    else: 
        h2.next = merge(h1, h2.next) 
        return h2 

# Driver Code 
if __name__=='__main__':  
    head1 = newNode(1) 
    head1.next = newNode(3) 
    head1.next.next = newNode(5) 

    # 1.3.5 LinkedList created 
    head2 = newNode(0) 
    head2.next = newNode(2) 
    head2.next.next = newNode(4) 

    # 0.2.4 LinkedList created 
    mergedhead = merge(head1, head2) 

    printList(mergedhead) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to merge two sorted 
// linked lists in-place. 
using System; 

class GFG { 

    public class Node { 
        public int data; 
        public Node next; 
    }; 

    // Function to create newNode in a linkedlist 
    static Node newNode(int key) 
    { 
        Node temp = new Node(); 
        temp.data = key; 
        temp.next = null; 
        return temp; 
    } 

    // A utility function to print linked list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            Console.Write("{0} ", node.data); 
            node = node.next; 
        } 
    } 

    // Merges two given lists in-place. This function 
    // mainly compares head nodes and calls mergeUtil() 
    static Node merge(Node h1, Node h2) 
    { 
        if (h1 == null) 
            return h2; 
        if (h2 == null) 
            return h1; 

        // start with the linked list 
        // whose head data is the least 
        if (h1.data < h2.data) { 
            h1.next = merge(h1.next, h2); 
            return h1; 
        } 
        else { 
            h2.next = merge(h1, h2.next); 
            return h2; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head1 = newNode(1); 
        head1.next = newNode(3); 
        head1.next.next = newNode(5); 

        // 1.3.5 LinkedList created 

        Node head2 = newNode(0); 
        head2.next = newNode(2); 
        head2.next.next = newNode(4); 

        // 0.2.4 LinkedList created 

        Node mergedhead = merge(head1, head2); 

        printList(mergedhead); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
0 1 2 3 4 5 

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    仅需要遍历链表之一。

*   **辅助空间**：`O(n)`。

    如果考虑了递归堆栈空间。

 **方法 2（迭代）

**方法**：这种方法与上述递归方法非常相似。

1.  从头到尾遍历列表。

2.  如果第二个列表的头节点位于第一个列表的两个节点之间，则将其插入其中，并使第二个列表的下一个节点为头。 继续此操作，直到两个列表中都没有节点为止，即遍历两个列表。

3.  如果在遍历时第一个列表已结束，请将下一个节点指向第二个列表的开头。

**注意**：比较两个列表，其中头值较小的列表是第一个列表。

## C++

```cpp

// C++ program to merge two sorted linked lists 
// in-place. 
#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to create newNode in a linkedlist 
struct Node* newNode(int key) 
{ 
    struct Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// A utility function to print linked list 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d  ", node->data); 
        node = node->next; 
    } 
} 

// Merges two lists with headers as h1 and h2\. 
// It assumes that h1's data is smaller than 
// or equal to h2's data. 
struct Node* mergeUtil(struct Node* h1, 
                       struct Node* h2) 
{ 
    // if only one node in first list 
    // simply point its head to second list 
    if (!h1->next) { 
        h1->next = h2; 
        return h1; 
    } 

    // Initialize current and next pointers of 
    // both lists 
    struct Node *curr1 = h1, *next1 = h1->next; 
    struct Node *curr2 = h2, *next2 = h2->next; 

    while (next1 && curr2) { 
        // if curr2 lies in between curr1 and next1 
        // then do curr1->curr2->next1 
        if ((curr2->data) >= (curr1->data) && (curr2->data) <= (next1->data)) { 
            next2 = curr2->next; 
            curr1->next = curr2; 
            curr2->next = next1; 

            // now let curr1 and curr2 to point 
            // to their immediate next pointers 
            curr1 = curr2; 
            curr2 = next2; 
        } 
        else { 
            // if more nodes in first list 
            if (next1->next) { 
                next1 = next1->next; 
                curr1 = curr1->next; 
            } 

            // else point the last node of first list 
            // to the remaining nodes of second list 
            else { 
                next1->next = curr2; 
                return h1; 
            } 
        } 
    } 
    return h1; 
} 

// Merges two given lists in-place. This function 
// mainly compares head nodes and calls mergeUtil() 
struct Node* merge(struct Node* h1, 
                   struct Node* h2) 
{ 
    if (!h1) 
        return h2; 
    if (!h2) 
        return h1; 

    // start with the linked list 
    // whose head data is the least 
    if (h1->data < h2->data) 
        return mergeUtil(h1, h2); 
    else
        return mergeUtil(h2, h1); 
} 

// Driver program 
int main() 
{ 
    struct Node* head1 = newNode(1); 
    head1->next = newNode(3); 
    head1->next->next = newNode(5); 

    // 1->3->5 LinkedList created 

    struct Node* head2 = newNode(0); 
    head2->next = newNode(2); 
    head2->next->next = newNode(4); 

    // 0->2->4 LinkedList created 

    struct Node* mergedhead = merge(head1, head2); 

    printList(mergedhead); 
    return 0; 
} 

```

## Java

```java

// Java program to merge two sorted 
// linked lists in-place. 
class GfG { 

    static class Node { 
        int data; 
        Node next; 
    } 

    // Function to create newNode in a linkedlist 
    static Node newNode(int key) 
    { 
        Node temp = new Node(); 
        temp.data = key; 
        temp.next = null; 
        return temp; 
    } 

    // A utility function to print linked list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
    } 

    // Merges two lists with headers as h1 and h2\. 
    // It assumes that h1's data is smaller than 
    // or equal to h2's data. 
    static Node mergeUtil(Node h1, Node h2) 
    { 
        // if only one node in first list 
        // simply point its head to second list 
        if (h1.next == null) { 
            h1.next = h2; 
            return h1; 
        } 

        // Initialize current and next pointers of 
        // both lists 
        Node curr1 = h1, next1 = h1.next; 
        Node curr2 = h2, next2 = h2.next; 

        while (next1 != null && curr2 != null) { 
            // if curr2 lies in between curr1 and next1 
            // then do curr1->curr2->next1 
            if ((curr2.data) >= (curr1.data) && (curr2.data) <= (next1.data)) { 
                next2 = curr2.next; 
                curr1.next = curr2; 
                curr2.next = next1; 

                // now let curr1 and curr2 to point 
                // to their immediate next pointers 
                curr1 = curr2; 
                curr2 = next2; 
            } 
            else { 
                // if more nodes in first list 
                if (next1.next != null) { 
                    next1 = next1.next; 
                    curr1 = curr1.next; 
                } 

                // else point the last node of first list 
                // to the remaining nodes of second list 
                else { 
                    next1.next = curr2; 
                    return h1; 
                } 
            } 
        } 
        return h1; 
    } 

    // Merges two given lists in-place. This function 
    // mainly compares head nodes and calls mergeUtil() 
    static Node merge(Node h1, Node h2) 
    { 
        if (h1 == null) 
            return h2; 
        if (h2 == null) 
            return h1; 

        // start with the linked list 
        // whose head data is the least 
        if (h1.data < h2.data) 
            return mergeUtil(h1, h2); 
        else
            return mergeUtil(h2, h1); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        Node head1 = newNode(1); 
        head1.next = newNode(3); 
        head1.next.next = newNode(5); 

        // 1->3->5 LinkedList created 

        Node head2 = newNode(0); 
        head2.next = newNode(2); 
        head2.next.next = newNode(4); 

        // 0->2->4 LinkedList created 

        Node mergedhead = merge(head1, head2); 

        printList(mergedhead); 
    } 
} 

// This code is contributed by 
// prerna saini 

```

## Python

```py

# Python program to merge two sorted linked lists 
# in-place. 

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to create newNode in a linkedlist 
def newNode(key): 

    temp = Node(0) 
    temp.data = key 
    temp.next = None
    return temp 

# A utility function to print linked list 
def printList(node): 

    while (node != None) : 
        print( node.data, end =" ") 
        node = node.next

# Merges two lists with headers as h1 and h2\. 
# It assumes that h1's data is smaller than 
# or equal to h2's data. 
def mergeUtil(h1, h2): 

    # if only one node in first list 
    # simply point its head to second list 
    if (h1.next == None) : 
        h1.next = h2 
        return h1 

    # Initialize current and next pointers of 
    # both lists 
    curr1 = h1 
    next1 = h1.next
    curr2 = h2 
    next2 = h2.next

    while (next1 != None and curr2 != None):  

        # if curr2 lies in between curr1 and next1 
        # then do curr1.curr2.next1 
        if ((curr2.data) >= (curr1.data) and
            (curr2.data) <= (next1.data)) : 
            next2 = curr2.next
            curr1.next = curr2 
            curr2.next = next1 

            # now let curr1 and curr2 to point 
            # to their immediate next pointers 
            curr1 = curr2 
            curr2 = next2 

        else : 
            # if more nodes in first list 
            if (next1.next) : 
                next1 = next1.next
                curr1 = curr1.next

            # else point the last node of first list 
            # to the remaining nodes of second list 
            else : 
                next1.next = curr2 
                return h1 

    return h1 

# Merges two given lists in-place. This function 
# mainly compares head nodes and calls mergeUtil() 
def merge( h1, h2): 

    if (h1 == None): 
        return h2 
    if (h2 == None): 
        return h1 

    # start with the linked list 
    # whose head data is the least 
    if (h1.data < h2.data): 
        return mergeUtil(h1, h2) 
    else: 
        return mergeUtil(h2, h1) 

# Driver program 

head1 = newNode(1) 
head1.next = newNode(3) 
head1.next.next = newNode(5) 

# 1.3.5 LinkedList created 

head2 = newNode(0) 
head2.next = newNode(2) 
head2.next.next = newNode(4) 

# 0.2.4 LinkedList created 

mergedhead = merge(head1, head2) 

printList(mergedhead) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to merge two sorted 
// linked lists in-place. 
using System; 

class GfG { 

    public class Node { 
        public int data; 
        public Node next; 
    } 

    // Function to create newNode in a linkedlist 
    static Node newNode(int key) 
    { 
        Node temp = new Node(); 
        temp.data = key; 
        temp.next = null; 
        return temp; 
    } 

    // A utility function to print linked list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
    } 

    // Merges two lists with headers as h1 and h2\. 
    // It assumes that h1's data is smaller than 
    // or equal to h2's data. 
    static Node mergeUtil(Node h1, Node h2) 
    { 
        // if only one node in first list 
        // simply point its head to second list 
        if (h1.next == null) { 
            h1.next = h2; 
            return h1; 
        } 

        // Initialize current and next pointers of 
        // both lists 
        Node curr1 = h1, next1 = h1.next; 
        Node curr2 = h2, next2 = h2.next; 

        while (next1 != null && curr2 != null) { 
            // if curr2 lies in between curr1 and next1 
            // then do curr1->curr2->next1 
            if ((curr2.data) >= (curr1.data) 
                && (curr2.data) <= (next1.data)) { 
                next2 = curr2.next; 
                curr1.next = curr2; 
                curr2.next = next1; 

                // now let curr1 and curr2 to point 
                // to their immediate next pointers 
                curr1 = curr2; 
                curr2 = next2; 
            } 
            else { 
                // if more nodes in first list 
                if (next1.next != null) { 
                    next1 = next1.next; 
                    curr1 = curr1.next; 
                } 

                // else point the last node of first list 
                // to the remaining nodes of second list 
                else { 
                    next1.next = curr2; 
                    return h1; 
                } 
            } 
        } 
        return h1; 
    } 

    // Merges two given lists in-place. This function 
    // mainly compares head nodes and calls mergeUtil() 
    static Node merge(Node h1, Node h2) 
    { 
        if (h1 == null) 
            return h2; 
        if (h2 == null) 
            return h1; 

        // start with the linked list 
        // whose head data is the least 
        if (h1.data < h2.data) 
            return mergeUtil(h1, h2); 
        else
            return mergeUtil(h2, h1); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head1 = newNode(1); 
        head1.next = newNode(3); 
        head1.next.next = newNode(5); 

        // 1->3->5 LinkedList created 

        Node head2 = newNode(0); 
        head2.next = newNode(2); 
        head2.next.next = newNode(4); 

        // 0->2->4 LinkedList created 

        Node mergedhead = merge(head1, head2); 
        printList(mergedhead); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
0 1 2 3 4 5 

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    由于只需要遍历链表之一。

*   **辅助空间**：`O(1)`。

    由于不需要空间。

本文由 **Mandula Vikitha** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 contribution.geeksforgeeks.org 撰写文章，或将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

