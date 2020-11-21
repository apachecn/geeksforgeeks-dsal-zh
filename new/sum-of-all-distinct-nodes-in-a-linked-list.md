# 链表

> 原文：[https://www.geeksforgeeks.org/sum-of-all-distinct-nodes-in-a-linked-list/](https://www.geeksforgeeks.org/sum-of-all-distinct-nodes-in-a-linked-list/)

中所有不同节点的总和

给定一个链表，它可能包含重复的节点。 任务是找到非重复节点的总和。

**示例**：

> **输入**：1-> 2-> 1-> 3-> 4-> 3->空
> **输出**：6
> 2 和 4 是唯一的非重复节点，并且 2 + 4 = 6。
> 
> **输入**：1-> 3-> 1-> 3-> 1-> 3->空
> **输出**：0

**方法**：我们遍历整个链表，并针对每个节点检查整个链表，该节点是否重复。 如果没有重复的节点，那么我们将该节点添加到存储总和的变量中。

下面是上述方法的实现：

## C++

```cpp

// C++ implementaion of the approach 
#include <iostream> 
using namespace std; 

// Represents a node of linked list 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert node in a linked list 
void insert(Node** head, int item) 
{ 
    Node* ptr = *head; 
    Node* temp = new Node; 

    temp->data = item; 
    temp->next = NULL; 

    if (*head == NULL) 
        *head = temp; 
    else { 
        while (ptr->next != NULL) 
            ptr = ptr->next; 
        ptr->next = temp; 
    } 
} 

// Function to find the sum of non duplicate nodes 
int sumOfNonDupNode(Node* head) 
{ 
    Node* ptr1 = head; 
    Node* ptr2; 
    int sum = 0, flag = 0; 

    while (ptr1 != NULL) { 
        ptr2 = head; 
        bool flag = false; 

        // Check if current node has some duplicate 
        while (ptr2 != NULL) { 

            // Check for duplicate node 
            if (ptr1 != ptr2 && ptr1->data == ptr2->data) { 
                flag = true; 
                break; 
            } 

            // Get to the next node 
            ptr2 = ptr2->next; 
        } 

        // If current node is unique 
        if (!flag) 
            sum += ptr1->data; 

        // Get to the next node 
        ptr1 = ptr1->next; 
    } 
    return sum; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 

    insert(&head, 1); 
    insert(&head, 2); 
    insert(&head, 1); 
    insert(&head, 3); 
    insert(&head, 4); 
    insert(&head, 3); 

    cout << sumOfNonDupNode(head) << endl; 

    return 0; 
} 

```

## Java

```java

// Java implementaion of the approach 
class GFG { 

    // Represents a node of linked list 
    static class Node { 
        int data; 
        Node next; 
    } 

    // Function to insert node in a linked list 
    static Node insert(Node head, int item) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 

        temp.data = item; 
        temp.next = null; 

        if (head == null) 
            head = temp; 
        else { 
            while (ptr.next != null) 
                ptr = ptr.next; 
            ptr.next = temp; 
        } 
        return head; 
    } 

    // Function to find the sum of non duplicate nodes 
    static int sumOfNonDupNode(Node head) 
    { 
        Node ptr1 = head; 
        Node ptr2; 
        int sum = 0; 

        while (ptr1 != null) { 
            ptr2 = head; 
            boolean flag = false; 

            // Check if current node has some duplicate 
            while (ptr2 != null) { 

                // Check for duplicate node 
                if (ptr1 != ptr2 && ptr1.data == ptr2.data) { 
                    flag = true; 
                    break; 
                } 

                // Get to the next node 
                ptr2 = ptr2.next; 
            } 

            // If current node is unique 
            if (!flag) 
                sum += ptr1.data; 

            // Get to the next node 
            ptr1 = ptr1.next; 
        } 
        return sum; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        Node head = null; 

        head = insert(head, 1); 
        head = insert(head, 2); 
        head = insert(head, 1); 
        head = insert(head, 3); 
        head = insert(head, 4); 
        head = insert(head, 3); 

        System.out.print(sumOfNonDupNode(head)); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 

# Represents node of the linked list 
class Node: 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# Insertion in linked list 
def insert(head, item): 

    ptr = head 
    temp = Node(item) 

    if head == None: 
        head = temp 
    else: 
        while ptr.next != None: 
            ptr = ptr.next

        ptr.next = temp 

    return head 

# Function to find the sum of  
# non duplicate nodes 
def sumOfNonDupNode(head): 

    ptr1 = head 
    Sum = flag = 0

    while ptr1 != None: 
        ptr2, flag = head, False

        # Check if current node  
        # has some duplicate 
        while ptr2 != None: 

            # Check for duplicate node 
            if (ptr1 != ptr2 and 
                ptr1.data == ptr2.data):  
                flag = True
                break

            # Get to the next node 
            ptr2 = ptr2.next

        # If current node is unique 
        if not flag: 
            Sum += ptr1.data 

        # Get to the next node 
        ptr1 = ptr1.next

    return Sum

# Driver code 
if __name__ == "__main__": 

    head = None

    head = insert(head, 1) 
    head = insert(head, 2) 
    head = insert(head, 1) 
    head = insert(head, 3) 
    head = insert(head, 4) 
    head = insert(head, 3) 

    print(sumOfNonDupNode(head)) 

# This code is contributed by Rituraj Jain 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG { 

    public class Node { 
        public int data; 
        public Node next; 
    } 

    // Function to insert node in a linked list 
    static Node insert(Node head, int item) 
    { 
        Node ptr = head; 
        Node temp = new Node(); 

        temp.data = item; 
        temp.next = null; 

        if (head == null) 
            head = temp; 
        else { 
            while (ptr.next != null) 
                ptr = ptr.next; 
            ptr.next = temp; 
        } 
        return head; 
    } 

    // Function to find the sum of non duplicate nodes 
    static int sumOfNonDupNode(Node head) 
    { 
        Node ptr1 = head; 
        Node ptr2; 
        int sum = 0; 

        while (ptr1 != null) { 
            ptr2 = head; 
            bool flag = false; 

            // Check if current node has some duplicate 
            while (ptr2 != null) { 

                // Check for duplicate node 
                if (ptr1 != ptr2 && ptr1.data == ptr2.data) { 
                    flag = true; 
                    break; 
                } 

                // Get to the next node 
                ptr2 = ptr2.next; 
            } 

            // If current node is unique 
            if (!flag) 
                sum += ptr1.data; 

            // Get to the next node 
            ptr1 = ptr1.next; 
        } 
        return sum; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head = null; 

        head = insert(head, 1); 
        head = insert(head, 2); 
        head = insert(head, 1); 
        head = insert(head, 3); 
        head = insert(head, 4); 
        head = insert(head, 3); 

        Console.Write(sumOfNonDupNode(head)); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**输出**：

```
6

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。