# 拉平链表的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-扁平化-a-link-list/](https://www.geeksforgeeks.org/javascript-program-for-flattening-a-linked-list/)

给定一个链表，其中每个节点代表一个链表，并包含两个同类型的指针:

1.  指向主列表中下一个节点的指针(我们在下面的代码中称之为“右”指针)。
2.  指向该节点所在的链表的指针(我们在下面的代码中称之为“向下”指针)。

所有链接列表都已排序。请参见以下示例

```
       5 -> 10 -> 19 -> 28
       |    |     |     |
       V    V     V     V
       7    20    22    35
       |          |     |
       V          V     V
       8          50    40
       |                |
       V                V
       30               45
```

编写函数 flat()将列表展平为一个链表。展平的链表也应该排序。例如，对于上面的输入列表，输出列表应该是 5-> 7-> 8-> 10-> 19-> 20-> 22-> 28-> 30-> 35-> 40-> 45-> 50。

想法是使用[的 Merge()过程对链表进行合并排序。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)我们使用 merge()逐个合并列表。我们递归合并()当前列表和已经展平的列表。
向下指针用于链接展平列表的节点。

下面是上述方法的实现:

## java 描述语言

```
<script>
// Javascript program for flattening 
// a Linked List

// Head of list
var head; 

// Linked list Node 
class Node 
{
    constructor(val) 
    {
        this.data = val;
        this.down = null;
        this.next = null;
    }
}

// An utility function to merge 
// two sorted linked lists
function merge(a, b) 
{
    // If first linked list is 
    // empty then second is the 
    // answer
    if (a == null)
    return b;

    // If second linked list is 
    // empty then first is the 
    // result
    if (b == null)
        return a;

    // Compare the data members of 
    // the two linked lists and put 
    // the larger one in the result
    var result;

    if (a.data < b.data) 
    {
        result = a;
        result.down = merge(a.down, b);
    }

    else 
    {
        result = b;
        result.down = merge(a, b.down);
    }

    result.right = null;
    return result;
}

function flatten(root) 
{
    // Base Cases
    if (root == null || 
        root.right == null)
        return root;

    // Recur for list on right
    root.right = flatten(root.right);

    // Now merge
    root = merge(root, root.right);

    // Return the root
    // It will be in turn merged
    // with its left
    return root;
}

/* Utility function to insert a node 
   at beginning of the linked list */
function push(head_ref, data) 
{
    /* 1 & 2: Allocate the Node & 
              Put in the data */
         var new_node = new Node(data);

    // 3\. Make next of new Node as head
    new_node.down = head_ref;

    // 4\. Move the head to point to 
    // new Node 
    head_ref = new_node;

    // 5\. return to link it back 
        return head_ref;
}

function printList() 
{
    var temp = head;
    while (temp != null) 
    {
        document.write(temp.data + " ");
        temp = temp.down;
    }
    document.write();
}

// Driver code
/* Create the following linked list 
   5 -> 10 -> 19 -> 28 | | | | V V V 
   V 7 20 22 35 | | | V V V 8 50 40 
   | | V V 30 45 */
head = push(head, 30);
head = push(head, 8);
head = push(head, 7);
head = push(head, 5);

head.right = push(head.right, 20);
head.right = push(head.right, 10);

head.right.right = 
push(head.right.right, 50);
head.right.right = 
push(head.right.right, 22);
head.right.right = 
push(head.right.right, 19);

head.right.right.right = 
push(head.right.right.right, 45);
head.right.right.right = 
push(head.right.right.right, 40);
head.right.right.right = 
push(head.right.right.right, 35);
head.right.right.right = 
push(head.right.right.right, 20);

// Flatten the list
head = flatten(head);

printList();
// This code is contributed by aashish1995 
</script>
```

**输出:**

```
5 7 8 10 19 20 20 22 30 35 40 45 50
```

更多详情请参考[整平链表](https://www.geeksforgeeks.org/flattening-a-linked-list/)整篇文章！