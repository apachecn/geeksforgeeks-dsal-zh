# 单链接列表的最小和最大素数

给定一个包含 N 个节点的单链列表，任务是查找最小和最大素数。

**示例：**

```
Input : List = 15 -> 16 -> 6 -> 7 -> 17
Output : Minimum : 7
         Maximum : 17

Input : List = 15 -> 3 -> 4 -> 2 -> 9
Output : Minimum : 2
         Maximum : 3

```

**方法：**

1.  这个想法是将链表遍历到最后，并将 max 和 min 变量分别初始化为 INT_MIN 和 INT_MAX。

2.  检查当前节点是否为素数。 如是：

    *   如果当前节点的值大于 max，则将当前节点的值分配给 max。

    *   如果当前节点的值小于 min，则将当前节点的值分配给 min。

3.  重复上述步骤，直到到达列表末尾。

以下是上述想法的实现：

## C++

```cpp

// C++ implementation to find minimum 
// and maximum prime number of 
// the singly linked list 
#include <bits/stdc++.h> 

using namespace std; 

// Node of the singly linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the beginning 
// of the singly Linked List 
void push(Node** head_ref, int new_data) 
{ 
    Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to check if a number is prime 
bool isPrime(int n) 
{ 
    // Corner cases 
    if (n <= 1) 
        return false; 
    if (n <= 3) 
        return true; 

    // This is checked so that we can skip 
    // middle five numbers in below loop 
    if (n % 2 == 0 || n % 3 == 0) 
        return false; 

    for (int i = 5; i * i <= n; i = i + 6) 
        if (n % i == 0 || n % (i + 2) == 0) 
            return false; 

    return true; 
} 

// Function to find maximum and minimum 
// prime nodes in a linked list 
void minmaxPrimeNodes(Node** head_ref) 
{ 
    int minimum = INT_MAX; 
    int maximum = INT_MIN; 
    Node* ptr = *head_ref; 

    while (ptr != NULL) { 
        // If current node is prime 
        if (isPrime(ptr->data)) { 
            // Update minimum 
            minimum = min(minimum, ptr->data); 

            // Update maximum 
            maximum = max(maximum, ptr->data); 
        } 
        ptr = ptr->next; 
    } 

    cout << "Minimum : " << minimum << endl; 
    cout << "Maximum : " << maximum << endl; 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the linked list 
    // 15 -> 16 -> 7 -> 6 -> 17 
    push(&head, 17); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 16); 
    push(&head, 15); 

    minmaxPrimeNodes(&head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find minimum  
// and maximum prime number of  
// the singly linked list  
class GFG 
{ 

// Node of the singly linked list  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to check if a number is prime  
static boolean isPrime(int n)  
{  
    // Corner cases  
    if (n <= 1)  
        return false;  
    if (n <= 3)  
        return true;  

    // This is checked so that we can skip  
    // middle five numbers in below loop  
    if (n % 2 == 0 || n % 3 == 0)  
        return false;  

    for (int i = 5; i * i <= n; i = i + 6)  
        if (n % i == 0 || n % (i + 2) == 0)  
            return false;  

    return true;  
}  

// Function to find maximum and minimum  
// prime nodes in a linked list  
static void minmaxPrimeNodes(Node head_ref)  
{  
    int minimum = Integer.MAX_VALUE;  
    int maximum = Integer.MIN_VALUE;  
    Node ptr = head_ref;  

    while (ptr != null)  
    {  
        // If current node is prime  
        if (isPrime(ptr.data)) 
        {  
            // Update minimum  
            minimum = Math.min(minimum, ptr.data);  

            // Update maximum  
            maximum = Math.max(maximum, ptr.data);  
        }  
        ptr = ptr.next;  
    }  

    System.out.println("Minimum : " + minimum );  
    System.out.println("Maximum : " + maximum );  
}  

// Driver code  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node head = null;  

    // create the linked list  
    // 15 . 16 . 7 . 6 . 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 16);  
    head = push(head, 15);  

    minmaxPrimeNodes(head);  

} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to find minimum  
# and maximum prime number of  
# the singly linked list  

# Structure of a Node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the beginning  
# of the singly Linked List  
def push(head_ref, new_data) : 

    new_node = Node(0)  
    new_node.data = new_data  
    new_node.next = (head_ref)  
    (head_ref) = new_node  
    return head_ref 

# Function to check if a number is prime  
def isPrime(n):  

    # Corner cases  
    if (n <= 1) : 
        return False
    if (n <= 3) : 
        return True

    # This is checked so that we can skip  
    # middle five numbers in below loop  
    if (n % 2 == 0 or n % 3 == 0) : 
        return False
    i = 5
    while(i * i <= n) : 
        if (n % i == 0 or n % (i + 2) == 0):  
            return False
        i = i + 6

    return True

# Function to find maximum and minimum  
# prime nodes in a linked list  
def minmaxPrimeNodes(head_ref) : 

    minimum = 999999999
    maximum = -999999999
    ptr = head_ref  

    while (ptr != None):  

        # If current node is prime  
        if (isPrime(ptr.data)): 

            # Update minimum  
            minimum = min(minimum, ptr.data)  

            # Update maximum  
            maximum = max(maximum, ptr.data)  

        ptr = ptr.next

    print ("Minimum : ", minimum) 
    print ("Maximum : ", maximum) 

# Driver code  

# start with the empty list  
head = None

# create the linked list  
# 15 . 16 . 7 . 6 . 17  
head = push(head, 17)  
head = push(head, 7)  
head = push(head, 6)  
head = push(head, 16)  
head = push(head, 15)  

minmaxPrimeNodes(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to find minimum  
// and maximum prime number of  
// the singly linked list  
using System; 

class GFG 
{ 

// Node of the singly linked list  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = (head_ref);  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to check if a number is prime  
static bool isPrime(int n)  
{  
    // Corner cases  
    if (n <= 1)  
        return false;  
    if (n <= 3)  
        return true;  

    // This is checked so that we can skip  
    // middle five numbers in below loop  
    if (n % 2 == 0 || n % 3 == 0)  
        return false;  

    for (int i = 5; i * i <= n; i = i + 6)  
        if (n % i == 0 || n % (i + 2) == 0)  
            return false;  

    return true;  
}  

// Function to find maximum and minimum  
// prime nodes in a linked list  
static void minmaxPrimeNodes(Node head_ref)  
{  
    int minimum = int.MaxValue;  
    int maximum = int.MinValue;  
    Node ptr = head_ref;  

    while (ptr != null)  
    {  
        // If current node is prime  
        if (isPrime(ptr.data)) 
        {  
            // Update minimum  
            minimum = Math.Min(minimum, ptr.data);  

            // Update maximum  
            maximum = Math.Max(maximum, ptr.data);  
        }  
        ptr = ptr.next;  
    }  

    Console.WriteLine("Minimum : " + minimum);  
    Console.WriteLine("Maximum : " + maximum);  
}  

// Driver code  
public static void Main() 
{  
    // start with the empty list  
    Node head = null;  

    // create the linked list  
    // 15 . 16 . 7 . 6 . 17  
    head = push(head, 17);  
    head = push(head, 7);  
    head = push(head, 6);  
    head = push(head, 16);  
    head = push(head, 15);  

    minmaxPrimeNodes(head);  
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
Minimum : 7
Maximum : 17

```

**时间复杂度：** O（N），其中 N 是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。