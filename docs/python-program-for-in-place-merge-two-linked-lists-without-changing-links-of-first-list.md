# 就地合并两个链表而不改变第一个链表的链接的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-in-place-merge-two-link-list-first-list-不变链接/](https://www.geeksforgeeks.org/python-program-for-in-place-merge-two-linked-lists-without-changing-links-of-first-list/)

给定两个排序的单链表，每个链表有 n 和 m 个元素，用常数空间合并它们。首先，两个列表中的 n 个最小元素应该成为第一个列表的一部分，其余元素应该成为第二个列表的一部分。应保持有序。我们不允许更改第一个链表的指针。

**示例:**

```
Input:
First List: 2->4->7->8->10
Second List: 1->3->12

Output: 
First List: 1->2->3->4->7
Second List: 8->10->12
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
如果允许我们更改第一个链表的指针，问题就变得非常简单了。如果允许我们改变链接，我们可以简单地做一些事情，比如合并排序算法的合并。我们将前 n 个最小的元素分配给第一个链表，其中 n 是第一个链表中的元素数，其余的分配给第二个链表。我们可以在 O(m + n)时间和 O(1)空间内实现这一点，但这种解决方案违反了我们不能更改第一个列表的链接的要求。

这个问题变得有点棘手，因为我们不允许更改第一个链表中的指针。这个想法类似于[这篇](https://www.geeksforgeeks.org/merge-two-sorted-arrays-o1-extra-space/)的帖子，但是由于我们得到了一个单链表，我们不能向后处理 LL2 的最后一个元素。

想法是对于 LL1 的每个元素，我们将其与 LL2 的第一个元素进行比较。如果 LL1 的元素比 LL2 的第一个元素大，那么我们交换涉及的两个元素。为了保持 LL2 有序，我们需要将 LL2 的第一个元素放在正确的位置。我们可以通过遍历 LL2 一次并纠正指针来发现不匹配。

下面是这个想法的实现。

## 蟒蛇 3

```
# Python3 program to merge two sorted linked 
# lists without using any extra space and 
# without changing links of first list

# Structure for a linked list node 
class Node:    
    def __init__(self):        
        self.data = 0
        self.next = None

# Given a reference (pointer to pointer) to 
# the head of a list and an int, push a new
# node on the front of the list. 
def push(head_ref, new_data):

    # Allocate node 
    new_node = Node()

    # Put in the data  
    new_node.data  = new_data

    # Link the old list off the 
    # new node 
    new_node.next = (head_ref)

    # Move the head to point to 
    # the new node 
    (head_ref) = new_node
    return head_ref

# Function to merge two sorted linked lists
# LL1 and LL2 without using any extra space.
def mergeLists(a, b):

    # Run till either one of a 
    # or b runs out
    while (a and b):

        # For each element of LL1, compare
        # it with first element of LL2.
        if (a.data > b.data):

            # Swap the two elements involved
            # if LL1 has a greater element
            a.data, b.data = b.data, a.data

            temp = b

            # To keep LL2 sorted, place first
            # element of LL2 at its correct place
            if (b.next and b.data > b.next.data):
                b = b.next
                ptr = b
                prev = None

                # Find mismatch by traversing the
                # second linked list once
                while (ptr and ptr.data < temp.data):
                    prev = ptr
                    ptr = ptr.next

                # Correct the pointers
                prev.next = temp
                temp.next = ptr

        # Move LL1 pointer to next element
        a = a.next

# Function to print the linked link
def printList(head):
    while (head):
        print(head.data, end = '->')
        head = head.next

    print('NULL')

# Driver code
if __name__=='__main__':    
    a = None
    a = push(a, 10)
    a = push(a, 8)
    a = push(a, 7)
    a = push(a, 4)
    a = push(a, 2)

    b = None
    b = push(b, 12)
    b = push(b, 3)
    b = push(b, 1)

    mergeLists(a, b)

    print("First List: ", 
           end = '')
    printList(a)

    print("Second List: ", 
           end = '')
    printList(b)
# This code is contributed by rutvik_56
```

**输出:**

```
First List: 1->2->3->4->7->NULL
Second List: 8->10->12->NULL
```

**时间复杂度:** O(mn)

更多详情请参考[原位合并两个链表不改变第一个链表](https://www.geeksforgeeks.org/in-place-merge-two-linked-list-without-changing-links-of-first-list/)的链接的完整文章！