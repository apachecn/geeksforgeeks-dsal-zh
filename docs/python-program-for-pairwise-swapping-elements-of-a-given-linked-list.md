# 给定链表成对交换元素的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-pair-swapping-给定链表的元素/](https://www.geeksforgeeks.org/python-program-for-pairwise-swapping-elements-of-a-given-linked-list/)

给定一个单链表，编写一个成对交换元素的函数。

```
Input: 1->2->3->4->5->6->NULL 
Output: 2->1->4->3->6->5->NULL

Input: 1->2->3->4->5->NULL 
Output: 2->1->4->3->5->NULL

Input: 1->NULL 
Output: 1->NULL 
```

例如，如果链表是 1->2->3->4->5，那么函数应该将其改为 2->1->4->3->5，如果链表是，那么函数应该将其改为。

**方法(迭代):**
从头节点开始遍历列表。同时用下一个节点的数据遍历每个节点的交换数据。
以下是上述方法的实施:

## 计算机编程语言

```
# Python program to swap the elements of
# linked list pairwise

# Node class
class Node:

    # Constructor to initialize the
    # node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Function to pairwise swap elements
    # of a linked list
    def pairwiseSwap(self):
        temp = self.head

        # There are no nodes in a
        # linked list
        if temp is None:
            return

        # Traverse further only if there
        # are at least two left
        while(temp and temp.next):

            # If both nodes are same,
            # no need to swap data
            if(temp.data != temp.next.data):

                # Swap data of node with its
                # next node's data
                temp.data, temp.next.data = temp.next.data, temp.data

            # Move temp by 2 to the next pair
            temp = temp.next.next

    # Function to insert a new node at the
    # beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Utility function to print the linked
    # LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

# Driver code
llist = LinkedList()
llist.push(5)
llist.push(4)
llist.push(3)
llist.push(2)
llist.push(1)

print "Linked list before calling pairWiseSwap() "
llist.printList()

llist.pairwiseSwap()

print "Linked list after calling pairWiseSwap()"
llist.printList()

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**输出:**

```
Linked list before calling pairWiseSwap()
1 2 3 4 5 
Linked list after calling pairWiseSwap()
2 1 4 3 5 
```

**时间复杂度:** O(n)
更多详情请参考[给定链表](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)两两互换元素的完整文章！