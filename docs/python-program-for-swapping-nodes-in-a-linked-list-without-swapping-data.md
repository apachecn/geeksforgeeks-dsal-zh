# 用于交换链表中的节点而不交换数据的 Python 程序

> 原文:[https://www . geesforgeks . org/python-程序交换-链表中的节点-不交换-数据/](https://www.geeksforgeeks.org/python-program-for-swapping-nodes-in-a-linked-list-without-swapping-data/)

给定一个链表和其中的两个键，用两个给定的键交换节点。应该通过更改链接来交换节点。当数据包含许多字段时，交换节点的数据在许多情况下可能是昂贵的。

可以假设链表中的所有键都是不同的。

**例:**

```
Input : 10->15->12->13->20->14,  x = 12, y = 20
Output: 10->15->20->13->12->14

Input : 10->15->12->13->20->14,  x = 10, y = 20
Output: 20->15->12->13->10->14

Input : 10->15->12->13->20->14,  x = 12, y = 13
Output: 10->15->13->12->20->14
```

这看起来可能是一个简单的问题，但这是一个有趣的问题，因为它有以下情况需要处理。

1.  x 和 y 可以相邻，也可以不相邻。
2.  x 或 y 都可以是头节点。
3.  x 或 y 可能是最后一个节点。
4.  链接列表中可能不存在 x 和/或 y。

如何编写一个干净的工作代码来处理上述所有可能性。

想法是首先在给定的链表中搜索 x 和 y。如果他们中的任何一个不存在，那么返回。在搜索 x 和 y 时，跟踪当前和以前的指针。首先更改上一个指针的下一个，然后更改当前指针的下一个。

下面是上述方法的实现。

## 巨蟒

T0T6】

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 1 2 4 3 5 6 7 
```

**优化:**以上代码可以优化为单次遍历搜索 x 和 y。两个循环用于保持程序简单。

**更简单的方法:**

## 蟒蛇

```
# Python3 program to swap two given
# nodes of a linked list

# A linked list node class
class Node:

    # constructor
    def __init__(self, val = None, 
                 next1 = None):
        self.data = val
        self.next = next1

    # Print list from this
    # to last till None
    def printList(self):
        node = self

        while (node != None):
            print(node.data, end = " ")
            node = node.next
        print(" ")

# Function to add a node
# at the beginning of List
def push(head_ref, new_data):

    # Allocate node
    (head_ref) = Node(new_data, head_ref)
    return head_ref

def swapNodes(head_ref, x, y):
    head = head_ref

    # Nothing to do if x and y are same
    if (x == y):
        return None

    a = None
    b = None

    # Search for x and y in the linked list
    # and store their pointer in a and b
    while (head_ref.next != None):

        if ((head_ref.next).data == x):
            a = head_ref

        elif ((head_ref.next).data == y):
            b = head_ref

        head_ref = ((head_ref).next)

    # If we have found both a and b
    # in the linked list swap current
    # pointer and next pointer of these
    if (a != None and b != None):
        temp = a.next
        a.next = b.next
        b.next = temp
        temp = a.next.next
        a.next.next = b.next.next
        b.next.next = temp

    return head

# Driver code
start = None

# The constructed linked list is:
# 1.2.3.4.5.6.7
start = push(start, 7)
start = push(start, 6)
start = push(start, 5)
start = push(start, 4)
start = push(start, 3)
start = push(start, 2)
start = push(start, 1)

print("Linked list before calling swapNodes() ")
start.printList()
start = swapNodes(start, 6, 1)
print("Linked list after calling swapNodes() ")
start.printList()
# This code is contributed by Arnab Kundu
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 6 2 3 4 5 1 7 
```

更多详情请参考完整文章[在链表中交换节点不交换数据](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)！