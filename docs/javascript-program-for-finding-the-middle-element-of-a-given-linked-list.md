# 寻找给定链表中间元素的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-find-给定链表的中间元素/](https://www.geeksforgeeks.org/javascript-program-for-finding-the-middle-element-of-a-given-linked-list/)

给定一个单链表，找到链表的中间。例如，如果给定的链表是 1->2->3->4->5，那么输出应该是 3。
如果有偶数个节点，那么就会有两个中间节点，我们需要打印第二个中间元素。例如，如果给定的链表是 1->2->3->4->5->6，那么输出应该是 4。

**方法 1:**
遍历整个链表，统计节点数。现在再次遍历列表，直到 count/2，并在 count/2 返回节点。

**方法 2:**
使用两个指针遍历链表。将一个指针移动一个，将另一个指针移动两个。当快速指针到达末尾时，慢速指针将到达链表的中间。

下图显示了 printMiddle 函数在代码中的工作方式:

![middle-of-a-given-linked-list-in-C-and-Java1](img/493d25a626ee5c18546ea813c81295e6.png)

## java 描述语言

```
<script>

// JavaScript program to find
// middle of linked list

// Head of linked list
var head;

// Linked list node
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Function to print middle of
// linked list
function printMiddle()
{
    var slow_ptr = head;
    var fast_ptr = head;
    if (head != null)
    {
        while (fast_ptr != null &&
               fast_ptr.next != null)
        {
            fast_ptr = fast_ptr.next.next;
            slow_ptr = slow_ptr.next;
        }
        document.write("The middle element is [" +
                        slow_ptr.data + "] <br/><br/>");
    }
}

// Inserts a new Node at front of the list.
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

// This function prints contents of linked
// list starting from the given node
function printList()
{
    var tnode = head;
    while (tnode != null)
    {
        document.write(tnode.data + "->");
        tnode = tnode.next;
    }
    document.write("NULL<br/>");
}

for (i = 5; i > 0; --i)
{
    push(i);
    printList();
    printMiddle();
}
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
5->NULL
The middle element is [5]

4->5->NULL
The middle element is [5]

3->4->5->NULL
The middle element is [4]

2->3->4->5->NULL
The middle element is [4]

1->2->3->4->5->NULL
The middle element is [3]
```

**方法 3:**
将中间元素初始化为 head，将一个计数器初始化为 0。从头开始遍历列表，遍历时递增计数器，当计数器为奇数时，将中间变为下一个中间>。所以 mid 只会移动列表总长度的一半。
感谢纳伦德拉·康拉尔卡尔提出这个方法。

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
var head = null;

// Link list node
class Node
{
    constructor(next, val)
    {
        this.data = val;
        this.next = next;
    }
}

// Function to get the middle of
// the linked list
function printMiddle(head)
{
    var count = 0;
    var mid = head;

    while (head != null)
    {
        // Update mid, when 'count'
        // is odd number
        if ((count % 2) == 1)
            mid = mid.next;

        ++count;
        head = head.next;
    }

    // If empty list is provided
    if (mid != null)
        document.write("The middle element is [" +
                        mid.data + "]<br/><br/>");
}

function push(head_ref, new_data)
{
    // Allocate node
    var new_node = new Node(head_ref,
                            new_data);

    // Move the head to point to the new node
    head = new_node;
    return head;
}

// A utility function to print
// given linked list
function printList(head)
{
    while (head != null)
    {
        document.write(head.data + "-> ");
        head = head.next;
    }
    document.write("null<br/>");
}

// Driver code
for (i = 5; i > 0; i--)
{
    head = push(head, i);
    printList(head);
    printMiddle(head);
}
// This code contributed by gauravrajput1
</script>
```

**输出:**

```
5->NULL
The middle element is [5]

4->5->NULL
The middle element is [5]

3->4->5->NULL
The middle element is [4]

2->3->4->5->NULL
The middle element is [4]

1->2->3->4->5->NULL
The middle element is [3]
```

更多详情请参考[找到给定链表](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)中间的整篇文章！