# 交替分割给定单链表的 Python 程序-集合 1

> 原文:[https://www . geesforgeks . org/python-program-for-alternative-split-of-给定-single-link-list-set-1/](https://www.geeksforgeeks.org/python-program-for-alternating-split-of-a-given-singly-linked-list-set-1/)

编写一个函数 AlternatingSplit()，该函数取一个列表，并将其节点划分为两个较小的列表“a”和“b”。子列表应该由原始列表中的交替元素组成。因此，如果原始列表是 0->1->0->1->0->1，那么一个子列表应该是 0->0->0，另一个应该是 1->1->1。

**方法(简单):**
最简单的方法是遍历源列表，从源中拉出节点，并交替地将它们放在“a”和“b”的前面(或开头)。唯一奇怪的是，节点的顺序与源列表中的顺序相反。方法 2 通过跟踪子列表中的最后一个节点在末尾插入节点。

## 计算机编程语言

```
# Python program to alternatively split 
# a linked list into two halves 

# Node class
class Node:    
    def __init__(self, data, 
                 next = None):        
        self.data = data
        self.next = None

class LinkedList:    
    def __init__(self):        
        self.head = None

    # Given the source list, split its nodes 
    # into two shorter lists. If we number the 
    # elements 0, 1, 2, ... then all the even 
    # elements should go in the first list, and 
    # all the odd elements in the second. The 
    # elements in the new lists may be in any order.
    def AlternatingSplit(self, a, b):        
        first = self.head
        second = first.next

        while (first is not None and 
               second is not None and 
               first.next is not None):

              # Move a node to list 'a'
              self.MoveNode(a, first) 

              # Move a node to list 'b'
              self.MoveNode(b, second) 

              first = first.next.next

              if first is None:
                break

              second = first.next

    # Pull off the front node of the 
    # source and put it in dest
    def MoveNode(self, dest, node):

        # Make the new node
        new_node = Node(node.data)

        if dest.head is None:
            dest.head = new_node
        else:

            # Link the old dest off the 
            # new node 
            new_node.next = dest.head

            # Move dest to point to the 
            # new node 
            dest.head = new_node

    # Utility Functions
    # Function to insert a node at  
    # the beginning of the linked list 
    def push(self, data):

        # 1 & 2 allocate the Node & 
        # put the data

        new_node = Node(data)

        # Make the next of new Node as head
        new_node.next = self.head

        # Move the head to point to 
        # new Node
        self.head = new_node

    # Function to print nodes in a given 
    # linked list 
    def printList(self):

        temp = self.head
        while temp:
            print temp.data,
            temp = temp.next

        print("")

# Driver Code
if __name__ == "__main__":

    # Start with empty list
    llist = LinkedList()
    a = LinkedList()
    b = LinkedList()

    # Created linked list will be
    # 0->1->2->3->4->5 
    llist.push(5)
    llist.push(4)
    llist.push(3)
    llist.push(2)
    llist.push(1)
    llist.push(0)

    llist.AlternatingSplit(a, b)

    print "Original Linked List: ",
    llist.printList()

    print "Resultant Linked List 'a' : ",
    a.printList()

    print "Resultant Linked List 'b' : ",
    b.printList()

# This code is contributed by kevalshah5
```

**输出:**

```
Original linked List: 0 1 2 3 4 5 
Resultant Linked List 'a' : 4 2 0 
Resultant Linked List 'b' : 5 3 1
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。
更多详情请参考[给定单链表的交替拆分|集合 1](https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/) 的完整文章！