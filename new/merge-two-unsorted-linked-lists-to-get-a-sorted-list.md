# 合并两个未排序的链表以得到一个已排序的列表

> 原文：[https://www.geeksforgeeks.org/merge-two-unsorted-linked-lists-to-get-a-sorted-list/](https://www.geeksforgeeks.org/merge-two-unsorted-linked-lists-to-get-a-sorted-list/)

给定两个未排序的[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)，任务是将它们合并以获得一个已排序的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)。

**示例**：

> **输入**：`list1 = 3 -> 1 -> 5, list2 = 6 -> 2 -> 4`
>
> **输出**：`1 -> 2 -> 3 -> 4 -> 5 -> 6`
> 
> **输入**：`list1 = 4 -> 7 -> 5, list2 = 2 -> 1 -> 8 -> 1`
>
> **输出**：`1 -> 1 -> 2 -> 4 -> 5 -> 7 -> 8`

**朴素的方法**：朴素的方法是对给定的链表进行排序，然后[将两个排序的链表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)按升序合并到一个列表中。

为了解决上述问题，朴素的方法是对两个链表进行单独排序，然后将两个链表合并为一个顺序递增的列表。

**高效方法**：为了优化上述方法，我们将两个链表连接起来，然后使用任何排序算法对其进行排序。 步骤如下：

1.  通过遍历第一个列表直到我们到达一个尾节点，然后将尾节点的下一个指向第二个列表的头节点，将两个列表连接起来。 将此连接列表存储在第一个列表中。

2.  对上面合并的链表进行排序。 在这里，我们将使用冒泡排序。 因此，如果`node->next->data`小于`node->data`，则交换两个相邻节点的数据。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Create structure for a node
struct node {
    int data;
    node* next;
};

// Function to print the linked list
void setData(node* head)
{
    node* tmp;

    // Store the head of the linked
    // list into a temporary node*
    // and iterate
    tmp = head;

    while (tmp != NULL) {

        cout << tmp->data
             << " -> ";
        tmp = tmp->next;
    }
}

// Function takes the head of the
// LinkedList and the data as
// argument and if no LinkedList
// exists, it creates one with the
// head pointing to first node.
// If it exists already, it appends
// given node at end of the last node
node* getData(node* head, int num)
{

    // Create a new node
    node* temp = new node;
    node* tail = head;

    // Insert data into the temporary
    // node and point it's next to NULL
    temp->data = num;
    temp->next = NULL;

    // Check if head is null, create a
    // linked list with temp as head
    // and tail of the list
    if (head == NULL) {
        head = temp;
        tail = temp;
    }

    // Else insert the temporary node
    // after the tail of the existing
    // node and make the temporary node
    // as the tail of the linked list
    else {

        while (tail != NULL) {

            if (tail->next == NULL) {
                tail->next = temp;
                tail = tail->next;
            }
            tail = tail->next;
        }
    }

    // Return the list
    return head;
}

// Function to concatenate the two lists
node* mergelists(node** head1,
                 node** head2)
{

    node* tail = *head1;

    // Iterate through the head1 to find the
    // last node join the next of last node
    // of head1 to the 1st node of head2
    while (tail != NULL) {

        if (tail->next == NULL
            && head2 != NULL) {
            tail->next = *head2;
            break;
        }
        tail = tail->next;
    }

    // return the concatenated lists as a
    // single list - head1
    return *head1;
}

// Sort the linked list using bubble sort
void sortlist(node** head1)
{
    node* curr = *head1;
    node* temp = *head1;

    // Compares two adjacent elements
    // and swaps if the first element
    // is greater than the other one.
    while (curr->next != NULL) {

        temp = curr->next;
        while (temp != NULL) {

            if (temp->data < curr->data) {
                int t = temp->data;
                temp->data = curr->data;
                curr->data = t;
            }
            temp = temp->next;
        }
        curr = curr->next;
    }
}

// Driver Code
int main()
{
    node* head1 = new node;
    node* head2 = new node;

    head1 = NULL;
    head2 = NULL;

    // Given Linked List 1
    head1 = getData(head1, 4);
    head1 = getData(head1, 7);
    head1 = getData(head1, 5);

    // Given Linked List 2
    head2 = getData(head2, 2);
    head2 = getData(head2, 1);
    head2 = getData(head2, 8);
    head2 = getData(head2, 1);

    // Merge the two lists
    // in a single list
    head1 = mergelists(&head1,
                       &head2);

    // Sort the unsorted merged list
    sortlist(&head1);

    // Print the final
    // sorted merged list
    setData(head1);
    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
class GFG{

static node head1 = null;
static node head2 = null;

// Create structure for a node
static class node
{
  int data;
  node next;
};

// Function to print 
// the linked list
static void setData(node head)
{
  node tmp;

  // Store the head of the linked
  // list into a temporary node
  // and iterate
  tmp = head;

  while (tmp != null) 
  {
    System.out.print(tmp.data + " -> ");
    tmp = tmp.next;
  }
}

// Function takes the head of the
// LinkedList and the data as
// argument and if no LinkedList
// exists, it creates one with the
// head pointing to first node.
// If it exists already, it appends
// given node at end of the last node
static node getData(node head, int num)
{
  // Create a new node
  node temp = new node();
  node tail = head;

  // Insert data into the temporary
  // node and point it's next to null
  temp.data = num;
  temp.next = null;

  // Check if head is null, create a
  // linked list with temp as head
  // and tail of the list
  if (head == null) 
  {
    head = temp;
    tail = temp;
  }

  // Else insert the temporary node
  // after the tail of the existing
  // node and make the temporary node
  // as the tail of the linked list
  else
  {
    while (tail != null) 
    {
      if (tail.next == null) 
      {
        tail.next = temp;
        tail = tail.next;
      }
      tail = tail.next;
    }
  }

  // Return the list
  return head;
}

// Function to concatenate 
// the two lists
static node mergelists()
{
  node tail = head1;

  // Iterate through the 
  // head1 to find the
  // last node join the 
  // next of last node
  // of head1 to the 
  // 1st node of head2
  while (tail != null) 
  {
    if (tail.next == null && 
        head2 != null) 
    {
      tail.next = head2;
      break;
    }
    tail = tail.next;
  }

  // return the concatenated 
  // lists as a single list - head1
  return head1;
}

// Sort the linked list 
// using bubble sort
static void sortlist()
{
  node curr = head1;
  node temp = head1;

  // Compares two adjacent elements
  // and swaps if the first element
  // is greater than the other one.
  while (curr.next != null) 
  {
    temp = curr.next;
    while (temp != null) 
    {
      if (temp.data < curr.data) 
      {
        int t = temp.data;
        temp.data = curr.data;
        curr.data = t;
      }
      temp = temp.next;
    }
    curr = curr.next;
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given Linked List 1
  head1 = getData(head1, 4);
  head1 = getData(head1, 7);
  head1 = getData(head1, 5);

  // Given Linked List 2
  head2 = getData(head2, 2);
  head2 = getData(head2, 1);
  head2 = getData(head2, 8);
  head2 = getData(head2, 1);

  // Merge the two lists
  // in a single list
  head1 = mergelists();

  // Sort the unsorted merged list
  sortlist();

  // Print the final
  // sorted merged list
  setData(head1);
}
}

// This code is contributed by shikhasingrajput

```

## C#

```cs

// C# program for 
// the above approach
using System;

class GFG{

static node head1 = null;
static node head2 = null;

// Create structure for a node
class node
{
    public int data;
    public node next;
};

// Function to print 
// the linked list
static void setData(node head)
{
    node tmp;

    // Store the head of the linked
    // list into a temporary node
    // and iterate
    tmp = head;

    while (tmp != null) 
    {
        Console.Write(tmp.data + " -> ");
        tmp = tmp.next;
    }
}

// Function takes the head of
//the List and the data as
// argument and if no List
// exists, it creates one with the
// head pointing to first node.
// If it exists already, it appends
// given node at end of the last node
static node getData(node head, int num)
{

    // Create a new node
    node temp = new node();
    node tail = head;

    // Insert data into the temporary
    // node and point it's next to null
    temp.data = num;
    temp.next = null;

    // Check if head is null, create a
    // linked list with temp as head
    // and tail of the list
    if (head == null) 
    {
        head = temp;
        tail = temp;
    }

    // Else insert the temporary node
    // after the tail of the existing
    // node and make the temporary node
    // as the tail of the linked list
    else
    {
        while (tail != null) 
        {
            if (tail.next == null) 
            {
                tail.next = temp;
                tail = tail.next;
            }
            tail = tail.next;
        }
    }

    // Return the list
    return head;
}

// Function to concatenate 
// the two lists
static node mergelists()
{
    node tail = head1;

    // Iterate through the 
    // head1 to find the
    // last node join the 
    // next of last node
    // of head1 to the 
    // 1st node of head2
    while (tail != null) 
    {
        if (tail.next == null && 
                head2 != null) 
        {
            tail.next = head2;
            break;
        }
        tail = tail.next;
    }

    // return the concatenated 
    // lists as a single list - head1
    return head1;
}

// Sort the linked list 
// using bubble sort
static void sortlist()
{
    node curr = head1;
    node temp = head1;

    // Compares two adjacent elements
    // and swaps if the first element
    // is greater than the other one.
    while (curr.next != null) 
    {
        temp = curr.next;
        while (temp != null) 
        {
            if (temp.data < curr.data) 
            {
                int t = temp.data;
                temp.data = curr.data;
                curr.data = t;
            }
            temp = temp.next;
        }
        curr = curr.next;
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given Linked List 1
    head1 = getData(head1, 4);
    head1 = getData(head1, 7);
    head1 = getData(head1, 5);

    // Given Linked List 2
    head2 = getData(head2, 2);
    head2 = getData(head2, 1);
    head2 = getData(head2, 8);
    head2 = getData(head2, 1);

    // Merge the two lists
    // in a single list
    head1 = mergelists();

    // Sort the unsorted merged list
    sortlist();

    // Print the final
    // sorted merged list
    setData(head1);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
1 -> 1 -> 2 -> 4 -> 5 -> 7 -> 8

```

**时间复杂度**：`O(M * N)`其中`M`和`N`是两个给定链表的长度。

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。