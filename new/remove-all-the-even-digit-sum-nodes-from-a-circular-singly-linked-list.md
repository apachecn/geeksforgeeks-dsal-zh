# 从循环单链接列表

> 原文：[https://www.geeksforgeeks.org/remove-all-the-even-digit-sum-nodes-from-a-circular-singly-linked-list/](https://www.geeksforgeeks.org/remove-all-the-even-digit-sum-nodes-from-a-circular-singly-linked-list/)

中删除所有偶数和节点

给定一个包含 **N 个**节点的[循环单链列表](https://www.geeksforgeeks.org/circular-linked-list/)，任务是从列表中删除所有节点，这些节点包含数字和为偶数的元素。

**范例**：

> **输入**：CLL = 9-> 11-> 34-> 6-> 13-> 21
> **输出**：9-> 34-> 21
> **说明**：
> 圆形单链表包含：
> 9-> 9
> 11-> 1 + 1 = 2
> 34-> 3 + 4 = 7
> 6-> 6
> 13-> 1 + 3 = 4
> 21-> 2 +1 = 3 [
> 这里，包含 11、6 和 13 的节点的数字总和为偶数。
> 因此，这些节点已删除。
> **输入**：5-> 11-> 16-> 21-> 17-> 10
> **输出**：5- > 16-> 21-> 10
> **说明**：
> 链表包含两位和值 11 和 17。
> 因此，这些节点已删除 。

**方法**：的想法是一个遍历循环单链列表的节点，对于每个节点，[通过遍历每个节点，找到节点中存在的值的数字总和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/) 数字。 如果数字总和为偶数，则[然后删除节点](https://www.geeksforgeeks.org/deletion-circular-linked-list/)。 否则，继续。

以下是上述方法的实现：

## C++

```cpp

// C++ program to remove all
// the Even Digit Sum Nodes from a
// circular singly linked list

#include <bits/stdc++.h>
using namespace std;

// Structure for a node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a node at the beginning
// of a Circular linked list
void push(struct Node** head_ref, int data)
{
    // Create a new node and make head as next
    // of it.
    struct Node* ptr1
        = (struct Node*)malloc(
            sizeof(struct Node));

    struct Node* temp = *head_ref;
    ptr1->data = data;
    ptr1->next = *head_ref;

    // If linked list is not NULL then
    // set the next of last node
    if (*head_ref != NULL) {

        // Find the node before head
        // and update next of it.
        while (temp->next != *head_ref)
            temp = temp->next;

        temp->next = ptr1;
    }
    else

        // Point for the first node
        ptr1->next = ptr1;

    *head_ref = ptr1;
}

// Function to delete the node from a 
// Circular Linked list
void deleteNode(Node* head_ref, Node* del)
{
    struct Node* temp = head_ref;

    // If node to be deleted is head node
    if (head_ref == del)
        head_ref = del->next;

    // Traverse list till not found
    // delete node
    while (temp->next != del) {
        temp = temp->next;
    }

    // Copy the address of the node
    temp->next = del->next;

    // Finally, free the memory
    // occupied by del
    free(del);

    return;
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

// Function to delete all the Even Digit Sum Nodes
// from the singly circular linked list
void deleteEvenDigitSumNodes(Node* head)
{
    struct Node* ptr = head;

    struct Node* next;

    // Traverse the list till the end
    do {

        // If the node's data is Fibonacci,
        // delete node 'ptr'
        if (!(digitSum(ptr->data) & 1))
            deleteNode(head, ptr);

        // Point to the next node
        next = ptr->next;
        ptr = next;

    } while (ptr != head);
}

// Function to print nodes in a
// given Circular linked list
void printList(struct Node* head)
{
    struct Node* temp = head;
    if (head != NULL) {
        do {
            printf("%d ", temp->data);
            temp = temp->next;
        } while (temp != head);
    }
}

// Driver code
int main()
{
    // Initialize lists as empty
    struct Node* head = NULL;

    // Created linked list will be
    // 9->11->34->6->13->21
    push(&head, 21);
    push(&head, 13);
    push(&head, 6);
    push(&head, 34);
    push(&head, 11);
    push(&head, 9);

    deleteEvenDigitSumNodes(head);

    printList(head);

    return 0;
}

```

## Java

```java

// Java program to remove all
// the Even Digit Sum Nodes from a
// circular singly linked list
import java.util.*;

class GFG{

// Structure for a node
static class Node
{
    int data;
    Node next;
};

// Function to insert a node at the beginning
// of a Circular linked list
static Node push(Node head_ref, int data)
{

    // Create a new node and make head 
    // as next of it.
    Node ptr1 = new Node();

    Node temp = head_ref;
    ptr1.data = data;
    ptr1.next = head_ref;

    // If linked list is not null then
    // set the next of last node
    if (head_ref != null) 
    {

        // Find the node before head
        // and update next of it.
        while (temp.next != head_ref)
            temp = temp.next;

        temp.next = ptr1;
    }
    else

        // Point for the first node
        ptr1.next = ptr1;

    head_ref = ptr1;
    return head_ref;
}

// Function to delete the node from a 
// Circular Linked list
static void deleteNode(Node head_ref, Node del)
{
    Node temp = head_ref;

    // If node to be deleted is head node
    if (head_ref == del)
        head_ref = del.next;

    // Traverse list till not found
    // delete node
    while (temp.next != del)
    {
        temp = temp.next;
    }

    // Copy the address of the node
    temp.next = del.next;

    // Finally, free the memory
    // occupied by del
    del = null;

    return;
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

// Function to delete all the Even Digit
// Sum Nodes from the singly circular 
// linked list
static void deleteEvenDigitSumNodes(Node head)
{
    Node ptr = head;
    Node next;

    // Traverse the list till the end
    do
    {

        // If the node's data is Fibonacci,
        // delete node 'ptr'
        if (!(digitSum(ptr.data) % 2 == 1))
            deleteNode(head, ptr);

        // Point to the next node
        next = ptr.next;
        ptr = next;
    } while (ptr != head);
}

// Function to print nodes in a
// given Circular linked list
static void printList(Node head)
{
    Node temp = head;
    if (head != null) 
    {
        do
        {
            System.out.printf("%d ", temp.data);
            temp = temp.next;
        } while (temp != head);
    }
}

// Driver code
public static void main(String[] args)
{

    // Initialize lists as empty
    Node head = null;

    // Created linked list will be
    // 9.11.34.6.13.21
    head = push(head, 21);
    head = push(head, 13);
    head = push(head, 6);
    head = push(head, 34);
    head = push(head, 11);
    head = push(head, 9);

    deleteEvenDigitSumNodes(head);

    printList(head);
}
}

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program to remove all
// the Even Digit Sum Nodes from a
// circular singly linked list
using System;
class GFG{

// Structure for a node
class Node
{
  public int data;
  public Node next;
};

// Function to insert a node 
// at the beginning of a 
// Circular linked list
static Node push(Node head_ref, 
                 int data)
{
  // Create a new node and make head 
  // as next of it.
  Node ptr1 = new Node();

  Node temp = head_ref;
  ptr1.data = data;
  ptr1.next = head_ref;

  // If linked list is not null then
  // set the next of last node
  if (head_ref != null) 
  {
    // Find the node before head
    // and update next of it.
    while (temp.next != head_ref)
      temp = temp.next;

    temp.next = ptr1;
  }
  else

    // Point for the first node
    ptr1.next = ptr1;

  head_ref = ptr1;
  return head_ref;
}

// Function to delete the node from a 
// Circular Linked list
static void deleteNode(Node head_ref, 
                       Node del)
{
  Node temp = head_ref;

  // If node to be deleted is head node
  if (head_ref == del)
    head_ref = del.next;

  // Traverse list till not found
  // delete node
  while (temp.next != del)
  {
    temp = temp.next;
  }

  // Copy the address of the node
  temp.next = del.next;

  // Finally, free the memory
  // occupied by del
  del = null;

  return;
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

// Function to delete all the Even Digit
// Sum Nodes from the singly circular 
// linked list
static void deleteEvenDigitSumNodes(Node head)
{
  Node ptr = head;
  Node next;

  // Traverse the list till the end
  do
  {
    // If the node's data is Fibonacci,
    // delete node 'ptr'
    if (!(digitSum(ptr.data) % 2 == 1))
      deleteNode(head, ptr);

    // Point to the next node
    next = ptr.next;
    ptr = next;
  } while (ptr != head);
}

// Function to print nodes in a
// given Circular linked list
static void printList(Node head)
{
  Node temp = head;
  if (head != null) 
  {
    do
    {
      Console.Write("{0} ", 
                    temp.data);
      temp = temp.next;
    } while (temp != head);
  }
}

// Driver code
public static void Main(String[] args)
{
  // Initialize lists as empty
  Node head = null;

  // Created linked list will be
  // 9.11.34.6.13.21
  head = push(head, 21);
  head = push(head, 13);
  head = push(head, 6);
  head = push(head, 34);
  head = push(head, 11);
  head = push(head, 9);

  deleteEvenDigitSumNodes(head);
  printList(head);
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
9 34 21

```

**时间复杂度**：*O（KN）*，其中 N 是链​​表的大小，K 是链表的最大数目中的位数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。