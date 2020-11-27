# 单链表的所有偶数和节点的和与乘积

> 原文：[https://www.geeksforgeeks.org/sum-and-product-of-all-even-digit-sum-nodes-of-a-singly-linked-list/](https://www.geeksforgeeks.org/sum-and-product-of-all-even-digit-sum-nodes-of-a-singly-linked-list/)

给定一个包含`N`个节点的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从列表中找到其数据值具有偶数数字和的所有节点的和与乘积。

**示例**：

> **输入**：`15 -> 16 -> 8 -> 6 -> 13`
>
> **输出**：
>
> ```
> sum = 42
> product = 9360
> ```
> 
> **说明**：
>
> 链表中数字的所有位数的总和为：
>
> ```
> 15 = 1 + 5 = 6
> 16 = 1 + 6 = 7
> 8 = 8
> 6 = 6
> 13 = 1 + 3 = 4
> ```
> 
> 该列表包含 4 个偶数和数据值 15、8、6 和 13。
>
> ```
> sum = 15 + 8 + 6 + 13 = 42
> product = 15 * 8 * 6 * 13 = 9360
> ```
>
> **输入**：`5 -> 3 -> 4 -> 2 -> 9`
>
> **输出**：
>
> ```
> sum = 6
> product = 8
> ```
> 
> **说明**：
>
> 该列表包含 2 个偶数总和数据值 4 和 2。
>
> ```
> sum = 4 + 2 = 6
> product = 4 * 2 = 8
> ```

**方法**：的想法是遍历给定的链表，并检查当前节点值的所有数字的[总和是否为偶数](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。 如果是，则将当前节点值包括到结果总和以及结果乘积中，否则检查下一个节点值。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Node of Linked List 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the 
// beginning of the singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    // Allocate new node 
    Node* new_node 
        = (Node*)malloc( 
            sizeof(struct Node)); 

    // Insert the data 
    new_node->data = new_data; 

    // Link old list to the new node 
    new_node->next = (*head_ref); 

    // Move head to point the new node 
    (*head_ref) = new_node; 
} 

// Function to find the digit sum 
// for a number 
int digitSum(int num) 
{ 
    int sum = 0; 
    while (num) { 
        sum += (num % 10); 
        num /= 10; 
    } 

    // Return the sum 
    return sum; 
} 

// Function to find the required 
// sum and product 
void sumAndProduct(Node* head_ref) 
{ 

    // Initialise the sum and product 
    // to 0 and 1 respectively 
    int prod = 1; 
    int sum = 0; 

    Node* ptr = head_ref; 

    // Traverse the given linked list 
    while (ptr != NULL) { 

        // If current node has even 
        // digit sum then include it in 
        // resultant sum and product 
        if (!(digitSum(ptr->data) & 1)) { 

            // Find the sum and the product 
            prod *= ptr->data; 
            sum += ptr->data; 
        } 

        ptr = ptr->next; 
    } 

    // Print the final Sum and Product 
    cout << "Sum = " << sum << endl; 
    cout << "Product = " << prod; 
} 

// Driver Code 
int main() 
{ 
    // Head of the linked list 
    Node* head = NULL; 

    // Create the linked list 
    // 15 -> 16 -> 8 -> 6 -> 13 
    push(&head, 13); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 16); 
    push(&head, 15); 

    // Function call 
    sumAndProduct(head); 

    return 0; 
} 

```

## Java

```java

// Java program for the above approach 

class GFG{ 

// Node of Linked List 
static class Node { 
    int data; 
    Node next; 
}; 

// Function to insert a node at the 
// beginning of the singly Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    // Allocate new node 
    Node new_node 
        = new Node(); 

    // Insert the data 
    new_node.data = new_data; 

    // Link old list to the new node 
    new_node.next = head_ref; 

    // Move head to point the new node 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to find the digit sum 
// for a number 
static int digitSum(int num) 
{ 
    int sum = 0; 
    while (num > 0) { 
        sum += (num % 10); 
        num /= 10; 
    } 

    // Return the sum 
    return sum; 
} 

// Function to find the required 
// sum and product 
static void sumAndProduct(Node head_ref) 
{ 

    // Initialise the sum and product 
    // to 0 and 1 respectively 
    int prod = 1; 
    int sum = 0; 

    Node ptr = head_ref; 

    // Traverse the given linked list 
    while (ptr != null) { 

        // If current node has even 
        // digit sum then include it in 
        // resultant sum and product 
        if ((digitSum(ptr.data) %2 != 1)) { 

            // Find the sum and the product 
            prod *= ptr.data; 
            sum += ptr.data; 
        } 

        ptr = ptr.next; 
    } 

    // Print the final Sum and Product 
    System.out.print("Sum = " + sum +"\n"); 
    System.out.print("Product = " + prod); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    // Head of the linked list 
    Node head = null; 

    // Create the linked list 
    // 15.16.8.6.13 
    head = push(head, 13); 
    head = push(head, 6); 
    head = push(head, 8); 
    head = push(head, 16); 
    head = push(head, 15); 

    // Function call 
    sumAndProduct(head); 

} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# program for the above approach 
using System; 

class GFG{ 

// Node of Linked List 
class Node 
{ 
    public int data; 
    public Node next; 
}; 

// Function to insert a node at the 
// beginning of the singly Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    // Allocate new node 
    Node new_node = new Node(); 

    // Insert the data 
    new_node.data = new_data; 

    // Link old list to the new node 
    new_node.next = head_ref; 

    // Move head to point the new node 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to find the digit sum 
// for a number 
static int digitSum(int num) 
{ 
    int sum = 0; 
    while (num > 0)  
    { 
        sum += (num % 10); 
        num /= 10; 
    } 

    // Return the sum 
    return sum; 
} 

// Function to find the required 
// sum and product 
static void sumAndProduct(Node head_ref) 
{ 

    // Initialise the sum and product 
    // to 0 and 1 respectively 
    int prod = 1; 
    int sum = 0; 

    Node ptr = head_ref; 

    // Traverse the given linked list 
    while (ptr != null) 
    { 

        // If current node has even 
        // digit sum then include it in 
        // resultant sum and product 
        if ((digitSum(ptr.data) % 2 != 1)) 
        { 

            // Find the sum and the product 
            prod *= ptr.data; 
            sum += ptr.data; 
        } 

        ptr = ptr.next; 
    } 

    // Print the readonly Sum and Product 
    Console.Write("Sum = " + sum + "\n"); 
    Console.Write("Product = " + prod); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    // Head of the linked list 
    Node head = null; 

    // Create the linked list 
    // 15.16.8.6.13 
    head = push(head, 13); 
    head = push(head, 6); 
    head = push(head, 8); 
    head = push(head, 16); 
    head = push(head, 15); 

    // Function call 
    sumAndProduct(head); 

} 
} 

// This code is contributed by Rohit_ranjan 

```

**输出**：

```
Sum = 42
Product = 9360

```

**时间复杂度**：`O(n)`，其中`N`是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。