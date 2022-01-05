# 寻找两个排序链表交集的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-寻找两个排序链表交集的程序/](https://www.geeksforgeeks.org/python-program-for-finding-intersection-of-two-sorted-linked-lists/)

给定两个按递增顺序排序的列表，创建并返回一个表示这两个列表交集的新列表。新的列表应该有自己的记忆——原来的列表不应该改变。

**示例:**

```
Input: 
First linked list: 1->2->3->4->6
Second linked list be 2->4->6->8, 
Output: 2->4->6.
The elements 2, 4, 6 are common in 
both the list so they appear in the 
intersection list. 

Input: 
First linked list: 1->2->3->4->5
Second linked list be 2->3->4, 
Output: 2->3->4
The elements 2, 3, 4 are common in 
both the list so they appear in the 
intersection list.
```

**<u>方法</u> :** 使用伪节点。
**方法:**
想法是在结果列表的开头使用一个临时伪节点。指针尾部总是指向结果列表中的最后一个节点，因此可以轻松添加新节点。伪节点最初给尾部一个内存空间来指向。这个虚拟节点是有效的，因为它只是临时的，并且是在堆栈中分配的。循环继续，从“a”或“b”中删除一个节点，并将其添加到尾部。当遍历给定的列表时，结果是伪的。接下来，当从虚拟的下一个节点分配值时。如果两个元素相等，则移除两个元素并将元素插入尾部。否则删除两个列表中较小的元素。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to implement
# the above approach
# Link list node 
class Node:
    def __init__(self):   
        self.data = 0
        self.next = None

''' This solution uses the temporary
    dummy to build up the result list '''
def sortedIntersect(a, b):
    dummy = Node()
    tail = dummy;
    dummy.next = None;

    ''' Once one or the other 
        list runs out -- we're done '''
    while (a != None and b != None):
        if (a.data == b.data):
            tail.next = push((tail.next), 
                              a.data);
            tail = tail.next;
            a = a.next;
            b = b.next;

        # Advance the smaller list
        elif(a.data < b.data):
            a = a.next;
        else:
            b = b.next;    
    return (dummy.next);

''' UTILITY FUNCTIONS '''
''' Function to insert a node at 
    the beginning of the linked list '''
def push(head_ref, new_data):

    # Allocate node 
    new_node = Node()

    # Put in the data  
    new_node.data = new_data;

    # Link the old list off the new node 
    new_node.next = (head_ref);

    # Move the head to point to the
    # new node 
    (head_ref) = new_node;    
    return head_ref

''' Function to print nodes in 
    a given linked list '''
def printList(node):
    while (node != None):
        print(node.data, end = ' ')
        node = node.next;

# Driver code
if __name__=='__main__':

    # Start with the empty lists 
    a = None;
    b = None;
    intersect = None;

    ''' Let us create the first sorted 
        linked list to test the functions
        Created linked list will be 
        1.2.3.4.5.6 '''
    a = push(a, 6);
    a = push(a, 5);
    a = push(a, 4);
    a = push(a, 3);
    a = push(a, 2);
    a = push(a, 1);

    ''' Let us create the second sorted 
        linked list. Created linked list 
        will be 2.4.6.8 '''
    b = push(b, 8);
    b = push(b, 6);
    b = push(b, 4);
    b = push(b, 2);

    # Find the intersection two linked lists 
    intersect = sortedIntersect(a, b);

    print("Linked list containing common items of a & b ");
    printList(intersect);
# This code is contributed by rutvik_56.
```

**输出:**

```
Linked list containing common items of a & b 
2 4 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m+n)，其中 m 和 n 分别是第一和第二链表中的节点数。
    只需要遍历列表一次。
*   **辅助空间:** O(min(m，n))。
    输出列表最多可以存储(m，n)个节点。

更多详情请参考完整文章[两个排序链表的交集](https://www.geeksforgeeks.org/intersection-of-two-sorted-linked-lists/)！