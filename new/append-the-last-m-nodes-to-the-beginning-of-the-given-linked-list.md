# 将最后 M 个节点追加到给定链表

的开头

给定一个链表和一个整数 **M** ，任务是将链表的最后 **M** 个节点附加到最前面。

**示例**：

> **输入**：列表= 4-> 5-> 6-> 1-> 2-> 3-> NULL，M = 3
> **输出**：1-> 2-> 3-> 4-> 5-> 6-> NULL
> 
> **输入**：列表= 8-> 7-> 0-> 4-> 1-> NULL，M = 2
> **输出**：4-> 1-> 8-> 7-> 0->空

**方法**：在列表中找到最后 M 个节点的第一个节点，此节点将是新的头节点，因此将上一个节点的下一个指针设为 NULL，然后将原始列表的最后一个节点指向 原始列表的标题。 最后，打印更新的列表。

下面是上述方法的实现：

## Java

```java

// Java implementation of the approach 
class GFG { 

    // Class for a node of 
    // the linked list 
    static class Node { 

        // Data and the pointer 
        // to the next node 
        int data; 
        Node next; 

        Node(int data) 
        { 
            this.data = data; 
            this.next = null; 
        } 
    } 

    // Function to print the linked list 
    static void printList(Node node) 
    { 
        while (node != null) { 
            System.out.print(node.data + " -> "); 
            node = node.next; 
        } 
        System.out.print("NULL"); 
    } 

    // Recursive function to return the 
    // count of nodes in the linked list 
    static int cntNodes(Node node) 
    { 
        if (node == null) 
            return 0; 

        return (1 + cntNodes(node.next)); 
    } 

    // Function to update and print 
    // the updated list nodes 
    static void updateList(Node head, int m) 
    { 

        // Total nodes in the list 
        int cnt = cntNodes(head); 

        if (cnt != m && m < cnt) { 

            // Count of nodes to be skipped 
            // from the beginning 
            int skip = cnt - m; 
            Node prev = null; 
            Node curr = head; 

            // Skip the nodes 
            while (skip > 0) { 
                prev = curr; 
                curr = curr.next; 
                skip--; 
            } 

            // Change the pointers 
            prev.next = null; 
            Node tempHead = head; 
            head = curr; 

            // Find the last node 
            while (curr.next != null) 
                curr = curr.next; 

            // Connect it to the head 
            // of the sub list 
            curr.next = tempHead; 
        } 

        // Print the updated list 
        printList(head); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        // Create the list 
        Node head = new Node(4); 
        head.next = new Node(5); 
        head.next.next = new Node(6); 
        head.next.next.next = new Node(1); 
        head.next.next.next.next = new Node(2); 
        head.next.next.next.next.next = new Node(3); 

        int m = 3; 

        updateList(head, m); 
    } 
} 

```

## Python3

```py

# Python3 implementation of the approach 

# Class for a node of 
# the linked list 
class newNode:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to print the linked list 
def printList(node): 

    while (node != None): 
        print(node.data,"->", end=" ") 
        node = node.next
    print("NULL") 

# Recursive function to return the 
# count of nodes in the linked list 
def cntNodes(node): 
    if (node == None): 
        return 0

    return (1 + cntNodes(node.next)) 

# Function to update and print 
# the updated list nodes 
def updateList(head, m): 

    # Total nodes in the list 
    cnt = cntNodes(head) 

    if (cnt != m and m < cnt): 

        # Count of nodes to be skipped 
        # from the beginning 
        skip = cnt - m 
        prev = None

        curr = head 

        # Skip the nodes 
        while (skip > 0): 
            prev = curr 
            curr = curr.next
            skip-=1

        # Change the pointers 
        prev.next = None
        tempHead = head 
        head = curr 

        # Find the last node 
        while (curr.next != None): 
            curr = curr.next

        # Connect it to the head 
        # of the sub list 
        curr.next = tempHead 

    # Print the updated list 
    printList(head) 

# Driver code 

# Create the list 
head = newNode(4) 
head.next = newNode(5) 
head.next.next = newNode(6) 
head.next.next.next = newNode(1) 
head.next.next.next.next = newNode(2) 
head.next.next.next.next.next = newNode(3) 

m = 3

updateList(head, m) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

    // Class for a node of 
    // the linked list 
    class Node 
    { 

        // Data and the pointer 
        // to the next node 
        public int data; 
        public Node next; 

        public Node(int data) 
        { 
            this.data = data; 
            this.next = null; 
        } 
    } 

    // Function to print the linked list 
    static void printList(Node node) 
    { 
        while (node != null)  
        { 
            Console.Write(node.data + " -> "); 
            node = node.next; 
        } 
        Console.Write("NULL"); 
    } 

    // Recursive function to return the 
    // count of nodes in the linked list 
    static int cntNodes(Node node) 
    { 
        if (node == null) 
            return 0; 

        return (1 + cntNodes(node.next)); 
    } 

    // Function to update and print 
    // the updated list nodes 
    static void updateList(Node head, int m) 
    { 

        // Total nodes in the list 
        int cnt = cntNodes(head); 

        if (cnt != m && m < cnt) 
        { 

            // Count of nodes to be skipped 
            // from the beginning 
            int skip = cnt - m; 
            Node prev = null; 
            Node curr = head; 

            // Skip the nodes 
            while (skip > 0) 
            { 
                prev = curr; 
                curr = curr.next; 
                skip--; 
            } 

            // Change the pointers 
            prev.next = null; 
            Node tempHead = head; 
            head = curr; 

            // Find the last node 
            while (curr.next != null) 
                curr = curr.next; 

            // Connect it to the head 
            // of the sub list 
            curr.next = tempHead; 
        } 

        // Print the updated list 
        printList(head); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        // Create the list 
        Node head = new Node(4); 
        head.next = new Node(5); 
        head.next.next = new Node(6); 
        head.next.next.next = new Node(1); 
        head.next.next.next.next = new Node(2); 
        head.next.next.next.next.next = new Node(3); 

        int m = 3; 

        updateList(head, m); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。