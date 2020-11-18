# 将节点插入到链表

的中间

给定一个包含 **n** 个节点的链表。 问题是在列表中间插入一个新节点，其数据为 **x** 。 如果 **n** 是偶数，则在第**（n / 2）**个节点后插入新节点，否则在**（n + 1）/ 2 [** th 节点。

**示例：**

```
Input : list: 1->2->4->5
        x = 3
Output : 1->2->3->4->5

Input : list: 5->10->4->32->16
        x = 41
Output : 5->10->4->41->32->16

```

**方法 1（使用链接列表的长度）：**

使用一个遍历查找节点数或链接的长度。 设为**等于**。 如果 **len** 是偶数，则计算 **c** =（len / 2），否则，如果 **len** ，则计算 **c** =（len + 1）/ 2 ]很奇怪。 再次遍历第一个 **c** 节点，并在第 **c** 个节点之后插入新节点。

## C++

```cpp

// C++ implementation to insert node at the middle 
// of the linked list 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to create and return a node 
Node* getNode(int data) 
{ 
    // allocating space 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // inserting the required data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// function to insert node at the middle 
// of the linked list 
void insertAtMid(Node** head_ref, int x) 
{ 
    // if list is empty 
    if (*head_ref == NULL) 
        *head_ref = getNode(x); 
    else { 

        // get a new node 
        Node* newNode = getNode(x); 

        Node* ptr = *head_ref; 
        int len = 0; 

        // calculate length of the linked list 
        //, i.e, the number of nodes 
        while (ptr != NULL) { 
            len++; 
            ptr = ptr->next; 
        } 

        // 'count' the number of nodes after which 
        //  the new node is to be inserted 
        int count = ((len % 2) == 0) ? (len / 2) : 
                                    (len + 1) / 2; 
        ptr = *head_ref; 

        // 'ptr' points to the node after which  
        // the new node is to be inserted 
        while (count-- > 1) 
            ptr = ptr->next; 

        // insert the 'newNode' and adjust the 
        // required links 
        newNode->next = ptr->next; 
        ptr->next = newNode; 
    } 
} 

// function to display the linked list 
void display(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Creating the list 1->2->4->5 
    Node* head = NULL; 
    head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(4); 
    head->next->next->next = getNode(5); 

    cout << "Linked list before insertion: "; 
    display(head); 

    int x = 3; 
    insertAtMid(&head, x); 

    cout << "\nLinked list after insertion: "; 
    display(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to insert node 
// at the middle of the linked list 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class LinkedList 
{ 
    static Node head; // head of list 

    /* Node Class */
    static class Node { 
        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    // function to insert node at the  
    // middle of the linked list 
    static void insertAtMid(int x) 
    { 
        // if list is empty 
        if (head == null) 
            head = new Node(x); 
        else { 
            // get a new node 
            Node newNode = new Node(x); 

            Node ptr = head; 
            int len = 0; 

            // calculate length of the linked list 
            //, i.e, the number of nodes 
            while (ptr != null) { 
                len++; 
                ptr = ptr.next; 
            } 

            // 'count' the number of nodes after which 
            // the new node is to be inserted 
            int count = ((len % 2) == 0) ? (len / 2) : 
                                        (len + 1) / 2; 
            ptr = head; 

            // 'ptr' points to the node after which  
            // the new node is to be inserted 
            while (count-- > 1) 
                ptr = ptr.next; 

            // insert the 'newNode' and adjust  
            // the required links 
            newNode.next = ptr.next; 
            ptr.next = newNode; 
        } 
    } 

    // function to display the linked list 
    static void display() 
    { 
        Node temp = head; 
        while (temp != null)  
        { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
    } 

    // Driver program to test above 
    public static void main (String[] args)  
    {  
        // Creating the list 1.2.4.5 
        head = null; 
        head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(4); 
        head.next.next.next = new Node(5); 

        System.out.println("Linked list before "+ 
                           "insertion: "); 
        display(); 

        int x = 3; 
        insertAtMid(x); 

        System.out.println("\nLinked list after"+ 
                           " insertion: "); 
        display(); 
    }  
} 

// This article is contributed by Chhavi 

```

## Python3

```py

# Python3 implementation to insert node 
# at the middle of a linked list 

# Node class 
class Node: 

    # constructor to create a new node 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# function to insert node at the 
# middle of linked list given the head 
def insertAtMid(head, x): 

    if(head == None): #if the list is empty 
        head = Node(x) 
    else: 

        # create a new node for the value 
        # to be inserted 
        newNode = Node(x) 

        ptr = head 
        length = 0

        # calcualte the length of the linked 
        # list 
        while(ptr != None): 
            ptr = ptr.next
            length += 1

        # 'count' the number of node after which 
        # the new node has to be inserted 
        if(length % 2 == 0): 
            count = length / 2 
        else: 
            (length + 1) / 2

        ptr = head 

        # move ptr to the node after which 
        # the new node has to inserted 
        while(count > 1): 
            count -= 1
            ptr = ptr.next

        # insert the 'newNode' and adjust 
        # links accordingly 
        newNode.next = ptr.next
        ptr.next = newNode 

# function to displat the linked list 
def display(head): 
    temp = head 
    while(temp != None): 
        print(str(temp.data), end = " ") 
        temp = temp.next

# Driver Code 

# Creating the linked list 1.2.4.5 
head = Node(1) 
head.next = Node(2) 
head.next.next = Node(4) 
head.next.next.next = Node(5) 

print("Linked list before insertion: ", end = "") 
display(head) 

# inserting 3 in the middle of the linked list. 
x = 3
insertAtMid(head, x) 

print("\nLinked list after insertion: " , end = "") 
display(head) 

# This code is contributed by Pranav Devarakonda 

```

## C#

```cs

// C# implementation to insert node  
// at the middle of the linked list  
using System; 

public class LinkedList  
{  
    static Node head; // head of list  

    /* Node Class */
    public class Node  
    {  
        public int data;  
        public Node next;  

        // Constructor to create a new node  
        public Node(int d)  
        {  
            data = d;  
            next = null;  
        }  
    }  

    // function to insert node at the  
    // middle of the linked list  
    static void insertAtMid(int x)  
    {  
        // if list is empty  
        if (head == null)  
            head = new Node(x);  
        else 
        {  
            // get a new node  
            Node newNode = new Node(x);  

            Node ptr = head;  
            int len = 0;  

            // calculate length of the linked list  
            //, i.e, the number of nodes  
            while (ptr != null) 
            {  
                len++;  
                ptr = ptr.next;  
            }  

            // 'count' the number of nodes after which  
            // the new node is to be inserted  
            int count = ((len % 2) == 0) ? (len / 2) :  
                                        (len + 1) / 2;  
            ptr = head;  

            // 'ptr' points to the node after which  
            // the new node is to be inserted  
            while (count-- > 1)  
                ptr = ptr.next;  

            // insert the 'newNode' and adjust  
            // the required links  
            newNode.next = ptr.next;  
            ptr.next = newNode;  
        }  
    }  

    // function to display the linked list  
    static void display()  
    {  
        Node temp = head;  
        while (temp != null)  
        {  
            Console.Write(temp.data + " ");  
            temp = temp.next;  
        }  
    }  

    // Driver code  
    public static void Main ()  
    {  
        // Creating the list 1.2.4.5  
        head = null;  
        head = new Node(1);  
        head.next = new Node(2);  
        head.next.next = new Node(4);  
        head.next.next.next = new Node(5);  

        Console.WriteLine("Linked list before "+  
                        "insertion: ");  
        display();  

        int x = 3;  
        insertAtMid(x);  

        Console.WriteLine("\nLinked list after"+  
                        " insertion: ");  
        display();  
    }  
}  

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Linked list before insertion: 1 2 4 5
Linked list after insertion: 1 2 3 4 5

```

**时间复杂度：** O（n）

**方法 2（使用两个指针）：**

基于乌龟和野兔算法，该算法使用两个指针，一个称为**慢速**，另一个称为**快速**。 该算法有助于找到链表的中间节点。 在此帖子的[正面和黑色拆分过程中对此进行了说明。 现在，您可以在通过上述过程获得的中间节点之后插入新节点。 这种方法只需要遍历列表。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

## C++

```cpp

// C++ implementation to insert node at the middle 
// of the linked list 
#include <bits/stdc++.h> 

using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// function to create and return a node 
Node* getNode(int data) 
{ 
    // allocating space 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // inserting the required data 
    newNode->data = data; 
    newNode->next = NULL; 
} 

// function to insert node at the middle 
// of the linked list 
void insertAtMid(Node** head_ref, int x) 
{ 
    // if list is empty 
    if (*head_ref == NULL) 
        *head_ref = getNode(x); 

    else { 
        // get a new node 
        Node* newNode = getNode(x); 

        // assign values to the slow and fast  
        // pointers 
        Node* slow = *head_ref; 
        Node* fast = (*head_ref)->next; 

        while (fast && fast->next) { 

            // move slow pointer to next node 
            slow = slow->next; 

            // move fast pointer two nodes at a time 
            fast = fast->next->next; 
        } 

        // insert the 'newNode' and adjust the 
        // required links 
        newNode->next = slow->next; 
        slow->next = newNode; 
    } 
} 

// function to display the linked list 
void display(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // Creating the list 1->2->4->5 
    Node* head = NULL; 
    head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(4); 
    head->next->next->next = getNode(5); 

    cout << "Linked list before insertion: "; 
    display(head); 

    int x = 3; 
    insertAtMid(&head, x); 

    cout << "\nLinked list after insertion: "; 
    display(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation to insert node  
// at the middle of the linked list 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class LinkedList 
{ 
    static Node head; // head of list 

    /* Node Class */
    static class Node { 
        int data; 
        Node next; 

        // Constructor to create a new node 
        Node(int d) { 
            data = d; 
            next = null; 
        } 
    } 

    // function to insert node at the  
    // middle of the linked list 
    static void insertAtMid(int x) 
    { 
        // if list is empty 
        if (head == null) 
        head = new Node(x); 

        else { 
            // get a new node 
            Node newNode = new Node(x); 

            // assign values to the slow  
            // and fast pointers 
            Node slow = head; 
            Node fast = head.next; 

            while (fast != null && fast.next  
                                  != null)  
            { 
                // move slow pointer to next node 
                slow = slow.next; 

                // move fast pointer two nodes  
                // at a time 
                fast = fast.next.next; 
            } 

            // insert the 'newNode' and adjust  
            // the required links 
            newNode.next = slow.next; 
            slow.next = newNode; 
        } 
    } 

    // function to display the linked list 
    static void display() 
    { 
        Node temp = head; 
        while (temp != null)  
        { 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } 
    } 

    // Driver program to test above 
    public static void main (String[] args)  
    {  
        // Creating the list 1.2.4.5 
        head = null; 
        head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(4); 
        head.next.next.next = new Node(5); 

        System.out.println("Linked list before"+ 
                           " insertion: "); 
        display(); 

        int x = 3; 
        insertAtMid(x); 

        System.out.println("\nLinked list after"+ 
                           " insertion: "); 
        display(); 
    }  
} 

// This article is contributed by Chhavi 

```

## Python3

```py

# Python implementation to insert node  
# at the middle of the linked list  

# Node Class 
class Node : 
    def __init__(self, d): 
        self.data = d  
        self.next = None

class LinkedList:  

    # function to insert node at the  
    # middle of the linked list 
    def __init__(self): 
        self.head = None

    # Function to insert a new node  
    # at the beginning  
    def push(self, new_data):  
        new_node = Node(new_data)  
        new_node.next = self.head  
        self.head = new_node  

    def insertAtMid(self, x): 

        # if list is empty  
        if (self.head == None):  
            self.head = Node(x)  

        else:  

            # get a new node  
            newNode = Node(x)  

            # assign values to the slow  
            # and fast pointers  
            slow = self.head 
            fast = self.head.next

            while (fast != None and 
                   fast.next != None):  

                # move slow pointer to next node  
                slow = slow.next

                # move fast pointer two nodes  
                # at a time  
                fast = fast.next.next

            # insert the 'newNode' and  
            # adjust the required links  
            newNode.next = slow.next
            slow.next = newNode 

    # function to display the linked list  
    def display(self): 
        temp = self.head  
        while (temp != None):  
            print(temp.data, end = " "), 
            temp = temp.next

# Driver Code 

# Creating the list 1.2.4.5  
ll = LinkedList() 
ll.push(5) 
ll.push(4) 
ll.push(2) 
ll.push(1) 
print("Linked list before insertion: "), 
ll.display() 

x = 3
ll.insertAtMid(x) 

print("\nLinked list after insertion: "), 
ll.display() 

# This code is contributed by prerna saini 

```

## C#

```cs

// C# implementation to insert node  
// at the middle of the linked list 
using System; 

public class LinkedList 
{ 
    static Node head; // head of list 

    /* Node Class */
    class Node  
    { 
        public int data; 
        public Node next; 

        // Constructor to create a new node 
        public Node(int d)  
        { 
            data = d; 
            next = null; 
        } 
    } 

    // function to insert node at the  
    // middle of the linked list 
    static void insertAtMid(int x) 
    { 
        // if list is empty 
        if (head == null) 
        head = new Node(x); 

        else
        { 
            // get a new node 
            Node newNode = new Node(x); 

            // assign values to the slow  
            // and fast pointers 
            Node slow = head; 
            Node fast = head.next; 

            while (fast != null && fast.next  
                                != null)  
            { 
                // move slow pointer to next node 
                slow = slow.next; 

                // move fast pointer two nodes  
                // at a time 
                fast = fast.next.next; 
            } 

            // insert the 'newNode' and adjust  
            // the required links 
            newNode.next = slow.next; 
            slow.next = newNode; 
        } 
    } 

    // function to display the linked list 
    static void display() 
    { 
        Node temp = head; 
        while (temp != null)  
        { 
            Console.Write(temp.data + " "); 
            temp = temp.next; 
        } 
    } 

    // Driver code 
    public static void Main (String[] args)  
    {  
        // Creating the list 1.2.4.5 
        head = null; 
        head = new Node(1); 
        head.next = new Node(2); 
        head.next.next = new Node(4); 
        head.next.next.next = new Node(5); 

        Console.WriteLine("Linked list before"+ 
                        " insertion: "); 
        display(); 

        int x = 3; 
        insertAtMid(x); 

        Console.WriteLine("\nLinked list after"+ 
                        " insertion: "); 
        display(); 
    }  
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Linked list before insertion: 1 2 4 5
Linked list after insertion: 1 2 3 4 5

```

**时间复杂度：** O（n）

本文由 **Ayush Jauhari** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

