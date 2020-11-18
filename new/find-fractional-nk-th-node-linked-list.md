# 在链表

中找到小数（或 n / k – th）节点

给定一个单链列表和一个数字 k，编写一个函数以查找第（n / k）个元素，其中 n 是列表中元素的数量。 在小数的情况下，我们需要考虑 ceil 值。

**示例：**

```
Input : list = 1->2->3->4->5->6 
        k = 2
Output : 3
Since n = 6 and k = 2, we print (6/2)-th node 
which is 3.

Input : list = 2->7->9->3->5
        k = 3
Output : 7 
Since n is 5 and k is 3, we print ceil(5/3)-th 
node which is 2nd node, i.e., 7.

```

1.  取两个指针 temp 和 fractionalNode 并分别用 null 和 head 初始化它们。
2.  对于临时指针的每 k 次跳转，对 fractionalNode 指针进行一次跳转。

## C++

```cpp

// C++ program to find fractional node in a linked list 
#include <bits/stdc++.h> 

/* Linked list node */
struct Node { 
    int data; 
    Node* next; 
}; 

/* Function to create a new node with given data */
Node* newNode(int data) 
{ 
    Node* new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

/* Function to find fractional node in the linked list */
Node* fractionalNodes(Node* head, int k) 
{ 
    // Corner cases 
    if (k <= 0 || head == NULL) 
        return NULL; 

    Node* fractionalNode = NULL; 

    // Traverse the given list  
    int i = 0; 
    for (Node* temp = head; temp != NULL; temp = temp->next) { 

        // For every k nodes, we move fractionalNode one 
        // step ahead.  
        if (i % k == 0) { 

            // First time we see a multiple of k 
            if (fractionalNode == NULL) 
                fractionalNode = head; 

            else
                fractionalNode = fractionalNode->next; 
        } 
        i++; 
    } 
    return fractionalNode; 
} 

// A utility function to print a linked list 
void printList(Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
    printf("\n"); 
} 

/* Driver program to test above function */
int main(void) 
{ 
    Node* head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 
    int k = 2; 

    printf("List is "); 
    printList(head); 

    Node* answer = fractionalNodes(head, k); 
    printf("\nFractional node is "); 
    printf("%d\n", answer->data); 

    return 0; 
} 

```

## Java

```java

// Java program to find fractional node in 
// a linked list 
public class FractionalNodell 
{ 
    /* Linked list node */
    static class Node{ 
        int data; 
        Node next; 

        //Constructor 
        Node (int data){ 
            this.data = data; 
        } 
    } 

    /* Function to find fractional node in the 
       linked list */
    static Node fractionalNodes(Node head, int k) 
    { 
        // Corner cases 
        if (k <= 0 || head == null) 
            return null; 

        Node fractionalNode = null; 

        // Traverse the given list 
        int i = 0; 
        for (Node temp = head; temp != null; 
                          temp = temp.next){ 

            // For every k nodes, we move 
            // fractionalNode one step ahead. 
            if (i % k == 0){ 

                // First time we see a multiple of k 
                if (fractionalNode == null) 
                    fractionalNode = head; 
                else
                    fractionalNode = fractionalNode.next; 
            } 
            i++; 
        } 
        return fractionalNode; 
    } 

    // A utility function to print a linked list 
    static void printList(Node node) 
    { 
        while (node != null) 
        { 
            System.out.print(node.data+" "); 
            node = node.next; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above function */
    public static void main(String[] args) { 
        Node head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(3); 
        head.next.next.next = new Node(4); 
        head.next.next.next.next = new Node(5); 
        int k =2; 

        System.out.print("List is "); 
        printList(head); 

        Node answer = fractionalNodes(head, k); 
        System.out.println("Fractional node is "+ 
                                      answer.data); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

# Python3 program to find fractional node 
# in a linked list 
import math 

# Linked list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to create a new node  
# with given data 
def newNode(data): 
    new_node = Node(data) 
    new_node.data = data 
    new_node.next = None
    return new_node 

# Function to find fractional node  
# in the linked list 
def fractionalNodes(head, k): 

    # Corner cases 
    if (k <= 0 or head == None): 
        return None

    fractionalNode = None

    # Traverse the given list 
    i = 0
    temp = head 
    while (temp != None): 

        # For every k nodes, we move  
        # fractionalNode one step ahead.  
        if (i % k == 0): 

            # First time we see a multiple of k 
            if (fractionalNode == None): 
                fractionalNode = head 

            else: 
                fractionalNode = fractionalNode.next

        i = i + 1
        temp = temp.next

    return fractionalNode 

# A utility function to print a linked list 
def prList(node): 
    while (node != None): 
        print(node.data, end = ' ') 
        node = node.next

# Driver Code 
if __name__ == '__main__': 
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(3) 
    head.next.next.next = newNode(4) 
    head.next.next.next.next = newNode(5) 
    k = 2

    print("List is", end = ' ') 
    prList(head) 

    answer = fractionalNodes(head, k) 
    print("\nFractional node is", end = ' ') 
    print(answer.data) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to find fractional node in 
// a linked list 
using System; 

public class FractionalNodell 
{ 
    /* Linked list node */
    public class Node 
    { 
        public int data; 
        public Node next; 

        //Constructor 
        public Node (int data) 
        { 
            this.data = data; 
        } 
    } 

    /* Function to find fractional node in the 
    linked list */
    static Node fractionalNodes(Node head, int k) 
    { 
        // Corner cases 
        if (k <= 0 || head == null) 
            return null; 

        Node fractionalNode = null; 

        // Traverse the given list 
        int i = 0; 
        for (Node temp = head; temp != null; 
                        temp = temp.next) 
        { 

            // For every k nodes, we move 
            // fractionalNode one step ahead. 
            if (i % k == 0) 
            { 

                // First time we see a multiple of k 
                if (fractionalNode == null) 
                    fractionalNode = head; 
                else
                    fractionalNode = fractionalNode.next; 
            } 
            i++; 
        } 
        return fractionalNode; 
    } 

    // A utility function to print a linked list 
    static void printList(Node node) 
    { 
        while (node != null) 
        { 
            Console.Write(node.data+" "); 
            node = node.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main(String[] args)  
    { 
        Node head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(3); 
        head.next.next.next = new Node(4); 
        head.next.next.next.next = new Node(5); 
        int k =2; 

        Console.Write("List is "); 
        printList(head); 

        Node answer = fractionalNodes(head, k); 
        Console.WriteLine("Fractional node is "+ 
                                    answer.data); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```

List is 1 2 3 4 5 
Fractional node is 3

```

本文由 **Prakriti Gupta** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

