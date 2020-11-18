# 给定链表

中的最大邻接节点数

给定一个链表，任务是找到任何连续节点的最大和。

**示例：**

> **输入：** -2-> -3-> 4-> -1-> -2-> 1-> 5-> -3- > NULL
> **输出：** 7
> 4-> -1-> -2-> 1-> 5是给定的子列表 和。
> 
> **输入：** 1-> 2-> 3-> 4->空
> **输出：** 10

**方法：[该](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)文章在[中讨论了Kadane的算法，该算法适用于数组以找到最大子数组总和，但也可以对其进行修改以适用于链表。 由于Kadane的算法不需要访问随机元素，因此它也可以线性时间应用于链表。](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)**

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
class Node { 
public: 
    int data; 
    Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, appends a new node at the end */
void append(Node** head_ref, int new_data) 
{ 
    // Allocate node 
    Node* new_node = new Node(); 

    Node* last = *head_ref; /* used in step 5*/

    // Put in the data 
    new_node->data = new_data; 

    /* This new node is going to be  
    the last node, so make next of  
    it as NULL*/
    new_node->next = NULL; 

    /* If the Linked List is empty,  
    then make the new node as head */
    if (*head_ref == NULL) { 
        *head_ref = new_node; 
        return; 
    } 

    // Else traverse till the last node 
    while (last->next != NULL) 
        last = last->next; 

    // Change the next of last node 
    last->next = new_node; 
    return; 
} 

// Function to return the maximum contiguous 
// nodes sum in the given linked list 
int MaxContiguousNodeSum(Node* head) 
{ 

    // If the list is empty 
    if (head == NULL) 
        return 0; 

    // If the list contains a single element 
    if (head->next == NULL) 
        return head->data; 

    // max_ending_here will store the maximum sum 
    // ending at the current node, currently it 
    // will be initialised to the maximum sum ending 
    // at the first node which is the first node's value 
    int max_ending_here = head->data; 

    // max_so_far will store the maximum sum of 
    // contiguous nodes so far which is the required 
    // answer at the end of the linked list traversal 
    int max_so_far = head->data; 

    // Starting from the second node 
    head = head->next; 

    // While there are nodes in linked list 
    while (head != NULL) { 

        // max_ending_here will be the maximum of either 
        // the current node's value or the current node's 
        // value added with the max_ending_here 
        // for the previous node 
        max_ending_here = max(head->data, 
                              max_ending_here + head->data); 

        // Update the maximum sum so far 
        max_so_far = max(max_ending_here, max_so_far); 

        // Get to the next node 
        head = head->next; 
    } 

    // Return the maximum sum so far 
    return max_so_far; 
} 

// Driver code 
int main() 
{ 
    // Create the linked list 
    Node* head = NULL; 
    append(&head, -2); 
    append(&head, -3); 
    append(&head, 4); 
    append(&head, -1); 
    append(&head, -2); 
    append(&head, 1); 
    append(&head, 5); 
    append(&head, -3); 

    cout << MaxContiguousNodeSum(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, appends a new node at the end */
static Node append(Node head_ref, int new_data) 
{ 
    // Allocate node 
    Node new_node = new Node(); 

    Node last = head_ref; /* used in step 5*/

    // Put in the data 
    new_node.data = new_data; 

    /* This new node is going to be  
    the last node, so make next of  
    it as null*/
    new_node.next = null; 

    /* If the Linked List is empty,  
    then make the new node as head */
    if (head_ref == null)  
    { 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Else traverse till the last node 
    while (last.next != null) 
        last = last.next; 

    // Change the next of last node 
    last.next = new_node; 
    return head_ref; 
} 

// Function to return the maximum contiguous 
// nodes sum in the given linked list 
static int MaxContiguousNodeSum(Node head) 
{ 

    // If the list is empty 
    if (head == null) 
    return 0; 

    // If the list contains a single element 
    if (head.next == null) 
        return head.data; 

    // max_ending_here will store the maximum sum 
    // ending at the current node, currently it 
    // will be initialised to the maximum sum ending 
    // at the first node which is the first node's value 
    int max_ending_here = head.data; 

    // max_so_far will store the maximum sum of 
    // contiguous nodes so far which is the required 
    // answer at the end of the linked list traversal 
    int max_so_far = head.data; 

    // Starting from the second node 
    head = head.next; 

    // While there are nodes in linked list 
    while (head != null)  
    { 

        // max_ending_here will be the maximum of either 
        // the current node's value or the current node's 
        // value added with the max_ending_here 
        // for the previous node 
        max_ending_here = Math.max(head.data, 
                            max_ending_here + head.data); 

        // Update the maximum sum so far 
        max_so_far = Math.max(max_ending_here, max_so_far); 

        // Get to the next node 
        head = head.next; 
    } 

    // Return the maximum sum so far 
    return max_so_far; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Create the linked list 
    Node head = null; 
    head = append(head, -2); 
    head = append(head, -3); 
    head = append(head, 4); 
    head = append(head, -1); 
    head = append(head, -2); 
    head = append(head, 1); 
    head = append(head, 5); 
    head = append(head, -3); 

    System.out.print(MaxContiguousNodeSum(head)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## C#

```cs

// C# implementation of the approach 
using System; 
class GFG 
{ 

// A linked list node 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, appends a new node at the end */
static Node append(Node head_ref, int new_data) 
{ 
    // Allocate node 
    Node new_node = new Node(); 

    Node last = head_ref; /* used in step 5*/

    // Put in the data 
    new_node.data = new_data; 

    /* This new node is going to be  
    the last node, so make next of  
    it as null*/
    new_node.next = null; 

    /* If the Linked List is empty,  
    then make the new node as head */
    if (head_ref == null)  
    { 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Else traverse till the last node 
    while (last.next != null) 
        last = last.next; 

    // Change the next of last node 
    last.next = new_node; 
    return head_ref; 
} 

// Function to return the maximum contiguous 
// nodes sum in the given linked list 
static int MaxContiguousNodeSum(Node head) 
{ 

    // If the list is empty 
    if (head == null) 
    return 0; 

    // If the list contains a single element 
    if (head.next == null) 
        return head.data; 

    // max_ending_here will store the maximum sum 
    // ending at the current node, currently it 
    // will be initialised to the maximum sum ending 
    // at the first node which is the first node's value 
    int max_ending_here = head.data; 

    // max_so_far will store the maximum sum of 
    // contiguous nodes so far which is the required 
    // answer at the end of the linked list traversal 
    int max_so_far = head.data; 

    // Starting from the second node 
    head = head.next; 

    // While there are nodes in linked list 
    while (head != null)  
    { 

        // max_ending_here will be the maximum of either 
        // the current node's value or the current node's 
        // value added with the max_ending_here 
        // for the previous node 
        max_ending_here = Math.Max(head.data, 
                                   max_ending_here +  
                                   head.data); 

        // Update the maximum sum so far 
        max_so_far = Math.Max(max_ending_here,  
                              max_so_far); 

        // Get to the next node 
        head = head.next; 
    } 

    // Return the maximum sum so far 
    return max_so_far; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Create the linked list 
    Node head = null; 
    head = append(head, -2); 
    head = append(head, -3); 
    head = append(head, 4); 
    head = append(head, -1); 
    head = append(head, -2); 
    head = append(head, 1); 
    head = append(head, 5); 
    head = append(head, -3); 

    Console.Write(MaxContiguousNodeSum(head)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
7

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。