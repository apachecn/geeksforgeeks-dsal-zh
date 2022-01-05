# 检查单链表是否回文的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-程序检查单链表是否是回文/](https://www.geeksforgeeks.org/javascript-program-to-check-if-a-singly-linked-list-is-palindrome/)

给定一个字符的单链表，写一个函数，如果给定的列表是回文，则返回 true，否则返回 false。

![Palindrome Linked List](img/7eef7faffebfb5a692784722f81c0a42.png)

**方法 1(使用堆栈)**

*   一个简单的解决方案是使用列表节点的堆栈。这主要涉及三个步骤。
*   从头到尾遍历给定的列表，并将每个访问过的节点推送到堆栈。
*   再次遍历列表。对于每个访问的节点，从堆栈中弹出一个节点，并将弹出的节点的数据与当前访问的节点进行比较。
*   如果所有节点都匹配，则返回 true，否则返回 false。

下图是上述方法的模拟运行:

![](img/8a3805a79066e7839ba6a0ca7e487a44.png)

下面是上述方法的实现:

## java 描述语言

```
<script>
// JavaScript program to check if
// linked list is palindrome recursively
class Node
{
    constructor(val)
    {
        this.data = val;
        this.ptr = null;
    }
}

var one = new Node(1);
var two = new Node(2);
var three = new Node(3);
var four = new Node(4);
var five = new Node(3);
var six = new Node(2);
var seven = new Node(1);
one.ptr = two;
two.ptr = three;
three.ptr = four;
four.ptr = five;
five.ptr = six;
six.ptr = seven;
var condition = isPalindrome(one);
document.write("isPalidrome: " + condition);

function isPalindrome(head)
{
    var slow = head;
    var ispalin = true;
    var stack = [];

    while (slow != null)
    {
        stack.push(slow.data);
        slow = slow.ptr;
    }

    while (head != null)
    {
        var i = stack.pop();
        if (head.data == i)
        {
            ispalin = true;
        }
        else
        {
            ispalin = false;
            break;
        }
        head = head.ptr;
    }
    return ispalin;
}
// This code is contributed by todaysgaurav
</script>
```

**输出:**

```
 isPalindrome: true
```

**时间复杂度:** O(n)。

**方法 2(通过反转列表):**
这个方法需要 O(n)个时间和 O(1)个额外空间。
**1)** 获得链表的中间。
**2)** 反转后半部分链表。
**3)** 检查前半部分和后半部分是否相同。
**4)** 通过再次反转后半部分并将其附着回前半部分来构建原始链表

将列表分成两半，使用[这个](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)帖子的方法 2。

当节点数为偶数时，前半部分和后半部分正好包含一半节点。这种方法的挑战是处理节点数为奇数的情况。我们不希望中间节点成为列表的一部分，因为我们要比较它们是否相等。对于奇数情况，我们使用一个单独的变量“中间节点”。

## java 描述语言

```
<script>
// Javascript program to check if
// linked list is palindrome

// Head of list
var head;
var slow_ptr,
    fast_ptr, second_half;

// Linked list Node
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Function to check if given linked list
// is palindrome or not
function isPalindrome(head)
{
    slow_ptr = head;
    fast_ptr = head;
    var prev_of_slow_ptr = head;

    // To handle odd size list
    var midnode = null;

    // Initialize result
    var res = true;

    if (head != null &&
        head.next != null)
    {
        // Get the middle of the list.
        // Move slow_ptr by 1 and fast_ptrr
        // by 2, slow_ptr will have the middle node
        while (fast_ptr != null &&
               fast_ptr.next != null)
        {
            fast_ptr = fast_ptr.next.next;

            // We need previous of the slow_ptr for
            //  linked lists with odd elements
            prev_of_slow_ptr = slow_ptr;
            slow_ptr = slow_ptr.next;
        }

        // fast_ptr would become NULL when there are
        // even elements in the list and not NULL for
        // odd elements. We need to skip the middle
        // node for odd case and store it somewhere
        // so that we can restore the original list        
        if (fast_ptr != null)
        {
            midnode = slow_ptr;
            slow_ptr = slow_ptr.next;
        }

        // Now reverse the second half and
        // compare it with first half
        second_half = slow_ptr;

        // NULL terminate first half
        prev_of_slow_ptr.next = null;

        // Reverse the second half
        reverse();

        // compare
        res = compareLists(head, second_half);

        // Construct the original list back
        // Reverse the second half again
        reverse();

        if (midnode != null)
        {
            // If there was a mid node (odd size case)
            // which was not part of either first half
            // or second half.
            prev_of_slow_ptr.next = midnode;
            midnode.next = second_half;
         }
         else
             prev_of_slow_ptr.next = second_half;
    }
    return res;
}

// Function to reverse the linked list.
// Note that this function may change the
// head
function reverse()
{
    var prev = null;
    var current = second_half;
    var next;
    while (current != null)
    {
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;
    }
    second_half = prev;
}

// Function to check if two input
// lists have same data
function compareLists(head1, head2)
{
    var temp1 = head1;
    var temp2 = head2;

    while (temp1 != null &&
           temp2 != null)
    {
        if (temp1.data == temp2.data)
        {
            temp1 = temp1.next;
            temp2 = temp2.next;
        }
        else
            return false;
    }

    // Both are empty return 1
    if (temp1 == null &&
        temp2 == null)
        return true;

    //Will reach here when one is NULL
    //  and other is not
    return false;
}

// Push a node to the linked list.
// Note that this function changes the head
function push(new_data)
{
    // Allocate the Node & Put in the data
    var new_node = new Node(new_data);

    // link the old list off the new one
    new_node.next = head;

    // Move the head to point to new Node
    head = new_node;
}

// A utility function to point a
// given linked list
function printList(ptr)
{
    while (ptr != null)
    {
        document.write(ptr.data + "->");
        ptr = ptr.next;
    }
        document.write("NULL<br/>");
}

// Driver code

// Start with the empty list
var str = ['a', 'b', 'a',
           'c', 'a', 'b', 'a'];
var string = str.toString();

for (i = 0; i < 7; i++)
{
    push(str[i]);
    printList(head);
    if (isPalindrome(head) != false)
    {
        document.write("Is Palindrome");
        document.write("<br/>");
    }
    else
    {
        document.write("Not Palindrome");
        document.write("<br/>");
    }
}
// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
a->NULL
Is Palindrome

b->a->NULL
Not Palindrome

a->b->a->NULL
Is Palindrome

c->a->b->a->NULL
Not Palindrome

a->c->a->b->a->NULL
Not Palindrome

b->a->c->a->b->a->NULL
Not Palindrome

a->b->a->c->a->b->a->NULL
Is Palindrome
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**方法 3(使用递归):**
使用左右两个指针。使用递归左右移动，并检查每个递归调用中的后续操作。
1)子列表是回文。
2)当前左右值匹配。

如果以上两个条件都成立，那么返回真。

其思想是使用函数调用堆栈作为容器。递归遍历，直到列表结束。当我们从最后一个空值返回时，我们将处于最后一个节点。最后一个节点将与列表的第一个节点进行比较。

为了访问列表的第一个节点，我们需要列表头在递归的最后一次调用中可用。因此，我们也将 head 传递给递归函数。如果它们都匹配，我们需要比较(2，n-2)个节点。同样，当递归回落到(n-2)第二个节点时，我们需要从头部引用第二个节点。我们在前面的调用中推进头指针，以引用列表中的下一个节点。
然而，诀窍在于识别双指针。传递一个指针就像传递一个值一样好，我们会一次又一次地传递同一个指针。我们需要传递头指针的地址，以反映父递归调用的变化。
感谢**沙拉德·钱德拉**提出这个方法。

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Head of the list
var head;
var left;

class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Initial parameters to this function
// are &head and head
function isPalindromeUtil(right)
{
    left = head;

    // Stop recursion when right
    // becomes null
    if (right == null)
        return true;

    // If sub-list is not palindrome then
    // no need to check for the current
    // left and right, return false
    var isp = isPalindromeUtil(right.next);
    if (isp == false)
        return false;

    // Check values at current left and right
    var isp1 = (right.data == left.data);

    left = left.next;

    // Move left to next node;
    return isp1;
}

// A wrapper over isPalindrome(Node head)
function isPalindrome(head)
{
    var result = isPalindromeUtil(head);
    return result;
}

// Push a node to linked list.
// Note that this function changes
// the head
function push(new_data)
{
    // Allocate the node and
    //  put in the data
    var new_node = new Node(new_data);

    // Link the old list off the
    // the new one
    new_node.next = head;

    // Move the head to point to new node
    head = new_node;
}

// A utility function to point a
// given linked list
function printList(ptr)
{
    while (ptr != null)
    {
        document.write(ptr.data + "->");
        ptr = ptr.next;
    }
    document.write("Null ");
    document.write("<br>");

}

// Driver Code
var str = ['a', 'b', 'a',
           'c', 'a', 'b', 'a'];
for (var i = 0; i < 7; i++)
{
    push(str[i]);
    printList(head);

     if (isPalindrome(head))
     {
         document.write("Is Palindrome");
         document.write("<br/>");
         document.write("<br>");
     }
     else
     {
         document.write("Not Palindrome");
         document.write("<br/>");
         document.write("<br/>");
     }
}
// This code is contributed by aashish1995
/script>
```

**输出:**

```
a->NULL
Not Palindrome

b->a->NULL
Not Palindrome

a->b->a->NULL
Is Palindrome

c->a->b->a->NULL
Not Palindrome

a->c->a->b->a->NULL
Not Palindrome

b->a->c->a->b->a->NULL
Not Palindrome

a->b->a->c->a->b->a->NULL
Is Palindrome
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)如果考虑函数调用栈大小，否则为 O(1)。

更多详情请参考[函数整篇文章，查看单链表是否回文](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)！