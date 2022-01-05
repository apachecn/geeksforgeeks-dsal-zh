# 为什么链表是在堆内存而不是栈内存上实现的？

> 原文:[https://www . geesforgeks . org/为什么链表是在堆内存而不是堆栈内存上实现的/](https://www.geeksforgeeks.org/why-linked-list-is-implemented-on-heap-memory-rather-than-stack-memory/)

**先决条件:**

[链表数据结构](https://www.geeksforgeeks.org/data-structures/linked-list/)
[栈 vs 堆内存分配](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)

[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)是一种线性数据结构，其中元素不存储在连续的存储位置。链表中的元素使用[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)链接。它是在[堆内存](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)上实现的，而不是在[堆栈内存](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/)上实现的。本文探讨其背后的原因。

**<u>堆栈 vs 堆内存</u>**

计算机的内存分为堆和栈内存段。堆栈内存段相对较小，因此主要用于递归等操作或 goto 语句等控制跳转语句。由于堆栈段的大小很小，它不用于深度递归级别，因为它可能会引发堆栈溢出错误。

另一方面，链表的主要优势是在需要时动态扩展自身，而不用担心内存消耗。这就是为什么堆更适合存储链表对象的原因。

**<u>为什么链表不存储在栈内存中？</u>T3】**

为什么不能用堆栈内存创建链表的问题是由于堆栈上的作用域规则和自动内存管理。链表的基本思想是根据节点的内存地址将节点链接在一起。如果每个节点都是在堆栈上创建的，那么这些节点将在超出范围后被删除，因此，即使用户保留指向其内存地址的指针，也不能认为它们不会被其他内容覆盖。

**链表也可以在堆栈内存上实现**。下面是在堆栈内存中创建链表的 C++实现:

## C++

```
// C++ program to implement
// linked list in stack
#include <iostream>
using namespace std;

// Structure of the linked list
struct Node {
    int data;
    struct Node* next;

    // Constructor
    Node(int x)
    {
        data = x;
        next = NULL;
    }
}* head = NULL;

// Function to print the linked list
void printLinkedList(Node* head)
{
    struct Node* temp = head;

    // Traversing linked list
    while (temp) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Driver code
int main()
{
    // Creation of linked list in stack
    struct Node first = Node(1);
    struct Node second = Node(2);
    struct Node third = Node(3);
    struct Node fourth = Node(4);

    head = &first;

    // 1 -> 2 -> 3 -> 4
    first.next = &second;
    second.next = &third;
    third.next = &fourth;
    fourth.next = NULL;

    // Printing the elements of
    // a linked list
    printLinkedList(head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// linked list in stack

import java.util.*;

class GFG{

// Structure of the linked list
static class Node {
    int data;
    Node next;

    // Constructor
    Node(int x)
    {
        data = x;
        next = null;
    }
};
static Node head = null;

// Function to print the linked list
static void printLinkedList(Node head)
{
    Node temp = head;

    // Traversing linked list
    while (temp!=null) {
        System.out.print(temp.data+ " ");
        temp = temp.next;
    }
}

// Driver code
public static void main(String[] args)
{
    // Creation of linked list in stack
    Node first = new Node(1);
    Node second = new  Node(2);
    Node third = new Node(3);
    Node fourth = new Node(4);

    head = first;

    // 1.2.3.4
    first.next = second;
    second.next = third;
    third.next = fourth;
    fourth.next = null;

    // Printing the elements of
    // a linked list
    printLinkedList(head);

}
}

// This code contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// linked list in stack
using System;
using System.Collections.Generic;

public class GFG{

  // Structure of the linked list
  class Node {
    public int data;
    public Node next;

    // Constructor
    public Node(int x)
    {
      data = x;
      next = null;
    }
  };
  static Node head = null;

  // Function to print the linked list
  static void printList(Node head)
  {
    Node temp = head;

    // Traversing linked list
    while (temp!=null) {
      Console.Write(temp.data+ " ");
      temp = temp.next;
    }
  }

  // Driver code
  public static void Main(String[] args)
  {

    // Creation of linked list in stack
    Node first = new Node(1);
    Node second = new  Node(2);
    Node third = new Node(3);
    Node fourth = new Node(4);

    head = first;

    // 1.2.3.4
    first.next = second;
    second.next = third;
    third.next = fourth;
    fourth.next = null;

    // Printing the elements of
    // a linked list
    printList(head);

  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// linked list in stack

// Structure of the linked list
class Node {

    // Constructor
    constructor(x) {
        this.data = x;
        this.next = null;
    }
}

// Function to print the linked list
function printLinkedList(head) {
    let temp = head;

    // Traversing linked list
    while (temp) {
        document.write(temp.data + " ");
        temp = temp.next;
    }
}

// Driver code

// Creation of linked list in stack
let first = new Node(1);
let second = new Node(2);
let third = new Node(3);
let fourth = new Node(4);

head = first;

// 1 -> 2 -> 3 -> 4
first.next = second;
second.next = third;
third.next = fourth;
fourth.next = null;

// Printing the elements of
// a linked list
printLinkedList(head);

// This code is contributed by gfgking.
</script>
```

**输出:**

> 1 2 3 4

**栈上链表实现不起作用的条件:**

如果我们把创建链表的逻辑写在一个单独的函数中，把打印链表元素的逻辑写在一个单独的函数中，上面的代码就行不通了。下面是它对上述概念的 C++实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Structure of the linked list
struct Node {
    int data;
    struct Node* next;

    Node(int x)
    {
        data = x;
        next = NULL;
    }
}* head = NULL;

// Function to return the head pointer
// of the created linked list
Node* CreateLinkedList()
{
    struct Node first = Node(1);
    struct Node second = Node(2);
    struct Node third = Node(3);
    struct Node fourth = Node(4);

    head = &first;

    // 1->2->3->4
    first.next = &second;
    second.next = &third;
    third.next = &fourth;
    fourth.next = NULL;

    return head;
}

// Function to print the linked list
void printLinkedList(Node* head)
{
    struct Node* temp = head;

    // Traversing linked list
    while (temp) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Driver Code
int main()
{
    struct Node* head = CreateLinkedList();
    printLinkedList(head);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

class GFG{

// Structure of the linked list
static class Node {
    int data;
    Node next;

    Node(int x)
    {
        data = x;
        next = null;
    }
}
static Node head = null;

// Function to return the head pointer
// of the created linked list
static Node CreateLinkedList()
{
    Node first = new Node(1);
    Node second = new Node(2);
    Node third = new Node(3);
    Node fourth = new Node(4);

    head = first;

    // 1.2.3.4
    first.next = second;
    second.next = third;
    third.next = fourth;
    fourth.next = null;

    return head;
}

// Function to print the linked list
static void printLinkedList(Node head)
{
    Node temp = head;

    // Traversing linked list
    while (temp!=null) {
        System.out.print(temp.data+ " ");
        temp = temp.next;
    }
}

// Driver Code
public static void main(String[] args)
{
    Node head = CreateLinkedList();
    printLinkedList(head);
}
}

// This code is contributed by 29AjayKumar
```

**说明:**

上述代码给出的结论为[分段故障](http://www.geeksforgeeks.org/core-dump-segmentation-fault-c-cpp/)。其背后的原因是，在堆栈内存中创建链表的过程中，当函数结束或返回时，堆栈帧弹出，函数创建的所有对象都将消失。请参考[这篇](https://www.geeksforgeeks.org/what-happens-when-we-call-a-function/)文章，了解每当功能结束时堆栈帧弹出的原因。

**<u>为什么链表存储在堆内存中？</u>T3】**

在链表中，当需要存储更多的数据时，我们可以在运行时通过使用 malloc 或 C/ C++中的新函数来分配内存。所以动态内存分配从堆区保留大小，因此，链表存储在堆内存中。
如果需要在堆栈区域存储链表，那么在不使用 malloc 或新函数的情况下实现链表。

下面是 C++程序，展示了如何在堆内存中实现链表而不抛出分段错误:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Structure of the linked list
struct Node {
    int data;
    struct Node* next;
};
struct Node* head = NULL;

// Function to create nodes of
// the linked list
void CreateLinkedList(int new_data)
{
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = head;
    head = new_node;
}

// Function to print the linked list
void printLinkedList()
{
    struct Node* temp;
    temp = head;

    // Traversing linked list
    while (temp != NULL) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Driver Code
int main()
{
    CreateLinkedList(1);
    CreateLinkedList(2);
    CreateLinkedList(3);
    CreateLinkedList(4);
    printLinkedList();
    return 0;
}
```

**输出:**

> 4 3 2 1

**<u>堆栈中的链表 vs 堆内存</u>**

<figure class="table">

| **序列号** | **堆栈内存中的链表** | **堆内存中的链表** |
| one | 堆栈中的链表将访问相对较小的内存，这种内存是不可动态扩展的。 | 堆中的链表可以访问动态扩展的内存。 |
| Two | 在链表中创建并存储在堆栈中的每个节点在超出范围后都会被链接删除。 | 需要为要删除的节点释放内存。 |
| three | 如果需要在堆栈区域存储一个链表，那么在不使用 malloc 或新函数的情况下实现一个链表。 | 如果需要在堆中存储链表，那么使用 malloc 或 new 函数实现链表。 |
| four | 在函数范围结束后，不能访问在堆栈中创建的链表节点。 | 创建并存储在堆内存中的链表节点可以在函数范围结束后访问。 |

</figure>