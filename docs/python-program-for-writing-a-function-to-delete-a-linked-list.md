# 编写删除链表函数的 Python 程序

> 原文:[https://www . geesforgeks . org/python-写程序-函数-删除-链表/](https://www.geeksforgeeks.org/python-program-for-writing-a-function-to-delete-a-linked-list/)

**Python 的算法:**
在 Python 中，会发生自动垃圾收集，所以删除链表很容易。只需要将 head 改为 null。

**实施:**

## 蟒蛇 3

```
# Python3 program to delete all
# the nodes of singly linked list

# Node class
class Node:

    # Function to initialize the 
    # node object
    def __init__(self, data):

        # Assign data
        self.data = data

        # Initialize next as null  
        self.next = None  

# Constructor to initialize the 
# node object
class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    def deleteList(self):

        # Initialize the current node
        current = self.head
        while current:

            # Move next node
            prev = current.next  

            # Delete the current node
            del current.data

            # Set current equals prev node
            current = prev

        # In python garbage collection happens
        # therefore, only self.head = None
        # would also delete the link list 

    # Push function to add node in 
    # front of llist
    def push(self, new_data):

        # Allocate the Node &
        # Put in the data
        new_node = Node(new_data)

        # Make next of new Node as head
        new_node.next = self.head

        # Move the head to point to the 
        # new Node
        self.head = new_node

# Use push() to construct list
# 1-> 12-> 1-> 4-> 1
if __name__ == '__main__':

    llist = LinkedList()
    llist.push(1)
    llist.push(4)
    llist.push(1)
    llist.push(12)
    llist.push(1)

    print("Deleting linked list")
    llist.deleteList()

    print("Linked list deleted")
# This code is contributed by Shrikant13
```

**输出:**

```
Deleting linked list
Linked list deleted
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

更多详情请参考[写函数删除链表](https://www.geeksforgeeks.org/write-a-function-to-delete-a-linked-list/)整篇文章！