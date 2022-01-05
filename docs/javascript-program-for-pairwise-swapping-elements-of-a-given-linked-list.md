# 给定链表成对交换元素的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-pair-swapping-elements-of-给定链表/](https://www.geeksforgeeks.org/javascript-program-for-pairwise-swapping-elements-of-a-given-linked-list/)

给定一个单链表，编写一个成对交换元素的函数。

```
**输入:**1->2->3->4->5->6->NULL
**输出:**2->1->4->3->6->5->NULL**输入:**1->2->3->4->5-
```

**例如，如果链表是 1->2->3->4->5，那么函数应该将其改为 2->1->4->3->5，如果链表是，那么函数应该将其改为。**

****方法 1(迭代):**
从头节点开始遍历列表。同时用下一个节点的数据遍历每个节点的交换数据。
以下是上述方法的实施:**

## **java 描述语言**

```
<script>
// JavaScript program to pairwise swap 
// elements of a linked list

// head of list
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

function pairWiseSwap() 
{
    var temp = head;

    /* Traverse only till there are 
       atleast 2 nodes left */
    while (temp != null && 
           temp.next != null) 
    {
        // Swap the data 
        var k = temp.data;
        temp.data = temp.next.data;
        temp.next.data = k;
        temp = temp.next.next;
    }
}

// Utility functions 
// Inserts a new Node at front 
// of the list. 
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
/ * Created Linked List 
    1->2->3->4->5 */
push(5);
push(4);
push(3);
push(2);
push(1);

document.write(
"Linked List before calling pairWiseSwap() <br/>");
printList();

pairWiseSwap();

document.write(
"Linked List after calling pairWiseSwap()<br/> ");
printList();
// This code is contributed by todaysgaurav
</script>
```

****输出:****

```
Linked list before calling pairWiseSwap()
1 2 3 4 5 
Linked list after calling pairWiseSwap()
2 1 4 3 5 
```

****时间复杂度:** O(n)**

****方法 2(递归):**
如果链表中有 2 个或 2 个以上的节点，那么交换前两个节点，递归调用链表的其余部分。
下图是上述方法的试运行:**

**![](img/e3cbac4a3d5b049aef5c57a1d325a8e3.png)**

**下面是上述方法的实现:**

## **java 描述语言**

```
<script>
/* Recursive function to pairwise swap 
   elements of a linked list */
function pairWiseSwap(head)
{
    /* There must be at-least two nodes
       in the list */
    if (head != null && 
        head.next != null) 
    { 
        /* Swap the node's data with data 
           of next node */
        swap(head.data, head.next.data);

        /* Call pairWiseSwap() for rest of 
           the list */
        pairWiseSwap(head.next.next);
    }
}
// This code is contributed by avanitrachhadiya2155
</script>
```

****时间复杂度:** O(n)
**提供的解决方案是交换节点的数据。如果数据包含许多字段，将会有许多交换操作。请参见** [**本**](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/) **了解更改链接而不是交换数据的实现。****

**更多细节请参考完整的文章[给定链表的成对交换元素](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)！**