# 用下一个随机指针集克隆链表的 Javascript 程序 2

> 原文:[https://www . geesforgeks . org/JavaScript-克隆程序-带有下一个随机指针集的链表-2/](https://www.geeksforgeeks.org/javascript-program-for-cloning-a-linked-list-with-next-and-random-pointer-set-2/)

我们已经讨论了克隆链表的两种不同方法。在[这篇](https://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/)的帖子中，讨论了一个更简单的克隆链表的方法。

想法是使用哈希。下面是算法。

1.  遍历原始链表，根据数据进行复制。
2.  制作一个键值对与原始链表节点和复制链表节点的哈希映射。
3.  再次遍历原始链表，并使用哈希映射调整克隆链表节点的下一个随机引用。

下面是上述方法的实现。

## java 描述语言

```
<script>
// JavaScript program to clone a linked 
// list with random pointers

// Linked List Node class
class Node
{
    constructor(data)
    {
        this.data = data;
        this.next = this.random = null;
    }
}

class LinkedList
{   
    // Linked list constructor
    constructor(head)    
    {
        this.head = head;
    }

    // Push method to put data always 
    // at the head in the linked list.
    push(data)
    {
        let node = new Node(data);
        node.next = this.head;
        this.head = node;
    }

    // Method to print the list.
    print()
    {
        let temp = this.head;
        while (temp != null)
        {
            let random = temp.random;
            let randomData = ((random != null) ? 
                               random.data : -1);
            document.write("Data = " + temp.data +
                           ", Random data = " + 
                           randomData + "<br>");
            temp = temp.next;
        }
    }

    // Actual clone method which returns head
    // reference of cloned linked list.
    clone()
    {
        // Initialize two references, one with 
        // original list's head.
        let origCurr = this.head, 
            cloneCurr = null;

        // Hash map which contains node to node
        // mapping of original and clone linked list.
        let map = new Map();

        // Traverse the original list and make a 
        // copy of that in the clone linked list.
        while (origCurr != null)
        {
            cloneCurr = new Node(origCurr.data);
            map.set(origCurr, cloneCurr);
            origCurr = origCurr.next;
        }

        // Adjusting the original list reference  
        // again.
        origCurr = this.head;

        // Traversal of original list again to 
        // adjust the next and random references 
        // of clone list using hash map.
        while (origCurr != null)
        {
            cloneCurr = map.get(origCurr);
            cloneCurr.next = map.get(origCurr.next);
            cloneCurr.random = map.get(origCurr.random);
            origCurr = origCurr.next;
        }

        // Return the head reference of the 
        // clone list.
        return new LinkedList(map.get(this.head));
    }
}

// Driver code
// Pushing data in the linked list.
let list = 
new LinkedList(new Node(5));
list.push(4);
list.push(3);
list.push(2);
list.push(1);

// Setting up random references.
list.head.random = 
list.head.next.next;
list.head.next.random =
list.head.next.next.next;
list.head.next.next.random =
list.head.next.next.next.next;
list.head.next.next.next.random =
list.head.next.next.next.next.next;
list.head.next.next.next.next.random =
list.head.next;

// Making a clone of the original 
// linked list.
let clone = list.clone();

// Print the original and cloned 
// linked list.
document.write(
"Original linked list<br>");
list.print();
document.write(
"<br>Cloned linked list<br>");
clone.print();
// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Original linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2

Cloned linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
详情请参考[上的完整文章用 next 和随机指针克隆链表| Set 2](https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/) ！