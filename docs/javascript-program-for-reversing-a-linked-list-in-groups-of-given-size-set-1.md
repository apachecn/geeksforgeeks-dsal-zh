# 在给定大小的组中反转链表的 Javascript 程序–设置 1

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-reverse-a-link-list-in-group-of-size-set-1/](https://www.geeksforgeeks.org/javascript-program-for-reversing-a-linked-list-in-groups-of-given-size-set-1/)

给定一个链表，编写一个函数来反转每 k 个节点(其中 k 是函数的输入)。

**示例:**

> 输入:1->【2】>【3】>【4】>【5】>【6】>【7】>【8】>【null】，K = 3
> **输出【0】**

**算法:** [*反转*](https://www.geeksforgeeks.org/reverse-a-linked-list/) *(head，k)*

*   反转大小为 k 的第一个子列表。反转时，跟踪下一个节点和上一个节点。让指向下一个节点的指针为*下一个*，指向上一个节点的指针为*上一个*。反向链表见[本帖](https://www.geeksforgeeks.org/reverse-a-linked-list/)。
*   *head- > next = reverse(next，k)* (递归调用列表的其余部分并链接两个子列表)
*   返回 *prev* ( *prev* 成为新的列表头(参见[这篇文章](https://www.geeksforgeeks.org/reverse-a-linked-list/)的一个迭代方法的图表)

下图显示了反向功能的工作原理:

![](img/3f1748b21788d25062bb837e8bbde98b.png)

下面是上述方法的实现:

## java 描述语言

```
<script>
// Javascript program to reverse a 
// linked list in groups of
// given size

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

function reverse(head, k) 
{
    if (head == null)
        return null;
    var current = head;
    var next = null;
    var prev = null;

    var count = 0;

    // Reverse first k nodes of 
    // linked list 
    while (count < k && 
           current != null) 
    {
        next = current.next;
        current.next = prev;
        prev = current;
            current = next;
            count++;
    }

    /* next is now a pointer to (k+1)th node
       Recursively call for the list starting
       from current. And make rest of the list
       as next of first node. */
    if (next != null)
        head.next = reverse(next, k);

    // prev is now head of input list
    return prev;
}

// Utility functions 
// Inserts a new Node at front 
// of the list. 
function push(new_data) 
{
    /* 1 & 2: Allocate the Node & 
              Put in the data */
    new_node = new Node(new_data);

    // 3\. Make next of new Node as head 
    new_node.next = head;

    // 4\. Move the head to point to
    // new Node 
    head = new_node;
}

// Function to print linked list
function printList() 
{
    temp = head;
    while (temp != null) 
    {
        document.write(temp.data + " ");
        temp = temp.next;
    }
    document.write("<br/>");
}

// Driver code  
/* Create Linked List
1->2->3->4->5->6-> 7->8->8->9->null */
push(9);
push(8);
push(7);
push(6);
push(5);
push(4);
push(3);
push(2);
push(1);

document.write("Given Linked List<br/>");
printList();

head = reverse(head, 3);

document.write("Reversed list<br/>");
printList();
// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Given Linked List
1 2 3 4 5 6 7 8 9 
Reversed list
3 2 1 6 5 4 9 8 7 
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    遍历列表只做一次，它有 n 个元素。
*   **辅助空间:** O(n/k)。
    对于每个大小为 n、n/k 或(n/k)+1 的链表，在递归过程中将进行调用。

更多详细信息，请参考完整的文章[在给定大小的组中反向链表|集合 1](https://www.geeksforgeeks.org/reverse-a-list-in-groups-of-given-size/) ！