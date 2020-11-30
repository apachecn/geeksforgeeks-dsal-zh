# 展开的链表 | 系列 1（简介）

> 原文：[https://www.geeksforgeeks.org/unrolled-linked-list-set-1-introduction/](https://www.geeksforgeeks.org/unrolled-linked-list-set-1-introduction/)

与数组和链表一样，展开的链表也是线性数据结构，并且是链表的变体。 与简单的链表不同，它在每个节点上存储多个元素。 也就是说，展开的链表不是在节点上存储单个元素，而是在节点上存储元素数组。 展开的链表涵盖了数组和链表的优点，因为与简单链表相比，它通过在每个节点上存储多个元素来减少内存开销，并且还具有与链表一样快速插入和删除的优点。

![unrolledlinkedlist](img/270be18553104bfaa436144075e51947.png)

**优点**：

*   由于缓存行为，在展开的链表中线性搜索要快得多。

*   与普通链表相比，它需要更少的指针/引用存储空间。

*   它比普通链表执行插入，删除和遍历等操作更快（因为搜索更快）。

**缺点**：

*   每个节点的开销都比单链表高。 请参考以下代码中的示例节点。

**简单实现**

下面的程序创建一个简单的展开的链表，其中包含 3 个节点，每个节点中包含可变数量的元素。 它还遍历创建的列表。

## C

```c

// C program to implement unrolled linked list
// and traversing it.
#include<stdio.h>
#include<stdlib.h>
#define maxElements 4

// Unrolled Linked List Node
struct Node
{
    int numElements;
    int array[maxElements];
    struct Node *next;
};

/* Function to traverse am unrolled linked list
   and print all the elements*/
void printUnrolledList(struct Node *n)
{
    while (n != NULL)
    {
        // Print elements in current node
        for (int i=0; i<n->numElements; i++)
            printf("%d ", n->array[i]);

        // Move to next node 
        n = n->next;
    }
}

// Program to create an unrolled linked list
// with 3 Nodes
int main()
{
    struct Node* head = NULL;
    struct Node* second = NULL;
    struct Node* third = NULL;

    // allocate 3 Nodes
    head = (struct Node*)malloc(sizeof(struct Node));
    second = (struct Node*)malloc(sizeof(struct Node));
    third = (struct Node*)malloc(sizeof(struct Node));

    // Let us put some values in second node (Number
    // of values must be less than or equal to
    // maxElement)
    head->numElements = 3;
    head->array[0] = 1;
    head->array[1] = 2;
    head->array[2] = 3;

    // Link first Node with the second Node
    head->next = second;

    // Let us put some values in second node (Number
    // of values must be less than or equal to
    // maxElement)
    second->numElements = 3;
    second->array[0] = 4;
    second->array[1] = 5;
    second->array[2] = 6;

    // Link second Node with the third Node
    second->next = third;

    // Let us put some values in third node (Number
    // of values must be less than or equal to
    // maxElement)
    third->numElements = 3;
    third->array[0] = 7;
    third->array[1] = 8;
    third->array[2] = 9;
    third->next = NULL;

    printUnrolledList(head);

    return 0;
}

```

## C++

```cpp

// C++ program to implement unrolled linked list 
// and traversing it. 
#include <bits/stdc++.h>
using namespace std;
#define maxElements 4 

// Unrolled Linked List Node 
class Node 
{ 
    public:
    int numElements; 
    int array[maxElements]; 
    Node *next; 
}; 

/* Function to traverse am unrolled linked list 
and print all the elements*/
void printUnrolledList(Node *n) 
{ 
    while (n != NULL) 
    { 
        // Print elements in current node 
        for (int i=0; i<n->numElements; i++) 
            cout<<n->array[i]<<" "; 

        // Move to next node 
        n = n->next; 
    } 
} 

// Program to create an unrolled linked list 
// with 3 Nodes 
int main() 
{ 
    Node* head = NULL; 
    Node* second = NULL; 
    Node* third = NULL; 

    // allocate 3 Nodes 
    head = new Node();
    second = new Node();
    third = new Node();

    // Let us put some values in second node (Number 
    // of values must be less than or equal to 
    // maxElement) 
    head->numElements = 3; 
    head->array[0] = 1; 
    head->array[1] = 2; 
    head->array[2] = 3; 

    // Link first Node with the second Node 
    head->next = second; 

    // Let us put some values in second node (Number 
    // of values must be less than or equal to 
    // maxElement) 
    second->numElements = 3; 
    second->array[0] = 4; 
    second->array[1] = 5; 
    second->array[2] = 6; 

    // Link second Node with the third Node 
    second->next = third; 

    // Let us put some values in third node (Number 
    // of values must be less than or equal to 
    // maxElement) 
    third->numElements = 3; 
    third->array[0] = 7; 
    third->array[1] = 8; 
    third->array[2] = 9; 
    third->next = NULL; 

    printUnrolledList(head); 

    return 0; 
} 

// This is code is contributed by rathbhupendra

```

## Java

```java

// Java program to implement unrolled
// linked list and traversing it. 
import java.util.*;

class GFG{

static final int maxElements = 4;

// Unrolled Linked List Node 
static class Node 
{ 
    int numElements; 
    int []array = new int[maxElements]; 
    Node next; 
}; 

// Function to traverse am unrolled 
// linked list  and print all the elements
static void printUnrolledList(Node n) 
{ 
    while (n != null) 
    { 

        // Print elements in current node 
        for(int i = 0; i < n.numElements; i++) 
            System.out.print(n.array[i] + " "); 

        // Move to next node 
        n = n.next; 
    } 
} 

// Program to create an unrolled linked list 
// with 3 Nodes 
public static void main(String[] args) 
{ 
    Node head = null; 
    Node second = null; 
    Node third = null; 

    // Allocate 3 Nodes 
    head = new Node();
    second = new Node();
    third = new Node();

    // Let us put some values in second 
    // node (Number of values must be 
    // less than or equal to maxElement) 
    head.numElements = 3; 
    head.array[0] = 1; 
    head.array[1] = 2; 
    head.array[2] = 3; 

    // Link first Node with the 
    // second Node 
    head.next = second; 

    // Let us put some values in 
    // second node (Number of values
    // must be less than or equal to 
    // maxElement) 
    second.numElements = 3; 
    second.array[0] = 4; 
    second.array[1] = 5; 
    second.array[2] = 6; 

    // Link second Node with the third Node 
    second.next = third; 

    // Let us put some values in third 
    // node (Number of values must be
    // less than or equal to maxElement) 
    third.numElements = 3; 
    third.array[0] = 7; 
    third.array[1] = 8; 
    third.array[2] = 9; 
    third.next = null; 

    printUnrolledList(head); 
} 
} 

// This code is contributed by amal kumar choubey  

```

## C#

```cs

// C# program to implement unrolled
// linked list and traversing it. 
using System;
class GFG{

static readonly int maxElements = 4;

// Unrolled Linked List Node 
class Node 
{ 
  public int numElements; 
  public int []array = new int[maxElements]; 
  public Node next; 
}; 

// Function to traverse am unrolled 
// linked list  and print all the elements
static void printUnrolledList(Node n) 
{ 
  while (n != null) 
  { 
    // Print elements in current node 
    for(int i = 0; i < n.numElements; i++) 
      Console.Write(n.array[i] + " "); 

    // Move to next node 
    n = n.next; 
  } 
} 

// Program to create an unrolled linked list 
// with 3 Nodes 
public static void Main(String[] args) 
{ 
  Node head = null; 
  Node second = null; 
  Node third = null; 

  // Allocate 3 Nodes 
  head = new Node();
  second = new Node();
  third = new Node();

  // Let us put some values in second 
  // node (Number of values must be 
  // less than or equal to maxElement) 
  head.numElements = 3; 
  head.array[0] = 1; 
  head.array[1] = 2; 
  head.array[2] = 3; 

  // Link first Node with the 
  // second Node 
  head.next = second; 

  // Let us put some values in 
  // second node (Number of values
  // must be less than or equal to 
  // maxElement) 
  second.numElements = 3; 
  second.array[0] = 4; 
  second.array[1] = 5; 
  second.array[2] = 6; 

  // Link second Node with the third Node 
  second.next = third; 

  // Let us put some values in third 
  // node (Number of values must be
  // less than or equal to maxElement) 
  third.numElements = 3; 
  third.array[0] = 7; 
  third.array[1] = 8; 
  third.array[2] = 9; 
  third.next = null; 

  printUnrolledList(head); 
} 
} 

// This code is contributed by Rajput-Ji

```

**输出**：

```
1 2 3 4 5 6 7 8 9

```

在本文中，我们介绍了展开列表及其优点。 我们还展示了如何遍历列表。 在下一篇文章中，我们将详细讨论`maxElements/numElements`的插入，删除和值。

[展开的链表中的插入](https://www.geeksforgeeks.org/insertion-unrolled-linked-list/)

本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

