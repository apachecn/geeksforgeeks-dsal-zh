# 单链表插入排序的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-插入程序-单链表排序/](https://www.geeksforgeeks.org/python-program-for-insertion-sort-in-a-singly-linked-list/)

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

## 计算机编程语言

```
# Python implementation of above 
# algorithm
# Node class 
class Node: 

    # Constructor to initialize the 
    # node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to sort a singly 
# linked list using insertion 
# sort
def insertionSort(head_ref):

    # Initialize sorted linked list
    sorted = None

    # Traverse the given linked list 
    # and insert every node to sorted
    current = head_ref
    while (current != None):

        # Store next for next iteration
        next = current.next

        # Insert current in sorted 
        # linked list
        sorted = sortedInsert(sorted, 
                              current)
        # Update current
        current = next

    # Update head_ref to point to 
    # sorted linked list
    head_ref = sorted
    return head_ref

# Function to insert a new_node in a list. 
# Note that this function expects a pointer 
# to head_ref as this can modify the head 
# of the input linked list (similar to push())
def sortedInsert(head_ref, new_node):
    current = None

    # Special case for the head end 
    if (head_ref == None or 
       (head_ref).data >= new_node.data):    
        new_node.next = head_ref
        head_ref = new_node

    else:

        # Locate the node before the point 
        # of insertion 
        current = head_ref
        while (current.next != None and
               current.next.data < new_node.data):        
            current = current.next

        new_node.next = current.next
        current.next = new_node

    return head_ref

# Utility Functions
# Function to print linked list
def printList(head):
    temp = head
    while(temp != None):    
        print( temp.data, end = " ")
        temp = temp.next

# A utility function to insert a node
# at the beginning of linked list 
def push( head_ref, new_data):

    # Allocate node
    new_node = Node(0)

    # Put in the data 
    new_node.data = new_data

    # Link the old list off the 
    # new node 
    new_node.next = (head_ref)

    # Move the head to point to 
    # the new node 
    (head_ref) = new_node
    return head_ref

# Driver code
a = None
a = push(a, 5)
a = push(a, 20)
a = push(a, 4)
a = push(a, 3)
a = push(a, 30)

print("Linked List before sorting ")
printList(a)

a = insertionSort(a)

print("Linked List after sorting ")
printList(a)
# This code is contributed by Arnab Kundu
```

**输出:**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

详情请参考[单链表插入排序](https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)整篇文章！