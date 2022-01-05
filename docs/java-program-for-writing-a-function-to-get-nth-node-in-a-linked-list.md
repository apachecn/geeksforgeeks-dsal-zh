# 编写函数获取链表中第 n 个节点的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-写程序-函数-获取-链表中的第 n 个节点/](https://www.geeksforgeeks.org/java-program-for-writing-a-function-to-get-nth-node-in-a-linked-list/)

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
     a. If count is equal to the passed index then return current
         node
     b. Increment count
     c. change current to point to next of the current.
```

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th node 
// in linked list
class Node
{
    int data;
    Node next;
    Node(int d)
    {
        data = d;
        next = null;
    }
}

class LinkedList 
{
    // Head of list
    Node head; 

    // Takes index as argument and 
    // return data at index
    public int GetNth(int index)
    {
        Node current = head;

        // Index of Node we are
        // currently looking at
        int count = 0; 
        while (current != null)
        {
            if (count == index)
                return current.data;
            count++;
            current = current.next;
        }

        /* If we get to this line, the caller 
           was asking for a non-existent element 
           so we assert fail */
        assert (false);
        return 0;
    }

    /* Given a reference to the head of a list 
       and an int, inserts a new Node on the 
       front of the list. */
    public void push(int new_data)
    {
        // 1\. Alloc the Node and put data
        Node new_Node = new Node(new_data);

        // 2\. Make next of new Node as head 
        new_Node.next = head;

        // 3\. Move the head to point to new Node
        head = new_Node;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with empty list
        LinkedList llist = new LinkedList();

        // Use push() to construct list
        // 1->12->1->4->1 
        llist.push(1);
        llist.push(4);
        llist.push(1);
        llist.push(12);
        llist.push(1);

        // Check the count function 
        System.out.println("Element at index 3 is " + 
                            llist.GetNth(3));
    }
}
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
    return getnth(node->next,n-1)
```

**实施:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n'th node 
// in linked list using recursion
class GFG 
{
    // Link list node 
    static class Node 
    {
        int data;
        Node next;
        Node(int data) 
        { 
           this.data = data; 
        }
    }

    /* Given a reference (pointer to pointer) 
       to the head of a list and an int, push 
       a new node on the front of the list. */
    static Node push(Node head, int new_data)
    {
        // Allocate node 
        Node new_node = new Node(new_data);

        // Put in the data 
        new_node.data = new_data;

        new_node.next = head;
        head = new_node;
        return head;
    }

    /* Takes head pointer of the linked list 
       and index as arguments and return data 
       at index*/
    static int GetNth(Node head, int n)
    {
        int count = 0;

        // Edge case - if head is null
        if (head == null) 
            return -1;

        // If count equal too n return 
        // node.data
        if (count == n)
            return head.data;

        // Recursively decrease n and 
        // increase head to next pointer
        return GetNth(head.next, n - 1);
    }

    // Driver code
    public static void main(String args[])
    {
        // Start with the empty list
        Node head = null;

        // Use push() to construct list
        // 1.12.1.4.1 
        head = push(head, 1);
        head = push(head, 4);
        head = push(head, 1);
        head = push(head, 12);
        head = push(head, 1);

        // Check the count function 
        System.out.printf("Element at index 3 is %d",
                           GetNth(head, 3));
    }
}
// This code is contributed by Arnab Kundu
```

**输出:**

```
Element at index 3 is 4
```

**时间复杂度:** O(n)

详情请参考[写函数获取链表](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)中第 n 个节点的完整文章！