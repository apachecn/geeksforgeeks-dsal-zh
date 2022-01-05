# 用于从链表中删除最后一个条目的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于从链接列表中删除最后出现的项目的程序/](https://www.geeksforgeeks.org/python-program-for-deleting-last-occurrence-of-an-item-from-linked-list/)

使用指针，循环遍历整个列表，并使用特殊指针跟踪包含最后一个出现键的节点之前的节点。在此之后，只需将下一个特殊指针存储到下一个特殊指针中，以从链表中移除所需的节点。

## 蟒蛇 3

```
# Python program to implement 
# the above approach
# A linked list Node
class Node: 
    def __init__(self, new_data):         
        self.data = new_data 
        self.next = None

# Function to delete the last
# occurrence
def deleteLast(head, x):
    temp = head
    ptr = None

    while (temp != None): 

        # If found key, update
        if (temp.data == x):
            ptr = temp     

        temp = temp.next

    # If the last occurrence is the 
    # last node
    if (ptr != None and ptr.next == None): 
        temp = head
        while (temp.next != ptr):
            temp = temp.next

        temp.next = None

    # If it is not the last node
    if (ptr != None and ptr.next != None): 
        ptr.data = ptr.next.data
        temp = ptr.next
        ptr.next = ptr.next.next

    return head

# Utility function to create a 
# new node
# with given key 
def newNode(x):

    node = Node(0)
    node.data = x
    node.next = None
    return node

# This function prints contents of 
# linked list starting from the given 
# Node
def display(head):
    temp = head

    if (head == None): 
        print("NULL")
        return

    while (temp != None): 
        print(temp.data, " --> ", 
              end = "")
        temp = temp.next

    print("NULL")

# Driver code
head = newNode(1)
head.next = newNode(2)
head.next.next = newNode(3)
head.next.next.next = 
newNode(4)
head.next.next.next.next = 
newNode(5)
head.next.next.next.next.next = 
newNode(4)
head.next.next.next.next.next.next = 
newNode(4)

print("Created Linked list: ", 
       end = '')
display(head)

# Pass the address of the head pointer
head = deleteLast(head, 4) 
print("List after deletion of 4: ", 
       end = '')

display(head)
# This code is contributed by rutvik_56
```

**输出:**

```
Created Linked list: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> 4 --> NULL
List after deletion of 4: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> NULL
```

给定一个喜欢的列表和一个要删除的键。从链接中删除键的最后一次出现。该列表可能有重复项。

**示例**:

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

想法是从头到尾遍历链表。遍历时，跟踪最后一个出现的键。遍历完整列表后，通过复制下一个节点的数据并删除下一个节点来删除最后一个匹配项。

## 蟒蛇 3

```
# Python3 program to demonstrate deletion 
# of last Node in singly linked list 

# A linked list Node 
class Node: 

    # Constructor to initialize the 
    # node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

def deleteLast(head, key):

    # Initialize previous of Node to 
    # be deleted 
    x = None

    # Start from head and find the Node 
    # to be deleted 
    temp = head 
    while (temp != None):

        # If we found the key, update xv 
        if (temp.key == key) :
            x = temp 

        temp = temp.next

    # key occurs at-least once 
    if (x != None):

        # Copy key of next Node to x 
        x.key = x.next.key 

        # Store and unlink next 
        temp = x.next
        x.next = x.next.next

        # Free memory for next 

    return head

# Utility function to create 
# a new node with given key 
def newNode(key):

    temp = Node(0) 
    temp.key = key 
    temp.next = None
    return temp 

# This function prints contents of 
# linked list starting from the given 
# Node 
def printList(node):
    while (node != None):

        print (node.key, 
               end = " ") 
        node = node.next

# Driver Code 
if __name__=='__main__': 

    # Start with the empty list 
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(3) 
    head.next.next.next = 
    newNode(5) 
    head.next.next.next.next = 
    newNode(2) 
    head.next.next.next.next.next = 
    newNode(10) 

    print("Created Linked List: ") 
    printList(head) 
    deleteLast(head, 2) 

    print("Linked List after Deletion of 1: ") 
    printList(head) 
# This code is contributed by Arnab Kundu
```

**输出:**

```
Created Linked List: 
1  2  3  5  2  10 
Linked List after Deletion of 1: 
1  2  3  5  10
```

**当要删除的节点是最后一个节点时，上述解决方案不起作用。**
以下方案处理所有案件。

## 蟒蛇 3

```
# A Python3 program to demonstrate deletion 
# of last Node in singly linked list

# A linked list Node
class Node: 
    def __init__(self, new_data): 
        self.data = new_data 
        self.next = None

# Function to delete the last 
# occurrence
def deleteLast(head, x):
    temp = head
    ptr = None
    while (temp != None): 

        # If found key, update
        if (temp.data == x):
            ptr = temp     
        temp = temp.next

    # If the last occurrence is the 
    # last node
    if (ptr != None and ptr.next == None): 
        temp = head
        while (temp.next != ptr) :
            temp = temp.next    
        temp.next = None

    # If it is not the last node
    if (ptr != None and ptr.next != None): 
        ptr.data = ptr.next.data
        temp = ptr.next
        ptr.next = ptr.next.next

    return head

# Utility function to create a 
# new node with given key 
def newNode(x):
    node = Node(0)
    node.data = x
    node.next = None
    return node

# This function prints contents of 
# linked list starting from the given 
# Node
def display(head):
    temp = head
    if (head == None): 
        print("None")
        return

    while (temp != None): 
        print(temp.data, " -> ", 
              end = "")
        temp = temp.next

    print("None")

# Driver code
head = newNode(1)
head.next = newNode(2)
head.next.next = newNode(3)
head.next.next.next = 
newNode(4)
head.next.next.next.next = 
newNode(5)
head.next.next.next.next.next = 
newNode(4)
head.next.next.next.next.next.next = 
newNode(4)
print("Created Linked list: ")
display(head)
head = deleteLast(head, 4)
print("List after deletion of 4: ")
display(head)
# This code is contributed by Arnab Kundu
```

**输出:**

```
Created Linked List: 
 1  2  3  4  5  4  4 
Linked List after Deletion of 1: 
 1  2  3  4  5  4
```

详情请参考[从链表](https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/)中删除最后一个条目的完整文章！