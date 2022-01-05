# Javascript 程序删除右侧值较大的节点

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-delete-nodes-哪些节点的右侧值更大/](https://www.geeksforgeeks.org/javascript-program-to-delete-nodes-which-have-a-greater-value-on-right-side/)

给定一个单链表，移除右边值较大的所有节点。

**示例:**

```
Input: 12->15->10->11->5->6->2->3->NULL
Output: 15->11->6->3->NULL
Explanation: 12, 10, 5 and 2 have been deleted because there is a 
             greater value on the right side. When we examine 12, 
             we see that after 12 there is one node with a value 
             greater than 12 (i.e. 15), so we delete 12. When we 
             examine 15, we find no node after 15 that has a value 
             greater than 15, so we keep this node. When we go like 
             this, we get 15->6->3

Input: 10->20->30->40->50->60->NULL
Output: 60->NULL
Explanation: 10, 20, 30, 40, and 50 have been deleted because 
             they all have a greater value on the right side.

Input: 60->50->40->30->20->10->NULL
Output: No Change.
```

**方法 1(简单):**
使用两个循环。在外循环中，逐个挑选链表的节点。在内部循环中，检查是否存在其值大于拾取节点的节点。如果存在值更大的节点，则删除拾取的节点。
**时间复杂度:** O(n^2)

**方法 2(反向使用):**
感谢帕拉斯提供以下算法。
1。颠倒列表。
2。遍历反向列表。把麦克斯留到现在。如果下一个节点小于 max，则删除下一个节点，否则 max =下一个节点。
3。再次反转列表以保留原始顺序。
**时间复杂度:** O(n)
感谢 R.Srinivasan 提供下面的代码。

## java 描述语言

```
<script>
// Javascript program to delete nodes which
// have a greater value on right side

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

/* Deletes nodes which have a node
   with greater value node on left side */
function delLesserNodes()
{
    // 1.Reverse the linked list
    reverseList();

    /* 2\. In the reversed list, delete nodes
          which have a node with greater value
          node on left side. Note that head node
          is never deleted because it is the leftmost
          node. */
    _delLesserNodes();

    /* 3\. Reverse the linked list again to retain
          the original order */
    reverseList();
}

/* Deletes nodes which have greater value node(s)
   on left side */
function _delLesserNodes()
{
    var current = head;

    // Initialise max
    var maxnode = head;
    var temp;

    while (current != null &&
           current.next != null)
    {
        /* If current is smaller than max,
           then delete current */
        if (current.next.data < maxnode.data)
        {
            temp = current.next;
            current.next = temp.next;
            temp = null;
        }

        /* If current is greater than max,
           then update max and move current */
        else
        {
            current = current.next;
            maxnode = current;
        }
    }
}

// Utility functions
// Inserts a new Node at front of the 
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

// Function to reverse the linked list
function reverseList()
{
    var current = head;
    var prev = null;
    var next;
    while (current != null)
    {
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }
    head = prev;
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
    document.write();
}

// Driver code
/* Constructed Linked List is
   12->15->10->11-> 5->6->2->3 */
push(3);
push(2);
push(6);
push(5);
push(11);
push(10);
push(15);
push(12);

document.write(
"Given Linked List<br/>");
printList();

delLesserNodes();

document.write(
"<br/>Modified Linked List<br/>");
printList();
// This code is contributed by aashish1995
</script>
```

**输出:**

```
Given Linked List 
 12 15 10 11 5 6 2 3
Modified Linked List 
 15 11 6 3
```

**方法 3:**
另一个比较简单的方法是从开始遍历列表，当当前 node <下一个 Node 时删除该节点。要删除当前节点，请遵循这种方法。让我们假设您必须删除当前节点 X:

1.  将下一个节点的数据复制到 X 中，即 X.data = X.next.data
2.  复制下一个节点的下一个地址，即 X.next = X.next.next

仅当当前节点>下一个节点时，才在列表中向前移动。

## java 描述语言

```
<script>
// Javascript program for above approach
// This class represents a single node
// in a linked list
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// This is a utility class for linked list
// This function creates a linked list from a
// given array and returns head
function createLL(arr)
{
    var head = new Node(arr[0]);
    var temp = head;

    var newNode = null;
    for (i = 1; i < arr.length; i++)
    {
        newNode = new Node(arr[i]);
        temp.next = newNode;
        temp = temp.next;
    }
    return head;
}

// This function prints given linked list
function printLL(head)
{
    while (head != null)
    {
        document.write(head.data +
                       " ");
        head = head.next;
    }
    document.write("<br/>");
}

// Main function
function deleteNodesOnRightSide(head)
{
    if (head == null ||
        head.next == null)
        return head;
    var nextNode =
        deleteNodesOnRightSide(head.next);

     if (nextNode.data > head.data)
         return nextNode;

     head.next = nextNode;
     return head;
}
var arr = [12, 15, 10, 11, 5, 6, 2, 3];
var head = createLL(arr);
document.write(
"Given Linked List<br/>");
printLL(head);
head = deleteNodesOnRightSide(head);
document.write(
"<br/>Modified Linked List<br/>");
printLL(head);
// This code is contributed by aashish1995
</script>
```

**输出:**

```
Given Linked List
12 15 10 11 5 6 2 3 
Modified Linked List
15 11 6 3
```

来源:[https://www . geeksforgeeks . org/forum/topic/Amazon-interview-question-for-software-engineer developer-about-linked-list-6](https://www.geeksforgeeks.org/forum/topic/amazon-interview-question-for-software-engineerdeveloper-about-linked-lists-6)

详情请参考[整篇文章删除右侧](https://www.geeksforgeeks.org/delete-nodes-which-have-a-greater-value-on-right-side/)数值较大的节点！