# 用于以之字形方式重新排列链表的 Python 程序

> 原文:[https://www . geeksforgeeks . org/python-program-for-重排-一个以之字形排列的链表/](https://www.geeksforgeeks.org/python-program-for-rearranging-a-linked-list-in-zig-zag-fashion/)

给定一个链表，重新排列它，使得转换后的列表应该是 a < b > c < d > e < f …的形式，其中 a，b，c…是链表的连续数据节点。

**示例:**

```
Input:  1->2->3->4
Output: 1->3->2->4 
Explanation: 1 and 3 should come first before 2 and 4 in
             zig-zag fashion, So resultant linked-list 
             will be 1->3->2->4\. 

Input:  11->15->20->5->10
Output: 11->20->5->15->10 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/probfunc-page.php?pid=700085)

一个简单的方法是使用合并排序对链表进行排序，然后交换替换，但是这需要 O(n Log n)的时间复杂度。这里 n 是链表中的元素个数。

一种需要 O(n)时间的**有效方法是，使用类似于冒泡排序的单次扫描，然后维护一个标志来表示我们当前所处的顺序()。如果当前的两个元素不是按这个顺序排列的，那么交换这些元素，否则就不是。关于对换顺序的详细说明，请参考[本](http://geeksquiz.com/converting-an-array-of-integers-into-zig-zag-fashion/)。**

遵循" href = " http://geek squiz . com/converting-a-array-of-integers-in-zig-zag-fashion/" >这一节，了解交换顺序的详细说明。

## 计算机编程语言

```
# Python code to rearrange linked list 
# in zig zac fashion

# Node class 
class Node: 

    # Constructor to initialize 
    # the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# This function distributes the Node 
# in zigzag fashion
def zigZagList(head):

    # If flag is true, then next node 
    # should be greater in the desired 
    # output.
    flag = True

    # Traverse linked list starting 
    # from head.
    current = head
    while (current.next != None):

        # "<" relation expected
        if (flag): 

            # If we have a situation like 
            # A > B > C where A, B and C 
            # are consecutive Nodes in list
            # we get A > B < C by swapping B
            # and C 
            if (current.data > 
                current.next.data):
                t = current.data
                current.data = current.next.data
                current.next.data = t

        # ">" relation expected
        else :

            # If we have a situation like 
            # A < B < C where A, B and C 
            # are consecutive Nodes in list we
            # get A < C > B by swapping B and C 
            if (current.data < 
                current.next.data):
                t = current.data
                current.data = current.next.data
                current.next.data = t

        current = current.next
        if(flag):

            # flip flag for reverse checking 
            flag = False 
        else:
            flag = True
    return head

# Function to insert a Node in 
# the linked list at the beginning.
def push(head, k):

    tem = Node(0)
    tem.data = k
    tem.next = head
    head = tem
    return head

# Function to display Node of 
# linked list.
def display(head):
    curr = head
    while (curr != None): 
        print(curr.data, 
              "->", end =" ")
        curr = curr.next

    print("None")

# Driver code
head = None

# create a list 4 -> 3 -> 7 -> 
# 8 -> 6 -> 2 -> 1
# answer should be -> 3 7 4 
# 8 2 6 1
head = push(head, 1)
head = push(head, 2)
head = push(head, 6)
head = push(head, 8)
head = push(head, 7)
head = push(head, 3)
head = push(head, 4)

print("Given linked list ")
display(head)

head = zigZagList(head)

print("Zig Zag Linked list ")
display(head)
# This code is contributed by Arnab Kundu
```

**输出:**

```
Given linked list 
4->3->7->8->6->2->1->NULL
Zig Zag Linked list 
3->7->4->8->2->6->1->NULL
```

**另一种方法:**
在上面的代码中，push 函数推链表前面的节点，代码可以很容易地修改为推链表末尾的节点。另一件需要注意的事情是，两个节点之间的数据交换是通过按值交换而不是按链接交换来完成的，为了简单起见，有关按链接交换的技术，请参见[本](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)。

这也可以递归完成。想法保持不变，让我们假设标志的值决定了比较当前元素需要检查的条件。因此，如果标志为 0(或假)，则当前元素应该小于下一个元素，如果标志为 1(或真)，则当前元素应该大于下一个元素。如果没有，交换节点的值。

## 蟒蛇 3

```
# Python program for the above approach
# Node class
class Node:

    # Constructor to initialize the 
    # node object
    def __init__(self, data):
        self.data = data
        self.next = None
head = None

# Point Linked List
def printLL():
    t = head
    while (t != None):
        print(t.data, end = " ->")
        t = t.next
    print()

# Swap both nodes
def swap(a,b):
    if(a == None or 
       b == None):
        return
    temp = a.data
    a.data = b.data
    b.data = temp

# Rearrange the linked list
# in zig zag way
def zigZag(node, flag):
    if(node == None or 
       node.next == None):
        return node
    if (flag == 0):
        if (node.data > 
            node.next.data):
            swap(node, node.next)
        return zigZag(node.next, 1)

    else:
        if (node.data < 
            node.next.data):
            swap(node, node.next)
        return zigZag(node.next, 0)

# Driver Code
head =  Node(11)
head.next =  Node(15)
head.next.next =  Node(20)
head.next.next.next =  Node(5)
head.next.next.next.next =  Node(10)
printLL();

# 0 means the current element
# should be smaller than the next    
flag = 0
zigZag(head, flag)
print("LL in zig zag fashion : ")
printLL()

# This code is contributed by avanitrachhadiya2155
```

**输出:**

```
11 ->15 ->20 ->5 ->10 ->
LL in zig zag fashion : 
11 ->20 ->5 ->15 ->10 ->
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    遍历列表只做一次，它有‘n’个元素。
*   **辅助空间:** O(n)。
    用于存储值的 O(n)额外空间数据结构。

更多详情请参考[以之字形方式重新排列链表](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)的完整文章！