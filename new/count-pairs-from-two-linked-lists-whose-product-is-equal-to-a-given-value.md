# 来自两个链表的计数对，两个链表的乘积等于给定值

> 原文：[https://www.geeksforgeeks.org/count-pairs-from-two-linked-lists-whose-product-is-equal-to-a-given-value/](https://www.geeksforgeeks.org/count-pairs-from-two-linked-lists-whose-product-is-equal-to-a-given-value/)

给定两个链表（可以排序或不排序），它们的大小分别为`n1`和`n2`。 给定值`X`。问题是要计算两个列表中乘积等于给定值`x`的所有对。

**注意**：该对必须具有每个链表中的一个元素。

**示例**：

```
Input : list1 = 3->1->5->7
        list2 = 8->2->5->3
        X = 10
Output : 1
The pair is: (5, 2)

Input : list1 = 4->3->5->7->11->2->1
        list2 = 2->3->4->5->6->8-12
        X = 9   
Output : 1
The pair is: (3, 3)

```

一种简单的方法是使用两个循环从两个链表中选择元素，并检查该对的乘积是否等于给定值 X。 计算所有这样的对并打印结果。

下面是上述方法的实现：

## C++

```cpp

// C++ program to count all pairs from both the 
// linked lists whose product is equal to 
// a given value 

#include <iostream> 
using namespace std; 

/* A Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to insert a node at the 
// beginning of the linked list 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list to the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to count all pairs from both the linked lists 
// whose product is equal to a given value 
int countPairs(struct Node* head1, struct Node* head2, int x) 
{ 
    int count = 0; 

    struct Node *p1, *p2; 

    // Traverse the 1st linked list 
    for (p1 = head1; p1 != NULL; p1 = p1->next) { 
        // for each node of 1st list 
        // Traverse the 2nd list 
        for (p2 = head2; p2 != NULL; p2 = p2->next) { 
            // if sum of pair is equal to 'x' 
            // increment count 
            if ((p1->data * p2->data) == x) 
                count++; 
        } 
    } 

    // required count of pairs 
    return count; 
} 

// Driver Code 
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    // create linked list1 3->1->5->7 
    push(&head1, 7); 
    push(&head1, 5); 
    push(&head1, 1); 
    push(&head1, 3); 

    // create linked list2 8->2->5->3 
    push(&head2, 3); 
    push(&head2, 5); 
    push(&head2, 2); 
    push(&head2, 8); 

    int x = 10; 

    cout << "Count = " << countPairs(head1, head2, x); 

    return 0; 
} 

```

## Java

```java

// Java program to count all pairs from both the 
// linked lists whose product is equal to 
// a given value 

class GFG  
{ 

    /* A Linked list node */
    static class Node  
    { 
        int data; 
        Node next; 
    }; 

    // function to insert a node at the 
    // beginning of the linked list 
    static Node push(Node head_ref, int new_data)  
    { 
        /* allocate node */
        Node new_node = new Node(); 

        /* put in the data */
        new_node.data = new_data; 

        /* link the old list to the new node */
        new_node.next = head_ref; 

        /* move the head to point to the new node */
        head_ref = new_node; 
        return head_ref; 
    } 

    // Function to count all pairs from both the linked lists 
    // whose product is equal to a given value 
    static int countPairs(Node head1, Node head2, int x) 
    { 
        int count = 0; 

        Node p1, p2; 

        // Traverse the 1st linked list 
        for (p1 = head1; p1 != null; p1 = p1.next)  
        { 
            // for each node of 1st list 
            // Traverse the 2nd list 
            for (p2 = head2; p2 != null; p2 = p2.next) 
            { 
                // if sum of pair is equal to 'x' 
                // increment count 
                if ((p1.data * p2.data) == x)  
                { 
                    count++; 
                } 
            } 
        } 

        // required count of pairs 
        return count; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        Node head1 = null; 
        Node head2 = null; 

        // create linked list1 3.1.5.7 
        head1 = push(head1, 7); 
        head1 = push(head1, 5); 
        head1 = push(head1, 1); 
        head1 = push(head1, 3); 

        // create linked list2 8.2.5.3 
        head2 = push(head2, 3); 
        head2 = push(head2, 5); 
        head2 = push(head2, 2); 
        head2 = push(head2, 8); 

        int x = 10; 

        System.out.print("Count = " + countPairs(head1, head2, x)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# program to count all pairs from both the 
// linked lists whose product is equal to 
// a given value 
using System; 

class GFG  
{ 

    /* A Linked list node */
    class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    // function to insert a node at the 
    // beginning of the linked list 
    static Node push(Node head_ref, int new_data)  
    { 
        /* allocate node */
        Node new_node = new Node(); 

        /* put in the data */
        new_node.data = new_data; 

        /* link the old list to the new node */
        new_node.next = head_ref; 

        /* move the head to point to the new node */
        head_ref = new_node; 
        return head_ref; 
    } 

    // Function to count all pairs from both the linked lists 
    // whose product is equal to a given value 
    static int countPairs(Node head1, Node head2, int x) 
    { 
        int count = 0; 

        Node p1, p2; 

        // Traverse the 1st linked list 
        for (p1 = head1; p1 != null; p1 = p1.next)  
        { 
            // for each node of 1st list 
            // Traverse the 2nd list 
            for (p2 = head2; p2 != null; p2 = p2.next) 
            { 
                // if sum of pair is equal to 'x' 
                // increment count 
                if ((p1.data * p2.data) == x)  
                { 
                    count++; 
                } 
            } 
        } 

        // required count of pairs 
        return count; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        Node head1 = null; 
        Node head2 = null; 

        // create linked list1 3->1->5->7 
        head1 = push(head1, 7); 
        head1 = push(head1, 5); 
        head1 = push(head1, 1); 
        head1 = push(head1, 3); 

        // create linked list2 8->2->5->3 
        head2 = push(head2, 3); 
        head2 = push(head2, 5); 
        head2 = push(head2, 2); 
        head2 = push(head2, 8); 

        int x = 10; 

        Console.Write("Count = " + countPairs(head1, head2, x)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Count = 1

```

**时间复杂度**：`O(N ^ 2)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。