# 在链接列表

中找到第一个重复元素

给定一个链表。 从左边找到第一个出现多次的元素。 如果所有元素都是唯一的，则打印-1。

**范例：**

> **输入：** 1 2 3 4 3 2 1
> **输出：** 1
> 在此链接列表中，元素 1 出现两次
> ，它是第一个元素 满足条件。
> 答案为 1。
> **输入：** 1 2、3、4、5
> **输出：** -1
> 所有元素都是唯一的 。 因此，答案是-1。

**方法：**

*   使用地图计算链接列表中所有元素的出现频率。

*   现在，再次遍历链表，从左侧查找第一个元素，其频率大于 1。

*   如果不存在这样的元素，则打印-1。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// A linked list node
class Node {
public:
    int data;
    Node* next;
};

// Given a reference (pointer to pointer)
// to the head of a list and an int,
// appends a new node at the end
void append(Node** head_ref, int new_data)
{
    // allocate node
    Node* new_node = new Node();

    Node* last = *head_ref;

    // put in the data
    new_node->data = new_data;

    // This new node is going to be
    // the last node, so make next of
    // it as NULL
    new_node->next = NULL;

    // If the Linked List is empty,
    // then make the new node as head
    if (*head_ref == NULL) {
        *head_ref = new_node;
        return;
    }

    // Else traverse till the last node
    while (last->next != NULL)
        last = last->next;

    // Change the next of last node
    last->next = new_node;
    return;
}

int getFirstDuplicate(Node* node)
{

    // Unordered map to store the
    // frequency of elements
    unordered_map<int, int> mp;
    Node* head = node;

    // update frequency of all the elements
    while (node != NULL) {
        mp[node->data]++;
        node = node->next;
    }

    node = head;

    // the first node from the left which
    // appears more than once is the answer

    while (node != NULL) {
        if (mp[node->data] > 1)
            return node->data;
        node = node->next;
    }

    // all the nodes are unique
    return -1;
}

// driver code
int main()
{
    // Start with the empty list
    Node* head = NULL;

    // Insert element
    append(&head, 6);
    append(&head, 2);
    append(&head, 1);
    append(&head, 6);
    append(&head, 2);
    append(&head, 1);

    cout << getFirstDuplicate(head);

    return 0;
}

```

## Java

```java

// Java implementation of 
// the above approach
import java.util.*;
class GFG{

// A linked list node
static class Node 
{
  int data;
  Node next;
};
static Node head_ref;

// Given a reference (pointer to 
// pointer) to the head of a list 
// and an int, appends a new node 
// at the end
static void append(int new_data)
{
  // allocate node
  Node new_node = new Node();

  Node last = head_ref;

  // put in the data
  new_node.data = new_data;

  // This new node is going 
  // to be the last node, 
  // so make next of it as 
  // null
  new_node.next = null;

  // If the Linked List is 
  // empty, then make the 
  // new node as head
  if (head_ref == null) 
  {
    head_ref = new_node;
    return;
  }

  // Else traverse till the
  // last node
  while (last.next != null)
    last = last.next;

  // Change the next of 
  // last node
  last.next = new_node;
  return;
}

static int getFirstDuplicate(Node node)
{
  // Unordered map to store the
  // frequency of elements
  HashMap<Integer,
          Integer> mp = new HashMap<Integer,
                                    Integer>();
  Node head = node;

  // update frequency of all 
  // the elements
  while (node != null)
  {
    if(mp.containsKey(node.data))
      mp.put(node.data, 
             mp.get(node.data) + 1);
    else
      mp.put(node.data, 1);

    node = node.next;
  }

  node = head;

  // the first node from the 
  // left which appears more 
  // than once is the answer
  while (node != null) 
  {
    if (mp.get(node.data) > 1)
      return node.data;
    node = node.next;
  }

  // all the nodes are unique
  return -1;
}

// Driver code
public static void main(String[] args)
{
  // Start with the empty list
  head_ref = null;

  // Insert element
  append(6);
  append(2);
  append(1);
  append(6);
  append(2);
  append(1);

  System.out.print(
         getFirstDuplicate(head_ref));
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 implementation of above approach

# Link list node 
class Node :
    def __init__(self):
        self.data = 0
        self.next = None

# Given a reference (pointer to pointer)
# to the head of a list and an int,
# appends a node at the end
def append(head_ref, new_data):

    # allocate node
    new_node = Node()

    last = head_ref

    # put in the data
    new_node.data = new_data

    # This node is going to be
    # the last node, so make next of
    # it as None
    new_node.next = None

    # If the Linked List is empty,
    # then make the node as head
    if (head_ref == None) :
        head_ref = new_node
        return head_ref

    # Else traverse till the last node
    while (last.next != None):
        last = last.next

    # Change the next of last node
    last.next = new_node
    return head_ref

def getFirstDuplicate(node):

    # Unordered map to store the
    # frequency of elements
    mp = dict()
    head = node

    # update frequency of all the elements
    while (node != None) :
        mp[node.data] = mp.get(node.data, 0) + 1
        node = node.next

    node = head

    # the first node from the left which
    # appears more than once is the answer
    while (node != None) :
        if (mp[node.data] > 1):
            return node.data
        node = node.next

    # all the nodes are unique
    return -1

# Driver code

# Start with the empty list
head = None

# Insert element
head = append(head, 6)
head = append(head, 2)
head = append(head, 1)
head = append(head, 6)
head = append(head, 2)
head = append(head, 1)

print(getFirstDuplicate(head))

# This code is contributed by Arnab Kundu

```

## C#

```cs

// C# implementation of 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// A linked list node
public class Node 
{
  public int data;
  public Node next;
};

static Node head_ref;

// Given a reference (pointer to 
// pointer) to the head of a list 
// and an int, appends a new node 
// at the end
static void append(int new_data)
{
  // allocate node
  Node new_node = new Node();

  Node last = head_ref;

  // put in the data
  new_node.data = new_data;

  // This new node is going 
  // to be the last node, 
  // so make next of it as 
  // null
  new_node.next = null;

  // If the Linked List is 
  // empty, then make the 
  // new node as head
  if (head_ref == null) 
  {
    head_ref = new_node;
    return;
  }

  // Else traverse till the
  // last node
  while (last.next != null)
    last = last.next;

  // Change the next of 
  // last node
  last.next = new_node;
  return;
}

static int getFirstDuplicate(Node node)
{
  // Unordered map to store the
  // frequency of elements
  Dictionary<int,
             int> mp = 
             new Dictionary<int,
                            int>();
  Node head = node;

  // update frequency of all 
  // the elements
  while (node != null)
  {
    if(mp.ContainsKey(node.data))
      mp[node.data]++;

    else
      mp.Add(node.data, 1);

    node = node.next;
  }

  node = head;

  // the first node from the 
  // left which appears more 
  // than once is the answer
  while (node != null) 
  {
    if (mp[node.data] > 1)
      return node.data;
    node = node.next;
  }

  // all the nodes are 
  // unique
  return -1;
}

// Driver code
public static void Main(String[] args)
{
  // Start with the empty list
  head_ref = null;

  // Insert element
  append(6);
  append(2);
  append(1);
  append(6);
  append(2);
  append(1);

  Console.Write(
  getFirstDuplicate(head_ref));
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
6

```

**时间复杂度：** O（N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。