# 用于链表合并排序的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-merge-sort-of-linked-list/](https://www.geeksforgeeks.org/python-program-for-merge-sort-of-linked-lists/)

[合并排序](http://en.wikipedia.org/wiki/Merge_sort)通常是对链表进行排序的首选。链表缓慢的随机访问性能使得其他一些算法(如 quicksort)性能很差，而其他算法(如 heapsort)则完全不可能。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

让 head 是要排序的链表的第一个节点，headRef 是指向 head 的指针。请注意，我们需要引用 MergeSort()中的 head，因为下面的实现会更改下一个链接以对链表进行排序(而不是节点处的数据)，因此如果原始 head 处的数据不是链表中的最小值，就必须更改 head 节点。

```
MergeSort(headRef)
1) If the head is NULL or there is only one element in the Linked List 
    then return.
2) Else divide the linked list into two halves.  
      FrontBackSplit(head, &a, &b); /* a and b are two halves */
3) Sort the two halves a and b.
      MergeSort(a);
      MergeSort(b);
4) Merge the sorted a and b (using SortedMerge() discussed here) 
   and update the head pointer using headRef.
     *headRef = SortedMerge(a, b);
```

## 蟒蛇 3

```
# Python3 program to merge sort of linked list

# create Node using class Node.
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    # push new value to linked list
    # using append method
    def append(self, new_value):

        # Allocate new node
        new_node = Node(new_value)

        # if head is None, initialize it to new node
        if self.head is None:
            self.head = new_node
            return
        curr_node = self.head
        while curr_node.next is not None:
            curr_node = curr_node.next

        # Append the new node at the end
        # of the linked list
        curr_node.next = new_node

    def sortedMerge(self, a, b):
        result = None

        # Base cases
        if a == None:
            return b
        if b == None:
            return a

        # pick either a or b and recur..
        if a.data <= b.data:
            result = a
            result.next = self.sortedMerge(a.next, b)
        else:
            result = b
            result.next = self.sortedMerge(a, b.next)
        return result

    def mergeSort(self, h):

        # Base case if head is None
        if h == None or h.next == None:
            return h

        # get the middle of the list 
        middle = self.getMiddle(h)
        nexttomiddle = middle.next

        # set the next of middle node to None
        middle.next = None

        # Apply mergeSort on left list 
        left = self.mergeSort(h)

        # Apply mergeSort on right list
        right = self.mergeSort(nexttomiddle)

        # Merge the left and right lists 
        sortedlist = self.sortedMerge(left, right)
        return sortedlist

    # Utility function to get the middle 
    # of the linked list 
    def getMiddle(self, head):
        if (head == None):
            return head

        slow = head
        fast = head

        while (fast.next != None and 
               fast.next.next != None):
            slow = slow.next
            fast = fast.next.next

        return slow

# Utility function to print the linked list 
def printList(head):
    if head is None:
        print(' ')
        return
    curr_node = head
    while curr_node:
        print(curr_node.data, end = " ")
        curr_node = curr_node.next
    print(' ')

# Driver Code
if __name__ == '__main__':
    li = LinkedList()

    # Let us create a unsorted linked list
    # to test the functions created. 
    # The list shall be a: 2->3->20->5->10->15 
    li.append(15)
    li.append(10)
    li.append(5)
    li.append(20)
    li.append(3)
    li.append(2)

    # Apply merge Sort 
    li.head = li.mergeSort(li.head)
    print ("Sorted Linked List is:")
    printList(li.head)

# This code is contributed by Vikas Chitturi
```

**Output:** 

```
Sorted Linked List is: 
2 3 5 10 15 20
```