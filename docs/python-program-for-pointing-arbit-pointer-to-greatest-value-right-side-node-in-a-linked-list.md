# 用于将仲裁指针指向链表中最大值右侧节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-pointing-arbitr-指向最大值的指针-右侧-链表中的节点/](https://www.geeksforgeeks.org/python-program-for-pointing-arbit-pointer-to-greatest-value-right-side-node-in-a-linked-list/)

给定单链表，每个节点都有一个额外的“任意”指针，该指针当前指向空。我们需要将“任意”指针指向右侧链表中最大值的节点。

![listwithArbit1](img/e37b455dc722e9b607243f9f28641891.png)

一个**简单的解决方案**就是逐个遍历所有节点。对于每个节点，找到右侧值最大的节点，并更改下一个指针。该解决方案的时间复杂度为 0(n<sup>2</sup>)。

一个**高效的解决方案**可以在 O(n)时间内工作。以下是步骤。

1.  反转给定的链表。
2.  开始遍历链表并存储到目前为止遇到的最大值节点。使每个节点的仲裁指向 max。如果到目前为止，当前节点中的数据多于 max 节点，请更新 max。
3.  反向修改链表和返回头。

下面是上述步骤的实现。

## 计算机编程语言

```
# Python Program to point arbit pointers 
# to highest value on its right

# Node class 
class Node: 

    # Constructor to initialize the 
    # node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None
        self.arbit = None

# Function to reverse the linked list 
def reverse(head):
    prev = None
    current = head
    next = None

    while (current != None):    
        next = current.next
        current.next = prev
        prev = current
        current = next

    return prev

# This function populates arbit pointer 
# in every node to the greatest value 
# to its right.
def populateArbit(head):

    # Reverse given linked list
    head = reverse(head)

    # Initialize pointer to maximum 
    # value node
    max = head

    # Traverse the reversed list
    temp = head.next
    while (temp != None):

        # Connect max through arbit
        # pointer
        temp.arbit = max

        # Update max if required
        if (max.data < temp.data):
            max = temp

        # Move ahead in reversed list
        temp = temp.next

    # Reverse modified linked list and 
    # return head.
    return reverse(head)

# Utility function to print result 
# linked list
def printNextArbitPointers(node):

    print("Node    ", 
          "Next Pointer    " , 
          "Arbit Pointer")
    while (node != None):

        print(node.data , 
              "        ", 
              end = "")

        if (node.next != None):
            print(node.next.data , 
                  "        ", end = "")
        else :
            print("None" , 
                  "        ",end = "")

        if (node.arbit != None):
            print(node.arbit.data, end = "")
        else :
            print("None", end = "")

        print("")
        node = node.next

# Function to create a new node 
# with given data 
def newNode(data):

    new_node = Node(0)
    new_node.data = data
    new_node.next = None
    return new_node

# Driver code
head = newNode(5)
head.next = newNode(10)
head.next.next = newNode(2)
head.next.next.next = newNode(3)
head = populateArbit(head)

print("Resultant Linked List is: ")
printNextArbitPointers(head)
# This code is contributed by Arnab Kundu
```

**输出:**

```
Resultant Linked List is: 
Node    Next Pointer    Arbit Pointer
5               10              10
10              2               3
2               3               3
3               NULL            NULL
```

**递归求解:**
我们可以递归到达最后一个节点，从头到尾遍历链表。递归解决方案不需要反向链表。我们也可以用堆栈代替递归来临时保存节点。感谢 Santosh Kumar Mishra 提供了这个解决方案。

## 蟒蛇 3

```
# Python3 program to point arbit pointers
# to highest value on its right 

''' Link list node '''
# Node class 
class newNode: 

    # Constructor to initialize the 
    # node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None
        self.arbit = None

# This function populates arbit pointer 
# in every node to the greatest value 
# to its right. 
maxNode = newNode(None)
def populateArbit(head):

    # using static maxNode to keep track 
    # of maximum orbit node address on 
    # right side 
    global maxNode

    # if head is null simply return the list 
    if (head == None):
        return

    ''' if head.next is null it means we 
        reached at the last node just update 
        the max and maxNode '''
    if (head.next == None):
        maxNode = head 
        return

    ''' Calling the populateArbit to the
        next node '''
    populateArbit(head.next) 

    ''' updating the arbit node of the 
        current node with the maximum 
        value on the right side '''
    head.arbit = maxNode 

    ''' if current Node value id greater 
        then the previous right node then 
        update it '''
    if (head.data > maxNode.data and 
        maxNode.data != None ):
        maxNode = head 
    return

# Utility function to prresult 
# linked list 
def printNextArbitPointers(node):
    print("Node    " , 
          "Next Pointer    " , 
          "Arbit Pointer")
    while (node != None):
        print(node.data, 
              "        ", 
              end = "")
        if(node.next):
            print(node.next.data,
                  "        ", 
                  end = "")
        else:
            print("NULL", "        ", 
                   end = "")
        if(node.arbit):
            print(node.arbit.data, end = "")
        else:
            print("NULL", end = "")
        print()
        node = node.next

# Driver code
head = newNode(5) 
head.next = newNode(10) 
head.next.next = newNode(2) 
head.next.next.next = newNode(3) 
populateArbit(head) 
print("Resultant Linked List is:") 
printNextArbitPointers(head) 
# This code is contributed by SHUBHAMSINGH10
```

**输出:**

```
Resultant Linked List is: 
Node    Next Pointer    Arbit Pointer
5               10              10
10              2               3
2               3               3
3               NULL            NULL
```

更多详情请参考完整文章[将仲裁指针指向链表](https://www.geeksforgeeks.org/point-arbit-pointer-greatest-value-right-side-node-linked-list/)右侧最大值节点！