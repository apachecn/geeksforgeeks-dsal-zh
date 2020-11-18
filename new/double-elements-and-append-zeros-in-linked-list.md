# 双元素并将零添加到链表

给定一个链表，在零之前有两个相邻的重复节点，任务是将第一个加倍，然后使下一个0。此后，将所有零附加到尾部。

**先决条件：** [单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/#singlyLinkedList)的实现基础

例子 ：

```
Input : 4 -> 4 -> 0 -> 2 -> 3 -> 4 -> 
        3 -> 3 -> 0 -> 4 -> 
Output : 8-> 2-> 3-> 4-> 6-> 4-> 0-> 
         0-> 0-> 0-> 

Explanation :
First, after doubling the first element and making
second element 0 before all zeros.
8 -> 0 -> 0 -> 2 -> 3 -> 4 -> 6 -> 0 
-> 0 -> 4 ->
Next :
8 -> 6 -> 5 -> 6 -> 0 -> 0 -> 0 -> 
0 -> 0 -> 0 -> 0 -> 

Input : 0 -> 4 -> 4 -> 0 -> 3 -> 3 -> 0 
        -> 5 -> 0 -> 0 -> 6 ->
Output : 8 -> 6 -> 5 -> 6 -> 0 -> 0 -> 0 
         -> 0 -> 0 -> 0 -> 0 ->

```

遍历链接列表，并且在0之前的节点上有两个相邻的相同数据（例如4-> 4-> 0），然后将第一个元素加倍，并将另一个设为0（例如8-> 0-> 0- >）。 最后，遍历链表并将所有零线性指向尾。

## 爪哇

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// Java code to modify linked list``import` `java.util.*;``// Linked List Node``class` `Node``{` `int` `data;` `Node next;`的 `// Constructor` `public` `Node(` `int` `data)` `{` `this` `.data = data;` `next =` `null` `;` `}``}``// Class ro perform operations``// on linked list``class` `GfG``{` `// Recursive function to double the one of two` `// elements and make next one as 0,` `// which are equal before 0` `public` `static` `void` `changeTwoBefore0(Node head)`[H TG50] `{` `// there should be atleast three elements` `// to perform required operation` `if` `(head ==` `null` `&#124;&#124; head.next ==` `null` `&#124;&#124;` `head.next.next ==` `null` `)` `return` `;`的 `// when two continuous elements` `// are same` `if` `((head.data == head.next.data) &&` `(head.next.next.data ==` `0` `))` `{` `int` `temp = head.data;` `head.data =` `2` `*temp;` `head.next.data =` `0` `;` `if` `(head.next.next.next !=` `null` `)` `head = head.next.next.next;` `else` [ `return` `;` `}` `else` `head = head.next;` `// recursive call to changeTwoBefore0` `// for next element` `changeTwoBefore0(head);` `}` [ `// function to append zeros at tail` `public` `static` `Node appendZero(Node head)` `{` `if` `(head ==` `null` `&#124;&#124; head.next ==` `null` `)` `return` `head;`的 `// Find tail node` `Node tail = head;` `while` `(tail.next !=` `null` `)` `tail = tail.next;` `Node  origTail = tail;` `// Case when starting nodes have 0 values` `// we need to change head in this case.` `Node curr = head;` `while` `(curr.next !=` `null` `&& curr.data ==` `0` `)` `{` `tail.next = curr;` `tail = curr;` `curr = curr.next;` `}` `head  = curr;` `// Now moving other 0s to end` `curr = curr.next;` `// We check until original tail` `while` `(curr != origTail)`] `{` `// If current data is 0, append` `// after tail and update tail.` `if` `(curr.data ==` `0` `)` `{` `tail.next = curr;` `tail = curr;` `prev.next = curr.next;` `}` `else` `prev = curr;` `// We always move current        ` `curr = curr.next;` `}`[ `// Finally making sure that linked` `// list is null terminated.` `tail.next =` `null` `;` `return` `head;` `}` `public` ] `static` `Node doubleAndAppend0(Node head)` `{` `// Change two same nodes before 0` `changeTwoBefore0(head);`[ `// Move all 0s to end` `return` `appendZero(head);` `}` ] `// function to display the nodes` `public` `static` `void` `display(Node head)` ​​ `{` `while` `(head !=` `null` `)` `{` `System.out.print(head.data +` `" -> "` `);` `head = head.next;` `}` `}`[HTG290 `// Driver code` `public` `static` `void` `main(String[] args)` `{` `Node head =` `new` `Node(` `4` `);` `head.next =` `new` `Node(` `4` `);` `head.next.next =` `new` `Node(` `0` `);` `head.next.next.next =` [HTG3 21] `Node(` `2` `);` `head.next.next.next.next =` `new` `Node(` `3` `);` `head.next.next.next.next.next =` `new` `Node(` `4` `);` `head.next.next.next.next.next.next =` `new` `Node(` `3` `);` `head.next.next.next.next.next.next.next =` `new` `Node(` `3` `);` `head.next.next.next.next.next.next.next.next =` `new` `Node(` `0` `);` `head.next.next.next.next.next.next.next.next.next =` `new` `Node(` `4` `);` `System.out.println(` `"Original linked list :"` `);` `display(head);` `head = doubleAndAppend0(head);` `System.out.println(` `"\nModified linked list :"` `);` ] `display(head);` `}``}` |

*chevron_right**filter_none*