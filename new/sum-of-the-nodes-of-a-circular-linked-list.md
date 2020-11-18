# 循环链表

的节点总和

给定一个[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)。 任务是找到给定链表的节点总数。

![](img/462afffb8d425a09fa443768f1676313.png)

对于上述通告列表，sum = 2 + 5 + 7 + 8 + 10 = 32

**示例：**

```
Input: 11->2->56->12
Output: Sum of Circular linked list is = 81

Input: 2-> 5 -> 7 -> 8 -> 10
Output: Sum of Circular linked list is = 32   

```

**方法：**

1.  使用链接列表的开头和0的sum变量初始化指针temp。
2.  Start traversing the linked list using a loop until all the nodes get traversed.
    *   将当前节点的值添加到总和，即总和+ = temp->数据。
    *   递增指向链接列表的下一个节点的指针，即temp = temp-> next。
3.  返回总和。

下面是上述方法的实现：

## C++

```cpp

// CPP program to find the sum of all nodes 
// of a Circular linked list 

#include <bits/stdc++.h> 
using namespace std; 

// Structure for a node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to insert a node at the beginning 
// of a Circular linked list 
void push(struct Node** head_ref, int data) 
{ 
    struct Node* ptr1 = (struct Node*)malloc(sizeof(struct Node)); 
    struct Node* temp = *head_ref; 
    ptr1->data = data; 
    ptr1->next = *head_ref; 

    // If linked list is not NULL then 
    // set the next of last node 
    if (*head_ref != NULL) { 
        while (temp->next != *head_ref) 
            temp = temp->next; 
        temp->next = ptr1; 
    } 
    else
        ptr1->next = ptr1; // For the first node 

    *head_ref = ptr1; 
} 

// Function to find sum of the given 
// Circular linked list 
int sumOfList(struct Node* head) 
{ 
    struct Node* temp = head; 
    int sum = 0; 
    if (head != NULL) { 
        do { 
            temp = temp->next; 
            sum += temp->data; 
        } while (temp != head); 
    } 

    return sum; 
} 

// Driver code 
int main() 
{ 
    // Initialize lists as empty 
    struct Node* head = NULL; 

    // Created linked list will be 11->2->56->12 
    push(&head, 12); 
    push(&head, 56); 
    push(&head, 2); 
    push(&head, 11); 

    cout << "Sum of Circular linked list is = " << sumOfList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to find the sum of 
// all nodes of a Circular linked list  
import java.util.*; 

class GFG 
{ 

// structure for a node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node  
// at the beginning of a  
// Circular linked list  
static Node push(Node head_ref,  
                      int data)  
{  
    Node ptr1 = new Node();  
    Node temp = head_ref;  
    ptr1.data = data;  
    ptr1.next = head_ref;  

    // If linked list is not null then  
    // set the next of last node  
    if (head_ref != null)  
    {  
        while (temp.next != head_ref)  
            temp = temp.next;  
        temp.next = ptr1;  
    }  
    else
        ptr1.next = ptr1; // For the first node  

    head_ref = ptr1;  

    return head_ref; 
}  

// Function to find sum of the  
// given Circular linked list  
static int sumOfList(Node head)  
{  
    Node temp = head;  
    int sum = 0;  
    if (head != null)  
    {  
        do 
        {  
            temp = temp.next;  
            sum += temp.data;  
        } while (temp != head);  
    }  

    return sum;  
}  

// Driver code  
public static void main(String args[]) 
{  
    // Initialize lists as empty  
    Node head = null;  

    // Created linked list will 
    // be 11.2.56.12  
    head = push(head, 12);  
    head = push(head, 56);  
    head = push(head, 2);  
    head = push(head, 11);  

    System.out.println("Sum of Circular linked" +  
                " list is = " + sumOfList(head));  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find the sum of all nodes  
# of a Circular linked list  
import math 

# class for a node 
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Function to insert a node at the beginning  
# of a Circular linked list  
def push(head, data): 
    if not head: 
        head = Node(data) 
        head.next = head 
        return head 
    lnode = head 

    # If linked list is not NULL then  
    # set the next of last node  
    while(lnode and lnode.next is not head): 
        lnode = lnode.next
    ptr1 = Node(data) # For the first node 
    ptr1.next = head 
    lnode.next = ptr1 
    head = ptr1 
    return head 

# Function to find sum of the given  
# Circular linked list      
def sumOfList(head): 
    temp = head 
    tsum = temp.data 
    temp = temp.next
    while(temp is not head): 
        tsum += temp.data 
        temp = temp.next
    return tsum 

# Driver code  
if __name__=='__main__': 

    # Initialize lists as empty 
    head = None

    # Created linked list will be 11->2->56->12  
    head = push(head, 12) 
    head = push(head, 56) 
    head = push(head, 2) 
    head = push(head, 11) 
    print("Sum of circular list is = {}" .  
                  format(sumOfList(head))) 

# This code is contributed by Vikash Kumar 37 

```

## C#

```cs

// C# program to find the sum of  
// all nodes of a Circular linked list  
using System; 

class GFG  
{  

    // structure for a node  
    class Node  
    {  
        public int data;  
        public Node next;  
    };  

    // Function to insert a node  
    // at the beginning of a  
    // Circular linked list  
    static Node push(Node head_ref,  
                        int data)  
    {  
        Node ptr1 = new Node();  
        Node temp = head_ref;  
        ptr1.data = data;  
        ptr1.next = head_ref;  

        // If linked list is not null then  
        // set the next of last node  
        if (head_ref != null)  
        {  
            while (temp.next != head_ref)  
                temp = temp.next;  
            temp.next = ptr1;  
        }  
        else
            ptr1.next = ptr1; // For the first node  

        head_ref = ptr1;  

        return head_ref;  
    }  

    // Function to find sum of the  
    // given Circular linked list  
    static int sumOfList(Node head)  
    {  
        Node temp = head;  
        int sum = 0;  
        if (head != null)  
        {  
            do
            {  
                temp = temp.next;  
                sum += temp.data;  
            } while (temp != head);  
        }  

        return sum;  
    }  

    // Driver code  
    public static void Main()  
    {  
        // Initialize lists as empty  
        Node head = null;  

        // Created linked list will  
        // be 11.2.56.12  
        head = push(head, 12);  
        head = push(head, 56);  
        head = push(head, 2);  
        head = push(head, 11);  

        Console.WriteLine("Sum of Circular linked" +  
                    " list is = " + sumOfList(head));  
    }  
} 

// This code is contributed by princiraj1992 

```

**Output:**

```
Sum of Circular linked list is = 81

```

**时间复杂度**：O（N），其中N是链​​表中节点的数量。
**辅助空间：** O（1）



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。