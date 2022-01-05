# 用于在链表中搜索元素的 Javascript 程序

> 原文:[https://www . geesforgeks . org/JavaScript-program-for-search-in-a-element-in-a-link-list/](https://www.geeksforgeeks.org/javascript-program-for-searching-an-element-in-a-linked-list/)

编写一个函数，在给定的单链表中搜索给定的键“x”。如果 x 出现在链表中，函数应该返回 true，否则返回 false。

```
bool search(Node *head, int x) 
```

例如，如果要搜索的关键字是 15，链表是 14->21->11->30->10，那么函数应该返回 false。如果要搜索的关键字是 14，那么函数应该返回 true。
**迭代求解:**

```
1) Initialize a node pointer, current = head.
2) Do following while current is not NULL
    a) current->key is equal to the key being searched return true.
    b) current = current->next
3) Return false 
```

下面是上述算法的迭代实现，以搜索给定的关键字。

## java 描述语言

```
<script>
// Iterative javascript program
// to search an element
// in linked list

//Node class
class Node
{
    constructor(d)
    {
        this.data = d;
        this.next = null;
    }
}

// Linked list class

// Head of list
var head;

// Inserts a new node at the front of the list
function push(new_data)
{
    // Allocate new node and putting data
    var new_node = new Node(new_data);

    // Make next of new node as head
    new_node.next = head;

    // Move the head to point to new Node
    head = new_node;
}

// Checks whether the value
// x is present in linked list
function search(head , x)
{
    // Initialize current
    var current = head;

    while (current != null)
    {
        if (current.data == x)

            // Data found
            return true;
            current = current.next;
        }

        // Data not found
        return false;
}

// Driver code

// Start with the empty list
// Use push() to construct list
// 14->21->11->30->10
push(10);
push(30);
push(11);
push(21);
push(14);

if (search(head, 21))
    document.write("Yes");
else
    document.write("No");
// This code contributed by aashish1995
</script>
```

**输出:**

```
Yes
```

**递归解:**

```
bool search(head, x)
1) If head is NULL, return false.
2) If head's key is same as x, return true;
3) Else return search(head->next, x) 
```

下面是上述算法的递归实现，用于搜索给定的关键字。

## java 描述语言

```
<script>
// Recursive javascript program to search
// an element in linked list

// Node class
class Node
{
    constructor(val)
    {
        this.data = val;
        this.next = null;
    }
}

// Linked list class
// Head of list
var head;

// Inserts a new node at the front
// of the list
function push(new_data)
{
    // Allocate new node and putting data
    var new_node = new Node(new_data);

    // Make next of new node as head
    new_node.next = head;

    // Move the head to point to new Node
    head = new_node;
}

// Checks whether the value x is present
// in linked list
function search(head, x)
{
    // Base case
    if (head == null)
        return false;

    // If key is present in current node,
    // return true
    if (head.data == x)
        return true;

    // Recur for remaining list
    return search(head.next, x);
}

// Driver code

// Start with the empty list
// Use push() to construct list
// 14->21->11->30->10
push(10);
push(30);
push(11);
push(21);
push(14);

if (search(head, 21))
    document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1
</script>
```

**输出:**

```
Yes
```

更多细节请参考完整的文章[在链表中搜索元素(迭代和递归)](https://www.geeksforgeeks.org/search-an-element-in-a-linked-list-iterative-and-recursive/)！