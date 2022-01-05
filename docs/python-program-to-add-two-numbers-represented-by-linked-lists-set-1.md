# Python 程序添加两个链表表示的数字-集合 1

> 原文:[https://www . geesforgeks . org/python-program-to-add-two-numbers-由链表表示-set-1/](https://www.geeksforgeeks.org/python-program-to-add-two-numbers-represented-by-linked-lists-set-1/)

给定两个由两个列表表示的数字，编写一个返回求和列表的函数。求和列表是两个输入数字相加的列表表示。

**例**:

```
Input: 
List1: 5->6->3 // represents number 563 
List2: 8->4->2 // represents number 842 
Output: 
Resultant list: 1->4->0->5 // represents number 1405 
Explanation: 563 + 842 = 1405

Input: 
List1: 7->5->9->4->6 // represents number 75946
List2: 8->4 // represents number 84
Output: 
Resultant list: 7->6->0->3->0// represents number 76030
Explanation: 75946+84=76030

```

**接近**:遍历两个列表，逐个选择两个列表的节点，并添加值。如果总和大于 10，则进位为 1 并减少总和。如果一个列表中的元素比另一个列表中的多，则认为该列表的剩余值为 0。

**步骤为:**

1.  从头到尾遍历两个链表
2.  将相应链接列表中的两位数字相加。
3.  如果其中一个列表已到达末尾，则取 0 作为它的数字。
4.  继续下去，直到两个列表都结束。
5.  如果两位数之和大于 9，则将进位设置为 1，将当前数字设置为*和% 10*

下面是这个方法的实现。

## 计算机编程语言

```
# Python program to add two numbers 
# represented by linked list

# Node class
class Node:

    # Constructor to initialize the 
    # node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Function to insert a new node at 
    # the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Add contents of two linked lists and 
    # return the head node of resultant list
    def addTwoLists(self, first, second):
        prev = None
        temp = None
        carry = 0

        # While both list exists
        while(first is not None or 
              second is not None):

            # Calculate the value of next digit 
            # in resultant list
            # The next digit is sum of following 
            # things
            # (i) Carry
            # (ii) Next digit of first list (if 
            # there is a next digit)
            # (iii) Next digit of second list (if 
            # there is a next digit)
            fdata = 0 if first is None else first.data
            sdata = 0 if second is None else second.data
            Sum = carry + fdata + sdata

            # Update carry for next calculation
            carry = 1 if Sum >= 10 else 0

            # Update sum if it is greater than 10
            Sum = Sum if Sum < 10 else Sum % 10

            # Create a new node with sum as data
            temp = Node(Sum)

            # if this is the first node then set 
            # it as head of resultant list
            if self.head is None:
                self.head = temp
            else:
                prev.next = temp

            # Set prev for next insertion
            prev = temp

            # Move first and second pointers to 
            # next nodes
            if first is not None:
                first = first.next
            if second is not None:
                second = second.next

        if carry > 0:
            temp.next = Node(carry)

    # Utility function to print the 
    # linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

# Driver code
first = LinkedList()
second = LinkedList()

# Create first list
first.push(6)
first.push(4)
first.push(9)
first.push(5)
first.push(7)
print "First List is ",
first.printList()

# Create second list
second.push(4)
second.push(8)
print "
Second List is ",
second.printList()

# Add the two lists and see result
res = LinkedList()
res.addTwoLists(first.head, second.head)
print "
Resultant list is ",
res.printList()
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**输出:**

```
First List is 7 5 9 4 6 
Second List is 8 4 
Resultant list is 5 0 0 5 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m + n)，其中 m 和 n 分别是第一和第二列表中的节点数。
    列表只需遍历一次。
*   **空间复杂度:** O(m + n)。
    需要一个临时链表来存储输出号

相关文章:[添加两个链表表示的数字|集合 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/)

更多详情请参考[整篇文章添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/) ！