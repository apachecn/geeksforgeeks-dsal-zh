# 从双链表

中删除所有偶数和节点

给定一个包含 **N 个**节点的[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，任务是从列表中删除所有节点，这些节点包含数字和为偶数的元素。

**示例：**

> **输入：** DLL = 18 < = > 15 < = > 8 < = > 9 < = > 14
> **输出 ：** 18 < = > 9 < = > 14
> **说明：**
> 链接列表包含：
> 18-> 1 + 8 = 9
> 15-> 1 + 5 = 6
> 8-> 8
> 9-> 9
> 14-> 1 + 4 = 5
> 在这里，包含 15 和 8 的节点的数字总和是偶数。
> 因此，这些节点已删除。
> 
> **输入：** DLL = 5 < = > 3 < = > 4 < = > 2 < = > 9
> **输出 ：** 5 < = > 3 < = > 9
> **说明：**
> 链表包含两个数字总和值 4 和 2。
> 因此，这些节点已被删除。

**方法：**

一种简单的方法是依次遍历双向链表的节点，并首先为每个节点遍历每个数字，找到该节点中存在的值的数字总和，然后 然后最后[删除数字和为偶数的节点](https://www.geeksforgeeks.org/delete-a-node-in-a-doubly-linked-list/)。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to remove all
// the Even Digit Sum Nodes from a
// doubly linked list

#include <bits/stdc++.h>

using namespace std;

// Node of the doubly linked list
struct Node {
    int data;
    Node *prev, *next;
};

// Function to insert a node at the beginning
// of the Doubly Linked List
void push(Node** head_ref, int new_data)
{
    // Allocate the node
    Node* new_node
        = (Node*)malloc(sizeof(struct Node));

    // Insert the data
    new_node->data = new_data;

    // Since we are adding at the beginning,
    // prev is always NULL
    new_node->prev = NULL;

    // Link the old list off the new node
    new_node->next = (*head_ref);

    // Change the prev of head node to new node
    if ((*head_ref) != NULL)
        (*head_ref)->prev = new_node;

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to find the digit sum
// for a number
int digitSum(int num)
{
    int sum = 0;
    while (num) {
        sum += (num % 10);
        num /= 10;
    }

    return sum;
}

// Function to delete a node
// in a Doubly Linked List.
// head_ref --> pointer to head node pointer.
// del --> pointer to node to be deleted
void deleteNode(Node** head_ref, Node* del)
{
    // Base case
    if (*head_ref == NULL || del == NULL)
        return;

    // If the node to be deleted is head node
    if (*head_ref == del)
        *head_ref = del->next;

    // Change next only if node to be
    // deleted is not the last node
    if (del->next != NULL)
        del->next->prev = del->prev;

    // Change prev only if node to be
    // deleted is not the first node
    if (del->prev != NULL)
        del->prev->next = del->next;

    // Finally, free the memory
    // occupied by del
    free(del);

    return;
}

// Function to to remove all
// the Even Digit Sum Nodes from a
// doubly linked list
void deleteEvenDigitSumNodes(Node** head_ref)
{
    Node* ptr = *head_ref;
    Node* next;

    // Iterating through the linked list
    while (ptr != NULL) {
        next = ptr->next;

        // If node's data's digit sum
        // is even
        if (!(digitSum(ptr->data) & 1))
            deleteNode(head_ref, ptr);

        ptr = next;
    }
}

// Function to print nodes in a
// given doubly linked list
void printList(Node* head)
{
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
}

// Driver Code
int main()
{

    Node* head = NULL;

    // Create the doubly linked list
    // 18 <-> 15 <-> 8 <-> 9 <-> 14
    push(&head, 14);
    push(&head, 9);
    push(&head, 8);
    push(&head, 15);
    push(&head, 18);

    cout << "Original List: ";
    printList(head);

    deleteEvenDigitSumNodes(&head);

    cout << "\nModified List: ";
    printList(head);
}

```

## Java

```java

// Java implementation to 
// remove all the Even 
// Digit Sum Nodes from a
// doubly linked list
import java.util.*;
class GFG{

// Node of the doubly 
// linked list
static class Node 
{
  int data;
  Node prev, next;
};

// Function to insert a node 
// at the beginning of the 
// Doubly Linked List
static Node push(Node head_ref, 
                 int new_data)
{
  // Allocate the node
  Node new_node = new Node();

  // Insert the data
  new_node.data = new_data;

  // Since we are adding 
  // at the beginning,
  // prev is always null
  new_node.prev = null;

  // Link the old list 
  // off the new node
  new_node.next = head_ref;

  // Change the prev of 
  // head node to new node
  if (head_ref != null)
    head_ref.prev = new_node;

  // Move the head to point 
  // to the new node
  head_ref = new_node;
  return head_ref;
}

// Function to find the digit sum
// for a number
static int digitSum(int num)
{
  int sum = 0;
  while (num > 0) 
  {
    sum += (num % 10);
    num /= 10;
  }
  return sum;
}

// Function to delete a node
// in a Doubly Linked List.
// head_ref -. pointer to head node pointer.
// del -. pointer to node to be deleted
static Node deleteNode(Node head_ref, 
                       Node del)
{
  // Base case
  if (head_ref == null || 
      del == null)
    return head_ref;

  // If the node to be 
  // deleted is head node
  if (head_ref == del)
    head_ref = del.next;

  // Change next only if node to be
  // deleted is not the last node
  if (del.next != null)
    del.next.prev = del.prev;

  // Change prev only if node to be
  // deleted is not the first node
  if (del.prev != null)
    del.prev.next = del.next;

  // Finally, free the memory
  // occupied by del
  del = null;

  return head_ref;
}

// Function to to remove all
// the Even Digit Sum Nodes from a
// doubly linked list
static Node deleteEvenDigitSumNodes(Node head_ref)
{
  Node ptr = head_ref;
  Node next;

  // Iterating through the linked list
  while (ptr != null) 
  {
    next = ptr.next;

    // If node's data's digit sum
    // is even
    if (!(digitSum(ptr.data) % 2 == 1))
      head_ref = deleteNode(head_ref, ptr);

    ptr = next;
  }
  return head_ref;
}

// Function to print nodes in a
// given doubly linked list
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
  Node head = null;

  // Create the doubly linked list
  // 18 <. 15 <. 8 <. 9 <. 14
  head = push(head, 14);
  head = push(head, 9);
  head = push(head, 8);
  head = push(head, 15);
  head = push(head, 18);

  System.out.print("Original List: ");
  printList(head);

  head = deleteEvenDigitSumNodes(head);

  System.out.print("\nModified List: ");
  printList(head);
}
}

// This code is contributed by shikhasingrajput

```

## Python3

```py

# Python3 implementation to remove all
# the Even Digit Sum Nodes from a
# doubly linked list

# Node of the doubly linked list
class Node():

    def __init__(self):

        self.data = 0
        self.prev = None
        self.next = None

# Function to insert a node at the
# beginning of the Doubly Linked List
def push(head_ref, new_data):

    # Allocate the node
    new_node = Node()

    # Insert the data
    new_node.data = new_data

    # Since we are adding at the beginning,
    # prev is always NULL
    new_node.prev = None

    # Link the old list off the new node
    new_node.next = head_ref

    # Change the prev of head node to new node
    if ((head_ref) != None):
        (head_ref).prev = new_node

    # Move the head to point to the new node
    (head_ref) = new_node

    return head_ref

# Function to find the digit sum
# for a number
def digitSum(num):

    sum = 0

    while (num != 0):
        sum += (num % 10)
        num //= 10

    return sum

# Function to delete a node
# in a Doubly Linked List.
# head_ref --> pointer to head node pointer.
# delete --> pointer to node to be deleted
def deleteNode(head_ref, delete):

    # Base case
    if (head_ref == None or delete == None):
        return

    # If the node to be deleted is head node
    if (head_ref == delete):
        head_ref = delete.next

    # Change next only if node to be
    # deleted is not the last node
    if (delete.next != None):
        delete.next.prev = delete.prev

    # Change prev only if node to be
    # deleted is not the first node
    if (delete.prev != None):
        delete.prev.next = delete.next

    # Finally, free the memory
    # occupied by delete
    del delete

    return

# Function to to remove all
# the Even Digit Sum Nodes from a
# doubly linked list
def deleteEvenDigitSumNodes(head_ref):

    ptr = head_ref
    next = None

    # Iterating through the linked list
    while (ptr != None):
        next = ptr.next

        # If node's data's digit sum
        # is even
        if (not (digitSum(ptr.data) & 1)):
            deleteNode(head_ref, ptr)

        ptr = next

    return head_ref

# Function to print nodes in a
# given doubly linked list
def printList(head):

    while (head != None):
        print(head.data, end = " ")
        head = head.next

# Driver code
if __name__=="__main__":

    head = None

    # Create the doubly linked list
    # 18 <-> 15 <-> 8 <-> 9 <-> 14
    head = push(head, 14)
    head = push(head, 9)
    head = push(head, 8)
    head = push(head, 15)
    head = push(head, 18)

    print("Original List:", end = " ")
    printList(head)

    head = deleteEvenDigitSumNodes(head)

    print("\nModified List: ", end = " ")
    printList(head)

# This code is contributed by rutvik_56

```

## C#

```cs

// C# implementation to 
// remove all the Even 
// Digit Sum Nodes from a
// doubly linked list
using System;
class GFG{

// Node of the doubly 
// linked list
class Node 
{
  public int data;
  public Node prev, next;
};

// Function to insert a node 
// at the beginning of the 
// Doubly Linked List
static Node push(Node head_ref, 
                 int new_data)
{
  // Allocate the node
  Node new_node = new Node();

  // Insert the data
  new_node.data = new_data;

  // Since we are adding 
  // at the beginning,
  // prev is always null
  new_node.prev = null;

  // Link the old list 
  // off the new node
  new_node.next = head_ref;

  // Change the prev of 
  // head node to new node
  if (head_ref != null)
    head_ref.prev = new_node;

  // Move the head to point 
  // to the new node
  head_ref = new_node;
  return head_ref;
}

// Function to find the digit sum
// for a number
static int digitSum(int num)
{
  int sum = 0;
  while (num > 0) 
  {
    sum += (num % 10);
    num /= 10;
  }
  return sum;
}

// Function to delete a node
// in a Doubly Linked List.
// head_ref -. pointer to head node pointer.
// del -. pointer to node to be deleted
static Node deleteNode(Node head_ref, 
                       Node del)
{
  // Base case
  if (head_ref == null || 
      del == null)
    return head_ref;

  // If the node to be 
  // deleted is head node
  if (head_ref == del)
    head_ref = del.next;

  // Change next only if node to be
  // deleted is not the last node
  if (del.next != null)
    del.next.prev = del.prev;

  // Change prev only if node to be
  // deleted is not the first node
  if (del.prev != null)
    del.prev.next = del.next;

  // Finally, free the memory
  // occupied by del
  del = null;

  return head_ref;
}

// Function to to remove all
// the Even Digit Sum Nodes from a
// doubly linked list
static Node deleteEvenDigitSumNodes(Node head_ref)
{
  Node ptr = head_ref;
  Node next;

  // Iterating through the linked list
  while (ptr != null) 
  {
    next = ptr.next;

    // If node's data's digit sum
    // is even
    if (!(digitSum(ptr.data) % 2 == 1))
      head_ref = deleteNode(head_ref, ptr);

    ptr = next;
  }
  return head_ref;
}

// Function to print nodes in a
// given doubly linked list
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
  Node head = null;

  // Create the doubly linked list
  // 18 <. 15 <. 8 <. 9 <. 14
  head = push(head, 14);
  head = push(head, 9);
  head = push(head, 8);
  head = push(head, 15);
  head = push(head, 18);

  Console.Write("Original List: ");
  printList(head);
  head = deleteEvenDigitSumNodes(head);
  Console.Write("\nModified List: ");
  printList(head);
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
Original List: 18 15 8 9 14 
Modified List: 18 9 14

```

***时间复杂度：**`O(n)`*，其中 N 是节点总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。