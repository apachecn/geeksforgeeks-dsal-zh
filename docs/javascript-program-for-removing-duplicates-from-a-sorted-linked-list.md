# 用于从排序的链表中删除重复项的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-从排序链表中删除重复项的程序/](https://www.geeksforgeeks.org/javascript-program-for-removing-duplicates-from-a-sorted-linked-list/)

编写一个函数，接受按非递减顺序排序的列表，并从列表中删除任何重复的节点。该列表只能遍历一次。
例如，如果链接列表是 11->11->11->21->43->43->60，则 removeDuplicates()应该将列表转换为 11- > 21- > 43- > 60。

**算法:**
从头(或开始)节点遍历列表。遍历时，将每个节点与其下一个节点进行比较。如果下一个节点的数据与当前节点相同，则删除下一个节点。在删除节点之前，我们需要存储节点的下一个指针

**实现:**
removeDuplicates()之外的函数只是创建一个链表并测试 remove duplicates()。

## java 描述语言

```
<script>
// Javascript program to remove duplicates
// from a sorted linked list

// Linked list Node
class Node
{
    constructor(d)
    {
        this.data = d;
        this.next = null;
    }
}

// Head of list
let head = new Node();   
function removeDuplicates()
{
    // Another reference to head
    let curr = head;

    // Traverse list till the last node
    while (curr != null)
    {
        let temp = curr;

        /* Compare current node with the
           next node and keep on deleting
           them until it matches the current
           node data */
        while(temp!=null &&
              temp.data==curr.data)
        {
            temp = temp.next;
        }

        /* Set current node next to the next
           different element denoted by temp*/
        curr.next = temp;
        curr = curr.next;
    }
}

// Utility functions

// Inserts a new Node at front of the list.
function push(new_data)
{
    /* 1 & 2: Allocate the Node &
              Put in the data */
    let new_node = new Node(new_data);

    // 3\. Make next of new Node as head
    new_node.next = head;

    // 4\. Move the head to point to
    // new Node
    head = new_node;
}

// Function to print linked list
function printList()
{
    let temp = head;
    while (temp != null && temp.data)
    {
        document.write(temp.data+" ");
        temp = temp.next;
    }
    document.write("<br>");
}

// Driver code
push(20)
push(13)
push(13)
push(11)
push(11)
push(11)

document.write(
         "List before removal of duplicates ");
printList();
removeDuplicates();
document.write(
         "List after removal of elements ");
printList();
// This code is contributed by unknown2108
</script>
```

**输出:**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**递归方法:**

## java 描述语言

```
<script>
// JavaScript Program to remove duplicates
// from a sorted linked list

// Link list node
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// The function removes duplicates
// from a sorted list
function removeDuplicates(head)
{
    /* Pointer to store the pointer
       of a node to be deleted */
    var to_free;

    // Do nothing if the list is empty
    if (head == null)
        return null;

    // Traverse the list till last node
    if (head.next != null)
    {
        // Compare head node with next node
        if (head.data == head.next.data)
        {
            /* The sequence of steps is important.
               to_free pointer stores the next of head
               pointer which is to be deleted. */
            to_free = head.next;
            head.next = head.next.next;
            removeDuplicates(head);
        }

        /* This is tricky: only advance
           if no deletion */
        else
        {
            removeDuplicates(head.next);
        }
    }
    return head;
}

// UTILITY FUNCTIONS
// Function to insert a node at
// the beginning of the linked list

function push(head_ref, new_data)
{
    // Allocate node */
var new_node = new Node();

        /* put in the data */
        new_node.data = new_data;

        /* link the old list off the new node */
        new_node.next = (head_ref);

        /* move the head to point to the new node */
        (head_ref) = new_node;
        return head_ref;
    }

    /* Function to print nodes in a given linked list */
    function printList(node) {
        while (node != null) {
            document.write(" " + node.data);
            node = node.next;
        }
    }

    /* Driver code */

        /* Start with the empty list */
var head = null;

        /*
          Let us create a sorted linked list to
         test the functions Created linked list
          will be 11.11.11.13.13.20
         */
        head = push(head, 20);
        head = push(head, 13);
        head = push(head, 13);
        head = push(head, 11);
        head = push(head, 11);
        head = push(head, 11);

        document.write("Linked list before" +
        " duplicate removal <br/>");
        printList(head);

        /* Remove duplicates from linked list */
        head = removeDuplicates(head);

        document.write("<br/>Linked list after" +
        " duplicate removal <br/>");
        printList(head);

// This code is contributed by todaysgaurav

</script>
```

**Output**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**另一种方法:**创建一个指向每个元素第一次出现的指针和另一个将迭代到每个元素的指针 temp，当前一个指针的值不等于 temp 指针时，我们将前一个指针的指针设置为另一个节点的第一次出现。

下面是上述方法的实现:

## java 描述语言

```
<script>
// javascript program to remove duplicates
// from a sorted linked list

    // head of list
    var head;

    // Linked list Node
     class Node {
            constructor(val) {
                this.data = val;
                this.next = null;
            }
        }

    // Function to remove duplicates
    // from the given linked list
    function removeDuplicates() {
        // Two references to head
        // temp will iterate to the
        // whole Linked List
        // prev will point towards
        // the first occurrence of every element
        var temp = head, prev = head;

        // Traverse list till the last node
        while (temp != null) {

            // Compare values of both pointers
            if (temp.data != prev.data) {
                /*
                 * if the value of prev is not equal to the value of temp that means there are
                 * no more occurrences of the prev data. So we can set the next of prev to the
                 * temp node.
                 */
                prev.next = temp;
                prev = temp;
            }
            /* Set the temp to the next node */
            temp = temp.next;
        }
        /*
         * This is the edge case if there are more than one occurrences of the last
         * element
         */
        if (prev != temp) {
            prev.next = null;
        }
    }

    /* Utility functions */

    /* Inserts a new Node at front of the list. */
    function push(new_data) {
        /*
         * 1 & 2: Allocate the Node & Put in the data
         */
        var new_node = new Node(new_data);

        /* 3\. Make next of new Node as head */
        new_node.next = head;

        /* 4\. Move the head to point to new Node */
        head = new_node;
    }

    /* Function to print linked list */
    function printList() {
        var temp = head;
        while (temp != null) {
            document.write(temp.data + " ");
            temp = temp.next;
        }
        document.write("<br/>");
    }

    /* Driver program to test above functions */

        push(20);
        push(13);
        push(13);
        push(11);
        push(11);
        push(11);

        document.write("List before ");
        document.write("removal of duplicates<br/>");
        printList();

        removeDuplicates();

        document.write("List after removal of elements<br/>");
        printList();

// This code contributed by aashish1995
</script>
```

**Output**

```
List before removal of duplicates
11 11 11 13 13 20 
List after removal of elements
11 13 20 
```

**另一种方法:使用地图**

这个想法是推送地图中的所有值并打印其关键点。

下面是上述方法的实现:

## java 描述语言

```
<script>

// Javascript program for the above approach
class Node
{
    constructor()
    {
        this.data = 0;
        this.next = null;
    }
}

/* Function to insert a node at
   the beginning of the linked
 * list */
function push(head_ref, new_data)
{

    /* allocate node */
    let new_node = new Node();

    /* put in the data */
    new_node.data = new_data;

    /* link the old list off
    the new node */
    new_node.next = (head_ref);

    /* move the head to point
    to the new node */
    head_ref = new_node;
    return head_ref;
}

/* Function to print nodes
in a given linked list */
function printList(node)
{
    while (node != null)
    {
        document.write(node.data + " ");
        node = node.next;
    }
}

// Function to remove duplicates
function removeDuplicates(head)
{
    let track = new Map();
    let temp = head;

    while(temp != null)
    {
        if (!track.has(temp.data))
        {
            document.write(temp.data + " ");
        }
        track.set(temp.data, true);
        temp = temp.next;
    }
}

// Driver Code
let head = null;

/* Created linked list will be
11->11->11->13->13->20 */
head = push(head, 20);
head = push(head, 13);
head = push(head, 13);
head = push(head, 11);
head = push(head, 11);
head = push(head, 11);
document.write("Linked list before duplicate removal ");
printList(head);
document.write("<br>Linked list after duplicate removal  ");
removeDuplicates(head);

// This code is contributed by patel2127

</script>
```

**Output**

```
Linked list before duplicate removal 11 11 11 13 13 20 
Linked list after duplicate removal 11 13 20 
```

**时间复杂度:** O(节点数)

**空间复杂度:** O(节点数)

更多详情请参考[从排序链表](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)中删除重复项的完整文章！