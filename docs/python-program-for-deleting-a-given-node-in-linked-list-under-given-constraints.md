# 给定约束下删除链表中给定节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-delete-给定约束下链表中的给定节点/](https://www.geeksforgeeks.org/python-program-for-deleting-a-given-node-in-linked-list-under-given-constraints/)

给定一个单链表，编写一个函数来删除给定的节点。您的函数必须遵循以下约束:
1)它必须接受指向起始节点的指针作为第一个参数，接受要删除的节点作为第二个参数，即指向头节点的指针不是全局的。
2)它不应该返回指向头节点的指针。
3)它不应该接受指向头节点的指针。
你可以假设链表永远不会变成空的。
让函数名为 deleteNode()。在一个简单的实现中，当要删除的节点是第一个节点时，函数需要修改头指针。正如[上一篇文章](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)中所讨论的，当一个函数修改头部指针时，该函数必须使用其中一个[给定的方法](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)，这里我们不能使用任何一个方法。
**解决方案**
我们明确处理待删除节点是第一个节点的情况，我们把下一个节点的数据复制到头上，删除下一个节点。被删除的节点不是头节点的情况可以通过找到前一个节点并改变前一个节点的下一个来正常处理。以下是实现。

## 蟒蛇 3

```
# Node class
class Node:

    def __init__(self, data):
        self.data = data
        self.next = None

# LinkedList class
class LinkedList:

    def __init__(self):
        self.head = None

    def deleteNode(self, data):
        temp = self.head
        prev = self.head
        if temp.data == data:
            if temp.next is None:
                print("Can't delete the node as it has only one node")
            else:
                temp.data = temp.next.data
                temp.next = temp.next.next
            return
        while temp.next is not None and temp.data != data:
            prev = temp
            temp = temp.next
        if temp.next is None and temp.data !=data:
            print("Can't delete the node as it doesn't exist")
         # If node is last node of the linked list
        elif temp.next is None and temp.data == data:
            prev.next = None
        else:
            prev.next = temp.next

    # To push a new element in the Linked List     
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # To print all the elements of the Linked List
    def PrintList(self):

        temp = self.head
        while(temp):
            print(temp.data, end = " ")
            temp = temp.next

# Driver Code
llist = LinkedList()
llist.push(3)
llist.push(2)
llist.push(6)
llist.push(5)
llist.push(11)
llist.push(10)
llist.push(15)
llist.push(12)

print("Given Linked List: ", end = ' ')
llist.PrintList()
print("

Deleting node 10:")
llist.deleteNode(10)
print("Modified Linked List: ", end = ' ')
llist.PrintList()
print("

Deleting first node")
llist.deleteNode(12)
print("Modified Linked List: ", end = ' ')
llist.PrintList()

# This code is contributed by Akarsh Somani
```

**输出:**

```
Given Linked List: 12 15 10 11 5 6 2 3

Deleting node 10:
Modified Linked List: 12 15 11 5 6 2 3

Deleting first node
Modified Linked List: 15 11 5 6 2 3
```

详情请参考[在给定约束下删除链表中给定节点](https://www.geeksforgeeks.org/delete-a-given-node-in-linked-list-under-given-constraints/)的完整文章！