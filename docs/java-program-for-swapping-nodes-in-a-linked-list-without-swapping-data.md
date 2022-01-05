# 用于交换链表中的节点而不交换数据的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序交换-链表中的节点-不交换-数据/](https://www.geeksforgeeks.org/java-program-for-swapping-nodes-in-a-linked-list-without-swapping-data/)

给定一个链表和其中的两个键，用两个给定的键交换节点。应该通过更改链接来交换节点。当数据包含许多字段时，交换节点的数据在许多情况下可能是昂贵的。

可以假设链表中的所有键都是不同的。

**例:**

```
Input : 10->15->12->13->20->14,  x = 12, y = 20
Output: 10->15->20->13->12->14

Input : 10->15->12->13->20->14,  x = 10, y = 20
Output: 20->15->12->13->10->14

Input : 10->15->12->13->20->14,  x = 12, y = 13
Output: 10->15->13->12->20->14
```

这看起来可能是一个简单的问题，但这是一个有趣的问题，因为它有以下情况需要处理。

1.  x 和 y 可以相邻，也可以不相邻。
2.  x 或 y 都可以是头节点。
3.  x 或 y 可能是最后一个节点。
4.  链接列表中可能不存在 x 和/或 y。

如何编写一个干净的工作代码来处理上述所有可能性。

想法是首先在给定的链表中搜索 x 和 y。如果他们中的任何一个不存在，那么返回。在搜索 x 和 y 时，跟踪当前和以前的指针。首先更改上一个指针的下一个，然后更改当前指针的下一个。

下面是上述方法的实现。

## 爪哇

T0T6】

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 1 2 4 3 5 6 7 
```

**优化:**以上代码可以优化为单次遍历搜索 x 和 y。两个循环用于保持程序简单。

**更简单的方法:**

## 爪哇

```
// Java program to swap two given nodes 
// of a linked list
public class Solution 
{
    // Represent a node of the 
    // singly linked list
    class Node 
    {
        int data;
        Node next;

        public Node(int data)
        {
            this.data = data;
            this.next = null;
        }
    }

    // Represent the head and tail
    // of the singly linked list
    public Node head = null;
    public Node tail = null;

    // addNode() will add a new node 
    // to the list
    public void addNode(int data)
    {
        // Create a new node
        Node newNode = new Node(data);

        // Checks if the list is empty
        if (head == null) 
        {
            // If list is empty, both head and
            // tail will point to new node
            head = newNode;
            tail = newNode;
        }
        else 
        {
            // newNode will be added after tail 
            // such that tail's next will point 
            // to newNode
            tail.next = newNode;
            // newNode will become new tail of 
            // the list
            tail = newNode;
        }
    }

    // swap() will swap the given two nodes
    public void swap(int n1, int n2)
    {
        Node prevNode1 = null, prevNode2 = null,
             node1 = head, node2 = head;

        // Checks if list is empty
        if (head == null) 
        {
            return;
        }

        // If n1 and n2 are equal, then
        // list will remain the same
        if (n1 == n2)
            return;

        // Search for node1
        while (node1 != null && 
               node1.data != n1) 
        {
            prevNode1 = node1;
            node1 = node1.next;
        }

        // Search for node2
        while (node2 != null && 
               node2.data != n2) 
        {
            prevNode2 = node2;
            node2 = node2.next;
        }

        if (node1 != null && 
            node2 != null) 
        {
            // If previous node to node1 is not
            // null then, it will point to node2
            if (prevNode1 != null)
                prevNode1.next = node2;
            else
                head = node2;

            // If previous node to node2 is not 
            // null then, it will point to node1
            if (prevNode2 != null)
                prevNode2.next = node1;
            else
                head = node1;

            // Swaps the next nodes of node1 
            // and node2
            Node temp = node1.next;
            node1.next = node2.next;
            node2.next = temp;
        }
        else 
        {
            System.out.println("Swapping is not possible");
        }
    }

    // display() will display all the
    // nodes present in the list
    public void display()
    {
        // Node current will point to head
        Node current = head;

        if (head == null) 
        {
            System.out.println("List is empty");
            return;
        }
        while (current != null) 
        {
            // Prints each node by incrementing 
            // pointer
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args)
    {
        Solution sList = new Solution();

        // Add nodes to the list
        sList.addNode(1);
        sList.addNode(2);
        sList.addNode(3);
        sList.addNode(4);
        sList.addNode(5);
        sList.addNode(6);
        sList.addNode(7);

        System.out.println("Original list: ");
        sList.display();

        // Swaps the node 2 with node 5
        sList.swap(6, 1);

        System.out.println(
               "List after swapping nodes: ");
        sList.display();
    }
}
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 6 2 3 4 5 1 7 
```

更多详情请参考完整文章[在链表中交换节点不交换数据](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)！