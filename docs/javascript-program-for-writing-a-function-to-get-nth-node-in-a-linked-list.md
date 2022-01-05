# 编写函数获取链表中第 n 个节点的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-写程序-函数-获取-链表中的第 n 个节点/](https://www.geeksforgeeks.org/javascript-program-for-writing-a-function-to-get-nth-node-in-a-linked-list/)

编写一个 GetNth()函数，该函数接受一个链表和一个整数索引，并返回存储在该索引位置的节点中的数据值。

**示例:**

```
Input:  1->10->30->14,  index = 2
Output: 30  
The node at index 2 is 30
```

**算法:**

```
1\. Initialize count = 0
2\. Loop through the link list
     a. If count is equal to the passed index then return 
        current node
     b. Increment count
     c. change current to point to next of the current.
```

**实施:**

## java 描述语言

```
<script>
// Javascript program to find n'th 
// node in linked list

class Node 
{
    constructor(d) 
    {
        this.data = d;
        this.next = null;
    }
}

// Head of list
var head; 

/* Takes index as argument and 
   return data at index */
function GetNth(index) 
{
    var current = head;

    // Index of Node we are currently 
    // looking at
    var count = 0; 

    while (current != null) 
    {
        if (count == index)
           return current.data;
        count++;
        current = current.next;
    }

    /* if we get to this line, the caller 
       was asking for a non-existent element 
       so we assert fail */
    assert (false);
    return 0;
}

/* Given a reference to the head of a 
   list and an int, inserts a new Node 
   on the front of the list. */
function push(new_data) 
{
    // 1\. Alloc the Node and put data 
    var new_Node = new Node(new_data);

    // 2\. Make next of new Node as head
    new_Node.next = head;

    // 3\. Move the head to point to new Node
    head = new_Node;
}

// Driver code

// Start with empty list 
// Use push() to construct list 
// 1->12->1->4->1
push(1);
push(4);
push(1);
push(12);
push(1);

// Check the count function 
document.write("Element at index 3 is " + 
                GetNth(3));
// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Element at index 3 is 4
```

**时间复杂度:** O(n)

**方法 2-带递归:**
此方法由 [MY_DOOM](https://auth.geeksforgeeks.org/user/MY_DOOM) 贡献。

**算法:**

```
getnth(node,n)
1\. Initialize count = 0
2\. if count==n
     return node->data
3\. else
    return getnth(node->next, n-1)
```

**实施:**

## java 描述语言

```
<script>
// javascript program to find n'th node 
// in linked list using recursion    

// Linked List node
class Node
{
    constructor(val) 
    {
        this.data = val;
        this.next = null;
    }
}

/* Given a reference (pointer to pointer) to the
   head of a list and an int, push a new node on
   the front of the list. */
function push(head, new_data) 
{
    // Allocate node
    var new_node = new Node(new_data);

    // Put in the data 
    new_node.data = new_data;

    new_node.next = head;
    head = new_node;
    return head;
}

/* Takes head pointer of the linked list and 
   index as arguments and return data at index */
function GetNth(head, n) 
{
    var count = 0;

    // Edge case - if head is null
    if (head == null) 
        return -1;

    // if count equal too n return node.data
    if (count == n)
        return head.data;

    // Recursively decrease n and increase
    // head to next pointer
    return GetNth(head.next, n - 1);
}

// Driver code

// Start with the empty list 
var head = null;

// Use push() to construct list
// 1->12->1->4->1
head = push(head, 1);
head = push(head, 4);
head = push(head, 1);
head = push(head, 12);
head = push(head, 1);

// Check the count function 
document.write("Element at index 3 is ", 
                GetNth(head, 3));
// This code contributed by gauravrajput1 
</script>
```

**输出:**

```
Element at index 3 is 4
```

**时间复杂度:** O(n)

详情请参考[写函数获取链表](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)中第 n 个节点的完整文章！