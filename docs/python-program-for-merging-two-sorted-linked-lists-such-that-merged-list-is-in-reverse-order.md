# Python 程序，用于合并两个已排序的链表，以使合并的链表处于相反的顺序

> 原文:[https://www . geeksforgeeks . org/python-用于合并的程序-两个排序的链表-这样-合并后的列表以相反的顺序排列/](https://www.geeksforgeeks.org/python-program-for-merging-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/)

给定两个按升序排序的链表。将它们合并，使结果列表按降序(逆序)排列。

**示例:**

```
**Input:**  a: 5->10->15->40
        b: 2->3->20 
**Output:** res: 40->20->15->10->5->3->2

**Input:**  a: NULL
        b: 2->3->20 
**Output:** res: 20->3->2
```

**一个**简单的解决方法**就是做以下几点。
1) [逆转首榜‘a’](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。
2) [反转第二个列表‘b’](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。
3) [合并两个反向列表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)。
另一个简单的解决方案是首先合并两个列表，然后反转合并的列表。
上述两种解决方案都需要链表的两次遍历。**

****没有反向，O(1)辅助空间(原地)，两个列表只有一次遍历，如何求解？**
思路是遵循合并风格流程。将结果列表初始化为空。从头到尾遍历两个列表。比较两个列表的当前节点，并在结果列表的开头插入两个中较小的一个。**

```
1) Initialize result list as empty: res = NULL.
2) Let 'a' and 'b' be heads first and second lists respectively.
3) While (a != NULL and b != NULL)
    a) Find the smaller of two (Current 'a' and 'b')
    b) Insert the smaller value node at the front of the result.
    c) Move ahead in the list of the smaller nodes. 
4) If 'b' becomes NULL before 'a', insert all nodes of 'a' 
   into the result list at the beginning.
5) If 'a' becomes NULL before 'b', insert all nodes of 'a' 
   into result list at the beginning. 
```

**下面是上述解决方案的实现。**

## **蟒蛇 3**

```
# Given two sorted non-empty linked lists. 
# Merge them in such a way that the result 
# list will be in reverse order. Reversing 
# of linked list is not allowed. Also,
# extra space should be O(1) 

# Node of a linked list 
class Node: 
    def __init__(self, next = None, 
                 data = None): 
        self.next = next
        self.data = data 

# Given two non-empty linked lists 
# 'a' and 'b'
def SortedMerge(a,b):

    # If both lists are empty
    if (a == None and b == None):
        return None

    # Initialize head of the 
    # resultant list
    res = None

    # Traverse both lists while both 
    # of then have nodes.
    while (a != None and b != None):

        # If a's current value is smaller 
        # or equal to b's current value.
        if (a.key <= b.key):

            # Store next of current Node 
            # in first list
            temp = a.next

            # Add 'a' at the front of 
            # resultant list
            a.next = res
            res = a

            # Move ahead in first list
            a = temp

        # If a's value is greater. Below steps 
        # are similar to above (Only 'a' is 
        # replaced with 'b')
        else:        
            temp = b.next
            b.next = res
            res = b
            b = temp

    # If second list reached end, but first 
    # list has nodes. Add remaining nodes of 
    # first list at the front of result list
    while (a != None):    
        temp = a.next
        a.next = res
        res = a
        a = temp

    # If first list reached end, but second 
    # list has node. Add remaining nodes of 
    # first list at the front of result list
    while (b != None):

        temp = b.next
        b.next = res
        res = b
        b = temp

    return res

# Function to print Nodes in a given 
# linked list 
def printList(Node):

    while (Node != None):

        print( Node.key, end = " ")
        Node = Node.next

# Utility function to create a new 
# node with given key 
def newNode(key):
    temp = Node()
    temp.key = key
    temp.next = None
    return temp

# Driver code
# Start with the empty list 
res = None

# Let us create two sorted linked lists 
# to test the above functions. Created 
# lists shall be
#     a: 5.10.15
#     b: 2.3.20 
a = newNode(5)
a.next = newNode(10)
a.next.next = newNode(15)

b = newNode(2)
b.next = newNode(3)
b.next.next = newNode(20)

print("List A before merge: ")
printList(a)

print("
List B before merge: ")
printList(b)

# Merge 2 increasing order LLs 
# in descresing order 
res = SortedMerge(a, b)

print("
Merged Linked List is: ")
printList(res)
# This code is contributed by Arnab Kundu
```

****输出:****

```
List A before merge: 
5 10 15 
List B before merge: 
2 3 20 
Merged Linked List is: 
20 15 10 5 3 2 
```

**这个解决方案只遍历两个列表一次，不需要反向，就地工作。
本文由[T2T4【穆罕默德·拉基布】供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息](https://www.linkedin.com/in/mohammed-raqeeb-soudagar-951b345a)** 

**更多详情请参考[完整文章合并两个排序链表，合并后的链表顺序相反](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/)！**