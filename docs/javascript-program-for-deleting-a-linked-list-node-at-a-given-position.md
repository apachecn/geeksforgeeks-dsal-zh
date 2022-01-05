# 删除给定位置链表节点的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-删除链表程序-给定位置的节点/](https://www.geeksforgeeks.org/javascript-program-for-deleting-a-linked-list-node-at-a-given-position/)

给定一个单链表和一个位置，删除给定位置的链表节点。

**例:**

```
Input: position = 1, Linked List = 8->2->3->1->7
Output: Linked List =  8->3->1->7

Input: position = 0, Linked List = 8->2->3->1->7
Output: Linked List = 2->3->1->7
```

如果要删除的节点是根节点，只需将其删除。要删除中间节点，我们必须有一个指向要删除的节点之前的节点的指针。所以如果位置不为零，我们运行一个位置循环 1 次，得到一个指向前一个节点的指针。

以下是上述想法的实现。

## Javascript

```
<script>

// A complete working javascript program to 
// delete a node in a linked list at a 
// given position

// head of list
var head; 

/* Linked list Node */
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

/* Inserts a new Node at front of the list. */
function push(new_data)
{

    /*
     * 1 & 2: Allocate the Node & Put in the data
     */
    var new_node = new Node(new_data);

    /* 3\. Make next of new Node as head */
    new_node.next = head;

    /* 4\. Move the head to povar to new Node */
    head = new_node;
}

/*
 * Given a reference (pointer to pointer) to the
 * head of a list and a position,
 * deletes the node at the given position
 */
function deleteNode(position)
{

    // If linked list is empty
    if (head == null)
        return;

    // Store head node
    var temp = head;

    // If head needs to be removed
    if (position == 0) 
    {

        // Change head
        head = temp.next; 
        return;
    }

    // Find previous node of the node to be deleted
    for(i = 0; temp != null && i < position - 1; i++)
        temp = temp.next;

    // If position is more than number of nodes
    if (temp == null || temp.next == null)
    return;

    // Node temp->next is the node to be deleted
    // Store pointer to the next of node to be deleted
    var next = temp.next.next;

    // Unlink the deleted node from list
    temp.next = next; 
}

/*
* This function prints contents of linked 
* list starting from the given node
*/
function printList()
{
    var tnode = head;
    while (tnode != null) 
    {
        document.write(tnode.data + " ");
        tnode = tnode.next;
    }
}

/*
* Driver program to test above functions.
* Ideally this function should be in a
* separate user class. It is kept here 
* to keep code compact
*/

/* Start with the empty list */
push(7);
push(1);
push(3);
push(2);
push(8);

document.write("Created Linked list is: <br/>");
printList();

// Delete node at position 4
deleteNode(4); 

document.write("<br/>Linked List after " +
               "Deletion at position 4: <br/>");
printList();

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Created Linked List: 
 8  2  3  1  7 
Linked List after Deletion at position 4: 
 8  2  3  1 
```

详情请参考[删除给定位置](https://www.geeksforgeeks.org/delete-a-linked-list-node-at-a-given-position/)的链表节点整篇文章！