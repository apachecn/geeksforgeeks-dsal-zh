# 交替合并两个链表的奇数和偶数节点

> 原文：[https://www.geeksforgeeks.org/merge-odd-and-even-positioned-nodes-of-two-linked-lists-alternately/](https://www.geeksforgeeks.org/merge-odd-and-even-positioned-nodes-of-two-linked-lists-alternately/)

给定两个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)`L1`和`L2`，任务是打印新的列表，通过交替合并`L1`奇数位置节点和`L2`的偶数位置节点来获得。 

**示例**：

> **输入**：`L1 = 8 -> 5 -> 3 -> 2 -> 10 -> NULL, L2 = 11 -> 13 -> 1  -> 6 -> 9 -> NULL`
>
> **输出**：`8 -> 13 -> 3 -> 6 -> 10 -> NULL`
>
> **说明**：
>
> `L1`的奇数位置节点是`{8, 3, 10}`，偶数的节点`L2`是`{13, 6}`。
>
> 交替合并将生成链表`8 -> 13 -> 3 -> 6 -> 10 -> NULL`
> 
> **输入**：`L1 = 1 -> 5 -> 10 -> 12 -> 13 -> 19 -> 6 -> NULL, L2 = 2  -> 7 -> 9 -> NULL`
>
> **输出**：`1 -> 7 -> 10 -> 13 -> 6 -> NULL`
>
> **说明**：
>
> `L1`的奇数位置节点为`{1, 10, 13, 6}`，`L2`的偶数位置节点为`{7}`。
>
> 交替合并将生成链表`1 -> 7 -> 10 -> 13 -> 6 -> NULL`

**方法**：请按照以下步骤解决问题：

*   同时开始从`L1`的**第一节点**和`L2`的第二节点开始遍历。

*   将`L1`的**第一个节点**添加到结果列表中，并将其与`L2`的第二个节点连接，然后移至`L1`的**下一个奇数节点**。 同样，将`L2`的**第二个节点**连接到`L1`的**当前奇数节点**，然后移至`L2`的**下一个偶数节点**。

*   重复上述步骤，直到到达列表之一的末尾。

*   遍历另一个列表，并继续从该列表中将所需节点添加到结果列表中。

*   最后，打印结果列表。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
class node {
public:
    int data;
    node* next;
    node(int d)
    {
        data = d;
        next = NULL;
    }
};

// Function to insert the node
// at the head of the linkedlist
void insert_at_head(node*& head, int data)
{
    node* n = new node(data);
    n->next = head;
    head = n;
    return;
}

// Function to print the linked list
void print(node* head)
{
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << endl;
    return;
}

// Function to merge the odd and
// even positioned nodes of two
// given linked lists alternately
node* merge_alternate(node* head1, node* head2)
{
    // Traverse from the second
    // node of second linked list
    if (head2)
        head2 = head2->next;

    // Stores the head of
    // the resultant list
    node* head3 = NULL;

    // Stores the current node
    node* cur = NULL;

    // Store the first node of
    // first list in the result
    if (head1)
        head3 = head1;

    // Otherwise
    else
        head3 = head2;

    // Traverse until end of a
    // one of the list is reached
    while (head1 != NULL && head2 != NULL) {

        // If there is a previous node then
        // connect that with the current node
        if (cur)
            cur->next = head1;

        // Update the current node
        cur = head1;

        // If next odd node exists
        if (head1->next != NULL)

            // Store the next odd node
            head1 = head1->next->next;

        // Otherwise
        else

            // Reach end of list
            head1 = NULL;

        // Connect the first node
        // with the second node
        cur->next = head2;

        // Update the current node
        cur = head2;

        // If next even node exists
        if (head2->next != NULL)

            // Store the next even node
            head2 = head2->next->next;

        // Otherwise
        else

            // Reach the end of the list
            head2 = NULL;
    }

    // If end of the second
    // list has been reached
    while (head1 != NULL) {

        // Connect with the
        // previous node
        if (cur)
            cur->next = head1;

        // Update the current node
        cur = head1;

        // If next odd node exists
        if (head1->next != NULL)

            // Store the next odd node
            head1 = head1->next->next;

        // Otherwise
        else

            // Reach end of list
            head1 = NULL;
    }

    // If end of second list
    // has been reached
    while (head2 != NULL) {

        // Connect with the
        // previous node
        if (cur)
            cur->next = head2;

        // Update the current node
        cur = head2;

        // If next even node exists
        if (head2->next != NULL)

            // Store the next odd node
            head2 = head2->next->next;

        // Otherwise
        else

            // Reach end of list
            head2 = NULL;
    }

    // End of the resultant list
    if (cur)
        cur->next = NULL;

    // Returning the head of
    // the resultant node
    return head3;
}

// Driver Code
int main()
{
    node *head1 = NULL, *head2 = NULL;

    // Create linked list
    insert_at_head(head1, 6);
    insert_at_head(head1, 19);
    insert_at_head(head1, 13);
    insert_at_head(head1, 12);
    insert_at_head(head1, 10);
    insert_at_head(head1, 5);
    insert_at_head(head1, 1);

    insert_at_head(head2, 9);
    insert_at_head(head2, 7);
    insert_at_head(head2, 2);

    // Merging the linked lists
    head1 = merge_alternate(head1, head2);

    print(head1);
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Structure of a Node
static class node 
{
  public int data;
  node next;
  node(int d)
  {
    data = d;
    next = null;
  }
};

// Function to insert the node
// at the head of the linkedlist
static node insert_at_head(node head, 
                           int data)
{
  node n = new node(data);
  n.next = head;
  head = n;
  return head;
}

// Function to print the linked list
static void print(node head)
{
  while (head != null) 
  {
    System.out.print(head.data + " ");
    head = head.next;
  }
  System.out.println();
  return;
}

// Function to merge the odd and
// even positioned nodes of two
// given linked lists alternately
static node merge_alternate(node head1, 
                            node head2)
{
  // Traverse from the second
  // node of second linked list
  if (head2 != null)
    head2 = head2.next;

  // Stores the head of
  // the resultant list
  node head3 = null;

  // Stores the current node
  node cur = null;

  // Store the first node of
  // first list in the result
  if (head1 != null)
    head3 = head1;

  // Otherwise
  else
    head3 = head2;

  // Traverse until end of a
  // one of the list is reached
  while (head1 != null && head2 != null) 
  {
    // If there is a previous node then
    // connect that with the current node
    if (cur != null)
      cur.next = head1;

    // Update the current node
    cur = head1;

    // If next odd node exists
    if (head1.next != null)

      // Store the next odd node
      head1 = head1.next.next;

    // Otherwise
    else

      // Reach end of list
      head1 = null;

    // Connect the first node
    // with the second node
    cur.next = head2;

    // Update the current node
    cur = head2;

    // If next even node exists
    if (head2.next != null)

      // Store the next even node
      head2 = head2.next.next;

    // Otherwise
    else

      // Reach the end of the list
      head2 = null;
  }

  // If end of the second
  // list has been reached
  while (head1 != null) 
  {
    // Connect with the
    // previous node
    if (cur != null)
      cur.next = head1;

    // Update the current node
    cur = head1;

    // If next odd node exists
    if (head1.next != null)

      // Store the next odd node
      head1 = head1.next.next;

    // Otherwise
    else

      // Reach end of list
      head1 = null;
  }

  // If end of second list
  // has been reached
  while (head2 != null) 
  {
    // Connect with the
    // previous node
    if (cur != null)
      cur.next = head2;

    // Update the current node
    cur = head2;

    // If next even node exists
    if (head2.next != null)

      // Store the next odd node
      head2 = head2.next.next;

    // Otherwise
    else

      // Reach end of list
      head2 = null;
  }

  // End of the resultant list
  if (cur != null)
    cur.next = null;

  // Returning the head of
  // the resultant node
  return head3;
}

// Driver Code
public static void main(String[] args)
{
  node head1 = null, head2 = null;

  // Create linked list
  head1 = insert_at_head(head1, 6);
  head1 = insert_at_head(head1, 19);
  head1 = insert_at_head(head1, 13);
  head1 = insert_at_head(head1, 12);
  head1 = insert_at_head(head1, 10);
  head1 = insert_at_head(head1, 5);
  head1 = insert_at_head(head1, 1);

  head2 = insert_at_head(head2, 9);
  head2 = insert_at_head(head2, 7);
  head2 = insert_at_head(head2, 2);

  // Merging the linked lists
  head1 = merge_alternate(head1, head2);

  print(head1);
}
}

// This code is contributed by gauravrajput1

```

## C#

```cs

// C# program to implement
// the above approach
using System;
class GFG{

// Structure of a Node
class node 
{
  public int data;
  public node next;
  public node(int d)
  {
    data = d;
    next = null;
  }
};

// Function to insert the node
// at the head of the linkedlist
static node insert_at_head(node head, 
                           int data)
{
  node n = new node(data);
  n.next = head;
  head = n;
  return head;
}

// Function to print the linked list
static void print(node head)
{
  while (head != null) 
  {
    Console.Write(head.data + " ");
    head = head.next;
  }

  Console.WriteLine();
  return;
}

// Function to merge the odd and
// even positioned nodes of two
// given linked lists alternately
static node merge_alternate(node head1, 
                            node head2)
{
  // Traverse from the second
  // node of second linked list
  if (head2 != null)
    head2 = head2.next;

  // Stores the head of
  // the resultant list
  node head3 = null;

  // Stores the current node
  node cur = null;

  // Store the first node of
  // first list in the result
  if (head1 != null)
    head3 = head1;

  // Otherwise
  else
    head3 = head2;

  // Traverse until end of a
  // one of the list is reached
  while (head1 != null && 
         head2 != null) 
  {
    // If there is a previous 
    // node then connect that 
    // with the current node
    if (cur != null)
      cur.next = head1;

    // Update the current node
    cur = head1;

    // If next odd node exists
    if (head1.next != null)

      // Store the next odd node
      head1 = head1.next.next;

    // Otherwise
    else

      // Reach end of list
      head1 = null;

    // Connect the first node
    // with the second node
    cur.next = head2;

    // Update the current node
    cur = head2;

    // If next even node exists
    if (head2.next != null)

      // Store the next even node
      head2 = head2.next.next;

    // Otherwise
    else

      // Reach the end of the list
      head2 = null;
  }

  // If end of the second
  // list has been reached
  while (head1 != null) 
  {
    // Connect with the
    // previous node
    if (cur != null)
      cur.next = head1;

    // Update the current node
    cur = head1;

    // If next odd node exists
    if (head1.next != null)

      // Store the next odd node
      head1 = head1.next.next;

    // Otherwise
    else

      // Reach end of list
      head1 = null;
  }

  // If end of second list
  // has been reached
  while (head2 != null) 
  {
    // Connect with the
    // previous node
    if (cur != null)
      cur.next = head2;

    // Update the current node
    cur = head2;

    // If next even node exists
    if (head2.next != null)

      // Store the next odd node
      head2 = head2.next.next;

    // Otherwise
    else

      // Reach end of list
      head2 = null;
  }

  // End of the resultant list
  if (cur != null)
    cur.next = null;

  // Returning the head of
  // the resultant node
  return head3;
}

// Driver Code
public static void Main(String[] args)
{
  node head1 = null, head2 = null;

  // Create linked list
  head1 = insert_at_head(head1, 6);
  head1 = insert_at_head(head1, 19);
  head1 = insert_at_head(head1, 13);
  head1 = insert_at_head(head1, 12);
  head1 = insert_at_head(head1, 10);
  head1 = insert_at_head(head1, 5);
  head1 = insert_at_head(head1, 1);

  head2 = insert_at_head(head2, 9);
  head2 = insert_at_head(head2, 7);
  head2 = insert_at_head(head2, 2);

  // Merging the linked lists
  head1 = merge_alternate(head1, head2);

  print(head1);
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
1 7 10 13 6

```

***时间复杂度**：`O(n)`*

***辅助空间**：`O(1)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。