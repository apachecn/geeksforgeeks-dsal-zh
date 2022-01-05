# 用于比较表示为链表的两个字符串的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-用于比较两个字符串的程序-表示为链表/](https://www.geeksforgeeks.org/javascript-program-for-comparing-two-strings-represented-as-linked-lists/)

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

## java 描述语言

```
<script>
// Javascript program to compare two 
// strings represented as a linked list

// Linked List Class

// head of list
var head;
var a, b;

// Node Class 
class Node 
{
    // Constructor to create a 
    // new node
    constructor(d) 
    {
        this.data = d;
        this.next = null;
    }
}

function compare(node1, node2) 
{
    if (node1 == null && 
        node2 == null) 
    {
        return 1;
    }

    while (node1 != null && 
           node2 != null && 
           node1.data == node2.data) 
    {
        node1 = node1.next;
        node2 = node2.next;
    }

    // If the list are different 
    // in size
    if (node1 != null && 
        node2 != null) 
    {
        return (node1.data > 
                node2.data ? 1 : -1);
    }

    // If either of the list has 
    // reached end
    if (node1 != null && 
        node2 == null) 
    {
        return 1;
    }

     if (node1 == null && 
         node2 != null) 
     {
         return -1;
     }
     return 0;
}

// Driver code
var result = null;
a = new Node('g');
a.next = new Node('e');
a.next.next = new Node('e');
a.next.next.next = 
new Node('k');
a.next.next.next.next = 
new Node('s');
a.next.next.next.next.next = 
new Node('b');

b = new Node('g');
b.next = new Node('e');
b.next.next = new Node('e');
b.next.next.next = 
new Node('k');
b.next.next.next.next = 
new Node('s');
b.next.next.next.next.next = 
new Node('a');

var value;
value = compare(a, b);
document.write(value);
// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
1
```

更多详细信息，请参考完整的文章[比较两个链表表示的字符串](https://www.geeksforgeeks.org/compare-two-strings-represented-as-linked-lists/)！