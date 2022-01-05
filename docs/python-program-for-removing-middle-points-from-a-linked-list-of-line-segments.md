# 从线段链表中删除中间点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于从线段链表中移除中间点的程序/](https://www.geeksforgeeks.org/python-program-for-removing-middle-points-from-a-linked-list-of-line-segments/)

给定相邻点形成垂直线或水平线的坐标链表。从链表中删除水平线或垂直线中间的点。
示例:

```
Input:  (0,10)->(1,10)->(5,10)->(7,10)
                                  |
                                (7,5)->(20,5)->(40,5)
Output: Linked List should be changed to following
        (0,10)->(7,10)
                  |
                (7,5)->(40,5) 
The given linked list represents a horizontal line from (0,10) 
to (7, 10) followed by a vertical line from (7, 10) to (7, 5), 
followed by a horizontal line from (7, 5) to (40, 5).

Input:     (2,3)->(4,3)->(6,3)->(10,3)->(12,3)
Output: Linked List should be changed to following
    (2,3)->(12,3) 
There is only one vertical line, so all middle points are removed.
```

来源:[微软面试体验](https://www.geeksforgeeks.org/microsoft-interview-experience-set-41-campus/)

其思想是跟踪当前节点、下一个节点和下一个节点。当下一个节点与下一个节点相同时，继续删除下一个节点。在这个完整的过程中，我们需要关注指针的移动并检查空值。
以下是上述想法的实现。

## 计算机编程语言

```
# Python program to remove middle points in a linked list of
# line segments,
class LinkedList(object):
    def __init__(self):
        self.head = None

    # Linked list Node
    class Node(object):
        def __init__(self, x, y):
            self.x = x
            self.y = y
            self.next = None

    # This function deletes middle nodes in a sequence of
    # horizontal and vertical line segments represented
    # by linked list.
    def deleteMiddle(self):
        # If only one node or no node...Return back
        if self.head == None or self.head.next == None or self.head.next.next == None:
            return self.head
        Next = self.head.next
        NextNext = Next.next
        # check if this is vertical or horizontal line
        if self.head.x == Next.x:
            # Find middle nodes with same value as x and
            # delete them.
            while NextNext != None and Next.x == NextNext.x:
                self.head.next = Next.next
                Next.next = None
                # Update NextNext for the next iteration
                Next = NextNext
                NextNext = NextNext.next
        elif self.head.y == Next.y:
            # find middle nodes with same value as y and
            # delete them
            while NextNext != None and Next.y == NextNext.y:
                self.head.next = Next.next
                Next.next = None
                # Update NextNext for the next iteration
                Next = NextNext
                NextNext = NextNext.next
        else:
            # Adjacent points should have same x or same y
            print "Given list is not valid"
            return None
        # recur for other segment
        # temporarily store the head and move head forward.
        temp = self.head
        self.head = self.head.next
        # call deleteMiddle() for next segment
        self.deleteMiddle()
        # restore head
        self.head = temp
        # return the head
        return self.head

    # Given a reference (pointer to pointer) to the head
    # of a list and an int, push a new node on the front
    # of the list.
    def push(self, x, y):
        # 1 & 2: Allocate the Node &
        # Put in the data
        new_node = self.Node(x, y)
        # 3\. Make next of new Node as head
        new_node.next = self.head
        # 4\. Move the head to point to new Node
        self.head = new_node

    def printList(self):
        temp = self.head
        while temp != None:
            print "(" + str(temp.x) + "," + str(temp.y) + ")->",
            temp = temp.next
        print ''

# Driver program
llist = LinkedList()
llist.push(40,5)
llist.push(20,5)
llist.push(10,5)
llist.push(10,8)
llist.push(10,10)
llist.push(3,10)
llist.push(1,10)
llist.push(0,10)

print "Given list"
llist.printList()

if llist.deleteMiddle() != None:
    print "Modified Linked List is"
    llist.printList()

# This code is contributed by BHAVYA JAIN
```

**输出:**

```
Given Linked List:
(0,10)-> (1,10)-> (3,10)-> (10,10)-> (10,8)-> (10,5)-> (20,5)-> (40,5)->
Modified Linked List:
(0,10)-> (10,10)-> (10,5)-> (40,5)-> 
```

上述解决方案的时间复杂度是 O(n)，其中 n 是给定链表中的节点数。
**练习:**
上面的代码是递归的，为同样的问题写一个迭代代码。请参见下面的解决方案。
[线段链表中去除中间点的迭代方法](https://www.geeksforgeeks.org/iterative-approach-for-removing-middle-points-in-a-linked-list-of-line-segements/)
请参考完整的文章[给定线段链表，去除中间点](https://www.geeksforgeeks.org/given-linked-list-line-segments-remove-middle-points/)了解更多细节！