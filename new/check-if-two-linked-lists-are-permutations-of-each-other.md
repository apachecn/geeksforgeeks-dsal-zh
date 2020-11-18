# 检查两个链接列表是否彼此置换

给定两个单独链接的整数数据列表。 任务是编写一个程序，该程序可以有效地检查两个链接列表是否相互置换。

**范例**：

```
Input: 1 -> 2 -> 3 -> 4 -> 5
        2 -> 1 -> 3 -> 5 -> 4
Output: Yes

Input: 10 -> 20 -> 30 -> 40
        20 -> 50 -> 60 -> 70
Output: No

```

**方法**：对两个链表执行以下操作：

1.  以一个临时节点指向链接列表的开头。

2.  开始遍历链表，并保留节点数据的总和和乘法。

**注意**：在两个链表的总和和相乘之后，检查两个链表的*和*和*乘和*是否相等。 如果它们相等，则意味着链表是彼此置换的，否则就不是。

下面是上述方法的实现：

## C++

```cpp

// C++ program to check if linked lists 
// are permutations of each other 
#include <bits/stdc++.h> 

using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/*Function to check if two linked lists 
* are permutations of each other 
* first : reference to head of first linked list 
* second : reference to head of second linked list 
*/
bool isPermutation(struct Node* first, struct Node* second) 
{ 

    // Variables to keep track of sum and multiplication 
    int sum1 = 0, sum2 = 0, mul1 = 1, mul2 = 1; 

    struct Node* temp1 = first; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp1 != NULL) { 
        sum1 += temp1->data; 
        mul1 *= temp1->data; 
        temp1 = temp1->next; 
    } 

    struct Node* temp2 = second; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp2 != NULL) { 
        sum2 += temp2->data; 
        mul2 *= temp2->data; 
        temp2 = temp2->next; 
    } 

    return ((sum1 == sum2) && (mul1 == mul2)); 
} 

// Function to add a node at the 
// beginning of Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* first = NULL; 

    /* First constructed linked list is:  
    12 -> 35 -> 1 -> 10 -> 34 -> 1 */
    push(&first, 1); 
    push(&first, 34); 
    push(&first, 10); 
    push(&first, 1); 
    push(&first, 35); 
    push(&first, 12); 

    struct Node* second = NULL; 
    /* Second constructed linked list is:  
    35 -> 1 -> 12 -> 1 -> 10 -> 34 */
    push(&second, 35); 
    push(&second, 1); 
    push(&second, 12); 
    push(&second, 1); 
    push(&second, 10); 
    push(&second, 34); 

    if (isPermutation(first, second)) { 
        cout << "Yes" << endl; 
    } 
    else { 
        cout << "No" << endl; 
    } 

    return 0; 
} 

```

## Java

```java

// Java program to check if linked lists 
// are permutations of each other 
import java.util.*; 

class GFG  
{ 
static class Node  
{ 
    int data; 
    Node next; 
}; 

/*Function to check if two linked lists 
* are permutations of each other 
* first : reference to head of first linked list 
* second : reference to head of second linked list 
*/
static boolean isPermutation(Node first,  
                             Node second) 
{ 

    // Variables to keep track of 
    // sum and multiplication 
    int sum1 = 0, sum2 = 0,  
        mul1 = 1, mul2 = 1; 

    Node temp1 = first; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp1 != null)  
    { 
        sum1 += temp1.data; 
        mul1 *= temp1.data; 
        temp1 = temp1.next; 
    } 

    Node temp2 = second; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp2 != null) 
    { 
        sum2 += temp2.data; 
        mul2 *= temp2.data; 
        temp2 = temp2.next; 
    } 

    return ((sum1 == sum2) &&  
            (mul1 == mul2)); 
} 

// Function to add a node at the 
// beginning of Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    Node first = null; 

    /* First constructed linked list is:  
    12 . 35 . 1 . 10 . 34 . 1 */
    first = push(first, 1); 
    first = push(first, 34); 
    first = push(first, 10); 
    first = push(first, 1); 
    first = push(first, 35); 
    first = push(first, 12); 

    Node second = null; 

    /* Second constructed linked list is:  
    35 . 1 . 12 . 1 . 10 . 34 */
    second = push(second, 35); 
    second = push(second, 1); 
    second = push(second, 12); 
    second = push(second, 1); 
    second = push(second, 10); 
    second = push(second, 34); 

    if (isPermutation(first, second)) 
    { 
        System.out.print("Yes"); 
    } 
    else 
    { 
        System.out.print("No"); 
    } 
} 
}  

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# program to check if linked lists 
// are permutations of each other 
using System; 

class GFG  
{ 
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

/*Function to check if two linked lists 
* are permutations of each other 
* first : reference to head of first linked list 
* second : reference to head of second linked list 
*/
static bool isPermutation(Node first,  
                          Node second) 
{ 

    // Variables to keep track of 
    // sum and multiplication 
    int sum1 = 0, sum2 = 0,  
        mul1 = 1, mul2 = 1; 

    Node temp1 = first; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp1 != null)  
    { 
        sum1 += temp1.data; 
        mul1 *= temp1.data; 
        temp1 = temp1.next; 
    } 

    Node temp2 = second; 

    // Traversing through linked list 
    // and calculating sum and multiply 
    while (temp2 != null) 
    { 
        sum2 += temp2.data; 
        mul2 *= temp2.data; 
        temp2 = temp2.next; 
    } 

    return ((sum1 == sum2) &&  
            (mul1 == mul2)); 
} 

// Function to add a node at the 
// beginning of Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head_ref; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    Node first = null; 

    /* First constructed linked list is:  
    12 . 35 . 1 . 10 . 34 . 1 */
    first = push(first, 1); 
    first = push(first, 34); 
    first = push(first, 10); 
    first = push(first, 1); 
    first = push(first, 35); 
    first = push(first, 12); 

    Node second = null; 

    /* Second constructed linked list is:  
    35 . 1 . 12 . 1 . 10 . 34 */
    second = push(second, 35); 
    second = push(second, 1); 
    second = push(second, 12); 
    second = push(second, 1); 
    second = push(second, 10); 
    second = push(second, 34); 

    if (isPermutation(first, second)) 
    { 
        Console.Write("Yes"); 
    } 
    else
    { 
        Console.Write("No"); 
    } 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Yes

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。