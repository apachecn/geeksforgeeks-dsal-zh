# 用于分离链表中奇数和偶数节点的 Javascript 程序

> 原文:[https://www . geeksforgeeks . org/JavaScript-隔离链表中奇偶节点的程序/](https://www.geeksforgeeks.org/javascript-program-for-segregating-even-and-odd-nodes-in-a-linked-list/)

给定一个整数链表，编写一个函数来修改链表，使得在修改后的链表中，所有偶数出现在所有奇数之前。此外，保持偶数和奇数的顺序相同。
**例:**

```
Input: 17->15->8->12->10->5->4->1->7->6->NULL
Output: 8->12->10->4->6->17->15->5->1->7->NULL

Input: 8->12->10->5->4->1->6->NULL
Output: 8->12->10->4->6->5->1->NULL

// If all numbers are even then do not change the list
Input: 8->12->10->NULL
Output: 8->12->10->NULL

// If all numbers are odd then do not change the list
Input: 1->3->5->7->NULL
Output: 1->3->5->7->NULL
```

**方法 1:**
思路是获取指向列表最后一个节点的指针。然后从头节点开始遍历列表，并将奇数值节点从它们的当前位置移动到列表的末尾。
感谢浮躁小子提出这个方法。
**算法:**

1.  获取指向最后一个节点的指针。
2.  将所有奇数节点移动到最后。
    *   考虑第一个偶数节点之前的所有奇数节点，并将它们移动到末尾。
    *   将头指针更改为指向第一个偶数节点。
    *   考虑第一个偶数节点之后的所有奇数节点，并将它们移动到最后。

## java 描述语言

```
<script>
// Javascript program to segregate even and
// odd nodes in a Linked List

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

function segregateEvenOdd()
{
    var end = head;
    var prev = null;
    var curr = head;

    // Get pointer to last Node
    while (end.next != null)
        end = end.next;

    var new_end = end;

    // Consider all odd nodes before
    // getting first eve node
    while (curr.data % 2 != 0 &&
           curr != end)
    {
        new_end.next = curr;
        curr = curr.next;
        new_end.next.next = null;
        new_end = new_end.next;
    }

    // Do following steps only if
    // there is an even node
    if (curr.data % 2 == 0)
    {
        head = curr;

        // Now curr points to first
        // even node
        while (curr != end)
        {
            if (curr.data % 2 == 0)
            {
                prev = curr;
                curr = curr.next;
            }
            else
            {
                // Break the link between prev
                // and curr
                prev.next = curr.next;

                // Make next of curr as null
                curr.next = null;

                // Move curr to end
                new_end.next = curr;

                // Make curr as new end of list
                new_end = curr;

                // Update curr pointer
                curr = prev.next;
            }
        }
    }

    /* We have to set prev before executing
       rest of this code */
    else
        prev = curr;

    if (new_end != end &&
        end.data % 2 != 0)
    {
        prev.next = end.next;
        end.next = null;
        new_end.next = end;
    }
}

/* Given a reference (pointer to pointer) to
   the head of a list and an int, push
   a new node on the front of the list */
function push(new_data)
{
    /* 1 & 2: Allocate the Node &
              Put in the data */
    var new_node = new Node(new_data);

    /* 3\. Make next of new Node as
          head */
    new_node.next = head;

    /* 4\. Move the head to point
          to new Node */
    head = new_node;
}

// Utility function to print
// a linked list
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

//  Driver code
push(11);
push(10);
push(8);
push(6);
push(4);
push(2);
push(0);
document.write(
         "Original Linked List ");

printList();
document.write("<br>");

segregateEvenOdd();
document.write(
         "Modified Linked List ");
// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Original Linked list 0 2 4 6 8 10 11
Modified Linked list 0 2 4 6 8 10 11
```

**时间复杂度:** O(n)

**方法二:**
思路是把链表一分为二:一个包含所有偶数节点，另一个包含所有奇数节点。最后，在偶数节点链表之后附加奇数节点链表。
要拆分链表，遍历原始链表，将所有奇数节点移动到所有奇数节点的单独链表中。在循环结束时，原始列表将包含所有偶数节点，奇数节点列表将包含所有奇数节点。为了保持所有节点的顺序相同，我们必须在奇数节点列表的末尾插入所有奇数节点。为了在恒定时间内做到这一点，我们必须跟踪奇数节点列表中的最后一个指针。

## java 描述语言

```
<script>
// JavaScript program to segregate
// even and odd nodes in a Linked List

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

function segregateEvenOdd()
{       
    var evenStart = null;
    var evenEnd = null;
    var oddStart = null;
    var oddEnd = null;
    var currentNode = head;

    while(currentNode != null)
    {
        var element = currentNode.data;

        if(element % 2 == 0)
        {               
            if(evenStart == null)
            {
                evenStart = currentNode;
                evenEnd = evenStart;
             }
             else
             {
                 evenEnd.next = currentNode;
                 evenEnd = evenEnd.next;
              }

        }
        else
        {               
            if(oddStart == null)
            {
                oddStart = currentNode;
                oddEnd = oddStart;
            }
            else
            {
                oddEnd.next = currentNode;
                oddEnd = oddEnd.next;
            }
        }

        // Move head pointer one step in
        // forward direction
        currentNode = currentNode.next;   
    }       

    if(oddStart == null ||
       evenStart == null)
    {
        return;
    }

    evenEnd.next = oddStart;
    oddEnd.next = null;
    head=evenStart;
}

/* Given a reference (pointer to pointer)
   to the head of a list and an int, push
   a new node on the front of the list. */
function push(new_data)
{
    /* 1 & 2: Allocate the Node &
              Put in the data*/
    var new_node = new Node(new_data);

    // 3\. Make next of new Node as head
    new_node.next = head;

    // 4\. Move the head to point to new Node
    head = new_node;
}

// Utility function to print a linked list
function printList()
{
    var temp = head;
    while(temp != null)
    {
        document.write(temp.data+" ");
        temp = temp.next;
    }
    document.write("<br/>");
}

// Driver code   
push(11);
push(10);
push(9);
push(6);
push(4);
push(1);
push(0);
document.write(
         "Original Linked List<br/>");
printList();

segregateEvenOdd();

document.write(
         "Modified Linked List<br/>");
printList();
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
Original Linked List
0 1 4 6 9 10 11 
Modified Linked List
0 4 6 10 1 9 11 
```

**时间复杂度:** O(n)
更多详情请参考完整文章[在链表中隔离奇偶节点](https://www.geeksforgeeks.org/segregate-even-and-odd-elements-in-a-linked-list/)！