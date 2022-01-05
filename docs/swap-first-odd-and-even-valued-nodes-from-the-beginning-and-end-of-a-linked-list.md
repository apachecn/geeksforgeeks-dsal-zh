# 从链表的开始和结束交换第一个奇数和偶数值的节点

> 原文:[https://www . geesforgeks . org/swap-first-奇数和偶数值节点-从链表的开始和结束/](https://www.geeksforgeeks.org/swap-first-odd-and-even-valued-nodes-from-the-beginning-and-end-of-a-linked-list/)

给定单个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，任务是交换链表开头的第一个奇值节点和末尾的第一个偶值[节点。如果列表包含单个奇偶校验的节点值，则不需要修改。](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)

**示例:**

> **输入:**4->3->5->2->3->NULL
> T3】输出:4->2->5->3->3->NULL
> T6】解释:T8】4->T9】3->5->T11】2 > 3 - > NULL
> 任何节点从开始的第一个奇数为 **3** 。
> 从末端开始任何节点的第一个偶数值是 **2** 。
> 交换上述两个节点值后，链表修改为 4->2->5->3->3->NULL。
> 
> **输入:**LL:2->6->8->2->NULL
> **输出:**2->6->8->2->NULL

**方法:**给定的问题可以通过分别跟踪奇数和偶数值节点的第一次和最后一次出现并交换它们来解决。按照以下步骤解决问题:

*   初始化两个[变量](https://www.geeksforgeeks.org/variables-in-c/)，比如**第一个奇数**和**第一个偶数**，分别从开始和结束存储第一个具有奇数和偶数值的节点。
*   初始化两个变量，比如**第一个奇数**和**第一个偶数**(最初[为空](https://www.geeksforgeeks.org/few-bytes-on-null-pointer-in-c/))。
*   [遍历链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)并执行以下步骤:
    *   如果[当前节点的值为**奇数**T3**第一个奇数**为**空**，则将**第一个奇数**节点更新为当前节点。](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)
    *   否则，首先更新**甚至**作为当前节点。
*   完成上述步骤后，如果**第一奇数**和**第一偶数**不是**空**，则[交换两个指针](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)的值。
*   将修改后的链接列表打印为结果链接列表。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

# Structure of a node
# in the Linked List
class Node:
    def __init__(self, x):
        self.val = x
        self.next = None

# Function to display the Linked List
def printLL(head):

    # Traverse until end
    # of list is reached
    while(head):

        # Print the value
        # stored in the head
        print(head.val, end =' ')

        # Move to the next of head
        head = head.next
    print()

# Function to swap the nodes
def swapNodes(head, even, odd):

    # Keeps the track of
    # prevEven and CurrEven
    prevEven = None
    currEven = head

    while currEven and currEven != even:
        prevEven = currEven
        currEven = currEven.next

    # Keeps the track of
    # prevOdd and currOdd
    prevOdd = None
    currOdd = head

    while currOdd and currOdd != odd:
        prevOdd = currOdd
        currOdd = currOdd.next

    # If list contains nodes
    # of a single parity
    if not currEven or not currOdd:
        return head

    # If head of the linked list
    # does not contain even value
    if prevEven:
        prevEven.next = currOdd

    # Make odd node the new head
    else:
        head = currOdd

    # If head of the linked list
    # does not contain odd value
    if prevOdd:
        prevOdd.next = currEven

    # Make even node the new head
    else:
        head = currEven

    # Swap the next pointers
    temp = currEven.next
    currEven.next = currOdd.next
    currOdd.next = temp

    # Return the modified Linked List
    return head

# Function to swap the first odd node
# from the beginning and the first even
# node from the end of the Linked List
def swapOddAndEvenNodes(head):

    # Find the first even node from
    # the end of the Linked List
    even = None
    curr = head
    while curr:
        if not curr.val & 1:
            even = curr
        curr = curr.next

    # Find the first odd node from
    # the front of the Linked List
    odd = None
    curr = head
    while curr:
        if curr.val & 1:
            odd = curr
            break
        curr = curr.next

    # If required odd and even
    # nodes are found, then swap
    if odd and even:
        head = swapNodes(head, even, odd)

    printLL(head)

# Function to convert given
# array into a Linked List
def linkedList(arr):
    head = None
    ptr = None

    # 4 -> 3 -> 5 -> 2 -> 3 -> NULL
    for i in arr:
        if not head:
            head = Node(i)
            ptr = head
        else:
            newNode = Node(i)
            ptr.next = newNode
            ptr = newNode
    return head

# Driver Code

# Given Linked List
arr = [4, 3, 5, 2, 3]

# Stores head of Linked List
head = linkedList(arr)

swapOddAndEvenNodes(head)
```

**Output:**

```
4 2 5 3 3

```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)