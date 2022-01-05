# 删除链表中间的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-to-delete-中间链表/](https://www.geeksforgeeks.org/python-program-to-delete-middle-of-linked-list/)

给定一个单链表，删除链表的中间。例如，如果给定的链表是 1->2->3->4->5，那么链表应该被修改为 1->2->4->5

如果有偶数个节点，那么就会有两个中间节点，我们需要删除第二个中间元素。例如，如果给定的链表是 1->2->3->4->5->6，那么它应该被修改为 1->2->3->5->6。
如果输入链表为空，那么应该保持为空。

如果输入的链表有 1 个节点，那么这个节点应该被删除，并返回一个新的头。

**简单的解决方案:**思路是先统计链表中的节点数，然后用简单的删除过程删除第 n/2 个节点。

## 蟒蛇 3

```
# Python3 program to delete middle
# of a linked list

# Link list Node 
class Node:    
    def __init__(self):        
        self.data = 0
        self.next = None

# Count of nodes
def countOfNodes(head):
    count = 0    
    while (head != None):
        head = head.next
        count += 1

    return count

# Deletes middle node and returns
# head of the modified list
def deleteMid(head):

    # Base cases
    if (head == None):
        return None
    if (head.next == None):
        del head
        return None

    copyHead = head

    # Find the count of nodes
    count = countOfNodes(head)

    # Find the middle node
    mid = count // 2

    # Delete the middle node
    while (mid > 1):
        mid -= 1
        head = head.next

    # Delete the middle node
    head.next = head.next.next

    return copyHead

# A utility function to print
# a given linked list
def printList(ptr):
    while (ptr != None):
        print(ptr.data, 
              end = '->')
        ptr = ptr.next

    print('NULL')

# Utility function to create 
# a new node.
def newNode(data):
    temp = Node()
    temp.data = data
    temp.next = None
    return temp

# Driver Code
if __name__=='__main__':

    # Start with the empty list
    head = newNode(1)
    head.next = newNode(2)
    head.next.next = newNode(3)
    head.next.next.next = newNode(4)

    print("Given Linked List")
    printList(head)

    head = deleteMid(head)

    print("Linked List after deletion of middle")
    printList(head)

# This code is contributed by rutvik_56
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    链表需要两次遍历
*   **辅助空间:** O(1)。
    不需要额外的空间。

**高效解决方案:**
**方法:**上述解决方案需要链表的两次遍历。中间节点可以通过一次遍历删除。想法是使用两个指针，slow_ptr 和 fast_ptr。两个指针都从列表头开始。当 fast_ptr 到达终点时，slow_ptr 到达中间。这个思路和[这个](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)帖子的方法二用的是一样的。这篇文章的额外内容是跟踪前一个中间节点，这样中间节点就可以被删除了。

下面是实现。

## 蟒蛇 3

```
# Python3 program to delete the
# middle of a linked list

# Linked List Node
class Node:    
    def __init__(self, data):
        self.data = data
        self.next = None

# Create and handle list 
# operations
class LinkedList:    
    def __init__(self):

        # Head of the list
        self.head = None 

    # Add new node to the list end
    def addToList(self, data):        
        newNode = Node(data)
        if self.head is None:
            self.head = newNode
            return

        last = self.head

        while last.next:
            last = last.next

        last.next = newNode

    # Returns the list in string 
    # format
    def __str__(self):        
        linkedListStr = ""
        temp = self.head

        while temp:
            linkedListStr += str(temp.data) + "->"
            temp = temp.next

        return linkedListStr + "NULL"

    # Method deletes middle node
    def deleteMid(self):

        # Base cases
        if (self.head is None or 
            self.head.next is None):
            return

        # Initialize slow and fast pointers
        # to reach middle of linked list
        slow_Ptr = self.head
        fast_Ptr = self.head

        # Find the middle and previous of 
        # middle
        prev = None

        # To store previous of slow pointer
        while (fast_Ptr is not None and 
               fast_Ptr.next is not None):
            fast_Ptr = fast_Ptr.next.next
            prev = slow_Ptr
            slow_Ptr = slow_Ptr.next

        # Delete the middle node
        prev.next = slow_Ptr.next

# Driver code
linkedList = LinkedList()

linkedList.addToList(1)
linkedList.addToList(2)
linkedList.addToList(3)
linkedList.addToList(4)

print("Given Linked List")
print(linkedList)

linkedList.deleteMid()

print("Linked List after deletion of middle")
print(linkedList)
# This code is contributed by Debidutta Rath
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历链表一次
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

详情请参考[删除链表中间](https://www.geeksforgeeks.org/delete-middle-of-linked-list/)整篇文章！