# 链表

的迭代选择排序

给定一个链表，任务是使用选择排序以升序对链表进行排序。

**示例：**

```
Input : 1->4->2->2->3
Output : 1->2->2->3->4

Input : 5->4->3->2
Output : 2->3->4->5

```

**选择排序算法**：迭代给定列表N次，其中N是列表中元素的数量。 在选择排序的每次迭代中，都会从未排序的子数组中选取最小元素（考虑升序）并将其移至已排序的子数组。

**范例**：

```
list = 64 25 12 22 11

// Find the minimum element in list(0...4)
// and place it at beginning
11 25 12 22 64

// Find the minimum element in list(1...4)
// and place it at beginning of list(1...4)
11 12 25 22 64

// Find the minimum element in list(2...4)
// and place it at beginning of list(2...4)
11 12 22 25 64

// Find the minimum element in list(3...4)
// and place it at beginning of list(3...4)
11 12 22 25 64 

```

可以通过两种方式完成所需的交换：

1.  通过交换节点的数据部分。
2.  通过交换完整的节点。

当列表的元素是某种记录时，通常使用第二种实现方式，因为在这种情况下，由于存在大量数据元素，数据交换变得乏味且昂贵。

**实现方法1** ：以下是通过仅交换节点的数据部分来对链表进行排序的选择排序功能的实现。

## C ++

```

void selectionSort(node* head) 
{ 
    node* temp = head; 

    // Traverse the List 
    while (temp) { 
        node* min = temp; 
        node* r = temp->next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min->data > r->data) 
                min = r; 

            r = r->next; 
        } 

        // Swap Data 
        int x = temp->data; 
        temp->data = min->data; 
        min->data = x; 
        temp = temp->next; 
    } 
} 

```

## 爪哇

```

void selectionSort(node head) 
{ 
    node temp = head; 

    // Traverse the List 
    while (temp) { 
        node min = temp; 
        node r = temp.next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min.data > r.data) 
                min = r; 

            r = r.next; 
        } 

        // Swap Data 
        int x = temp.data; 
        temp.data = min.data; 
        min.data = x; 
        temp = temp.next; 
    } 
} 

// This code is contributed by shivanisinghss2110 

```

## C＃

```

static void selectionSort(node head) 
{ 
    node temp = head; 

    // Traverse the List 
    while (temp) { 
        node min = temp; 
        node r = temp.next; 

        // Traverse the unsorted sublist 
        while (r) { 
            if (min.data > r.data) 
                min = r; 

            r = r.next; 
        } 

        // Swap Data 
        int x = temp.data; 
        temp.data = min.data; 
        min.data = x; 
        temp = temp.next; 
    } 
} 
// This code contributed by shivanisinghss2110 

```

## Python3

```

def selectionSort(head): 

    temp = head 

    # Traverse the List 
    while (temp): 

        minn = temp 
        r = temp.next

        # Traverse the unsorted sublist 
        while (r): 
            if (minn.data > r.data): 
                minn = r 

            r = r.next

        # Swap Data 
        x = temp.data 
        temp.data = minn.data 
        minn.data = x 
        temp = temp.next

# This code is contributed by shubhamsingh10 

```

**方法2** ：数据交换无疑易于实现和理解，但在某些情况下（如上所述），这是不希望的。 在交换两个节点的下一部分时，需要考虑四种情况：

1.  节点是相邻的，第一个节点是起始节点。
2.  节点相邻，第一个节点不是起始节点。
3.  节点不相邻，第一个节点是起始节点。
4.  节点不相邻，第一个节点也不是起始节点。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <bits/stdc++.h>``using` `namespace` `std;``// Linked List Node``struct` `Node {` `int` `data;` `Node* next;``};``// Utility function to create a``// new Linked List Node``Node* newNode(` `int` `val)``{` `Node* temp =` `new` `Node;` `temp->data = val;`] `temp->next = NULL;` `return` `temp;``}`[`// Function to sort a linked list using selection``// sort algorithm by swapping the next pointers``Node* selectionSort(Node* head)``{` `Node *a, *b, *c, *d, *r;`[H TG368]  `a = b = head;` `// While b is not the last node` `while` `(b->next) {` `c = d = b->next;` `// While d is pointing to a valid node` `while` `(d) {` `if` `(b->data > d->data) {` `// If d appears immediately after b` `if` `(b->next == d) {` `// Case 1: b is the head of the linked list` `if` `(b == head) {` `// Move d before b` `b->next = d->next;` `d->next = b;` `// Swap b and d pointers` `r = b;` `b = d;`[ `d = r;` `c = d;` `// Update the head` `head = b;` `// Skip to the next element` `// as it is already in order` `d = d->next;` `}` `// Case 2: b is not the head of the linked list``{` `// Move d before b` `b->next = d->next;` `d->next = b;` `a->next = d;` `// Swap b and d pointers` `r = b;` `b = d;` `d = r;` `c = d;` `// Skip to the next element` `// as it is already in order` `d = d->next;` `}` `}` `// If b and d have some non-zero` `// number of nodes in between them`] `else` `{` `// Case 3: b is the head of the linked list` `if` `(b == head) {` `// Swap b->next and d->next` `r = b->next;` `b->next = d->next;` `d->next = r;` `c->next = b;` `// Swap b and d pointers` `r = b;` `b = d;` `d = r;` `c = d;` `// Skip to the next element` `// as it is already in order` `// Update the head` `head = b;` `}` `// Case 4: b is not the head of the linked list` `else` `{` `// Swap b->next and d->next` `r = b->next;` `b->next = d->next;` `d->next = r;` `c->next = b;` `a->next = d;` `// Swap b and d pointers` `r = b;`]  `b = d;` `d = r;` `c = d;` `// Skip to the next element` `// as it is already in order` `d = d->next;`]  `}` `}` `}` `else` `{` `// Update c and skip to the next element` `// as it is already in order` `c = d;` `d = d->next;` `}` `}` `a = b;`] `b = b->next;` `}` `return` `head;` ​​`}``// Function to print the list``void` `printList(Node* head)`24] `{` `while` `(head) {` `cout << head->data <<` `" "` `;` `head = head->next;` `}``}``// Driver Code``int` `main()``{` `Node* head = newNode(5);` `head->next = newNode(4);` `head->next->next = newNode(3);` `head = selectionSort(head);` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*