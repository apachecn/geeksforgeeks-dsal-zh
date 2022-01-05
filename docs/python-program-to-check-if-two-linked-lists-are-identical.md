# 检查两个链表是否相同的 Python 程序

> 原文:[https://www . geesforgeks . org/python-程序检查两个链表是否相同/](https://www.geeksforgeeks.org/python-program-to-check-if-two-linked-lists-are-identical/)

当两个链表具有相同的数据并且数据的排列也相同时，它们是相同的。例如，链表 a (1->2->3)和 b(1->2->3)是相同的。。编写一个函数来检查给定的两个链表是否相同。

**方法 1(迭代):**
要确定两个列表是否相同，我们需要同时遍历两个列表，遍历时需要比较数据。

## 蟒蛇 3

```
# An iterative Java program to check if 
# two linked lists are identical or not 

# Linked list Node 
class Node: 
    def __init__(self, d):
        self.data = d
        self.next = None

class LinkedList:
    def __init__(self):

        # Head of list 
        self.head = None 

    # Returns true if linked lists a 
    # and b are identical, otherwise false 
    def areIdentical(self, listb): 
        a = self.head
        b = listb.head

        while (a != None and b != None): 
            if (a.data != b.data): 
                return False

            # If we reach here, then a and b 
            # are not null and their data is 
            # same, so move to next nodes 
            # in both lists 
            a = a.next
            b = b.next

        # If linked lists are identical, 
        # then 'a' and 'b' must be null
        # at this point. 
        return (a == None and b == None) 

    # UTILITY FUNCTIONS TO TEST fun1() 
    # and fun2() 
    # Given a reference (pointer to pointer) 
    # to the head of a list and an int, push 
    # a new node on the front of the list. 
    def push(self, new_data):

        # 1 & 2: Allocate the Node & 
        # Put in the data
        new_node = Node(new_data) 

        # 3\. Make next of new Node as head 
        new_node.next = self.head 

        # 4\. Move the head to point to 
        # new Node 
        self.head = new_node

# Driver Code
llist1 = LinkedList() 
llist2 = LinkedList() 

# The constructed linked lists are : 
# llist1: 3->2->1 
# llist2: 3->2->1 
llist1.push(1) 
llist1.push(2) 
llist1.push(3) 
llist2.push(1) 
llist2.push(2) 
llist2.push(3) 

if (llist1.areIdentical(llist2) == True): 
    print("Identical ")
else:
    print("Not identical ")
# This code is contributed by Prerna Saini
```

**输出:**

```
Identical
```

**方法 2(递归):**
递归求解代码比迭代代码干净得多。然而，您可能不想将递归版本用于生产代码，因为它将使用与列表长度成比例的堆栈空间。

## 蟒蛇 3

```
# A recursive Python3 function to check 
# if two linked lists are identical 
# or not 
def areIdentical(a, b): 

    # If both lists are empty 
    if (a == None and b == None): 
        return True

    # If both lists are not empty, 
    # then data of current nodes must 
    # match, and same should be recursively 
    # true for rest of the nodes. 
    if (a != None and b != None): 
        return ((a.data == b.data) and 
                 areIdentical(a.next, b.next)) 

    # If we reach here, then one of the lists 
    # is empty and other is not 
    return False
# This code is contributed by Princi Singh
```

**时间复杂度:** O(n)对于迭代和递归版本。n 是 a 和 b 中较小列表的长度。

更多详情请参考[完全相同链表](https://www.geeksforgeeks.org/identical-linked-lists/)的完整文章！