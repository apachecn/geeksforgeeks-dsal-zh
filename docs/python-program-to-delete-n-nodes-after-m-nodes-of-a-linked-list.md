# 删除链表 M 个节点后 N 个节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-to-delete-n-nodes-after-m-nodes-of-a-link-list/](https://www.geeksforgeeks.org/python-program-to-delete-n-nodes-after-m-nodes-of-a-linked-list/)

给定一个链表和两个整数 M 和 N。遍历链表，保留 M 个节点，然后删除下 N 个节点，一直到链表结束。
难度等级:菜鸟
**示例:**

```
Input:
M = 2, N = 2
Linked List: 1->2->3->4->5->6->7->8
Output:
Linked List: 1->2->5->6

Input:
M = 3, N = 2
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->2->3->6->7->8

Input:
M = 1, N = 1
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->3->5->7->9
```

问题的主要部分是维护节点之间的适当链接，确保所有的角落案例都得到处理。下面是 skipMdeleteN()函数的 C 实现，它跳过 M 个节点，删除 N 个节点，直到列表结束。假设 M 不能为 0。

## 计算机编程语言

```
# Python program to delete M nodes 
# after N nodes
# Node class 
class Node:

    # Constructor to initialize 
    # the node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Function to insert a new node 
    # at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Utility function to print the 
    # linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

    def skipMdeleteN(self, M, N):
        curr = self.head

        # The main loop that traverses 
        # through the whole list
        while(curr):
            # Skip M nodes
            for count in range(1, M):
                if curr is None:
                    return 
                curr = curr.next

            if curr is None :
                return 

            # Start from next node and delete 
            # N nodes
            t = curr.next 
            for count in range(1, N+1):
                if t is None:
                    break
                t = t.next

            # Link the previous list with 
            # remaining nodes
            curr.next = t

            # Set Current pointer for next 
            # iteration
            curr = t 

# Driver code

# Create following linked list
# 1->2->3->4->5->6->7->8->9->10
llist = LinkedList()
M = 2 
N = 3
llist.push(10)
llist.push(9)
llist.push(8)
llist.push(7)
llist.push(6)
llist.push(5)
llist.push(4)
llist.push(3)
llist.push(2)
llist.push(1)

print "M = %d, N = %d
Given Linked List is:" %(M, N)
llist.printList()
print 

llist.skipMdeleteN(M, N)

print "Linked list after deletion is"
llist.printList()
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**输出:**

```
M = 2, N = 3
Given Linked list is :
1 2 3 4 5 6 7 8 9 10
Linked list after deletion is :
1 2 6 7
```

**时间复杂度:**
O(n)，其中 n 为链表中的节点数。

更多详情请参考完整文章[删除链表](https://www.geeksforgeeks.org/delete-n-nodes-after-m-nodes-of-a-linked-list/)M 个节点后的 N 个节点！