# 用于反转单链表中交替 K 个节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-for-reverse-alternate-k-nodes-in-a-single-link-list/](https://www.geeksforgeeks.org/python-program-for-reversing-alternate-k-nodes-in-a-singly-linked-list/)

给定一个链表，编写一个函数以高效的方式反转每一个交替的 k 个节点(其中 k 是函数的输入)。给出你的算法的复杂性。

**示例:**

```
Inputs:   1->2->3->4->5->6->7->8->9->NULL and k = 3
Output:   3->2->1->4->5->6->9->8->7->NULL. 
```

**方法 1(处理 2k 个节点并递归调用列表的其余部分):**
这个方法基本上是[这篇](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/)帖子中讨论的方法的扩展。

```
kAltReverse(struct node *head, int k)
  1)  Reverse first k nodes.
  2)  In the modified list head points to the kth node.  So change next 
       of head to (k+1)th node
  3)  Move the current pointer to skip next k nodes.
  4)  Call the kAltReverse() recursively for rest of the n - 2k nodes.
  5)  Return new head of the list.
```

## 蟒蛇 3

```
# Python3 program to reverse alternate
# k nodes in a linked list
import math

# Link list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Reverses alternate k nodes and 
#returns the pointer to the new 
# head node 
def kAltReverse(head, k) : 
    current = head 
    next = None
    prev = None
    count = 0

    # 1) reverse first k nodes of the 
    # linked list 
    while (current != None and 
           count < k) : 
        next = current.next
        current.next = prev 
        prev = current 
        current = next
        count = count + 1;

    # 2) Now head pos to the kth node. 
    # So change next of head to (k+1)th node
    if(head != None): 
        head.next = current 

    # 3) We do not want to reverse next k 
    # nodes. So move the current 
    # pointer to skip next k nodes 
    count = 0
    while(count < k - 1 and 
          current != None ): 
        current = current.next
        count = count + 1

    # 4) Recursively call for the list 
    # starting from current.next. And make
    # rest of the list as next of first node 
    if(current != None): 
        current.next = 
                kAltReverse(current.next, k) 

    # 5) prev is the new head of the 
    # input list 
    return prev 

# UTILITY FUNCTIONS 
# Function to push a node 
def push(head_ref, new_data): 

    # Allocate node 
    new_node = Node(new_data)

    # Put in the data 
    # new_node.data = new_data 

    # Link the old list off the 
    # new node 
    new_node.next = head_ref 

    # Move the head to po to the 
    # new node 
    head_ref = new_node

    return head_ref

# Function to print linked list 
def prList(node): 
    count = 0
    while(node != None): 
        print(node.data, end = " ") 
        node = node.next
        count = count + 1

# Driver code
if __name__=='__main__':

    # Start with the empty list 
    head = None

    # Create a list 
    # 1.2.3.4.5...... .20 
    for i in range(20, 0, -1):
        head = push(head, i) 

    print("Given linked list ") 
    prList(head) 
    head = kAltReverse(head, 3) 

    print("Modified Linked list") 
    prList(head) 
# This code is contributed by Srathore
```

**输出:**

```
Given linked list
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
Modified Linked list
3 2 1 4 5 6 9 8 7 10 11 12 15 14 13 16 17 18 20 19
```

**时间复杂度:** O(n)

**方法 2(处理 k 个节点并递归调用列表的其余部分):**
方法 1 反转第一个 k 个节点，然后将指针移动到前面的 k 个节点。所以方法 1 使用两个 while 循环，在一次递归调用中处理 2k 个节点。

这个方法在递归调用中只处理 k 个节点。它使用第三个 bool 参数 b 来决定是反转 k 个元素还是简单地移动指针。

```
_kAltReverse(struct node *head, int k, bool b)
  1)  If b is true, then reverse first k nodes.
  2)  If b is false, then move the pointer k nodes ahead.
  3)  Call the kAltReverse() recursively for rest of the n - k nodes and link 
       rest of the modified list with end of first k nodes. 
  4)  Return new head of the list.
```

## 蟒蛇 3

```
# Python code for above algorithm

# Link list node 
class node:     
    def __init__(self, data): 
        self.data = data 
        self.next = next

# Function to insert a node at the
# beginning of the linked list
def push(head_ref, new_data):

    # Allocate node 
    new_node = node(0)

    # Put in the data 
    new_node.data = new_data

    # Link the old list to the 
    # new node 
    new_node.next = (head_ref)

    # Move the head to point to the 
    # new node 
    (head_ref) = new_node

    return head_ref

""" Alternatively reverses the given 
    linked list in groups of given 
    size k. """
def kAltReverse(head, k) :
    return _kAltReverse(head, k, True) 

""" Helper function for kAltReverse(). 
    It reverses k nodes of the list only 
    if the third parameter b is passed as 
    True, otherwise moves the pointer k 
    nodes ahead and recursively call itself """
def _kAltReverse(Node, k, b) :
    if(Node == None) :
        return None

    count = 1
    prev = None
    current = Node 
    next = None

    """ The loop serves two purposes 
        1) If b is True, 
        then it reverses the k nodes 
        2) If b is false, 
        then it moves the current pointer """
    while(current != None and count <= k) :

        next = current.next

        """ Reverse the nodes only if b 
            is True """
        if(b == True) :
            current.next = prev 

        prev = current 
        current = next
        count = count + 1

    """ 3) If b is True, then node is the 
        kth node. So attach rest of the list 
        after node. 
        4) After attaching, return the new 
        head """
    if(b == True) :

        Node.next = 
            _kAltReverse(current, 
                         k, not b) 
        return prev         

    else :

        """ If b is not True, then attach 
            rest of the list after prev. 
            So attach rest of the list 
            after prev """
        prev.next = _kAltReverse(current, 
                                 k, not b) 
        return Node     

""" Function to print linked list """
def printList(node) :

    count = 0
    while(node != None) :

        print( node.data, end = " ") 
        node = node.next
        count = count + 1

# Driver Code

# Start with the empty list 
head = None
i = 20

# Create a list 
# 1->2->3->4->5...... ->20 
while(i > 0 ): 
    head = push(head, i) 
    i = i - 1

print("Given linked list ") 
printList(head) 
head = kAltReverse(head, 3) 

print("Modified Linked list ") 
printList(head) 
# This code is contributed by Arnab Kundu
```

**输出:**

```
Given linked list
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
Modified Linked list
3 2 1 4 5 6 9 8 7 10 11 12 15 14 13 16 17 18 20 19
```

**时间复杂度:** O(n)

更多详情请参考[反向单链表中交替 K 节点](https://www.geeksforgeeks.org/reverse-alternate-k-nodes-in-a-singly-linked-list/)整篇文章！