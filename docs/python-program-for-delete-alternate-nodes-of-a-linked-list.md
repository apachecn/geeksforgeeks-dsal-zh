# 删除链表备用节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-delete-alternate-nodes-of-a-link-list/](https://www.geeksforgeeks.org/python-program-for-delete-alternate-nodes-of-a-linked-list/)

给定一个单链表，从第二个节点开始删除它的所有替换节点。例如，如果给定的链表是 1->2->3->4->5，那么你的函数应该把它转换成 1->3->5，如果给定的链表是 1->2->3->4，那么把它转换成 1->3。

**方法 1(迭代):**
跟踪要删除的节点的前一个。首先，更改上一个节点的下一个链接，并迭代移动到下一个节点。

## 蟒蛇 3

```
# Python3 program to remove alternate 
# nodes of a linked list 
import math 

# A linked list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Deletes alternate nodes 
# of a list starting with head 
def deleteAlt(head): 
    if (head == None):
        return

    # Initialize prev and node to 
    # be deleted 
    prev = head 
    now = head.next

    while (prev != None and 
           now != None): 

        # Change next link of previous
        # node 
        prev.next = now.next

        # Free memory 
        now = None

        # Update prev and node 
        prev = prev.next
        if (prev != None): 
            now = prev.next

# UTILITY FUNCTIONS TO TEST 
# fun1() and fun2() 
# Given a reference (pointer to pointer) 
# to the head of a list and an , push a 
# new node on the front of the list. 
def push(head_ref, new_data): 

    # Allocate node 
    new_node = Node(new_data)

    # Put in the data 
    new_node.data = new_data 

    # Link the old list off the 
    # new node 
    new_node.next = head_ref 

    # Move the head to po to the 
    # new node 
    head_ref = new_node 
    return head_ref

# Function to print nodes in a 
# given linked list 
def prList(node): 
    while (node != None): 
        print(node.data, end = " ") 
        node = node.next

# Driver code 
if __name__=='__main__': 

    # Start with the empty list 
    head = None

    # Using head=push() to construct 
    # list 1.2.3.4.5 
    head = push(head, 5) 
    head = push(head, 4) 
    head = push(head, 3) 
    head = push(head, 2) 
    head = push(head, 1) 

    print("List before calling deleteAlt() ")
    prList(head) 

    deleteAlt(head) 

    print("List after calling deleteAlt() ") 
    prList(head) 
# This code is contributed by Srathore
```

**输出:**

```
List before calling deleteAlt() 
1 2 3 4 5 
List after calling deleteAlt() 
1 3 5 
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**方法 2(递归):**
递归代码使用与方法 1 相同的方法。递归代码简单而简短，但会导致 O(n)个递归函数调用大小为 n 的链表。

## 蟒蛇 3

```
# Deletes alternate nodes of a list 
# starting with head 
def deleteAlt(head): 
    if (head == None): 
        return

    node = head.next

    if (node == None): 
        return

    # Change the next link of head 
    head.next = node.next

    # Free memory allocated for node 
    free(node) 

    # Recursively call for the new 
    # next of head 
    deleteAlt(head.next) 
# This code is contributed by Srathore
```

**时间复杂度:** O(n)

更多详情请参考[删除链表备用节点](https://www.geeksforgeeks.org/delete-alternate-nodes-of-a-linked-list/)整篇文章！