# 用于交换链表中的节点而不交换数据的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序交换-链表中的节点-不交换-数据/](https://www.geeksforgeeks.org/javascript-program-for-swapping-nodes-in-a-linked-list-without-swapping-data/)

给定一个链表和其中的两个键，用两个给定的键交换节点。应该通过更改链接来交换节点。当数据包含许多字段时，交换节点的数据在许多情况下可能是昂贵的。

可以假设链表中的所有键都是不同的。

**示例:**

```
Input : 10->15->12->13->20->14,  x = 12, y = 20
Output: 10->15->20->13->12->14

Input : 10->15->12->13->20->14,  x = 10, y = 20
Output: 20->15->12->13->10->14

Input : 10->15->12->13->20->14,  x = 12, y = 13
Output: 10->15->13->12->20->14
```

这看起来可能是一个简单的问题，但这是一个有趣的问题，因为它有以下情况需要处理。

1.  x 和 y 可以相邻，也可以不相邻。
2.  x 或 y 都可以是头节点。
3.  x 或 y 可能是最后一个节点。
4.  链接列表中可能不存在 x 和/或 y。

如何编写一个干净的工作代码来处理上述所有可能性。

想法是首先在给定的链表中搜索 x 和 y。如果他们中的任何一个不存在，那么返回。在搜索 x 和 y 时，跟踪当前和以前的指针。首先更改上一个指针的下一个，然后更改当前指针的下一个。

下面是上述方法的实现。

## java 描述语言

```
<script>
// JavaScript program to swap two
// given nodes of a linked list
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Head of list
var head;

/* Function to swap Nodes x and y in
   linked list by changing links */
function swapNodes(x, y)
{
    // Nothing to do if x and y
    // are same
    if (x == y)
        return;

    // Search for x (keep track of
    prevX and CurrX)
    var prevX = null, currX = head;
    while (currX != null &&
           currX.data != x)
    {
        prevX = currX;
        currX = currX.next;
    }

    // Search for y (keep track of
    // prevY and currY)
    var prevY = null, currY = head;
    while (currY != null &&
           currY.data != y)
    {
        prevY = currY;
        currY = currY.next;
    }

    // If either x or y is not present,
    // nothing to do
    if (currX == null || currY == null)
        return;

    // If x is not head of linked list
    if (prevX != null)
        prevX.next = currY;
    else

        // make y the new head
        head = currY;

    // If y is not head of linked list
    if (prevY != null)
        prevY.next = currX;
    else

        // make x the new head
        head = currX;

    // Swap next pointers
    var temp = currX.next;
    currX.next = currY.next;
    currY.next = temp;
}

// Function to add Node at beginning
// of list
function push(new_data)
{
    // 1\. alloc the Node and put the data
    var new_Node = new Node(new_data);

    // 2\. Make next of new Node as head
    new_Node.next = head;

    // 3\. Move the head to point to new Node
    head = new_Node;
}

// This function prints contents of
// linked list starting from the
// given Node
function printList()
{
    var tNode = head;
    while (tNode != null)
    {
        document.write(tNode.data + " ");
        tNode = tNode.next;
    }
}

// Driver code
/* The constructed linked list is:
   1->2->3->4->5->6->7 */
push(7);
push(6);
push(5);
push(4);
push(3);
push(2);
push(1);

document.write(
         "Linked list before calling swapNodes()<br/> ");
printList();
swapNodes(4, 3);
document.write(
         "<br/> Linked list after calling swapNodes() <br/>");
printList();
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 1 2 4 3 5 6 7 
```

**优化:**以上代码可以优化为单次遍历搜索 x 和 y。两个循环用于保持程序简单。

**更简单的方法:**

## java 描述语言

```
<script>
// Javascript program to swap two given
// nodes of a linked list
// Represent a node of the singly
// linked list
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Represent the head and tail of
// the singly linked list
var head = null;
var tail = null;

// addNode() will add a new node
// to the list
function addNode(data)
{
    // Create a new node
    var newNode = new Node(data);

    // Checks if the list is empty
    if (head == null)
    {
        // If list is empty, both head and
        // tail will point to new node
        head = newNode;
        tail = newNode;
    }
    else
    {
        // newNode will be added after tail
        // such that tail's next will point
        // to newNode
        tail.next = newNode;

        // newNode will become new tail
        // of the list
        tail = newNode;
    }
}

// swap() will swap the given
// two nodes
function swap(n1 , n2)
{
    var prevNode1 = null,
        prevNode2 = null,
        node1 = head, node2 = head;

    // Checks if list is empty
    if (head == null)
    {
        return;
    }

    // If n1 and n2 are equal, then
    // list will remain the same
    if (n1 == n2)
        return;

    // Search for node1
    while (node1 != null &&
           node1.data != n1)
    {
        prevNode1 = node1;
        node1 = node1.next;
    }

    // Search for node2
    while (node2 != null &&
           node2.data != n2)
    {
        prevNode2 = node2;
        node2 = node2.next;
    }

    if (node1 != null &&
        node2 != null)
    {
        // If previous node to node1 is not
        // null then, it will point to node2
        if (prevNode1 != null)
            prevNode1.next = node2;
        else
            head = node2;

        // If previous node to node2 is
        // not null then, it will point to node1
        if (prevNode2 != null)
            prevNode2.next = node1;
        else
            head = node1;

        // Swaps the next nodes of node1 and node2
        var temp = node1.next;
        node1.next = node2.next;
        node2.next = temp;
    }
    else
    {
        document.write("Swapping is not possible");
    }
}

// display() will display all the
// nodes present in the list
function display()
{
    // Node current will point to head
    var current = head;

    if (head == null)
    {
        document.write("List is empty");
        return;
    }
    while (current != null)
    {
        // Prints each node by incrementing
        // pointer
        document.write(current.data + " ");
        current = current.next;
    }
    document.write();
}

// Add nodes to the list
addNode(1);
addNode(2);
addNode(3);
addNode(4);
addNode(5);
addNode(6);
addNode(7);

document.write("Original list:<br/> ");
display();

// Swaps node 2 with node 5
swap(6, 1);

document.write(
         "<br/>List after swapping nodes: <br/>");
display();
// This code contributed by aashish1995
</script>
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 6 2 3 4 5 1 7 
```

更多详情请参考完整文章[在链表中交换节点不交换数据](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)！