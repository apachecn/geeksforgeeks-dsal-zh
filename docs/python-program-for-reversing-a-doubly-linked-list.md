# 反向双链表的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-for-reverse-a-double-link-list/](https://www.geeksforgeeks.org/python-program-for-reversing-a-doubly-linked-list/)

给定一个[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，任务是反转给定的双链表。

例如，见下图。

```
(a) Original Doubly Linked List 
```

![](img/ac986bf04212b6c02bcab8a71a5727c1.png)

```
(b) Reversed Doubly Linked List 
```

![](img/f8570d09b2d0146b6381105d1bf628ac.png)

这里有一个简单的方法来反转双向链表。我们所需要做的就是交换所有节点的上一个和下一个指针，改变头(或开始)的上一个，最后改变头指针。

## 计算机编程语言

```
# Program to reverse a doubly linked list
# A node of the doubly linked list
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:

    # Constructor for empty Doubly 
    # Linked List
    def __init__(self):
        self.head = None

    # Function reverse a Doubly Linked List
    def reverse(self):
        temp = None
        current = self.head

        # Swap next and prev for all nodes 
        # of doubly linked list
        while current is not None:
            temp = current.prev
            current.prev = current.next
            current.next = temp
            current = current.prev

        # Before changing head, check for the
        # cases like empty list and list with 
        # only one node
        if temp is not None:
            self.head = temp.prev

    # Given a reference to the head of a list 
    # and an integer,inserts a new node on the 
    # front of list
    def push(self, new_data):

        # 1\. Allocates node
        # 2\. Put the data in it
        new_node = Node(new_data)

        # 3\. Make next of new node as head 
        # and previous as None (already None)
        new_node.next = self.head

        # 4\. change prev of head node to 
        # new_node
        if self.head is not None:
            self.head.prev = new_node

        # 5\. move the head to point to the 
        # new node
        self.head = new_node

    def printList(self, node):
        while(node is not None):
            print node.data,
            node = node.next

# Driver code
dll = DoublyLinkedList()
dll.push(2)
dll.push(4)
dll.push(8)
dll.push(10)

print 
"Original Linked List"
dll.printList(dll.head)

# Reverse doubly linked list
dll.reverse()

print 
"Reversed Linked List"
dll.printList(dll.head)
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**输出:**

```
Original linked list 
10 8 4 2 
The reversed Linked List is 
2 4 8 10
```

**时间复杂度:** O(N)，其中 N 表示双向链表中的节点数。
辅助空间:O(1)

我们也可以交换数据而不是指针来反转双链表。[用于反转数组的方法](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)可以用来交换数据。与指针相比，如果数据项的大小更大，交换数据的成本会更高。
如发现以上代码/算法有不正确的地方，请写评论，或者找到更好的方法解决同样的问题。

**方法二:**

同样的问题也可以用 Stacks 来做。

步骤:

1.  继续在堆栈中推送节点的数据。-> O(n)
2.  不断弹出元素并更新双向链表

## 蟒蛇 3

```
"""
Function to reverse a doubly-linked list
swap next and prev pointers for all the 
nodes change prev of the head node
change head pointer
"""
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
        self.prev = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    """
    Method to reverse a Doubly-Linked List 
    using Stacks
    """
    def reverseUsingStacks(self):
        stack = []
        temp = self.head
        while temp is not None:
            stack.append(temp.data)
            temp = temp.next

        # Add all the elements in the stack 
        # in a sequence to the stack
        temp = self.head
        while temp is not None:
            temp.data = stack.pop()
            temp = temp.next

        # Popped all the elements and the 
        # added in the linked list, 
        # in a reversed order.

    """
    Method to push a new item before 
    the head
    """
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head

        if self.head is not None:
            self.head.prev = new_node

        self.head = new_node

    """
    Method to traverse the doubly-linked 
    list and print every node in the list
    """
    def printList(self, node):
        while(node is not None):
            print(node.data)
            node = node. next

# Driver code
dll = DoublyLinkedList()
dll.push(2)
dll.push(4)
dll.push(8)
dll.push(10)

print(
"original doubly-linked list")
dll.printList(dll.head)

# Reverse a doubly-linked list
dll.reverseUsingStacks()

print("Reversed doubly-linked list")
dll.printList(dll.head)
```

**输出:**

```
Original linked list 
10 8 4 2 
The reversed Linked List is 
2 4 8 10
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

在这个方法中，我们遍历链表一次，并将元素添加到堆栈中，然后再次遍历整个链表来更新所有元素。整体耗时 2n，是 O(n)的时间复杂度。

更多详情请参考[反向双链表](https://www.geeksforgeeks.org/reverse-a-doubly-linked-list/)整篇文章！