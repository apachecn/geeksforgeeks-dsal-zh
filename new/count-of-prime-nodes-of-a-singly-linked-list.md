# 单链接列表

的主要节点数

给定一个包含N个节点的单链列表，任务是查找素数的总数。

**示例：**

```
Input: List = 15 -> 5 -> 6 -> 10 -> 17
Output: 2
5 and 17 are the prime nodes

Input: List = 29 -> 3 -> 4 -> 2 -> 9
Output: 3
2, 3 and 29 are the prime nodes

```

**方法：**的想法是将链表遍历到最后并检查当前节点是否为质数。 如果是，则将计数增加1并继续执行相同操作，直到遍历所有节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find count of prime numbers 
// in the singly linked list 
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

// Function to find count of prime 
// nodes in a linked list 
int countPrime(Node** head_ref) 
{ 
    int count = 0; 
    Node* ptr = *head_ref; 

    while (ptr != NULL) { 
        // If current node is prime 
        if (isPrime(ptr->data)) { 
            // Update count 
            count++; 
        } 
        ptr = ptr->next; 
    } 

    return count; 
} 

// Driver program 
int main() 
{ 
    // start with the empty list 
    Node* head = NULL; 

    // create the linked list 
    // 15 -> 5 -> 6 -> 10 -> 17 
    push(&head, 17); 
    push(&head, 10); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 15); 

    // Function call to print require answer 
    cout << "Count of prime nodes = "
         << countPrime(&head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find count of prime numbers  
// in the singly linked list  
class solution 
{ 

// Node of the singly linked list  
static class Node {  
    int data;  
    Node  next;  
} 

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node   head_ref, int new_data)  
{  
    Node  new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = ( head_ref);  
    ( head_ref) = new_node;  
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

// Function to find count of prime  
// nodes in a linked list  
static int countPrime(Node   head_ref)  
{  
    int count = 0;  
    Node  ptr =  head_ref;  

    while (ptr != null) {  
        // If current node is prime  
        if (isPrime(ptr.data)) {  
            // Update count  
            count++;  
        }  
        ptr = ptr.next;  
    }  

    return count;  
}  

// Driver program  
public static void main(String args[]) 
{  
    // start with the empty list  
    Node  head = null;  

    // create the linked list  
    // 15 . 5 . 6 . 10 . 17  
    head=push(head, 17);  
    head=push(head, 10);  
    head=push(head, 6);  
    head=push(head, 5);  
    head=push(head, 15);  

    // Function call to print require answer  
    System.out.print( "Count of prime nodes = "+ countPrime(head));  

}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation to find count of  
# prime numbers in the singly linked list 

# Function to check if a number is prime  
def isPrime(n):  

    # Corner cases  
    if n <= 1:  
        return False
    if n <= 3: 
        return True

    # This is checked so that we can skip  
    # middle five numbers in below loop  
    if n % 2 == 0 or n % 3 == 0:  
        return False

    i = 5
    while i * i <= n:  
        if n % i == 0 or n % (i + 2) == 0:  
            return False
        i += 6

    return True

# Link list node 
class Node:  

    def __init__(self, data, next): 
        self.data = data 
        self.next = next

class LinkedList: 

    def __init__(self): 
        self.head = None

    # Push a new node on the front of the list.      
    def push(self, new_data): 
        new_node = Node(new_data, self.head) 
        self.head = new_node 

    # Function to find count of prime  
    # nodes in a linked list  
    def countPrime(self):  

        count = 0
        ptr = self.head  

        while ptr != None:  

            # If current node is prime  
            if isPrime(ptr.data):  

                # Update count  
                count += 1

            ptr = ptr.next

        return count  

# Driver Code 
if __name__ == "__main__": 

    # Start with the empty list 
    linkedlist = LinkedList() 

    # create the linked list  
    # 15 -> 5 -> 6 -> 10 -> 17  
    linkedlist.push(17)  
    linkedlist.push(10)  
    linkedlist.push(6)  
    linkedlist.push(5)  
    linkedlist.push(15)  

    # Function call to print require answer  
    print("Count of prime nodes =", 
           linkedlist.countPrime())  

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation to find count of prime numbers  
// in the singly linked list  
using System; 

class GFG 
{ 

// Node of the singly linked list  
public class Node  
{  
    public int data;  
    public Node next;  
} 

// Function to insert a node at the beginning  
// of the singly Linked List  
static Node push(Node head_ref, int new_data)  
{  
    Node new_node = new Node();  
    new_node.data = new_data;  
    new_node.next = ( head_ref);  
    ( head_ref) = new_node;  
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

// Function to find count of prime  
// nodes in a linked list  
static int countPrime(Node head_ref)  
{  
    int count = 0;  
    Node ptr = head_ref;  

    while (ptr != null)  
    {  
        // If current node is prime  
        if (isPrime(ptr.data))  
        {  
            // Update count  
            count++;  
        }  
        ptr = ptr.next;  
    }  

    return count;  
}  

// Driver code  
public static void Main(String []args) 
{  
    // start with the empty list  
    Node head = null;  

    // create the linked list  
    // 15 . 5 . 6 . 10 . 17  
    head=push(head, 17);  
    head=push(head, 10);  
    head=push(head, 6);  
    head=push(head, 5);  
    head=push(head, 15);  

    // Function call to print require answer  
    Console.Write( "Count of prime nodes = "+ countPrime(head));  
}  
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Count of prime nodes = 2

```

**时间复杂度：** O（N * sqrt（P）），其中N是LinkedList的长度，P是列表中的最大元素



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。