# Java 中的静态和动态数据结构以及示例

> 原文：[https://www.geeksforgeeks.org/static-and-dynamic-data-structures-in-java-with-examples/](https://www.geeksforgeeks.org/static-and-dynamic-data-structures-in-java-with-examples/)

[数据结构](https://www.geeksforgeeks.org/data-structures/)是一种有效地存储和组织数据的方式，这样就可以相对于时间和内存有效地执行对它们的所需操作。 简单来说，数据结构用于减少代码的复杂度（主要是时间复杂度）。

数据结构可以有两种类型：

### 静态数据结构

在静态数据结构中，结构的大小是固定的。 可以修改数据结构的内容，但无需更改分配给它的存储空间。

![](img/f135b70319b69f7c8fc3364f232504ba.png)

静态数据结构示例：

1.  ### [数组](https://www.geeksforgeeks.org/arrays-in-java/)

    数组是一个包含固定数量的单一类型值的容器对象。 创建数组时将确定数组的长度。 数组是一组由通用名称引用的相似类型的变量。 Java 中的数组与 C / C++中的数组工作方式不同。

    **语法**：

    ```
    // Declaration
    type var-name[];
    OR
    type[] var-name;

    // Initialization
    var-name = new type [size];

    ```

    **实施**：

    ```

    // Java program to illustrate creating an array 
    // of integers, puts some values in the array, 
    // and prints each value to standard output. 

    class GFG { 
        public static void main(String[] args) 
        { 
            // declares an Array of integers. 
            int[] arr; 

            // allocating memory for 5 integers. 
            arr = new int[5]; 

            // initialize the first 
            // element of the array 
            arr[0] = 10; 

            // initialize the second 
            // element of the array 
            arr[1] = 20; 

            // so on... 
            arr[2] = 30; 
            arr[3] = 40; 
            arr[4] = 50; 

            // accessing the elements 
            // of the specified array 
            for (int i = 0; i < arr.length; i++) 
                System.out.println( 
                    "Element at index "
                    + i + " : " + arr[i]); 
        } 
    } 

    ```

    **Output:**

    ```
    Element at index 0 : 10
    Element at index 1 : 20
    Element at index 2 : 30
    Element at index 3 : 40
    Element at index 4 : 50

    ```

    *上面的数组实现存在问题：*

    创建数组后，我们无法更改数组的大小。 因此，数组的大小是不可更改的。

### 动态数据结构

在动态数据结构中，结构的大小不是固定的，可以在对其执行的操作期间进行修改。 动态数据结构旨在促进运行时数据结构的更改。

![](img/f3277ee37f20568b18a51cd230eb1fa6.png)

动态数据结构示例：

1.  ### [单链表](https://www.geeksforgeeks.org/linked-list-in-java/)

    链表是线性数据结构，其中元素未存储在连续的位置，并且每个元素都是具有数据部分和地址部分的单独对象。 元素使用指针和地址链接。 每个元素称为一个节点。 由于动态性以及插入和删除的简便性，它们比数组更可取。

    ```

    // Java code for Linked List implementation 

    import java.util.*; 

    public class Test { 
        public static void main(String args[]) 
        { 
            // Creating object of class linked list 
            LinkedList<String> object 
                = new LinkedList<String>(); 

            // Adding elements to the linked list 
            object.add("A"); 
            object.add("B"); 
            object.addLast("C"); 
            object.addFirst("D"); 
            object.add(2, "E"); 
            object.add("F"); 
            object.add("G"); 
            System.out.println("Linked list : "
                               + object); 

            // Removing elements from the linked list 
            object.remove("B"); 
            object.remove(3); 
            object.removeFirst(); 
            object.removeLast(); 
            System.out.println( 
                "Linked list after deletion: "
                + object); 

            // Finding elements in the linked list 
            boolean status = object.contains("E"); 

            if (status) 
                System.out.println( 
                    "List contains the element 'E' "); 
            else
                System.out.println( 
                    "List doesn't contain the element 'E'"); 

            // Number of elements in the linked list 
            int size = object.size(); 
            System.out.println( 
                "Size of linked list = " + size); 

            // Get and set elements from linked list 
            Object element = object.get(2); 
            System.out.println( 
                "Element returned by get() : "
                + element); 
            object.set(2, "Y"); 
            System.out.println( 
                "Linked list after change : "
                + object); 
        } 
    } 

    ```

    **Output:**

    ```
    Linked list : [D, A, E, B, C, F, G]
    Linked list after deletion: [A, E, F]
    List contains the element 'E' 
    Size of linked list = 3
    Element returned by get() : F
    Linked list after change : [A, E, Y]

    ```

2.  ### [双链表](https://www.geeksforgeeks.org/doubly-linked-list/)

    双链表（DLL）包含一个额外的指针（通常称为**上一个指针**）以及在单个链表中的**下一个指针**和**数据** 。

    ![](img/1fac4717827a04f080fae80f8fd57fe7.png)

    ```

    // Java program to demonstrate DLL 

    // Class for Doubly Linked List 
    public class DLL { 
        Node head; // head of list 

        /* Doubly Linked list Node*/
        class Node { 
            int data; 
            Node prev; 
            Node next; 

            // Constructor to create a new node 
            // next and prev is by default 
            // initialized as null 
            Node(int d) { data = d; } 
        } 

        // Adding a node at the front of the list 
        public void push(int new_data) 
        { 
            /* 1\. allocate node  
            * 2\. put in the data */
            Node new_Node = new Node(new_data); 

            /* 3\. Make next of new node as head 
            and previous as NULL */
            new_Node.next = head; 
            new_Node.prev = null; 

            /* 4\. change prev of head node to new node */
            if (head != null) 
                head.prev = new_Node; 

            /* 5\. move the head to point to the new node */
            head = new_Node; 
        } 

        /* Given a node as prev_node,  
        insert a new node after the given node */
        public void InsertAfter( 
            Node prev_Node, int new_data) 
        { 

            /*1\. check if the given 
            prev_node is NULL */
            if (prev_Node == null) { 
                System.out.println( 
                    "The given previous node"
                    + " cannot be NULL "); 
                return; 
            } 

            /* 2\. allocate node  
            * 3\. put in the data */
            Node new_node = new Node(new_data); 

            /* 4\. Make next of new node  
            as next of prev_node */
            new_node.next = prev_Node.next; 

            /* 5\. Make the next of 
            prev_node as new_node */
            prev_Node.next = new_node; 

            /* 6\. Make prev_node as 
            previous of new_node */
            new_node.prev = prev_Node; 

            /* 7\. Change previous of  
            new_node's next node */
            if (new_node.next != null) 
                new_node.next.prev = new_node; 
        } 

        // Add a node at the end of the list 
        void append(int new_data) 
        { 
            /* 1\. allocate node  
            * 2\. put in the data */
            Node new_node = new Node(new_data); 

            Node last = head; /* used in step 5*/

            /* 3\. This new node is going 
            to be the last node, so  
            * make next of it as NULL*/
            new_node.next = null; 

            /* 4\. If the Linked List is empty, 
            * then make the new  
            * node as head */
            if (head == null) { 
                new_node.prev = null; 
                head = new_node; 
                return; 
            } 

            /* 5\. Else traverse till 
            the last node */
            while (last.next != null) 
                last = last.next; 

            /* 6\. Change the next of last node */
            last.next = new_node; 

            /* 7\. Make last node as 
            previous of new node */
            new_node.prev = last; 
        } 

        // This function prints contents 
        // of linked list starting 
        // from the given node 
        public void printlist(Node node) 
        { 
            Node last = null; 
            System.out.println( 
                "Traversal in forward Direction"); 
            while (node != null) { 
                System.out.print(node.data + " "); 
                last = node; 
                node = node.next; 
            } 
            System.out.println(); 
            System.out.println( 
                "Traversal in reverse direction"); 
            while (last != null) { 
                System.out.print(last.data + " "); 
                last = last.prev; 
            } 
        } 

        /* Driver program to test above functions*/
        public static void main(String[] args) 
        { 
            /* Start with the empty list */
            DLL dll = new DLL(); 

            // Insert 6\. So linked list becomes 6->NULL 
            dll.append(6); 

            // Insert 7 at the beginning. 
            // So linked list becomes 7->6->NULL 
            dll.push(7); 

            // Insert 1 at the beginning. 
            // So linked list becomes 1->7->6->NULL 
            dll.push(1); 

            // Insert 4 at the end. 
            // So linked list becomes 
            // 1->7->6->4->NULL 
            dll.append(4); 

            // Insert 8, after 7\. 
            // So linked list becomes 
            // 1->7->8->6->4->NULL 
            dll.InsertAfter(dll.head.next, 8); 

            System.out.println("Created DLL is: "); 
            dll.printlist(dll.head); 
        } 
    } 

    ```

    **Output:**

    ```
    Created DLL is: 
    Traversal in forward Direction
    1 7 8 6 4 
    Traversal in reverse direction
    4 6 8 7 1

    ```

3.  ### [矢量](https://www.geeksforgeeks.org/java-util-vector-class-java/)

    Vector 类实现可增长的对象数组。 向量基本上属于传统类，但现在与集合完全兼容。 Vector 实现了动态数组，这意味着它可以根据需要增长或收缩。 像数组一样，它包含可以使用整数索引访问的组件。

    ```

    // Java code illustrating Vector data structure 

    import java.util.*; 

    class Vector_demo { 
        public static void main(String[] arg) 
        { 

            // Create default vector 
            Vector v = new Vector(); 

            v.add(1); 
            v.add(2); 
            v.add("geeks"); 
            v.add("forGeeks"); 
            v.add(3); 

            System.out.println("Vector is " + v); 
        } 
    } 

    ```

    **输出**：

    ```
    Vector is [1, 2, geeks, forGeeks, 3]

    ```

4.  ### [堆栈](https://www.geeksforgeeks.org/stack-class-in-java/)

    Java Collection 框架提供了一个 Stack 类，该类可以建模和实现 Stack 数据结构。 该课程基于后进先出的基本原则。 除了基本的推入和弹出操作外，该类还提供了空，搜索和查看的三个功能。 也可以说该类是 Vector 的扩展，并将其视为具有五个提到的函数的堆栈。 该类也可以称为 Vector 的子类。

    ![](img/65e1db85d6cbd7231fe141e47968bdc0.png)

    ```

    // Java code for stack implementation 

    import java.io.*; 
    import java.util.*; 

    public class stack_implementation { 
        public static void main(String a[]) 
        { 
            Stack<Integer> stack = new Stack<>(); 
            stack.push(1); 
            stack.push(2); 
            stack.push(3); 
            stack.push(4); 

            int n = stack.size(); 

            for (int i = 0; i < n; i++) { 
                System.out.println(stack.pop()); 
            } 
        } 
    } 

    ```

    **Output:**

    ```
    4
    3
    2
    1

    ```

    **相关文章**：

    *   [使用数组](https://www.geeksforgeeks.org/stack-data-structure-introduction-program/)的堆栈实现

    *   [使用单链表](https://www.geeksforgeeks.org/implement-a-stack-using-singly-linked-list/)的堆栈实现

    *   [使用队列](https://www.geeksforgeeks.org/implement-stack-using-queue/)的堆栈实现

5.  ### [队列](https://www.geeksforgeeks.org/queue-interface-java/)

    Queue 接口在 java.util 包中可用，并且扩展了 Collection 接口。 队列集合用于保存要处理的元素，并提供各种操作，如插入，删除等。它是对象的有序列表，其使用仅限于在列表的末尾插入元素并从头开始删除元素 列表，即遵循先进先出或先进先出的原则。

    ![](img/c42036f3f74cce8827236640b7f21a49.png)

    ```

    // Java orogram to demonstrate working 
    // of Queue interface in Java 

    import java.util.LinkedList; 
    import java.util.Queue; 

    public class QueueExample { 
        public static void main(String[] args) 
        { 
            Queue<Integer> q = new LinkedList<>(); 

            // Adds elements {0, 1, 2, 3, 4} to queue 
            for (int i = 0; i < 5; i++) 
                q.add(i); 

            // Display contents of the queue. 
            System.out.println("Elements of queue-" + q); 

            // To remove the head of queue. 
            int removedele = q.remove(); 
            System.out.println("removed element-"
                               + removedele); 

            System.out.println(q); 

            // To view the head of queue 
            int head = q.peek(); 
            System.out.println("head of queue-"
                               + head); 

            // Rest all methods of collection interface, 
            // Like size and contains can be 
            // used with this implementation. 
            int size = q.size(); 
            System.out.println("Size of queue-"
                               + size); 
        } 
    } 

    ```

    **Output:**

    ```
    Elements of queue-[0, 1, 2, 3, 4]
    removed element-0
    [1, 2, 3, 4]
    head of queue-1
    Size of queue-4

    ```

    **相关文章**：

    *   [使用数组](https://www.geeksforgeeks.org/array-implementation-of-queue-simple/)的队列实现

    *   [使用单链表](https://www.geeksforgeeks.org/queue-linked-list-implementation/)的队列实现

    *   [使用堆栈](https://www.geeksforgeeks.org/queue-using-stacks/)的队列实现

6.  ### 树

    树是一种将值存储在称为**节点**的实体内部的数据结构。 节点通过称为**边缘**的线连接。 每个节点在其中存储一个值。

    **术语**：

    *   **根**是树的最高节点。

    *   **父级**是一个已附加一个或多个节点的节点。

    *   **边缘**是连接两个节点的链接。

    *   **子级**是具有父节点的节点

    *   **叶子**是一个未附加任何子节点的节点，它是树的最底节点。

    ```

    // Java program for different tree traversals 

    /* Class containing left and right child of current  
    node and key value*/
    class Node { 
        int key; 
        Node left, right; 

        public Node(int item) 
        { 
            key = item; 
            left = right = null; 
        } 
    } 

    class BinaryTree { 
        // Root of Binary Tree 
        Node root; 

        BinaryTree() 
        { 
            root = null; 
        } 

        /* Given a binary tree, print 
        its nodes according to the  
        "bottom-up" postorder traversal. */
        void printPostorder(Node node) 
        { 
            if (node == null) 
                return; 

            // first recur on left subtree 
            printPostorder(node.left); 

            // then recur on right subtree 
            printPostorder(node.right); 

            // now deal with the node 
            System.out.print(node.key + " "); 
        } 

        /* Given a binary tree,  
        print its nodes in inorder*/
        void printInorder(Node node) 
        { 
            if (node == null) 
                return; 

            /* first recur on left child */
            printInorder(node.left); 

            /* then print the data of node */
            System.out.print(node.key + " "); 

            /* now recur on right child */
            printInorder(node.right); 
        } 

        /* Given a binary tree, 
        print its nodes in preorder*/
        void printPreorder(Node node) 
        { 
            if (node == null) 
                return; 

            /* first print data of node */
            System.out.print(node.key + " "); 

            /* then recur on left sutree */
            printPreorder(node.left); 

            /* now recur on right subtree */
            printPreorder(node.right); 
        } 

        // Wrappers over above recursive functions 
        void printPostorder() { printPostorder(root); } 
        void printInorder() { printInorder(root); } 
        void printPreorder() { printPreorder(root); } 

        // Driver method 
        public static void main(String[] args) 
        { 
            BinaryTree tree = new BinaryTree(); 
            tree.root = new Node(1); 
            tree.root.left = new Node(2); 
            tree.root.right = new Node(3); 
            tree.root.left.left = new Node(4); 
            tree.root.left.right = new Node(5); 

            System.out.println( 
                "Preorder traversal of binary tree is "); 
            tree.printPreorder(); 

            System.out.println( 
                "\nInorder traversal of binary tree is "); 
            tree.printInorder(); 

            System.out.println( 
                "\nPostorder traversal of binary tree is "); 
            tree.printPostorder(); 
        } 
    } 

    ```

    **Output:**

    ```
    Preorder traversal of binary tree is
    1 2 4 5 3 
    Inorder traversal of binary tree is
    4 2 5 1 3 
    Postorder traversal of binary tree is
    4 5 2 3 1

    ```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。