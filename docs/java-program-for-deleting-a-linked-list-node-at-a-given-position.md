# 删除给定位置链表节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-删除链表程序-给定位置的节点/](https://www.geeksforgeeks.org/java-program-for-deleting-a-linked-list-node-at-a-given-position/)

给定一个单链表和一个位置，删除给定位置的链表节点。

**例:**

```
Input: position = 1, Linked List = 8->2->3->1->7
Output: Linked List =  8->3->1->7

Input: position = 0, Linked List = 8->2->3->1->7
Output: Linked List = 2->3->1->7
```

如果要删除的节点是根，只需将其删除即可。要删除中间节点，我们必须有一个指向要删除的节点之前的节点的指针。所以如果位置不为零，我们运行一个位置循环 1 次，得到一个指向前一个节点的指针。

以下是上述想法的实现。

## 爪哇

T0T6】

**输出:**

```
Created Linked List: 
 8  2  3  1  7 
Linked List after Deletion at position 4: 
 8  2  3  1 
```

详情请参考[删除给定位置](https://www.geeksforgeeks.org/delete-a-linked-list-node-at-a-given-position/)的链表节点整篇文章！