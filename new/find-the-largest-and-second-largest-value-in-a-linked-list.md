# 在链表中查找最大和第二大的值

> 原文：[https://www.geeksforgeeks.org/find-the-largest-and-second-largest-value-in-a-linked-list/](https://www.geeksforgeeks.org/find-the-largest-and-second-largest-value-in-a-linked-list/)

给定[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，任务是在链表中找到最大和第二大的值。

**例如**：

> **输入**：`LL = 10 -> 15 -> 5 -> 20 -> 7 ->-> 9`
>
> **输出**：
>
> 最大为 20
>
> 第二大为 15
>
> **输入**：`LL = 0 -> 5 -> 52 -> 21`
>
> **输出**：
>
> 最大为 52
>
> 第二大为 21

**方法**：

1.  将前两个节点的最大值存储在变量`max`中。

2.  将前两个节点的最小值存储在变量`second_max`中。

3.  遍历其余的链表。 对于每个节点：

    *   如果当前节点的值大于`max`，则将`second_max`设置为`max`，将`max`设置为当前节点的值。

    *   否则，如果当前节点的值大于`second_max`，则将`second_max`设置为当前节点的值。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the largest and 
// second largest element in a Linked List 

#include <bits/stdc++.h> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to push the node at the 
// beginning of the linked list 
void push(struct Node** head_ref, 
          int new_data) 
{ 
    struct Node* new_node 
        = (struct Node*)malloc( 
            sizeof(struct Node)); 

    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to print the largest 
// and second largest element 
void findLargestAndSecondLargest(struct Node* head) 
{ 
    // initialise max and second max using 
    // first two nodes of linked list 
    int val1 = head->data, 
        val2 = head->next->data, 
        max = std::max(val1, val2), 
        second_max = std::min(val1, val2); 

    // move the head pointer to 3rd node 
    head = head->next->next; 

    // iterate over rest of linked list 
    while (head != NULL) { 

        if (head->data > max) { 

            // If current node value is greater 
            // than max, then set second_max as 
            // current max value and max as 
            // current node value 
            second_max = max; 
            max = head->data; 
        } 
        else if (head->data > second_max) { 

            // else if current node value is 
            // greater than second_max, set 
            // second_max as node value 
            second_max = head->data; 
        } 

        // move the head pointer to next node 
        head = head->next; 
    } 

    // Print the largest 
    // and second largest value 
    cout << "Largest = "
         << max << endl; 
    cout << "Second Largest = "
         << second_max << endl; 
} 

// Driver code 
int main() 
{ 
    struct Node* head = NULL; 

    push(&head, 20); 
    push(&head, 5); 
    push(&head, 15); 
    push(&head, 10); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 11); 
    push(&head, 9); 

    findLargestAndSecondLargest(head); 

    return 0; 
} 

```

## Java

```java

// Java program to find the largest and 
// second largest element in a Linked List 
class GFG{ 

// Link list node 
static class Node { 
    int data; 
    Node next; 

}; 

// Function to push the node at the 
// beginning of the linked list 
static Node push(Node head_ref, 
          int new_data) 
{ 
    Node new_node 
        = new Node(); 

    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to print the largest 
// and second largest element 
static void findLargestAndSecondLargest(Node head) 
{ 
    // initialise max and second max using 
    // first two nodes of linked list 
    int val1 = head.data, 
        val2 = head.next.data, 
        max = Math.max(val1, val2), 
        second_max = Math.min(val1, val2); 

    // move the head pointer to 3rd node 
    head = head.next.next; 

    // iterate over rest of linked list 
    while (head != null) { 

        if (head.data > max) { 

            // If current node value is greater 
            // than max, then set second_max as 
            // current max value and max as 
            // current node value 
            second_max = max; 
            max = head.data; 
        } 
        else if (head.data > second_max) { 

            // else if current node value is 
            // greater than second_max, set 
            // second_max as node value 
            second_max = head.data; 
        } 

        // move the head pointer to next node 
        head = head.next; 
    } 

    // Print the largest 
    // and second largest value 
    System.out.print("Largest = "
         + max +"\n"); 
    System.out.print("Second Largest = "
         + second_max +"\n"); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node head = null; 

    head = push(head, 20); 
    head = push(head, 5); 
    head = push(head, 15); 
    head = push(head, 10); 
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 11); 
    head = push(head, 9); 

    findLargestAndSecondLargest(head); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 program to find the largest and 
# second largest element in a Linked List 
# Node class  
class Node:  

    # Function to initialize the node object  
    def __init__(self, data):  

        # Assign data  
        self.data = data  

        # Initialize  
        # next as null 
        self.next = None 

# Linked List Class 
class LinkedList: 

    # Function to initialize the 
    # LinkedList class. 
    def __init__(self):  

        # Initialize head as None  
        self.head = None 

    # This function insert a new node at the  
    # beginning of the linked list  
    def push(self, new_data):  

        # Create a new Node  
        new_node = Node(new_data)  

        # Make next of new Node as head  
        new_node.next = self.head  

        # Move the head to point to new Node  
        self.head = new_node 

    # Function to find the max and 
    # second largest value from the list 
    def findLargestAndSecondLargest(self): 

        # Take a Head to iterate list 
        Head = self.head 

        # Initialize max and second_max 
        # using first two nodes of the list 
        val1 = Head.data 
        val2 = Head.next.data 
        Max = max(val1, val2) 
        second_max = min(val1, val2) 

        # Move the Head to third node 
        Head = Head.next.next

        # Iterate over rest of linked list 
        while(Head != None): 

            # If current node value is  
            # greater then Max then 
            if(Head.data > Max): 

                # Set the current max to second_max 
                # and current node value to max 
                second_max = Max
                Max = Head.data 

            # Else if current node value is 
            # greater then second_max value 
            elif(Head.data > second_max): 

                # Then current node value 
                # to second_max 
                second_max = Head.data 

            # Move the head to next node 
            Head = Head.next

        # Print the largest and second largest values 
        print("Largest = ", Max) 
        print("Second Largest = ", second_max) 

# Driver code 
if __name__ == '__main__': 

    # Initialising the linked list 
    head = LinkedList() 

    # Pushing the values in list 
    head.push(20) 
    head.push(5) 
    head.push(15) 
    head.push(10) 
    head.push(7) 
    head.push(6) 
    head.push(11) 
    head.push(9) 

    # Calling the function to print 
    # largest and second largest values. 
    head.findLargestAndSecondLargest() 

# This code is contributed by Amit Mangal. 

```

## C#

```cs

// C# program to find the largest and 
// second largest element in a Linked List 
using System; 

class GFG{ 

// Link list node 
class Node { 
    public int data; 
    public Node next; 

}; 

// Function to push the node at the 
// beginning of the linked list 
static Node push(Node head_ref, 
          int new_data) 
{ 
    Node new_node 
        = new Node(); 

    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to print the largest 
// and second largest element 
static void findLargestAndSecondLargest(Node head) 
{ 
    // initialise max and second max using 
    // first two nodes of linked list 
    int val1 = head.data, 
        val2 = head.next.data, 
        max = Math.Max(val1, val2), 
        second_max = Math.Min(val1, val2); 

    // move the head pointer to 3rd node 
    head = head.next.next; 

    // iterate over rest of linked list 
    while (head != null) { 

        if (head.data > max) { 

            // If current node value is greater 
            // than max, then set second_max as 
            // current max value and max as 
            // current node value 
            second_max = max; 
            max = head.data; 
        } 
        else if (head.data > second_max) { 

            // else if current node value is 
            // greater than second_max, set 
            // second_max as node value 
            second_max = head.data; 
        } 

        // move the head pointer to next node 
        head = head.next; 
    } 

    // Print the largest 
    // and second largest value 
    Console.Write("Largest = "
         + max +"\n"); 
    Console.Write("Second Largest = "
         + second_max +"\n"); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node head = null; 

    head = push(head, 20); 
    head = push(head, 5); 
    head = push(head, 15); 
    head = push(head, 10); 
    head = push(head, 7); 
    head = push(head, 6); 
    head = push(head, 11); 
    head = push(head, 9); 

    findLargestAndSecondLargest(head); 
} 
} 

// This code is contributed by Princi Singh 

```

**输出**： 

```
Largest = 20
Second Largest = 15

```

**性能分析**：

*   **时间复杂度**：在上述方法中，由于我们仅对链表进行一次迭代，因此时间复杂度为`O(n)`。

*   **辅助空间复杂度**：在上述方法中，除了几个恒定大小的变量之外，我们没有使用任何额外的空间，因此辅助空间复杂度为`O(1)`。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。