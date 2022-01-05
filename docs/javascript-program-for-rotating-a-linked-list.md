# 用于旋转链表的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-用于旋转链表的程序/](https://www.geeksforgeeks.org/javascript-program-for-rotating-a-linked-list/)

给定一个单链表，逆时针旋转链表 k 个节点。其中 k 是给定的正整数。例如，如果给定的链表是 10->20->30->40->50->60，k 是 4，那么应该将链表修改为 50->60->10->20->30->40。假设 k 小于链表中的节点数。

**方法 1:**
要旋转链表，我们需要将第 kth 个节点的下一个节点改为 NULL，将最后一个节点的下一个节点改为前一个头节点，最后将头改为第(k+1)个节点。所以我们需要获得三个节点:第 k 个节点，(k+1)个节点和最后一个节点。
从头遍历列表，在第 kth 个节点停止。存储指向第 k 个节点的指针。接下来我们可以使用 kthNode- >获得第(k+1)个节点。一直遍历到最后，并存储一个指向最后一个节点的指针。最后，如上所述更改指针。

下图显示了旋转函数如何在代码中工作:

![](img/d20bcab15c5c1bfdac020daf13ed0cb5.png)

## java 描述语言

```
<script>
// Javascript program to rotate
// a linked list

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

// This function rotates a linked list
// counter-clockwise and updates the head.
// The function assumes that k is smaller
// than size of linked list. It doesn't
// modify the list if k is greater than
// or equal to size
function rotate(k)
{
    if (k == 0)
        return;

    // Let us understand the below code
    // for example k = 4 and list =
    // 10->20->30->40->50->60.
    var current = head;

    // current will either point to kth or
    // NULL after this loop. current will
    // point to node 40 in the above example
    var count = 1;

    while (count < k && current != null)
    {
        current = current.next;
        count++;
    }

    // If current is NULL, k is greater than
    // or equal to count of nodes in linked list.
    // Don't change the list in this case
    if (current == null)
        return;

    // current points to kth node. Store it in
    // a variable. kthNode points to node 40
    // in the above example
    var kthNode = current;

    // current will point to last node after
    // this loop current will point to node
    // 60 in the above example
    while (current.next != null)
        current = current.next;

    // Change next of last node to previous
    // head Next of 60 is now changed to
    // node 10
    current.next = head;

    // Change head to (k+1)th node
    // head is now changed to node 50
    head = kthNode.next;

    // change next of kth node to null
    kthNode.next = null;
}

/* Given a reference (pointer to pointer) to
   the head of a list and an int, push
   a new node on the front of the list. */
    function push(new_data) {

/* 1 & 2: Allocate the Node &
          Put in the data */
var new_node = new Node(new_data);

// 3\. Make next of new Node as head
new_node.next = head;

// 4\. Move the head to point to new Node
head = new_node;
}

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
// Create a list
// 10->20->30->40->50->60
for (i = 60; i >= 10; i -= 10)
    push(i);

document.write("Given list<br/>");
printList();

rotate(4);

document.write("Rotated Linked List<br/>");
printList();
// This code is contributed by todaysgaurav
</script>
```