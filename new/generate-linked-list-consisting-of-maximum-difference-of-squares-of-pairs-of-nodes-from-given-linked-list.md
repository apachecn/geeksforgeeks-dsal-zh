# 生成链表，该列表由给定链表

> 原文：[https://www.geeksforgeeks.org/generate-linked-list-consisting-of-maximum-difference-of-squares-of-pairs-of-nodes-from-given-linked-list/](https://www.geeksforgeeks.org/generate-linked-list-consisting-of-maximum-difference-of-squares-of-pairs-of-nodes-from-given-linked-list/)

中节点对的平方的最大差值组成

给定节点数为偶数的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，任务是生成一个新的[链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，使其包含节点值的平方的最大平方差[。 通过将每个节点包括在一对中来降低顺序。](https://www.geeksforgeeks.org/check-whether-number-can-represented-sum-two-squares/)

**示例**：

> **输入**：`1 -> 6 -> 4 -> 3 -> 5 -> 2`
>
> **输出**：`35 -> 21 -> 7`
>
> **说明**：
>
> 6 和 1 的平方差形成值为 35 的第一个节点。
>
> 5 和 2 的平方差​​构成具有值 21 的第二个节点。 
>
> 4 和 3 的平方之差形成具有值 7 的第三个节点。
>
> 因此，形成的链表为`35 -> 21 -> 7`。
> 
> **输入**：`2 -> 4 -> 5 -> 3 -> 7 -> 8 -> 9 -> 10`
>
> **输出**：`96 -> 72 -> 48 -> 10`
>
> **说明**：
>
> 10 和 2 的平方之差形成值为 96 的第一个节点。
>
> 9 和 3 的平方之差形成值为 72 的第二个节点。
>
> 8 和 4 的平方之差形成值为 48 的第三个节点。
>
> 7 和 5 的平方之差形成值为 10 的第四个节点。
>
> 因此，形成的链表为`96 -> 72 -> 48 -> 10`。

**方法**：方法是找到节点的最大值，并始终使最大节点和最小节点之间的**差**。 因此，创建一个[双端队列](https://www.geeksforgeeks.org/deque-set-1-introduction-applications/) 并在其中插入所有节点值，然后[对双端队列](https://www.geeksforgeeks.org/sorting-queue-without-extra-space/)进行排序。 现在，从两端访问最大值和最小值。 步骤如下：

*   创建**双端队列**，并将所有节点值插入双端队列。

*   **对**的双端队列进行排序，以在恒定时间内获得最大的节点值和最小的节点值。

*   创建另一个**链表**，其值**分别与双端队列的后面和前面的平方和**的平方和之差最大。

*   在每次迭代[之后，从双端队列弹出](https://www.geeksforgeeks.org/dequepop_front-dequepop_back-c-stl/)最小值和最大值。

*   完成上述步骤后，打印形成的新链表的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Linked list node
struct Node {
    int data;
    struct Node* next;
};

// Function to push into Linked List
void push(struct Node** head_ref,
          int new_data)
{
    // Allocate node
    struct Node* new_node
        = (struct Node*)malloc(
            sizeof(struct Node));

    // Put in the data
    new_node->data = new_data;
    new_node->next = (*head_ref);

    // Move the head to point
    // to the new node
    (*head_ref) = new_node;
}

// Function to print the Linked List
void print(struct Node* head)
{
    Node* curr = head;

    // Iterate until curr is NULL
    while (curr) {

        // Print the data
        cout << curr->data << " ";

        // Move to next
        curr = curr->next;
    }
}

// Function to create a new Node of
// the Linked List
struct Node* newNode(int x)
{
    struct Node* temp
        = (struct Node*)malloc(
            sizeof(struct Node));

    temp->data = x;
    temp->next = NULL;

    // Return the node created
    return temp;
}

// Function used to re-order list
struct Node* reorder(Node* head)
{
    // Stores the node of LL
    deque<int> v;
    Node* curr = head;

    // Traverse the LL
    while (curr) {
        v.push_back(curr->data);
        curr = curr->next;
    }

    // Sort the deque
    sort(v.begin(), v.end());

    // Node head1 stores the
    // head of the new Linked List
    Node* head1 = NULL;
    Node* prev = NULL;

    // Size of new LL
    int x = v.size() / 2;

    // Loop to make new LL
    while (x--) {
        int a = v.front();
        int b = v.back();

        // Difference of squares of
        // largest and smallest value
        int ans = pow(b, 2) - pow(a, 2);

        // Create node with value ans
        struct Node* temp = newNode(ans);
        if (head1 == NULL) {
            head1 = temp;
            prev = temp;
        }

        // Otherwsie, update prev
        else {
            prev->next = temp;
            prev = temp;
        }

        // Pop the front and back node
        v.pop_back();
        v.pop_front();
    }

    // Return head of the new LL
    return head1;
}

// Driver Code
int main()
{
    struct Node* head = NULL;

    // Given Linked ist
    push(&head, 6);
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    // Function Call
    Node* temp = reorder(head);

    // Print the new LL formed
    print(temp);

    return 0;
}

```

## Java

```java

// Java program for the 
// above approach
import java.util.*;
class GFG{

// Linked list node
static class Node 
{
  int data;
  Node next;
};

static Node head ;

// Function to push 
// into Linked List
static void push(int new_data)
{
  // Allocate node
  Node new_node = new Node();

  // Put in the data
  new_node.data = new_data;
  new_node.next = head;

  // Move the head to point
  // to the new node
  head = new_node;
}

// Function to print the
// Linked List
static void print(Node head)
{
  Node curr = head;

  // Iterate until curr 
  // is null
  while (curr != null) 
  {
    // Print the data
    System.out.print(curr.data + " ");

    // Move to next
    curr = curr.next;
  }
}

// Function to create a 
// new Node of the Linked List
static Node newNode(int x)
{
  Node temp = new Node();
  temp.data = x;
  temp.next = null;

  // Return the node 
  // created
  return temp;
}

// Function used to re-order 
// list
static Node reorder(Node head)
{
  // Stores the node of LL
  Deque<Integer> v =
        new LinkedList<>();
  Node curr = head;

  // Traverse the LL
  while (curr != null) 
  {
    v.add(curr.data);
    curr = curr.next;
  }

  // Sort the deque
  // Collections.sort(v);

  // Node head1 stores the
  // head of the new Linked
  // List
  Node head1 = null;
  Node prev = null;

  // Size of new LL
  int x = v.size() / 2;

  // Loop to make new LL
  while ((x--) > 0) 
  {
    int a = v.peek();
    int b = v.getLast();

    // Difference of squares of
    // largest and smallest value
    int ans = (int)(Math.pow(b, 2) - 
                    Math.pow(a, 2));

    // Create node with value ans
    Node temp = newNode(ans);
    if (head1 == null) 
    {
      head1 = temp;
      prev = temp;
    }

    // Otherwsie, update prev
    else
    {
      prev.next = temp;
      prev = temp;
    }

    // Pop the front and
    // back node
    v.removeFirst();
    v.removeLast();
  }

  // Return head of the 
  // new LL
  return head1;
}

// Driver Code
public static void main(String[] args)
{
  head = null;

  // Given Linked ist
  push(6);
  push(5);
  push(4);
  push(3);
  push(2);
  push(1);

  // Function Call
  Node temp = reorder(head);

  // Print the new 
  // LL formed
  print(temp);
}
}

// This code is contributed by Amit Katiyar

```

## C#

```cs

// C# program for the 
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Linked list node
public class Node 
{
  public int data;
  public Node next;
};

static Node head ;

// Function to push 
// into Linked List
static void push(int new_data)
{
  // Allocate node
  Node new_node = new Node();

  // Put in the data
  new_node.data = new_data;
  new_node.next = head;

  // Move the head to point
  // to the new node
  head = new_node;
}

// Function to print the
// Linked List
static void print(Node head)
{
  Node curr = head;

  // Iterate until curr 
  // is null
  while (curr != null) 
  {
    // Print the data
    Console.Write(curr.data + " ");

    // Move to next
    curr = curr.next;
  }
}

// Function to create a 
// new Node of the Linked List
static Node newNode(int x)
{
  Node temp = new Node();
  temp.data = x;
  temp.next = null;

  // Return the node 
  // created
  return temp;
}

// Function used to re-order 
// list
static Node reorder(Node head)
{
  // Stores the node of LL
  List<int> v =
       new List<int>();     
  Node curr = head;

  // Traverse the LL
  while (curr != null) 
  {
    v.Add(curr.data);
    curr = curr.next;
  }

  // Sort the deque
  // Collections.sort(v);

  // Node head1 stores the
  // head of the new Linked
  // List
  Node head1 = null;
  Node prev = null;

  // Size of new LL
  int x = v.Count / 2;

  // Loop to make new LL
  while ((x--) > 0) 
  {
    int a = v[0];
    int b = v[v.Count-1];

    // Difference of squares of
    // largest and smallest value
    int ans = (int)(Math.Pow(b, 2) - 
                    Math.Pow(a, 2));

    // Create node with value ans
    Node temp = newNode(ans);
    if (head1 == null) 
    {
      head1 = temp;
      prev = temp;
    }

    // Otherwsie, update prev
    else
    {
      prev.next = temp;
      prev = temp;
    }

    // Pop the front and
    // back node
    v.RemoveAt(0);
    v.RemoveAt(v.Count - 1);
  }

  // Return head of the 
  // new LL
  return head1;
}

// Driver Code
public static void Main(String[] args)
{
  head = null;

  // Given Linked ist
  push(6);
  push(5);
  push(4);
  push(3);
  push(2);
  push(1);

  // Function Call
  Node temp = reorder(head);

  // Print the new 
  // LL formed
  print(temp);
}
}

// This code is contributed by gauravrajput1

```

**输出**： 

```
35 21 7

```

**时间复杂度**：`O(N * log N)`

**辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。