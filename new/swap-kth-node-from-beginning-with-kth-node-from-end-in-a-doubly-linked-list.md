# 在双向链表中交换距离开头的第`K`个节点和距离末尾的第`K`个节点

> 原文：[https://www.geeksforgeeks.org/swap-kth-node-from-beginning-with-kth-node-from-end-in-a-doubly-linked-list/](https://www.geeksforgeeks.org/swap-kth-node-from-beginning-with-kth-node-from-end-in-a-doubly-linked-list/)



先决条件：[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)

给定[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)，任务是距离开头的第`K`个节点和距离末尾的第`K`个节点。

**注意**：请注意，此处交换了节点，而不交换了节点中的数据。

**示例**：

> **输入**：`DLL = 1 <-> 2 <-> 3 <-> 4 <-> 5 <-> 6, K = 3`
> **输出**：`1 2 4 3 5 6`
> **说明**：
> 距离开头的第三个节点（3）与距离末尾的第三个节点（4）。
> 
> **输入**：`DLL = 1 <-> 2 <-> 3 <-> 4 <-> 5, K = 1`
> **输出**：`5 2 3 4 1`

**方法**：想法是遍历距离开头的和距离结尾的第`K`个元素，并更改上一个和下一个指针。 假设`K1`为从头开始的第`K`个节点，`K2`为距离结束的第`K`个节点。 然后：

*   `K2`的先前节点必须更改为`K1`的先前节点。

*   `K2`的下一个节点必须更改为`K1`的下一个节点。

*   `K1`的先前节点必须更改为`K2`的先前节点。

*   `K1`的下一个节点必须更改为`K2`的下一个节点。

下面是上述方法的实现：

## Java

```java

// Java implementation of the approach 

public class GFG { 

    // Doubly Linked List implementation 
    private class Node { 
        private int data; 
        private Node next; 
        private Node previous; 

        public Node(int data, Node next, 
                    Node previous) 
        { 
            this.data = data; 
            this.next = next; 
            this.previous = previous; 
        } 

        public int getData() 
        { 
            return data; 
        } 

        public void setData(int data) 
        { 
            this.data = data; 
        } 

        public Node getNext() 
        { 
            return next; 
        } 

        public void setNext(Node next) 
        { 
            this.next = next; 
        } 

        public Node getPrevious() 
        { 
            return previous; 
        } 

        public void setPrevious(Node previous) 
        { 
            this.previous = previous; 
        } 
    } 

    private Node head; 
    private Node tail; 

    public GFG() 
    { 
        this.head = null; 
        this.tail = null; 
    } 

    public Node getHead() 
    { 
        return head; 
    } 

    public void setHead(Node head) 
    { 
        this.head = head; 
    } 

    public Node getTail() 
    { 
        return tail; 
    } 

    public void setTail(Node tail) 
    { 
        this.tail = tail; 
    } 

    // Function to replace Kth node from 
    // beginning with Kth node from end 
    public void swapNode(Node headReference, 
                         Node tailReference, int k) 
    { 

        // If K is 1, then the first node 
        // has to be swapped with the 
        // last node in the doubly linked list 
        if (k == 1) { 
            swapFirstAndLast(headReference, 
                             tailReference); 
            return; 
        } 

        // If k is N, then the last node 
        // has to be swapped with the 
        // first node in the doubly linked list 
        int nodeCount = getCount(headReference); 
        if (k == nodeCount) { 
            swapFirstAndLast(headReference, 
                             tailReference); 
            return; 
        } 

        // If the K<sup>th</sup> node from 
        // the beginning and K<sup>th</sup> node 
        // from the ending are same 
        if (2 * k - 1 == nodeCount) { 
            return; 
        } 

        // fNode represents K<sup>th</sup> node 
        // from the beginning 
        Node fNode = headReference; 
        for (int i = 1; i < k; i++) { 
            fNode = fNode.getNext(); 
        } 
        Node fNodePrevious = fNode.getPrevious(); 
        Node fNodeNext = fNode.getNext(); 

        // sNode represents K<sup>th</sup> node 
        // from the ending 
        Node sNode = tailReference; 
        for (int i = 1; i < k; i++) { 
            sNode = sNode.getPrevious(); 
        } 

        Node sNodePrevious = sNode.getPrevious(); 
        Node sNodeNext = sNode.getNext(); 

        // Checking if any of the pointers is null 
        // and interchanging the pointers 
        if (fNodePrevious != null && sNode != null) { 

            fNodePrevious.setNext(sNode); 
            sNode.setPrevious(fNodePrevious); 
            sNode.setNext(fNodeNext); 
            fNodeNext.setPrevious(sNode); 
        } 
        if (sNodePrevious != null && sNodeNext != null) { 

            sNodeNext.setPrevious(fNode); 
            fNode.setNext(sNodeNext); 
            sNodePrevious.setNext(fNode); 
            fNode.setPrevious(sNodePrevious); 
        } 
    } 

    // Function to swap the first and 
    // last node in the doubly linked list 
    private void swapFirstAndLast( 
        Node headReference, 
        Node tailReference) 
    { 
        Node headRef = headReference; 
        Node tailRef = tailReference; 

        headReference 
            = headReference.getNext(); 
        tailReference 
            = tailReference.getPrevious(); 

        tailReference.setNext(headRef); 
        headRef.setPrevious(tailReference); 
        headRef.setNext(null); 
        this.setTail(tailReference.getNext()); 

        headReference.setPrevious(tailRef); 
        tailRef.setNext(headReference); 
        tailRef.setPrevious(null); 
        this.setHead(headReference 
                         .getPrevious()); 
    } 

    // Function to return the number of nodes 
    // in the linked list 
    private int getCount(Node headReference) 
    { 
        int nodeCount = 0; 
        while (headReference != null) { 
            nodeCount++; 
            headReference = headReference 
                                .getNext(); 
        } 
        return nodeCount; 
    } 

    // Function to print the Linked List 
    public void printList(Node headReference) 
    { 
        if (headReference == null) { 
            System.out.println( 
                "Doubly linked list is empty"); 
            return; 
        } 
        else { 
            while (headReference != null) { 
                System.out.print( 
                    headReference.getData() 
                    + " "); 
                headReference 
                    = headReference.getNext(); 
            } 
        } 
    } 

    // Function to insert a node at 
    // the end of the doubly linked list 
    public void push(int data) 
    { 
        Node newNode 
            = new Node(data, null, null); 

        if (head == null) { 
            head = tail = newNode; 
        } 
        else { 
            tail.setNext(newNode); 
            newNode.setPrevious(tail); 
            tail = newNode; 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        // Creating an object for the class 
        GFG list = new GFG(); 

        // Adding data to the linked list 
        list.push(1); 
        list.push(2); 
        list.push(3); 
        list.push(4); 
        list.push(5); 

        // Calling the function 
        int K = 2; 
        list.swapNode(list.getHead(), 
                      list.getTail(), K); 
        list.printList(list.getHead()); 
    } 
} 

```

## C#

```cs

// C# implementation of the approach 
using System; 
public class GFG { 

    // Doubly Linked List implementation 
    private class Node { 
        private int data; 
        private Node next; 
        private Node previous; 

        public Node(int data, Node next, 
                    Node previous) 
        { 
            this.data = data; 
            this.next = next; 
            this.previous = previous; 
        } 

        public int getData() 
        { 
            return data; 
        } 

        public void setData(int data) 
        { 
            this.data = data; 
        } 

        public Node getNext() 
        { 
            return next; 
        } 

        public void setNext(Node next) 
        { 
            this.next = next; 
        } 

        public Node getPrevious() 
        { 
            return previous; 
        } 

        public void setPrevious(Node previous) 
        { 
            this.previous = previous; 
        } 
    } 

    private Node head; 
    private Node tail; 

    public GFG() 
    { 
        this.head = null; 
        this.tail = null; 
    } 

    Node getHead() 
    { 
        return head; 
    } 

    void setHead(Node head) 
    { 
        this.head = head; 
    } 

    Node getTail() 
    { 
        return tail; 
    } 

    void setTail(Node tail) 
    { 
        this.tail = tail; 
    } 

    // Function to replace Kth node from 
    // beginning with Kth node from end 
    void swapNode(Node headReference, 
                         Node tailReference, int k) 
    { 

        // If K is 1, then the first node 
        // has to be swapped with the 
        // last node in the doubly linked list 
        if (k == 1) { 
            swapFirstAndLast(headReference, 
                             tailReference); 
            return; 
        } 

        // If k is N, then the last node 
        // has to be swapped with the 
        // first node in the doubly linked list 
        int nodeCount = getCount(headReference); 
        if (k == nodeCount) { 
            swapFirstAndLast(headReference, 
                             tailReference); 
            return; 
        } 

        // If the K<sup>th</sup> node from 
        // the beginning and K<sup>th</sup> node 
        // from the ending are same 
        if (2 * k - 1 == nodeCount) { 
            return; 
        } 

        // fNode represents K<sup>th</sup> node 
        // from the beginning 
        Node fNode = headReference; 
        for (int i = 1; i < k; i++) { 
            fNode = fNode.getNext(); 
        } 
        Node fNodePrevious = fNode.getPrevious(); 
        Node fNodeNext = fNode.getNext(); 

        // sNode represents K<sup>th</sup> node 
        // from the ending 
        Node sNode = tailReference; 
        for (int i = 1; i < k; i++) { 
            sNode = sNode.getPrevious(); 
        } 

        Node sNodePrevious = sNode.getPrevious(); 
        Node sNodeNext = sNode.getNext(); 

        // Checking if any of the pointers is null 
        // and interchanging the pointers 
        if (fNodePrevious != null && sNode != null) { 

            fNodePrevious.setNext(sNode); 
            sNode.setPrevious(fNodePrevious); 
            sNode.setNext(fNodeNext); 
            fNodeNext.setPrevious(sNode); 
        } 
        if (sNodePrevious != null && sNodeNext != null) { 

            sNodeNext.setPrevious(fNode); 
            fNode.setNext(sNodeNext); 
            sNodePrevious.setNext(fNode); 
            fNode.setPrevious(sNodePrevious); 
        } 
    } 

    // Function to swap the first and 
    // last node in the doubly linked list 
    private void swapFirstAndLast( 
        Node headReference, 
        Node tailReference) 
    { 
        Node headRef = headReference; 
        Node tailRef = tailReference; 

        headReference 
            = headReference.getNext(); 
        tailReference 
            = tailReference.getPrevious(); 

        tailReference.setNext(headRef); 
        headRef.setPrevious(tailReference); 
        headRef.setNext(null); 
        this.setTail(tailReference.getNext()); 

        headReference.setPrevious(tailRef); 
        tailRef.setNext(headReference); 
        tailRef.setPrevious(null); 
        this.setHead(headReference 
                         .getPrevious()); 
    } 

    // Function to return the number of nodes 
    // in the linked list 
    private int getCount(Node headReference) 
    { 
        int nodeCount = 0; 
        while (headReference != null) { 
            nodeCount++; 
            headReference = headReference 
                                .getNext(); 
        } 
        return nodeCount; 
    } 

    // Function to print the Linked List 
    void printList(Node headReference) 
    { 
        if (headReference == null) { 
            Console.WriteLine( 
                "Doubly linked list is empty"); 
            return; 
        } 
        else { 
            while (headReference != null) { 
                Console.Write( 
                    headReference.getData() 
                    + " "); 
                headReference 
                    = headReference.getNext(); 
            } 
        } 
    } 

    // Function to insert a node at 
    // the end of the doubly linked list 
    void Push(int data) 
    { 
        Node newNode 
            = new Node(data, null, null); 

        if (head == null) { 
            head = tail = newNode; 
        } 
        else { 
            tail.setNext(newNode); 
            newNode.setPrevious(tail); 
            tail = newNode; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        // Creating an object for the class 
        GFG list = new GFG(); 

        // Adding data to the linked list 
        list.Push(1); 
        list.Push(2); 
        list.Push(3); 
        list.Push(4); 
        list.Push(5);       

        // Calling the function 
        int K = 2; 
        list.swapNode(list.getHead(), 
                      list.getTail(), K); 
        list.printList(list.getHead()); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
1 4 3 2 5

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。