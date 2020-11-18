# 链表中最长的子列表

给定一个单链表，我们要计算不断增加的元素并打印出不断增加的链表。

**示例：**

```
Input  : 8 -> 5 -> 7 -> 10 -> 9 -> 11 -> 12 -> 13 -> NULL
Output : Number of continuously increasing elements = 4      
         Increasing linked list : 9 11 12 13

Input : 5 -> 12 -> 18 -> 7 -> 12 -> 15 -> NULL
Output : Number of continuously increasing elements = 3
         Increasing linked list = 5 12 18

```

这个想法是遍历单链表，并比较curr-> data和curr-> next-> data，其中curr是要遍历的当前节点。 如果curr-> data较小，则curr-> next-> data则curr指针指向curr-> next，并将长度（连续增加的元素）加1。 如果条件为假，则将长度与max进行比较，如果max小于len，则将len值分配给max。 继续此过程，直到head不等于NULL。 还要找到连续增加元素的起始指标。 接下来遍历链表，并在链表中显示连续增加的元素。

## C++

```cpp

// Program to count maximum number of continuous 
// increasing element in linked list and display 
// the elements of linked list. 
#include <bits/stdc++.h> 
using namespace std; 

struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function that count maximum number of continuous 
// increasing elements in linked list and display 
// the list. 
void countIncreasingElements(struct Node *head) 
{ 
    // Traverse the list and keep track of max increasing 
    // and current increasing lengths 
    int curr_len = 1, max_len = 1; 
    int total_count = 1, res_index = 0; 
    for (Node *curr=head; curr->next!=NULL; curr=curr->next) 
    { 
        // Compare head->data with head->next->data 
        if (curr->data < curr->next->data) 
            curr_len++; 
        else
        { 
            // compare maximum length with len. 
            if (max_len < curr_len) 
            { 
                max_len = curr_len; 
                res_index = total_count - curr_len; 
            } 

            curr_len = 1; 
        } 
        total_count++; 
    } 

    if (max_len < curr_len) 
    { 
        max_len = curr_len; 
        res_index = total_count - max_len; 
    } 

    // Print the maximum number of continuous elements 
    // in linked list. 
    cout << "Number of continuously increasing element"
            " in list : "; 
    cout << max_len << endl; 

    // Traverse the list again to print longest increasing 
    // sublist 
    int i = 0; 
    cout << "Increasing linked list" << endl; 
    for (Node* curr=head; curr!=NULL; curr=curr->next) 
    { 
        // compare with starting index and index of 
        // maximum increasing elements if both are 
        // equals then execute it. 
        if (i == res_index) 
        { 
            // loop until max greater then 0\. 
            while (max_len > 0) 
            { 
                // Display the list and temp point 
                // to the next element. 
                cout << curr->data << " "; 
                curr = curr->next; 
                max_len--; 
            } 
            break; 
        } 

        i++; 
    } 
} 

// Function to insert an element at the beginning 
void push(struct Node** head, int data) 
{ 
    struct Node* newNode = new Node; 
    newNode->data = data; 
    newNode->next = (*head); 
    (*head) = newNode; 
} 

// Display linked list. 
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
    cout << endl; 
} 

// Driver functions 
int main() 
{ 
    // Create a node and initialize with NULL 
    struct Node* head = NULL; 

    // push() insert node in linked list. 
    // 15 -> 18 -> 5 -> 8 -> 11 -> 12 
    push(&head, 12); 
    push(&head, 11); 
    push(&head, 8); 
    push(&head, 5); 
    push(&head, 18); 
    push(&head, 15); 
    cout << "Linked list:" << endl; 
    printList(head); 

    // Function call countIncreasingElements(head) 
   // cout << countIncreasingElements(head) << endl; 
    countIncreasingElements(head); 
    return 0; 
} 

```

## Java

```java

// A Java Program to count maximum number  
// of continuous increasing element in 
// linked list and display the elements 
// of linked list. 
import java.util.*; 
class GFG  
{  
static class Node  
{ 
    int data; 
    Node next; 
} 
static Node head; 

// Function that count maximum number  
// of continuous increasing elements  
// in linked list and display the list. 
static void countIncreasingElements(Node head) 
{ 
    // Traverse the list and keep track  
    // of max increasing and 
    // current increasing lengths 
    int curr_len = 1, max_len = 1; 
    int total_count = 1, res_index = 0; 
    for (Node curr = head; curr.next != null;  
                           curr = curr.next) 
    { 
        // Compare head.data with head.next.data 
        if (curr.data < curr.next.data) 
            curr_len++; 
        else
        { 
            // compare maximum length with len. 
            if (max_len < curr_len) 
            { 
                max_len = curr_len; 
                res_index = total_count - curr_len; 
            } 

            curr_len = 1; 
        } 
        total_count++; 
    } 

    if (max_len < curr_len) 
    { 
        max_len = curr_len; 
        res_index = total_count - max_len; 
    } 

    // Print the maximum number of  
    // continuous elements in linked list. 
    System.out.print("Number of continuously " + 
                     "increasing element in list : "); 
    System.out.println(max_len); 

    // Traverse the list again to print  
    // longest increasing sublist 
    int i = 0; 
    System.out.println("Increasing linked list"); 
    for (Node curr = head; curr != null;  
                           curr = curr.next) 
    { 
        // compare with starting index and index of 
        // maximum increasing elements if both are 
        // equals then execute it. 
        if (i == res_index) 
        { 
            // loop until max greater then 0\. 
            while (max_len > 0) 
            { 
                // Display the list and temp point 
                // to the next element. 
                System.out.print(curr.data + " "); 
                curr = curr.next; 
                max_len--; 
            } 
            break; 
        } 
        i++; 
    } 
} 

// Function to insert an element at the beginning 
static void push(Node head_ref, int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = head_ref; 
    head_ref = newNode; 
    head = head_ref; 
} 

// Display linked list. 
static void printList(Node node) 
{ 
    while (node != null)  
    { 
        System.out.print(node.data + " "); 
        node = node.next; 
    } 
    System.out.println(); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    // Create a node and initialize with null 
    head = null; 

    // push() insert node in linked list. 
    // 15 -> 18 -> 5 -> 8 -> 11 -> 12 
    push(head, 12); 
    push(head, 11); 
    push(head, 8); 
    push(head, 5); 
    push(head, 18); 
    push(head, 15); 
    System.out.println("Linked list:"); 
    printList(head); 

    // Function call countIncreasingElements(head) 
    countIncreasingElements(head); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Program to count maximum number of continuous  
# increasing element in linked list and display  
# the elements of linked list.  
import math 

class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Function that count maximum number of continuous  
# increasing elements in linked list and display  
# the list.  
def countIncreasingElements(head):  

    # Traverse the list and keep track of  
    # max increasing and current increasing lengths  
    curr_len = 1
    max_len = 1
    total_count = 1
    res_index = 0
    curr = head  
    while(curr.next != None):  

        # Compare head.data with head.next.data  
        if (curr.data < curr.next.data):  
            curr_len = curr_len + 1
        else:  

            # compare maximum length with len.  
            if (max_len < curr_len):  
                max_len = curr_len  
                res_index = total_count - curr_len  

            curr_len = 1

        total_count = total_count + 1
        curr = curr.next

    if (max_len < curr_len):  
        max_len = curr_len  
        res_index = total_count - max_len  

    # Print the maximum number of  
    # continuous elements in linked list.  
    print("Number of continuously increasing",  
               "element in list : ", end = "")  
    print(max_len)  

    # Traverse the list again to print  
    # longest increasing sublist  
    i = 0
    print("Increasing linked list")  
    curr = head 
    while(curr != None):  

        # compare with starting index and index of  
        # maximum increasing elements if both are  
        # equals then execute it.  
        if (i == res_index):  

            # loop until max greater then 0.  
            while (max_len > 0): 

                # Display the list and temp point  
                # to the next element.  
                print(curr.data, end = " ") 
                curr = curr.next
                max_len = max_len - 1

            break

        i = i + 1
        curr = curr.next

# Function to insert an element 
# at the beginning  
def push(head, data):  
    newNode = Node(data)  
    newNode.data = data  
    newNode.next = head 
    head = newNode  
    return head 

# Display linked list.  
def printList(node) :  
    while (node != None):  
        print(node.data, end = " ") 
        node = node.next

    print()  

# Driver Code 
if __name__=='__main__':  

    # Create a node and initialize with None  
    head = None

    # push() insert node in linked list.  
    # 15 . 18 . 5 . 8 . 11 . 12  
    head = push(head, 12)  
    head = push(head, 11)  
    head = push(head, 8)  
    head = push(head, 5)  
    head = push(head, 18)  
    head = push(head, 15)  
    print("Linked list:")  
    printList(head)  

    # Function call countIncreasingElements(head)  
    countIncreasingElements(head)  

# This code is contributed by Srathore 

```

## C#

```cs

// C# Program to count maximum number  
// of continuous increasing element in 
// linked list and display the elements 
// of linked list. 
using System; 

class GFG  
{  
class Node  
{ 
    public int data; 
    public Node next; 
} 
static Node head; 

// Function that count maximum number  
// of continuous increasing elements  
// in linked list and display the list. 
static void countIncreasingElements(Node head) 
{ 
    // Traverse the list and keep track  
    // of max increasing and 
    // current increasing lengths 
    int curr_len = 1, max_len = 1; 
    int total_count = 1, res_index = 0; 
    for (Node curr = head; curr.next != null;  
                           curr = curr.next) 
    { 
        // Compare head.data with head.next.data 
        if (curr.data < curr.next.data) 
            curr_len++; 
        else
        { 
            // compare maximum length with len. 
            if (max_len < curr_len) 
            { 
                max_len = curr_len; 
                res_index = total_count - curr_len; 
            } 

            curr_len = 1; 
        } 
        total_count++; 
    } 

    if (max_len < curr_len) 
    { 
        max_len = curr_len; 
        res_index = total_count - max_len; 
    } 

    // Print the maximum number of  
    // continuous elements in linked list. 
    Console.Write("Number of continuously " + 
                  "increasing element in list : "); 
    Console.WriteLine(max_len); 

    // Traverse the list again to print  
    // longest increasing sublist 
    int i = 0; 
    Console.WriteLine("Increasing linked list"); 
    for (Node curr = head; curr != null;  
                           curr = curr.next) 
    { 
        // compare with starting index and index of 
        // maximum increasing elements if both are 
        // equals then execute it. 
        if (i == res_index) 
        { 
            // loop until max greater then 0\. 
            while (max_len > 0) 
            { 
                // Display the list and temp point 
                // to the next element. 
                Console.Write(curr.data + " "); 
                curr = curr.next; 
                max_len--; 
            } 
            break; 
        } 
        i++; 
    } 
} 

// Function to insert an element at the beginning 
static void push(Node head_ref, int data) 
{ 
    Node newNode = new Node(); 
    newNode.data = data; 
    newNode.next = head_ref; 
    head_ref = newNode; 
    head = head_ref; 
} 

// Display linked list. 
static void printList(Node node) 
{ 
    while (node != null)  
    { 
        Console.Write(node.data + " "); 
        node = node.next; 
    } 
    Console.WriteLine(); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    // Create a node and initialize with null 
    head = null; 

    // push() insert node in linked list. 
    // 15 -> 18 -> 5 -> 8 -> 11 -> 12 
    push(head, 12); 
    push(head, 11); 
    push(head, 8); 
    push(head, 5); 
    push(head, 18); 
    push(head, 15); 
    Console.WriteLine("Linked list:"); 
    printList(head); 

    // Function call countIncreasingElements(head) 
    countIncreasingElements(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出：**

```
Linked list:
15 18 5 8 11 12 
Number of continuously increasing element in list :4
Increasing linked list
5 8 11 12

```

本文由 [**Dharmendra kumar**](https://auth.geeksforgeeks.org/profile.php?user=dharammnnit&list=practice) 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

