# 通过改变链接成对交换给定链表元素的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-pair-swapping-elements-of-a-给定-link-list-by-changing-link/](https://www.geeksforgeeks.org/python-program-for-pairwise-swapping-elements-of-a-given-linked-list-by-changing-links/)

给定一个单链表，编写一个成对交换元素的函数。例如，如果链表是 1->2->3->4->5->6->7，那么函数应该把它改成 2->1->4->3->6->5->7，如果链表是 1->2->3->4->5->6，那么函数应该把它改成 2->1->4->3->6->5

这个问题已经在[这里](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)讨论过了。这里提供的解决方案交换节点的数据。如果数据包含许多字段，将会有许多交换操作。所以一般来说，改变链接是一个更好的主意。下面是更改链接而不是交换数据的实现。

## 蟒 3

```
# Python3 program to swap elements of
# linked list by changing links

# Linked List Node
class Node:    
    def __init__(self, data):        
        self.data = data
        self.next = None

# Create and Handle list 
# operations
class LinkedList:

    def __init__(self):

        # Head of list
        self.head = None 

    # Add data to list
    def addToList(self, data):        
        newNode = Node(data)
        if self.head is None:
            self.head = newNode
            return

        last = self.head

        while last.next:
            last = last.next

        last.next = newNode

    # Function to print nodes 
    # in a given linked list
    def __str__(self):        
        linkedListStr = ""
        temp = self.head

        while temp:
            linkedListStr = (linkedListStr + 
                             str(temp.data) + " ")
            temp = temp.next

        return linkedListStr

    # Function to pairwise swap elements
    # of a linked list. It returns head of
    # the modified list, so return value 
    # of this node must be assigned
    def pairWiseSwap(self):

        # If list is empty or with one 
        # node
        if (self.head is None or 
            self.head.next is None):
            return

        # Initialize previous and current 
        # pointers
        prevNode = self.head
        currNode = self.head.next

        # Change head node
        self.head = currNode

        # Traverse the list
        while True:
            nextNode = currNode.next

            # Change next of current 
            # node to previous node
            currNode.next = prevNode  

            # If next node is the last node
            if nextNode.next is None:
                prevNode.next = nextNode
                break

            # Change next of previous to 
            # next of next
            prevNode.next = nextNode.next

            # Update previous and current nodes
            prevNode = nextNode
            currNode = prevNode.next

# Driver Code
linkedList = LinkedList()
linkedList.addToList(1)
linkedList.addToList(2)
linkedList.addToList(3)
linkedList.addToList(4)
linkedList.addToList(5)
linkedList.addToList(6)
linkedList.addToList(7)

print("Linked list before calling"  
      "pairwiseSwap() ", linkedList)

linkedList.pairWiseSwap()

print("Linked list after calling " 
      "pairwiseSwap() ", linkedList)
# This code is contributed by AmiyaRanjanRout
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

**时间复杂度:**上述程序的时间复杂度为 O(n)，其中 n 为给定链表中的节点数。while 循环遍历给定的链表。

以下是相同方法的**递归实现**。我们更改前两个节点，并对剩余的列表重复执行。感谢 geek 和 omer salem 提出这个方法。

## 蟒 3

```
# Python3 program to pairwise swap
# linked list using recursive method

# Linked List Node
class Node:    
    def __init__(self, data):        
        self.data = data
        self.next = None

# Create and Handle list 
# operations
class LinkedList:    
    def __init__(self):

        # Head of list
        self.head = None  

    # Add data to list
    def addToList(self, data):        
        newNode = Node(data)

        if self.head is None:
            self.head = newNode
            return

        last = self.head

        while last.next:
            last = last.next

        last.next = newNode

    # Function to print nodes in 
    # a given linked list 
    def __str__(self):        
        linkedListStr = ""
        temp = self.head

        while temp:
            linkedListStr = (linkedListStr + 
                             str(temp.data) + " ")
            temp = temp.next
        return linkedListStr

    # Function to pairwise swap elements of
    # a linked list. It returns head of the 
    # modified list, so return value
    # of this node must be assigned
    def pairWiseSwap(self, node):

        # If list is empty or with one node
        if node is None or node.next is None:
            return node

        # Store head of list after 
        # 2 nodes
        remaining = node.next.next

        # Change head
        newHead = node.next

        # Change next to second node
        node.next.next = node

        # Recur for remaining list and 
        # change next of head
        node.next = self.pairWiseSwap(remaining)

        # Return new head of modified list
        return newHead

# Driver Code
linkedList = LinkedList()
linkedList.addToList(1)
linkedList.addToList(2)
linkedList.addToList(3)
linkedList.addToList(4)
linkedList.addToList(5)
linkedList.addToList(6)
linkedList.addToList(7)

print("Linked list before calling " 
      "pairwiseSwap() ", linkedList)

linkedList.head = linkedList.pairWiseSwap(
                  linkedList.head)
print("Linked list after calling " 
      "pairwiseSwap() ", linkedList)
# This code is contributed by AmiyaRanjanRout
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

更多细节请参考完整的文章[通过改变链接来成对交换给定链表的元素](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/)！