# 写函数删除链表的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-写程序-函数-删除-链表/](https://www.geeksforgeeks.org/javascript-program-for-writing-a-function-to-delete-a-linked-list/)

链表是一种线性数据结构，其中元素不存储在连续的内存位置。链表中的元素使用指针进行链接。这篇文章的重点是写一个删除链表的函数。

**实施:**

## java 描述语言

```
<script>
// Javascript program to delete
// a linked list

// Head of the list
var head;

// Linked List node
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Function deletes the entire
// linked list
function deleteList()
{
    head = null;
}

// Inserts a new Node at front
// of the list.
function push(new_data)
{
    /* 1 & 2: Allocate the Node &
              Put in the data */
    var new_node = new Node(new_data);

    // 3\. Make next of new Node as head
    new_node.next = head;

    // 4\. Move the head to point to new Node
    head = new_node;
}

// Use push() to construct list
// 1->12->1->4->1
push(1);
push(4);
push(1);
push(12);
push(1);

document.write("Deleting the list<br/>");
deleteList();
document.write("Linked list deleted");
// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
Deleting linked list
Linked list deleted
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

更多详情请参考[写函数删除链表](https://www.geeksforgeeks.org/write-a-function-to-delete-a-linked-list/)整篇文章！