# 在两个单链表

中找到公共节点

给定两个链表，任务是在两个单链表中查找公共节点的数量。

**示例：**

> **输入：**列表 A = 3-> 4-> 12-> 10-> 17，列表 B = 10-> 4-> 8-> 575-> 34-> 12
> **输出：**两个列表中的公共节点数均为= 3
> 
> **输入：**列表 A = 12-> 4-> 65-> 14-> 59，列表 B = 14-> 15-> 23-> 17-> 41-> 54
> **输出：**两个列表中的公共节点数均为= 1

**天真的方法：**将列表 A 的每个节点与列表 B 的每个节点进行比较。如果该节点匹配，则在比较所有节点后增加计数并返回计数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to common nodes which have 
// same value node(s) both list 
int countCommonNodes(struct Node* head1, struct Node* head2) 
{ 
    // list A 
    struct Node* current1 = head1; 

    // list B 
    struct Node* current2 = head2; 

    // set count = 0 
    int count = 0; 

    // traverse list A till the end of list 
    while (current1 != NULL) { 

        // traverse list B till the end of list 
        while (current2 != NULL) { 

            // if data is match then count increase 
            if (current1->data == current2->data) 
                count++; 

            // increase current pointer for next node 
            current2 = current2->next; 
        } 

        // increase current pointer of list A 
        current1 = current1->next; 

        // initialize list B starting point 
        current2 = head2; 
    } 

    // return count 
    return count; 
} 

/* Utility function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

/* Driver program to test above functions */
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    /* Create following linked list  
    List A = 3 -> 4 -> 12 -> 10 -> 17 
*/

    push(&head1, 17); 
    push(&head1, 10); 
    push(&head1, 12); 
    push(&head1, 4); 
    push(&head1, 3); 

    // List B = 10 -> 4 -> 8 -> 575 -> 34 -> 12 
    push(&head2, 12); 
    push(&head2, 34); 
    push(&head2, 575); 
    push(&head2, 8); 
    push(&head2, 4); 
    push(&head2, 10); 

    // print list A 
    cout << "Given Linked List A: \n"; 
    printList(head1); 

    // print list B 
    cout << "Given Linked List B: \n"; 
    printList(head2); 

    // call function for count common node 
    int count = countCommonNodes(head1, head2); 

    // print number of common node in both list 
    cout << "Number of common node in both list is = " << count; 
    return 0; 
} 

```

## Java

```java

// Java implementation of above approach 
class GFG { 

    // Structure of a linked list node 
    static class Node { 
        int data; 
        Node next; 
    }; 

    // Function to common nodes which have 
    // same value node(s) both list 
    static int countCommonNodes(Node head1, Node head2) 
    { 
        // list A 
        Node current1 = head1; 

        // list B 
        Node current2 = head2; 

        // set count = 0 
        int count = 0; 

        // traverse list A till the end of list 
        while (current1 != null) { 

            // traverse list B till the end of list 
            while (current2 != null) { 

                // if data is match then count increase 
                if (current1.data == current2.data) 
                    count++; 

                // increase current pointer for next node 
                current2 = current2.next; 
            } 

            // increase current pointer of list A 
            current1 = current1.next; 

            // initialize list B starting point 
            current2 = head2; 
        } 

        // return count 
        return count; 
    } 

    // Utility function to insert a node at the beginning / 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Utility function to print a linked list 
    static void printList(Node head) 
    { 
        while (head != null) { 
            System.out.print(head.data + " "); 
            head = head.next; 
        } 
        System.out.println(); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        Node head1 = null; 
        Node head2 = null; 

        // Create following linked list 
        // List A = 3 . 4 . 12 . 10 . 17 

        head1 = push(head1, 17); 
        head1 = push(head1, 10); 
        head1 = push(head1, 12); 
        head1 = push(head1, 4); 
        head1 = push(head1, 3); 

        // List B = 10 . 4 . 8 . 575 . 34 . 12 
        head2 = push(head2, 12); 
        head2 = push(head2, 34); 
        head2 = push(head2, 575); 
        head2 = push(head2, 8); 
        head2 = push(head2, 4); 
        head2 = push(head2, 10); 

        // print list A 
        System.out.print("Given Linked List A: \n"); 
        printList(head1); 

        // print list B 
        System.out.print("Given Linked List B: \n"); 
        printList(head2); 

        // call function for count common node 
        int count = countCommonNodes(head1, head2); 

        // print number of common node in both list 
        System.out.print("Number of common node in both list is = " + count); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of above approach 

# Link list node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function to common nodes which have 
# same value node(s) both list 
def countCommonNodes(head1, head2): 

    # list A 
    current1 = head1 

    # list B 
    current2 = head2 

    # set count = 0 
    count = 0

    # traverse list A till the end of list 
    while (current1 != None): 

        # traverse list B till the end of list 
        while (current2 != None): 

            # if data is match then count increase 
            if (current1.data == current2.data): 
                count = count + 1

            # increase current pointer for next node 
            current2 = current2.next

        # increase current pointer of list A 
        current1 = current1.next

        # initialize list B starting point 
        current2 = head2 

    # return count 
    return count 

# Utility function to insert a node at the beginning  
def push(head_ref, new_data): 
    new_node = Node(0) 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Utility function to print a linked list 
def printList( head): 
    while (head != None): 
        print(head.data, end = " ") 
        head = head.next

    print("") 

# Driver Code  
if __name__=='__main__':  

    head1 = None
    head2 = None

    # Create following linked list 
    # List A = 3 . 4 . 12 . 10 . 17 
    head1 = push(head1, 17) 
    head1 = push(head1, 10) 
    head1 = push(head1, 12) 
    head1 = push(head1, 4) 
    head1 = push(head1, 3) 

    # List B = 10 . 4 . 8 . 575 . 34 . 12 
    head2 = push(head2, 12) 
    head2 = push(head2, 34) 
    head2 = push(head2, 575) 
    head2 = push(head2, 8) 
    head2 = push(head2, 4) 
    head2 = push(head2, 10) 

    # print list A 
    print("Given Linked List A: ") 
    printList(head1) 

    # print list B 
    print("Given Linked List B: ") 
    printList(head2) 

    # call function for count common node 
    count = countCommonNodes(head1, head2) 

    # print number of common node in both list 
    print("Number of common node in both list is = ", count) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG { 

    // Structure of a linked list node 
    public class Node { 
        public int data; 
        public Node next; 
    }; 

    // Function to common nodes which have 
    // same value node(s) both list 
    static int countCommonNodes(Node head1, Node head2) 
    { 
        // list A 
        Node current1 = head1; 

        // list B 
        Node current2 = head2; 

        // set count = 0 
        int count = 0; 

        // traverse list A till the end of list 
        while (current1 != null) { 

            // traverse list B till the end of list 
            while (current2 != null) { 

                // if data is match then count increase 
                if (current1.data == current2.data) 
                    count++; 

                // increase current pointer for next node 
                current2 = current2.next; 
            } 

            // increase current pointer of list A 
            current1 = current1.next; 

            // initialize list B starting point 
            current2 = head2; 
        } 

        // return count 
        return count; 
    } 

    // Utility function to insert a node at the beginning / 
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Utility function to print a linked list 
    static void printList(Node head) 
    { 
        while (head != null) { 
            Console.Write(head.data + " "); 
            head = head.next; 
        } 
        Console.WriteLine(); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        Node head1 = null; 
        Node head2 = null; 

        // Create following linked list 
        // List A = 3 . 4 . 12 . 10 . 17 

        head1 = push(head1, 17); 
        head1 = push(head1, 10); 
        head1 = push(head1, 12); 
        head1 = push(head1, 4); 
        head1 = push(head1, 3); 

        // List B = 10 . 4 . 8 . 575 . 34 . 12 
        head2 = push(head2, 12); 
        head2 = push(head2, 34); 
        head2 = push(head2, 575); 
        head2 = push(head2, 8); 
        head2 = push(head2, 4); 
        head2 = push(head2, 10); 

        // print list A 
        Console.Write("Given Linked List A: \n"); 
        printList(head1); 

        // print list B 
        Console.Write("Given Linked List B: \n"); 
        printList(head2); 

        // call function for count common node 
        int count = countCommonNodes(head1, head2); 

        // print number of common node in both list 
        Console.Write("Number of common node in both list is = " + count); 
    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
Given Linked List A: 
3 4 12 10 17 
Given Linked List B: 
10 4 8 575 34 12 
Number of common node in both list is = 3

```

**时间复杂度：** O（M * N），其中 M 是列表 A 的长度，N 是列表 B 的长度

**有效解决方案：**将链接列表 A 的所有节点插入 unordered_set 中，然后检查 unordered_set 中的链接列表 B 的每个节点。 如果找到，则增加计数并在最后返回计数。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to common nodes which have 
// same value node(s) both list 
int countCommonNodes(struct Node* head1, struct Node* head2) 
{ 
    // list  A 
    struct Node* current1 = head1; 

    // list B 
    struct Node* current2 = head2; 

    // set count  = 0 
    int count = 0; 

    // create unordered_set 
    unordered_set<int> map; 

    // traverse list A till the end of list 
    while (current1 != NULL) { 

        // insert list data in map 
        map.insert(current1->data); 

        // increase current pointer of list A 
        current1 = current1->next; 
    } 

    while (current2 != NULL) { 

        // traverse list B till the end of list 
        // if data match then increase count 
        if (map.find(current2->data) != map.end()) 
            count++; 

        // increase current pointer of list B 
        current2 = current2->next; 
    } 

    // return count 
    return count; 
} 

/* Utility function to insert a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

/* Utility function to print a linked list */
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

/* Driver program to test above functions */
int main() 
{ 
    struct Node* head1 = NULL; 
    struct Node* head2 = NULL; 

    /* Create following linked list  
    List A = 3 -> 4 -> 12 -> 10 -> 17 
   */

    push(&head1, 17); 
    push(&head1, 10); 
    push(&head1, 12); 
    push(&head1, 4); 
    push(&head1, 3); 

    // List B = 10 -> 4 -> 8 -> 575 -> 34 -> 12 
    push(&head2, 12); 
    push(&head2, 34); 
    push(&head2, 575); 
    push(&head2, 8); 
    push(&head2, 4); 
    push(&head2, 10); 

    // print list A 
    cout << "Given Linked List A: \n"; 
    printList(head1); 

    // print list B 
    cout << "Given Linked List B: \n"; 
    printList(head2); 

    // call function for count common node 
    int count = countCommonNodes(head1, head2); 

    // print number of common node in both list 
    cout << "Number of common node in both list is = " << count; 

    return 0; 
} 

```

## Java

```java

// Java implementation of above approach 
import java.util.*; 
class solution { 

    // static class of a linked list node 
    static class Node { 
        int data; 
        Node next; 
    } 

    // Function to common nodes which have 
    // same value node(s) both list 
    static int countCommonNodes(Node head1, Node head2) 
    { 
        // list  A 
        Node current1 = head1; 

        // list B 
        Node current2 = head2; 

        // set count  = 0 
        int count = 0; 

        // create vector 
        Vector<Integer> map = new Vector<Integer>(); 

        // traverse list A till the end of list 
        while (current1 != null) { 

            // insert list data in map 
            map.add(current1.data); 

            // increase current pointer of list A 
            current1 = current1.next; 
        } 

        while (current2 != null) { 

            // traverse list B till the end of list 
            // if data match then increase count 
            if (map.contains(current2.data)) 
                count++; 

            // increase current pointer of list B 
            current2 = current2.next; 
        } 

        // return count 
        return count; 
    } 

    /* Utility function to insert a node at the beginning */
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 

        return head_ref; 
    } 

    /* Utility function to print a linked list */
    static void printList(Node head) 
    { 
        while (head != null) { 
            System.out.print(head.data + " "); 
            head = head.next; 
        } 
        System.out.println(); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        Node head1 = null; 
        Node head2 = null; 

        /* Create following linked list  
    List A = 3 . 4 . 12 . 10 . 17 
   */

        head1 = push(head1, 17); 
        head1 = push(head1, 10); 
        head1 = push(head1, 12); 
        head1 = push(head1, 4); 
        head1 = push(head1, 3); 

        // List B = 10 . 4 . 8 . 575 . 34 . 12 
        head2 = push(head2, 12); 
        head2 = push(head2, 34); 
        head2 = push(head2, 575); 
        head2 = push(head2, 8); 
        head2 = push(head2, 4); 
        head2 = push(head2, 10); 

        // print list A 
        System.out.print("Given Linked List A: \n"); 
        printList(head1); 

        // print list B 
        System.out.print("Given Linked List B: \n"); 
        printList(head2); 

        // call function for count common node 
        int count = countCommonNodes(head1, head2); 

        // print number of common node in both list 
        System.out.print("Number of common node in both list is = " + count); 
    } 
} 
// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach 

# Structure of a linked list node 
class Node:  
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to common nodes which have 
# same value node(s) both list 
def countCommonNodes(head1, head2): 

    # List A 
    current1 = head1 

    # List B 
    current2 = head2 

    # Set count = 0 
    count = 0

    # Create unordered_set 
    map_=set() 

    # Traverse list A till the end of list 
    while (current1 != None) : 

        # Add list data in map_ 
        map_.add(current1.data) 

        # Increase current pointer of list A 
        current1 = current1.next

    while (current2 != None) : 

        # Traverse list B till the end of list 
        # if data match then increase count 
        if ((current2.data) in map_): 
            count = count + 1

        # Increase current pointer of list B 
        current2 = current2.next

    # Return count 
    return count 

# Utility function to add a node at the beginning  
def push(head_ref,new_data): 
    new_node = Node() 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return head_ref 

# Utility function to print a linked list 
def printList(head): 
    while (head != None) : 
        print(head.data, end = " ") 
        head = head.next

# Driver program to test above functions  
head1 = None
head2 = None

# Create following linked list  
# List A = 3 . 4 . 12 . 10 . 17 
head1 = push(head1, 17) 
head1 = push(head1, 10) 
head1 = push(head1, 12) 
head1 = push(head1, 4) 
head1 = push(head1, 3) 

# List B = 10 . 4 . 8 . 575 . 34 . 12 
head2 = push(head2, 12) 
head2 = push(head2, 34) 
head2 = push(head2, 575) 
head2 = push(head2, 8) 
head2 = push(head2, 4) 
head2 = push(head2, 10) 

# Print list A 
print("Given Linked List A: ") 
printList(head1) 

# Print list B 
print( "\nGiven Linked List B: ") 
printList(head2) 

# Call function for count common node 
count = countCommonNodes(head1, head2) 

# Print number of common node in both list 
print("\nNumber of common node in both list is = " , count) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of above approach 
using System; 
using System.Collections.Generic;  

class GFG 
{ 

    // static class of a linked list node 
    public class Node  
    { 
        public int data; 
        public Node next; 
    } 

    // Function to common nodes which have 
    // same value node(s) both list 
    static int countCommonNodes(Node head1, Node head2) 
    { 
        // list A 
        Node current1 = head1; 

        // list B 
        Node current2 = head2; 

        // set count = 0 
        int count = 0; 

        // create vector 
        List<int> map = new List<int>(); 

        // traverse list A till the end of list 
        while (current1 != null)  
        { 

            // insert list data in map 
            map.Add(current1.data); 

            // increase current pointer of list A 
            current1 = current1.next; 
        } 

        while (current2 != null)  
        { 

            // traverse list B till the end of list 
            // if data match then increase count 
            if (map.Contains(current2.data)) 
                count++; 

            // increase current pointer of list B 
            current2 = current2.next; 
        } 

        // return count 
        return count; 
    } 

    /* Utility function to insert a node at the beginning */
    static Node push(Node head_ref, int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 

        return head_ref; 
    } 

    /* Utility function to print a linked list */
    static void printList(Node head) 
    { 
        while (head != null)  
        { 
            Console.Write(head.data + " "); 
            head = head.next; 
        } 
        Console.WriteLine(); 
    } 

    /* Driver code */
    public static void Main(String []args) 
    { 
        Node head1 = null; 
        Node head2 = null; 

        /* Create following linked list  
    List A = 3 . 4 . 12 . 10 . 17 
*/

        head1 = push(head1, 17); 
        head1 = push(head1, 10); 
        head1 = push(head1, 12); 
        head1 = push(head1, 4); 
        head1 = push(head1, 3); 

        // List B = 10 . 4 . 8 . 575 . 34 . 12 
        head2 = push(head2, 12); 
        head2 = push(head2, 34); 
        head2 = push(head2, 575); 
        head2 = push(head2, 8); 
        head2 = push(head2, 4); 
        head2 = push(head2, 10); 

        // print list A 
        Console.Write("Given Linked List A: \n"); 
        printList(head1); 

        // print list B 
        Console.Write("Given Linked List B: \n"); 
        printList(head2); 

        // call function for count common node 
        int count = countCommonNodes(head1, head2); 

        // print number of common node in both list 
        Console.Write("Number of common node in both list is = " + count); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Given Linked List A: 
3 4 12 10 17 
Given Linked List B: 
10 4 8 575 34 12 
Number of common node in both list is = 3

```

**时间复杂度：** O（N）

**空间复杂度：** O（N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。