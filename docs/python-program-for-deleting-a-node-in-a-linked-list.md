# 删除链表中节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于删除链表中节点的程序/](https://www.geeksforgeeks.org/python-program-for-deleting-a-node-in-a-linked-list/)

我们在之前关于单链表的文章中讨论过[链表介绍](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)和[链表插入](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。
让我们制定问题陈述，了解删除过程。*给定一个‘键’，删除链表中该键的第一次出现*。

**<u>迭代方法:</u>**
要从链表中删除一个节点，我们需要做以下步骤。
1)找到要删除节点的上一个节点。
2)更改上一个节点的下一个。
3)为要删除的节点释放内存。

![linkedlist_deletion](img/fe3a6a2699fb99ae5429afd588e89619.png)

由于链表的每个节点都是使用 C 语言中的 malloc()动态分配的，所以我们需要调用 [free()](http://www.cplusplus.com/reference/cstdlib/free/) 来释放分配给待删除节点的内存。

## 蟒蛇 3

```
# A complete working Python3 program to
# demonstrate deletion in singly 
# linked list with class 

# Node class 
class Node: 

    # Constructor to initialize the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Function to insert a new node at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Given a reference to the head of a list and a key, 
    # delete the first occurrence of key in linked list 
    def deleteNode(self, key): 

        # Store head node 
        temp = self.head 

        # If head node itself holds the key to be deleted 
        if (temp is not None): 
            if (temp.data == key): 
                self.head = temp.next
                temp = None
                return

        # Search for the key to be deleted, keep track of the 
        # previous node as we need to change 'prev.next' 
        while(temp is not None): 
            if temp.data == key: 
                break
            prev = temp 
            temp = temp.next

        # if key was not present in linked list 
        if(temp == None): 
            return

        # Unlink the node from linked list 
        prev.next = temp.next

        temp = None

    # Utility function to print the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print (" %d" %(temp.data)), 
            temp = temp.next

# Driver program 
llist = LinkedList() 
llist.push(7) 
llist.push(1) 
llist.push(3) 
llist.push(2) 

print ("Created Linked List: ")
llist.printList() 
llist.deleteNode(1) 
print ("
Linked List after Deletion of 1:")
llist.printList() 

# This code is contributed by Nikhil Kumar Singh (nickzuck_007) 
```

**Output:**

```
Created Linked List: 
 2  3  1  7 
Linked List after Deletion of 1: 
 2  3  7
```

详情请参考[链表|集合 3(删除节点)](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)整篇文章！