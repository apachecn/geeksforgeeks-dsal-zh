# 已对绝对值进行排序的链表

> 原文：[https://www.geeksforgeeks.org/sort-linked-list-already-sorted-absolute-values/](https://www.geeksforgeeks.org/sort-linked-list-already-sorted-absolute-values/)

给定一个基于绝对值排序的链表。 根据实际值对列表进行排序。

**示例**：

```
Input :  1 -> -10 
output: -10 -> 1

Input : 1 -> -2 -> -3 -> 4 -> -5 
output: -5 -> -3 -> -2 -> 1 -> 4 

Input : -5 -> -10 
Output: -10 -> -5

Input : 5 -> 10 
output: 5 -> 10

```

资料来源：[亚马逊面试](https://www.geeksforgeeks.org/amazon-interview-experience-set-258-for-sde1/)

一个简单的解决方案是从头到尾遍历链表。 对于每个访问的节点，请检查其是否有故障。 如果是，请将其从当前位置移除，然后插入正确的位置。 这是对链表的[插入排序的实现，此解决方案的时间复杂度为`O(n * n)`。](http://geeksquiz.com/insertion-sort-for-singly-linked-list/)

更好的解决方案是[使用归并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对链表进行排序。 该解决方案的时间复杂度为`O(n Log n)`。

一个有效的解决方案可以在`O(n)`时间内工作。 一个重要的观察结果是，所有负面因素都以相反的顺序出现。 因此，我们遍历列表，每当找到不规则的元素时，便将其移到链表的前面。

以下是上述想法的实现。

## C++

```cpp

// C++ program to sort a linked list, already 
// sorted by absolute values 
#include <bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node 
{ 
    Node* next; 
    int data; 
}; 

// Utility function to insert a node at the 
// beginning 
void push(Node** head, int data) 
{ 
    Node* newNode = new Node; 
    newNode->next = (*head); 
    newNode->data = data; 
    (*head) = newNode; 
} 

// Utility function to print a linked list 
void printList(Node* head) 
{ 
    while (head != NULL) 
    { 
        cout << head->data; 
        if (head->next != NULL) 
            cout << " -> "; 
        head = head->next; 
    } 
    cout<<endl; 
} 

// To sort a linked list by actual values. 
// The list is assumed to be sorted by absolute 
// values. 
void sortList(Node** head) 
{ 
    // Initialize previous and current nodes 
    Node* prev = (*head); 
    Node* curr = (*head)->next; 

    // Traverse list 
    while (curr != NULL) 
    { 
        // If curr is smaller than prev, then 
        // it must be moved to head 
        if (curr->data < prev->data) 
        { 
            // Detach curr from linked list 
            prev->next = curr->next; 

            // Move current node to beginning 
            curr->next = (*head); 
            (*head) = curr; 

            // Update current 
            curr = prev; 
        } 

        // Nothing to do if current element 
        // is at right place 
        else
            prev = curr; 

        // Move current 
        curr = curr->next; 
    } 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    push(&head, -5); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, -2); 
    push(&head, 1); 
    push(&head, 0); 

    cout << "Original list :\n"; 
    printList(head); 

    sortList(&head); 

    cout << "\nSorted list :\n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to sort a linked list, already 
// sorted by absolute values 
class SortList 
{ 
    static Node head;  // head of list 

    /* Linked list Node*/
    static class Node 
    { 
        int data; 
        Node next; 
        Node(int d) {data = d; next = null; } 
    } 

    // To sort a linked list by actual values. 
        // The list is assumed to be sorted by absolute 
        // values. 
    Node sortedList(Node head) 
    { 
        // Initialize previous and current nodes 
        Node prev = head; 
        Node curr = head.next; 

        // Traverse list 
        while(curr != null) 
        { 
            // If curr is smaller than prev, then 
                        // it must be moved to head 
            if(curr.data < prev.data) 
            { 
                // Detach curr from linked list 
                prev.next = curr.next; 

                // Move current node to beginning 
                curr.next = head; 
                head = curr; 

                // Update current 
                curr = prev; 
            } 

            // Nothing to do if current element 
                        // is at right place 
            else
            prev = curr; 

            // Move current 
            curr = curr.next; 
        } 
        return head; 
    } 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                  Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Function to print linked list */
    void printList(Node head) 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
           System.out.print(temp.data+" "); 
           temp = temp.next; 
        }   
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        SortList llist = new SortList(); 

        /* Constructed Linked List is 1->2->3->4->5->6-> 
           7->8->8->9->null */
        llist.push(-5); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(-2); 
        llist.push(1); 
        llist.push(0); 

        System.out.println("Original List :"); 
        llist.printList(llist.head); 

        llist.head = llist.sortedList(head); 

        System.out.println("Sorted list :"); 
        llist.printList(llist.head); 
    } 
}  

// This code has been contributed by Amit Khandelwal(Amit Khandelwal 1). 

```

## Python3

```py

# Python3 program to sort a linked list,  
# already sorted by absolute values  

# Linked list Node 
class Node: 
    def __init__(self, d): 
        self.data = d  
        self.next = None

class SortList: 
    def __init__(self): 
        self.head = None

    # To sort a linked list by actual values.  
    # The list is assumed to be sorted by  
    # absolute values.  
    def sortedList(self, head): 

        # Initialize previous and  
        # current nodes  
        prev = self.head  
        curr = self.head.next

        # Traverse list  
        while(curr != None):  

            # If curr is smaller than prev,  
            # then it must be moved to head  
            if(curr.data < prev.data): 

                # Detach curr from linked list  
                prev.next = curr.next

                # Move current node to beginning  
                curr.next = self.head  
                self.head = curr 

                # Update current  
                curr = prev  

            # Nothing to do if current element  
            # is at right place  
            else: 
                prev = curr 

            # Move current  
            curr = curr.next
        return self.head  

    # Inserts a new Node at front of the list 
    def push(self, new_data): 

        # 1 & 2: Allocate the Node &  
        #        Put in the data 
        new_node = Node(new_data)  

        # 3\. Make next of new Node as head  
        new_node.next = self.head  

        # 4\. Move the head to point to new Node  
        self.head = new_node 

    # Function to print linked list  
    def printList(self, head): 
        temp = head 
        while (temp != None):  
            print(temp.data, end = " ") 
            temp = temp.next
        print()  

# Driver Code 
llist = SortList() 

# Constructed Linked List is   
# 1->2->3->4->5->6->7->8->8->9->null  
llist.push(-5)  
llist.push(5)  
llist.push(4)  
llist.push(3)  
llist.push(-2)  
llist.push(1)  
llist.push(0)  

print("Original List :")  
llist.printList(llist.head) 

start = llist.sortedList(llist.head) 

print("Sorted list :")  
llist.printList(start) 

# This code is contributed by 
# Prerna Saini 

```

## C#

```cs

// C# program to sort a linked list, already 
// sorted by absolute values  
using System; 

public class SortList 
{ 
    Node head; // head of list 

    /* Linked list Node*/
    class Node 
    { 
        public int data; 
        public Node next; 
        public Node(int d)  
        { 
            data = d; next = null;  
        } 
    } 

    // To sort a linked list by actual values. 
    // The list is assumed to be sorted by absolute 
    // values. 
    Node sortedList(Node head) 
    { 
        // Initialize previous and current nodes 
        Node prev = head; 
        Node curr = head.next; 

        // Traverse list 
        while(curr != null) 
        { 
            // If curr is smaller than prev, then 
            // it must be moved to head 
            if(curr.data < prev.data) 
            { 
                // Detach curr from linked list 
                prev.next = curr.next; 

                // Move current node to beginning 
                curr.next = head; 
                head = curr; 

                // Update current 
                curr = prev; 
            } 

            // Nothing to do if current element 
            // is at right place 
            else
            prev = curr; 

            // Move current 
            curr = curr.next; 
        } 
        return head; 
    } 

    /* Inserts a new Node at front of the list. */
    public void push(int new_data) 
    { 
        /* 1 & 2: Allocate the Node & 
                Put in the data*/
        Node new_node = new Node(new_data); 

        /* 3\. Make next of new Node as head */
        new_node.next = head; 

        /* 4\. Move the head to point to new Node */
        head = new_node; 
    } 

    /* Function to print linked list */
    void printList(Node head) 
    { 
        Node temp = head; 
        while (temp != null) 
        { 
        Console.Write(temp.data + " "); 
        temp = temp.next; 
        }  
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main(String []args) 
    { 
        SortList llist = new SortList(); 

        /* Constructed Linked List is 1->2->3-> 
        4->5->6->7->8->8->9->null */
        llist.push(-5); 
        llist.push(5); 
        llist.push(4); 
        llist.push(3); 
        llist.push(-2); 
        llist.push(1); 
        llist.push(0); 

        Console.WriteLine("Original List :"); 
        llist.printList(llist.head); 

        llist.head = llist.sortedList(llist.head); 

        Console.WriteLine("Sorted list :"); 
        llist.printList(llist.head); 
    } 
}  

/* This code is contributed by 29AjayKumar */

```

**输出**：

```
Original list :
0 -> 1 -> -2 -> 3 -> 4 -> 5 -> -5

Sorted list :
-5 -> -2 -> 0 -> 1 -> 3 -> 4 -> 5

```

本文由 **Rahul Titare** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

