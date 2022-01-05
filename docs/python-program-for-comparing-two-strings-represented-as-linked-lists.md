# 用于比较两个表示为链表的字符串的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于比较两个字符串的程序-表示为链表/](https://www.geeksforgeeks.org/python-program-for-comparing-two-strings-represented-as-linked-lists/)

给定两个字符串，表示为链表(每个字符都是链表中的一个节点)。编写一个与 strcmp()类似的函数 compare()，即如果两个字符串相同，则返回 0，如果第一个链表在字典序上更大，则返回 1，如果第二个字符串在字典序上更大，则返回-1。
**例:**

```
Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s->b
Output: -1

Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s
Output: 1

Input: list1 = g->e->e->k->s
       list2 = g->e->e->k->s
Output: 0
```

## 计算机编程语言

```
# Python program to compare two strings 
# represented as linked lists

# A linked list node 
# structure
class Node:

    # Constructor to create 
    # a new node
    def __init__(self, key):
        self.c = key ; 
        self.next = None

def compare(list1, list2):

    # Traverse both lists. Stop when 
    # either end of linked list is 
    # reached or current characters 
    # don't match
    while(list1 and list2 and 
          list1.c == list2.c):
        list1 = list1.next 
        list2 = list2.next 

    # If both lists are not empty, 
    # compare mismatching characters 
    if(list1 and list2):
        return 1 if list1.c > list2.c else -1 

    # If either of the two lists has 
    # reached end
    if (list1 and not list2):
        return 1 

    if (list2 and not list1):
        return -1 
    return 0

# Driver code
list1 = Node('g')
list1.next = Node('e')
list1.next.next = Node('e')
list1.next.next.next = Node('k')
list1.next.next.next.next = Node('s')
list1.next.next.next.next.next = Node('b')

list2 = Node('g')
list2.next = Node('e')
list2.next.next = Node('e')
list2.next.next.next = Node('k')
list2.next.next.next.next = Node('s')
list2.next.next.next.next.next = Node('a')

print compare(list1, list2)
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**输出:**

```
1
```

更多详细信息，请参考完整的文章[比较两个链表表示的字符串](https://www.geeksforgeeks.org/compare-two-strings-represented-as-linked-lists/)！