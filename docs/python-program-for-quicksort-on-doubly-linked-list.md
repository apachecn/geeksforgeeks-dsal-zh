# 双链表快速排序的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-quick sort-on-double-link-list/](https://www.geeksforgeeks.org/python-program-for-quicksort-on-doubly-linked-list/)

以下是数组的[快速排序](http://en.wikipedia.org/wiki/Quicksort)的典型递归实现。该实现使用最后一个元素作为透视。

## 蟒蛇 3

```
"""A typical recursive implementation of Quicksort for array """

""" This function takes last element as pivot, 
   places the pivot element at its correct 
   position in sorted array, and places all 
   smaller (smaller than pivot) to left of
   pivot and all greater elements to right 
   of pivot 
"""

"""
 i --> is the first index in the array
 x --> is the last index in the array
 tmp --> is a temporary variable for swapping values (integer)
"""
# array arr, integer l, integer h
def  partition (arr, l, h):
    x = arr[h]
    i = (l - 1)
    for j in range(l, h):
        if (arr[j] <= x):
            i +=1
            tmp = arr[i]
            arr[i] = arr[j]
            arr[j] = tmp

    tmp = arr[i + 1]
    arr[i + 1] = arr[h]
    arr[h] = tmp
    return(i + 1)

"""
A --> Array to be sorted,
l --> Starting index, 
h --> Ending index
"""

# array A, integer l, integer h
def quickSort(A, l, h):
    if (l < h):
        p = partition(A, l, h) # pivot index
        quickSort(A, l, p - 1) # left
        quickSort(A, p + 1, h) # right

# This code is contributed by humphreykibet.
```

**链表可以用同样的算法吗？**
下面是双链表的 C++实现。思路很简单，我们先找出指向最后一个节点的指针。一旦我们有了指向最后一个节点的指针，我们就可以使用指向链表的第一个和最后一个节点的指针来递归地对链表进行排序，类似于上面的递归函数，在那里我们传递第一个和最后一个数组元素的索引。链表的分区函数也类似于数组的分区。它不是返回透视元素的索引，而是返回指向透视元素的指针。在下面的实现中，quickSort()只是一个包装函数，主要的递归函数是 _quickSort()，对于数组的实现类似于 quickSort()。

![](img/907e6783a6130c711cfa83c52cb7210e.png)

## 蟒蛇 3

```
# A Python program to sort a linked list using Quicksort
head = None

# a node of the doubly linked list
class Node:
    def __init__(self, d):
        self.data = d
        self.next = None
        self.prev = None

# A utility function to find last node of linked list
def lastNode(node):
    while(node.next != None):
            node = node.next;
    return node;

# Considers last element as pivot, places the pivot element at its
#   correct position in sorted array, and places all smaller (smaller than
#   pivot) to left of pivot and all greater elements to right of pivot 
def partition(l, h):

    # set pivot as h element
        x = h.data;

        # similar to i = l-1 for array implementation
        i = l.prev;

        j = l

        # Similar to "for (int j = l; j <= h- 1; j++)"
        while(j != h):
            if(j.data <= x):

                # Similar to i++ for array
                i = l if(i == None) else i.next;

                temp = i.data;
                i.data = j.data;
                j.data = temp;
            j = j.next

        i = l if (i == None) else i.next;  # Similar to i++
        temp = i.data;
        i.data = h.data;
        h.data = temp;
        return i;

# A recursive implementation of quicksort for linked list 
def _quickSort(l,h):
    if(h != None and l != h and l != h.next):
            temp = partition(l, h);
            _quickSort(l,temp.prev);
            _quickSort(temp.next, h);

# The main function to sort a linked list. It mainly calls _quickSort()
def quickSort(node):

    # Find last node
        head = lastNode(node);

        # Call the recursive QuickSort
        _quickSort(node,head);

# A utility function to print contents of arr
def printList(head):
    while(head != None):
            print(head.data, end=" ");
            head = head.next;

# Function to insert a node at the beginning of the Doubly Linked List 
def push(new_Data):
    global head;
    new_Node = Node(new_Data);     # allocate node 

    # if head is null, head = new_Node
    if(head == None):
        head = new_Node;
        return;

    # link the old list off the new node 
    new_Node.next = head;

    # change prev of head node to new node 
    head.prev = new_Node;

    # since we are adding at the beginning, prev is always NULL 
    new_Node.prev = None;

    # move the head to point to the new node 
    head = new_Node;

# Driver program to test above function 
push(5);
push(20);
push(4);
push(3);
push(30);

print("Linked List before sorting ");
printList(head);
print("
Linked List after sorting");
quickSort(head);
printList(head);

# This code is contributed by _saurabh_jaiswal
```

**输出:**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

**时间复杂度:**上述实现的时间复杂度与快速排序()对于数组的时间复杂度相同。最坏的情况下需要 O(n^2 时间，一般情况下和最好的情况下都需要 0。最坏的情况发生在链表已经排序的时候。
我们能为链表实现随机快速排序吗？
只有当我们可以选择一个固定点作为轴心时(就像上面实现中的最后一个元素)，链表才能实现快速排序。随机快速排序不能通过选择随机透视来有效地实现链表。

详情请参考[双链表快速排序](https://www.geeksforgeeks.org/quicksort-for-linked-list/)整篇文章！