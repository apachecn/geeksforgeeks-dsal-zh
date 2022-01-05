# Python 程序在交替位置将一个链表合并到另一个链表中

> 原文:[https://www . geesforgeks . org/python-program-to-merge-a-link-list-in-other-link-list-at-alternate-position/](https://www.geeksforgeeks.org/python-program-to-merge-a-linked-list-into-another-linked-list-at-alternate-positions/)

给定两个链表，在第一个链表的交替位置将第二个链表的节点插入第一个链表。
例如，如果第一个列表是 5- > 7- > 17- > 13- > 11，第二个是 12- > 10- > 2- > 4- > 6，则第一个列表应该变成 5->12->7->10->17->2->13->4->11->仅当有位置可用时，才应插入第二个列表的节点。例如，如果第一个列表是 1- > 2- > 3，第二个列表是 4- > 5- > 6- > 7- > 8，那么第一个列表应该变成 1->4->2->5->3->6，第二个列表变成 7- > 8。
不允许使用额外的空间(不允许创建额外的节点)，即必须就地插入。预期的时间复杂度是 O(n)，其中 n 是第一个列表中的节点数。

想法是在第一个循环中有可用位置时运行一个循环，并通过更改指针来插入第二个列表的节点。下面是这种方法的实现。

## 蟒蛇 3

```
# Python program to merge a linked list 
# into another at alternate positions
class Node(object):
    def __init__(self, data:int):
        self.data = data
        self.next = None

class LinkedList(object):
    def __init__(self):
        self.head = None

    def push(self, new_data:int):
        new_node = Node(new_data)
        new_node.next = self.head

        # 4\. Move the head to point to 
        # new Node
        self.head = new_node

    # Function to print linked list from 
    # the Head
    def printList(self):
        temp = self.head
        while temp != None:
            print(temp.data)
            temp = temp.next

    # Main function that inserts nodes of linked 
    # list q into p at alternate positions. 
    # Since head of first list never changes
    # but head of second list/ may change, 
    # we need single pointer for first list and 
    # double pointer for second list.
    def merge(self, p, q):
        p_curr = p.head
        q_curr = q.head

        # swap their positions until one 
        # finishes off
        while p_curr != None and q_curr != None:

            # Save next pointers
            p_next = p_curr.next
            q_next = q_curr.next

            # make q_curr as next of p_curr
            # change next pointer of q_curr
            q_curr.next = p_next  

            # change next pointer of p_curr
            p_curr.next = q_curr  

            # update current pointers for next 
            # iteration
            p_curr = p_next
            q_curr = q_next
            q.head = q_curr

# Driver code
llist1 = LinkedList()
llist2 = LinkedList()

# Creating Linked lists
# 1.
llist1.push(3)
llist1.push(2)
llist1.push(1)
llist1.push(0)

# 2.
for i in range(8, 3, -1):
    llist2.push(i)

print("First Linked List:")
llist1.printList()

print("Second Linked List:")
llist2.printList()

# Merging the LLs
llist1.merge(p=llist1, q=llist2)

print("Modified first linked list:")
llist1.printList()

print("Modified second linked list:")
llist2.printList()

# This code is contributed by Deepanshu Mehta
```

**输出:**

```
First Linked List:
1 2 3
Second Linked List:
4 5 6 7 8
Modified First Linked List:
1 4 2 5 3 6
Modified Second Linked List:
7 8 
```

更多详情请参考[整篇文章在交替位置](https://www.geeksforgeeks.org/merge-a-linked-list-into-another-linked-list-at-alternate-positions/)将一个链表合并成另一个链表！