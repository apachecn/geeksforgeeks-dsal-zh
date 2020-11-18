# 在单链表

中找到元素K的可能性

给定一个大小为 **N** 的单链接列表和另一个键 **K** ，我们必须找到单链接列表中存在键 **K** 的可能性。
**范例：**

> **输入：**链接列表= 2-> 3-> 3-> 3-> 4-> 2，键= 5
> **输出：** 0
> **说明：**
> 由于列表中不存在Key的值为5，因此在链接列表中找到Key的概率为0。
> **输入：**链接列表= 2-> 3-> 5-> 1-> 9-> 8-> 0-> 7-> 6- > 5，键= 5
> **输出：** 0.2

**方法：**
在单链表中找到关键元素 **K** 的概率如下：

> 概率=元素K的出现次数/链表的大小

在我们的方法中，我们将首先计算单链列表中元素K的数量，然后通过将K的出现次数除以单链列表的大小来计算概率。
以下是上述方法的实现：

## C

```

// C code to find the probability
// of finding an Element
// in a Singly Linked List

#include <stdio.h>
#include <stdlib.h>

// Link list node
struct Node {
    int data;
    struct Node* next;
};

/* Given a reference (pointer to pointer)
   to the head of a list and an int,
   push a new node on the front of the list. */
void push(struct Node** head_ref, int new_data)
{
    // allocate node
    struct Node* new_node
        = (struct Node*)malloc(
            sizeof(struct Node));

    // put in the data
    new_node->data = new_data;

    // link the old list off the new node
    new_node->next = (*head_ref);

    // move the head to point to the new node
    (*head_ref) = new_node;
}

// Counts nnumber of nodes in linked list
int getCount(struct Node* head)
{

    // Initialize count
    int count = 0;

    // Initialize current
    struct Node* current = head;

    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}

float kPresentProbability(
    struct Node* head,
    int n, int k)
{

    // Initialize count
    float count = 0;

    // Initialize current
    struct Node* current = head;

    while (current != NULL) {
        if (current->data == k)
            count++;
        current = current->next;
    }
    return count / n;
}

// Driver Code
int main()
{
    // Start with the empty list
    struct Node* head = NULL;

    // Use push() to construct below list
    // 1->2->1->3->1
    push(&head, 2);
    push(&head, 3);
    push(&head, 5);
    push(&head, 1);
    push(&head, 9);
    push(&head, 8);
    push(&head, 0);
    push(&head, 7);
    push(&head, 6);
    push(&head, 5);

    printf("%.1f",
           kPresentProbability(
               head, getCount(head), 5));

    return 0;
}

```

## 爪哇

```

// Java code to find the probability
// of finding an Element
// in a Singly Linked List
class GFG{

// Link list node
static class Node 
{
  int data;
  Node next;
};

// Given a reference (pointer to 
// pointer) to the head of a list 
// and an int, push a new node 
// on the front of the list.
static Node push(Node head_ref, 
                 int new_data)
{
  // Allocate node
  Node new_node = new Node();

  // Put in the data
  new_node.data = new_data;

  // Link the old list 
  // off the new node
  new_node.next = head_ref;

  // Move the head to 
  // point to the new node
  head_ref = new_node;

  return head_ref;
}

// Counts nnumber of nodes 
// in linked list
static int getCount(Node head)
{
  // Initialize count
  int count = 0;

  // Initialize current
  Node current = head;

  while (current != null) 
  {
    count++;
    current = current.next;
  }
  return count;
}

static float kPresentProbability(Node head,
                                 int n, int k)
{
  // Initialize count
  float count = 0;

  // Initialize current
  Node current = head;

  while (current != null) 
  {
    if (current.data == k)
      count++;
    current = current.next;
  }
  return count / n;
}

// Driver Code
public static void main(String[] args)
{
  // Start with the empty list
  Node head = null;

  // Use push() to conbelow list
  // 1.2.1.3.1
  head = push(head, 2);
  head = push(head, 3);
  head = push(head, 5);
  head = push(head, 1);
  head = push(head, 9);
  head = push(head, 8);
  head = push(head, 0);
  head = push(head, 7);
  head = push(head, 6);
  head = push(head, 5);

  System.out.printf("%.1f", kPresentProbability(
                     head, getCount(head), 5));

}
}

// This code is contributed by shikhasingrajput

```

## Python3

```

# Python3 code to find the probability 
# of finding an Element 
# in a Singly Linked List 

# Node class
class Node:

    def __init__(self, data, next = None):

        self.data = data
        self.next = None

class LinkedList:

    def __init__(self):

        self.head = None

    def push(self, data):

        # Allocate the Node & 
        # put the data
        new_node = Node(data)

        # Make the next of new Node as head
        new_node.next = self.head

        # Move the head to point to new Node
        self.head = new_node

    # Counts the number of nodes in linkedlist
    def getCount(self):

        # Initialize current
        current = self.head

        # Initialize count
        count = 0

        while current is not None:
            count += 1
            current = current.next

        return count

    def kPresentProbability(self, n, k):

        # Initialize current
        current = self.head

        # Initialize count
        count = 0.0

        while current is not None:
            if current.data == k:
                count += 1

            current = current.next

        return count / n

# Driver Code
if __name__ == "__main__":

    # Start with empty list
    llist = LinkedList()

    # Use push to construct the linked list
    llist.push(2)
    llist.push(3)
    llist.push(5)
    llist.push(1)
    llist.push(9)
    llist.push(8)
    llist.push(0)
    llist.push(7)
    llist.push(6)
    llist.push(5)

    print(llist.kPresentProbability(
          llist.getCount(), 5))

# This code is contributed by kevalshah5    

```

## C＃

```

// C# code to find the probability
// of finding an Element
// in a Singly Linked List
using System;
class GFG{

// Link list node
class Node 
{
  public int data;
  public Node next;
};

// Given a reference (pointer to 
// pointer) to the head of a list 
// and an int, push a new node 
// on the front of the list.
static Node push(Node head_ref, 
                 int new_data)
{
  // Allocate node
  Node new_node = new Node();

  // Put in the data
  new_node.data = new_data;

  // Link the old list 
  // off the new node
  new_node.next = head_ref;

  // Move the head to 
  // point to the new node
  head_ref = new_node;

  return head_ref;
}

// Counts nnumber of nodes 
// in linked list
static int getCount(Node head)
{
  // Initialize count
  int count = 0;

  // Initialize current
  Node current = head;

  while (current != null) 
  {
    count++;
    current = current.next;
  }
  return count;
}

static float kPresentProbability(Node head,
                                 int n, int k)
{
  // Initialize count
  float count = 0;

  // Initialize current
  Node current = head;

  while (current != null) 
  {
    if (current.data == k)
      count++;
    current = current.next;
  }
  return count / n;
}

// Driver Code
public static void Main(String[] args)
{
  // Start with the empty list
  Node head = null;

  // Use push() to conbelow list
  // 1.2.1.3.1
  head = push(head, 2);
  head = push(head, 3);
  head = push(head, 5);
  head = push(head, 1);
  head = push(head, 9);
  head = push(head, 8);
  head = push(head, 0);
  head = push(head, 7);
  head = push(head, 6);
  head = push(head, 5);

  Console.Write("{0:F1}", kPresentProbability(
                 head, getCount(head), 5));
}
}

// This code is contributed by Princi Singh

```

**Output**

```
0.2
```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。