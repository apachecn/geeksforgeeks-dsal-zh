# 计算给定链接列表

中的重复项

给定一个链表。 任务是计算链接列表中重复节点的数量。
**范例：**

> **输入：** 5-> 7-> 5-> 1-> 7->空
> **输出：** 2
> 
> **输入：** 5-> 7-> 8-> 7-> 1->空
> **输出：** 1

**简单方法：**我们遍历整个链表。 对于每个节点，我们在其余列表中检查是否存在重复节点。 如果是，那么我们增加计数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
#include <unordered_set> 
using namespace std; 

// Representation of node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the beginning 
void insert(Node** head, int item) 
{ 
    Node* temp = new Node(); 
    temp->data = item; 
    temp->next = *head; 
    *head = temp; 
} 

// Function to count the number of 
// duplicate nodes in the linked list 
int countNode(Node* head) 
{ 
    int count = 0; 

    while (head->next != NULL) { 

        // Starting from the next node 
        Node *ptr = head->next; 
        while (ptr != NULL) { 

            // If some duplicate node is found 
            if (head->data == ptr->data) { 
                count++; 
                break; 
            } 
            ptr = ptr->next; 
        } 

        head = head->next; 
    } 

    // Return the count of duplicate nodes 
    return count; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    insert(&head, 5); 
    insert(&head, 7); 
    insert(&head, 5); 
    insert(&head, 1); 
    insert(&head, 7); 

    cout << countNode(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GFG 
{ 

// Representation of node  
static class Node  
{  
    int data;  
    Node next;  
};  

// Function to insert a node at the beginning  
static Node insert(Node head, int item)  
{  
    Node temp = new Node();  
    temp.data = item;  
    temp.next = head;  
    head = temp; 
    return head; 
}  

// Function to count the number of  
// duplicate nodes in the linked list  
static int countNode(Node head)  
{  
    int count = 0;  

    while (head.next != null)  
    {  

        // Starting from the next node  
        Node ptr = head.next;  
        while (ptr != null)  
        {  

            // If some duplicate node is found  
            if (head.data == ptr.data)  
            {  
                count++;  
                break;  
            }  
            ptr = ptr.next;  
        }  

        head = head.next;  
    }  

    // Return the count of duplicate nodes  
    return count;  
}  

// Driver code  
public static void main(String args[]) 
{  
    Node head = null;  
    head = insert(head, 5);  
    head = insert(head, 7);  
    head = insert(head, 5);  
    head = insert(head, 1);  
    head = insert(head, 7);  

    System.out.println( countNode(head));  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 
import math 

# Representation of node 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to push a node at the beginning 
def push(head, item):  
    temp = Node(item);  
    temp.data = item;  
    temp.next = head;  
    head = temp; 
    return head; 

# Function to count the number of 
# duplicate nodes in the linked list 
def countNode(head): 
    count = 0
    while (head.next != None): 

        # print(1) 
        # Starting from the next node 
        ptr = head.next
        while (ptr != None): 

            # print(2) 
            # If some duplicate node is found 
            if (head.data == ptr.data): 
                count = count + 1
                break
            ptr = ptr.next
        head = head.next

    # Return the count of duplicate nodes 
    return count 

# Driver code 
if __name__=='__main__':  

    head = None; 
    head = push(head, 5) 
    head = push(head, 7) 
    head = push(head, 5) 
    head = push(head, 1) 
    head = push(head, 7) 
    print(countNode(head)) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the approach  
using System; 

class GFG 
{ 

// Representation of node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to insert a node at the beginning  
static Node insert(Node head, int item)  
{  
    Node temp = new Node();  
    temp.data = item;  
    temp.next = head;  
    head = temp; 
    return head; 
}  

// Function to count the number of  
// duplicate nodes in the linked list  
static int countNode(Node head)  
{  
    int count = 0;  

    while (head.next != null)  
    {  

        // Starting from the next node  
        Node ptr = head.next;  
        while (ptr != null)  
        {  

            // If some duplicate node is found  
            if (head.data == ptr.data)  
            {  
                count++;  
                break;  
            }  
            ptr = ptr.next;  
        }  

        head = head.next;  
    }  

    // Return the count of duplicate nodes  
    return count;  
}  

// Driver code  
public static void Main(String []args) 
{  
    Node head = null;  
    head = insert(head, 5);  
    head = insert(head, 7);  
    head = insert(head, 5);  
    head = insert(head, 1);  
    head = insert(head, 7);  

    Console.WriteLine( countNode(head));  
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
2

```

**时间复杂度：** O（n * n）

**有效方法：**的想法是使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
#include <unordered_set> 
using namespace std; 

// Representation of node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to insert a node at the beginning 
void insert(Node** head, int item) 
{ 
    Node* temp = new Node(); 
    temp->data = item; 
    temp->next = *head; 
    *head = temp; 
} 

// Function to count the number of 
// duplicate nodes in the linked list 
int countNode(Node* head) 
{ 
    if (head == NULL) 
       return 0;; 

    // Create a hash table insert head 
    unordered_set<int> s; 
    s.insert(head->data); 

    // Traverse through remaining nodes     
    int count = 0; 
    for (Node *curr=head->next; curr != NULL; curr=curr->next) { 
        if (s.find(curr->data) != s.end()) 
             count++;  

        s.insert(curr->data); 
    } 

    // Return the count of duplicate nodes 
    return count; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    insert(&head, 5); 
    insert(&head, 7); 
    insert(&head, 5); 
    insert(&head, 1); 
    insert(&head, 7); 

    cout << countNode(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
import java.util.HashSet; 

class GFG  
{ 

// Representation of node 
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head; 

// Function to insert a node at the beginning 
static void insert(Node ref_head, int item) 
{ 
    Node temp = new Node(); 
    temp.data = item; 
    temp.next = ref_head; 
    head = temp; 

} 

// Function to count the number of 
// duplicate nodes in the linked list 
static int countNode(Node head) 
{ 
    if (head == null) 
    return 0;; 

    // Create a hash table insert head 
    HashSet<Integer>s = new HashSet<>(); 
    s.add(head.data); 

    // Traverse through remaining nodes  
    int count = 0; 
    for (Node curr=head.next; curr != null; curr=curr.next)  
    { 
        if (s.contains(curr.data)) 
            count++;  

        s.add(curr.data); 
    } 

    // Return the count of duplicate nodes 
    return count; 
} 

// Driver code 
public static void main(String[] args)  
{ 

    insert(head, 5); 
    insert(head, 7); 
    insert(head, 5); 
    insert(head, 1); 
    insert(head, 7); 

    System.out.println(countNode(head)); 
} 
} 

// This code is contributed by Princi Singh 

```

## 蟒蛇

```

# Python3 implementation of the approach  

# Node of a linked list  
class Node:  
    def __init__(self, data = None, next = None):  
        self.next = next
        self.data = data  

head = None

# Function to insert a node at the beginning 
def insert(ref_head, item): 
    global head 
    temp = Node() 
    temp.data = item 
    temp.next = ref_head 
    head = temp 

# Function to count the number of 
# duplicate nodes in the linked list 
def countNode(head): 

    if (head == None): 
        return 0

    # Create a hash table insert head 
    s = set() 
    s.add(head.data) 

    # Traverse through remaining nodes  
    count = 0
    curr = head.next
    while ( curr != None ) : 
        if (curr.data in s): 
            count = count + 1

        s.add(curr.data) 
        curr = curr.next

    # Return the count of duplicate nodes 
    return count 

# Driver code 
insert(head, 5) 
insert(head, 7) 
insert(head, 5) 
insert(head, 1) 
insert(head, 7) 

print(countNode(head)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// Representation of node 
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head; 

// Function to insert a node at the beginning 
static void insert(Node ref_head, int item) 
{ 
    Node temp = new Node(); 
    temp.data = item; 
    temp.next = ref_head; 
    head = temp; 

} 

// Function to count the number of 
// duplicate nodes in the linked list 
static int countNode(Node head) 
{ 
    if (head == null) 
    return 0;; 

    // Create a hash table insert head 
    HashSet<int>s = new HashSet<int>(); 
    s.Add(head.data); 

    // Traverse through remaining nodes  
    int count = 0; 
    for (Node curr=head.next; curr != null; curr=curr.next)  
    { 
        if (s.Contains(curr.data)) 
            count++;  

        s.Add(curr.data); 
    } 

    // Return the count of duplicate nodes 
    return count; 
} 

// Driver code 
public static void Main(String[] args)  
{ 

    insert(head, 5); 
    insert(head, 7); 
    insert(head, 5); 
    insert(head, 1); 
    insert(head, 7); 

    Console.WriteLine(countNode(head)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
2

```

**时间复杂度：** O（n）



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。