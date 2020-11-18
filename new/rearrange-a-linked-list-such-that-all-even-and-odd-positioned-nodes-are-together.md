# 重新排列链接列表，以便所有偶数和奇数定位的节点都在一起

重新排列链表，使所有奇数位置节点都在一起，而所有偶数位置节点都在一起，

**示例：**

```
Input:   1->2->3->4
Output:  1->3->2->4

Input:   10->22->30->43->56->70
Output:  10->30->56->22->43->70

```

这个问题的重点是确保处理以下所有情况

1）空链表

2）仅具有一个节点的链表

3）仅具有两个节点的链表

4）节点数为奇数的链表

5）节点数为偶数的链表

下面的程序将当前节点的两个指针“奇数”和“偶数”分别维持在奇数和偶数位置。 我们还存储偶数链接列表的第一个节点，以便在将所有奇数和偶数节点连接到两个不同的列表中之后，可以将偶数列表附加到奇数列表的末尾。

## C++

```cpp

// C++ program to rearrange a linked list in such a  
// way that all odd positioned node are stored before  
// all even positioned nodes  
#include<bits/stdc++.h>  
using namespace std;  

// Linked List Node  
class Node  
{  
    public: 
    int data;  
    Node* next;  
};  

// A utility function to create a new node  
Node* newNode(int key)  
{  
    Node *temp = new Node;  
    temp->data = key;  
    temp->next = NULL;  
    return temp;  
}  

// Rearranges given linked list such that all even  
// positioned nodes are before odd positioned.  
// Returns new head of linked List.  
Node *rearrangeEvenOdd(Node *head)  
{  
    // Corner case  
    if (head == NULL)  
        return NULL;  

    // Initialize first nodes of even and  
    // odd lists  
    Node *odd = head;  
    Node *even = head->next;  

    // Remember the first node of even list so  
    // that we can connect the even list at the  
    // end of odd list.  
    Node *evenFirst = even;  

    while (1)  
    {  
        // If there are no more nodes, then connect  
        // first node of even list to the last node  
        // of odd list  
        if (!odd || !even || !(even->next))  
        {  
            odd->next = evenFirst;  
            break;  
        }  

        // Connecting odd nodes  
        odd->next = even->next;  
        odd = even->next;  

        // If there are NO more even nodes after  
        // current odd.  
        if (odd->next == NULL)  
        {  
            even->next = NULL;  
            odd->next = evenFirst;  
            break;  
        }  

        // Connecting even nodes  
        even->next = odd->next;  
        even = odd->next;  
    }  

    return head;  
}  

// A utility function to print a linked list  
void printlist(Node * node)  
{  
    while (node != NULL)  
    {  
        cout << node->data << "->";  
        node = node->next;  
    }  
    cout << "NULL" << endl;  
}  

// Driver code  
int main(void)  
{  
    Node *head = newNode(1);  
    head->next = newNode(2);  
    head->next->next = newNode(3);  
    head->next->next->next = newNode(4);  
    head->next->next->next->next = newNode(5);  

    cout << "Given Linked List\n";  
    printlist(head);  

    head = rearrangeEvenOdd(head);  

    cout << "Modified Linked List\n";  
    printlist(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```c

// C program to rearrange a linked list in such a 
// way that all odd positioned node are stored before 
// all even positioned nodes 
#include<bits/stdc++.h> 
using namespace std; 

// Linked List Node 
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// A utility function to create a new node 
Node* newNode(int key) 
{ 
    Node *temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Rearranges given linked list such that all even 
// positioned nodes are before odd positioned. 
// Returns new head of linked List. 
Node *rearrangeEvenOdd(Node *head) 
{ 
    // Corner case 
    if (head == NULL) 
        return NULL; 

    // Initialize first nodes of even and 
    // odd lists 
    Node *odd = head; 
    Node *even = head->next; 

    // Remember the first node of even list so 
    // that we can connect the even list at the 
    // end of odd list. 
    Node *evenFirst = even; 

    while (1) 
    { 
        // If there are no more nodes, then connect 
        // first node of even list to the last node 
        // of odd list 
        if (!odd || !even || !(even->next)) 
        { 
            odd->next = evenFirst; 
            break; 
        } 

        // Connecting odd nodes 
        odd->next = even->next; 
        odd = even->next; 

        // If there are NO more even nodes after 
        // current odd. 
        if (odd->next == NULL) 
        { 
            even->next = NULL; 
            odd->next = evenFirst; 
            break; 
        } 

        // Connecting even nodes 
        even->next = odd->next; 
        even = odd->next; 
    } 

    return head; 
} 

// A utility function to print a linked list 
void printlist(Node * node) 
{ 
    while (node != NULL) 
    { 
        cout << node->data << "->"; 
        node = node->next; 
    } 
    cout << "NULL" << endl; 
} 

// Driver code 
int main(void) 
{ 
    Node *head = newNode(1); 
    head->next = newNode(2); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(5); 

    cout << "Given Linked List\n"; 
    printlist(head); 

    head = rearrangeEvenOdd(head); 

    cout << "\nModified Linked List\n"; 
    printlist(head); 

    return 0; 
} 

```

## Java

```java

// Java program to rearrange a linked list  
// in such a way that all odd positioned   
// node are stored before all even positioned nodes  
class GfG  
{  

// Linked List Node  
static class Node  
{  
    int data;  
    Node next;  
} 

// A utility function to create a new node  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

// Rearranges given linked list  
// such that all even positioned  
// nodes are before odd positioned.  
// Returns new head of linked List.  
static Node rearrangeEvenOdd(Node head)  
{  
    // Corner case  
    if (head == null)  
        return null;  

    // Initialize first nodes of even and  
    // odd lists  
    Node odd = head;  
    Node even = head.next;  

    // Remember the first node of even list so  
    // that we can connect the even list at the  
    // end of odd list.  
    Node evenFirst = even;  

    while (1 == 1)  
    {  
        // If there are no more nodes,   
        // then connect first node of even   
        // list to the last node of odd list  
        if (odd == null || even == null || 
                        (even.next) == null)  
        {  
            odd.next = evenFirst;  
            break;  
        }  

        // Connecting odd nodes  
        odd.next = even.next;  
        odd = even.next;  

        // If there are NO more even nodes   
        // after current odd.  
        if (odd.next == null)  
        {  
            even.next = null;  
            odd.next = evenFirst;  
            break;  
        }  

        // Connecting even nodes  
        even.next = odd.next;  
        even = odd.next;  
    }  
    return head;  
}  

// A utility function to print a linked list  
static void printlist(Node node)  
{  
    while (node != null)  
    {  
        System.out.print(node.data + "->");  
        node = node.next;  
    }  
    System.out.println("NULL") ;  
}  

// Driver code  
public static void main(String[] args)  
{  
    Node head = newNode(1);  
    head.next = newNode(2);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(5);  

    System.out.println("Given Linked List");  
    printlist(head);  

    head = rearrangeEvenOdd(head);  

    System.out.println("Modified Linked List");  
    printlist(head);  
} 
}  

// This code is contributed by Prerna saini 

```

## Python3

```py

# Python3 program to rearrange a linked list  
# in such a way that all odd positioned  
# node are stored before all even positioned nodes  

# Linked List Node  
class Node:  
    def __init__(self, d): 
        self.data = d 
        self.next = None

class LinkedList: 
    def __init__(self): 
        self.head = None

    # A utility function to create 
    # a new node  
    def newNode(self, key):  
        temp = Node(key)  
        self.next = None
        return temp  

    # Rearranges given linked list  
    # such that all even positioned  
    # nodes are before odd positioned.  
    # Returns new head of linked List.  
    def rearrangeEvenOdd(self, head):  

        # Corner case  
        if (self.head == None):  
            return None

        # Initialize first nodes of  
        # even and odd lists  
        odd = self.head  
        even = self.head.next

        # Remember the first node of even list so  
        # that we can connect the even list at the  
        # end of odd list.  
        evenFirst = even  

        while (1 == 1):  

            # If there are no more nodes,  
            # then connect first node of even  
            # list to the last node of odd list  
            if (odd == None or even == None or 
                              (even.next) == None):  
                odd.next = evenFirst  
                break

            # Connecting odd nodes  
            odd.next = even.next
            odd = even.next

            # If there are NO more even nodes  
            # after current odd.  
            if (odd.next == None):  
                even.next = None
                odd.next = evenFirst  
                break

            # Connecting even nodes  
            even.next = odd.next
            even = odd.next
        return head 

    # A utility function to print a linked list  
    def printlist(self, node):  
        while (node != None):  
            print(node.data, end = "") 
            print("->", end = "") 
            node = node.next
        print ("NULL") 

    # Function to insert a new node  
    # at the beginning  
    def push(self, new_data):  
        new_node = Node(new_data)  
        new_node.next = self.head  
        self.head = new_node 

# Driver code  
ll = LinkedList() 
ll.push(5) 
ll.push(4) 
ll.push(3) 
ll.push(2) 
ll.push(1) 
print ("Given Linked List") 
ll.printlist(ll.head)  

start = ll.rearrangeEvenOdd(ll.head)  

print ("\nModified Linked List") 
ll.printlist(start) 

# This code is contributed by Prerna Saini 

```

## C#

```cs

// C# program to rearrange a linked list  
// in such a way that all odd positioned  
// node are stored before all even positioned nodes  
using System; 

class GfG  
{  

    // Linked List Node  
    class Node  
    {  
        public int data;  
        public Node next;  
    }  

    // A utility function to create a new node  
    static Node newNode(int key)  
    {  
        Node temp = new Node();  
        temp.data = key;  
        temp.next = null;  
        return temp;  
    }  

    // Rearranges given linked list  
    // such that all even positioned  
    // nodes are before odd positioned.  
    // Returns new head of linked List.  
    static Node rearrangeEvenOdd(Node head)  
    {  
        // Corner case  
        if (head == null)  
            return null;  

        // Initialize first nodes of even and  
        // odd lists  
        Node odd = head;  
        Node even = head.next;  

        // Remember the first node of even list so  
        // that we can connect the even list at the  
        // end of odd list.  
        Node evenFirst = even;  

        while (1 == 1)  
        {  
            // If there are no more nodes,  
            // then connect first node of even  
            // list to the last node of odd list  
            if (odd == null || even == null ||  
                            (even.next) == null)  
            {  
                odd.next = evenFirst;  
                break;  
            }  

            // Connecting odd nodes  
            odd.next = even.next;  
            odd = even.next;  

            // If there are NO more even nodes  
            // after current odd.  
            if (odd.next == null)  
            {  
                even.next = null;  
                odd.next = evenFirst;  
                break;  
            }  

            // Connecting even nodes  
            even.next = odd.next;  
            even = odd.next;  
        }  
        return head;  
    }  

    // A utility function to print a linked list  
    static void printlist(Node node)  
    {  
        while (node != null)  
        {  
            Console.Write(node.data + "->");  
            node = node.next;  
        }  
        Console.WriteLine("NULL") ;  
    }  

    // Driver code  
    public static void Main()  
    {  
        Node head = newNode(1);  
        head.next = newNode(2);  
        head.next.next = newNode(3);  
        head.next.next.next = newNode(4);  
        head.next.next.next.next = newNode(5);  

        Console.WriteLine("Given Linked List");  
        printlist(head);  

        head = rearrangeEvenOdd(head);  

        Console.WriteLine("Modified Linked List");  
        printlist(head);  
    }  
}  

/* This code is contributed PrinciRaj1992 */

```

**Output:**

```
Given Linked List
1->2->3->4->5->NULL
Modified Linked List
1->3->5->2->4->NULL

```

本文由 **Harsh Parikh** 提供。请在此处查看[由 **Gautam Singh** 提供的另一个代码](https://ide.geeksforgeeks.org/vLDGJY)。 一篇文章，然后将您的文章邮寄到 contribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

