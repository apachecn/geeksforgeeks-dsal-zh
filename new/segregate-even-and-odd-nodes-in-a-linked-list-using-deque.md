# 使用双端队列

> 原文：[https://www.geeksforgeeks.org/segregate-even-and-odd-nodes-in-a-linked-list-using-deque/](https://www.geeksforgeeks.org/segregate-even-and-odd-nodes-in-a-linked-list-using-deque/)

隔离链表中的偶数和奇数节点

给定一个整数链表。 任务是编写一个程序来修改链表，以使所有偶数出现在修改后的链表中的所有奇数之前。 不需要保持偶数和奇数节点的顺序与原始列表的顺序相同，任务只是重新排列节点，以使所有偶数节点出现在奇数节点之前。

**另请参见**：[隔离链表中的偶数和奇数节点](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)

**示例**：

> **输入**：`1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> NULL`
>
> **输出**：`10 -> 8 -> 6 -> 4 -> 2 -> 1 -> 3 -> 5 -> 7 -> 9 -> NULL`
>
> **输入**：`4 -> 3 -> 2 -> 1 -> NULL`
>
> **输出**：`2 -> 4 -> 3 -> 1 -> NULL`

这个想法是按照以下条件迭代地将链表的所有元素推入双端队列：

*   开始遍历链表，如果元素是偶数，则将其推到双端队列的前面，然后，

*   如果元素是奇数，则将其推到双端队列的后面。

最后，从第一个元素开始，用双端队列元素替换链表中的所有元素。

以下是上述方法的实现：

## C++

```cpp

// CPP program to segregate even and
// odd noeds in a linked list using deque
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
    int data;
    struct Node* next;
};

/*UTILITY FUNCTIONS*/
/* Push a node to linked list. Note that this function
changes the head */
void push(struct Node** head_ref, char new_data)
{
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    /* put in the data */
    new_node->data = new_data;

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to pochar to the new node */
    (*head_ref) = new_node;
}

// printing the linked list
void printList(struct Node* head)
{
    struct Node* temp = head;
    while (temp != NULL) {
                printf("%d ", temp->data);
        temp = temp->next;
    }
}

// Function to rearrange even and odd
// elements in a linked list using deque
void evenOdd(struct Node* head)
{
    struct Node* temp = head;

    // Declaring a Deque
    deque<int> d; 

    // Push all the elements of
    // linked list in to deque
    while (temp != NULL) {

        // if element is even push it
        // to front of the deque
        if (temp->data % 2 == 0) 
            d.push_front(temp->data);

        else // else push at the back of the deque
            d.push_back(temp->data);
        temp = temp->next; // increase temp
    }

    temp = head;

    // Replace all elements of the linked list
    // with the elements of Deque starting from 
    // the first element
    while (!d.empty()) {
        temp->data = d.front();
        d.pop_front();
        temp = temp->next; 
    }
}

// Driver code
int main()
{
    struct Node* head = NULL;
    push(&head, 10);
    push(&head, 9);
    push(&head, 8);
    push(&head, 7);
    push(&head, 6);
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    cout << "Given linked list: ";
        printList(head);

    evenOdd(head);

    cout << "\nAfter rearrangement: ";
        printList(head);

    return 0;
}

```

## Java

```java

// JAVA program to segregate 
// even and odd noeds in a 
// linked list using deque 
import java.util.*;
class GFG{ 

// Link list node 
static class Node 
{  
  int data; 
  Node next; 
}; 

// UTILITY FUNCTIONS
// Push a node to linked list. 
// Note that this function 
// changes the head 
static Node push(Node head_ref, 
                 int new_data) 
{ 
  // allocate node
  Node new_node = new Node(); 

  // put in the data 
  new_node.data = new_data; 

  // link the old list off 
  // the new node 
  new_node.next = head_ref; 

  // move the head to pochar 
  // to the new node 
  head_ref = new_node; 
  return head_ref;
} 

// Printing the linked list 
static void printList(Node head) 
{ 
  Node temp = head; 
  while (temp != null) 
  { 
    System.out.printf("%d ", 
                      temp.data); 
    temp = temp.next; 
  } 
} 

// Function to rearrange even 
// and odd elements in a linked 
// list using deque 
static void evenOdd(Node head) 
{ 
  Node temp = head; 

  // Declaring a Deque 
  Deque<Integer> d = 
        new LinkedList<>(); 

  // Push all the elements of 
  // linked list in to deque 
  while (temp != null) 
  {
    // if element is even push it 
    // to front of the deque 
    if (temp.data % 2 == 0) 
      d.addFirst(temp.data); 

    else

      // else push at the 
      // back of the deque 
      d.add(temp.data);

    // increase temp 
    temp = temp.next; 
  } 

  temp = head; 

  // Replace all elements of 
  // the linked list with the 
  // elements of Deque starting 
  // from the first element 
  while (!d.isEmpty()) 
  { 
    temp.data = d.peek(); 
    d.pollFirst(); 
    temp = temp.next; 
  } 
} 

// Driver code 
public static void main(String[] args) 
{ 
  Node head = null; 
  head = push(head, 10); 
  head = push(head, 9); 
  head = push(head, 8); 
  head = push(head, 7); 
  head = push(head, 6); 
  head = push(head, 5); 
  head = push(head, 4); 
  head = push(head, 3); 
  head = push(head, 2); 
  head = push(head, 1); 

  System.out.print("Given linked list: "); 
  printList(head); 

  evenOdd(head); 

  System.out.print("\nAfter rearrangement: "); 
  printList(head);         
}
} 

// This code is contributed by shikhasingrajput

```

## Python

```py

# Python program to segregate even and
# odd noeds in a linked list using deque
import collections

# Node class 
class Node: 

    # Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None

# UTILITY FUNCTIONS
# Push a node to linked list. Note that this function
# changes the head 
def push( head_ref, new_data):

    # allocate node 
    new_node = Node(0)

    # put in the data 
    new_node.data = new_data

    # link the old list off the new node 
    new_node.next = (head_ref)

    # move the head to pochar to the new node 
    (head_ref) = new_node

    return head_ref

# printing the linked list
def printList( head):

    temp = head
    while (temp != None): 
        print( temp.data, end = " ")
        temp = temp.next

# Function to rearrange even and odd
# elements in a linked list using deque
def evenOdd( head):

    temp = head

    # Declaring a Deque
    d = collections.deque([]) 

    # Push all the elements of
    # linked list in to deque
    while (temp != None) :

        # if element is even push it
        # to front of the deque
        if (temp.data % 2 == 0): 
            d.appendleft(temp.data)

        else: # else push at the back of the deque
            d.append(temp.data)
        temp = temp.next # increase temp

    temp = head

    # Replace all elements of the linked list
    # with the elements of Deque starting from 
    # the first element
    while (len(d) > 0) :
        temp.data = d[0]
        d.popleft()
        temp = temp.next

# Driver code

head = None
head = push(head, 10)
head = push(head, 9)
head = push(head, 8)
head = push(head, 7)
head = push(head, 6)
head = push(head, 5)
head = push(head, 4)
head = push(head, 3)
head = push(head, 2)
head = push(head, 1)

print( "Given linked list: ", end = "")
printList(head)

evenOdd(head)

print("\nAfter rearrangement: ", end = "")
printList(head)

# This code is contributed by Arnab Kundu

```

## C#

```cs

// C# program to segregate 
// even and odd noeds in a 
// linked list using deque 
using System;
using System.Collections.Generic;
class GFG{ 

// Link list node 
public class Node 
{  
  public int data; 
  public Node next; 
}; 

// UTILITY FUNCTIONS
// Push a node to linked list. 
// Note that this function 
// changes the head 
static Node push(Node head_ref, 
                 int new_data) 
{ 
  // allocate node
  Node new_node = new Node(); 

  // put in the data 
  new_node.data = new_data; 

  // link the old list off 
  // the new node 
  new_node.next = head_ref; 

  // move the head to pochar 
  // to the new node 
  head_ref = new_node; 
  return head_ref;
} 

// Printing the linked list 
static void printList(Node head) 
{ 
  Node temp = head; 
  while (temp != null) 
  { 
    Console.Write(" " + temp.data); 
    temp = temp.next; 
  } 
} 

// Function to rearrange even 
// and odd elements in a linked 
// list using deque 
static void evenOdd(Node head) 
{ 
  Node temp = head; 

  // Declaring a Deque 
  List<int> d = 
       new List<int>(); 

  // Push all the elements of 
  // linked list in to deque 
  while (temp != null) 
  {
    // if element is even push it 
    // to front of the deque 
    if (temp.data % 2 == 0) 
      d.Insert(0, temp.data); 

    else

      // else push at the 
      // back of the deque 
      d.Add(temp.data);

    // increase temp 
    temp = temp.next; 
  } 

  temp = head; 

  // Replace all elements of 
  // the linked list with the 
  // elements of Deque starting 
  // from the first element 
  while (d.Count != 0) 
  { 
    temp.data = d[0]; 
    d.RemoveAt(0);
    temp = temp.next; 
  } 
} 

// Driver code 
public static void Main(String[] args) 
{ 
  Node head = null; 
  head = push(head, 10); 
  head = push(head, 9); 
  head = push(head, 8); 
  head = push(head, 7); 
  head = push(head, 6); 
  head = push(head, 5); 
  head = push(head, 4); 
  head = push(head, 3); 
  head = push(head, 2); 
  head = push(head, 1); 

  Console.Write("Given linked list: "); 
  printList(head); 

  evenOdd(head); 

  Console.Write("\nAfter rearrangement: "); 
  printList(head);         
}
} 

// This code is contributed by 29AjayKumar

```

**Output:** 

```
Given linked list: 1 2 3 4 5 6 7 8 9 10 
After rearrangement: 10 8 6 4 2 1 3 5 7 9

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`，其中`N`是链​​表中节点的总数。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。