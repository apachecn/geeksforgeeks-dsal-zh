# 如何使用递归在给定位置的单链表中插入节点

> 原文:[https://www . geesforgeks . org/如何使用递归在给定位置插入单链表中的节点/](https://www.geeksforgeeks.org/how-to-insert-a-node-in-a-singly-linked-list-at-a-given-position-using-recursion/)

给定一个 [**单链表**](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/) 作为**链表**，一个**位置**，一个**节点**，任务是**使用递归**在给定的**链表**中的一个**给定位置插入**那个元素。

**示例:**

> **输入:**列表= 1->2->3->4->5->6->7，节点= (val=100，next=null)，位置= 4
> **输出:**1->2->3->100->4->5->6->7
> **解释:-最初在第 4 个位置，该值为 4。现在，当在第 4 个位置插入 100 时，从 4 开始的所有值将向右移动 1 个位置。这可以通过以下方式可视化:**
> 
> 1-> 2-> 3->**4**->5->6->7
> 1->2->3->T3】100->4->5->6->7
> 
> **输入:**列表= 1->2->3->100->4->5->6->7，节点= (val=101，next=null)，位置= 1
> T3】输出:10->1->2->3->100->4->5->6-

**解决方案:**

会有 **3 种情况**:

1.  **在链表的第一个位置插入一个节点**
    *   **方法:**遵循以下步骤:
        1.  创建临时节点。
        2.  现在在 head 之前插入临时节点，并将 head 指针更改为指向临时节点。
2.  **在链表的第一个和最后一个节点之间插入一个节点**
    *   **方法:**遵循以下步骤:
        1.  调用递归函数到达所需位置。
        2.  如果位置大于列表的长度，则无法插入。
        3.  如果没有，则在所需位置插入新节点。
3.  **在链表末尾插入一个节点**
    *   **方法:**遵循以下步骤:
        1.  递归移动到链表的末尾。
        2.  在列表末尾插入新节点。

**递推关系:** T(n) = T(n-1) + c

下面是上述方法的实现

## C++

```
// C++ code to insert a node
// at a given position
// in singly linked list
#include <bits/stdc++.h>
#define null nullptr

using namespace std;

// Structure of the node of linked list
struct node {
    int item;
    node* nxt;
    node(int item, node* t)
    {
        this->item = item;
        (*this).nxt = t;
    }
};

// Function to insert a node
// at the first position
node* insertAtFirst(node*& listHead, node* x)
{
    node* temp = listHead;
    x->nxt = temp;
    listHead = temp = x;
    return temp;
}

// Function to insert a node
// at the last position
node* insertAtEnd(node* listHead, node* x)
{
    if (listHead->nxt == null) {
        listHead->nxt = x;
        return listHead;
    }
    listHead->nxt
      = insertAtEnd(listHead->nxt, x);
    return listHead;
}

// Function to insert a node
// in between first and last
node* insertInBetween(node* temp,
                      node* x, int pos)
{
    if (pos == 2) {
        if (temp != null) {
            x->nxt = temp->nxt;
            temp->nxt = x;
        }
        return temp;
    }
    if (temp == null) {
        return temp;
    }
    temp->nxt
      = insertInBetween(temp->nxt, x, --pos);
}

// Printing through recursion
void print(node* head)
{
    if (head == null) {
        return;
    }
    cout << head->item << " ";
    print(head->nxt);
}

// Driver code
int main()
{
    node* head = new node(1, 0);

    // Creating a linked list of length 15
    for (int i = 2; i < 16; i++)
        insertAtEnd(head, new node(i, 0));

    // Insert node with value 100
    // at 4th position
    insertInBetween(head,
                    new node(100, 0), 4);

    // Insert node with value 101
    // at 200th position
    insertInBetween(head,
                    new node(101, 0), 200);

    // Insert node with value 100
    // at 1st position
    insertAtFirst(head, new node(100, 0));

    // Insert node with value 100
    // at the end position
    insertAtEnd(head, new node(100, 0));

    // Printing the new linked list
    print(head);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to insert a node at a given
//position in singly linked list
class GFG{

// Structure of the node of linked list
static class node
{
    int item;
    node nxt;

    node(int item, node t)
    {
        this.item = item;
        this.nxt = t;
    }
};

// Function to insert a node
// at the first position
static node insertAtFirst(node listHead, node x)
{
    x.nxt = listHead;
    listHead = null;
    listHead = x;
    return listHead;
}

// Function to insert a node
// at the last position
static node insertAtEnd(node listHead, node x)
{
    if (listHead.nxt == null)
    {
        listHead.nxt = x;
        return listHead;
    }
    listHead.nxt = insertAtEnd(listHead.nxt, x);
    return listHead;
}

// Function to insert a node
// in between first and last
static node insertInBetween(node temp, node x,
                            int pos)
{
    if (pos == 2)
    {
        if (temp != null)
        {
            x.nxt = temp.nxt;
            temp.nxt = x;
        }
        return temp;
    }
    if (temp == null)
    {
        return temp;
    }
    temp.nxt = insertInBetween(temp.nxt, x, --pos);
    return temp;
}

// Printing through recursion
static void print(node head)
{
    if (head == null)
    {
        return;
    }
    System.out.print(head.item + " ");
    print(head.nxt);
}

// Driver code
public static void main(String[] args)
{
    node head = new node(1, null);

    // Creating a linked list of length 15
    for(int i = 2; i < 16; i++)
        insertAtEnd(head, new node(i, null));

    // Insert node with value 100
    // at 4th position
    head = insertInBetween(head,
                    new node(100, null), 4);

    // Insert node with value 101
    // at 200th position
    head = insertInBetween(head,
                    new node(101, null), 200);

    // Insert node with value 100
    // at 1st position
    head = insertAtFirst(head, new node(100, null));

    // Insert node with value 100
    // at the end position
    head = insertAtEnd(head, new node(100, null));

    // Printing the new linked list
    print(head);
}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# code to insert a node at a given
//position in singly linked list
using System;

public class GFG{

// Structure of the node of linked list
class node
{
    public int item;
    public node nxt;

    public node(int item, node t)
    {
        this.item = item;
        this.nxt = t;
    }
};

// Function to insert a node
// at the first position
static node insertAtFirst(node listHead, node x)
{
    x.nxt = listHead;
    listHead = null;
    listHead = x;
    return listHead;
}

// Function to insert a node
// at the last position
static node insertAtEnd(node listHead, node x)
{
    if (listHead.nxt == null)
    {
        listHead.nxt = x;
        return listHead;
    }
    listHead.nxt = insertAtEnd(listHead.nxt, x);
    return listHead;
}

// Function to insert a node
// in between first and last
static node insertInBetween(node temp, node x,
                            int pos)
{
    if (pos == 2)
    {
        if (temp != null)
        {
            x.nxt = temp.nxt;
            temp.nxt = x;
        }
        return temp;
    }
    if (temp == null)
    {
        return temp;
    }
    temp.nxt = insertInBetween(temp.nxt, x, --pos);
    return temp;
}

// Printing through recursion
static void print(node head)
{
    if (head == null)
    {
        return;
    }
    Console.Write(head.item + " ");
    print(head.nxt);
}

// Driver code
public static void Main(String[] args)
{
    node head = new node(1, null);

    // Creating a linked list of length 15
    for(int i = 2; i < 16; i++)
        insertAtEnd(head, new node(i, null));

    // Insert node with value 100
    // at 4th position
    head = insertInBetween(head,
                    new node(100, null), 4);

    // Insert node with value 101
    // at 200th position
    head = insertInBetween(head,
                    new node(101, null), 200);

    // Insert node with value 100
    // at 1st position
    head = insertAtFirst(head, new node(100, null));

    // Insert node with value 100
    // at the end position
    head = insertAtEnd(head, new node(100, null));

    // Printing the new linked list
    print(head);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript code to insert a node at a given
// position in singly linked list

// Structure of the node of linked list
class node {

    constructor(item, t) {
        this.item = item;
        this.nxt = t;
    }
};

// Function to insert a node
// at the first position
function insertAtFirst(listHead, x) {
    x.nxt = listHead;
    listHead = null;
    listHead = x;
    return listHead;
}

// Function to insert a node
// at the last position
function insertAtEnd(listHead, x) {
    if (listHead.nxt == null) {
        listHead.nxt = x;
        return listHead;
    }
    listHead.nxt = insertAtEnd(listHead.nxt, x);
    return listHead;
}

// Function to insert a node
// in between first and last
function insertInBetween(temp, x, pos) {
    if (pos == 2) {
        if (temp != null) {
            x.nxt = temp.nxt;
            temp.nxt = x;
        }
        return temp;
    }
    if (temp == null) {
        return temp;
    }
    temp.nxt = insertInBetween(temp.nxt, x, --pos);
    return temp;
}

// Printing through recursion
function _print(head) {
    if (head == null) {
        return;
    }
    document.write(head.item + " ");
    _print(head.nxt);
}

// Driver code
let head = new node(1, null);

// Creating a linked list of length 15
for (let i = 2; i < 16; i++)
    insertAtEnd(head, new node(i, null));

// Insert node with value 100
// at 4th position
head = insertInBetween(head,
    new node(100, null), 4);

// Insert node with value 101
// at 200th position
head = insertInBetween(head,
    new node(101, null), 200);

// Insert node with value 100
// at 1st position
head = insertAtFirst(head, new node(100, null));

// Insert node with value 100
// at the end position
head = insertAtEnd(head, new node(100, null));

// Printing the new linked list
_print(head);

    // This code is contributed by Saurabh Jaiswal
</script>
```

**Output**

```
100 1 2 3 100 4 5 6 7 8 9 10 11 12 13 14 15 100 
```

**时间复杂度:** O(N)其中 N 为链表大小
T3】辅助空间: O(N)其中 N 为链表大小