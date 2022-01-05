# 向链表表示的数字加 1 的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于将 1 添加到表示为链表的数字中的程序/](https://www.geeksforgeeks.org/python-program-for-adding-1-to-a-number-represented-as-linked-list/)

数字在链表中表示，每个数字对应链表中的一个节点。再加 1。例如，1999 被表示为(1-> 9-> 9 -> 9)，将 1 添加到它应该会将其更改为(2->0->0->0)

以下是步骤:

1.  反转给定的链表。例如，1-> 9-> 9 -> 9 被转换为 9-> 9-> 9-> 9-> 1。
2.  从最左边的节点开始遍历链表，并向其中添加 1。如果有进位，移到下一个节点。当有进位时，继续移动到下一个节点。
3.  反向修改链表和返回头。

下面是以上步骤的实现。

## 蟒蛇 3

```
# Python3 program to add 1 to 
# a linked list
import sys
import math

# Linked list node
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

# Function to create a new node 
# with given data 
def newNode(data):
    return Node(data)

# Function to reverse the 
# linked list
def reverseList(head):
    if not head:
        return
    curNode = head
    prevNode = head
    nextNode = head.next
    curNode.next = None

    while(nextNode):
        curNode = nextNode
        nextNode = nextNode.next
        curNode.next = prevNode
        prevNode = curNode

    return curNode

# Adds one to a linked lists and 
# return the head node of 
# resultant list
def addOne(head):

    # Reverse linked list and add 
    # one to head
    head = reverseList(head)
    k = head
    carry = 0
    prev = None
    head.data += 1

    # update carry for next calculation
    while(head != None) and (head.data > 9 or carry > 0):
        prev = head
        head.data += carry
        carry = head.data // 10
        head.data = head.data % 10
        head = head.next

    if carry > 0:
        prev.next = Node(carry)
    # Reverse the modified list
    return reverseList(k)

# A utility function to print 
# a linked list
def printList(head):
    if not head:
        return

    while(head):
        print("{}".format(head.data), end="")
        head = head.next

# Driver code
if __name__ == '__main__':
    head = newNode(1)
    head.next = newNode(9)
    head.next.next = newNode(9)
    head.next.next.next = newNode(9)

    print("List is: ", 
           end = "")
    printList(head)

    head = addOne(head)

    print("Resultant list is: ", 
           end = "")
    printList(head)
# This code is contributed by Rohit
```

**输出:**

```
List is 1999
Resultant list is 2000
```

**递归实现:**
我们可以递归到达最后一个节点，并结转到之前的节点。递归解决方案不需要链表的反转。我们也可以用堆栈代替递归来临时保存节点。

下面是递归解决方案的实现。

## 计算机编程语言

```
# Recursive Python program to add 1 to 
# a linked list

# Node class 
class Node: 

    # Constructor to initialize 
    # the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to create a new node 
# with given data 
def newNode(data):

    new_node = Node(0)
    new_node.data = data
    new_node.next = None
    return new_node

# Recursively add 1 from end to beginning 
# and returns carry after all nodes are 
# processed.
def addWithCarry(head):

    # If linked list is empty, then
    # return carry
    if (head == None):
        return 1

    # Add carry returned be next node 
    # call
    res = head.data + addWithCarry(head.next)

    # Update data and return new carry
    head.data = int((res) % 10)
    return int((res) / 10)

# This function mainly uses 
# addWithCarry().
def addOne(head):

    # Add 1 to linked list from end 
    # to beginning
    carry = addWithCarry(head)

    # If there is carry after processing 
    # all nodes, then we need to add a 
    # new node to linked list
    if (carry != 0):

        newNode = Node(0)
        newNode.data = carry
        newNode.next = head

        # New node becomes head now
        return newNode 

    return head

# A utility function to print a 
# linked list
def printList(node):

    while (node != None):    
        print(node.data,
              end = "")
        node = node.next

    print("")

# Driver code
head = newNode(1)
head.next = newNode(9)
head.next.next = newNode(9)
head.next.next.next = newNode(9)

print("List is ")
printList(head)

head = addOne(head)

print("Resultant list is ")
printList(head)
# This code is contributed by Arnab Kundu
```

**输出:**

```
List is 1999
Resultant list is 2000
```

更多详情请参考[上的完整文章将 1 添加到表示为链表](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)的数字中！