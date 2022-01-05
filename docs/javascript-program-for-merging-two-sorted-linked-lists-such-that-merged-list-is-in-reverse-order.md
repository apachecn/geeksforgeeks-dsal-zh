# 用于合并两个排序的链表的 Javascript 程序，使得合并的链表处于相反的顺序

> 原文:[https://www . geesforgeks . org/JavaScript-用于合并的程序-两个排序的链表-这样合并后的列表就处于相反的顺序/](https://www.geeksforgeeks.org/javascript-program-for-merging-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/)

给定两个按升序排序的链表。将它们合并，使结果列表按降序(逆序)排列。

**示例:**

```
Input:  a: 5->10->15->40
        b: 2->3->20 
Output: res: 40->20->15->10->5->3->2

Input:  a: NULL
        b: 2->3->20 
Output: res: 20->3->2
```

一个**简单的解决方法**就是做以下几点。
1) [逆转首榜‘a’](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。
2) [反转第二个列表‘b’](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。
3) [合并两个反向列表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)。
另一个简单的解决方案是首先合并两个列表，然后反转合并的列表。
上述两种解决方案都需要链表的两次遍历。

**没有反向，O(1)辅助空间(原地)，两个列表只有一次遍历，如何求解？**
思路是遵循合并风格流程。将结果列表初始化为空。从头到尾遍历两个列表。比较两个列表的当前节点，并在结果列表的开头插入两个中较小的一个。

```
1) Initialize result list as empty: res = NULL.
2) Let 'a' and 'b' be heads first and second lists respectively.
3) While (a != NULL and b != NULL)
    a) Find the smaller of two (Current 'a' and 'b')
    b) Insert the smaller value node at the front of result.
    c) Move ahead in the list of smaller node. 
4) If 'b' becomes NULL before 'a', insert all nodes of 'a' 
   into result list at the beginning.
5) If 'a' becomes NULL before 'b', insert all nodes of 'a' 
   into result list at the beginning. 
```

下面是上述解决方案的实现。

## java 描述语言

```
<script>
// Javascript program to merge two 
// sorted linked list such that merged 
// list is in reverse order

// Node Class 
class Node
{
    constructor(d)
    {
        this.data = d;
        this.next = null;
    }
}

// Head of list
let head;  
let a, b;

function printlist(node)
{
    while (node != null) 
    {
        document.write(node.data + " ");
        node = node.next;
    }
}

function sortedmerge(node1, node2)
{    
    // If both the nodes are null
    if (node1 == null && node2 == null)
    {
        return null;
    }

    // Resultant node
    let res = null;

    // If both of them have nodes
    //  present traverse them
    while (node1 != null && 
           node2 != null) 
    {        
        // Now compare both nodes 
        // current data
        if (node1.data <= node2.data) 
        {
            let temp = node1.next;
            node1.next = res;
            res = node1;
            node1 = temp;
        } 
        else
        {
            let temp = node2.next;
            node2.next = res;
            res = node2;
            node2 = temp;
        }
    }

    // If second list reached end, but
    // first list has nodes. Add 
    // remaining nodes of first
    // list at the front of result list
    while (node1 != null) 
    {
        let temp = node1.next;
        node1.next = res;
        res = node1;
        node1 = temp;
    }

    // If first list reached end, but
    // second list has node. Add 
    // remaining nodes of first 
    // list at the front of result list
    while (node2 != null)
    {
        let temp = node2.next;
        node2.next = res;
        res = node2;
        node2 = temp;
    }
    return res;
}

// Driver code
let result = null;

/*Let us create two sorted linked lists 
  to test the above functions. Created 
  lists shall be
  a: 5->10->15
  b: 2->3->20*/
a = new Node(5);
a.next = new Node(10);
a.next.next = new Node(15);

b = new Node(2);
b.next = new Node(3);
b.next.next = new Node(20);

document.write("List a before merge :<br>");
printlist(a);
document.write("<br>");
document.write("List b before merge :<br>");
printlist(b);

// Merge two sorted linkedlist in 
// decreasing order
result = sortedmerge(a, b);
document.write("<br>");
document.write("Merged linked list : <br>");
printlist(result);
// This code is contributed by rag2127
</script>
```

**输出:**

```
List A before merge: 
5 10 15 
List B before merge: 
2 3 20 
Merged Linked List is: 
20 15 10 5 3 2 
```

这个解决方案只遍历两个列表一次，不需要反向，就地工作。
本文由[T2T4【穆罕默德·拉基布】供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息](https://www.linkedin.com/in/mohammed-raqeeb-soudagar-951b345a) 

更多详情请参考[完整文章合并两个排序链表，合并后的链表顺序相反](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists-such-that-merged-list-is-in-reverse-order/)！