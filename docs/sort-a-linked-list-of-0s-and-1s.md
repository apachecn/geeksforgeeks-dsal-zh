# 对 0 和 1 的链表进行排序

> 原文:[https://www . geesforgeks . org/sort-a-link-list-of-0s-and-1s/](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-and-1s/)

给定由二进制整数 0 和 1 组成的大小为 **N** 的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的头部，任务是[对给定的链表](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序。

**示例:**

> ***输入:**head =*1->0->1->0->1->0->NULL****输出:***0->0->0->1->1->1->NULL*
> 
> ****输入:***head = 1->1->0->NULL ****输出:***0->1->1->NULL**

****天真方法:**解决给定问题最简单的方法是对给定链表执行[合并排序](https://www.geeksforgeeks.org/merge-sort/)或[插入排序](https://www.geeksforgeeks.org/insertion-sort/)并排序。已经讨论了[使用合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对链表进行排序和[使用插入排序](https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)对链表进行排序的实现。**

*****时间复杂度:** O(N * log N)*
***辅助空间:** O(N)***

****高效方法:**上述方法也可以通过统计给定链表中 **1s** 和 **0s** 的数量，并相应更新链表中节点的值来进行优化。按照以下步骤解决问题:**

*   **[遍历给定的链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)并将 **0s** 和 **1s** 的计数存储在变量中，分别说**零**和**一**。**
*   **现在，再次遍历链表，将第一个**值为零的**节点改为 **0** ，然后将剩余的节点改为 **1** 。**
*   **完成上述步骤后，[打印链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)作为结果排序列表。**

**下面是上述方法的实现:**

## **C++**

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Link list node
class Node {
public:
    int data;
    Node* next;
};

// Function to print linked list
void printList(Node* node)
{
    // Iterate until node is NOT NULL
    while (node != NULL) {

        // Print the data
        cout << node->data << " ";
        node = node->next;
    }
}

// Function to sort the linked list
// consisting of 0s and 1s
void sortList(Node* head)
{
    // Base Case
    if ((head == NULL)
        || (head->next == NULL)) {
        return;
    }

    // Store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    // Stores the head node
    Node* temp = head;

    // Traverse the list Head
    while (temp != NULL) {

        // If node->data value is 0
        if (temp->data == 0) {

            // Increment count0 by 1
            count0++;
        }

        // Otherwise, increment the
        // count of 1s
        else {
            count1++;
        }

        // Update the temp node
        temp = temp->next;
    }

    // Update the temp to head
    temp = head;

    // Traverse the list and update
    // the first count0 nodes as 0
    while (count0--) {
        temp->data = 0;
        temp = temp->next;
    }

    // Now, update the value of the
    // remaining count1 nodes as 1
    while (count1--) {
        temp->data = 1;
        temp = temp->next;
    }

    // Print the Linked List
    printList(head);
}

// Function to push a node
void push(Node** head_ref, int new_data)
{
    // Allocate node
    Node* new_node = new Node();

    // Put in the data
    new_node->data = new_data;

    // Link the old list of the
    // new node
    new_node->next = (*head_ref);

    // Move the head to point to
    // the new node
    (*head_ref) = new_node;
}

// Driver Code
int main(void)
{
    Node* head = NULL;
    push(&head, 0);
    push(&head, 1);
    push(&head, 0);
    push(&head, 1);
    push(&head, 1);
    push(&head, 1);
    push(&head, 1);
    push(&head, 1);
    push(&head, 0);
    sortList(head);

    return 0;
}**
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
**// Java program for the above approach
import java.util.*;
class GFG{

  // Link list node
  static class Node {

    int data;
    Node next;
  };

  // Function to print linked list
  static void printList(Node node)
  {

    // Iterate until node is NOT null
    while (node != null) {

      // Print the data
      System.out.print(node.data+ " ");
      node = node.next;
    }
  }

  // Function to sort the linked list
  // consisting of 0s and 1s
  static void sortList(Node head)
  {
    // Base Case
    if ((head == null)
        || (head.next == null)) {
      return;
    }

    // Store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    // Stores the head node
    Node temp = head;

    // Traverse the list Head
    while (temp != null) {

      // If node.data value is 0
      if (temp.data == 0) {

        // Increment count0 by 1
        count0++;
      }

      // Otherwise, increment the
      // count of 1s
      else {
        count1++;
      }

      // Update the temp node
      temp = temp.next;
    }

    // Update the temp to head
    temp = head;

    // Traverse the list and update
    // the first count0 nodes as 0
    while (count0>0) {
      temp.data = 0;
      temp = temp.next;
      count0--;
    }

    // Now, update the value of the
    // remaining count1 nodes as 1
    while (count1>0) {
      temp.data = 1;
      temp = temp.next;
      count1--;
    }

    // Print the Linked List
    printList(head);
  }

  // Function to push a node
  static Node push(Node head_ref, int new_data)
  {
    // Allocate node
    Node new_node = new Node();

    // Put in the data
    new_node.data = new_data;

    // Link the old list of the
    // new node
    new_node.next = head_ref;

    // Move the head to point to
    // the new node
    head_ref = new_node;
    return head_ref;
  }

  // Driver Code
  public static void main(String[] args)
  {
    Node head = null;
    head = push(head, 0);
    head = push(head, 1);
    head = push(head, 0);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 0);
    sortList(head);

  }
}

// This code is contributed by umadevi9616**
```

## **蟒蛇 3**

```
**# Python program for the above approach

# Link list Node
class Node:
    def __init__(self):
        self.data = 0;
        self.next = None;

# Function to prlinked list
def printList(Node):

    # Iterate until Node is NOT None
    while (Node != None):

        # Prthe data
        print(Node.data, end=" ");
        Node = Node.next;

# Function to sort the linked list
# consisting of 0s and 1s
def sortList(head):
    # Base Case
    if ((head == None) or (head.next == None)):
        return;

    # Store the count of 0s and 1s
    count0 = 0; count1 = 0;

    # Stores the head Node
    temp = head;

    # Traverse the list Head
    while (temp != None):

        # If Node.data value is 0
        if (temp.data == 0):

            # Increment count0 by 1
            count0 += 1;

        # Otherwise, increment the
        # count of 1s
        else:
            count1 += 1;

        # Update the temp Node
        temp = temp.next;

    # Update the temp to head
    temp = head;

    # Traverse the list and update
    # the first count0 Nodes as 0
    while (count0 > 0):
        temp.data = 0;
        temp = temp.next;
        count0 -= 1;

    # Now, update the value of the
    # remaining count1 Nodes as 1
    while (count1 > 0):
        temp.data = 1;
        temp = temp.next;
        count1 -= 1;

    # Prthe Linked List
    printList(head);

# Function to push a Node
def push(head_ref, new_data):

    # Allocate Node
    new_Node = Node();

    # Put in the data
    new_Node.data = new_data;

    # Link the old list of the
    # new Node
    new_Node.next = head_ref;

    # Move the head to poto
    # the new Node
    head_ref = new_Node;
    return head_ref;

# Driver Code
if __name__ == '__main__':
    head = None;
    head = push(head, 0);
    head = push(head, 1);
    head = push(head, 0);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 1);
    head = push(head, 0);
    sortList(head);

# This code is contributed by umadevi9616**
```

## **C#**

```
**// C# program for the above approach
using System;

public class GFG {

    // Link list node
public    class Node {

    public    int data;
    public    Node next;
    };

    // Function to print linked list
    static void printList(Node node) {

        // Iterate until node is NOT null
        while (node != null) {

            // Print the data
            Console.Write(node.data + " ");
            node = node.next;
        }
    }

    // Function to sort the linked list
    // consisting of 0s and 1s
    static void sortList(Node head) {
        // Base Case
        if ((head == null) || (head.next == null)) {
            return;
        }

        // Store the count of 0s and 1s
        int count0 = 0, count1 = 0;

        // Stores the head node
        Node temp = head;

        // Traverse the list Head
        while (temp != null) {

            // If node.data value is 0
            if (temp.data == 0) {

                // Increment count0 by 1
                count0++;
            }

            // Otherwise, increment the
            // count of 1s
            else {
                count1++;
            }

            // Update the temp node
            temp = temp.next;
        }

        // Update the temp to head
        temp = head;

        // Traverse the list and update
        // the first count0 nodes as 0
        while (count0 > 0) {
            temp.data = 0;
            temp = temp.next;
            count0--;
        }

        // Now, update the value of the
        // remaining count1 nodes as 1
        while (count1 > 0) {
            temp.data = 1;
            temp = temp.next;
            count1--;
        }

        // Print the Linked List
        printList(head);
    }

    // Function to push a node
    static Node push(Node head_ref, int new_data) {
        // Allocate node
        Node new_node = new Node();

        // Put in the data
        new_node.data = new_data;

        // Link the old list of the
        // new node
        new_node.next = head_ref;

        // Move the head to point to
        // the new node
        head_ref = new_node;
        return head_ref;
    }

    // Driver Code
    public static void Main(String[] args) {
        Node head = null;
        head = push(head, 0);
        head = push(head, 1);
        head = push(head, 0);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 0);
        sortList(head);

    }
}

// This code is contributed by umadevi9616**
```

## **java 描述语言**

```
**<script>
// javascript program for the above approach

    // Link list node
class Node {
    constructor() {
        this.data = 0;
        this.next = null;
    }
}

    // Function to print linked list
    function printList(node) {

        // Iterate until node is NOT null
        while (node != null) {

            // Print the data
            document.write(node.data + " ");
            node = node.next;
        }
    }

    // Function to sort the linked list
    // consisting of 0s and 1s
    function sortList(head)
    {

        // Base Case
        if ((head == null) || (head.next == null)) {
            return;
        }

        // Store the count of 0s and 1s
        var count0 = 0, count1 = 0;

        // Stores the head node
        var temp = head;

        // Traverse the list Head
        while (temp != null) {

            // If node.data value is 0
            if (temp.data == 0) {

                // Increment count0 by 1
                count0++;
            }

            // Otherwise, increment the
            // count of 1s
            else {
                count1++;
            }

            // Update the temp node
            temp = temp.next;
        }

        // Update the temp to head
        temp = head;

        // Traverse the list and update
        // the first count0 nodes as 0
        while (count0 > 0) {
            temp.data = 0;
            temp = temp.next;
            count0--;
        }

        // Now, update the value of the
        // remaining count1 nodes as 1
        while (count1 > 0) {
            temp.data = 1;
            temp = temp.next;
            count1--;
        }

        // Print the Linked List
        printList(head);
    }

    // Function to push a node
    function push(head_ref , new_data)
    {

        // Allocate node
        var new_node = new Node();

        // Put in the data
        new_node.data = new_data;

        // Link the old list of the
        // new node
        new_node.next = head_ref;

        // Move the head to point to
        // the new node
        head_ref = new_node;
        return head_ref;
    }

    // Driver Code   
        var head = null;
        head = push(head, 0);
        head = push(head, 1);
        head = push(head, 0);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 1);
        head = push(head, 0);
        sortList(head);

// This code is contributed by umadevi9616
</script>**
```

****Output:** 

```
0 0 0 1 1 1 1 1 1
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**