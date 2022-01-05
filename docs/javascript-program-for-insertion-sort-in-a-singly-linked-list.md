# 用于在单链表中插入排序的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-插入程序-单链表排序/](https://www.geeksforgeeks.org/javascript-program-for-insertion-sort-in-a-singly-linked-list/)

我们已经讨论了数组的插入排序。在本文中，我们将讨论链表的插入排序。
下面是一个简单的链表插入排序算法。

```
1) Create an empty sorted (or result) list.
2) Traverse the given list, do following for every node.
......a) Insert current node in sorted way in sorted or result list.
3) Change head of given linked list to head of sorted (or result) list.
```

主要步骤是(2.a)已经在帖子[单链表排序插入](https://www.geeksforgeeks.org/given-a-linked-list-which-is-sorted-how-will-you-insert-in-sorted-way/)
中介绍过了，下面是上述算法的实现:

## java 描述语言

```
<script>
// Javascript program to sort link list
// using insertion sort
var head = null;
var sorted = null;

class node
{
    constructor(val)
    {
        this.val = val;
        this.next = null;
    }
}

function push(val)
{
    // Allocate node
    var newnode = new node(val);

    // Link the old list off the
    // new node
    newnode.next = head;

    // Move the head to point to
    // the new node
    head = newnode;
}

// Function to sort a singly linked list
// using insertion sort
function insertionSort(headref)
{
    // Initialize sorted linked list
    var sorted = null;
    var current = headref;

    // Traverse the given linked list
    // and insert every node to sorted
    while (current != null)
    {
        // Store next for next iteration
        var next = current.next;

        // Insert current in sorted
        // linked list
        sortedInsert(current);

        // Update current
        current = next;
    }
    // Update head_ref to point to
    // sorted linked list
    head = sorted;
}

/* Function to insert a new_node in a Linked List.
   Note that this function expects a pointer to
   head_ref as this can modify the head of the
   input linked list (similar to push()) */
function sortedInsert(newnode)
{
    // Special case for the head end
    if (sorted == null ||
        sorted.val >= newnode.val)
     {
         newnode.next = sorted;
         sorted = newnode;
     }
     else
     {
         var current = sorted;

         /* Locate the node before the point
            of insertion */
         while (current.next != null &&
                current.next.val < newnode.val)
         {
             current = current.next;
         }
         newnode.next = current.next;
         current.next = newnode;
     }
}

// Function to prvar linked list
function printlist(head)
{
    while (head != null)
    {
        document.write(head.val + " ");
        head = head.next;
    }
}

// Driver code
push(5);
push(20);
push(4);
push(3);
push(30);
document.write(
"Linked List before Sorting..<br/>");
printlist(head);
insertionSort(head);
document.write(
"<br/>LinkedList After sorting<br/>");
printlist(sorted);
// This code is contributed by aashish1995
</script>
```

**输出:**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

详情请参考[单链表插入排序](https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)整篇文章！