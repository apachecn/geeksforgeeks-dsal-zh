# 从循环链表

中删除每个第 K 个节点

从循环链接列表中删除每个第 k 个节点，直到只剩下一个节点。 同时打印中间列表。

**示例**：

```
Input : n=4, k=2, list = 1->2->3->4
Output : 
1->2->3->4->1
1->2->4->1
2->4->2
2->2

Input : n=9, k=4, list = 1->2->3->4->5->6->7->8->9
Output :
1->2->3->4->5->6->7->8->9->1
1->2->3->4->6->7->8->9->1
1->2->3->4->6->7->8->1
1->2->3->6->7->8->1
2->3->6->7->8->2
2->3->6->8->2
2->3->8->2
2->3->2
2->2

```

**算法**

重复以下步骤，直到列表中仅剩一个节点。

**情况 1** ：列表为空。

如果列表为空，只需返回即可。

**情况 2** ：列表只有一个节点。

如果列表仅剩一个节点，我们将打印列表并在达到目标时返回。

**情况 3** ：列表具有多个节点。

定义两个指针 curr 和 prev 并使用头节点初始化指针 curr。

使用 curr 指针遍历列表 k 次，遍历列表。

*   要删除的节点是列表的第一个节点。

    要检查的条件（当前==头& &当前->接下来==头）。

    如果是，则向前移动直到到达最后一个节点。 prev 到达最后一个节点后，将 head = head-next->设置为 prev-> next = head。 删除 curr。

*   要删除的节点是列表中的最后一个节点。

    要检查的条件是（当前->下一个==头）。

    如果 curr 是最后一个节点。 设置 prev-> next = head 并通过 free（curr）删除节点 curr。

*   要删除的节点既不是第一个节点，也不是最后一个节点，然后设置 prev-> next = temp-> next 并删除 curr。

## C++

```cpp

// C++ program to delete every kth Node from 
// circular linked list. 
#include <bits/stdc++.h> 
using namespace std; 

/* structure for a Node */
struct Node { 
    int data; 
    Node* next; 
    Node(int x) 
    { 
        data = x; 
        next = NULL; 
    } 
}; 

/*Utility function to print the circular linked list*/
void printList(Node* head) 
{ 
    if (head == NULL) 
        return; 
    Node* temp = head; 
    do { 
        cout << temp->data << "->"; 
        temp = temp->next; 
    } while (temp != head); 
    cout << head->data << endl; 
} 

/*Function to delete every kth Node*/
void deleteK(Node** head_ref, int k) 
{ 
    Node* head = *head_ref; 

    // If list is empty, simply return. 
    if (head == NULL) 
        return; 

    // take two pointers - current and previous 
    Node *curr = head, *prev; 
    while (true) { 

        // Check if Node is the only Node\ 
        // If yes, we reached the goal, therefore  
        // return. 
        if (curr->next == head && curr == head) 
            break; 

        // Print intermediate list. 
        printList(head); 

        // If more than one Node present in the list, 
        // Make previous pointer point to current 
        // Iterate current pointer k times, 
        // i.e. current Node is to be deleted. 
        for (int i = 0; i < k; i++) { 
            prev = curr; 
            curr = curr->next; 
        } 

        // If Node to be deleted is head 
        if (curr == head) { 
            prev = head; 
            while (prev->next != head) 
                prev = prev->next; 
            head = curr->next; 
            prev->next = head; 
            *head_ref = head; 
            free(curr); 
        } 

        // If Node to be deleted is last Node. 
        else if (curr->next == head) { 
            prev->next = head; 
            free(curr); 
        } 
        else { 
            prev->next = curr->next; 
            free(curr); 
        } 
    } 
} 

/* Function to insert a Node at the end of  
a Circular linked list */
void insertNode(Node** head_ref, int x) 
{ 
    // Create a new Node 
    Node* head = *head_ref; 
    Node* temp = new Node(x); 

    // if the list is empty, make the new Node head 
    // Also, it will point to itself. 
    if (head == NULL) { 
        temp->next = temp; 
        *head_ref = temp; 
    } 

    // traverse the list to reach the last Node  
    // and insert the Node 
    else { 
        Node* temp1 = head; 
        while (temp1->next != head) 
            temp1 = temp1->next; 
        temp1->next = temp; 
        temp->next = head; 
    } 
} 

/* Driver program to test above functions */
int main() 
{ 
    // insert Nodes in the circular linked list 
    struct Node* head = NULL; 
    insertNode(&head, 1); 
    insertNode(&head, 2); 
    insertNode(&head, 3); 
    insertNode(&head, 4); 
    insertNode(&head, 5); 
    insertNode(&head, 6); 
    insertNode(&head, 7); 
    insertNode(&head, 8); 
    insertNode(&head, 9); 

    int k = 4; 

    // Delete every kth Node from the 
    // circular linked list. 
    deleteK(&head, k); 

    return 0; 
} 

```

## Java

```java

// Java program to delete every kth Node from  
// circular linked list.  
class GFG 
{ 

/* structure for a Node */
static class Node 
{  
    int data;  
    Node next;  
    Node(int x)  
    {  
        data = x;  
        next = null;  
    }  
};  

/*Utility function to print  
the circular linked list*/
static void printList(Node head)  
{  
    if (head == null)  
        return;  
    Node temp = head;  
    do 
    {  
        System.out.print( temp.data + "->");  
        temp = temp.next;  
    }  
    while (temp != head);  
    System.out.println(head.data );  
}  

/*Function to delete every kth Node*/
static Node deleteK(Node head_ref, int k)  
{  
    Node head = head_ref;  

    // If list is empty, simply return.  
    if (head == null)  
        return null;  

    // take two pointers - current and previous  
    Node curr = head, prev=null;  
    while (true)  
    {  

        // Check if Node is the only Node\  
        // If yes, we reached the goal, therefore  
        // return.  
        if (curr.next == head && curr == head)  
            break;  

        // Print intermediate list.  
        printList(head);  

        // If more than one Node present in the list,  
        // Make previous pointer point to current  
        // Iterate current pointer k times,  
        // i.e. current Node is to be deleted.  
        for (int i = 0; i < k; i++)  
        {  
            prev = curr;  
            curr = curr.next;  
        }  

        // If Node to be deleted is head  
        if (curr == head)  
        {  
            prev = head;  
            while (prev.next != head)  
                prev = prev.next;  
            head = curr.next;  
            prev.next = head;  
            head_ref = head;  
        }  

        // If Node to be deleted is last Node.  
        else if (curr.next == head)  
        {  
            prev.next = head;  
        }  
        else
        {  
            prev.next = curr.next;  
        }  
    }  
    return head; 
}  

/* Function to insert a Node at the end of  
a Circular linked list */
static Node insertNode(Node head_ref, int x)  
{  
    // Create a new Node  
    Node head = head_ref;  
    Node temp = new Node(x);  

    // if the list is empty, make the new Node head  
    // Also, it will point to itself.  
    if (head == null)  
    {  
        temp.next = temp;  
        head_ref = temp;  
        return head_ref; 
    }  

    // traverse the list to reach the last Node  
    // and insert the Node  
    else 
    {  
        Node temp1 = head;  
        while (temp1.next != head)  
            temp1 = temp1.next;  
        temp1.next = temp;  
        temp.next = head;  
    }  
    return head; 
}  

/* Driver code */
public static void main(String args[]) 
{  
    // insert Nodes in the circular linked list  
    Node head = null;  
    head = insertNode(head, 1);  
    head = insertNode(head, 2);  
    head = insertNode(head, 3);  
    head = insertNode(head, 4);  
    head = insertNode(head, 5);  
    head = insertNode(head, 6);  
    head = insertNode(head, 7);  
    head = insertNode(head, 8);  
    head = insertNode(head, 9);  

    int k = 4;  

    // Delete every kth Node from the  
    // circular linked list.  
    head = deleteK(head, k);  
}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to delete every kth Node from 
# circular linked list. 
import math 

# structure for a Node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Utility function to print the circular linked list 
def prList(head): 
    if (head == None): 
        return
    temp = head 

    print(temp.data, end = "->") 
    temp = temp.next
    while (temp != head): 
        print(temp.data, end = "->") 
        temp = temp.next
    print(head.data) 

# Function to delete every kth Node 
def deleteK(head_ref, k): 
    head = head_ref 

    # If list is empty, simply return. 
    if (head == None): 
        return

    # take two poers - current and previous 
    curr = head 
    prev = None
    while True: 

        # Check if Node is the only Node\ 
        # If yes, we reached the goal, therefore  
        # return. 
        if (curr.next == head and curr == head): 
            break

        # Pr intermediate list. 
        prList(head) 

        # If more than one Node present in the list, 
        # Make previous pointer po to current 
        # Iterate current pointer k times, 
        # i.e. current Node is to be deleted. 
        for i in range(k): 
            prev = curr 
            curr = curr.next

        # If Node to be deleted is head 
        if (curr == head): 
            prev = head 
            while (prev.next != head): 
                prev = prev.next
            head = curr.next
            prev.next = head 
            head_ref = head 

        # If Node to be deleted is last Node. 
        elif (curr.next == head) : 
            prev.next = head 

        else : 
            prev.next = curr.next

# Function to insert a Node at the end of  
#a Circular linked list  
def insertNode(head_ref, x): 

    # Create a new Node 
    head = head_ref 
    temp = Node(x) 

    # if the list is empty, make the new Node head 
    # Also, it will po to itself. 
    if (head == None): 
        temp.next = temp 
        head_ref = temp 
        return head_ref 

    # traverse the list to reach the last Node  
    # and insert the Node 
    else : 
        temp1 = head 
        while (temp1.next != head): 
            temp1 = temp1.next
        temp1.next = temp 
        temp.next = head 
    return head 

# Driver Code 
if __name__=='__main__': 

    # insert Nodes in the circular linked list 
    head = None
    head = insertNode(head, 1)  
    head = insertNode(head, 2)  
    head = insertNode(head, 3)  
    head = insertNode(head, 4)  
    head = insertNode(head, 5)  
    head = insertNode(head, 6)  
    head = insertNode(head, 7)  
    head = insertNode(head, 8)  
    head = insertNode(head, 9)  

    k = 4

    # Delete every kth Node from the 
    # circular linked list. 
    deleteK(head, k) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to delete every kth Node from  
// circular linked list. 
using System; 

class GFG 
{ 

/* structure for a Node */
public class Node 
{  
    public int data;  
    public Node next;  
    public Node(int x)  
    {  
        data = x;  
        next = null;  
    }  
};  

/*Utility function to print  
the circular linked list*/
static void printList(Node head)  
{  
    if (head == null)  
        return;  
    Node temp = head;  
    do
    {  
        Console.Write( temp.data + "->");  
        temp = temp.next;  
    }  
    while (temp != head);  
    Console.WriteLine(head.data );  
}  

/*Function to delete every kth Node*/
static Node deleteK(Node head_ref, int k)  
{  
    Node head = head_ref;  

    // If list is empty, simply return.  
    if (head == null)  
        return null;  

    // take two pointers - current and previous  
    Node curr = head, prev = null;  
    while (true)  
    {  

        // Check if Node is the only Node\  
        // If yes, we reached the goal, therefore  
        // return.  
        if (curr.next == head && curr == head)  
            break;  

        // Print intermediate list.  
        printList(head);  

        // If more than one Node present in the list,  
        // Make previous pointer point to current  
        // Iterate current pointer k times,  
        // i.e. current Node is to be deleted.  
        for (int i = 0; i < k; i++)  
        {  
            prev = curr;  
            curr = curr.next;  
        }  

        // If Node to be deleted is head  
        if (curr == head)  
        {  
            prev = head;  
            while (prev.next != head)  
                prev = prev.next;  
            head = curr.next;  
            prev.next = head;  
            head_ref = head;  
        }  

        // If Node to be deleted is last Node.  
        else if (curr.next == head)  
        {  
            prev.next = head;  
        }  
        else
        {  
            prev.next = curr.next;  
        }  
    }  
    return head; 
}  

/* Function to insert a Node at the end of  
a Circular linked list */
static Node insertNode(Node head_ref, int x)  
{  
    // Create a new Node  
    Node head = head_ref;  
    Node temp = new Node(x);  

    // if the list is empty, make the new Node head  
    // Also, it will point to itself.  
    if (head == null)  
    {  
        temp.next = temp;  
        head_ref = temp;  
        return head_ref; 
    }  

    // traverse the list to reach the last Node  
    // and insert the Node  
    else
    {  
        Node temp1 = head;  
        while (temp1.next != head)  
            temp1 = temp1.next;  
        temp1.next = temp;  
        temp.next = head;  
    }  
    return head; 
}  

/* Driver code */
public static void Main(String []args) 
{  
    // insert Nodes in the circular linked list  
    Node head = null;  
    head = insertNode(head, 1);  
    head = insertNode(head, 2);  
    head = insertNode(head, 3);  
    head = insertNode(head, 4);  
    head = insertNode(head, 5);  
    head = insertNode(head, 6);  
    head = insertNode(head, 7);  
    head = insertNode(head, 8);  
    head = insertNode(head, 9);  

    int k = 4;  

    // Delete every kth Node from the  
    // circular linked list.  
    head = deleteK(head, k);  
}  
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
1->2->3->4->5->6->7->8->9->1
1->2->3->4->6->7->8->9->1
1->2->3->4->6->7->8->1
1->2->3->6->7->8->1
2->3->6->7->8->2
2->3->6->8->2
2->3->8->2
2->3->2
2->2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。