# 反向循环链接列表

给定大小为 **n** 的循环链表。 问题是通过更改节点之间的链接来反转给定的循环链接列表。

**示例：**
**输入：**
![INPUT:](img/2c869a227a799ea7a302020b01e3fd9b.png)

**输出：**
![OUTPUT:](img/5d99f7959d7e56b765c139b037f23775.png)

**方法：**该方法与[反转单个链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)中的方法相同。 只有在这里，我们才需要通过将反向列表的最后一个节点链接到第一个节点来进行更多调整。

## C ++

```

// C++ implementation to reverse 
// a circular linked list 
#include <bits/stdc++.h> 

using namespace std; 

// Linked list node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate memory for node 
    Node* newNode = new Node; 

    // put in the data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to reverse the circular linked list 
void reverse(Node** head_ref) 
{ 
    // if list is empty 
    if (*head_ref == NULL) 
        return; 

    // reverse procedure same as reversing a 
    // singly linked list 
    Node* prev = NULL; 
    Node* current = *head_ref; 
    Node* next; 
    do { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } while (current != (*head_ref)); 

    // adjutsing the links so as to make the 
    // last node point to the first node 
    (*head_ref)->next = prev; 
    *head_ref = prev; 
} 

// Function to print circular linked list 
void printList(Node* head) 
{ 
    if (head == NULL) 
        return; 

    Node* temp = head; 
    do { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } while (temp != head); 
} 

// Driver program to test above 
int main() 
{ 
    // Create a circular linked list 
    // 1->2->3->4->1 
    Node* head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(3); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = head; 

    cout << "Given circular linked list: "; 
    printList(head); 

    reverse(&head); 

    cout << "\nReversed circular linked list: "; 
    printList(head); 

    return 0; 
} 

```

## 爪哇

```

// Java implementation to reverse  
// a circular linked list  
class GFG 
{ 

// Linked list node  
static class Node 
{  
    int data;  
    Node next;  
};  

// function to get a new node  
static Node getNode(int data)  
{  
    // allocate memory for node  
    Node newNode = new Node();  

    // put in the data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

// Function to reverse the circular linked list  
static Node reverse(Node head_ref)  
{  
    // if list is empty  
    if (head_ref == null)  
        return null;  

    // reverse procedure same as reversing a  
    // singly linked list  
    Node prev = null;  
    Node current = head_ref;  
    Node next;  
    do 
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
    } while (current != (head_ref));  

    // adjutsing the links so as to make the  
    // last node point to the first node  
    (head_ref).next = prev;  
    head_ref = prev;  
    return head_ref; 
}  

// Function to print circular linked list  
static void printList(Node head)  
{  
    if (head == null)  
        return;  

    Node temp = head;  
    do
    {  
        System.out.print( temp.data + " ");  
        temp = temp.next;  
    } while (temp != head);  
}  

// Driver code  
public static void main(String args[]) 
{  
    // Create a circular linked list  
    // 1.2.3.4.1  
    Node head = getNode(1);  
    head.next = getNode(2);  
    head.next.next = getNode(3);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = head;  

    System.out.print("Given circular linked list: ");  
    printList(head);  

    head = reverse(head);  

    System.out.print("\nReversed circular linked list: ");  
    printList(head);  

}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 implementation to reverse 
# a circular linked list 
import math 

# Linked list node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function to get a new node 
def getNode(data): 

    # allocate memory for node 
    newNode = Node(data) 

    # put in the data 
    newNode.data = data 
    newNode.next = None
    return newNode 

# Function to reverse the  
# circular linked list 
def reverse(head_ref): 

    # if list is empty 
    if (head_ref == None): 
        return None

    # reverse procedure same as  
    # reversing a singly linked list 
    prev = None
    current = head_ref 

    next = current.next
    current.next = prev 
    prev = current 
    current = next
    while (current != head_ref): 
        next = current.next
        current.next = prev 
        prev = current 
        current = next

    # adjutsing the links so as to make the 
    # last node po to the first node 
    head_ref.next = prev 
    head_ref = prev 
    return head_ref 

# Function to print circular linked list 
def prList(head): 
    if (head == None): 
        return

    temp = head 

    print(temp.data, end = " ") 
    temp = temp.next
    while (temp != head): 
        print(temp.data, end = " ") 
        temp = temp.next

# Driver Code 
if __name__=='__main__':  

    # Create a circular linked list 
    # 1.2.3.4.1 
    head = getNode(1) 
    head.next = getNode(2) 
    head.next.next = getNode(3) 
    head.next.next.next = getNode(4) 
    head.next.next.next.next = head 

    print("Given circular linked list: ",  
                                end = "") 
    prList(head) 

    head = reverse(head) 

    print("\nReversed circular linked list: ",  
                                     end = "") 
    prList(head) 

# This code is contributed by Srathore 

```

## C＃

```

// C# implementation to reverse  
// a circular linked list  
using System; 

class GFG  
{  

    // Linked list node  
    public class Node  
    {  
        public int data;  
        public Node next;  
    };  

    // function to get a new node  
    static Node getNode(int data)  
    {  
        // allocate memory for node  
        Node newNode = new Node();  

        // put in the data  
        newNode.data = data;  
        newNode.next = null;  
        return newNode;  
    }  

    // Function to reverse the circular linked list  
    static Node reverse(Node head_ref)  
    {  
        // if list is empty  
        if (head_ref == null)  
            return null;  

        // reverse procedure same as reversing a  
        // singly linked list  
        Node prev = null;  
        Node current = head_ref;  
        Node next;  
        do
        {  
            next = current.next;  
            current.next = prev;  
            prev = current;  
            current = next;  
        } while (current != (head_ref));  

        // adjutsing the links so as to make the  
        // last node point to the first node  
        (head_ref).next = prev;  
        head_ref = prev;  
        return head_ref;  
    }  

    // Function to print circular linked list  
    static void printList(Node head)  
    {  
        if (head == null)  
            return;  

        Node temp = head;  
        do
        {  
            Console.Write( temp.data + " ");  
            temp = temp.next;  
        } while (temp != head);  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
        // Create a circular linked list  
        // 1.2.3.4.1  
        Node head = getNode(1);  
        head.next = getNode(2);  
        head.next.next = getNode(3);  
        head.next.next.next = getNode(4);  
        head.next.next.next.next = head;  

        Console.Write("Given circular linked list: ");  
        printList(head);  

        head = reverse(head);  

        Console.Write("\nReversed circular linked list: ");  
        printList(head);  

    }  
}  

// This code contributed by Rajput-Ji 

```

**Output:**

```
Given circular linked list: 1 2 3 4
Reversed circular linked list: 4 3 2 1

```

**时间复杂度：** O（n）

本文由 [**Ayush Jauhari**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 贡献。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。