# 用于查找链表长度的 Java 程序

> 原文:[https://www . geeksforgeeks . org/Java-寻找链表长度的程序-迭代和递归方法/](https://www.geeksforgeeks.org/java-program-for-finding-length-of-a-linked-list-iterative-and-recursive-approach/)

编写一个函数来计算给定单链表中的节点数。

![linkedlist_find_length](img/e38a7cce1aae90394ef3ebc5cd8323c1.png)

例如，对于链表 1->3->1->2->1，函数应该返回 5。

**迭代解:**

```
1) Initialize count as 0 
2) Initialize a node pointer, current = head.
3) Do following while current is not NULL
     a) current = current -> next
     b) count++;
4) Return count 
```

下面是上述算法的迭代实现，用于查找给定单链表中的节点数。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of 
// nodes in a linked list

// Linked list Node
class Node
{
    int data;
    Node next;
    Node(int d)  { data = d;  next = null; }
}

// Linked List class
class LinkedList
{
    // Head of list
    Node head;  

    // Inserts a new Node at front 
    // of the list.
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point to new Node 
        head = new_node;
    }

    // Returns count of nodes in linked list
    public int getCount()
    {
        Node temp = head;
        int count = 0;
        while (temp != null)
        {
            count++;
            temp = temp.next;
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with the empty list 
        LinkedList llist = new LinkedList();
        llist.push(1);
        llist.push(3);
        llist.push(1);
        llist.push(2);
        llist.push(1);

        System.out.println("Count of nodes is " +
                            llist.getCount());
    }
}
```

**输出:**

```
count of nodes is 5
```

**递归解:**

```
int getCount(head)
1) If head is NULL, return 0.
2) Else return 1 + getCount(head->next) 
```

下面是上述算法的递归实现，用于查找给定单链表中的节点数。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to count number 
// of nodes in a linked list

// Linked list Node
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

// Linked List class
class LinkedList
{

    Node head;  

    // Inserts a new Node at front of
    // the list. 
    public void push(int new_data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data*/
        Node new_node = new Node(new_data);

        // 3\. Make next of new Node as head 
        new_node.next = head;

        // 4\. Move the head to point to new Node
        head = new_node;
    }

    // Returns count of nodes in linked list
    public int getCountRec(Node node)
    {
        // Base case
        if (node == null)
            return 0;

        // Count is this node plus rest 
        // of the list
        return 1 + getCountRec(node.next);
    }

    // Wrapper over getCountRec() 
    public int getCount()
    {
        return getCountRec(head);
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with the empty list
        LinkedList llist = new LinkedList();
        llist.push(1);
        llist.push(3);
        llist.push(1);
        llist.push(2);
        llist.push(1);

        System.out.println("Count of nodes is " +
                            llist.getCount());
    }
}
```

**输出:**

```
Count of nodes is 5
```

详情请参考[求链表长度(迭代和递归)](https://www.geeksforgeeks.org/find-length-of-a-linked-list-iterative-and-recursive/)整篇文章！