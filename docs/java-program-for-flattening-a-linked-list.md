# 用于展平链表的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-for-扁平化-a-link-list/](https://www.geeksforgeeks.org/java-program-for-flattening-a-linked-list/)

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for flattening 
// a Linked List
class LinkedList
{
    // Head of list
    Node head;  

    // Linked list Node
    class Node
    {
        int data;
        Node right, down;
        Node(int data)
        {
            this.data = data;
            right = null;
            down = null;
        }
    }

    // An utility function to merge 
    // two sorted linked lists
    Node merge(Node a, Node b)
    {
        // If first linked list is empty 
        // then second is the answer
        if (a == null)     
            return b;

        // If second linked list is empty 
        // then first is the result
        if (b == null)      
            return a;

        // Compare the data members of the 
        // two linked lists and put the 
        // larger one in the result
        Node result;

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

    Node flatten(Node root)
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
        // it will be in turn merged with 
        // its left
        return root;
    }

    /* Utility function to insert a node 
       at beginning of the linked list */
    Node push(Node head_ref, int data)
    {
        /* 1 & 2: Allocate the Node &
                  Put in the data */
        Node new_node = new Node(data);

        // 3\. Make next of new Node as head 
        new_node.down = head_ref;

        // 4\. Move the head to point to 
        // new Node 
        head_ref = new_node;

        // 5\. return to link it back 
        return head_ref;
    }

    void printList()
    {
        Node temp = head;
        while (temp != null)
        {
            System.out.print(temp.data + " ");
            temp = temp.down;
        }
        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        LinkedList L = new LinkedList();

        /* Create the following linked list
            5 -> 10 -> 19 -> 28
            |    |     |     |
            V    V     V     V
            7    20    22    35
            |          |     |
            V          V     V
            8          50    40
            |                |
            V                V
            30               45 */
        L.head = L.push(L.head, 30);
        L.head = L.push(L.head, 8);
        L.head = L.push(L.head, 7);
        L.head = L.push(L.head, 5);

        L.head.right = 
        L.push(L.head.right, 20);
        L.head.right = 
        L.push(L.head.right, 10);

        L.head.right.right = 
        L.push(L.head.right.right, 50);
        L.head.right.right = 
        L.push(L.head.right.right, 22);
        L.head.right.right = 
        L.push(L.head.right.right, 19);

        L.head.right.right.right = 
        L.push(L.head.right.right.right, 45);
        L.head.right.right.right = 
        L.push(L.head.right.right.right, 40);
        L.head.right.right.right = 
        L.push(L.head.right.right.right, 35);
        L.head.right.right.right = 
        L.push(L.head.right.right.right, 20);

        // Flatten the list
        L.head = L.flatten(L.head);

        L.printList();
    }
} 
// This code is contributed by Rajat Mishra 
```

**输出:**

```
5 7 8 10 19 20 20 22 30 35 40 45 50
```

更多详情请参考[整平链表](https://www.geeksforgeeks.org/flattening-a-linked-list/)整篇文章！