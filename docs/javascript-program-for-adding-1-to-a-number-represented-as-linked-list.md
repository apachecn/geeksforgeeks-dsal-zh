# 用于向表示为链表的数字加 1 的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-用于将 1 添加到表示为链表的数字中的程序/](https://www.geeksforgeeks.org/javascript-program-for-adding-1-to-a-number-represented-as-linked-list/)

数字在链表中表示，每个数字对应链表中的一个节点。再加 1。例如，1999 被表示为(1-> 9-> 9 -> 9)，将 1 添加到它应该会将其更改为(2->0->0->0)

以下是步骤:

1.  反转给定的链表。例如，1-> 9-> 9 -> 9 被转换为 9-> 9-> 9-> 9-> 1。
2.  从最左边的节点开始遍历链表，并向其中添加 1。如果有进位，移到下一个节点。当有进位时，继续移动到下一个节点。
3.  反向修改链表和返回头。

下面是以上步骤的实现。

## java 描述语言

```
<script>
// Javascript program to add 1 to 
// a linked list 

// Linked list node 
class Node 
{ 
    constructor()
    {
        this.data = 0;
        this.next = null;
    }
}; 

/* Function to create a new node 
   with given data */
function newNode(data) 
{ 
    var new_node = new Node(); 
    new_node.data = data; 
    new_node.next = null; 
    return new_node; 
} 

// Function to reverse the 
// linked list 
function reverse(head) 
{ 
    var prev = null; 
    var current = head; 
    var next; 
    while (current != null) 
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    } 
    return prev; 
} 

/* Adds one to a linked lists and 
   return the head node of resultant 
   list */
function addOneUtil(head) 
{ 
    // res is head node of the 
    // resultant list 
    var res = head; 
    var temp, prev = null; 

    var carry = 1, sum; 

    // while both lists exist 
    while (head != null) 
    { 
        // Calculate value of next digit in 
        // resultant list. The next digit is 
        // sum of following things 
        // (i) Carry 
        // (ii) Next digit of head list (if 
        // there is a next digit) 
        sum = carry + head.data; 

        // update carry for next calculation 
        carry = (sum >= 10)? 1 : 0; 

        // update sum if it is greater than 10 
        sum = sum % 10; 

        // Create a new node with sum as data 
        head.data = sum; 

        // Move head and second pointers to 
        // next nodes 
        temp = head; 
        head = head.next; 
    } 

    // if some carry is still there, add a 
    // new node to result list. 
    if (carry > 0) 
        temp.next = newNode(carry); 

    // return head of the resultant list 
    return res; 
} 

// This function mainly uses addOneUtil(). 
function addOne(head) 
{ 
    // Reverse linked list 
    head = reverse(head); 

    // Add one from left to right of 
    // reversed list 
    head = addOneUtil(head); 

    // Reverse the modified list 
    return reverse(head); 
} 

// A utility function to print a 
// linked list 
function printList(node) 
{ 
    while (node != null) 
    { 
        document.write(node.data); 
        node = node.next; 
    } 
    document.write("<br>");
} 

// Driver code
var head = newNode(1); 
head.next = newNode(9); 
head.next.next = newNode(9); 
head.next.next.next = newNode(9); 
document.write( "List is "); 
printList(head); 
head = addOne(head); 
document.write("<br>Resultant list is "); 
printList(head); 
// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
List is 1999
Resultant list is 2000
```

**递归实现:**
我们可以递归到达最后一个节点，并结转到之前的节点。递归解决方案不需要链表的反转。我们也可以用堆栈代替递归来临时保存节点。

下面是递归解决方案的实现。

## java 描述语言

```
<script>
// Recursive JavaScript program
// to add 1 to a linked list
// Linked list node 
class Node
{
    constructor() 
    {
        this.data = 0;
        this.next = null;
    }
}

/* Function to create a new node 
   with given data */
function newNode(data) 
{
    var new_node = new Node();
    new_node.data = data;
    new_node.next = null;
    return new_node;
}

// Recursively add 1 from end to 
// beginning and returns carry after 
// all nodes are processed.
function addWithCarry(head) 
{
    // If linked list is empty, then
    // return carry
    if (head == null) return 1;

    // Add carry returned be next node 
    // call
    var res = head.data + addWithCarry(head.next);

    // Update data and return new carry
    head.data = res % 10;
    return parseInt(res / 10);
}

// This function mainly uses 
// addWithCarry().
function addOne(head) 
{
    // Add 1 to linked list from end  
    // to beginning
    var carry = addWithCarry(head);
    var newNodes = null;

    // If there is carry after processing 
    // all nodes, then we need to add a 
    // new node to linked list
    if (carry > 0) 
    {
        newNodes = newNode(carry);
        newNodes.next = head;

        // New node becomes head now
        return newNodes; 
    }

    return head;
}

// A utility function to print a 
// linked list
function printList(node) 
{
    while (node != null) 
    {
        document.write(node.data);
        node = node.next;
    }
    document.write("<br>");
}

// Driver code 
var head = newNode(1);
head.next = newNode(9);
head.next.next = newNode(9);
head.next.next.next = newNode(9);

document.write("List is ");
printList(head);

head = addOne(head);
document.write("<br>");
document.write("Resultant list is ");
printList(head);
</script>
```

**输出:**

```
List is 1999
Resultant list is 2000
```

更多详情请参考[上的完整文章将 1 添加到表示为链表](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)的数字中！