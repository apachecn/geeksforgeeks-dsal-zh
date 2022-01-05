# 用链表表示的两个数字相加的 Javascript 程序-集合 1

> 原文:[https://www . geesforgeks . org/JavaScript-program-add-two-numbers-由链表表示-set-1/](https://www.geeksforgeeks.org/javascript-program-to-add-two-numbers-represented-by-linked-lists-set-1/)

给定两个由两个列表表示的数字，编写一个返回求和列表的函数。求和列表是两个输入数字相加的列表表示。

**例**:

```
Input: 
List1: 5->6->3 // represents number 563 
List2: 8->4->2 // represents number 842 
Output: 
Resultant list: 1->4->0->5 // represents number 1405 
Explanation: 563 + 842 = 1405

Input: 
List1: 7->5->9->4->6 // represents number 75946
List2: 8->4 // represents number 84
Output: 
Resultant list: 7->6->0->3->0// represents number 76030
Explanation: 75946+84=76030

```

**接近**:遍历两个列表，逐个选择两个列表的节点，并添加值。如果总和大于 10，则进位为 1 并减少总和。如果一个列表中的元素比另一个列表中的多，则认为该列表的剩余值为 0。

**步骤为:**

1.  从头到尾遍历两个链表
2.  将相应链接列表中的两位数字相加。
3.  如果其中一个列表已到达末尾，则取 0 作为它的数字。
4.  继续下去，直到两个列表都结束。
5.  如果两位数之和大于 9，则将进位设置为 1，将当前数字设置为*和% 10*

下面是这个方法的实现。

## java 描述语言

```
<script>
// Javascript program to add two numbers
// represented by linked list
var head1, head2;

class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

/* Adds contents of two linked lists 
   and return the head node of resultant 
   list */
function  addTwoLists(first, second) 
{
    // res is head node of the resultant 
    // list
    var res = null;
    var prev = null;
    var temp = null;
    var carry = 0, sum;

    // while both lists exist
    while (first != null || 
           second != null) 
    {
        // Calculate value of next digit in 
        // resultant list. The next digit is 
        // sum of following things
        // (i) Carry
        // (ii) Next digit of first list (if 
        // there is a next digit)
        // (ii) Next digit of second list (if 
        // there is a next digit)
        sum = carry + (first != null ? first.data : 0) +
              (second != null ? second.data : 0);

        // Update carry for next calculation
        carry = (sum >= 10) ? 1 : 0;

        // Update sum if it is greater than 10
        sum = sum % 10;

        // Create a new node with sum as data
        temp = new Node(sum);

        // If this is the first node then set
        // it as head of the resultant list
        if (res == null) 
        {
            res = temp;
        }

        // If this is not the first node then 
        // connect it to the rest.
        else 
        {
            prev.next = temp;
        }

        // Set prev for next insertion
        prev = temp;

        // Move first and second pointers to 
        // next nodes
        if (first != null) 
        {
            first = first.next;
        }
        if (second != null)  
        {
            second = second.next;
        }
    }

    if (carry > 0) 
    {
        temp.next = new Node(carry);
    }

    // return head of the resultant list
    return res;
}

/* Utility function to print a 
   linked list */
function  printList(head) 
{
    while (head != null) 
    {
        document.write(head.data + " ");
        head = head.next;
    }
    document.write("<br/>");
}

// Driver Code
// Creating first list
head1 = new Node(7);
head1.next = new Node(5);
head1.next.next = new Node(9);
head1.next.next.next = new Node(4);
head1.next.next.next.next = new Node(6);
document.write("First List is ");
printList(head1);

// Creating second list
head2 = new Node(8);
head2.next = new Node(4);
document.write("Second List is ");
printList(head2);

// Add the two lists and see the 
// result
rs = addTwoLists(head1, head2);
document.write("Resultant List is ");
printList(rs);
// This code is contributed by aashish1995 
</script>
```

**输出:**

```
First List is 7 5 9 4 6 
Second List is 8 4 
Resultant list is 5 0 0 5 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m + n)，其中 m 和 n 分别是第一和第二列表中的节点数。
    列表只需遍历一次。
*   **空间复杂度:** O(m + n)。
    需要一个临时链表来存储输出号

相关文章:[添加两个链表表示的数字|集合 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/)

更多详情请参考[整篇文章添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/) ！