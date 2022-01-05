# 删除链表备用节点的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-delete-alternate-nodes-of-a-link-list/](https://www.geeksforgeeks.org/javascript-program-to-delete-alternate-nodes-of-a-linked-list/)

给定一个单链表，从第二个节点开始删除它的所有替换节点。例如，如果给定的链表是 1->2->3->4->5，那么你的函数应该把它转换成 1->3->5，如果给定的链表是 1->2->3->4，那么把它转换成 1->3。

**方法 1(迭代):**
跟踪要删除的节点的前一个。首先，更改上一个节点的下一个链接，并迭代移动到下一个节点。

## java 描述语言

```
<script>
// Javascript program to delete alternate
// nodes of a linked list

// Head of list
var head; 

// Linked list Node 
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

function deleteAlt() 
{
    if (head == null)
        return;

    var prev = head;
    var now = head.next;

    while (prev != null && 
           now != null) 
    {
        // Change next link of previous 
        // node 
        prev.next = now.next;

        // Free node 
        now = null;

        // Update prev and now 
        prev = prev.next;
        if (prev != null)
            now = prev.next;
    }
}

// Utility functions 
// Inserts a new Node at front of 
// the list. 
function push(new_data) 
{
    /* 1 & 2: Allocate the Node & 
              Put in the data */
    var new_node = new Node(new_data);

    // 3\. Make next of new Node as head 
    new_node.next = head;

    // 4\. Move the head to point to 
    // new Node 
    head = new_node;
}

// Function to print linked list 
function printList() 
{
    var temp = head;
    while (temp != null) 
    {
        document.write(temp.data + " ");
        temp = temp.next;
    }
    document.write("<br/>");
}

// Driver code
/* Constructed Linked List is
   1->2->3->4->5->null */
push(5);
push(4);
push(3);
push(2);
push(1);

document.write(
         "Linked List before calling deleteAlt() <br/>");
printList();

deleteAlt();

document.write(
         "Linked List after calling deleteAlt()<br/> ");
printList();
// This code is contributed by gauravrajput1 
</script>
```

**输出:**

```
List before calling deleteAlt() 
1 2 3 4 5 
List after calling deleteAlt() 
1 3 5 
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**方法 2(递归):**
递归代码使用与方法 1 相同的方法。递归代码简单而简短，但会导致 O(n)个递归函数调用大小为 n 的链表。

## java 描述语言

```
<script>
/* Deletes alternate nodes of a list
   starting with head */
function deleteAlt(head) 
{ 
    if (head == null) 
        return; 

    var node = head.next; 

    if (node == null) 
        return; 

    // Change the next link of head    
    /* Recursively call for the new 
       next of head */
    head.next = node.next;    
    head.next = deleteAlt(head.next); 
} 
// This code contributed by aashish1995 
</script>
```

**时间复杂度:** O(n)

更多详情请参考[删除链表备用节点](https://www.geeksforgeeks.org/delete-alternate-nodes-of-a-linked-list/)整篇文章！