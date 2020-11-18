# 在单遍历中查找链表的倒数第二个节点

给定一个链表。 任务是仅使用单个遍历查找链表的倒数第二个节点。

**示例**：

> **输入**：列表= 1-> 2-> 3-> 4-> 5->空
> **输出**：4
> 
> **输入**：列表= 2-> 4-> 6-> 8-> 33-> 67->空
> **输出**：33

想法是按照以下方法遍历链表：

1.  如果列表为空或包含少于 2 个元素，则返回 false。

2.  否则，请检查当前节点是否为链表的倒数第二个节点。 也就是说，**如果（current_node- > next-next == NULL）**，则当前节点为倒数第二个节点。

3.  如果当前节点是倒数第二个节点，请打印该节点，否则移至下一个节点。

4.  重复上述两个步骤，直到到达倒数第二个节点。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the second last node 
// of a linked list in single traversal 

#include <iostream> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to find the second last 
// node of the linked list 
int findSecondLastNode(struct Node* head) 
{ 
    struct Node* temp = head; 

    // If the list is empty or contains less 
    // than 2 nodes 
    if (temp == NULL || temp->next == NULL) 
        return -1; 

    // Traverse the linked list 
    while (temp != NULL) { 

        // Check if the current node  is the 
        // second last node or not 
        if (temp->next->next == NULL) 
            return temp->data; 

        // If not then move to the next node 
        temp = temp->next; 
    } 
} 

// Function to push node at head 
void push(struct Node** head_ref, int new_data) 
{ 
    Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver code 
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() function to construct  
    the below list 8 -> 23 -> 11 -> 29 -> 12 */
    push(&head, 12); 
    push(&head, 29); 
    push(&head, 11); 
    push(&head, 23); 
    push(&head, 8); 

    cout << findSecondLastNode(head); 

    return 0; 
} 

```

## Java

```java

// Java program to find the second last node  
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

    // method to find the second last  
    // node of the linked list  
    public int findSecondLastNode(Node ptr) 
    { 
        Node temp = ptr; 

        // If the list is empty or contains less  
        // than 2 nodes 
        if(temp == null || temp.next == null) 
            return -1; 

            // This loop stops at second last node 
        while(temp.next.next != null) 
        { 
            temp = temp.next; 
        } 
        return temp.data; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        LinkedList ll = new LinkedList(); 

        /* Use push() function to construct  
        the below list 8 -> 23 -> 11 -> 29 -> 12 */
        ll.push(12); 
        ll.push(29); 
        ll.push(11); 
        ll.push(23); 
        ll.push(8); 
        System.out.println(ll.findSecondLastNode(ll.start)); 
    } 
} 

// This code is Contributed by Adarsh_Verma 

```

## Python3

```py

# Python3 program to find the second last node 
# of a linked list in single traversal 
import math 

# Link list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to find the second last 
# node of the linked list 
def findSecondLastNode(head): 
    temp = head 

    # If the list is empty or  
    # contains less than 2 nodes 
    if (temp == None or temp.next == None): 
        return -1

    # Traverse the linked list 
    while (temp != None): 

        # Check if the current node is the 
        # second last node or not 
        if (temp.next.next == None): 
            return temp.data 

        # If not then move to the next node 
        temp = temp.next

# Function to push node at head 
def push(head, new_data): 
    new_node = Node(new_data) 
    #new_node.data = new_data 
    new_node.next = head 
    head = new_node 
    return head 

# Driver code 
if __name__ == '__main__': 

    # Start with the empty list 
    head = None

    # Use push() function to construct 
    # the below list 8 . 23 . 11 . 29 . 12 
    head = push(head, 12) 
    head = push(head, 29) 
    head = push(head, 11) 
    head = push(head, 23) 
    head = push(head, 8) 

    print(findSecondLastNode(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# program to find the second last node  
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

    // method to find the second last  
    // node of the linked list  
    public int findSecondLastNode(Node ptr) 
    { 
        Node temp = ptr; 

        // If the list is empty or contains less  
        // than 2 nodes 
        if(temp == null || temp.next == null) 
            return -1; 

            // This loop stops at second last node 
        while(temp.next.next != null) 
        { 
            temp = temp.next; 
        } 
        return temp.data; 
    } 

    // Driver code 
    public static void Main() 
    { 
        LinkedList ll = new LinkedList(); 

        /* Use push() function to construct  
        the below list 8 -> 23 -> 11 -> 29 -> 12 */
        ll.push(12); 
        ll.push(29); 
        ll.push(11); 
        ll.push(23); 
        ll.push(8); 
        Console.WriteLine(ll.findSecondLastNode(ll.start)); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
29

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。