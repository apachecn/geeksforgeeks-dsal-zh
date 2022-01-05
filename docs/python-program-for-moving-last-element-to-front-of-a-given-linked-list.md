# 将最后一个元素移到给定链表前面的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-move-last-element-to-front-给定链表/](https://www.geeksforgeeks.org/python-program-for-moving-last-element-to-front-of-a-given-linked-list/)

编写一个函数，在给定的单链表中把最后一个元素移到前面。例如，如果给定的链表是 1->2->3->4->5，那么函数应该将链表改为 5->1->2->3->4。
**算法:**
遍历列表直到最后一个节点。使用两个指针:一个存储最后一个节点的地址，另一个存储第二个最后一个节点的地址。循环结束后，执行以下操作。

1.  将倒数第二个设为最后一个(倒数第二个->下一个=空)。
2.  将倒数第二个设置为标题(最后->下一个= *head_ref)。
3.  将最后一个作为标题(*head_ref =最后一个)。

## 蟒蛇 3

```
# Python3 code to move the last item 
# to front
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    # Function to add a node 
    # at the beginning of Linked List
    def push(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    # Function to print nodes in 
    # a given linked list
    def printList(self):
        tmp = self.head
        while tmp is not None:
            print(tmp.data, end = ", ")
            tmp = tmp.next
        print()

    # Function to bring the last node 
    # to the front
    def moveToFront(self):
        tmp = self.head

        # To maintain the track of
        # the second last node
        sec_last = None 

        # To check whether we have not 
        # received the empty list or list 
        # with a single node
        if not tmp or not tmp.next: 
            return

        # Iterate till the end to get
        # the last and second last node 
        while tmp and tmp.next :
            sec_last = tmp
            tmp = tmp.next

        # Point the next of the second
        # last node to None
        sec_last.next = None

        # Make the last node as the 
        # first Node
        tmp.next = self.head
        self.head = tmp

# Driver Code
if __name__ == '__main__':
    llist = LinkedList()

    # Swap the 2 nodes
    llist.push(5)
    llist.push(4)
    llist.push(3)
    llist.push(2)
    llist.push(1)
    print (
    "Linked List before moving last to front ")
    llist.printList()
    llist.moveToFront()
    print (
    "Linked List after moving last to front ")
    llist.printList()
```

**输出:**

```
Linked list before moving last to front 
1 2 3 4 5 
Linked list after removing last to front 
5 1 2 3 4
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

详情请参考完整文章[将最后一个元素移到给定链表](https://www.geeksforgeeks.org/move-last-element-to-front-of-a-given-linked-list/)的前面！