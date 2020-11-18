# 在链表

中查找模块化节点

给定一个单链列表和一个数字 k，找到最后一个节点，其 n％k == 0，其中 n 是列表中的节点数。

**示例：**

```
Input : list = 1->2->3->4->5->6->7
        k = 3
Output : 6

Input : list = 3->7->1->9->8
        k = 2
Output : 9

```

1.取得一个指针 moduleNode 并将其初始化为 NULL。 遍历链接列表。
2.对于每个 i％k = 0，更新 moduleNode。

## C++

```cpp

// C++ program to find modular node in a linked list 
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

/* Function to find modular node in the linked list */
Node* modularNode(Node* head, int k) 
{ 
    // Corner cases 
    if (k <= 0 || head == NULL) 
        return NULL;    

    // Traverse the given list 
    int i = 1; 
    Node* modularNode = NULL; 
    for (Node* temp = head; temp != NULL; temp = temp->next) { 
        if (i % k == 0)  
            modularNode = temp; 

        i++; 
    } 
    return modularNode; 
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
    Node* answer = modularNode(head, k); 
    printf("\nModular node is "); 
    if (answer != NULL)  
        printf("%d\n", answer->data); 
    else
        printf("null\n"); 
    return 0; 
} 

```

## Java

```java

// A Java program to find modular node in a linked list 
public class GFG 
{ 
    // A Linkedlist node 
    static class Node{ 
        int data; 
        Node next; 
        Node(int data){ 
            this.data = data; 
        } 
    } 

    // Function to find modular node in the linked list 
    static Node modularNode(Node head, int k) 
    { 
        // Corner cases 
        if (k <= 0 || head == null) 
            return null;    

        // Traverse the given list 
        int i = 1; 
        Node modularNode = null; 
        for (Node temp = head; temp != null; temp = temp.next) { 
            if (i % k == 0)  
                modularNode = temp; 

            i++; 
        } 
        return modularNode; 
    } 

    // Driver code to test above function 
    public static void main(String[] args)  
    { 
        Node head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(3); 
        head.next.next.next = new Node(4); 
        head.next.next.next.next = new Node(5); 
        int k = 2; 
        Node answer = modularNode(head, k); 
        System.out.print("Modular node is "); 
        if (answer != null)  
            System.out.println(answer.data); 
        else
            System.out.println("null"); 
    } 
} 
// This code is contributed by Sumit Ghosh 

```

## Python3

```py

# Python3 program to find modular node  
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

# Function to find modular node  
# in the linked list 
def modularNode(head, k): 

    # Corner cases 
    if (k <= 0 or head == None): 
        return None

    # Traverse the given list 
    i = 1
    modularNode = None
    temp = head 
    while (temp != None): 
        if (i % k == 0): 
            modularNode = temp 

        i = i + 1
        temp = temp.next
    return modularNode 

# Driver Code 
if __name__ == '__main__': 
    head = newNode(1) 
    head.next = newNode(2) 
    head.next.next = newNode(3) 
    head.next.next.next = newNode(4) 
    head.next.next.next.next = newNode(5) 
    k = 2
    answer = modularNode(head, k) 
    print("Modular node is", end = ' ') 
    if (answer != None): 
        print(answer.data, end = ' ') 
    else: 
        print("None") 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to find modular node in a linked list 
using System; 

class GFG  
{  
    // A Linkedlist node  
    public class Node 
    {  
        public int data;  
        public Node next;  
        public Node(int data) 
        {  
            this.data = data;  
        }  
    }  

    // Function to find modular node in the linked list  
    static Node modularNode(Node head, int k)  
    {  
        // Corner cases  
        if (k <= 0 || head == null)  
            return null;  

        // Traverse the given list  
        int i = 1;  
        Node modularNode = null;  
        for (Node temp = head; temp != null; temp = temp.next) 
        {  
            if (i % k == 0)  
                modularNode = temp;  

            i++;  
        }  
        return modularNode;  
    }  

    // Driver code   
    public static void Main(String[] args)  
    {  
        Node head = new Node(1);  
        head.next = new Node(2);  
        head.next.next = new Node(3);  
        head.next.next.next = new Node(4);  
        head.next.next.next.next = new Node(5);  
        int k = 2;  

        Node answer = modularNode(head, k);  
        Console.Write("Modular node is ");  

        if (answer != null)  
            Console.WriteLine(answer.data);  
        else
            Console.WriteLine("null");  
    }  
}  

// This code is contibuted by Rajput-JI 

```

**Output:**

```
Modular node is 4

```

本文由 **Prakriti Gupta** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

