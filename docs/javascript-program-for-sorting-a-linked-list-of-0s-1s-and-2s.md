# 用于排序 0、1 和 2s 链表的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-用于排序的程序-链接列表-0s-1s-和-2s/](https://www.geeksforgeeks.org/javascript-program-for-sorting-a-linked-list-of-0s-1s-and-2s/)

给定一个 0、1 和 2 的链表，对其进行排序。
**例**:

```
Input: 1 -> 1 -> 2 -> 0 -> 2 -> 0 -> 1 -> NULL
Output: 0 -> 0 -> 1 -> 1 -> 1 -> 2 -> 2 -> NULL

Input: 1 -> 1 -> 2 -> 1 -> 0 -> NULL 
Output: 0 -> 1 -> 1 -> 1 -> 2 -> NULL

```

来源:[微软访谈|第一集](https://www.geeksforgeeks.org/microsoft-interview-set-1/)

可以使用以下步骤对给定的链表进行排序。

*   遍历列表，计算 0、1 和 2 的数量。让计数分别为 n1、n2 和 n3。
*   再次遍历列表，首先用 0 填充 n1 个节点，然后用 1 填充 n2 个节点，最后用 2 填充 n3 个节点。

下图是上述方法的模拟运行:

![](img/17513c1428d4f78489a3b4005798659b.png)

下面是上述方法的实现:

## java 描述语言

```
<script>
// Javascript program to sort a 
// linked list of 0, 1 and 2

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

function sortList() 
{
    // Initialise count of 0 1 
    // and 2 as 0
    var count = [ 0, 0, 0 ];

    var ptr = head;

    /* Count total number of '0', '1' and '2'
       count[0] will store total number of
       '0's count[1] will store total number
       of '1's count[2] will store total
       number of '2's */
    while (ptr != null) 
    {
        count[ptr.data]++;
        ptr = ptr.next;
    }

    var i = 0;
    ptr = head;

    /* Let say count[0] = n1, count[1] = n2 and 
       count[2] = n3 now start traversing
       list from head node, 1) fill the list
       with 0, till n1 > 0 2) fill the list
       with 1, till n2 > 0 3) 
       fill the list with 2, till n3 > 0 */
    while (ptr != null) 
    {
        if (count[i] == 0)
            i++;
        else 
        {
            ptr.data = i;
            --count[i];
            ptr = ptr.next;
        }
    }
}

// Utility functions
/* Inserts a new Node at front 
   of the list. */
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
   1->2->3->4->5->6->7-> 8->8->9->null */
push(0);
push(1);
push(0);
push(2);
push(1);
push(1);
push(2);
push(1);
push(2);

document.write(
         "Linked List before sorting<br/>");
printList();

sortList();

document.write(
         "Linked List after sorting<br/>");
printList();
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Linked List Before Sorting
2  1  2  1  1  2  0  1  0
Linked List After Sorting
0  0  1  1  1  1  2  2  2
```

**时间复杂度:** O(n)，其中 n 为链表中的节点数。
**辅助空间:** O(1)

更多详情请参考[整理 0，1，2s](https://www.geeksforgeeks.org/sort-a-linked-list-of-0s-1s-or-2s/) 链表整篇文章！