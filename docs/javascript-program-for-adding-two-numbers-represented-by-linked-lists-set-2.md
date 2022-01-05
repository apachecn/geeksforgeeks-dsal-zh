# 用链表表示的两个数相加的 Javascript 程序-集合 2

> 原文:[https://www . geesforgeks . org/JavaScript-用于添加两个数字的程序-由链表表示-set-2/](https://www.geeksforgeeks.org/javascript-program-for-adding-two-numbers-represented-by-linked-lists-set-2/)

给定两个由两个链表表示的数字，编写一个返回求和列表的函数。求和列表是两个输入数字相加的链表表示。不允许修改列表。另外，不允许使用显式的额外空间(提示:使用递归)。

**例**:

```
Input:
First List: 5->6->3  
Second List: 8->4->2 

Output:
Resultant list: 1->4->0->5
```

我们在这里讨论了一个解决方案，它适用于链表，其中最低有效位是链表的第一个节点，最高有效位是最后一个节点。在这个问题中，最重要的节点是第一个节点，最不重要的数字是最后一个节点，我们不允许修改列表。这里使用递归从右向左计算总和。

以下是步骤。

1.  Calculate sizes of given two linked lists.
2.  如果大小相同，则使用递归计算总和。将递归调用堆栈中的所有节点保留到最右边的节点，计算最右边节点的总和，并向左侧结转。
3.  如果大小不一样，则按照以下步骤操作:
    *   计算两个链表的大小差。让差异不同。
    *   在更大的链表中向前移动 *diff* 节点。现在使用步骤 2 计算较小列表和较大列表的右边子列表(大小相同)的总和。另外，存储这个总和的进位。
    *   计算进位(在上一步中计算)与较大列表的剩余左子列表的总和。此总和的节点被添加到上一步获得的总和列表的开头。

以下是上述方法的模拟运行:

![](img/dee4d25298ae9b88a4fb4ed12da5149e.png)

下图是上述方法的实现。

## java 描述语言

```
<script>
// A javascript recursive program to 
// add two linked lists
class node 
{
    constructor(val) 
    {
        this.val = val;
        this.next = null;
    }
}

// Function to print linked list
function printlist( head) 
{
    while (head != null) 
    {
        document.write(head.val + " ");
        head = head.next;
    }
}

var head1, head2, result;
var carry;

/* A utility function to push a 
   value to linked list */
function push(val, list) 
{
    var newnode = new node(val);
    if (list == 1) 
    {
        newnode.next = head1;
        head1 = newnode;
    } 
    else if (list == 2) 
    {
        newnode.next = head2;
        head2 = newnode;
    } 
    else 
    {
        newnode.next = result;
        result = newnode;
    }
}

// Adds two linked lists of same size 
// represented by head1 and head2 and 
// returns head of the resultant 
// linked list. Carry is propagated 
// while returning from the recursion
function addsamesize(n, m) 
{
    // Since the function assumes 
    // linked lists are of same size, 
    // check any of the two head pointers
    if (n == null)
        return;

    // Recursively add remaining nodes 
    // and get the carry
    addsamesize(n.next, m.next);

    // Add digits of current nodes and 
    // propagated carry
    var sum = n.val + m.val + carry;
    carry = parseInt(sum / 10);
    sum = sum % 10;

    // Push this to result list
    push(sum, 3);
}

var cur;

// This function is called after the 
// smaller list is added to the bigger 
// lists's sublist of same size. Once 
// the right sublist is added, the carry 
// must be added to the left side of 
// larger list to get the final result.
function propogatecarry(head1) 
{
    // If diff. number of nodes are not
    // traversed, add carry
    if (head1 != cur) 
    {            
        propogatecarry(head1.next);
        var sum = carry + head1.val;
        carry = parseInt(sum / 10);
        sum %= 10;

        // Add this node to the front 
        // of the result
        push(sum, 3);
    }
}

function getsize(head) 
{
    var count = 0;
    while (head != null) 
    {
        count++;
        head = head.next;
    }
    return count;
}

// The main function that adds two 
// linked lists represented by head1 
// and head2\. The sum of two lists 
// is stored in a list referred by 
// result
function addlists() 
{
    // first list is empty
    if (head1 == null) 
    {
        result = head2;
        return;
    }

    // First list is empty
    if (head2 == null) 
    {
        result = head1;
        return;  
    }

    var size1 = getsize(head1);
    var size2 = getsize(head2);

    // Add same size lists
    if (size1 == size2) 
    {
        addsamesize(head1, head2);
    } 
    else   
    {
        // First list should always be 
        // larger than second list.
        // If not, swap pointers
        if (size1 < size2) 
        {
            var temp = head1;
            head1 = head2;
            head2 = temp;
        }
        var diff = 
            Math.abs(size1 - size2);

        // Move diff. number of nodes in 
        // first list
        var temp = head1;
        while (diff-- >= 0) 
        {
            cur = temp;
            temp = temp.next;
        }

        // Get addition of same size lists
        addsamesize(cur, head2);

        // Get addition of remaining first 
        // list and carry
        propogatecarry(head1);
    }
    // If some carry is still there, add 
    // a new node to the front of the result 
    // list. e.g. 999 and 87
    if (carry > 0)
        push(carry, 3);
}

// Driver code
head1 = null;
head2 = null;
result = null;
carry = 0;
var arr1 = [9, 9, 9];
var arr2 = [1, 8];

// Create first list as 9->9->9
for (i = arr1.length - 1; i >= 0; --i)
    push(arr1[i], 1);

// Create second list as 1->8
for (i = arr2.length - 1; i >= 0; --i)
    push(arr2[i], 2);

addlists();
printlist(result);
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
1 0 1 7
```

**时间复杂度:** O(m+n)，其中 m 和 n 是给定的两个链表的大小。

**迭代方法:**

这个实现没有任何递归调用开销，这意味着它是一个迭代解决方案。

因为我们需要从两个链表的最后一个开始添加数字。因此，这里我们将使用堆栈数据结构来实现这一点。

*   我们将首先从给定的两个链表中创建两个栈。
*   然后，我们将运行一个循环，直到两个堆栈都变空。
*   在每次迭代中，我们跟踪进位。
*   最后，如果进位> 0，这意味着我们需要在结果列表的开头有额外的节点来容纳这个进位。

## java 描述语言

```
<script>
// Javascript Iterative program to add 
// two linked lists       
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}
var l1, l2, result;

// To push a new node to 
// linked list
function push(new_data) 
{
    // Allocate node
    var new_node = new Node(0);

    // Put in the data
    new_node.data = new_data;

    // Link the old list off the 
    // new node
    new_node.next = l1;

    // Move the head to point to the 
    // new node
    l1 = new_node;
}

function push1(new_data) 
{
    // Allocate node
    var new_node = new Node(0);

    // Put in the data
    new_node.data = new_data;

    // Link the old list off the 
    // new node
    new_node.next = l2;

    // Move the head to point to
    // the new node
    l2 = new_node;
}

// To add two new numbers
function addTwoNumbers() 
{
    var stack1 = [];
    var stack2 = [];

    while (l1 != null) 
    {
        stack1.push(l1.data);
        l1 = l1.next;
    }

    while (l2 != null) 
    {
        stack2.push(l2.data);
        l2 = l2.next;
    }

    var carry = 0;
    var result = null;

    while (stack1.length != 0 || 
           stack2.length != 0) 
    {
        var a = 0, b = 0;

        if (stack1.length != 0) 
        {
            a = stack1.pop();
        }

        if (stack2.length != 0) 
        {
            b = stack2.pop();
        }

        var total = a + b + carry;
        var temp = new Node(total % 10);
        carry = parseInt(total / 10);

        if (result == null) 
        {
            result = temp;
        } 
        else 
        {
            temp.next = result;
            result = temp;
        }
    }

    if (carry != 0) 
    {
        var temp = new Node(carry);
        temp.next = result;
        result = temp;
    }
    return result;
}

// To print a linked list
function printList() 
{
    while (result != null) 
    {
        document.write(result.data + " ");
        result = result.next;
    }
    document.write();
}

// Driver code
var arr1 = [5, 6, 7];
var arr2 = [1, 8];

var size1 = 3;
var size2 = 2;

// Create first list as 
// 5->6->7
var i;
for (var i = size1 - 1; i >= 0; --i)
push(arr1[i]);

// Create second list as 1->8
for (i = size2 - 1; i >= 0; --i)
    push1(arr2[i]);

result = addTwoNumbers();
printList();
// This code contributed by umadevi9616 
</script>
```

**输出:**

```
5 8 5
```

相关文章:[添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/)
详情请参考[添加两个链表表示的数字|集合 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/) 完整文章！