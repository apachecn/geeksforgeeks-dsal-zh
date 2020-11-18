# 从中间到链表

的开头查找第k个节点

给定链接列表和数字K。任务是从列表的中间到开头打印第K个节点的值。 如果不存在这样的元素，则打印“ -1”。

**注意**：中间节点的位置是：（n / 2）+1，其中n是列表中节点的总数。

**范例**：

```
Input :  List is 1->2->3->4->5->6->7
         K= 2 
Output : 2

Input :  list is 7->8->9->10->11->12
         K = 3
Output : 7

```

从头到尾遍历列表并计算节点总数。 现在，假设![n](img/42ce0a847b20a2f8a781c8a50bdab975.png "Rendered by QuickLaTeX.com")是列表中的节点总数。 因此，中间节点将位于位置（n / 2）+1。 现在，剩下的任务是从列表的开头打印位于[（n / 2 +1-k）位置的节点。](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)

以下是上述想法的实现：

## C ++

```

// CPP program to find kth node from middle 
// towards Head of the Linked List 

#include <bits/stdc++.h> 

using namespace std; 

// Linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to   
   pointer) to the head of a list  
   and an int, push a new node on  
   the front of the list. */
void push(struct Node** head_ref, 
          int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to count number of nodes 
int getCount(struct Node* head) 
{ 
    int count = 0; // Initialize count 
    struct Node* current = head; // Initialize current 
    while (current != NULL) { 
        count++; 
        current = current->next; 
    } 
    return count; 
} 

// Function to get the kth node from the mid 
// towards begin of the linked list 
int printKthfrommid(struct Node* head_ref, int k) 
{ 
    // Get the count of total number of 
    // nodes in the linked list 
    int n = getCount(head_ref); 

    int reqNode = ((n / 2 + 1) - k); 

    // If no such node exists, return -1 
    if (reqNode <= 0) { 
        return -1; 
    } 

    // Find node at position reqNode 
    else { 
        struct Node* current = head_ref; 

        // the index of the 
        // node we're currently 
        // looking at 
        int count = 1; 
        while (current != NULL) { 
            if (count == reqNode) 
                return (current->data); 
            count++; 
            current = current->next; 
        } 
    } 
} 

// Driver code 
int main() 
{ 
    // start with empty list 
    struct Node* head = NULL; 
    int k = 2; 

    // create linked list 
    // 1->2->3->4->5->6->7 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    cout << printKthfrommid(head, 2); 

    return 0; 
} 

```

## 爪哇

```

// Java program to find Kth node from mid 
// of a linked list in single traversal 

// Linked list node 
class Node 
{ 
    int data; 
    Node next; 
    Node(int d) 
    { 
        this.data = d; 
        this.next = null; 
    } 
} 

class LinkedList 
{ 
    Node start; 
    LinkedList() 
    { 
        start = null; 
    } 

    // Function to push node at head 
    public void push(int data) 
    {  
        if(this.start == null) 
        { 
            Node temp = new Node(data); 
            this.start = temp; 
        } 
        else
        { 
            Node temp = new Node(data); 
            temp.next = this.start; 
            this.start = temp; 
        } 
    } 

    //method to get the count of node 
    public int getCount(Node start) 
    { 
        Node temp = start; 
        int cnt = 0; 
        while(temp != null) 
        { 
            temp = temp.next; 
            cnt++; 
        } 
        return cnt; 
    } 

    // Function to get the kth node from the mid 
    // towards begin of the linked list 
    public int printKthfromid(Node start, int k) 
    {  
        // Get the count of total number of 
        // nodes in the linked list 
        int n = getCount(start); 
        int reqNode = ((n + 1) / 2) - k; 

        // If no such node exists, return -1 
        if(reqNode <= 0) 
            return -1; 
        else
        { 
            Node current = start; 
            int count = 1,ans = 0; 
            while (current != null)  
            {  
                if (count == reqNode)  
                { 
                    ans = current.data; 
                    break;  
                } 
                count++;  
                current = current.next;  
            } 
            return ans; 
        } 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
    // create linked list 
        // 1->2->3->4->5->6->7  
    LinkedList ll = new LinkedList(); 
        ll.push(7); 
        ll.push(6); 
        ll.push(5); 
        ll.push(4); 
        ll.push(3); 
        ll.push(2); 
        ll.push(1); 
        System.out.println(ll.printKthfromid(ll.start, 2)); 
    } 
} 

// This Code is contributed by Adarsh_Verma 

```

## Python3

```

# Python3 program to find kth node from  
# middle towards Head of the Linked List 

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to insert a node at the  
# beginning of the linked list  
def push(head, data):  
    if not head:  

        # Return new node  
        return Node(data)  

    # allocate node  
    new_node = Node(data)  

    # link the old list to the new node  
    new_node.next = head  

    # move the head to point 
    # to the new node  
    head = new_node  
    return head  

# Function to count number of nodes 
def getCount(head): 

    count = 0 # Initialize count 
    current = head # Initialize current 
    while (current ):  
        count = count + 1
        current = current.next

    return count 

# Function to get the kth node from the mid 
# towards begin of the linked list 
def printKthfrommid(head_ref, k): 

    # Get the count of total number of 
    # nodes in the linked list 
    n = getCount(head_ref) 

    reqNode = int((n / 2 + 1) - k) 

    # If no such node exists, return -1 
    if (reqNode <= 0) : 
        return -1

    # Find node at position reqNode 
    else : 
        current = head_ref 

        # the index of the 
        # node we're currently 
        # looking at 
        count = 1
        while (current) : 
            if (count == reqNode): 
                return (current.data) 
            count = count + 1
            current = current.next

# Driver Code  
if __name__=='__main__':  

    # start with empty list 
    head = None
    k = 2

    # create linked list 
    # 1.2.3.4.5.6.7 
    head = push(head, 7) 
    head = push(head, 6) 
    head = push(head, 5) 
    head = push(head, 4) 
    head = push(head, 3) 
    head = push(head, 2) 
    head = push(head, 1) 

    print(printKthfrommid(head, 2)) 

# This code is contributed by Arnab Kundu 

```

## C＃

```

// C# program to find Kth node from mid 
// of a linked list in single traversal 
using System; 

// Linked list node 
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int d) 
    { 
        this.data = d; 
        this.next = null; 
    } 
} 

public class LinkedList 
{ 
    Node start; 
    LinkedList() 
    { 
        start = null; 
    } 

    // Function to push node at head 
    public void push(int data) 
    {  
        if(this.start == null) 
        { 
            Node temp = new Node(data); 
            this.start = temp; 
        } 
        else
        { 
            Node temp = new Node(data); 
            temp.next = this.start; 
            this.start = temp; 
        } 
    } 

    //method to get the count of node 
    public int getCount(Node start) 
    { 
        Node temp = start; 
        int cnt = 0; 
        while(temp != null) 
        { 
            temp = temp.next; 
            cnt++; 
        } 
        return cnt; 
    } 

    // Function to get the kth node from the mid 
    // towards begin of the linked list 
    public int printKthfromid(Node start, int k) 
    {  
        // Get the count of total number of 
        // nodes in the linked list 
        int n = getCount(start); 
        int reqNode = ((n + 1) / 2) - k; 

        // If no such node exists, return -1 
        if(reqNode <= 0) 
            return -1; 
        else
        { 
            Node current = start; 
            int count = 1,ans = 0; 
            while (current != null)  
            {  
                if (count == reqNode)  
                { 
                    ans = current.data; 
                    break;  
                } 
                count++;  
                current = current.next;  
            } 
            return ans; 
        } 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        // create linked list 
        // 1->2->3->4->5->6->7  
        LinkedList ll = new LinkedList(); 
        ll.push(7); 
        ll.push(6); 
        ll.push(5); 
        ll.push(4); 
        ll.push(3); 
        ll.push(2); 
        ll.push(1); 
        Console.WriteLine(ll.printKthfromid(ll.start, 2)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
2

```

**时间复杂度**：O（n），其中n是列表的长度。
**辅助空间**：O（1）

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。